---
title: 1.4 NuGet-Versionshinweise
description: Versionshinweise für NuGet 1.4 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5e4c2a5f2db80b0ebc3fec7c653aecb8bcc4ab5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="04b97-103">1.4 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="04b97-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="04b97-104">[Anmerkungen zur Version des NuGet-1.3](../release-notes/nuget-1.3.md) | [NuGet 1.5-Versionshinweise](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="04b97-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="04b97-105">NuGet 1.4 wurde 17 Juni 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="04b97-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="04b97-106">Features</span><span class="sxs-lookup"><span data-stu-id="04b97-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="04b97-107">Updatepaket Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="04b97-107">Update-Package improvements</span></span>
<span data-ttu-id="04b97-108">NuGet 1.4 führt viele Verbesserungen an den Update-Paket-Befehl zu Pakete über die gleiche Version für mehrere Projekte in einer Projektmappe erleichtern.</span><span class="sxs-lookup"><span data-stu-id="04b97-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="04b97-109">Beispielsweise ist, wenn ein Paket auf die neueste Version zu aktualisieren, es üblich, die alle Projekte mit diesem Paket installiert, um auf die gleiche Verision aktualisiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="04b97-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="04b97-110">Die `Update-Package` Befehl jetzt vereinfacht:</span><span class="sxs-lookup"><span data-stu-id="04b97-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="04b97-111">Aktualisieren Sie alle Pakete in einem einzelnen Projekt</span><span class="sxs-lookup"><span data-stu-id="04b97-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="04b97-112">Aktualisieren eines Pakets in allen Projekten</span><span class="sxs-lookup"><span data-stu-id="04b97-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="04b97-113">Aktualisieren Sie alle Pakete in allen Projekten</span><span class="sxs-lookup"><span data-stu-id="04b97-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="04b97-114">Ausführen eines "sicheren" Updates für alle Pakete</span><span class="sxs-lookup"><span data-stu-id="04b97-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="04b97-115">Die `-Safe` Flag beschränkt Upgrades auf nur Versionen mit der gleichen Haupt- und Version-Komponente.</span><span class="sxs-lookup"><span data-stu-id="04b97-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="04b97-116">Angenommen, wenn die Version 1.0.0 eines Pakets installiert ist und die Versionen 1.0.1, 1.0.2 und 1.1 im Feed verfügbar sind die `-Safe` Flag aktualisiert das Paket auf die Version 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="04b97-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="04b97-117">Aktualisieren der ohne die `-Safe` Flag würde aktualisieren Sie das Paket auf die neueste Version 1.1.</span><span class="sxs-lookup"><span data-stu-id="04b97-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="04b97-118">Verwalten von Paketen auf Projektmappenebene</span><span class="sxs-lookup"><span data-stu-id="04b97-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="04b97-119">Vor der Einführung NuGet 1.4 war die Installation eines Pakets in mehrere Projekte mühsam mithilfe des Dialogfelds.</span><span class="sxs-lookup"><span data-stu-id="04b97-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="04b97-120">Das Dialogfeld ", einmal pro Projekt starten muss.</span><span class="sxs-lookup"><span data-stu-id="04b97-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="04b97-121">NuGet 1.4 fügt Unterstützung für Installation/Deinstallation/Aktualisieren von Paketen in mehreren Projekten gleichzeitig hinzu.</span><span class="sxs-lookup"><span data-stu-id="04b97-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="04b97-122">Starten Sie einfach die von mit der rechten Maustaste auf die Projektmappe, und wählen die **NuGet-Pakete verwalten** Option des Menüs.</span><span class="sxs-lookup"><span data-stu-id="04b97-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Dialogfeld für Projektmappen auf NuGet-Pakete verwalten](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="04b97-124">Beachten Sie, dass in der Titelleiste des Dialogfelds, der Namen der Projektmappe angezeigt wird, nicht den Namen eines Projekts.</span><span class="sxs-lookup"><span data-stu-id="04b97-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="04b97-125">Paketvorgängen bieten nun eine Liste von Kontrollkästchen mit der Liste der Projekte, denen die Operation angewendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="04b97-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Verwalten von NuGet-Pakete Projektauswahl](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="04b97-127">Weitere Informationen finden Sie im Thema auf [Verwaltung von Paketen für die Projektmappe](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="04b97-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="04b97-128">Einschränken von Upgrades auf Versionen zulässig</span><span class="sxs-lookup"><span data-stu-id="04b97-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="04b97-129">Standardmäßig wird beim Ausführen der `Update-Package` Befehl für ein Paket (oder beim Aktualisieren des Pakets im Dialogfeld), wird Sie auf die neueste Version im Feed aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="04b97-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="04b97-130">Mit der neuen Unterstützung für alle Pakete aktualisiert es gibt möglicherweise Fälle, die in denen Sie ein Paket für eine bestimmte Version Palette sperren möchten.</span><span class="sxs-lookup"><span data-stu-id="04b97-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="04b97-131">Sie können z. B. im Voraus wissen, dass Ihre Anwendung nur bei Version 2.\* eines Pakets, aber nicht 3.0 und höher verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="04b97-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="04b97-132">Um zu verhindern, dass versehentlich beim Aktualisieren des Pakets auf 3 NuGet 1.4 fügt Unterstützung für die Beschränkung der Bereich von Versionen, die Pakete von Hand bearbeiten aktualisiert werden können die `packages.config` Datei mit dem neuen `allowedVersions` Attribut.</span><span class="sxs-lookup"><span data-stu-id="04b97-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="04b97-133">Z. B. das folgende Beispiel veranschaulicht das Sperren der `SomePackage` Paket die Version im Bereich (exklusiv) 2.0-3.0.</span><span class="sxs-lookup"><span data-stu-id="04b97-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="04b97-134">Die `allowedVersions` Attribut akzeptiert die Werte mithilfe der [Bereich Versionsformat](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="04b97-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="04b97-135">Beachten Sie, dass in 1.4, Sperren ein Paket für eine bestimmte Version Palette manuell bearbeitet werden muss.</span><span class="sxs-lookup"><span data-stu-id="04b97-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="04b97-136">In NuGet 1.5 wir planen die zum Hinzufügen der Unterstützung für die Platzierung dieser Bereich über dem `Install-Package` Befehl.</span><span class="sxs-lookup"><span data-stu-id="04b97-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="04b97-137">Paket-Schnellansicht</span><span class="sxs-lookup"><span data-stu-id="04b97-137">Package Visualizer</span></span>
<span data-ttu-id="04b97-138">Das neue Paket-Schnellansicht gestartet wird, über die **Tools** -> **Bibliothekspaket-Manager** -> **Paket Schnellansicht** Menüoption, können Sie Visualisieren Sie einfach alle Projekte und ihre Abhängigkeiten des Pakets in einer Projektmappe ein.</span><span class="sxs-lookup"><span data-stu-id="04b97-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="04b97-139">_**Wichtiger Hinweis:** diese Funktion nutzt die DGML-Unterstützung in Visual Studio. Erstellen die Visualisierung wird nur in Visual Studio Ultimate unterstützt. Anzeigen von DGML-Diagrammen wird nur in Visual Studio Premium oder höher unterstützt._</span><span class="sxs-lookup"><span data-stu-id="04b97-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Paket-Schnellansicht](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="04b97-141">Automatische Updates für das Dialogfeld "NuGet"</span><span class="sxs-lookup"><span data-stu-id="04b97-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="04b97-142">Einige Versionen von NuGet ggf. neue Features, die über ausgedrückt der `.nuspec` Datei, die nicht mit älteren Versionen von das Dialogfeld "NuGet" verstanden werden.</span><span class="sxs-lookup"><span data-stu-id="04b97-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="04b97-143">Ein Beispiel ist der Einführung in NuGet 1.4 für [angeben Frameworkassemblys](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="04b97-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="04b97-144">Aus diesem Grund ist es wichtig, die neueste Version von NuGet verwenden, um sicherzustellen, dass Sie die neuesten Features nutzen Pakete verwenden können.</span><span class="sxs-lookup"><span data-stu-id="04b97-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="04b97-145">Um Updates zu NuGet mehr sichtbar zu machen, enthält das Dialogfeld "NuGet" Logik zum Markieren, wenn eine neuere Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="04b97-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="04b97-146">_**Hinweis**: die Überprüfung erfolgt nur, wenn die **Online** Registerkarte in der aktuellen Sitzung ausgewählt wurde._</span><span class="sxs-lookup"><span data-stu-id="04b97-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Dialogfeld mit neuen Version verfügbaren NuGet-Pakete verwalten](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="04b97-148">Um die automatische Prüfung auf Updates zu deaktivieren, wechseln Sie zum Dialogfeld "NuGet-Einstellungen", und deaktivieren Sie **automatisch nach Updates suchen**.</span><span class="sxs-lookup"><span data-stu-id="04b97-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet-Einstellungen](./media/nuget-settings.png)

<span data-ttu-id="04b97-150">Diese Funktion tatsächlich in NuGet 1.3 hinzugefügt wurde, aber nicht sichtbar ist, natürlich, bis ein Update für 1.3, z. B. NuGet 1.4, zur Verfügung gestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="04b97-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="04b97-151">Dialogfeld "Paket-Manager"-Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="04b97-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="04b97-152">**Verbesserte Menünamen**: Menüoptionen zum Starten Sie des Dialogfeld "wurden aus Gründen der Übersichtlichkeit umbenannt.</span><span class="sxs-lookup"><span data-stu-id="04b97-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="04b97-153">Die Menüoption ist jetzt **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="04b97-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="04b97-154">**Im Detailbereich zeigt die neuesten Update Datum**: das NuGet-Dialogfeld zeigt das Datum des neuesten Updates im Detailbereich für ein Paket bei der **Online** oder **aktualisiert** Registerkarte ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="04b97-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="04b97-155">**Liste der RFID-Transponder angezeigt**: Tags für das NuGet-Dialogfeld angezeigt.</span><span class="sxs-lookup"><span data-stu-id="04b97-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="04b97-156">PowerShell-Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="04b97-156">Powershell Improvements</span></span>
* <span data-ttu-id="04b97-157">**PowerShell-Skripts signiert**: NuGet enthält signierte Powershell-Skripts, die Verwendung in enger gefassten Umgebungen aktivieren.</span><span class="sxs-lookup"><span data-stu-id="04b97-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="04b97-158">**Unterstützung aufzufordern**: die Package Manager Console unterstützt jetzt die Bestätigung über die `$host.ui.Prompt` und `$host.ui.PromptForChoice` Befehle.</span><span class="sxs-lookup"><span data-stu-id="04b97-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="04b97-159">**Paket Quellennamen**: der Name der Paketquelle wird unterstützt, bei der Angabe der Quelle für ein Paket mit der `-Source` Flag.</span><span class="sxs-lookup"><span data-stu-id="04b97-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="04b97-160">NuGet.exe Befehlszeile Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="04b97-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="04b97-161">**Benutzerdefinierte NuGet-Befehle**: nuget.exe über benutzerdefinierte Befehle, die mithilfe von MEF erweiterbar ist.</span><span class="sxs-lookup"><span data-stu-id="04b97-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="04b97-162">**Einfacher Workflow zum Erstellen von Paketen Symbol**: die `-Symbols` -Flag kann in einer normalen konventionsbasierten Ordnerstruktur erstellen ein Symbolpaket dazu nur die Quelle angewendet werden und `.pdb` Dateien innerhalb des Ordners.</span><span class="sxs-lookup"><span data-stu-id="04b97-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="04b97-163">**Angeben von mehreren Quellen**: die `NuGet install` Befehl unterstützt die Angabe von mehreren Quellen mit Semikolons als Trennzeichen oder durch Angabe `-Source` mehrere Male.</span><span class="sxs-lookup"><span data-stu-id="04b97-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="04b97-164">**Proxy-Authentifizierung unterstützen**: NuGet 1.4 fügt Unterstützung für die Eingabeaufforderung für Anmeldeinformationen des Benutzers, wenn NuGet hinter einem Proxy verwenden, die eine Authentifizierung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="04b97-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="04b97-165">**NuGet.exe unterbrechende Änderung aktualisieren**: die `-Self` Flag ist jetzt erforderlich für nuget.exe selbst aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="04b97-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="04b97-166">`nuget.exe Update` Jetzt dauert in einen Pfad zu der `packages.config` Datei und versucht, Pakete zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="04b97-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="04b97-167">Beachten Sie, dass dieses Update beschränkt ist, da dies nicht der Fall: ** zu aktualisieren, hinzufügen und Entfernen von Inhalt in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="04b97-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="04b97-168">** Führen Sie Powershell-Skripts im Paket.</span><span class="sxs-lookup"><span data-stu-id="04b97-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="04b97-169">NuGet-Server-Unterstützung für Push-Pakete, die mittels nuget.exe</span><span class="sxs-lookup"><span data-stu-id="04b97-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="04b97-170">NuGet enthält eine einfache Methode zum Hosten einer [einfache webbasierte NuGet-Repository](../hosting-packages/nuget-server.md) über die `NuGet.Server` NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="04b97-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="04b97-171">Mit NuGet-1.4 unterstützt einfache Server per Push übertragen, und Löschen von Paketen mit nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="04b97-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="04b97-172">Die neueste Version des `NuGet.Server` wird ein neues `appSetting`mit dem Namen `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="04b97-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="04b97-173">Wenn der Schlüssel weggelassen oder leer gelassen wird, wird die Pakete auf den Feed übertragen deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="04b97-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="04b97-174">Durch das Festlegen der "apikey" auf einen Wert (im Idealfall ein sicheres Kennwort) können wie Pakete mit nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="04b97-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="04b97-175">Unterstützung für Windows Phone Tools Mango Edition</span><span class="sxs-lookup"><span data-stu-id="04b97-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="04b97-176">NuGet ist jetzt in der Release Candidate-Version von Windows Phone-Tools für Mango unterstützt.</span><span class="sxs-lookup"><span data-stu-id="04b97-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="04b97-177">Aktuell-Tools für Windows Phone verfügt nicht über die Unterstützung für die Erweiterung für Visual Studio-Manager damit NuGet für Windows Phone-Tools zu installieren, müssen Sie möglicherweise herunterladen und die VSIX manuell ausführen.</span><span class="sxs-lookup"><span data-stu-id="04b97-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="04b97-178">Führen Sie den folgenden Befehl zum Deinstallieren von NuGet für Windows Phone-Tools.</span><span class="sxs-lookup"><span data-stu-id="04b97-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="04b97-179">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="04b97-179">Bug Fixes</span></span>
<span data-ttu-id="04b97-180">NuGet 1.4 mussten insgesamt 88 Arbeitsaufgaben behoben.</span><span class="sxs-lookup"><span data-stu-id="04b97-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="04b97-181">71 dieser wurden als Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="04b97-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="04b97-182">Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.4, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="04b97-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="04b97-183">Fehlerkorrekturen Folgendes zu beachten:</span><span class="sxs-lookup"><span data-stu-id="04b97-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="04b97-184">[Problem 603](http://nuget.codeplex.com/workitem/603): paketabhängigkeiten über unterschiedliche Repositorys ordnungsgemäß aufgelöst werden bei der eine bestimmte Paketquelle angeben.</span><span class="sxs-lookup"><span data-stu-id="04b97-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="04b97-185">[Problem 1036](http://nuget.codeplex.com/workitem/1036): Hinzufügen von `NuGet Pack SomeProject.csproj` Ereignis nicht mehr nach dem Erstellen verursacht eine Endlosschleife.</span><span class="sxs-lookup"><span data-stu-id="04b97-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="04b97-186">[Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` Flag unterstützt relative Pfade.</span><span class="sxs-lookup"><span data-stu-id="04b97-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="04b97-187">NuGet-1.4-Update</span><span class="sxs-lookup"><span data-stu-id="04b97-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="04b97-188">Kurz nach der Version des NuGet-1.4 stellten wir eine Reihe von Problemen, die wichtig, die behoben wurden.</span><span class="sxs-lookup"><span data-stu-id="04b97-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="04b97-189">Die spezifische Versionsnummer für dieses Update 1.4 ist 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="04b97-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="04b97-190">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="04b97-190">Bug Fixes</span></span>
* <span data-ttu-id="04b97-191">[Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Paket nicht ausgeführt werden `install.ps1` / `uninstall.ps1` in allen Projekten bei mehr als ein Projekt</span><span class="sxs-lookup"><span data-stu-id="04b97-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="04b97-192">[Problem 1156](http://nuget.codeplex.com/workitem/1156): Paket-Manager Computerkonsole hängen unter W2K3/XP (wenn es sich um eine Powershell-2 nicht installiert ist)</span><span class="sxs-lookup"><span data-stu-id="04b97-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>