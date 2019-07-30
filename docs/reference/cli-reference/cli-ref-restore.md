---
title: Befehl "nuget CLI Restore"
description: Referenz für den Befehl "nuget. exe Restore"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327637"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="54809-103">Restore-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="54809-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="54809-104">**Gilt für:** &bullet; **unterstützte Versionen** : 2.7+</span><span class="sxs-lookup"><span data-stu-id="54809-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="54809-105">Alle Pakete, die im `packages` Ordner fehlen, werden heruntergeladen und installiert.</span><span class="sxs-lookup"><span data-stu-id="54809-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="54809-106">Bei der Verwendung mit nuget 4.0 und höher und dem packagereferenzierungsformat wird `<project>.nuget.props` `obj` bei Bedarf im Ordner eine Datei generiert.</span><span class="sxs-lookup"><span data-stu-id="54809-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="54809-107">(Die Datei kann in der Quell Code Verwaltung ausgelassen werden.)</span><span class="sxs-lookup"><span data-stu-id="54809-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="54809-108">Unter Mac OSX und Linux mit der CLI in Mono wird das Wiederherstellen von Paketen mit packagereferenzierung nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="54809-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="54809-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="54809-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="54809-110">Dabei gibt den Speicherort einer Projekt Mappe oder `packages.config` einer Datei an. `<projectPath>`</span><span class="sxs-lookup"><span data-stu-id="54809-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="54809-111">Informationen zu den Verhaltens Details finden [Sie unten in](#remarks) den hinweisen.</span><span class="sxs-lookup"><span data-stu-id="54809-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="54809-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="54809-112">Options</span></span>

| <span data-ttu-id="54809-113">Option</span><span class="sxs-lookup"><span data-stu-id="54809-113">Option</span></span> | <span data-ttu-id="54809-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="54809-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54809-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="54809-115">ConfigFile</span></span> | <span data-ttu-id="54809-116">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="54809-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="54809-117">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="54809-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="54809-118">DirectDownload</span></span> | <span data-ttu-id="54809-119">*(4.0* und höher) Pakete werden direkt heruntergeladen, ohne dass Caches mit Binärdateien oder Metadaten aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="54809-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="54809-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="54809-120">DisableParallelProcessing</span></span> | <span data-ttu-id="54809-121">Deaktiviert die parallele Wiederherstellung mehrerer Pakete.</span><span class="sxs-lookup"><span data-stu-id="54809-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="54809-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="54809-122">FallbackSource</span></span> | <span data-ttu-id="54809-123">*(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="54809-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="54809-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="54809-124">ForceEnglishOutput</span></span> | <span data-ttu-id="54809-125">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="54809-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="54809-126">Help</span><span class="sxs-lookup"><span data-stu-id="54809-126">Help</span></span> | <span data-ttu-id="54809-127">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="54809-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="54809-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="54809-128">MSBuildPath</span></span> | <span data-ttu-id="54809-129">*(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll `-MSBuildVersion`, und hat Vorrang vor.</span><span class="sxs-lookup"><span data-stu-id="54809-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="54809-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="54809-130">MSBuildVersion</span></span> | <span data-ttu-id="54809-131">*(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="54809-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="54809-132">Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="54809-132">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="54809-133">Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="54809-134">NoCache</span><span class="sxs-lookup"><span data-stu-id="54809-134">NoCache</span></span> | <span data-ttu-id="54809-135">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="54809-136">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="54809-136">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="54809-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="54809-137">NonInteractive</span></span> | <span data-ttu-id="54809-138">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="54809-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="54809-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="54809-139">OutputDirectory</span></span> | <span data-ttu-id="54809-140">Gibt den Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="54809-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="54809-141">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="54809-142">Erforderlich, wenn mit einer `packages.config` Datei wieder `PackagesDirectory` hergestellt `SolutionDirectory` wird, sofern nicht oder verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="54809-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="54809-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="54809-143">PackageSaveMode</span></span> | <span data-ttu-id="54809-144">Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden `nuspec`sollen `nupkg`: einer `nuspec;nupkg`von, oder.</span><span class="sxs-lookup"><span data-stu-id="54809-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="54809-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="54809-145">PackagesDirectory</span></span> | <span data-ttu-id="54809-146">Wie in `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="54809-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="54809-147">Erforderlich, wenn mit einer `packages.config` Datei wieder `OutputDirectory` hergestellt `SolutionDirectory` wird, sofern nicht oder verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="54809-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="54809-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="54809-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="54809-149">Timeout in Sekunden für das Auflösen von Projekt-zu-Projekt-verweisen.</span><span class="sxs-lookup"><span data-stu-id="54809-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="54809-150">Rekursive</span><span class="sxs-lookup"><span data-stu-id="54809-150">Recursive</span></span> | <span data-ttu-id="54809-151">*(4.0* und höher) Stellt alle Referenzprojekte für UWP-und .net Core-Projekte wieder her.</span><span class="sxs-lookup"><span data-stu-id="54809-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="54809-152">Gilt nicht für Projekte, die `packages.config`verwenden.</span><span class="sxs-lookup"><span data-stu-id="54809-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="54809-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="54809-153">RequireConsent</span></span> | <span data-ttu-id="54809-154">Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden.</span><span class="sxs-lookup"><span data-stu-id="54809-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="54809-155">Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="54809-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="54809-156">Projektmappenverzeichnis</span><span class="sxs-lookup"><span data-stu-id="54809-156">SolutionDirectory</span></span> | <span data-ttu-id="54809-157">Gibt den Projektmappenordner an.</span><span class="sxs-lookup"><span data-stu-id="54809-157">Specifies the solution folder.</span></span> <span data-ttu-id="54809-158">Ungültig beim Wiederherstellen von Paketen für eine Projekt Mappe.</span><span class="sxs-lookup"><span data-stu-id="54809-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="54809-159">Erforderlich, wenn mit einer `packages.config` Datei wieder `PackagesDirectory` hergestellt `OutputDirectory` wird, sofern nicht oder verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="54809-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="54809-160">Source</span><span class="sxs-lookup"><span data-stu-id="54809-160">Source</span></span> | <span data-ttu-id="54809-161">Gibt die Liste der Paketquellen (als URLs) an, die für die Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="54809-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="54809-162">Wenn der Befehl weggelassen wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="54809-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="54809-163">Verbosity</span><span class="sxs-lookup"><span data-stu-id="54809-163">Verbosity</span></span> | <span data-ttu-id="54809-164">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="54809-164">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="54809-165">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="54809-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="54809-166">Hinweise</span><span class="sxs-lookup"><span data-stu-id="54809-166">Remarks</span></span>

<span data-ttu-id="54809-167">Der Restore-Befehl führt die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="54809-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="54809-168">Bestimmen Sie den Betriebsmodus des Restore-Befehls.</span><span class="sxs-lookup"><span data-stu-id="54809-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="54809-169">ProjectPath-Dateityp</span><span class="sxs-lookup"><span data-stu-id="54809-169">projectPath file type</span></span> | <span data-ttu-id="54809-170">Verhalten</span><span class="sxs-lookup"><span data-stu-id="54809-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="54809-171">Lösung (Ordner)</span><span class="sxs-lookup"><span data-stu-id="54809-171">Solution (folder)</span></span> | <span data-ttu-id="54809-172">Nuget sucht nach einer `.sln` Datei und verwendet diese, wenn Sie gefunden wird, andernfalls wird ein Fehler ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="54809-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="54809-173">`(SolutionDir)\.nuget`wird als Startordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="54809-174">`.sln`Datei</span><span class="sxs-lookup"><span data-stu-id="54809-174">`.sln` file</span></span> | <span data-ttu-id="54809-175">Von der Lösung identifizierte Pakete wiederherstellen; Gibt einen Fehler aus `-SolutionDirectory` , wenn verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="54809-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="54809-176">`$(SolutionDir)\.nuget`wird als Startordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="54809-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="54809-177">`packages.config`-oder-Projektdatei</span><span class="sxs-lookup"><span data-stu-id="54809-177">`packages.config` or project file</span></span> | <span data-ttu-id="54809-178">Wiederherstellen der in der Datei aufgeführten Pakete, auflösen und Installieren von Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="54809-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="54809-179">Anderer Dateityp</span><span class="sxs-lookup"><span data-stu-id="54809-179">Other file type</span></span> | <span data-ttu-id="54809-180">Es wird davon ausgegangen, dass `.sln` eine Datei wie oben angegeben wird. wenn es sich nicht um eine Lösung handelt, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="54809-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="54809-181">(ProjectPath nicht angegeben)</span><span class="sxs-lookup"><span data-stu-id="54809-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="54809-182">Nuget sucht im aktuellen Ordner nach Projektmappendateien.</span><span class="sxs-lookup"><span data-stu-id="54809-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="54809-183">Wenn eine einzelne Datei gefunden wird, wird diese zum Wiederherstellen von Paketen verwendet. Wenn mehrere Lösungen gefunden werden, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="54809-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="54809-184">Wenn keine Projektmappendateien vorhanden sind, sucht nuget `packages.config` nach einem und verwendet dieses zum Wiederherstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="54809-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="54809-185">Wenn keine Projekt Mappe `packages.config` oder Datei gefunden wird, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="54809-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="54809-186">Bestimmen Sie den Ordner "Pakete" mit der folgenden Prioritäts Reihenfolge (nuget gibt einen Fehler aus, wenn keiner dieser Ordner gefunden wird):</span><span class="sxs-lookup"><span data-stu-id="54809-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="54809-187">Der mit `-PackagesDirectory`angegebene Ordner.</span><span class="sxs-lookup"><span data-stu-id="54809-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="54809-188">Der `repositoryPath` Wert in`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="54809-188">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="54809-189">Der mit angegebene Ordner`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="54809-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="54809-190">Beim Wiederherstellen von Paketen für eine Lösung führt nuget Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="54809-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="54809-191">Lädt die Projektmappendatei.</span><span class="sxs-lookup"><span data-stu-id="54809-191">Loads the solution file.</span></span>
    - <span data-ttu-id="54809-192">Stellt Pakete auf Projektmappenebene wieder `packages` her, die in `$(SolutionDir)\.nuget\packages.config` aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="54809-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="54809-193">Wiederherstellen der in `$(ProjectDir)\packages.config` aufgelisteten Pakete `packages` in den Ordner.</span><span class="sxs-lookup"><span data-stu-id="54809-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="54809-194">Stellen Sie das Paket für jedes angegebene Paket parallel wieder her `-DisableParallelProcessing` , es sei denn, wird angegeben.</span><span class="sxs-lookup"><span data-stu-id="54809-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="54809-195">Beispiele</span><span class="sxs-lookup"><span data-stu-id="54809-195">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```