---
title: "Auswirkungen von „project.json“ auf das Erstellen von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informationen darüber, was die Implementierung von „project.json“ in NuGet 3.x für Paketersteller bedeutet, z.B. nicht unterstützte Features und Paketformate sowie nicht unterstützter Inhalt."
keywords: "NuGet und „project.json“, Auswirkungen von „project.json“, Überlegungen zur Paketerstellung, Features von „project.json“"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="bbceb-104">Auswirkungen von „project.json“ auf das Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="bbceb-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="bbceb-105">Dieser Inhalt ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="bbceb-105">This content is deprecated.</span></span> <span data-ttu-id="bbceb-106">Projekte sollten entweder das Format `packages.config` oder das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="bbceb-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="bbceb-107">Das in NuGet 3 und höher verwendete System `project.json` wirkt sich, wie in den folgenden Abschnitten beschrieben, für Paketersteller auf verschiedene Arten aus.</span><span class="sxs-lookup"><span data-stu-id="bbceb-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="bbceb-108">Änderungen, die das Verwenden vorhandener Pakete betreffen</span><span class="sxs-lookup"><span data-stu-id="bbceb-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="bbceb-109">NuGet-Pakete unterstützen üblicherweise einige Features, die nicht in die transitive Welt übertragen werden.</span><span class="sxs-lookup"><span data-stu-id="bbceb-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="bbceb-110">Installations- und Deinstallationsskripts werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="bbceb-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="bbceb-111">Dem Modell zur transitiven Wiederherstellung, das in einem anderen Artikel im Abschnitt zum Thema [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference) beschrieben wird, ist das Konzept der „Paketinstallationszeit“ nicht bekannt.</span><span class="sxs-lookup"><span data-stu-id="bbceb-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="bbceb-112">Ein Paket ist entweder vorhanden oder nicht vorhanden. Es existiert also kein einheitlicher Prozess, der beim Installieren eines Pakets abläuft.</span><span class="sxs-lookup"><span data-stu-id="bbceb-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="bbceb-113">Des Weiteren wurden Installationsskripts nur in Visual Studio unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bbceb-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="bbceb-114">Andere integrierte Entwicklungsumgebungen konnten nur durch Modellieren der Visual Studio-Erweiterbarkeits-API versuchen, solche Skripts zu unterstützen. In üblichen Editoren und Befehlszeilentools war dagegen keine Unterstützung verfügbar.</span><span class="sxs-lookup"><span data-stu-id="bbceb-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="bbceb-115">Transformationen von Inhalten werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bbceb-115">Content transforms are not supported</span></span>

<span data-ttu-id="bbceb-116">Transformationen werden, ähnlich wie Installationsskripts, mithilfe des Prozesses der Paketinstallation ausgeführt und sind in der Regel nicht idempotent.</span><span class="sxs-lookup"><span data-stu-id="bbceb-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="bbceb-117">Da das Konzept der „Installationszeit“ nicht mehr vorhanden ist, werden XDT Transform und ähnliche Features nicht unterstützt. Diese werden ignoriert, wenn ein entsprechendes Paket in einem transitiven Szenario verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="bbceb-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="bbceb-118">Inhalt</span><span class="sxs-lookup"><span data-stu-id="bbceb-118">Content</span></span>

<span data-ttu-id="bbceb-119">NuGet-Pakete transportieren üblicherweise Inhaltsdateien, z.B. Quellcode- und Konfigurationsdateien.</span><span class="sxs-lookup"><span data-stu-id="bbceb-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="bbceb-120">Diese werden in der Regel in zwei Szenarios verwendet:</span><span class="sxs-lookup"><span data-stu-id="bbceb-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="bbceb-121">Als Startdateien, die im Projekt abgelegt werden, damit der Benutzer diese zu einem späteren Zeitpunkt bearbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="bbceb-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="bbceb-122">Ein gängiges Beispiel dafür sind Standardkonfigurationsdateien.</span><span class="sxs-lookup"><span data-stu-id="bbceb-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="bbceb-123">Inhaltsdateien, die als Ergänzung zu den im Projekt installierten Assemblys verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bbceb-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="bbceb-124">Ein Beispiel dafür wäre ein Logobild, das von einer Assembly verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="bbceb-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="bbceb-125">Die Unterstützung von Inhaltsdateien ist derzeit aus ähnlichen Gründen deaktiviert, wie der für Skripts und Transformationen. Wir arbeiten jedoch bereits an deren Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="bbceb-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="bbceb-126">Inhaltsdateien können weiterhin in Pakete übertragen werden, werden aber derzeit ignoriert. Benutzer können diese dennoch an die richtige Stelle kopieren.</span><span class="sxs-lookup"><span data-stu-id="bbceb-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="bbceb-127">Sie können einen der Vorschläge, wie Inhaltsdateien wieder eingebunden werden könnten, hier einsehen und seinen Fortschritt verfolgen: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="bbceb-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="bbceb-128">Auswirkungen für Paketersteller</span><span class="sxs-lookup"><span data-stu-id="bbceb-128">Impact for package authors</span></span>

