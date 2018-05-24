---
title: 'Verwenden von NuGet-Paketen: Übersicht und Workflow'
description: Eine Übersicht über das Nutzen von NuGet-Paketen in einem Projekt, die Links zu anderen spezifischen Teilen des Prozesses enthält.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 765b48b474aee17415f53491514bf6e9d50af010
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="7e58e-103">Workflow der Nutzung von Paketen</span><span class="sxs-lookup"><span data-stu-id="7e58e-103">Package consumption workflow</span></span>

<span data-ttu-id="7e58e-104">Zwischen nuget.org und privaten Katalogen für Pakete, die Ihre Organisation möglicherweise erstellt, können Sie eine Vielzahl von nützlichen Paketen finden, die Sie für Ihre Apps und Dienste verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7e58e-104">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="7e58e-105">Unabhängig von der Quelle folgt die Nutzung eines Pakets demselben allgemeinen Workflow.</span><span class="sxs-lookup"><span data-stu-id="7e58e-105">But regardless of the source, consuming a package follows the same general workflow.</span></span>

![Workflow: zur Quelle eines Pakets navigieren, ein Paket suchen, ein Paket in einem Projekt installiert, die using-Anweisung und Aufrufe der Paket-API hinzufügen](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="7e58e-107">\* _Nur Visual Studio und dotnet.ex. Der nuget-Installationsbefehl ändert keine Projektdateien oder packages.config; die Einträge müssen manuell verwaltet werden._</span><span class="sxs-lookup"><span data-stu-id="7e58e-107">\* _Visual Studio and dotnet.ex\` only. The nuget install command does not modify project files or packages.config; entries must be managed manually._</span></span>

<span data-ttu-id="7e58e-108">Weitere Informationen finden Sie unter [Suchen und Auswerten von NuGet-Paketen für Ihr Projekt](../consume-packages/finding-and-choosing-packages.md) und [Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen](ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7e58e-108">For further details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

<span data-ttu-id="7e58e-109">NuGet speichert die Identität und Versionsnummer jedes installierten Pakets entweder in der [`packages.config`](../reference/packages-config.md) oder in der Projektdatei (unter Verwendung von [PackageReference](../consume-packages/package-references-in-project-files.md)), abhängig vom Projekttyp und Ihrer NuGet-Version.</span><span class="sxs-lookup"><span data-stu-id="7e58e-109">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file (using [PackageReference](../consume-packages/package-references-in-project-files.md)), depending on project type and your version of NuGet.</span></span> <span data-ttu-id="7e58e-110">Mit NuGet 4.0+ wird PackageReference bevorzugt, obwohl dies in Visual Studio über die [Paket-Manager-UI-Optionen](../tools/package-manager-ui.md) konfigurierbar ist.</span><span class="sxs-lookup"><span data-stu-id="7e58e-110">With NuGet 4.0+, PackageReference is preferred, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="7e58e-111">Sie können in der entsprechenden Datei jederzeit eine vollständige Liste der Abhängigkeiten für Ihr Projekt anzeigen lassen.</span><span class="sxs-lookup"><span data-stu-id="7e58e-111">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="7e58e-112">Sie müssen die Lizenz für jedes Paket überprüfen, das Sie in Ihrer Software verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="7e58e-112">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="7e58e-113">Auf nuget.org finden Sie auf der rechten Seite der Beschreibungsseite jedes Pakets den Link **License Info** (Lizenzinformationen).</span><span class="sxs-lookup"><span data-stu-id="7e58e-113">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="7e58e-114">Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete verwenden.</span><span class="sxs-lookup"><span data-stu-id="7e58e-114">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="7e58e-115">Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.</span><span class="sxs-lookup"><span data-stu-id="7e58e-115">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="7e58e-116">Bei der Installation eines Pakets überprüft NuGet üblicherweise, ob das Paket bereits aus seinem Cache verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="7e58e-116">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="7e58e-117">Sie können diesen Cache manuell über die Befehlszeile löschen. Dieser Vorgang wird unter [Managing the NuGet cache (Verwalten des NuGet-Caches)](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7e58e-117">You can manually clear this cache from the command line, as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="7e58e-118">NuGet stellt ebenfalls sicher, dass die vom Paket unterstützten Zielframeworks mit Ihrem Projekt kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="7e58e-118">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="7e58e-119">Wenn das Paket keine kompatiblen Assemblys enthält, zeigt NuGet eine Fehlermeldung an.</span><span class="sxs-lookup"><span data-stu-id="7e58e-119">If the package does not contain compatible assemblies, NuGet displays an error.</span></span> <span data-ttu-id="7e58e-120">Weitere Informationen dazu finden Sie unter [Resolving incompatible package errors (Beheben von Fehlern mit inkompatiblen Paketen)](dependency-resolution.md#resolving-incompatible-package-errors).</span><span class="sxs-lookup"><span data-stu-id="7e58e-120">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="7e58e-121">Wenn Sie Projektcode zu einem Quellrepository hinzufügen, schließen Sie üblicherweise keine NuGet-Pakete ein.</span><span class="sxs-lookup"><span data-stu-id="7e58e-121">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="7e58e-122">Personen, die später ein Repository klonen oder auf andere Weise das Projekt erhalten, das Build-Agents auf Systemen wie Visual Studio Team Services enthält, müssen die erforderlichen Pakete wiederherstellen, bevor ein Build ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="7e58e-122">Those who later clone the repository or otherwise acquire the project, including build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![Workflow: NuGet-Pakete wiederherstellen, indem ein Repository geklont wird oder durch Verwenden des restore-Befehls](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="7e58e-124">Die [Paketwiederherstellung](../consume-packages/package-restore.md) verwendet die in der Projektdatei oder `packages.config` enthaltenen Informationen, um alle Abhängigkeiten erneut zu installieren.</span><span class="sxs-lookup"><span data-stu-id="7e58e-124">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="7e58e-125">Beachten Sie, dass es wie in [Abhängigkeitsauflösungen](../consume-packages/dependency-resolution.md) beschrieben Unterschiede zwischen den beteiligten Prozessen gibt.</span><span class="sxs-lookup"><span data-stu-id="7e58e-125">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span> <span data-ttu-id="7e58e-126">Das obige Diagramm zeigt auch keinen Wiederherstellungsbefehl für die Paket-Manager-Konsole, da Sie sich mit der Konsole bereits im Kontext von Visual Studio befinden, das normalerweise Pakete automatisch wiederherstellt und den Befehl auf Lösungsebene wie gezeigt bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="7e58e-126">Also, the diagram above does not show a restore command for the Package Manager Console because you're with the Console you're already in the context of Visual Studio, which typically restores packages automatically and provides the solution-level command as shown.</span></span>

<span data-ttu-id="7e58e-127">Gelegentlich ist es erforderlich, Pakete erneut zu installieren, die bereits in einem Projekt enthalten sind. Dadurch können auch Abhängigkeiten erneut installiert werden.</span><span class="sxs-lookup"><span data-stu-id="7e58e-127">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="7e58e-128">Dazu können Sie einfach den Befehl `nuget reinstall` oder die NuGet-Paket-Manager-Konsole verwenden.</span><span class="sxs-lookup"><span data-stu-id="7e58e-128">This is easy to do using the `nuget reinstall` command or the NuGet Package Manager Console.</span></span> <span data-ttu-id="7e58e-129">Weitere Informationen finden Sie unter [Reinstalling and Updating Packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7e58e-129">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="7e58e-130">Das Verhalten von NuGet wird von den `Nuget.Config`-Dateien gesteuert.</span><span class="sxs-lookup"><span data-stu-id="7e58e-130">Finally, NuGet's behavior is driven by `Nuget.Config` files.</span></span> <span data-ttu-id="7e58e-131">Mehrere Dateien können zum Zentralisieren von bestimmten Eigenschaften auf verschiedenen Ebenen verwendet werden. Weitere Informationen dazu finden Sie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7e58e-131">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="7e58e-132">Nutzen Sie NuGet-Pakete, um produktiv zu programmieren.</span><span class="sxs-lookup"><span data-stu-id="7e58e-132">Enjoy your productive coding with NuGet packages!</span></span>