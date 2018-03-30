---
title: 'Vorgehensweise: Verpacken von UWP-Steuerelementen mit NuGet | Microsoft-Dokumentation'
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Vorgehensweise beim Erstellen von NuGet-Paketen mit UWP-Steuerelementen einschließlich der erforderlichen Metadaten und der unterstützenden Dateien für die Visual Studio- und Blend-Designer.
keywords: UWP-Steuerelemente von NuGet, Visual Studio XAML-Designer, Blend-Designer, benutzerdefinierte Steuerelemente
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f024fd1823c77d57d30c4f841bf03494194c8339
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="9734a-104">Erstellen von UWP-Steuerelementen als NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="9734a-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="9734a-105">Mit Visual Studio 2017 können Sie zusätzliche Funktionen für UWP-Steuerelemente nutzen, die Sie in NuGet-Pakete übermitteln.</span><span class="sxs-lookup"><span data-stu-id="9734a-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="9734a-106">Dieser Leitfaden führt Sie anhand des [ExtensionSDKasNuGetPackage-Beispiels](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) durch diese Funktionen.</span><span class="sxs-lookup"><span data-stu-id="9734a-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9734a-107">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="9734a-107">Prerequisites</span></span>

1. <span data-ttu-id="9734a-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9734a-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="9734a-109">Kenntnisse hinsichtlich der [Erstellung von UWP-Paketen](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9734a-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="9734a-110">Hinzufügen von Unterstützung für die Toolbox bzw. den Bereich „Objekte“ bei XAML-Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="9734a-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="9734a-111">Damit ein XAML-Steuerelement in der Toolbox des XAML-Designers in Visual Studio und im Bereich „Objekte“ in Blend angezeigt wird, müssen Sie im Stammverzeichnis des Ordners `tools` Ihres Paketprojekts die Datei `VisualStudioToolsManifest.xml` erstellen.</span><span class="sxs-lookup"><span data-stu-id="9734a-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="9734a-112">Diese Datei ist nicht erforderlich, wenn das Steuerelement in der Toolbox oder im Bereich „Objekte“ nicht angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="9734a-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="9734a-113">Die Struktur der Datei lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="9734a-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="9734a-114">Dabei gilt:</span><span class="sxs-lookup"><span data-stu-id="9734a-114">where:</span></span>

- <span data-ttu-id="9734a-115">*your_package_file*: Der Name Ihrer Steuerungsdatei, wie z.B. `ManagedPackage.winmd` („ManagedPackage“ ist ein beliebiger, in diesem Beispiel verwendeter Name und hat keine andere Bedeutung).</span><span class="sxs-lookup"><span data-stu-id="9734a-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="9734a-116">*vs_category*: Die Bezeichnung der Gruppe, in der das Steuerelement in der Toolbox des Visual Studio-Designers angezeigt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="9734a-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="9734a-117">Damit das Steuerelement in der Toolbox angezeigt wird, ist ein `VSCategory` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="9734a-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="9734a-118">*blend_category*: Die Bezeichnung der Gruppe, in der das Steuerelement im Bereich „Objekte“ des Blend-Designers angezeigt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="9734a-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="9734a-119">Damit das Steuerelement unter „Objekte“ angezeigt wird, ist `BlendCategory` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="9734a-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="9734a-120">*type_full_name_n*: Der vollständig qualifizierte Name der einzelnen Steuerelemente, einschließlich des Namespace, z.B. `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="9734a-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="9734a-121">Beachten Sie, dass das Format mit Punkt für verwaltete und native Typen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9734a-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="9734a-122">In erweiterten Szenarios können Sie auch mehrere `<File>`-Elemente innerhalb von `<FileList>` einschließen, wenn ein einzelnes Paket mehrere Steuerelementassemblys enthält.</span><span class="sxs-lookup"><span data-stu-id="9734a-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="9734a-123">Es können auch mehrere `<ToolboxItems>`-Knoten in einem einzelnen `<File>`-Element enthalten sein, wenn Sie Ihre Steuerelemente in separaten Kategorien organisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="9734a-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="9734a-124">Im folgenden Beispiel wird das in `ManagedPackage.winmd` angezeigte Steuerelement in Visual Studio und Blend in einer Gruppe mit dem Namen „Verwaltetes Paket“ angezeigt, und „MyCustomControl“ wird in dieser Gruppe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9734a-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="9734a-125">Alle diese Namen wurden willkürlich ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="9734a-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ein Beispielsteuerelement, wie es in Visual Studio angezeigt wird](media/UWP-control-vs-toolbox.png)

