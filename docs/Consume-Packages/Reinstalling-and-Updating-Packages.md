---
title: Erneutes Installieren und Aktualisieren von NuGet-Paketen | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2785879b-97f0-4a85-b3cc-bf4eaa5c39bf
description: "Hier finden Sie Informationen dazu, wann es nötig ist, Pakete neu zu installieren und zu aktualisieren (z.B. bei fehlerhaften Paketverweisen in Visual Studio)."
keywords: NuGet-Paketinstallation, erneute Installation eines NuGet-Pakets, NuGet-Paketwiederherstellung, Aktualisieren eines Pakets, Paketwiederherstellung, Beheben fehlerhafter Verweise
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e2875630b24fbe04fc7bcab52335d849e54160de
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="how-to-reinstall-and-update-packages"></a><span data-ttu-id="0db70-104">Neuinstallieren und Aktualisieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="0db70-104">How to reinstall and update packages</span></span>

<span data-ttu-id="0db70-105">Es gibt einige Situationen, die nachfolgend unter [Wann ein Paket neu installiert wird](#when-to-reinstall-a-package) beschrieben werden, in denen Verweise auf ein Paket innerhalb eines Visual Studio-Projekts fehlerhaft werden können.</span><span class="sxs-lookup"><span data-stu-id="0db70-105">There are a number of situations, described below under [When to Reinstall a Package](#when-to-reinstall-a-package), where references to a package might get broken within a Visual Studio project.</span></span> <span data-ttu-id="0db70-106">In diesen Fällen werden diese Verweise durch das Löschen und die Neuinstallation der gleichen Paketversion ordnungsgemäß wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="0db70-106">In these cases, uninstalling and then reinstalling the same version of the package will restore those references to working order.</span></span> <span data-ttu-id="0db70-107">Ein Paket zu aktualisieren bedeutet einfach, eine aktualisierte Version zu installieren. So lässt sich ein Paket häufig ordnungsgemäß wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="0db70-107">Updating a package simply means installing an updated version, which often restores a package to working order.</span></span>

<span data-ttu-id="0db70-108">Das Aktualisieren und die Neuinstallation von Paketen erfolgt wie im Folgenden dargestellt:</span><span class="sxs-lookup"><span data-stu-id="0db70-108">Updating and reinstalling packages is accomplished as follows:</span></span>

| <span data-ttu-id="0db70-109">Methode</span><span class="sxs-lookup"><span data-stu-id="0db70-109">Method</span></span> | <span data-ttu-id="0db70-110">Update</span><span class="sxs-lookup"><span data-stu-id="0db70-110">Update</span></span> | <span data-ttu-id="0db70-111">Neuinstallation</span><span class="sxs-lookup"><span data-stu-id="0db70-111">Reinstall</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0db70-112">Paket-Manager-Konsole (beschrieben unter [Verwenden des Updatepakets](#using-update-package))</span><span class="sxs-lookup"><span data-stu-id="0db70-112">Package Manager console (described in [Using Update-Package](#using-update-package))</span></span> | <span data-ttu-id="0db70-113">`Update-Package`-Befehl</span><span class="sxs-lookup"><span data-stu-id="0db70-113">`Update-Package` command</span></span> | <span data-ttu-id="0db70-114">`Update-Package -reinstall`-Befehl</span><span class="sxs-lookup"><span data-stu-id="0db70-114">`Update-Package -reinstall` command</span></span> |
| <span data-ttu-id="0db70-115">Benutzeroberfläche des Paket-Managers</span><span class="sxs-lookup"><span data-stu-id="0db70-115">Package Manager UI</span></span> | <span data-ttu-id="0db70-116">Wählen Sie auf der Registerkarte **Updates** mindestens ein Paket aus, und klicken Sie auf **Update** (Aktualisieren).</span><span class="sxs-lookup"><span data-stu-id="0db70-116">On the **Updates** tab, select one or more packages and select **Update**</span></span> | <span data-ttu-id="0db70-117">Wählen Sie auf der Registerkarte **Installiert** ein Paket aus, dokumentieren Sie dessen Namen, und klicken Sie dann auf **Deinstallieren**.</span><span class="sxs-lookup"><span data-stu-id="0db70-117">On the **Installed** tab, select a package, record its name, then select **Uninstall**.</span></span> <span data-ttu-id="0db70-118">Wechseln Sie zur Registerkarte **Durchsuchen**, suchen Sie nach dem Paketnamen, wählen Sie ihn aus, und klicken Sie dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="0db70-118">Switch to the **Browse** tab, search for the package name, select it, then select **Install**).</span></span> |
| <span data-ttu-id="0db70-119">nuget.exe-CLI</span><span class="sxs-lookup"><span data-stu-id="0db70-119">nuget.exe CLI</span></span> | <span data-ttu-id="0db70-120">`nuget update`-Befehl</span><span class="sxs-lookup"><span data-stu-id="0db70-120">`nuget update` command</span></span> | <span data-ttu-id="0db70-121">Löschen Sie für alle Pakete den Paketordner, und führen Sie dann `nuget install` aus.</span><span class="sxs-lookup"><span data-stu-id="0db70-121">For all packages, delete the package folder, then run `nuget install`.</span></span> <span data-ttu-id="0db70-122">Löschen Sie für ein einzelnes Paket den Paketordner, und verwenden Sie `nuget install <id>`, um den gleichen Ordner neu zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0db70-122">For a single package, delete the package folder and use `nuget install <id>` to reinstall the same one.</span></span> |

