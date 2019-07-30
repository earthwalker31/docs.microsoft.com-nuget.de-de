---
title: Befehl "nuget CLI config"
description: Referenz für den Befehl "nuget. exe config"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433320"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="19711-103">config-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="19711-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="19711-104">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="19711-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="19711-105">Ruft nuget-Konfigurationswerte ab oder legt Sie fest.</span><span class="sxs-lookup"><span data-stu-id="19711-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="19711-106">Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="19711-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="19711-107">Ausführliche Informationen zu zulässigen Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="19711-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="19711-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="19711-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="19711-109">`<name>` dabeigebenSieeinSchlüssel-Wert-Paaran,dasinderKonfiguration`<value>` festgelegt werden soll.</span><span class="sxs-lookup"><span data-stu-id="19711-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="19711-110">Sie können beliebig viele Paare angeben.</span><span class="sxs-lookup"><span data-stu-id="19711-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="19711-111">Um einen Wert zu entfernen, geben Sie den Namen `=` und das Vorzeichen an, aber keinen Wert.</span><span class="sxs-lookup"><span data-stu-id="19711-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="19711-112">Zulässige Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="19711-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="19711-113">In nuget 3.4 und `<value>` höher kann [Umgebungsvariablen](cli-ref-environment-variables.md)verwenden.</span><span class="sxs-lookup"><span data-stu-id="19711-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="19711-114">Optionen</span><span class="sxs-lookup"><span data-stu-id="19711-114">Options</span></span>

| <span data-ttu-id="19711-115">Option</span><span class="sxs-lookup"><span data-stu-id="19711-115">Option</span></span> | <span data-ttu-id="19711-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="19711-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19711-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="19711-117">AsPath</span></span> | <span data-ttu-id="19711-118">Gibt den Konfigurations Wert als Pfad zurück, der ignoriert `-Set` wird, wenn verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="19711-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="19711-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="19711-119">ConfigFile</span></span> | <span data-ttu-id="19711-120">Die zu ändernde nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="19711-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="19711-121">Wenn nichts angegeben ist, wird die Standarddatei verwendet`%AppData%\NuGet\NuGet.Config` : (Windows) `~/.config/NuGet/NuGet.Config` oder (Mac/Linux) `~/.nuget/NuGet/NuGet.Config` oder (variiert je nach Betriebssystem Verteilung).</span><span class="sxs-lookup"><span data-stu-id="19711-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="19711-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="19711-122">ForceEnglishOutput</span></span> | <span data-ttu-id="19711-123">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="19711-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="19711-124">Help</span><span class="sxs-lookup"><span data-stu-id="19711-124">Help</span></span> | <span data-ttu-id="19711-125">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="19711-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="19711-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="19711-126">NonInteractive</span></span> | <span data-ttu-id="19711-127">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="19711-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="19711-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="19711-128">Verbosity</span></span> | <span data-ttu-id="19711-129">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="19711-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="19711-130">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="19711-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="19711-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="19711-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```