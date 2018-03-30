---
title: Konfigurieren des NuGet-Verhaltens | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Config-Dateien steuern das Verhalten von NuGet global und auf Projektebene und werden mit dem Befehl „nuget config“ bearbeitet."
keywords: "NuGet-Konfigurationsdateien, NuGet-Konfiguration, Einstellungen für das NuGet-Verhalten, NuGet-Einstellungen, NuGet.Config, NuGetDefaults.Config, Standardeinstellungen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c46f23fcbec5dfcb6122434d43097212f6230fb0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="5e99f-104">Konfigurieren des NuGet-Verhaltens</span><span class="sxs-lookup"><span data-stu-id="5e99f-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="5e99f-105">Das Verhalten von NuGet wird durch die Eigenschaften gesteuert, die in einer oder mehreren `NuGet.Config`-Dateien (XML) gesammelt sind, die auf Projekt-, Benutzer- oder Computerebene vorhanden sein kann.</span><span class="sxs-lookup"><span data-stu-id="5e99f-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="5e99f-106">Eine globale `NuGetDefaults.Config`-Datei konfiguriert insbesondere Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-106">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="5e99f-107">Die Einstellungen gelten für alle Befehle, die in der CLI, der Konsole oder der Benutzeroberfläche des Paket-Managers ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="5e99f-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="5e99f-108">Speicherorte und Verwendungsmöglichkeiten von Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="5e99f-108">Config file locations and uses</span></span>

