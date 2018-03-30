---
title: NuGet-Paketwiederherstellung | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Übersicht über die Wiederherstellung von Paketen mit NuGet, von denen ein Projekt abhängig ist, die auch die Deaktivierung von Wiederherstellungsversionen sowie von eingeschränkten Versionen umfasst."
keywords: "NuGet-Paketwiederherstellung, NuGet-Paketinstallation, Installieren eines Pakets, Wiederherstellen von Paketen, Abhängigkeitsversionen, Deaktivieren von automatischen Wiederherstellungen, einschränkende Paketversionen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a><span data-ttu-id="a90c1-104">Paketwiederherstellung</span><span class="sxs-lookup"><span data-stu-id="a90c1-104">Package Restore</span></span>

<span data-ttu-id="a90c1-105">Die NuGet-**Paketwiederherstellung** installiert vor dem Erstellen eines Projekts alle Pakete, auf die verwiesen wird, um eine übersichtlichere Entwicklungsumgebung zu unterstützen und die Größe des Repositorys zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="a90c1-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="a90c1-106">Dieses häufig verwendete Feature &mdash; verfügbar in Visual Studio, .NET Core 2.0 und höher und xbuild in Mono &mdash; stellt sicher, dass alle Abhängigkeiten in einem Projekt verfügbar sind. Dabei ist es nicht erforderlich, dass diese Pakete in der Quellcodeverwaltung gespeichert werden (Informationen zur Konfiguration ihres Repositorys zum Ausschließen von Paketbinärdateien finden Sie unter [Pakete und Quellcodeverwaltung](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="a90c1-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="a90c1-107">Sie können Pakete jederzeit auch manuell wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="a90c1-108">Weitere Details zur Paketwiederherstellung auf Buildservern finden Sie unter [Package restore with TFBuild (Paketwiederherstellung mit TFBuild)](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="a90c1-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="a90c1-109">Übersicht zur Paketwiederherstellung</span><span class="sxs-lookup"><span data-stu-id="a90c1-109">Package restore overview</span></span>

<span data-ttu-id="a90c1-110">Durch das Wiederherstellen von Paketen werden bei Bedarf zunächst die direkten Abhängigkeiten eines Projekts installiert, dann werden alle Abhängigkeiten dieser Pakete von dem gesamten Abhängigkeitsdiagramm installiert.</span><span class="sxs-lookup"><span data-stu-id="a90c1-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="a90c1-111">Wenn ein Paket noch nicht installiert ist, versucht NuGet erst, das Paket aus dem [Cache](../consume-packages/managing-the-nuget-cache.md) abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="a90c1-112">Wenn sich das Paket nicht im Cache befindet, versucht NuGet, das Paket von allen aktivierten Quellen herunterzuladen (und zwischenzuspeichern) (Informationen finden Sie unter [Konfigurieren des NuGet-Verhaltens](Configuring-NuGet-Behavior.md)). Außerdem werden Quellen in Visual Studio in einer der Liste unter **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="a90c1-112">If the package is not in the cache, NuGet then attempts to download (and cache) the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md)); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="a90c1-113">NuGet ignoriert die Reihenfolgen der Paketquellen und verwendet dabei das Paket aus einer beliebigen Quelle, die als erstes auf Anforderungen reagiert.</span><span class="sxs-lookup"><span data-stu-id="a90c1-113">NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="a90c1-114">NuGet zeigt erst einen Fehler an, wenn alle Quellen überprüft wurden. Erst dann kann ein Paket wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="a90c1-114">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="a90c1-115">Dann meldet NuGet den Fehler nur für die letzte Quelle aus der Liste.</span><span class="sxs-lookup"><span data-stu-id="a90c1-115">At that time, NuGet reports the failure for only the last source in the list.</span></span> <span data-ttu-id="a90c1-116">Der Fehler deutet darauf hin, dass das Paket auch in *keiner* der anderen Quellen vorhanden ist, auch wenn für die einzelnen Quellen kein Fehler angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="a90c1-116">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="a90c1-117">Die Paketwiederherstellung wird auf folgenden Wegen ausgelöst:</span><span class="sxs-lookup"><span data-stu-id="a90c1-117">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="a90c1-118">**dotnet-CLI**: Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)) aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="a90c1-118">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="a90c1-119">In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="a90c1-119">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="a90c1-120">**Benutzeroberfläche des Paket-Managers (Visual Studio unter Windows)**: Pakete werden automatisch wiederhergestellt, wenn Sie ein Projekt aus einer Vorlage erstellen und wenn Sie ein Projekt erstellen (gemäß der unter [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore) beschriebenen Option).</span><span class="sxs-lookup"><span data-stu-id="a90c1-120">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="a90c1-121">Die Wiederherstellung wird in NuGet 4.0 und höher auch automatisch durchgeführt, wenn Änderungen an einem Projekt vorgenommen werden, das auf dem .NET Core SDK basiert.</span><span class="sxs-lookup"><span data-stu-id="a90c1-121">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="a90c1-122">Zum manuellen Wiederherstellen klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die Projektmappe, und wählen Sie **NuGet-Pakete wiederherstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="a90c1-122">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="a90c1-123">Wenn danach einzelne Pakete immer noch nicht ordnungsgemäß installiert sind (also im Projektmappen-Explorer ein Fehlersymbol angezeigt wird), deinstallieren Sie die betroffenen Pakete über die Benutzeroberfläche des Paket-Managers, und installieren Sie diese über die Benutzeroberfläche erneut.</span><span class="sxs-lookup"><span data-stu-id="a90c1-123">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="a90c1-124">Informationen dazu finden Sie unter [Reinstalling and updating packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a90c1-124">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="a90c1-125">Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, aktivieren Sie die automatische Wiederherstellung, indem Sie die Anweisungen unter [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore) ausführen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-125">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="a90c1-126">**NuGet-CLI**: Verwenden Sie den Befehl [nuget restore](../tools/cli-ref-restore.md), der Pakete wiederherstellt, die in der Projektdatei (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)) oder einer [packages.config](../reference/packages-config.md)-Datei aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="a90c1-126">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)) or in a [packages.config](../reference/packages-config.md) file.</span></span> <span data-ttu-id="a90c1-127">Sie können auch eine Projektmappendatei angeben.</span><span class="sxs-lookup"><span data-stu-id="a90c1-127">You can also specify a solution file.</span></span>

- <span data-ttu-id="a90c1-128">**MSBuild**: Verwenden Sie den Befehl [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), der Pakete wiederherstellt, die in der Projektdatei (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)) aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="a90c1-128">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="a90c1-129">Nur in NuGet 4.x und MSBuild 15.1 und deren höheren Versionen verfügbar, die in Visual Studio 2017 enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="a90c1-129">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="a90c1-130">Sowohl `nuget restore` als auch `dotnet restore` verwenden diesen Befehl für anwendbare Projekte.</span><span class="sxs-lookup"><span data-stu-id="a90c1-130">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="a90c1-131">**Visual Studio Team Services**: Fügen Sie bei der Erstellung einer Builddefinition auf Team Services dieser die Aufgabe [NuGet-Wiederherstellung](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) oder [.NET Core-Wiederherstellung](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) hinzu, bevor Sie eine Buildaufgabe ausführen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-131">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="a90c1-132">Diese Aufgabe ist standardmäßig in einer Reihe von Buildvorlagen enthalten.</span><span class="sxs-lookup"><span data-stu-id="a90c1-132">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="a90c1-133">**Team Foundation Server**: In TFS 2013 und höher werden Pakete automatisch beim Build wiederhergestellt, wenn Sie eine Team Build-Vorlage für TFS 2013 oder höher verwenden.</span><span class="sxs-lookup"><span data-stu-id="a90c1-133">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="a90c1-134">Bei früheren Versionen von TFS können Sie einen Buildschritt hinzufügen, um eine der oben genannten Optionen für Wiederherstellungsbefehlszeilen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-134">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="a90c1-135">Optional können Sie die Buildvorlage zu TFS 2013 migrieren.</span><span class="sxs-lookup"><span data-stu-id="a90c1-135">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="a90c1-136">Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise für die Paketwiederherstellung mit Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="a90c1-136">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="a90c1-137">Aktivieren und Deaktivieren der Paketwiederherstellung</span><span class="sxs-lookup"><span data-stu-id="a90c1-137">Enabling and disabling package restore</span></span>

