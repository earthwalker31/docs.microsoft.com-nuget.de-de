---
title: Befehl "nuget CLI Push"
description: Referenz für den Befehl "nuget. exe Push"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327627"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="f6f5a-103">Push-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="f6f5a-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="f6f5a-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle; 4.1.0 + erforderlich für nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6f5a-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="f6f5a-105">Um Pakete per Push an nuget.org zu überführen, müssen Sie "nuget. exe v 4.1.0 +" verwenden, das die erforderlichen [nuget-Protokolle](../../api/nuget-protocols.md)implementiert.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="f6f5a-106">Überträgt ein Paket an eine Paketquelle und veröffentlicht es.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="f6f5a-107">Die nuget-Standardkonfiguration wird durch Laden `%AppData%\NuGet\NuGet.Config` von (Windows) `~/.nuget/NuGet/NuGet.Config` oder (Mac/Linux) abgerufen, und `Nuget.Config` anschließend `.nuget\Nuget.Config` werden alle-Dateien oder-Dateien gestartet, die vom Stamm des Laufwerks stammen und im aktuellen Verzeichnis enden (siehe [Common nuget). Konfigurationen](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="f6f5a-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="f6f5a-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="f6f5a-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="f6f5a-109">gibt `<packagePath>` an, wo das Paket angibt, das per Push an den Server über</span><span class="sxs-lookup"><span data-stu-id="f6f5a-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="f6f5a-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="f6f5a-110">Options</span></span>

| <span data-ttu-id="f6f5a-111">Option</span><span class="sxs-lookup"><span data-stu-id="f6f5a-111">Option</span></span> | <span data-ttu-id="f6f5a-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f6f5a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6f5a-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="f6f5a-113">ApiKey</span></span> | <span data-ttu-id="f6f5a-114">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-114">The API key for the target repository.</span></span> <span data-ttu-id="f6f5a-115">Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f6f5a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f6f5a-116">ConfigFile</span></span> | <span data-ttu-id="f6f5a-117">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f6f5a-118">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f6f5a-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="f6f5a-119">DisableBuffering</span></span> | <span data-ttu-id="f6f5a-120">Deaktiviert die Pufferung beim Push an einen HTTP (s)-Server, um Speicher Verwendungen zu verringern.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="f6f5a-121">Vorsicht: Wenn diese Option verwendet wird, funktioniert die integrierte Windows-Authentifizierung möglicherweise nicht.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="f6f5a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f6f5a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="f6f5a-123">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f6f5a-124">Help</span><span class="sxs-lookup"><span data-stu-id="f6f5a-124">Help</span></span> | <span data-ttu-id="f6f5a-125">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="f6f5a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f6f5a-126">NonInteractive</span></span> | <span data-ttu-id="f6f5a-127">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f6f5a-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="f6f5a-128">NoSymbols</span></span> | <span data-ttu-id="f6f5a-129">*(3.5* und höher) Wenn ein Symbol Paket vorhanden ist, wird es nicht auf einen Symbol Server übermittelt.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="f6f5a-130">Source</span><span class="sxs-lookup"><span data-stu-id="f6f5a-130">Source</span></span> | <span data-ttu-id="f6f5a-131">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-131">Specifies the server URL.</span></span> <span data-ttu-id="f6f5a-132">Nuget identifiziert eine UNC-oder lokale Ordner Quelle und kopiert die Datei dort, anstatt Sie per HTTP zu pushen.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="f6f5a-133">Ab nuget 3.4.2 handelt es sich hierbei um einen obligatorischen Parameter, es sei `NuGet.Config` denn, die Datei gibt einen *defaultpushsource* -Wert an (Weitere Informationen finden Sie unter [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="f6f5a-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="f6f5a-134">Überspringen</span><span class="sxs-lookup"><span data-stu-id="f6f5a-134">SkipDuplicate</span></span> | <span data-ttu-id="f6f5a-135">*(5.1 +)* Wenn ein Paket und eine Version bereits vorhanden sind, überspringen Sie es, und fahren Sie mit dem nächsten Paket im Push fort, falls vorhanden.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="f6f5a-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="f6f5a-136">SymbolSource</span></span> | <span data-ttu-id="f6f5a-137">*(3.5* und höher) Gibt die Symbol Server-URL an. nuget.smbsrc.net wird beim Push an nuget.org verwendet.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="f6f5a-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="f6f5a-138">SymbolApiKey</span></span> | <span data-ttu-id="f6f5a-139">*(3.5* und höher) Gibt den API-Schlüssel für die URL an `-SymbolSource`, die in angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="f6f5a-140">Timeout</span><span class="sxs-lookup"><span data-stu-id="f6f5a-140">Timeout</span></span> | <span data-ttu-id="f6f5a-141">Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="f6f5a-142">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="f6f5a-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="f6f5a-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f6f5a-143">Verbosity</span></span> | <span data-ttu-id="f6f5a-144">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="f6f5a-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f6f5a-145">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f6f5a-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f6f5a-146">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f6f5a-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```