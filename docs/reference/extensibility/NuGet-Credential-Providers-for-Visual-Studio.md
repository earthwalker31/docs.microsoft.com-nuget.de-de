---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: Nuget-Anmelde Informationsanbieter authentifizieren sich mit Feeds, indem die ivscredentialprovider-Schnittstelle in einer Visual Studio-Erweiterung implementiert wird.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 13b6f5abe93a17c809564265990f86f6780aa67e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230810"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Authentifizieren von Feeds in Visual Studio mit nuget-Anmelde Informationsanbietern

Die nuget Visual Studio-Erweiterung 3.6 und höher unterstützt Anmelde Informationsanbieter, mit denen nuget mit authentifizierten Feeds arbeiten kann.
Nachdem Sie einen nuget-Anmelde Informationsanbieter für Visual Studio installiert haben, werden die Anmelde Informationen für authentifizierte Feeds von der nuget-Erweiterung für Visual Studio nach Bedarf automatisch abgerufen und aktualisiert.

Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

In Visual Studio verwendet nuget einen internen `VsCredentialProviderImporter`, der auch nach Plug-in-Anmelde Informationsanbietern sucht. Diese Plug-in-Anmelde Informationsanbieter müssen als MEF-Export vom Typ `IVsCredentialProvider`erkennbar sein.

Ab 4.8 + nuget in Visual Studio unterstützt auch die neuen plattformübergreifenden Authentifizierungs-Plug-ins, aber Sie sind aus Leistungsgründen nicht empfehlenswert.

> [!Note]
> Nuget-Anmelde Informationsanbieter für Visual Studio müssen als reguläre Visual Studio-Erweiterung installiert sein und benötigen [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.
>
> Nuget-Anmelde Informationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht in dotnet Restore oder nuget. exe). Informationen zu Anmelde Informationsanbietern mit nuget. exe finden [Sie unter nuget. exe](nuget-exe-Credential-providers.md)-Anmelde Informationsanbieter.
> Informationen zu Anmelde Informationsanbietern in dotnet und MSBuild finden [Sie unter nuget-plattformübergreifende](nuget-cross-platform-authentication-plugin.md) Plug-ins

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Erstellen eines nuget-Anmelde Informationsanbieters für Visual Studio

Die nuget Visual Studio-Erweiterung 3.6 + implementiert einen internen "dedentialservice", der zum Abrufen von Anmelde Informationen verwendet wird. Der Dienst "eigene Anmelde Informationen" enthält eine Liste integrierter und Plug-in-Anmelde Informationsanbieter. Jeder Anbieter wird sequenziell ausprobiert, bis Anmelde Informationen abgerufen werden.

Beim Erwerb der Anmelde Informationen versucht der Anmelde Informationsdienst, Anmelde Informationsanbieter in der folgenden Reihenfolge zu verwenden, und wird beendet, sobald Anmelde Informationen abgerufen werden:

1. Anmelde Informationen werden aus den nuget-Konfigurationsdateien abgerufen (mithilfe der integrierten `SettingsCredentialProvider`).
1. Wenn sich die Paketquelle auf Visual Studio Team Services befindet, wird die `VisualStudioAccountProvider` verwendet.
1. Alle anderen Plug-in-Anmelde Informationsanbieter für Visual Studio werden nacheinander ausprobiert.
1. Versuchen Sie, alle nuget-plattformübergreifenden Anmelde Informationsanbieter sequenziell zu verwenden.
1. Wenn noch keine Anmelde Informationen abgerufen wurden, wird der Benutzer über ein Standardmäßiges Standard Authentifizierungs Dialogfeld zur Eingabe von Anmelde Informationen aufgefordert.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementieren von ivscredentialprovider. getkredentialsasync

Um einen nuget-Anmelde Informationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export verfügbar macht, der den `IVsCredentialProvider` Typ implementiert, und den unten beschriebenen Prinzipien entspricht.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Jeder nuget-Anmelde Informationsanbieter für Visual Studio muss folgende Aktionen ausführen:

1. Bestimmen Sie, ob die Anmelde Informationen für den Ziel-URI vor dem Initiieren der Anmelde Informationen bereitgestellt werden können. Wenn der Anbieter keine Anmelde Informationen für die Ziel Quelle angeben kann, sollte er `null`zurückgeben.
1. Wenn der Anbieter Anforderungen für den Ziel-URI verarbeitet, aber keine Anmelde Informationen angeben kann, sollte eine Ausnahme ausgelöst werden.

Ein benutzerdefinierter nuget-Anmelde Informationsanbieter für Visual Studio muss die `IVsCredentialProvider`-Schnittstelle implementieren, die im [nuget. VisualStudio-Paket](https://www.nuget.org/packages/NuGet.VisualStudio/)verfügbar ist.

#### <a name="getcredentialasync"></a>Getkredentialasync

| Eingabeparameter |BESCHREIBUNG|
| ----------------|-----------|
| URI-URI | Der Paketquellen-URI, für den Anmelde Informationen angefordert werden.|
| IWebProxy-Proxy | Der WebProxy, der für die Kommunikation im Netzwerk verwendet werden soll. NULL, wenn keine Proxy Authentifizierung konfiguriert ist. |
| bool isproxyrequest | True, wenn die Anforderung besteht, Anmelde Informationen für die Proxy Authentifizierung zu erhalten. Wenn die Implementierung für den Erwerb von Proxy Anmelde Informationen nicht gültig ist, sollte NULL zurückgegeben werden. |
| Boolescher isretry | True, wenn zuvor Anmelde Informationen für diesen URI angefordert wurden, die angegebenen Anmelde Informationen aber keinen autorisierten Zugriff hatten. |
| bool nicht interaktiv | True gibt an, dass der Anmelde Informationsanbieter alle Benutzer Aufforderungen unterdrücken und stattdessen Standardwerte verwenden muss. |
| CancellationToken CancellationToken | Dieses Abbruch Token sollte geprüft werden, um zu bestimmen, ob der Vorgang zum Anfordern von Anmelde Informationen abgebrochen wurde. |

**Rückgabewert**: ein Anmelde Informationsobjekt, das die [`System.Net.ICredentials`-Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0)implementiert.