<span data-ttu-id="a90c1-138">Die Paketwiederherstellung ist standardmäßig in Visual Studio über **Tools > Optionen > NuGet-Paket-Manager** aktiviert:</span><span class="sxs-lookup"><span data-stu-id="a90c1-138">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Überwachen der Wiederherstellungsverhalten mithilfe von Optionen des NuGet-Paket-Managers](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="a90c1-140">**Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben): überwacht, wie im Folgenden dargestellt, jegliche Arten der Paketwiederherstellung durch die Änderung der `packageRestore/enabled`-Einstellung in der `NuGet.Config`-Datei (`%AppData%\NuGet\NuGet.Config` unter Windows, `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a90c1-140">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="a90c1-141">In Visual Studio sorgt diese Einstellungen dafür, dass der Befehl zur **Wiederherstellung von NuGet-Paketen** im Kontextmenü der Projektmappe ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="a90c1-141">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="a90c1-142">Die `packageRestore/enabled`-Einstellung kann global außer Kraft gesetzt werden, indem eine Umgebungsvariable namens **EnableNuGetPackageRestore** mit einem Wert von TRUE oder FALSE festgelegt wird, bevor Visual Studio gestartet oder mit einem Build begonnen wird.</span><span class="sxs-lookup"><span data-stu-id="a90c1-142">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="a90c1-143">**Automatically check for missing packages during build in Visual Studio** (Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen): überwacht die automatische Wiederherstellung, indem die Einstellung `packageRestore/automatic`, wie im Folgenden dargestellt, in der Datei `NuGet.Config` geändert wird (`%AppData%\NuGet\NuGet.Config` unter Windows, `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a90c1-143">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="a90c1-144">Wenn diese Option festgelegt ist, werden automatisch fehlende Pakete wiederhergestellt, wenn ein Build über Visual Studio ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a90c1-144">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="a90c1-145">Sie hat keine Auswirkungen auf Builds, die über die Befehlszeile unter Verwendung von MSBuild ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a90c1-145">The option does not affect builds run from the command line using MSBuild.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="a90c1-146">Weitere Informationen finden Sie unter [NuGet config file – packageRestore section (NuGet-Konfigurationsdatei: Abschnitt „packageRestore“)](../reference/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="a90c1-146">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="a90c1-147">In einigen Fällen kann es dazu kommen, dass ein Entwickler oder ein Unternehmen für alle Benutzer Pakete auf einem Computer aktivieren oder deaktivieren möchte.</span><span class="sxs-lookup"><span data-stu-id="a90c1-147">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="a90c1-148">Diese Einstellung können Sie vornehmen, indem Sie über der globalen NuGet-Konfigurationsdatei in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` dieselbe Einstellung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="a90c1-148">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="a90c1-149">Einzelne Benutzer können dann nach Bedarf die Wiederherstellung auf Projektebene aktivieren.</span><span class="sxs-lookup"><span data-stu-id="a90c1-149">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="a90c1-150">Weitere Informationen zur Vorgehensweise von NuGet bei der Priorisierung von mehreren Konfigurationsdateien finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="a90c1-150">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="a90c1-151">Einschränken der Paketversionen mit der Wiederherstellung</span><span class="sxs-lookup"><span data-stu-id="a90c1-151">Constraining package versions with restore</span></span>

<span data-ttu-id="a90c1-152">Wenn Pakete durch eine beliebige Methode wiederhergestellt werden, berücksichtigt es alle Einschränkungen, die in `packages.config` oder der Projektdatei angegeben sind:</span><span class="sxs-lookup"><span data-stu-id="a90c1-152">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="a90c1-153">`packages.config`: Gibt einen Versionsbereich in der `allowedVersion`-Eigenschaft der Abhängigkeit an.</span><span class="sxs-lookup"><span data-stu-id="a90c1-153">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="a90c1-154">Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="a90c1-154">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="a90c1-155">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a90c1-155">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="a90c1-156">PackageReference: Gibt einen Versionsbereich zusammen mit der Versionsnummer der Abhängigkeit an.</span><span class="sxs-lookup"><span data-stu-id="a90c1-156">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="a90c1-157">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a90c1-157">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="a90c1-158">Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../reference/package-versioning.md) beschriebene Notation.</span><span class="sxs-lookup"><span data-stu-id="a90c1-158">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a90c1-159">Problembehandlung</span><span class="sxs-lookup"><span data-stu-id="a90c1-159">Troubleshooting</span></span>

<span data-ttu-id="a90c1-160">Informationen zur Problembehandlung finden Sie unter [Problembehandlung bei der Paketwiederherstellung](package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a90c1-160">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>