<span data-ttu-id="0db70-123">In diesem Artikel:</span><span class="sxs-lookup"><span data-stu-id="0db70-123">In this article:</span></span>

- [<span data-ttu-id="0db70-124">Wann ein Paket neu installiert werden sollte</span><span class="sxs-lookup"><span data-stu-id="0db70-124">When to Reinstall a Package</span></span>](#when-to-reinstall-a-package)
- [<span data-ttu-id="0db70-125">Einschränken von Updateversionen</span><span class="sxs-lookup"><span data-stu-id="0db70-125">Constraining upgrade versions</span></span>](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a><span data-ttu-id="0db70-126">Wann ein Paket neu installiert werden sollte</span><span class="sxs-lookup"><span data-stu-id="0db70-126">When to Reinstall a Package</span></span>

1. <span data-ttu-id="0db70-127">**Fehlerhafte Verweise nach der Paketwiederherstellung:** Wenn Sie ein Projekt geöffnet und NuGet-Pakete wiederhergestellt haben, jedoch noch immer fehlerhafte Verweise angezeigt werden, versuchen Sie, jedes einzelne Paket wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="0db70-127">**Broken references after package restore**: If you've opened a project and restored NuGet packages, but still see broken references, try reinstalling each of those packages.</span></span>
1. <span data-ttu-id="0db70-128">**Projekt ist aufgrund gelöschter Dateien fehlerhaft:** NuGet hält Sie nicht davon ab, Elemente zu löschen, die aus Paketen hinzugefügt wurden. Es ist also einfach, versehentlich die aus einem Paket installierten Inhalte zu verändern und Ihr Projekt so zu zerstören.</span><span class="sxs-lookup"><span data-stu-id="0db70-128">**Project is broken due to deleted files**: NuGet does not prevent you from removing items added from packages, so it's easy to inadvertently modify contents installed from a package and break your project.</span></span> <span data-ttu-id="0db70-129">Installieren Sie die betroffenen Pakete erneut, um das Projekt wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="0db70-129">To restore the project, reinstall the affected packages.</span></span>
1. <span data-ttu-id="0db70-130">**Das Paketupdate hat zu einem Fehler im Projekt geführt:** Wenn ein Update für ein Paket einen Fehler in einem Projekt verursacht, wurde dieser in der Regel von einem Abhängigkeitspaket ausgelöst, das möglicherweise auch aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="0db70-130">**Package update broke the project**: If an update to a package breaks a project, the failure is generally caused by a dependency package which may have also been updated.</span></span> <span data-ttu-id="0db70-131">Installieren Sie das spezifische Paket neu, um den Zustand der Abhängigkeit wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="0db70-131">To restore the state of the dependency, reinstall that specific package.</span></span>
1. <span data-ttu-id="0db70-132">**Erneutes Zuweisen oder Upgrade eines Projekts:** Dies kann hilfreich sein, wenn ein Projekt erneut zugewiesen oder ein Upgrade für dieses durchgeführt wurde, und wenn das Paket eine Neuinstallation aufgrund der Änderung im Zielframework erfordert.</span><span class="sxs-lookup"><span data-stu-id="0db70-132">**Project retargeting or upgrade**: This can be useful when a project has been retargeted or upgraded and if the package requires reinstallation due to the change in target framework.</span></span> <span data-ttu-id="0db70-133">NuGet zeigt in solchen Fällen sofort nach der Projektneuzuweisung einen Buildfehler an, und in nachfolgenden Buildwarnungen wird Ihnen mitgeteilt, dass das Paket möglicherweise neu installiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="0db70-133">NuGet shows a build error in such cases immediately after project retargeting, and subsequent build warnings let you know that the package may need to be reinstalled.</span></span> <span data-ttu-id="0db70-134">Für das Projektupgrade zeigt NuGet einen Fehler im Projektupgradeprotokoll an.</span><span class="sxs-lookup"><span data-stu-id="0db70-134">For project upgrade, NuGet shows an error in the Project Upgrade Log.</span></span>
1. <span data-ttu-id="0db70-135">**Neuinstallation eines Pakets während der Entwicklung:** Paketautoren müssen oft dieselbe Version des Pakets neu installieren, das Sie entwickeln, um das Verhalten zu testen.</span><span class="sxs-lookup"><span data-stu-id="0db70-135">**Reinstalling a package during its development**: Package authors often need to reinstall the same version of package they're developing to test the behavior.</span></span> <span data-ttu-id="0db70-136">Der `Install-Package`-Befehl bietet keine Option zum Erzwingen einer Neuinstallation an. Verwenden Sie deshalb stattdessen `Update-Package -reinstall`.</span><span class="sxs-lookup"><span data-stu-id="0db70-136">The `Install-Package` command does not provide an option to force a reinstall, so use `Update-Package -reinstall` instead.</span></span>

## <a name="constraining-upgrade-versions"></a><span data-ttu-id="0db70-137">Einschränken von Updateversionen</span><span class="sxs-lookup"><span data-stu-id="0db70-137">Constraining upgrade versions</span></span>

<span data-ttu-id="0db70-138">Standardmäßig wird durch die Neuinstallation oder das Update eines Pakets *immer* die neueste verfügbare Version aus der Paketquelle installiert.</span><span class="sxs-lookup"><span data-stu-id="0db70-138">By default, reinstalling or updating a package *always* installs the latest version available from the package source.</span></span>

<span data-ttu-id="0db70-139">In Projekten, die das `packages.config`-Verweisformat verwenden, können Sie jedoch den Versionsbereich explizit einschränken.</span><span class="sxs-lookup"><span data-stu-id="0db70-139">In projects using the `packages.config` reference format, however, you can specifically constrain the version range.</span></span> <span data-ttu-id="0db70-140">Wenn Sie z.B. wissen, dass Ihre Anwendung nur mit Version 1.x eines Pakets funktioniert, jedoch nicht mit 2.0 oder höher (vielleicht aufgrund einer größeren Änderung in der Paket-API), sollten Sie die Upgrades auf 1.x-Versionen beschränken.</span><span class="sxs-lookup"><span data-stu-id="0db70-140">For example, if you know that your application works only with version 1.x of a package but not 2.0 and above, perhaps due to a major change in the package API, then you'd want to constrain upgrades to 1.x versions.</span></span> <span data-ttu-id="0db70-141">Dadurch werden versehentliche Updates verhindert, die die Anwendung zerstören würden.</span><span class="sxs-lookup"><span data-stu-id="0db70-141">This prevents accidental updates that would break the application.</span></span>

<span data-ttu-id="0db70-142">Um eine Einschränkung festzulegen, öffnen Sie `packages.config` in einem Text-Editor, suchen Sie nach der betreffenden Abhängigkeit, und fügen Sie das Attribut `allowedVersions` mit einem Versionsbereich hinzu.</span><span class="sxs-lookup"><span data-stu-id="0db70-142">To set a constraint, open `packages.config` in a text editor, locate the dependency in question, and add the `allowedVersions` attribute with a version range.</span></span> <span data-ttu-id="0db70-143">Wenn Sie z.B. Updates auf Version 1.x beschränken möchten, legen Sie `allowedVersions` auf `[1,2)` fest:</span><span class="sxs-lookup"><span data-stu-id="0db70-143">For example, to constrain updates to version 1.x, set `allowedVersions` to `[1,2)`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

<span data-ttu-id="0db70-144">Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschriebene Notation.</span><span class="sxs-lookup"><span data-stu-id="0db70-144">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-update-package"></a><span data-ttu-id="0db70-145">Verwenden eines Updatepakets</span><span class="sxs-lookup"><span data-stu-id="0db70-145">Using Update-Package</span></span>

<span data-ttu-id="0db70-146">Unter Berücksichtigung der nachfolgend beschriebenen [Überlegungen](#considerations) können Sie einfach beliebige Paket neu installieren, indem Sie den [Befehl „Updatepaket“](../Tools/ps-ref-update-package.md) in der Paket-Manager-Konsole von Visual Studio verwenden (**Extras** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole**):</span><span class="sxs-lookup"><span data-stu-id="0db70-146">Being mindful of the [Considerations](#considerations) described below, you can easily reinstall any package using the [Update-Package command](../Tools/ps-ref-update-package.md) in the Visual Studio Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

```ps
Update-Package -Id <package_name> –reinstall
```

<span data-ttu-id="0db70-147">Die Verwendung dieses Befehls ist viel einfacher als das Entfernen eines Pakets und der anschließende Versuch, dasselbe Paket im NuGet-Katalog mit der gleichen Version zu finden.</span><span class="sxs-lookup"><span data-stu-id="0db70-147">Using this command is much easier than removing a package and then trying to locate the same package in the NuGet gallery with the same version.</span></span> <span data-ttu-id="0db70-148">Beachten Sie, dass der `-Id`-Schalter optional ist.</span><span class="sxs-lookup"><span data-stu-id="0db70-148">Note that the `-Id` switch is optional.</span></span>

<span data-ttu-id="0db70-149">Wenn Sie den gleichen Befehl ohne `-reinstall` verwenden, wird ein Paket auf die neuere Version aktualisiert (falls zutreffend).</span><span class="sxs-lookup"><span data-stu-id="0db70-149">The same command without `-reinstall` updates a package to a newer version, if applicable.</span></span> <span data-ttu-id="0db70-150">Der Befehl gibt einen Fehler aus, wenn das betreffende Paket nicht bereits in einem Projekt installiert ist. Das bedeutet, dass `Update-Package` Pakete nicht direkt installiert.</span><span class="sxs-lookup"><span data-stu-id="0db70-150">The command gives an error if the package in question is not already installed in a project; that is, `Update-Package` does not install packages directly.</span></span>

```ps
Update-Package <package_name>
```

<span data-ttu-id="0db70-151">Standardmäßig wirkt sich `Update-Package` auf alle Pakete in einer Projektmappe aus.</span><span class="sxs-lookup"><span data-stu-id="0db70-151">By default, `Update-Package` affects all packages in a solution.</span></span> <span data-ttu-id="0db70-152">Verwenden Sie den Parameter `-ProjectName` mithilfe des Namens des Projekts, wie es im Projektmappen-Explorer dargestellt wird, um die Aktion auf ein bestimmtes Projekt zu beschränken:</span><span class="sxs-lookup"><span data-stu-id="0db70-152">To limit the action to a specific project, use the `-ProjectName` switch, using the name of the project as it appears in Solution Explorer:</span></span>

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

<span data-ttu-id="0db70-153">Um alle Pakete in einem Projekt zu *aktualisieren* (oder mithilfe von `-reinstall` neu zu installieren), verwenden Sie `-ProjectName` ohne Angabe eines bestimmten Pakets:</span><span class="sxs-lookup"><span data-stu-id="0db70-153">To *update* all packages in a project (or reinstall using `-reinstall`), use `-ProjectName` without specifying any particular package:</span></span>

```ps
Update-Package -ProjectName MyProject
```

<span data-ttu-id="0db70-154">Verwenden Sie `Update-Package` nur ohne andere Argumente oder Parameter, um alle Pakete in einer Projektmappe zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0db70-154">To update all packages in a solution, just use `Update-Package` by itself with no other arguments or switches.</span></span> <span data-ttu-id="0db70-155">Verwenden Sie dieses Formular mit Bedacht, da es lange dauern kann, alle Updates auszuführen:</span><span class="sxs-lookup"><span data-stu-id="0db70-155">Use this form carefully, because it can take considerable time to perform all the updates:</span></span>

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

<span data-ttu-id="0db70-156">Mit einem Update von Paketen in einem Projekt oder einer Projektmappe mithilfe von [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md), wird immer ein Update auf die neueste Version des Pakets ausgeführt (Paketvorabversionen sind davon ausgeschlossen).</span><span class="sxs-lookup"><span data-stu-id="0db70-156">Updating packages in a project or solution using [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) always updates to the latest version of the package (excluding pre-release packages).</span></span> <span data-ttu-id="0db70-157">Projekte, die `packages.config` verwenden, können – sofern gewünscht – die Updateversionen einschränken, so wie unten unter [Einschränken von Updateversionen](#constraining-upgrade-versions) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="0db70-157">Projects that use `packages.config` can, if desired, limit update versions as described below in [Constraining upgrade versions](#constraining-upgrade-versions).</span></span>

<span data-ttu-id="0db70-158">Ausführliche Informationen zu dem Befehl finden Sie unter [Updatepaket](../Tools/ps-ref-update-package.md).</span><span class="sxs-lookup"><span data-stu-id="0db70-158">For full details on the command, see the [Update-Package](../Tools/ps-ref-update-package.md) reference.</span></span>

### <a name="considerations"></a><span data-ttu-id="0db70-159">Weitere Überlegungen</span><span class="sxs-lookup"><span data-stu-id="0db70-159">Considerations</span></span>

<span data-ttu-id="0db70-160">Folgendes kann bei der Neuinstallation eines Pakets beeinträchtigt werden:</span><span class="sxs-lookup"><span data-stu-id="0db70-160">The following may be affected when reinstalling a package:</span></span>

1. <span data-ttu-id="0db70-161">**Neuinstallation von Paketen gemäß der Neuzuweisung des Projektzielframeworks**</span><span class="sxs-lookup"><span data-stu-id="0db70-161">**Reinstalling packages according to project target framework retargeting**</span></span>
    - <span data-ttu-id="0db70-162">In einem einfachen Fall funktioniert die Neuinstallation eines Pakets mithilfe von `Update-Package –reinstall <package_name>`.</span><span class="sxs-lookup"><span data-stu-id="0db70-162">In a simple case, just reinstalling a package using `Update-Package –reinstall <package_name>` works.</span></span> <span data-ttu-id="0db70-163">Ein Paket, das für ein altes Zielframework installiert wurde, wird deinstalliert, und das gleiche Paket wird für das aktuelle Zielframework des Projekts installiert.</span><span class="sxs-lookup"><span data-stu-id="0db70-163">A package that is installed against an old target framework gets uninstalled and the same package gets installed against the current target framework of the project.</span></span>
    - <span data-ttu-id="0db70-164">In einigen Fällen ist womöglich ein Paket vorhanden, das das neue Zielframework nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0db70-164">In some cases, there may be a package that does not support the new target framework.</span></span>
        - <span data-ttu-id="0db70-165">Wenn ein Paket portable Klassenbibliotheken (Portable Class Libraries, PCLs) unterstützt, und das Projekt einer Kombination aus Plattformen zugewiesen wird, die nicht länger vom Paket unterstützt werden, fehlen die Paketverweise nach der Neuinstallation.</span><span class="sxs-lookup"><span data-stu-id="0db70-165">If a package supports portable class libraries (PCLs) and the project is retargeted to a combination of platforms no longer supported by the package, references to the package will be missing after reinstalling.</span></span>
        - <span data-ttu-id="0db70-166">Dadurch können Probleme für Pakete auftreten, die Sie direkt verwenden oder für Pakete, die als Abhängigkeiten installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="0db70-166">This can surface for packages you're using directly or for packages installed as dependencies.</span></span> <span data-ttu-id="0db70-167">Es ist möglich, dass das von Ihnen direkt verwendete Paket das neue Zielframework unterstützt, obwohl dessen Abhängigkeit dies nicht tut.</span><span class="sxs-lookup"><span data-stu-id="0db70-167">It's possible for the package you're using directly to support the new target framework while its dependency does not.</span></span>
        - <span data-ttu-id="0db70-168">Wenn Sie Pakete nach der Neuzuweisung Ihrer Anwendungsergebnisse in Build- oder Runtimefehlern neu installieren, sollten Sie Ihr Zielframework wiederherstellen oder nach alternativen Paketen suchen, die Ihr neues Zielframework ordnungsgemäß unterstützen.</span><span class="sxs-lookup"><span data-stu-id="0db70-168">If reinstalling packages after retargeting your application results in build or runtime errors, you may need to revert your target framework or search for alternative packages that properly support your new target framework.</span></span>

1. <span data-ttu-id="0db70-169">**Das Attribut „requireReinstallation“ wurde in „packages.config“ nach der Projektneuzuweisung oder dem Projektupgrade hinzugefügt**</span><span class="sxs-lookup"><span data-stu-id="0db70-169">**requireReinstallation attribute added in packages.config after project retargeting or upgrade**</span></span>
    - <span data-ttu-id="0db70-170">Wenn NuGet erkennt, dass Pakete von der Neuzuweisung oder einem Upgrade eines Projekts betroffen waren, wird allen betroffenen Paketverweisen ein `requireReinstallation="true"`-Attribut in `packages.config` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="0db70-170">If NuGet detects that packages were affected by retargeting or upgrading a project, it adds a `requireReinstallation="true"` attribute in  `packages.config` to all affected package references.</span></span> <span data-ttu-id="0db70-171">Aus diesem Grund löst jeder nachfolgende Build in Visual Studio Buildwarnungen für diese Pakete aus, damit Sie daran erinnert werden, diese neu zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0db70-171">Because of this, each subsequent build in Visual Studio raises build warnings for those packages so you can remember to reinstall them.</span></span>

1. <span data-ttu-id="0db70-172">**Neuinstallation von Paketen mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="0db70-172">**Reinstalling packages with dependencies**</span></span>
    - <span data-ttu-id="0db70-173">`Update-Package –reinstall` installiert zwar die gleiche Version des ursprünglichen Pakets, es wird jedoch die neueste Version der Abhängigkeiten installiert, wenn keine bestimmten Versionseinschränkungen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="0db70-173">`Update-Package –reinstall` reinstalls the same version of the original package, but installs the latest version of dependencies unless specific version constraints are provided.</span></span> <span data-ttu-id="0db70-174">Dadurch können Sie nur die Abhängigkeiten aktualisieren, die zum Beheben eines Fehlers benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="0db70-174">This allows you to update only the dependencies as required to fix an issue.</span></span> <span data-ttu-id="0db70-175">Wenn dies jedoch eine Abhängigkeit auf eine ältere Version zurücksetzt, können Sie sie mit `Update-Package <dependency_name>` neu installieren, ohne das Abhängigkeitspaket zu beeinflussen.</span><span class="sxs-lookup"><span data-stu-id="0db70-175">However, if this rolls a dependency back to an earlier version, you can use `Update-Package <dependency_name>` to reinstall that one dependency without affecting the dependent package.</span></span>
    - <span data-ttu-id="0db70-176">`Update-Package –reinstall <packageName> -ignoreDependencies` installiert zwar die gleiche Version des ursprünglichen Pakets erneut, jedoch nicht die Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="0db70-176">`Update-Package –reinstall <packageName> -ignoreDependencies` reinstalls the same version of the original package but does not reinstall dependencies.</span></span> <span data-ttu-id="0db70-177">Nutzen Sie diese Maßnahme, wenn das Update von Paketabhängigkeiten zu einem unterbrochenen Zustand führen würde.</span><span class="sxs-lookup"><span data-stu-id="0db70-177">Use this when updating package dependencies might result in a broken state</span></span>

1. <span data-ttu-id="0db70-178">**Neuinstallation von Paketen, wenn abhängige Versionen involviert sind**</span><span class="sxs-lookup"><span data-stu-id="0db70-178">**Reinstalling packages when dependent versions are involved**</span></span>
    - <span data-ttu-id="0db70-179">Wie oben erläutert, ändert die Neuinstallation von Paketen nicht die Versionen anderer installierter Pakete, die davon abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="0db70-179">As explained above, reinstalling a package does not change versions of any other installed packages that depend on it.</span></span> <span data-ttu-id="0db70-180">Es ist dann möglich, dass die Neuinstallation einer Abhängigkeit das abhängige Paket zerstört.</span><span class="sxs-lookup"><span data-stu-id="0db70-180">It's possible, then, that reinstalling a dependency could break the dependent package.</span></span>