| <span data-ttu-id="5e99f-109">Bereich</span><span class="sxs-lookup"><span data-stu-id="5e99f-109">Scope</span></span> | <span data-ttu-id="5e99f-110">Speicherort der NuGet.Config-Datei</span><span class="sxs-lookup"><span data-stu-id="5e99f-110">NuGet.Config file location</span></span> | <span data-ttu-id="5e99f-111">description</span><span class="sxs-lookup"><span data-stu-id="5e99f-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e99f-112">Projekt</span><span class="sxs-lookup"><span data-stu-id="5e99f-112">Project</span></span> | <span data-ttu-id="5e99f-113">Aktueller Ordner (bzw. Projektordner) oder ein beliebiger anderer Ordner im Stammlaufwerk.</span><span class="sxs-lookup"><span data-stu-id="5e99f-113">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="5e99f-114">Die Einstellungen in einem Projektordner gelten nur für dieses Projekt.</span><span class="sxs-lookup"><span data-stu-id="5e99f-114">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="5e99f-115">Die Einstellungen in einem übergeordneten Ordner, der mehrere Unterordner mit Projekten enthält, gelten für alle Projekte in diesen Unterordnern.</span><span class="sxs-lookup"><span data-stu-id="5e99f-115">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="5e99f-116">Benutzer</span><span class="sxs-lookup"><span data-stu-id="5e99f-116">User</span></span> | <span data-ttu-id="5e99f-117">Windows: `%APPDATA%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="5e99f-117">Windows: `%APPDATA%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="5e99f-118">Mac/Linux: `~/.nuget/NuGet/NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="5e99f-118">Mac/Linux: `~/.nuget/NuGet/NuGet.Config`</span></span> | <span data-ttu-id="5e99f-119">Die Einstellungen gelten für alle Vorgänge, werden jedoch durch sämtliche Einstellungen auf Projektebene überschrieben.</span><span class="sxs-lookup"><span data-stu-id="5e99f-119">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="5e99f-120">Computer</span><span class="sxs-lookup"><span data-stu-id="5e99f-120">Computer</span></span> | <span data-ttu-id="5e99f-121">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="5e99f-121">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="5e99f-122">Mac/Linux: `$XDG_DATA_HOME` (in der Regel `~/.local/share`)</span><span class="sxs-lookup"><span data-stu-id="5e99f-122">Mac/Linux: `$XDG_DATA_HOME` (typically `~/.local/share`)</span></span> | <span data-ttu-id="5e99f-123">Die Einstellungen gelten für alle Vorgänge auf dem Computer, werden jedoch durch sämtliche Einstellungen auf Benutzer- oder Projektebene überschrieben.</span><span class="sxs-lookup"><span data-stu-id="5e99f-123">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="5e99f-124">Hinweise für frühere Versionen von NuGet:</span><span class="sxs-lookup"><span data-stu-id="5e99f-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="5e99f-125">In NuGet 3.3 und früher wurde ein `.nuget`-Ordner für projektmappenweite Einstellungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="5e99f-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="5e99f-126">Diese Datei wird nicht in NuGet 3.4 oder höher verwendet.</span><span class="sxs-lookup"><span data-stu-id="5e99f-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="5e99f-127">Bei NuGet 2.6 bis 3.x unter Windows befindet sich die Konfigurationsdatei auf Computerebene unter %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config. Hierbei kann *{IDE}* z.B. für *Visual Studio* stehen, *{Version}* stellt die Version von Visual Studio dar, z.B. *14.0*, und *{SKU}* steht für *Community*, *Professional* oder *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="5e99f-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="5e99f-128">Kopieren Sie die Konfigurationsdatei in %ProgramFiles(x86)%\NuGet\Config, um Einstellungen zu NuGet 4.0 und höher zu migrieren. Unter Linux war der Speicherort zuvor /etc/opt, unter Mac /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="5e99f-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="5e99f-129">Ändern von Konfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="5e99f-129">Changing config settings</span></span>

<span data-ttu-id="5e99f-130">Bei einer `NuGet.Config`-Datei handelt es sich um eine einfache XML-Textdatei, die wie im Artikel [NuGet Configuration Settings (NuGet-Konfigurationseinstellungen)](../reference/nuget-config-file.md) beschrieben Schlüssel/Wert-Paare enthält.</span><span class="sxs-lookup"><span data-stu-id="5e99f-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="5e99f-131">Einstellungen werden mithilfe des NuGet-CLI-Befehls [config](../tools/cli-ref-config.md) verwaltet:</span><span class="sxs-lookup"><span data-stu-id="5e99f-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="5e99f-132">Standardmäßig werden Änderungen an der Konfigurationsdatei auf Benutzerebene vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="5e99f-133">Verwenden Sie den `-configFile`-Parameter, um die Einstellungen in einer anderen Datei zu ändern.</span><span class="sxs-lookup"><span data-stu-id="5e99f-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="5e99f-134">In diesem Fall kann ein beliebiger Dateiname für Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5e99f-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="5e99f-135">Bei Schlüsseln wird die Groß-/Kleinschreibung immer beachtet.</span><span class="sxs-lookup"><span data-stu-id="5e99f-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="5e99f-136">Es ist eine Erhöhung der Rechte erforderlich, um die Einstellungen in der Einstellungsdatei auf Computerebene zu ändern.</span><span class="sxs-lookup"><span data-stu-id="5e99f-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="5e99f-137">Sie können die Datei zwar in jedem Text-Editor bearbeiten, NuGet (3.4.3 und höher) ignoriert jedoch die gesamte Konfigurationsdatei, wenn diese falsche XML-Formatierungen (nicht übereinstimmende Tags, ungültige Anführungszeichen usw.) enthält.</span><span class="sxs-lookup"><span data-stu-id="5e99f-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="5e99f-138">Deshalb wird empfohlen, Einstellungen mithilfe von `nuget config` zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="5e99f-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="5e99f-139">Festlegen eines Werts</span><span class="sxs-lookup"><span data-stu-id="5e99f-139">Setting a value</span></span>

<span data-ttu-id="5e99f-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="5e99f-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="5e99f-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="5e99f-141">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="5e99f-142">In NuGet 3.4 und höher können Sie Umgebungsvariablen in jedem Wert verwenden, z.B. in `repositoryPath=%PACKAGEHOME%` (Windows) oder `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5e99f-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="5e99f-143">Entfernen eines Werts</span><span class="sxs-lookup"><span data-stu-id="5e99f-143">Removing a value</span></span>

<span data-ttu-id="5e99f-144">Geben Sie einen Schlüssel mit einem leeren Wert an, um einen Wert zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="5e99f-145">Erstellen einer neuen Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="5e99f-145">Creating a new config file</span></span>

<span data-ttu-id="5e99f-146">Kopieren Sie die unten aufgeführte Vorlage in die neue Datei, und verwenden Sie dann `nuget config --configFile <filename>`, um Werte festzulegen:</span><span class="sxs-lookup"><span data-stu-id="5e99f-146">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="5e99f-147">Anwenden der Einstellungen</span><span class="sxs-lookup"><span data-stu-id="5e99f-147">How settings are applied</span></span>

