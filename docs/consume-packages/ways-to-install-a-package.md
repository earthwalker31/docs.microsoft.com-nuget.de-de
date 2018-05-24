---
title: Möglichkeiten zum Installieren von NuGet-Paketen
description: Beschreibt den Prozess der Installation von NuGet-Pakete in ein Projekt, inklusive, was auf dem Datenträger und mit anwendbaren Projektdateien passiert.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 028fb9710e808974348d9cca3c56103c087d5390
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a><span data-ttu-id="bac75-103">Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="bac75-103">Different ways to install a NuGet Package</span></span>

<span data-ttu-id="bac75-104">NuGet-Pakete werden mithilfe einer der Methoden in den folgenden Tabellen heruntergeladen und installiert (siehe [Install NuGet client tools (Installieren von NuGet-Clienttools)](../install-nuget-client-tools.md), falls Sie diese noch nicht installiert haben).</span><span class="sxs-lookup"><span data-stu-id="bac75-104">NuGet packages are downloaded and installed using any of the methods in the following table (see [Install NuGet client tools](../install-nuget-client-tools.md) if you don't have these installed already).</span></span> <span data-ttu-id="bac75-105">Das Paket wird möglicherweise aus dem Cache abgerufen und nicht heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="bac75-105">The package may be retrieved from a cache instead of downloaded.</span></span>

| <span data-ttu-id="bac75-106">Methode</span><span class="sxs-lookup"><span data-stu-id="bac75-106">Method</span></span> | <span data-ttu-id="bac75-107">description</span><span class="sxs-lookup"><span data-stu-id="bac75-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bac75-108">dotnet.exe-CLI</span><span class="sxs-lookup"><span data-stu-id="bac75-108">dotnet.exe CLI</span></span><br/>`dotnet add package <package_name>` | <span data-ttu-id="bac75-109">(Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird abgerufen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt, und ein Verweis zur Projektdatei wird hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="bac75-109">(All platforms) Retrieves the package identified by \<package_name\>, expands its contents into a folder in the current directory, and adds a reference to the project file.</span></span> <span data-ttu-id="bac75-110">Ruft auch Abhängigkeiten ab und installiert sie.</span><span class="sxs-lookup"><span data-stu-id="bac75-110">Also retrieves and installs dependencies.</span></span><ul><li>[<span data-ttu-id="bac75-111">Installieren und Verwenden eines Pakets (dotnet-CLI)</span><span class="sxs-lookup"><span data-stu-id="bac75-111">Install and use a package (dotnet CLI)</span></span>](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[<span data-ttu-id="bac75-112">Befehl „dotnet add package“</span><span class="sxs-lookup"><span data-stu-id="bac75-112">dotnet add package command</span></span>](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| <span data-ttu-id="bac75-113">Benutzeroberfläche des Paket-Managers (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bac75-113">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="bac75-114">(Windows und Mac) Bietet eine Benutzeroberfläche, über die Sie die Liste der Pakete durchsuchen, Pakete auswählen und diese Pakete und ihre Abhängigkeiten in ein Projekt aus einer angegebenen Paketquelle installieren können.</span><span class="sxs-lookup"><span data-stu-id="bac75-114">(Windows and Mac) Provides a UI through which you can browse, select, and install packages and their dependencies into a project from a specified package source.</span></span> <span data-ttu-id="bac75-115">Fügt der Projektdatei Verweise auf installierte Pakete zu.</span><span class="sxs-lookup"><span data-stu-id="bac75-115">Adds references to installed packages to the project file.</span></span><ul><li>[<span data-ttu-id="bac75-116">Installieren und Verwenden eines Pakets (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bac75-116">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="bac75-117">Referenz zur Benutzeroberfläche des Paket-Managers (Windows)</span><span class="sxs-lookup"><span data-stu-id="bac75-117">Package Manager UI reference (Windows)</span></span>](../tools/package-manager-ui.md)</li><li>[<span data-ttu-id="bac75-118">Einschließen eines NuGet-Pakets in Ihr Projekt (Mac)</span><span class="sxs-lookup"><span data-stu-id="bac75-118">Including a NuGet package in your project (Mac)</span></span>](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| <span data-ttu-id="bac75-119">Paket-Manager-Konsole (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bac75-119">Package Manager Console (Visual Studio)</span></span><br/>`Install-Package <package_name>` | <span data-ttu-id="bac75-120">(Nur Windows) Ruft das Paket ab, das durch \<package_name\> identifiziert wurde, und installiert es aus einer ausgewählten Quelle in ein angegebenes Projekt in der Projektmappe und fügt dann einen Verweis zur Projektdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="bac75-120">(Windows only) Retrieves and installs the package identified by \<package_name\> from a selected source into a specified project in the solution, then adds a reference to the project file.</span></span> <span data-ttu-id="bac75-121">Ruft auch Abhängigkeiten ab und installiert sie.</span><span class="sxs-lookup"><span data-stu-id="bac75-121">Also retrieves and installs dependencies.</span></span><ul><li>[<span data-ttu-id="bac75-122">Installieren und Verwenden eines Pakets (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bac75-122">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="bac75-123">Leitfaden für die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="bac75-123">Package Manager Console guide</span></span>](../tools/package-manager-console.md)</li></ul> |
| <span data-ttu-id="bac75-124">nuget.exe-CLI</span><span class="sxs-lookup"><span data-stu-id="bac75-124">nuget.exe CLI</span></span><br/>`nuget install <package_name>` | <span data-ttu-id="bac75-125">(Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird abgerufen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt. Kann auch alle Pakete abrufen, die in einer `packages.config`-Datei aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="bac75-125">(All platforms) Retrieves the package identified by \<package_name\> and expands its contents into a folder in the current directory; can also retrieve all packages listed in a `packages.config` file.</span></span> <span data-ttu-id="bac75-126">Ruft außerdem Abhängigkeiten ab und installiert sie, nimmt aber keine Änderungen an Projektdateien oder `packages.config` vor.</span><span class="sxs-lookup"><span data-stu-id="bac75-126">Also retrieves and installs dependencies, but makes no changes to project files or `packages.config`.</span></span><ul><li>[<span data-ttu-id="bac75-127">install-Befehl</span><span class="sxs-lookup"><span data-stu-id="bac75-127">install command</span></span>](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a><span data-ttu-id="bac75-128">Nach der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="bac75-128">What happens when a package is installed</span></span>

<span data-ttu-id="bac75-129">Die verschiedenen NuGet-Tools erstellen typischerweise einen Verweis auf ein Paket in der Projektdatei oder `packages.config` und führen dann eine Paketwiederherstellung durch, die das Paket effektiv installiert.</span><span class="sxs-lookup"><span data-stu-id="bac75-129">Simply said, the different NuGet tools typically create a reference to a package in the project file or `packages.config`, then perform a package restore, which effectively installs the package.</span></span> <span data-ttu-id="bac75-130">`nuget install` ist die Ausnahme, bei der das Paket nur in einen `packages`-Ordner erweitert wird, andere Dateien jedoch unverändert bleiben.</span><span class="sxs-lookup"><span data-stu-id="bac75-130">The exception is `nuget install`, which only expands the package into a `packages` folder and does not modify any other files.</span></span>

<span data-ttu-id="bac75-131">Im Allgemeinen läuft der Prozess wie folgt ab:</span><span class="sxs-lookup"><span data-stu-id="bac75-131">The general process is as follows:</span></span>

1. <span data-ttu-id="bac75-132">(Alle Tools außer `nuget.exe`) Speichern Sie den Paketbezeichner und die Paketversion in der Projektdatei oder `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bac75-132">(All tools except `nuget.exe`) Record the package identifer and version into the project file or `packages.config`.</span></span>

2. <span data-ttu-id="bac75-133">Erhalten des Pakets:</span><span class="sxs-lookup"><span data-stu-id="bac75-133">Acquire the package:</span></span>
   - <span data-ttu-id="bac75-134">Überprüfen Sie, ob das Paket (mit exaktem Bezeichner und Versionsnummer) bereits im Ordner *global-packages* installiert ist, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bac75-134">Check if the package (by exact identifer and version number) is already installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

   - <span data-ttu-id="bac75-135">Wenn sich das Paket nicht im Ordner *global-packages* befindet, versuchen Sie, es aus den in den [Konfigurationsdateien](Configuring-NuGet-Behavior.md) aufgelisteten Quellen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="bac75-135">If the package is not in the *global-packages* folder, attempt to retrieve it from the sources listed listed in the [configuration files](Configuring-NuGet-Behavior.md).</span></span> <span data-ttu-id="bac75-136">Bei Onlinequellen versuchen Sie zuerst, das Paket aus dem Cache abzurufen, es sei denn, `-NoCache` wird mit `nuget.exe`-Befehlen oder `--no-cache` mit `dotnet restore` angegeben.</span><span class="sxs-lookup"><span data-stu-id="bac75-136">For online sources, attempt first to retrieve the package from the cache unless `-NoCache` is specified with `nuget.exe` commands or `--no-cache` is specified with `dotnet restore`.</span></span> <span data-ttu-id="bac75-137">(Visual Studio und `dotnet add package` verwenden immer den Cache.) Wenn ein Paket aus dem Cache verwendet wird, erscheint „CACHE“ in der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="bac75-137">(Visual Studio and `dotnet add package` always use the cache.) If a package is used from the cache, "CACHE" appears in the output.</span></span> <span data-ttu-id="bac75-138">Die Ablaufzeit des Caches beträgt 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="bac75-138">The cache has an expiration time of 30 minutes.</span></span>

   - <span data-ttu-id="bac75-139">Wenn sich das Paket nicht im Cache befindet, versuchen Sie, es aus den in der Konfiguration aufgeführten Quellen herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="bac75-139">If the package is not in the cache, attempt to download it from the sources listed in the configuration.</span></span> <span data-ttu-id="bac75-140">Wird ein Paket heruntergeladen, erscheinen „GET“ und „OK“ in der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="bac75-140">If a package is downloaded, "GET" and "OK" appear in the output.</span></span>

   - <span data-ttu-id="bac75-141">Wenn das Paket nicht erfolgreich aus einer Quelle bezogen werden kann, tritt bei der Installation an dieser Stelle ein Fehler auf, z.B. [NU1103](../reference/errors-and-warnings.md#nu1103).</span><span class="sxs-lookup"><span data-stu-id="bac75-141">If the package cannot be successfully acquired from any sources, installation fails at this point with an error such as [NU1103](../reference/errors-and-warnings.md#nu1103).</span></span> <span data-ttu-id="bac75-142">Beachten Sie, dass Fehler von `nuget.exe`-Befehlen nur die zuletzt geprüfte Quelle anzeigen, aber implizieren, dass das Paket aus keiner Quelle abgerufen werden konnte.</span><span class="sxs-lookup"><span data-stu-id="bac75-142">Note that errors from `nuget.exe` commands show only the last source checked, but implies that the package wasn't available from any source.</span></span>

   <span data-ttu-id="bac75-143">Beim Beziehen des Pakets gilt möglicherweise die Reihenfolge der Quellen in der NuGet-Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="bac75-143">When acquiring the package, the order of sources in the NuGet configuration may apply:</span></span>

   - <span data-ttu-id="bac75-144">Bei Projekten, die das PackageReference-Format verwenden, prüft NuGet zuerst die lokalen Ordner und Netzwerkfreigaben der Quellen und dann erst HTTP-Quellen.</span><span class="sxs-lookup"><span data-stu-id="bac75-144">For projects using the PackageReference format, NuGet checks sources local folder and network shares before checking HTTP sources.</span></span>

   - <span data-ttu-id="bac75-145">Bei Projekten, die das Verwaltungsformat `packages.config` verwenden, übernimmt NuGet die Reihenfolge der Quellen in der Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="bac75-145">For projects using the `packages.config` management format, NuGet uses the order of the sources in the configuration.</span></span> <span data-ttu-id="bac75-146">Eine Ausnahme sind Wiederherstellungsvorgänge, bei denen die Reihenfolge der Quellen ignoriert wird und NuGet das Paket verwendet, von dem die Quelle zuerst antwortet.</span><span class="sxs-lookup"><span data-stu-id="bac75-146">An exception is restore operations, in which case source ordering is ignored and NuGet uses the package from whichever source responds first.</span></span>

   - <span data-ttu-id="bac75-147">Im Allgemeinen spielt die Reihenfolge, in der NuGet Quellen überprüft, keine besondere Rolle, weil jedes Paket mit einem bestimmten Bezeichner und einer bestimmten Versionsnummer unabhängig von der Quelle, in der es sich befindet, genau identisch ist.</span><span class="sxs-lookup"><span data-stu-id="bac75-147">In general, the order in which NuGet checks sources isn't particularly meaningful, because any given package with a specific identifier and version number is exactly the same on whatever source it's found.</span></span>

3. <span data-ttu-id="bac75-148">(Alle Tools außer `nuget.exe`) Speichern Sie eine Kopie des Pakets und andere Informationen im Ordner *http-cache*, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bac75-148">(All tools except `nuget.exe`) Save a copy of the package and other information in the *http-cache* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

4. <span data-ttu-id="bac75-149">Wenn Sie das Paket heruntergeladen haben, installieren Sie es pro Benutzer im Ordner *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="bac75-149">If downloaded, install the package into the per-user *global-packages* folder.</span></span> <span data-ttu-id="bac75-150">NuGet erstellt einen Unterordner für jeden Paketbezeichner und erstellt dann Unterordner für jede installierte Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="bac75-150">NuGet creates a subfolder for each package identifier, then creates subfolders for each installed version of the package.</span></span>

5. <span data-ttu-id="bac75-151">Aktualisieren Sie andere Projektdateien und -ordner:</span><span class="sxs-lookup"><span data-stu-id="bac75-151">Update other project files and folders:</span></span>

    - <span data-ttu-id="bac75-152">Bei Projekten, die PackageReference verwenden, aktualisieren Sie das in `obj/project.assets.json` gespeicherte Abhängigkeitsdiagramm für das Paket.</span><span class="sxs-lookup"><span data-stu-id="bac75-152">For projects using PackageReference, update the package dependency graph stored in `obj/project.assets.json`.</span></span> <span data-ttu-id="bac75-153">Paketinhalte selbst werden nicht in einen Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="bac75-153">Package contents themselves are not copied into any project folder.</span></span>
    - <span data-ttu-id="bac75-154">Bei Projekten, die `packages.config` verwenden, kopieren Sie die Teile des erweiterten Pakets, die dem Zielframework des Projekts entsprechen, in den `packages`-Ordner des Projekts.</span><span class="sxs-lookup"><span data-stu-id="bac75-154">For projects using `packages.config`, copy those parts of the expanded package that match the project's target framework into project's `packages` folder.</span></span> <span data-ttu-id="bac75-155">(Bei der Verwendung von `nuget install` wird das gesamte erweiterte Paket kopiert, da `nuget.exe` zum Identifizieren des Zielframeworks keine Projektdateien untersucht.)</span><span class="sxs-lookup"><span data-stu-id="bac75-155">(When using `nuget install`, the entire expanded package is copied because `nuget.exe` does not examine project files to identify the target framework.)</span></span>
    - <span data-ttu-id="bac75-156">Aktualisieren Sie `app.config` und/oder `web.config`, wenn das Paket [Transformationen von Quell- und Konfigurationsdateien](../create-packages/source-and-config-file-transformations.md) verwendet.</span><span class="sxs-lookup"><span data-stu-id="bac75-156">Update `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>

6. <span data-ttu-id="bac75-157">Installieren Sie alle untergeordneten Abhängigkeiten, die nicht bereits im Projekt vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="bac75-157">Install any down-level dependencies if not already present in the project.</span></span> <span data-ttu-id="bac75-158">Möglicherweise werden bei diesem Prozess Paketversionen im Prozess aktualisiert, wie in [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bac75-158">This process might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>

7. <span data-ttu-id="bac75-159">(Nur Visual Studio) Zeigt die Infodatei des Pakets, falls vorhanden, in einem Visual Studio-Fenster.</span><span class="sxs-lookup"><span data-stu-id="bac75-159">(Visual Studio only) Display the package's readme file, if available, in a Visual Studio window.</span></span>

## <a name="related-articles"></a><span data-ttu-id="bac75-160">Verwandte Artikel</span><span class="sxs-lookup"><span data-stu-id="bac75-160">Related articles</span></span>

- [<span data-ttu-id="bac75-161">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="bac75-161">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="bac75-162">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="bac75-162">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="bac75-163">Verwalten des Cacheordners und des Ordners „global-packages“ von NuGet</span><span class="sxs-lookup"><span data-stu-id="bac75-163">Managing the NuGet cache and global-packages folders</span></span>](managing-the-global-packages-and-cache-folders.md)
- [<span data-ttu-id="bac75-164">Konfigurieren des NuGet-Verhaltens</span><span class="sxs-lookup"><span data-stu-id="bac75-164">Configuring NuGet behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)