![Ein Beispielsteuerelement, wie es in Blend angezeigt wird](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="9734a-128">Sie müssen explizit jedes Steuerelement angeben, das in der Toolbox bzw. im Bereich „Objekte“ angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="9734a-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="9734a-129">Stellen Sie sicher, dass Sie die Steuerelemente im Format `Namespace.ControlName` angeben.</span><span class="sxs-lookup"><span data-stu-id="9734a-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="9734a-130">Hinzufügen benutzerdefinierter Symbole zu Ihren Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="9734a-130">Add custom icons to your controls</span></span>

<span data-ttu-id="9734a-131">Damit Sie ein benutzerdefiniertes Symbol in der Toolbox bzw. im Bereich „Objekte“ anzeigen können, müssen Sie ein Image zu Ihrem Projekt oder dem entsprechenden `design.dll`-Projekt mit dem Namen „Namespace.ControlName.extension“ hinzufügen und den Buildvorgang auf „Eingebettete Ressource“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="9734a-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="9734a-132">Als Formate werden `.png`, `.jpg`, `.jpeg`, `.gif` und `.bmp` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9734a-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="9734a-133">Die empfohlene Bildgröße ist 64 x 64 Pixel.</span><span class="sxs-lookup"><span data-stu-id="9734a-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="9734a-134">Im nachfolgenden Beispiel enthält das Projekt eine Imagedatei mit dem Namen „ManagedPackage.MyCustomControl.png“.</span><span class="sxs-lookup"><span data-stu-id="9734a-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Festlegen eines benutzerdefinierten Symbols in einem Projekt](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="9734a-136">Bei nativen Steuerelementen müssen Sie das Symbol im Projekt `design.dll` als Ressource einfügen.</span><span class="sxs-lookup"><span data-stu-id="9734a-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="9734a-137">Unterstützung bestimmter Windows-Plattformversionen</span><span class="sxs-lookup"><span data-stu-id="9734a-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="9734a-138">UWP-Pakete weisen eine TargetPlatformVersion (TPV) und eine TargetPlatformMinVersion (TPMinV) auf, die die oberen und unteren Grenzen der Betriebssystemversion definieren, unter der die App installiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="9734a-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="9734a-139">TPV gibt ferner die Version des SDK an, für das die App erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="9734a-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="9734a-140">Achten Sie bei der Erstellung eines UWP-Pakets auf diese Eigenschaften: Durch die Verwendung von APIs außerhalb der Grenzen der in der App definierten Plattformversionen schlägt entweder das Build oder die App zur Laufzeit fehl.</span><span class="sxs-lookup"><span data-stu-id="9734a-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="9734a-141">Angenommen beispielsweise, Sie haben die TPMinV für Ihr Steuerelementpaket auf Windows 10 Anniversary Edition (10.0; Build 14393) festgelegt und möchten sicherstellen, dass das Paket nur von UWP-Projekten genutzt wird, die dieser Untergrenze entsprechen.</span><span class="sxs-lookup"><span data-stu-id="9734a-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="9734a-142">Damit Ihr Paket von UWP-Projekten genutzt werden kann, müssen Sie Ihre Steuerelemente mit den folgenden Ordnernamen packen:</span><span class="sxs-lookup"><span data-stu-id="9734a-142">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="9734a-143">Erstellen Sie zur Durchsetzung einer entsprechenden Überprüfung von TPMinV eine [MSBuild-Zieldatei](/visualstudio/msbuild/msbuild-targets), und packen Sie diese unter `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name> mit dem Namen Ihrer spezifischen Assembly.</span><span class="sxs-lookup"><span data-stu-id="9734a-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="9734a-144">Im Folgenden wird ein Beispiel dafür aufgeführt, wie die Zieldatei aussehen sollte:</span><span class="sxs-lookup"><span data-stu-id="9734a-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="9734a-145">Hinzufügen von Entwurfszeitunterstützung</span><span class="sxs-lookup"><span data-stu-id="9734a-145">Add design-time support</span></span>

<span data-ttu-id="9734a-146">Wenn Sie konfigurieren möchten, wo die Steuerelementeigenschaften in der Eigenschaftenanalyse erscheinen sollen, wo benutzerdefinierte Adorner hinzugefügt werden können usw., müssen Sie Ihre Datei entsprechend der Zielplattform `design.dll` im Ordner `lib\uap10.0\Design` anordnen.</span><span class="sxs-lookup"><span data-stu-id="9734a-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="9734a-147">Zudem sollten Sie `Generic.xaml` und alle Ressourcenwörterbücher einschließen, die im Ordner `<your_assembly_name>\Themes` zusammengeführt werden, um sicherzustellen, dass das Feature **[Vorlage bearbeiten > Kopie bearbeiten](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funktioniert. (Verwenden Sie dafür erneut Ihren Assemblynamen).</span><span class="sxs-lookup"><span data-stu-id="9734a-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="9734a-148">(Diese Datei hat keine Auswirkungen auf das Laufzeitverhalten eines Steuerelements.) Die Ordnerstruktur sollte dann wie folgt angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="9734a-148">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="9734a-149">Steuerelementeigenschaften werden in der Eigenschaftenanalyse standardmäßig in der Kategorie „Sonstiges“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9734a-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="9734a-150">Verwenden von Zeichenfolgen und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9734a-150">Use strings and resources</span></span>

<span data-ttu-id="9734a-151">Sie können Zeichenfolgenressourcen (`.resw`) in Ihr Paket einbetten, das durch Ihr Steuerelement oder das verwendete UWP-Projekt verwendet werden kann, und die Eigenschaft **Buildvorgang** der `.resw`-Datei auf **PRIResource** festlegen.</span><span class="sxs-lookup"><span data-stu-id="9734a-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="9734a-152">Ein entsprechendes Beispiel finden Sie unter [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) im ExtensionSDKasNuGetPackage-Beispiel.</span><span class="sxs-lookup"><span data-stu-id="9734a-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="9734a-153">Paketinhalte wie Images</span><span class="sxs-lookup"><span data-stu-id="9734a-153">Package content such as images</span></span>

<span data-ttu-id="9734a-154">Platzieren Sie zum Packen von Inhalten wie Images, die von Ihrem Steuerelement oder dem verwendeten UWP-Projekt verwendet werden können, diese Dateien in dem `lib\uap10.0`-Ordner.</span><span class="sxs-lookup"><span data-stu-id="9734a-154">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="9734a-155">Sie können auch eine [MSBuild-Zieldatei](/visualstudio/msbuild/msbuild-targets) erstellen, um sicherzustellen, dass das Objekt in den Ausgabeordner des verwendeten Projekts kopiert wird:</span><span class="sxs-lookup"><span data-stu-id="9734a-155">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="9734a-156">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9734a-156">See also</span></span>

- [<span data-ttu-id="9734a-157">Erstellen von UWP-Paketen</span><span class="sxs-lookup"><span data-stu-id="9734a-157">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="9734a-158">Beispiel „ExtensionSDKasNuGetPackage“</span><span class="sxs-lookup"><span data-stu-id="9734a-158">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)