<span data-ttu-id="5e99f-148">Durch mehrere `NuGet.Config`-Dateien können Sie Einstellungen an verschiedenen Orten speichern, sodass diese entweder für ein einzelnes Projekt, für mehrere Projekte oder für alle Projekte gelten.</span><span class="sxs-lookup"><span data-stu-id="5e99f-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="5e99f-149">Diese Einstellungen gelten zusammen für jeden NuGet-Vorgang, der über die Befehlszeile oder über Visual Studio ausgeführt wird. Hierbei haben die Einstellungen Vorrang, die dem Projekt oder dem aktuellen Ordner am „nächsten“ liegen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="5e99f-150">NuGet lädt Einstellungen aus verschiedenen Konfigurationsdateien in folgender Reihenfolge:</span><span class="sxs-lookup"><span data-stu-id="5e99f-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="5e99f-151">Die [NuGetDefaults.Config-Datei](#nuget-defaults-file), die ausschließlich Einstellungen für die Paketquellen enthält.</span><span class="sxs-lookup"><span data-stu-id="5e99f-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="5e99f-152">Die Datei auf Computerebene.</span><span class="sxs-lookup"><span data-stu-id="5e99f-152">The computer-level file.</span></span>
1. <span data-ttu-id="5e99f-153">Die Datei auf Benutzerebene.</span><span class="sxs-lookup"><span data-stu-id="5e99f-153">The user-level file.</span></span>
1. <span data-ttu-id="5e99f-154">Die Datei, die mit `-configFile` angegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="5e99f-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="5e99f-155">Dateien, die vom Stamm des Laufwerks bis zum aktuellen Ordner (in dem „nuget.exe“ ausgeführt wird oder der das Visual Studio-Projekt enthält) in jedem Ordner im Pfad gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="5e99f-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="5e99f-156">Wenn beispielsweise ein Befehl in c:\A\B\C aufgerufen wird, sucht NuGet nach Konfigurationsdateien in c:\,, dann in c:\A\B und schließlich in c:\A\B\C und lädt diese anschließend.</span><span class="sxs-lookup"><span data-stu-id="5e99f-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="5e99f-157">Wenn NuGet Einstellungen in diesen Dateien vorfindet, werden diese folgendermaßen angewendet:</span><span class="sxs-lookup"><span data-stu-id="5e99f-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="5e99f-158">Für einzelne Elemente ersetzt NuGet jeden zuvor gefundenen Wert mit demselben Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="5e99f-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="5e99f-159">Das bedeutet, dass die Einstellungen, die dem aktuellen Ordner oder Projekt „am nächsten“ liegen die zuvor gefundenen überschreiben.</span><span class="sxs-lookup"><span data-stu-id="5e99f-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="5e99f-160">Die `defaultPushSource`-Einstellung in `NuGetDefaults.Config` wird beispielsweise überschrieben, wenn diese in einer anderen Konfigurationsdatei vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="5e99f-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="5e99f-161">Bei Auflistungselementen (z.B. `<packageSources>`) kombiniert NuGet die Werte aller Konfigurationsdateien zu einer einzelnen Auflistung.</span><span class="sxs-lookup"><span data-stu-id="5e99f-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="5e99f-162">Wenn `<clear />` für einen bestimmten Knoten vorhanden ist, ignoriert NuGet die zuvor definierten Konfigurationswerte für diesen Knoten.</span><span class="sxs-lookup"><span data-stu-id="5e99f-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="5e99f-163">Exemplarische Vorgehensweise: Einstellungen</span><span class="sxs-lookup"><span data-stu-id="5e99f-163">Settings walkthrough</span></span>

<span data-ttu-id="5e99f-164">Nehmen wir an, dass Sie über folgende Ordnerstruktur auf zwei separaten Laufwerken verfügen:</span><span class="sxs-lookup"><span data-stu-id="5e99f-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="5e99f-165">Sie verfügen dann über vier `NuGet.Config`-Dateien an folgenden Speicherorten mit dem angegebenen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="5e99f-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="5e99f-166">(Die Datei auf Computerebene ist in diesem Beispiel nicht enthalten. Diese würde sich jedoch ähnlich wie die Datei auf Benutzerebene verhalten.)</span><span class="sxs-lookup"><span data-stu-id="5e99f-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="5e99f-167">Datei A auf Benutzerebene (`%APPDATA%\NuGet\NuGet.Config` unter Windows, `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="5e99f-167">File A. User-level file, (`%APPDATA%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="5e99f-168">Datei B (disk_drive_2/NuGet.Config):</span><span class="sxs-lookup"><span data-stu-id="5e99f-168">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="5e99f-169">Datei C (disk_drive_2/Project1/NuGet.Config):</span><span class="sxs-lookup"><span data-stu-id="5e99f-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="5e99f-170">Datei D (disk_drive_2/Project2/NuGet.Config):</span><span class="sxs-lookup"><span data-stu-id="5e99f-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="5e99f-171">Je nachdem, wo aus NuGet aufgerufen wird, werden die Einstellungen folgendermaßen geladen und angewendet:</span><span class="sxs-lookup"><span data-stu-id="5e99f-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="5e99f-172">**Aufruf von disk_drive_1/users aus:** Nur die Standardrepository, die in der Konfigurationsdatei auf Benutzerebene (A) aufgeführt wird, wird verwendet, da dies die einzige Datei ist, die auf disk_drive_1 gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="5e99f-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="5e99f-173">**Aufruf von disk_drive_2/ oder disk_drive_/tmp aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, dann sucht NuGet im Stamm von disk_drive_2 und findet Datei B.</span><span class="sxs-lookup"><span data-stu-id="5e99f-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="5e99f-174">NuGet sucht ebenfalls in /tmp nach einer Konfigurationsdatei, findet jedoch keine.</span><span class="sxs-lookup"><span data-stu-id="5e99f-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="5e99f-175">Deshalb wird das Standardrepository auf nuget.org verwendet, außerdem wird die Paketwiederherstellung aktiviert und Pakete werden in disk_drive_2/tmp erweitert.</span><span class="sxs-lookup"><span data-stu-id="5e99f-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="5e99f-176">**Aufruf von disk_drive_2/Project1 oder disk_drive_2/Project1/Source aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, dann lädt NuGet Datei B aus dem Stamm von disk_drive_2 und schließlich Datei C.</span><span class="sxs-lookup"><span data-stu-id="5e99f-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="5e99f-177">Die Einstellungen in Datei C überschreiben die in Datei A und B. Pakete werden deshalb im `repositoryPath` disk_drive_2/Project1/External/Packages statt in *disk_drive_2/tmp* installiert.</span><span class="sxs-lookup"><span data-stu-id="5e99f-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="5e99f-178">Da `<packageSources>` durch Datei C gelöscht wird, ist nuget.org nicht mehr als Quelle verfügbar, sondern nur noch `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="5e99f-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="5e99f-179">**Aufruf von disk_drive_2/Project2 oder disk_drive_2/Project2/Source aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, anschließend werden Datei B und D geladen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="5e99f-180">Da `packageSources` nicht gelöscht wurde, sind `nuget.org` und `https://MyPrivateRepo/DQ/nuget` als Quellen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="5e99f-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="5e99f-181">Die Pakete werden wie in Datei B angegeben in disk_drive_2/tmp erweitert.</span><span class="sxs-lookup"><span data-stu-id="5e99f-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="5e99f-182">NuGet-Standarddatei</span><span class="sxs-lookup"><span data-stu-id="5e99f-182">NuGet defaults file</span></span>

<span data-ttu-id="5e99f-183">Die `NuGetDefaults.Config`-Datei ist vorhanden, um Paketquellen anzugeben, von denen aus Pakete installiert und aktualisiert werden können und um das Standardziel für das Veröffentlichen von Paketen mit `nuget push` anzugeben.</span><span class="sxs-lookup"><span data-stu-id="5e99f-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="5e99f-184">Da Administratoren konsistente `NuGetDefaults.Config`-Dateien einfach für Entwickler- und Buildcomputer bereitstellen können (z.B. mithilfe von Gruppenrichtlinie), können diese sicherstellen, dass jeder in der Organisation die richtige Paketquelle anstelle von nuget.org verwendet.</span><span class="sxs-lookup"><span data-stu-id="5e99f-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="5e99f-185">Durch die `NuGetDefaults.Config`-Datei werden Paketquellen niemals aus der NuGet-Konfiguration eines Entwicklers gelöscht.</span><span class="sxs-lookup"><span data-stu-id="5e99f-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="5e99f-186">Wenn der Entwickler also bereits NuGet verwendet und deshalb eine Paketquelle von nuget.org registriert, wird diese nach der Erstellung der `NuGetDefaults.Config`-Datei nicht entfernt.</span><span class="sxs-lookup"><span data-stu-id="5e99f-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="5e99f-187">Darüber hinaus kann weder `NuGetDefaults.Config` noch ein anderer Mechanismus in NuGet den Zugriff auf Paketquellen wie nuget.org verhindern. Wenn eine Organisation solche Zugriffe blockieren möchte, müssen dafür andere Mittel, z.B. eine Firewall, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5e99f-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="5e99f-188">Speicherort von NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5e99f-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="5e99f-189">In der folgenden Tabelle wird beschrieben, wo die `NuGetDefaults.Config`-Datei gespeichert werden soll. Dies ist vom jeweiligen Betriebssystem abhängig:</span><span class="sxs-lookup"><span data-stu-id="5e99f-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="5e99f-190">Betriebssystemplattform</span><span class="sxs-lookup"><span data-stu-id="5e99f-190">OS Platform</span></span>  | <span data-ttu-id="5e99f-191">Speicherort von NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5e99f-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="5e99f-192">Windows</span><span class="sxs-lookup"><span data-stu-id="5e99f-192">Windows</span></span>      | <span data-ttu-id="5e99f-193">**Visual Studio 2017 oder NuGet 4.x und höher:** %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="5e99f-193">**Visual Studio 2017 or NuGet 4.x+:** %ProgramFiles(x86)%\NuGet\Config</span></span> <br /><span data-ttu-id="5e99f-194">**Visual Studio 2015 und früher oder NuGet 3.x und früher:** %PROGRAMDATA%\NuGet</span><span class="sxs-lookup"><span data-stu-id="5e99f-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** %PROGRAMDATA%\NuGet</span></span> |
| <span data-ttu-id="5e99f-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5e99f-195">Mac/Linux</span></span>    | <span data-ttu-id="5e99f-196">$XDG_DATA_HOME (in der Regel ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="5e99f-196">$XDG_DATA_HOME (typically ~/.local/share)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="5e99f-197">Einstellungen von NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5e99f-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="5e99f-198">`packageSources`: Diese Auflistung hat in regulären Konfigurationsdateien die gleiche Bedeutung wie `packageSources` und gibt die Standardquellen an.</span><span class="sxs-lookup"><span data-stu-id="5e99f-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="5e99f-199">NuGet verwendet die Quellen in der chronologischen Reihenfolge der Installation oder Aktualisierung von Paketen in Projekten unter Verwendung der Referenzformate von `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5e99f-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` reference format.</span></span> <span data-ttu-id="5e99f-200">Für Pakete, die das PackageReference-Format verwenden, verwendet NuGet unabhängig von der Reihenfolge der Konfigurationsdateien zuerst die lokalen Quellen, dann die Quellen auf Netzwerkfreigaben und anschließend HTTP-Quellen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="5e99f-201">NuGet ignoriert immer die Reihenfolge von Quellen mit Wiederherstellungsvorgängen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="5e99f-202">`disabledPackageSources`: Diese Auflistung hat ebenfalls die gleiche Bedeutung wie in `NuGet.Config`-Dateien, bei denen jede betroffene Quelle mit ihrem Namen und einem TRUE- oder FALSE-Wert aufgeführt wird, der angibt, ob diese deaktiviert ist oder nicht.</span><span class="sxs-lookup"><span data-stu-id="5e99f-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="5e99f-203">Dadurch wird ermöglicht, dass der Quellname und die URL in `packageSources` verbleiben, ohne dass diese standardmäßig aktiviert sein muss.</span><span class="sxs-lookup"><span data-stu-id="5e99f-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="5e99f-204">Einzelne Entwickler können die Quelle erneut aktivieren, indem sie den Wert der Quelle in anderen `NuGet.Config`-Dateien auf FALSE festlegen. Die richtige URL muss somit nicht erneut gesucht werden.</span><span class="sxs-lookup"><span data-stu-id="5e99f-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="5e99f-205">Dies ist nützlich, um Entwicklern eine vollständige Liste der internen Quell-URLs für eine Organisation bereitzustellen und gleichzeitig nur eine einzige Quelle für das Team standardmäßig zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="5e99f-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="5e99f-206">`defaultPushSource`: Gibt das Standardziel für `nuget push`-Vorgänge an und überschreibt die integrierten Standardeinstellungen von nuget.org. Administratoren können diese Einstellung bereitstellen, um das versehentliche Veröffentlichen von internen Paketen für den öffentlichen Katalog von nuget.org zu verhindern, da Entwickler `nuget push -Source` verwenden müssen, um auf nuget.org zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="5e99f-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="5e99f-207">Beispiel für NuGetDefaults.Config und eine Anwendung</span><span class="sxs-lookup"><span data-stu-id="5e99f-207">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```