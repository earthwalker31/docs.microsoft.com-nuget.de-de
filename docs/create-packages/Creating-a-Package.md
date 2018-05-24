---
title: Erstellen eines NuGet-Pakets
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: c1e3bfd1c7e80c7deb505ef732d73c2edf3e32f7
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="48e2d-103">Erstellen von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="48e2d-103">Creating NuGet packages</span></span>

<span data-ttu-id="48e2d-104">Unabhängig davon, was Ihr Paket macht oder welchen Code es enthält, können Sie die Funktionalität mit `nuget.exe` in eine Komponente packen, die für andere Entwickler freigegeben und von ihnen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="48e2d-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="48e2d-105">Weitere Informationen zum Installieren von `nuget.exe` finden Sie unter [Install NuGet CLI (Installieren der NuGet-CLI)](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="48e2d-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="48e2d-106">Beachten Sie, dass `nuget.exe` nicht automatisch in Visual Studio enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="48e2d-107">Technisch gesehen ist ein NuGet-Paket eine ZIP-Datei, die mit der `.nupkg`-Erweiterung umbenannt wurde und deren Inhalt bestimmten Konventionen entspricht.</span><span class="sxs-lookup"><span data-stu-id="48e2d-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="48e2d-108">In diesem Thema werden die Schritte zum Erstellen eines Pakets, das diesen Konventionen entspricht, ausführlich beschrieben.</span><span class="sxs-lookup"><span data-stu-id="48e2d-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="48e2d-109">Eine fokussierte exemplarische Vorgehensweise finden Sie unter [Quickstart: Create and Publish a Package (Schnellstart: Erstellen und Veröffentlichen eines Pakets)](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="48e2d-110">Das Packen beginnt mit dem kompilierten Code (Assemblys), Symbolen und/oder anderen Dateien, die Sie als Paket übermitteln möchten. Weitere Informationen finden Sie unter [Overview and workflow (Übersicht und Workflow)](overview-and-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="48e2d-111">Dieser Vorgang wird unabhängig vom Kompilieren oder jeder anderen Methode zum Erstellen der Dateien ausgeführt, die in das Paket einfließen. Sie können die kompilierten Assemblys und Pakete jedoch mithilfe der Informationen in einer Projektdatei kontinuierlich synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="48e2d-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="48e2d-112">Dieses Thema gilt nicht für .NET Core-Projekte, in denen Visual Studio 2017 und NuGet 4.0 und höher verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="48e2d-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="48e2d-113">In diesen .NET-Projekten verwendet NuGet die Informationen direkt in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="48e2d-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="48e2d-114">Weitere Informationen finden Sie unter [Create .NET Standard Packages with Visual Studio 2017 (Erstellen von .NET Standard-Paketen mit Visual Studio 2017)](../guides/create-net-standard-packages-vs2017.md) und [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="48e2d-115">Welche Assemblys sollen gepackt werden?</span><span class="sxs-lookup"><span data-stu-id="48e2d-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="48e2d-116">Die meisten allgemeinen Pakete enthalten mindestens eine Assembly, die andere Entwickler in ihren eigenen Projekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="48e2d-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="48e2d-117">Es ist empfehlenswert, in jedem NuGet-Paket eine Assembly zu haben, vorausgesetzt, dass jede Assembly für sich nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="48e2d-118">Beispiel: Wenn `Utilities.dll` von `Parser.dll` abhängt und `Parser.dll` für sich allein bereits nützlich ist, dann müssen Sie für jede Datei ein eigenes Paket erstellen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="48e2d-119">So können Entwickler `Parser.dll` unabhängig von `Utilities.dll` verwenden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="48e2d-120">Wenn Ihre Bibliothek aus mehreren Assemblys besteht, die für sich allein nicht nützlich sind, können diese in einem Paket zusammengefasst werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="48e2d-121">Bleiben wir beim vorherigen Beispiel: Wenn `Parser.dll` Code enthält, der nur von `Utilities.dll` verwendet wird, kann `Parser.dll` in dasselbe Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="48e2d-122">Auch `Utilities.dll` und `Utilities.resources.dll` können im selben Paket zusammengefasst werden, wenn erstere DLL von der letzteren abhängt und die letztere nicht für sich allein nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="48e2d-123">Ressourcen hingegen sind ein besonderer Fall.</span><span class="sxs-lookup"><span data-stu-id="48e2d-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="48e2d-124">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch den DLLs des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind, werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Weitere Informationen finden Sie unter [Creating localized NuGet packages (Erstellen lokalisierter NuGet-Pakete)](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="48e2d-125">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="48e2d-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="48e2d-126">Wenn Ihre Bibliothek COM-Interop-Assemblys enthält, führen Sie die zusätzlichen Schritte unter [Erstellen von Paketen, die COM-Interop-Assemblys enthalten](#authoring-packages-with-com-interop-assemblies) aus.</span><span class="sxs-lookup"><span data-stu-id="48e2d-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="48e2d-127">Rolle und Struktur der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="48e2d-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="48e2d-128">Nachdem Sie entschieden haben, welche Dateien gepackt werden sollen, erstellen Sie ein Paketmanifest in einer `.nuspec`-XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="48e2d-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="48e2d-129">Das Manifest:</span><span class="sxs-lookup"><span data-stu-id="48e2d-129">The manifest:</span></span>

1. <span data-ttu-id="48e2d-130">Beschreibt den Inhalt des Pakets und ist im Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="48e2d-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="48e2d-131">Ist unerlässlich für die Erstellung des Pakets und weist NuGet an, wie das Paket in ein Projekt installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="48e2d-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="48e2d-132">Das Manifest erkennt z.B. andere Paketabhängigkeiten, sodass NuGet bei der Installation des Hauptpakets auch diese installieren kann.</span><span class="sxs-lookup"><span data-stu-id="48e2d-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="48e2d-133">Enthält wie unten beschrieben erforderliche und optionale Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="48e2d-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="48e2d-134">Weitere Informationen, einschließlich anderer Eigenschaften, die hier nicht erwähnt werden, finden Sie unter [.nuspec reference (NUSPEC-Referenz)](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="48e2d-135">Erforderliche Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="48e2d-135">Required properties:</span></span>

- <span data-ttu-id="48e2d-136">Der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="48e2d-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="48e2d-137">Eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]*, wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden</span><span class="sxs-lookup"><span data-stu-id="48e2d-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="48e2d-138">Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte</span><span class="sxs-lookup"><span data-stu-id="48e2d-138">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="48e2d-139">Informationen zum Autor und zum Besitzer</span><span class="sxs-lookup"><span data-stu-id="48e2d-139">Author and owner information.</span></span>
- <span data-ttu-id="48e2d-140">Eine ausführliche Beschreibung des Pakets</span><span class="sxs-lookup"><span data-stu-id="48e2d-140">A long description of the package.</span></span>

<span data-ttu-id="48e2d-141">Allgemeine optionale Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="48e2d-141">Common optional properties:</span></span>

- <span data-ttu-id="48e2d-142">Anmerkungen zu diesem Release</span><span class="sxs-lookup"><span data-stu-id="48e2d-142">Release notes</span></span>
- <span data-ttu-id="48e2d-143">Copyrightinformationen</span><span class="sxs-lookup"><span data-stu-id="48e2d-143">Copyright information</span></span>
- <span data-ttu-id="48e2d-144">Eine kurze Beschreibung der [Paket-Manager-UI in Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="48e2d-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="48e2d-145">Eine Gebietsschema-ID</span><span class="sxs-lookup"><span data-stu-id="48e2d-145">A locale ID</span></span>
- <span data-ttu-id="48e2d-146">URL der Startseite und der Lizenz</span><span class="sxs-lookup"><span data-stu-id="48e2d-146">Home page and license URLs</span></span>
- <span data-ttu-id="48e2d-147">Eine URL für das Symbol</span><span class="sxs-lookup"><span data-stu-id="48e2d-147">An icon URL</span></span>
- <span data-ttu-id="48e2d-148">Listen der Abhängigkeiten und Verweise</span><span class="sxs-lookup"><span data-stu-id="48e2d-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="48e2d-149">Tags für die Katalogsuche</span><span class="sxs-lookup"><span data-stu-id="48e2d-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="48e2d-150">Im folgenden Beispiel sehen Sie eine typische, aber fiktive `.nuspec`-Datei mit Kommentaren, die die Eigenschaften beschreiben:</span><span class="sxs-lookup"><span data-stu-id="48e2d-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="48e2d-151">Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="48e2d-152">Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `include` und `exclude` des Elements `dependency` direkt im Paket verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="48e2d-153">Informationen dazu finden Sie unter [.nuspec Reference – Dependencies (NUSPEC-Referenz: Abhängigkeiten)](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="48e2d-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="48e2d-154">Da das Manifest im Paket enthalten ist, aus dem es erstellt wurde, finden Sie viele weitere Beispiele in den vorhandenen Paketen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="48e2d-155">Eine gute Quelle ist z.B. der Ordner *global-packages* auf Ihrem Computer, der sich mithilfe des folgenden Befehls öffnen lässt:</span><span class="sxs-lookup"><span data-stu-id="48e2d-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="48e2d-156">Wechseln Sie in einen Ordner unter *package\version*, kopieren die `.nupkg`- in eine `.zip`-Datei, öffnen Sie dann die `.zip`-Datei, und sehen Sie sich die `.nuspec`-Datei darin an.</span><span class="sxs-lookup"><span data-stu-id="48e2d-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="48e2d-157">Wenn Sie eine `.nuspec`-Datei aus einem Visual Studio-Projekt erstellen, enthält das Manifest Tokens, die bei der Paketerstellung durch Informationen aus dem Projekt ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="48e2d-158">Weitere Informationen finden Sie im Abschnitt [Aus einem Visual Studio-Projekt](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="48e2d-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="48e2d-159">Erstellen der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="48e2d-159">Creating the .nuspec file</span></span>

<span data-ttu-id="48e2d-160">Das Erstellen eines vollständigen Manifests beginnt in der Regel mit einer einfachen `.nuspec`-Datei, die mithilfe einer der folgenden Methoden generiert wird:</span><span class="sxs-lookup"><span data-stu-id="48e2d-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="48e2d-161">einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="48e2d-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="48e2d-162">einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="48e2d-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="48e2d-163">einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="48e2d-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="48e2d-164">einer neuen Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="48e2d-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="48e2d-165">Anschließend bearbeiten Sie die Datei manuell, sodass sie den genauen Inhalt beschreibt, den das letzte Paket enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="48e2d-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="48e2d-166">Generierte `.nuspec`-Dateien enthalten Platzhalter. Diese müssen geändert werden, bevor das Paket mit dem Befehl `nuget pack` erstellt wird,</span><span class="sxs-lookup"><span data-stu-id="48e2d-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="48e2d-167">da dieser fehlschlägt, wenn die `.nuspec`-Datei Platzhalter enthält.</span><span class="sxs-lookup"><span data-stu-id="48e2d-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="48e2d-168">Aus einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="48e2d-168">From a convention-based working directory</span></span>

<span data-ttu-id="48e2d-169">Da ein NuGet-Paket nur eine mit der `.nupkg`-Erweiterung umbenannte ZIP-Datei ist, ist es oftmals am einfachsten, die gewünschte Ordnerstruktur im Dateisystem und die `.nuspec`-Datei anschließend direkt aus dieser Struktur zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="48e2d-170">Der Befehl `nuget pack` fügt dann automatisch alle Dateien in dieser Ordnerstruktur ein (außer den Ordnern, die mit einem `.` beginnen, sodass private Dateien in der gleichen Struktur bleiben können).</span><span class="sxs-lookup"><span data-stu-id="48e2d-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="48e2d-171">Der Vorteil dieses Ansatzes ist, dass Sie nicht wie weiter unten in diesem Thema erläutert im Manifest angeben müssen, welche Dateien im Paket enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="48e2d-172">Sie können einfach beim Buildprozess die genaue Ordnerstruktur für das Paket erstellen lassen und problemlos weitere Dateien aufnehmen, die andernfalls zu keinem Projekt gehören würden:</span><span class="sxs-lookup"><span data-stu-id="48e2d-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="48e2d-173">Inhalt und Quellcode, der in das Zielprojekt eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="48e2d-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="48e2d-174">PowerShell-Skripts (in NuGet 2.x verwendete Pakete können auch Installationsskripts enthalten, die in NuGet 3.x und höher nicht unterstützt werden).</span><span class="sxs-lookup"><span data-stu-id="48e2d-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="48e2d-175">Transformationen in vorhandene Konfigurations- und Quellcodedateien in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="48e2d-176">Die Ordnerkonventionen lauten folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="48e2d-177">Ordner</span><span class="sxs-lookup"><span data-stu-id="48e2d-177">Folder</span></span> | <span data-ttu-id="48e2d-178">description</span><span class="sxs-lookup"><span data-stu-id="48e2d-178">Description</span></span> | <span data-ttu-id="48e2d-179">Aktion bei der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="48e2d-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48e2d-180">(Stammverzeichnis)</span><span class="sxs-lookup"><span data-stu-id="48e2d-180">(root)</span></span> | <span data-ttu-id="48e2d-181">Speicherort für „readme.txt“</span><span class="sxs-lookup"><span data-stu-id="48e2d-181">Location for readme.txt</span></span> | <span data-ttu-id="48e2d-182">In Visual Studio wird die Datei „readme.txt“ im Stammverzeichnis des Pakets angezeigt, wenn das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="48e2d-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="48e2d-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="48e2d-183">lib/{tfm}</span></span> | <span data-ttu-id="48e2d-184">Assembly- (`.dll`), Dokumentations- (`.xml`) und Symboldateien (`.pdb`) für den angegebenen Zielframeworkmoniker (Target Framework Moniker, TFM)</span><span class="sxs-lookup"><span data-stu-id="48e2d-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="48e2d-185">Assemblys werden als Verweise hinzugefügt, und `.xml` sowie `.pdb` werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="48e2d-185">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="48e2d-186">Informationen zum Erstellen von für das Zielframework spezifischen Unterordnern finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="48e2d-187">Laufzeiten</span><span class="sxs-lookup"><span data-stu-id="48e2d-187">runtimes</span></span> | <span data-ttu-id="48e2d-188">Architekturspezifische Assembly- (`.dll`), Symbol- (`.pdb`) und native Ressourcendateien (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="48e2d-188">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="48e2d-189">Assemblys werden als Verweise hinzugefügt. Andere Dateien werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="48e2d-189">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="48e2d-190">Weitere Informationen finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-190">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="48e2d-191">Inhalt</span><span class="sxs-lookup"><span data-stu-id="48e2d-191">content</span></span> | <span data-ttu-id="48e2d-192">Beliebige Dateien</span><span class="sxs-lookup"><span data-stu-id="48e2d-192">Arbitrary files</span></span> | <span data-ttu-id="48e2d-193">Inhalte werden in das Projektstammverzeichnis kopiert.</span><span class="sxs-lookup"><span data-stu-id="48e2d-193">Contents are copied to the project root.</span></span> <span data-ttu-id="48e2d-194">Der Ordner **content** (Inhalt) entspricht in etwa dem Stammverzeichnis der Zielanwendung, die das Paket letztendlich nutzt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-194">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="48e2d-195">Damit das Paket dem Ordner */images* der Anwendung ein Image hinzufügt, müssen Sie es im Ordner *content/images* ablegen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-195">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="48e2d-196">Build</span><span class="sxs-lookup"><span data-stu-id="48e2d-196">build</span></span> | <span data-ttu-id="48e2d-197">MSBuild-Dateien `.targets` und `.props`</span><span class="sxs-lookup"><span data-stu-id="48e2d-197">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="48e2d-198">Sie werden automatisch in die Projektdatei oder in `project.lock.json` (NuGet 3.x und höher) eingefügt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-198">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="48e2d-199">Tools</span><span class="sxs-lookup"><span data-stu-id="48e2d-199">tools</span></span> | <span data-ttu-id="48e2d-200">PowerShell-Skripts und -Programme, auf die über die Paket-Manager-Konsole zugegriffen werden kann</span><span class="sxs-lookup"><span data-stu-id="48e2d-200">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="48e2d-201">Der Ordner `tools` wird nur zur Umgebungsvariable `PATH` der Paket-Manager-Konsole hinzugefügt, *niemals* jedoch zu `PATH`, so wie es für MSBuild beim Erstellen des Projekts festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-201">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="48e2d-202">Da die Ordnerstruktur beliebig viele Assemblys für beliebig viele Zielframeworks enthalten kann, ist diese Methode für das Erstellen von Paketen erforderlich, die mehrere Frameworks unterstützen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-202">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="48e2d-203">Sobald Sie die gewünschte Ordnerstruktur eingerichtet haben, führen Sie den folgenden Befehl in diesem Ordner aus, um die `.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-203">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="48e2d-204">Die generierte `.nuspec`-Datei enthält wie bereits erwähnt keine expliziten Verweise auf Dateien in der Ordnerstruktur.</span><span class="sxs-lookup"><span data-stu-id="48e2d-204">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="48e2d-205">NuGet schließt bei der Paketerstellung automatisch alle Dateien ein.</span><span class="sxs-lookup"><span data-stu-id="48e2d-205">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="48e2d-206">Die Platzhalterwerte müssen jedoch trotzdem noch in anderen Teilen des Manifests bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-206">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="48e2d-207">Aus einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="48e2d-207">From an assembly DLL</span></span>

<span data-ttu-id="48e2d-208">Das Erstellen eines Pakets aus einer Assembly ist ein einfacher Vorgang. Dabei können Sie eine `.nuspec`-Datei aus den Metadaten in der Assembly mithilfe des folgenden Befehls generieren:</span><span class="sxs-lookup"><span data-stu-id="48e2d-208">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="48e2d-209">Bei dieser Schreibweise werden einige Platzhalter im Manifest durch bestimmte Werte aus der Assembly ersetzt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-209">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="48e2d-210">Die Eigenschaft `<id>` wird beispielsweise auf den Assemblynamen festgelegt und `<version>` auf die Version.</span><span class="sxs-lookup"><span data-stu-id="48e2d-210">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="48e2d-211">Andere Manifesteigenschaften haben jedoch keine übereinstimmenden Werte in der Assembly und enthalten somit weiterhin Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="48e2d-211">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="48e2d-212">Aus einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="48e2d-212">From a Visual Studio project</span></span>

<span data-ttu-id="48e2d-213">Es empfiehlt sich, eine `.nuspec`-Datei aus einer `.csproj`- oder `.vbproj`-Datei zu erstellen, da auf andere Pakete, die in dieses Projekt installiert wurden, automatisch als Abhängigkeiten verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="48e2d-213">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="48e2d-214">Verwenden Sie einfach den folgenden Befehl im Ordner der Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="48e2d-214">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="48e2d-215">Die anschließend erstellte `<project-name>.nuspec`-Datei enthält *Tokens*, die zur Packzeit durch Werte aus dem Projekt ersetzt werden, einschließlich der Verweise auf alle anderen Pakete, die bereits installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-215">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="48e2d-216">Ein Token wird auf beiden Seiten der Projekteigenschaft durch das Symbol `$` begrenzt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-216">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="48e2d-217">Wird der Wert `<id>` auf diese Weise in einem Manifest generiert, wird er in der Regel folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="48e2d-217">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="48e2d-218">Dieses Token wird zur Packzeit durch den Wert `AssemblyName` aus der Projektdatei ersetzt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-218">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="48e2d-219">Weitere Informationen zur genauen Zuordnung von Projektwerten und `.nuspec`-Tokens finden Sie im Abschnitt [Replacement tokens (Ersetzungstokens)](../reference/nuspec.md#replacement-tokens) im Artikel „.nuspec reference“ (NUSPEC-Referenz).</span><span class="sxs-lookup"><span data-stu-id="48e2d-219">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="48e2d-220">Durch Tokens müssen Sie wichtige Werte wie die Versionsnummer in der `.nuspec`-Datei nicht mit dem Projekt zusammen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="48e2d-220">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="48e2d-221">Sie können die Tokens bei Bedarf jederzeit durch Literalwerte ersetzen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-221">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="48e2d-222">Wenn Sie in einem Visual Studio-Projekt arbeiten, haben weitere Packoptionen zur Auswahl. Dies wird weiter unten im Abschnitt [Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei](#running-nuget-pack-to-generate-the-nupkg-file) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="48e2d-222">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="48e2d-223">Pakete auf Projektmappenebene</span><span class="sxs-lookup"><span data-stu-id="48e2d-223">Solution-level packages</span></span>

<span data-ttu-id="48e2d-224">*Nur NuGet 2.x. Nicht verfügbar in NuGet 3.0 und höher.*</span><span class="sxs-lookup"><span data-stu-id="48e2d-224">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="48e2d-225">In NuGet 2.x werden Pakete auf Projektmappenebene unterstützt, über die Tools oder zusätzliche Befehle für die Paket-Manager-Konsole installiert werden (der Inhalt des Ordners `tools`), die jedoch weder Verweise noch Inhalt hinzufügen oder Anpassungen für Projekte in der Projektmappe erstellen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-225">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="48e2d-226">Solche Pakete enthalten keine Dateien in den direkten Ordnern `lib`, `content` oder `build`, und keine der dazugehörigen Abhängigkeiten besitzt Dateien in den jeweiligen `lib`-, `content`- oder `build`-Ordnern.</span><span class="sxs-lookup"><span data-stu-id="48e2d-226">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="48e2d-227">NuGet verfolgt installierte Pakete auf Projektmappenebene in einer `packages.config`-Datei im Ordner `.nuget` nach, statt in der `packages.config`-Datei des Projekts.</span><span class="sxs-lookup"><span data-stu-id="48e2d-227">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="48e2d-228">Neue Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="48e2d-228">New file with default values</span></span>

<span data-ttu-id="48e2d-229">Mit dem folgenden Befehl wird ein Standardmanifest mit Platzhaltern erstellt, das gewährleistet, dass Sie mit der richtigen Dateistruktur beginnen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-229">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="48e2d-230">Wenn Sie \<package-name\> weglassen, lautet die Ergebnisdatei `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-230">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="48e2d-231">Wenn Sie einen Namen wie `Contoso.Utility.UsefulStuff` angeben, lautet die Datei `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-231">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="48e2d-232">Die resultierende `.nuspec`-Datei enthält Platzhalter für Werte wie `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-232">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="48e2d-233">Denken Sie daran, die Datei zu bearbeiten, bevor Sie mit ihr die endgültige `.nupkg`-Datei erstellen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-233">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="48e2d-234">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="48e2d-234">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="48e2d-235">Der Paketbezeichner (`<id>`-Element) und die Versionsnummer (`<version>`-Element) sind die beiden wichtigsten Werte im Manifest, da sie eindeutig den exakten Code bezeichnen, der im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-235">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="48e2d-236">**Bewährte Methoden für den Paketbezeichner:**</span><span class="sxs-lookup"><span data-stu-id="48e2d-236">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="48e2d-237">**Eindeutigkeit:** Der Bezeichner muss auf „nuget.org“ bzw. in dem Katalog, in dem das Paket gehostet wird, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="48e2d-237">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="48e2d-238">Bevor Sie sich für einen Bezeichner entscheiden, vergewissern Sie sich, dass dieser im entsprechenden Katalog nicht bereits verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="48e2d-238">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="48e2d-239">Zur Vermeidung von Konflikten empfiehlt es sich, den Namen Ihres Unternehmens im ersten Teil des Bezeichners zu nutzen, z.B. `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-239">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="48e2d-240">**Namespace-ähnliche Namen:** Verwenden Sie Punkte statt Bindestrichen, wie bei der Notation von Namespaces in .NET.</span><span class="sxs-lookup"><span data-stu-id="48e2d-240">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="48e2d-241">Schreiben Sie z.B. `Contoso.Utility.UsefulStuff` statt `Contoso-Utility-UsefulStuff` oder `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-241">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="48e2d-242">Benutzer finden es auch hilfreich, wenn der Paketbezeichner den im Code verwendeten Namespaces entspricht.</span><span class="sxs-lookup"><span data-stu-id="48e2d-242">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="48e2d-243">**Beispielpakete:** Wenn Sie ein Paket mit Beispielcode erstellen, das veranschaulicht, wie ein anderes Paket verwenden, fügen Sie `.Sample` als Suffix an den Bezeichner an, z.B. `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-243">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="48e2d-244">Das Beispielpaket würde natürlich vom anderen Paket abhängen. Verwenden Sie beim Erstellen eines Beispielpakets wie weiter oben beschrieben das konventionsbasierte Arbeitsverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="48e2d-244">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="48e2d-245">Arrangieren Sie den Beispielcode im Ordner `content` in einem Ordner namens `\Samples\<identifier>`, z.B. `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-245">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="48e2d-246">**Bewährte Methoden für die Paketversion:**</span><span class="sxs-lookup"><span data-stu-id="48e2d-246">**Best practices for the package version:**</span></span>

- <span data-ttu-id="48e2d-247">Legen Sie die Version des Pakets auf die der Bibliothek fest, obwohl dies nicht zwingend erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-247">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="48e2d-248">Dies ist sehr einfach, wenn Sie ein Paket, wie zuvor im Abschnitt [Welche Assemblys sollen gepackt werden?](#deciding-which-assemblies-to-package) beschrieben, auf eine einzelne Assembly beschränken.</span><span class="sxs-lookup"><span data-stu-id="48e2d-248">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="48e2d-249">Bedenken Sie, dass NuGet sich beim Auflösen der Abhängigkeiten nach den Paketversionen richtet, nicht nach den Assemblyversionen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-249">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="48e2d-250">Wenn Sie ein nicht standardmäßiges Versionsschema verwenden, müssen Sie die NuGet-Versionsregeln wie unter [Package versioning (Paketversionsverwaltung](../reference/package-versioning.md) beschrieben anwenden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-250">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="48e2d-251">Die folgenden kurzen Blogbeiträge enthalten weitere Informationen zur Versionsverwaltung:</span><span class="sxs-lookup"><span data-stu-id="48e2d-251">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="48e2d-252">Part 1: Taking on DLL Hell (Teil 1: DLLs)</span><span class="sxs-lookup"><span data-stu-id="48e2d-252">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="48e2d-253">Part 2: The core algorithm (Teil 2: Der Kernalgorithmus)</span><span class="sxs-lookup"><span data-stu-id="48e2d-253">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="48e2d-254">Part 3: Unification via Binding Redirects (Teil 3: Vereinheitlichung über Bindungsumleitungen)</span><span class="sxs-lookup"><span data-stu-id="48e2d-254">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="48e2d-255">Festlegen eines Pakettyps</span><span class="sxs-lookup"><span data-stu-id="48e2d-255">Setting a package type</span></span>

<span data-ttu-id="48e2d-256">In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben.</span><span class="sxs-lookup"><span data-stu-id="48e2d-256">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="48e2d-257">Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-257">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="48e2d-258">Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="48e2d-258">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="48e2d-259">Pakete mit Typ `DotnetCliTool` sind Erweiterungen der [.NET-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-259">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="48e2d-260">Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge.</span><span class="sxs-lookup"><span data-stu-id="48e2d-260">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="48e2d-261">Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="48e2d-261">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="48e2d-262">Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-262">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="48e2d-263">Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetCliTool`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-263">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="48e2d-264">Pakettypen werden in der `.nuspec`-Datei festgelegt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-264">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="48e2d-265">Für die Abwärtskompatibilität wird empfohlen, den `Dependency`-Typ *nicht* explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-265">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="48e2d-266">`.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:</span><span class="sxs-lookup"><span data-stu-id="48e2d-266">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="48e2d-267">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="48e2d-267">Adding a readme and other files</span></span>

<span data-ttu-id="48e2d-268">Verwenden Sie den `<files>`-Knoten in der `.nuspec`-Datei, die dem `<metadata>`-Tag *folgt*, um Dateien, die in das Paket aufgenommen werden sollen, direkt anzugeben:</span><span class="sxs-lookup"><span data-stu-id="48e2d-268">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="48e2d-269">Bei einem konventionsbasierten Arbeitsverzeichnis können Sie die Datei „readme.txt“ im Stammverzeichnis des Pakets und andere Inhalte im Ordner `content` platzieren.</span><span class="sxs-lookup"><span data-stu-id="48e2d-269">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="48e2d-270">Dazu sind keine `<file>`-Elemente im Manifest erforderlich.</span><span class="sxs-lookup"><span data-stu-id="48e2d-270">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="48e2d-271">Wenn Sie eine Datei namens `readme.txt` im Stammverzeichnis des Pakets einschließen, zeigt Visual Studio unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an.</span><span class="sxs-lookup"><span data-stu-id="48e2d-271">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="48e2d-272">Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-272">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="48e2d-273">Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="48e2d-273">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="48e2d-275">Wenn Sie einen leeren `<files>`-Knoten in die `.nuspec`-Datei einschließen, fügt NuGet dem Paket keine weiteren Inhalte außer denen im Ordner `lib` hinzu.</span><span class="sxs-lookup"><span data-stu-id="48e2d-275">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="48e2d-276">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="48e2d-276">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="48e2d-277">In einigen Fällen (z.B. beim Ausführen eines benutzerdefinierten Tools oder Prozesses während des Buildvorgangs) sollten Sie benutzerdefinierte Buildziele oder -eigenschaften zu Projekten hinzufügen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-277">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="48e2d-278">Platzieren Sie dazu Dateien mit der Schreibweise `<package_id>.targets` oder `<package_id>.props` (z.B. `Contoso.Utility.UsefulStuff.targets`) im `\build`-Ordner des Projekts.</span><span class="sxs-lookup"><span data-stu-id="48e2d-278">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="48e2d-279">Dateien im `\build`-Stammverzeichnis gelten als für alle Zielframeworks geeignet.</span><span class="sxs-lookup"><span data-stu-id="48e2d-279">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="48e2d-280">Um frameworkspezifische Dateien bereitzustellen, platzieren Sie zuerst Dateien wie die folgenden in den entsprechenden Unterordnern:</span><span class="sxs-lookup"><span data-stu-id="48e2d-280">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="48e2d-281">Verweisen Sie dann in der `.nuspec`-Datei im `<files>`-Knoten auf diese Dateien:</span><span class="sxs-lookup"><span data-stu-id="48e2d-281">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="48e2d-282">Das Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket wurde [mit NuGet 2.5 eingeführt](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). Daher wird empfohlen, dem Element `metadata` das `minClientVersion="2.5"`-Attribut hinzuzufügen, damit die für das Paket erforderliche Mindestversion des NuGet-Clients angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="48e2d-282">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="48e2d-283">Wenn NuGet ein Paket mit `\build`-Dateien erstellt, werden der Projektdatei MSBuild-`<Import>`-Elemente hinzufügt, die auf die `.targets`- und `.props`-Dateien zeigen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-283">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="48e2d-284">`.props` wird oben in der Projektdatei hinzugefügt und `.targets` ganz unten. Für jedes Zielframework wird ein eigenes bedingtes MSBuild-`<Import>`-Element hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-284">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="48e2d-285">MSBuild-`.props`- und -`.targets`-Dateien für frameworkübergreifende Ziele können im Ordner `\buildCrossTargeting` abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-285">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="48e2d-286">Bei der Paketinstallation fügt NuGet die entsprechenden `<Import>`-Elemente in die Projektdatei mit der Bedingung ein, dass das Zielframework nicht festgelegt ist (die MSBuild-Eigenschaft `$(TargetFramework)` muss leer sein).</span><span class="sxs-lookup"><span data-stu-id="48e2d-286">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="48e2d-287">In NuGet 3.x werden Ziele nicht zum Projekt hinzugefügt, sondern über `project.lock.json` zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-287">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="48e2d-288">Erstellen von Paketen, die COM-Interop-Assemblys enthalten</span><span class="sxs-lookup"><span data-stu-id="48e2d-288">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="48e2d-289">Pakete, die COM-Interop-Assemblys enthalten, müssen eine entsprechende [Zieledatei](#including-msbuild-props-and-targets-in-a-package) enthalten, damit die richtigen `EmbedInteropTypes`-Metadaten zu Projekten hinzugefügt werden, die das Format „PackageReference“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-289">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="48e2d-290">Die `EmbedInteropTypes`-Metadaten sind für alle Assemblys immer FALSE, wenn „PackageReference“ verwendet wird, damit die Zieledatei diese Metadaten explizit hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-290">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="48e2d-291">Um Konflikte zu vermeiden, sollte der Name des Ziels eindeutig sein. Verwenden Sie am besten eine Kombination aus dem Paketnamen und der Assembly, die eingebettet wird, und ersetzen Sie `{InteropAssemblyName}` im folgenden Beispiel durch diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="48e2d-291">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="48e2d-292">Ein weiteres Beispiel finden Sie unter [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).</span><span class="sxs-lookup"><span data-stu-id="48e2d-292">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="48e2d-293">Hinweis: Wenn Sie das `packages.config`-Verwaltungsformat verwenden, prüfen NuGet und Visual Studio beim Hinzufügen von Verweisen zu den Assemblys aus Paketen auf COM-Interop-Assemblys und legen `EmbedInteropTypes` in der Projektdatei auf TRUE fest.</span><span class="sxs-lookup"><span data-stu-id="48e2d-293">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="48e2d-294">In diesem Fall werden die Ziele überschrieben.</span><span class="sxs-lookup"><span data-stu-id="48e2d-294">In this case the targets are overriden.</span></span>

<span data-ttu-id="48e2d-295">Darüber hinaus werden die [Buildressourcen standardmäßig nicht transitiv weitergeben](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="48e2d-295">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="48e2d-296">Pakete, die dieser Beschreibung nach erstellt werden, funktionieren anders, wenn sie als transitive Abhängigkeit aus einem Projekt in einen Projektverweis gezogen werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-296">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="48e2d-297">Der Paketbenutzer kann die Weiterleitung zulassen, indem er den Standardwert „PrivateAssets“ so ändert, dass „build“ nicht enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-297">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="48e2d-298">Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei</span><span class="sxs-lookup"><span data-stu-id="48e2d-298">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="48e2d-299">Wenn Sie eine Assembly oder das konventionsbasierte Arbeitsverzeichnis verwenden, erstellen Sie ein Paket, indem Sie den Befehl `nuget pack` mit der `.nuspec`-Datei ausführen und dabei `<manifest-name>` durch den bestimmten Dateinamen ersetzen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-299">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="48e2d-300">Wenn Sie ein Visual Studio-Projekt verwenden, führen Sie `nuget pack` mit der Projektdatei aus, die automatisch die `.nuspec`-Datei des Projekts lädt und alle Tokens darin durch die Werte in der Projektdatei ersetzt:</span><span class="sxs-lookup"><span data-stu-id="48e2d-300">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="48e2d-301">Die direkte Verwendung der Projektdatei ist für die Tokenersetzung erforderlich, da das Projekt die Quelle der Tokenwerte ist.</span><span class="sxs-lookup"><span data-stu-id="48e2d-301">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="48e2d-302">Die Tokenersetzung wird nicht ausgeführt, wenn Sie `nuget pack` mit einer `.nuspec`-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-302">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="48e2d-303">`nuget pack` schließt auf jeden Fall Ordner aus, die mit einem Punkt beginnen, z.B. `.git` oder `.hg`.</span><span class="sxs-lookup"><span data-stu-id="48e2d-303">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="48e2d-304">NuGet gibt an, ob die `.nuspec`-Datei Fehler enthält, die korrigiert werden müssen, z.B. nicht geänderte Platzhalterwerte im Manifest.</span><span class="sxs-lookup"><span data-stu-id="48e2d-304">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="48e2d-305">Wenn `nuget pack` erfolgreich ausgeführt wurde, können Sie die erstellte `.nupkg`-Datei wie in [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben in einem geeigneten Katalog veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-305">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="48e2d-306">Wenn Sie sich das erstellte Paket genauer ansehen möchten, öffnen Sie es einfach im [Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="48e2d-306">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="48e2d-307">Dieser stellt den Inhalt des Pakets und das Manifest grafisch dar.</span><span class="sxs-lookup"><span data-stu-id="48e2d-307">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="48e2d-308">Sie können die resultierende `.nupkg`-Datei auch in eine `.zip`-Datei umbenennen und deren Inhalt direkt prüfen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-308">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="48e2d-309">Zusätzliche Optionen</span><span class="sxs-lookup"><span data-stu-id="48e2d-309">Additional options</span></span>

<span data-ttu-id="48e2d-310">Sie können `nuget pack` mit verschiedenen Befehlszeilenparameter verwenden, um z.B. Dateien auszuschließen, die Versionsnummer im Manifest zu überschreiben und den Ausgabeordner zu ändern.</span><span class="sxs-lookup"><span data-stu-id="48e2d-310">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="48e2d-311">Eine vollständige Liste finden Sie in der [Referenz zum Packbefehl](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-311">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="48e2d-312">Folgende Optionen werden beispielsweise häufig in Visual Studio-Projekten verwendet:</span><span class="sxs-lookup"><span data-stu-id="48e2d-312">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="48e2d-313">**Referenzierte Projekte:** Wenn das Projekt auf andere verweist, können Sie die referenzierten Projekte mithilfe der Option `-IncludeReferencedProjects` als Teil des Pakets oder als Abhängigkeiten hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-313">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="48e2d-314">Diese Einschließung ist rekursiv. Wenn also `MyProject.csproj` auf die Projekte B und C verweist und diese Projekte ihrerseits auf die Projekte D, E und F, dann werden Dateien aus B, C, D, E und F in das Paket aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-314">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="48e2d-315">Wenn ein referenziertes Projekt selbst eine `.nuspec`-Datei enthält, fügt NuGet dieses Projekt stattdessen als Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="48e2d-315">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="48e2d-316">Dieses Projekt muss separat gepackt und veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-316">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="48e2d-317">**Buildkonfiguration:** NuGet verwendet die in der Projektdatei festgelegte Standardbuildkonfiguration, üblicherweise *Debuggen*.</span><span class="sxs-lookup"><span data-stu-id="48e2d-317">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="48e2d-318">Um Dateien aus einer anderen Buildkonfiguration zu packen, z.B. *Release*, verwenden Sie die Option `-properties` mit folgender Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="48e2d-318">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="48e2d-319">**Symbole:** Um Symbole einzuschließen, mit denen Benutzer den Paketcode im Debugger schrittweise ausführen können, verwenden Sie die Option `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="48e2d-319">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="48e2d-320">Testen der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="48e2d-320">Testing package installation</span></span>

<span data-ttu-id="48e2d-321">Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="48e2d-321">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="48e2d-322">Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-322">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="48e2d-323">Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/ways-to-install-a-package.md) über die Befehlszeile testen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-323">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="48e2d-324">Für automatisierte Tests gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="48e2d-324">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="48e2d-325">Kopieren Sie die `.nupkg`-Datei in einen lokalen Ordner.</span><span class="sxs-lookup"><span data-stu-id="48e2d-325">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="48e2d-326">Fügen Sie den Ordner mithilfe des `nuget sources add -name <name> -source <path>`-Befehls den Paketquellen hinzu. Weitere Informationen finden Sie unter [sources command (NuGet CLI) (sources-Befehl (NuGet-CLI))](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="48e2d-326">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="48e2d-327">Diese lokale Quelle muss auf einem Computer nur einmal festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-327">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="48e2d-328">Installieren Sie das Paket aus dieser Quelle mithilfe von `nuget install <packageID> -source <name>`, wobei `<name>` dem Namen der Quelle entspricht, so wie er an `nuget sources` übergeben wurde.</span><span class="sxs-lookup"><span data-stu-id="48e2d-328">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="48e2d-329">Durch das Angeben der Quelle wird sichergestellt, dass das Paket nur aus dieser Quelle installiert wird.</span><span class="sxs-lookup"><span data-stu-id="48e2d-329">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="48e2d-330">Überprüfen Sie das Dateisystem, um sicherzustellen, dass Dateien richtig installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="48e2d-330">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48e2d-331">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="48e2d-331">Next Steps</span></span>

<span data-ttu-id="48e2d-332">Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="48e2d-332">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="48e2d-333">Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-333">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="48e2d-334">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="48e2d-334">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="48e2d-335">Unterstützen mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="48e2d-335">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="48e2d-336">Transformationen von Quell- und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="48e2d-336">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="48e2d-337">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="48e2d-337">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="48e2d-338">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="48e2d-338">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="48e2d-339">Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="48e2d-339">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="48e2d-340">Native Pakete</span><span class="sxs-lookup"><span data-stu-id="48e2d-340">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="48e2d-341">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="48e2d-341">Symbol Packages</span></span>](../create-packages/symbol-packages.md)