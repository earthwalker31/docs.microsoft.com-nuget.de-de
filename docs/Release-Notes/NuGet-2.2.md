---
title: NuGet-2.2-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet-2.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="7c5a3-104">NuGet-2.2-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="7c5a3-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="7c5a3-105">[Anmerkungen zur Version des NuGet-2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1-Versionshinweise](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="7c5a3-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="7c5a3-106">NuGet-2.2 wurde 12 Dezember 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="7c5a3-107">Visual Studio-Schnellstart</span><span class="sxs-lookup"><span data-stu-id="7c5a3-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="7c5a3-108">Eine der neuen Funktionen, die in Visual Studio 2012 hinzugefügten war die [Schnellstart Dialogfeld](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="7c5a3-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="7c5a3-109">NuGet-2.2 erweitert dieses Dialogfeld so initialisieren das Dialogfeld "Paket-Manager" mit den Suchbegriffen, die in der Schnellstartleiste eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="7c5a3-110">Beispielsweise enthält ein eingeben "Jquery" in der Schnellstartleiste jetzt eine Option in den Ergebnissen, NuGet-Pakete "Jquery" Übereinstimmung gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet in Visual Studio-Schnellstart](./media/quick-launch.png)

<span data-ttu-id="7c5a3-112">Nach Auswahl dieser Option wird die standardmäßige NuGet-Paket-Manager Suchfunktionen für den Begriff "Jquery" gestartet.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Vorgegebenen NuGet-Paket-Manager-Dialogfeld](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="7c5a3-114">Geben Sie ganze Ordner für den Paketinhalt</span><span class="sxs-lookup"><span data-stu-id="7c5a3-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="7c5a3-115">NuGet-2.2 ermöglicht Ihnen die Angabe für einen ganzen Ordner in jetzt die `<file>` Element von der `.nuspec` Datei, um den Inhalt des Ordners einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="7c5a3-116">Beispielsweise wird Folgendes dazu führen, dass alle Skripts im Ordner "Skripts" das Paket auf den Ordner Contents\scripts hinzugefügt, wenn das Paket in einem Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="7c5a3-117">**Aktualisieren von 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn Sie das Paket zu installieren.**</span><span class="sxs-lookup"><span data-stu-id="7c5a3-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="7c5a3-118">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="7c5a3-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="7c5a3-119">Paketinstallation für f#-Projekten schlägt fehl, wenn mit der Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="7c5a3-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="7c5a3-120">Beim Versuch, ein NuGet-Paket in ein f#-Projekt mit der Paket-Manager-Konsole zu installieren, wird eine InvalidOperationException ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="7c5a3-121">Wir arbeiten mit dem f#-Team das Problem zu beheben, aber in der Zwischenzeit behelfslösung ist das NuGet-Pakete in F#-Projekte über das Dialogfeld "NuGet Paket-Manager" statt der Konsole zu installieren.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="7c5a3-122">[Weitere Informationen finden Sie auf der CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="7c5a3-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="7c5a3-123">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="7c5a3-123">Bug Fixes</span></span>
<span data-ttu-id="7c5a3-124">NuGet-2.2 enthält zahlreiche Programmfehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="7c5a3-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="7c5a3-125">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet-2.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="7c5a3-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>