<span data-ttu-id="bbceb-129">Pakete, die auf die oben genannten Features zurückgreifen, müssen einen anderen Mechanismus verwenden.</span><span class="sxs-lookup"><span data-stu-id="bbceb-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="bbceb-130">Der in den meisten Fällen für diesen Zweck geeignete Mechanismus wäre „MSBuild-Ziele und -Eigenschaften“, da dieser weiterhin vollständig unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="bbceb-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="bbceb-131">Das Buildsystem kann auch andere Konventionen aus dem Paket übernehmen.</span><span class="sxs-lookup"><span data-stu-id="bbceb-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="bbceb-132">Auf diese Weise werden MSBuild-Ziele sowie Roslyn-Analysetools unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bbceb-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="bbceb-133">Es ist möglich, Pakete zu erstellen, die Ziele und Analysetools für die Szenarios `packages.config` und `project.json` unterstützen.</span><span class="sxs-lookup"><span data-stu-id="bbceb-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="bbceb-134">Pakete, die darauf abzielen, das Projekt zum Erleichtern des Starts zu verändern, können meist nur in wenigen Szenarios verwendet werden. Daher sollten die Pakete stattdessen eine Infodatei oder Richtlinien zum Verwenden des Pakets bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="bbceb-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="bbceb-135">Bei den meisten vorhandenen Paketen ist das Verwenden des unten beschriebenen Paketformats nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="bbceb-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="bbceb-136">Das Format ermöglicht, dass nativer Inhalt in einem erstklassigen Szenario verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="bbceb-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="bbceb-137">Dies bedeutet, dass verwaltete Assemblys davon abhängig sind, dass hardwaregebundene Implementierungen binäre Implementierungen neben verwalteten Assemblys auf Grundlage der Zielplattform liefern.</span><span class="sxs-lookup"><span data-stu-id="bbceb-137">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="bbceb-138">Das Paket „System.IO.Compression“ nutzt diese Technologie beispielsweise.</span><span class="sxs-lookup"><span data-stu-id="bbceb-138">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="bbceb-139">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="bbceb-139">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="bbceb-140">Falls die oben genannte Funktionalität nicht unbedingt erforderlich ist, empfiehlt es sich also, bei dem bestehenden Paketformat zu bleiben, da das hier beschriebene Format nur von NuGet 3.x und höher unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="bbceb-140">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="bbceb-141">Mithilfe von Shims ist es möglich, Pakete zu erstellen, die sowohl in `packages.config`- als auch in `project.json`-Szenarios funktionieren. Jedoch ist es oft leichter, die Pakete auf herkömmliche Weise zu strukturieren – ohne die oben erwähnten veralteten Funktionen.</span><span class="sxs-lookup"><span data-stu-id="bbceb-141">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="bbceb-142">Paketformat „3.x“</span><span class="sxs-lookup"><span data-stu-id="bbceb-142">3.x package format</span></span>

<span data-ttu-id="bbceb-143">Das Paketformat „3.x“ lässt mehrere zusätzliche Funktionen zu, die NuGet 2.x nicht zulässt:</span><span class="sxs-lookup"><span data-stu-id="bbceb-143">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="bbceb-144">Definieren einer Referenzassembly, die für die Kompilierung verwendet wird und mehrerer Implementierungsassemblys, die für die Laufzeit auf verschiedenen Plattformen bzw. Geräten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bbceb-144">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="bbceb-145">Dies ermöglicht es Ihnen, plattformspezifische APIs zu verwenden und zeitgleich für Ihre Benutzer eine gemeinsam genutzte Oberfläche bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="bbceb-145">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="bbceb-146">Dadurch wird Ihnen insbesondere das Schreiben von portablen Zwischenbibliotheken erleichtert.</span><span class="sxs-lookup"><span data-stu-id="bbceb-146">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="bbceb-147">Ermöglicht Paketen, auf Plattformen, z.B. Betriebssystemen oder CPU-Architektur, zu pivotieren</span><span class="sxs-lookup"><span data-stu-id="bbceb-147">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="bbceb-148">Ermöglicht das Trennen von plattformspezifischen Implementierungen, um Pakete in Ergänzungen zu verwandeln</span><span class="sxs-lookup"><span data-stu-id="bbceb-148">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="bbceb-149">Unterstützen nativer Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="bbceb-149">Support Native dependencies as a first class citizen.</span></span>