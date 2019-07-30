---
title: Identifizieren des Projektformats
description: Beschreibt, wie Sie das Projektformat identifizieren
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843442"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="49dce-103">Identifizieren des Projektformats</span><span class="sxs-lookup"><span data-stu-id="49dce-103">Identify the project format</span></span>

<span data-ttu-id="49dce-104">NuGet kann für alle .NET-Projekte verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="49dce-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="49dce-105">Das Projektformat (SDK-Format oder Nicht-SDK-Format) bestimmt jedoch einige der Tools und Methoden, die zum Verwenden und Erstellen von NuGet-Paketen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="49dce-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="49dce-106">Projekte im SDK-Format verwenden das [SDK-Attribut](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="49dce-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="49dce-107">Es ist wichtig, den Projekttyp zu identifizieren, da die Methoden und Tools, mit denen Sie NuGet-Pakete verwenden und erstellen, vom Projektformat abhängen.</span><span class="sxs-lookup"><span data-stu-id="49dce-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="49dce-108">Für Projekte im Nicht-SDK-Format hängen die Methoden und Tools ebenfalls davon ab, ob das Projekt zum `PackageReference`-Format migriert wurde.</span><span class="sxs-lookup"><span data-stu-id="49dce-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="49dce-109">Ob es sich um ein Projekt im SDK-Format handelt, hängt von der Methode ab, die zum Erstellen des Projekts verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="49dce-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="49dce-110">In der folgenden Tabelle werden das Standardprojektformat und das zugehörige CLI-Tool für das Projekt angegeben, wenn Sie es mit Visual Studio 2017 oder einer neueren Version erstellen.</span><span class="sxs-lookup"><span data-stu-id="49dce-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="49dce-111">Projekt&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="49dce-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="49dce-112">Standard-projekt-format</span><span class="sxs-lookup"><span data-stu-id="49dce-112">Default project format</span></span> | <span data-ttu-id="49dce-113">CLI-Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="49dce-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="49dce-114">Hinweise</span><span class="sxs-lookup"><span data-stu-id="49dce-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="49dce-115">.NET-Standard</span><span class="sxs-lookup"><span data-stu-id="49dce-115">.NET Standard</span></span> | <span data-ttu-id="49dce-116">SDK-Format</span><span class="sxs-lookup"><span data-stu-id="49dce-116">SDK-style</span></span> | [<span data-ttu-id="49dce-117">dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="49dce-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="49dce-118">Projekte, die vor Visual Studio 2017 erstellt wurden, weisen nicht das SDK-Format auf.</span><span class="sxs-lookup"><span data-stu-id="49dce-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="49dce-119">Verwenden Sie die `nuget.exe`-CLI.</span><span class="sxs-lookup"><span data-stu-id="49dce-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="49dce-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="49dce-120">.NET Core</span></span> | <span data-ttu-id="49dce-121">SDK-Format</span><span class="sxs-lookup"><span data-stu-id="49dce-121">SDK-style</span></span> | [<span data-ttu-id="49dce-122">dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="49dce-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="49dce-123">Projekte, die vor Visual Studio 2017 erstellt wurden, weisen nicht das SDK-Format auf.</span><span class="sxs-lookup"><span data-stu-id="49dce-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="49dce-124">Verwenden Sie die `nuget.exe`-CLI.</span><span class="sxs-lookup"><span data-stu-id="49dce-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="49dce-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49dce-125">.NET Framework</span></span> | <span data-ttu-id="49dce-126">Nicht-SDK-Format</span><span class="sxs-lookup"><span data-stu-id="49dce-126">Non-SDK-style</span></span> | [<span data-ttu-id="49dce-127">nuget.exe-CLI</span><span class="sxs-lookup"><span data-stu-id="49dce-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="49dce-128">.NET Framework Projekte, die mit anderen Methoden erstellt werden, sind möglicherweise Projekte im SDK-Format.</span><span class="sxs-lookup"><span data-stu-id="49dce-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="49dce-129">Verwenden Sie für diese stattdessen die [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="49dce-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="49dce-130">[Migriertes](../reference/migrate-packages-config-to-package-reference.md) .NET-Projekt</span><span class="sxs-lookup"><span data-stu-id="49dce-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="49dce-131">Nicht-SDK-Format</span><span class="sxs-lookup"><span data-stu-id="49dce-131">Non-SDK-style</span></span>| <span data-ttu-id="49dce-132">Verwenden Sie zum Erstellen von Paketen [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="49dce-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="49dce-133">Zum Erstellen von Paketen wird `msbuild -t:pack` empfohlen.</span><span class="sxs-lookup"><span data-stu-id="49dce-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="49dce-134">Verwenden Sie andernfalls die [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="49dce-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="49dce-135">Migrierte Projekte sind keine Projekte im SDK-Format.</span><span class="sxs-lookup"><span data-stu-id="49dce-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="49dce-136">Überprüfen des Projektformats</span><span class="sxs-lookup"><span data-stu-id="49dce-136">Check the project format</span></span>

<span data-ttu-id="49dce-137">Wenn Sie sich nicht sicher sind, ob ein Projekt das SDK-Format aufweist, suchen Sie in der Projektdatei (für C# ist dies die CSPROJ-Datei) das SDK-Attribut im `<Project>`-Element.</span><span class="sxs-lookup"><span data-stu-id="49dce-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="49dce-138">Wenn es vorhanden ist, handelt es sich um ein Projekt im SDK-Format.</span><span class="sxs-lookup"><span data-stu-id="49dce-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="49dce-139">Überprüfen des Projektformats in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49dce-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="49dce-140">Wenn Sie in Visual Studio arbeiten, können Sie mit einer der folgenden Methoden das Projektformat schnell überprüfen:</span><span class="sxs-lookup"><span data-stu-id="49dce-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="49dce-141">Klicken Sie mit der rechten Maustaste im Projektmappen-Explorer, und wählen Sie **"myprojectname.csproj" bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="49dce-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="49dce-142">Diese Option ist nur ab Visual Studio 2017 für Projekte verfügbar, die das SDK-Attribut verwenden.</span><span class="sxs-lookup"><span data-stu-id="49dce-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="49dce-143">Verwenden Sie andernfalls die andere Methode.</span><span class="sxs-lookup"><span data-stu-id="49dce-143">Otherwise, use the other method.</span></span>

   ![Bearbeiten der Projektdatei](media/edit-project-file.png)

   <span data-ttu-id="49dce-145">Für ein Projekt im SDK-Format wird in der Projektdatei das [SDK-Attribut](/dotnet/core/tools/csproj#additions) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="49dce-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="49dce-146">Wählen Sie im Menü **Projekt** die Option **Projekt entladen** aus (oder klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **Projekt entladen** aus).</span><span class="sxs-lookup"><span data-stu-id="49dce-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="49dce-147">In der Projektdatei dieses Projekts ist das SDK-Attribut nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="49dce-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="49dce-148">Es handelt sich nicht um ein Projekt im SDK-Format.</span><span class="sxs-lookup"><span data-stu-id="49dce-148">It is not an SDK-style project.</span></span>

   ![Entladen des Projekts](media/unload-project.png)

   <span data-ttu-id="49dce-150">Klicken Sie dann mit der rechten Maustaste auf das entladene Projekt, und wählen Sie **"myprojectname.csproj" bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="49dce-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="49dce-151">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="49dce-151">See also</span></span>

- [<span data-ttu-id="49dce-152">Erstellen von .NET Standard-Paketen mit der dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="49dce-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="49dce-153">Erstellen von .NET Standard-Paketen mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49dce-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="49dce-154">Erstellen und Veröffentlichen eines .NET Framework-Pakets (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="49dce-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="49dce-155">NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="49dce-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)