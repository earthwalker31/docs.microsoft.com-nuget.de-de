---
title: NuGet-CLI-Umgebungsvariablen | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Umgebungsvariablen für die nuget.exe"
keywords: NuGet-Umgebungsvariablen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 516a66103d6159a3d68b5383090e8e3b519a5588
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-cli-environment-variables"></a><span data-ttu-id="72ea8-104">NuGet-CLI-Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="72ea8-104">NuGet CLI environment variables</span></span>

<span data-ttu-id="72ea8-105">Das Verhalten von der CLI nuget.exe kann durch eine Reihe von Umgebungsvariablen, konfiguriert werden, die Auswirkungen auf nuget.exe für den gesamten Computer, Benutzer oder Ebenen verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="72ea8-105">The behavior of the nuget.exe CLI can be configured through a number of environment variables, which affect nuget.exe on computer-wide, user, or process levels.</span></span>

<span data-ttu-id="72ea8-106">Im Allgemeinen ist direkt in der Befehlszeile oder in NuGet-Konfigurationsdateien angegebene Optionen haben Vorrang vor, aber es gibt wenige Ausnahmen wie *FORCE_NUGET_EXE_INTERACTIVE*.</span><span class="sxs-lookup"><span data-stu-id="72ea8-106">In general, options specified directly on the command line or in NuGet configuration files have precedence, but there are a few exceptions such as *FORCE_NUGET_EXE_INTERACTIVE*.</span></span> <span data-ttu-id="72ea8-107">Wenn Sie, dass diese nuget.exe zwischen verschiedenen Computern unterschiedlich verhält feststellen, konnte eine Umgebungsvariable, die Ursache sein.</span><span class="sxs-lookup"><span data-stu-id="72ea8-107">If you find that nuget.exe behaves differently between different computers, an environment variable could be the cause.</span></span> <span data-ttu-id="72ea8-108">Azure Web Apps Kudu (während der Bereitstellung verwendet) hat z. B. *NUGET_XMLDOC_MODE* festgelegt *überspringen* um paketleistung für die Wiederherstellung zu beschleunigen und sparen Sie Speicherplatz.</span><span class="sxs-lookup"><span data-stu-id="72ea8-108">For example, Azure Web Apps Kudu (used during deployment) has *NUGET_XMLDOC_MODE* set to *skip* to speed up package restore performance and save disk space.</span></span>

| <span data-ttu-id="72ea8-109">Variable</span><span class="sxs-lookup"><span data-stu-id="72ea8-109">Variable</span></span> | <span data-ttu-id="72ea8-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="72ea8-110">Description</span></span> | <span data-ttu-id="72ea8-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="72ea8-111">Remarks</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72ea8-112">http_proxy</span><span class="sxs-lookup"><span data-stu-id="72ea8-112">http_proxy</span></span> | <span data-ttu-id="72ea8-113">HTTP-Proxy für NuGet-HTTP-Vorgänge verwendet.</span><span class="sxs-lookup"><span data-stu-id="72ea8-113">Http proxy used for NuGet HTTP operations.</span></span> | <span data-ttu-id="72ea8-114">Dies würde angegeben werden, als `http://<username>:<password>@proxy.com`.</span><span class="sxs-lookup"><span data-stu-id="72ea8-114">This would be specified as `http://<username>:<password>@proxy.com`.</span></span> |
| <span data-ttu-id="72ea8-115">no_proxy</span><span class="sxs-lookup"><span data-stu-id="72ea8-115">no_proxy</span></span> | <span data-ttu-id="72ea8-116">Konfiguriert die Domänen aus mithilfe der Proxy umgangen.</span><span class="sxs-lookup"><span data-stu-id="72ea8-116">Configures domains to bypass from using proxy.</span></span> | <span data-ttu-id="72ea8-117">Als Domänen, die durch Kommas (,) getrennt angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="72ea8-117">Specified as domains separated by comma (,).</span></span> |
| <span data-ttu-id="72ea8-118">EnableNuGetPackageRestore</span><span class="sxs-lookup"><span data-stu-id="72ea8-118">EnableNuGetPackageRestore</span></span> | <span data-ttu-id="72ea8-119">Ein Flag Wenn NuGet implizit Zustimmung erteilen soll, wenn dies vom Paket bei der Wiederherstellung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="72ea8-119">Flag for if NuGet should implicitly grant consent if that's required by package on restore.</span></span> | <span data-ttu-id="72ea8-120">Angegebene Kennzeichen werden angegeben.</span><span class="sxs-lookup"><span data-stu-id="72ea8-120">Specified flag is specified</span></span> | <span data-ttu-id="72ea8-121">als *"true"* oder *1*, ein anderer Wert als Flag nicht festgelegt.</span><span class="sxs-lookup"><span data-stu-id="72ea8-121">as *true* or *1*, any other value treated as flag not set.</span></span> |
| <span data-ttu-id="72ea8-122">NUGET_EXE_NO_PROMPT</span><span class="sxs-lookup"><span data-stu-id="72ea8-122">NUGET_EXE_NO_PROMPT</span></span> | <span data-ttu-id="72ea8-123">Verhindert, dass die EXE-Datei für die Aufforderung zum Eingeben von Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="72ea8-123">Prevents the exe for prompting for credentials.</span></span>| <span data-ttu-id="72ea8-124">Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Kennzeichen Satz / "true".</span><span class="sxs-lookup"><span data-stu-id="72ea8-124">Any value except null or empty string will be treated as this flag set/true.</span></span> |
<span data-ttu-id="72ea8-125">FORCE_NUGET_EXE_INTERACTIVE</span><span class="sxs-lookup"><span data-stu-id="72ea8-125">FORCE_NUGET_EXE_INTERACTIVE</span></span> | <span data-ttu-id="72ea8-126">Globale Umgebungsvariable im interaktiven Modus erzwingen.</span><span class="sxs-lookup"><span data-stu-id="72ea8-126">Global environment variable to force interactive mode.</span></span> | <span data-ttu-id="72ea8-127">Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Kennzeichen Satz / "true".</span><span class="sxs-lookup"><span data-stu-id="72ea8-127">Any value except null or empty string will be treated as this flag set/true.</span></span> |
| <span data-ttu-id="72ea8-128">NUGET_PACKAGES</span><span class="sxs-lookup"><span data-stu-id="72ea8-128">NUGET_PACKAGES</span></span> | <span data-ttu-id="72ea8-129">Pfad, in denen Pakete gespeichert bzw. zwischengespeichert werden kann.</span><span class="sxs-lookup"><span data-stu-id="72ea8-129">Path to where packages are stored / cached.</span></span> | <span data-ttu-id="72ea8-130">Als absoluter Pfad angegeben.</span><span class="sxs-lookup"><span data-stu-id="72ea8-130">Specified as absolute path.</span></span> |
| <span data-ttu-id="72ea8-131">NUGET_FALLBACK_PACKAGES</span><span class="sxs-lookup"><span data-stu-id="72ea8-131">NUGET_FALLBACK_PACKAGES</span></span> | <span data-ttu-id="72ea8-132">Globale fallback Pakete-Ordner.</span><span class="sxs-lookup"><span data-stu-id="72ea8-132">Global fallback packages folders.</span></span> | <span data-ttu-id="72ea8-133">Absolute Pfade durch Semikolon (;) getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="72ea8-133">Absolute folder paths separated by semicolon (;).</span></span> |
| <span data-ttu-id="72ea8-134">NUGET_HTTP_CACHE_PATH</span><span class="sxs-lookup"><span data-stu-id="72ea8-134">NUGET_HTTP_CACHE_PATH</span></span> | <span data-ttu-id="72ea8-135">HTTP-Cache-Ordner.</span><span class="sxs-lookup"><span data-stu-id="72ea8-135">HTTP cache folder.</span></span> | <span data-ttu-id="72ea8-136">Als absoluter Pfad angegeben.</span><span class="sxs-lookup"><span data-stu-id="72ea8-136">Specified as absolute path.</span></span> |
| <span data-ttu-id="72ea8-137">NUGET_PERSIST_DG</span><span class="sxs-lookup"><span data-stu-id="72ea8-137">NUGET_PERSIST_DG</span></span> | <span data-ttu-id="72ea8-138">Ein Flag, der angibt, wenn dg-Dateien (vom MSBuild gesammelten Daten) beibehalten werden soll.</span><span class="sxs-lookup"><span data-stu-id="72ea8-138">Flag indicating if dg files (data collected from MSBuild) should be persisted.</span></span> | <span data-ttu-id="72ea8-139">Als angegebenen *"true"* oder *"false"* (Standard), wenn NUGET_PERSIST_DG_PATH nicht festgelegt werden in temporären Verzeichnis (NuGetScratch Ordner im aktuellen Umgebung temporären Verzeichnis) gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="72ea8-139">Specified as *true* or *false* (default), if NUGET_PERSIST_DG_PATH not set will be stored to temporary directory (NuGetScratch folder in current environment temp directory).</span></span> |
| <span data-ttu-id="72ea8-140">NUGET_PERSIST_DG_PATH</span><span class="sxs-lookup"><span data-stu-id="72ea8-140">NUGET_PERSIST_DG_PATH</span></span> | <span data-ttu-id="72ea8-141">Pfad zur Verteilergruppe Dateien beizubehalten.</span><span class="sxs-lookup"><span data-stu-id="72ea8-141">Path to persist dg files.</span></span> | <span data-ttu-id="72ea8-142">Als absoluter Pfad angegeben, wird diese Option nur verwendet, wenn *NUGET_PERSIST_DG* festgelegt ist auf "true".</span><span class="sxs-lookup"><span data-stu-id="72ea8-142">Specified as absolute path, this option is only used when *NUGET_PERSIST_DG* is set to true.</span></span> |
| <span data-ttu-id="72ea8-143">NUGET_RESTORE_MSBUILD_ARGS</span><span class="sxs-lookup"><span data-stu-id="72ea8-143">NUGET_RESTORE_MSBUILD_ARGS</span></span> | <span data-ttu-id="72ea8-144">Legt zusätzliche MSBuild-Argumente.</span><span class="sxs-lookup"><span data-stu-id="72ea8-144">Sets additional MSBuild arguments.</span></span> |
| <span data-ttu-id="72ea8-145">NUGET_RESTORE_MSBUILD_</span><span class="sxs-lookup"><span data-stu-id="72ea8-145">NUGET_RESTORE_MSBUILD_</span></span>| <span data-ttu-id="72ea8-146">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="72ea8-146">Verbosity</span></span> |<span data-ttu-id="72ea8-147">Legt die Ausführlichkeit der MSBuild-Protokoll.</span><span class="sxs-lookup"><span data-stu-id="72ea8-147">Sets the MSBuild log verbosity.</span></span> | <span data-ttu-id="72ea8-148">Standardmäßig wird *stillen* ("/ V: Q").</span><span class="sxs-lookup"><span data-stu-id="72ea8-148">Default is *quiet* ("/v:q").</span></span> <span data-ttu-id="72ea8-149">Mögliche Werte *Q [Uiet]*, *m [mindestens]*, *n [Ormal]*, *d [etaillierte]*, und *Diag [Nostic]*.</span><span class="sxs-lookup"><span data-stu-id="72ea8-149">Possible values *q[uiet]*, *m[inimal]*, *n[ormal]*, *d[etailed]*, and *diag[nostic]*.</span></span> |
| <span data-ttu-id="72ea8-150">NUGET_SHOW_STACK</span><span class="sxs-lookup"><span data-stu-id="72ea8-150">NUGET_SHOW_STACK</span></span> | <span data-ttu-id="72ea8-151">Bestimmt, ob der Benutzer die vollständige Ausnahme (einschließlich stapelüberwachung) angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="72ea8-151">Determines whether the full exception (including stack trace) should be displayed to the user.</span></span> | <span data-ttu-id="72ea8-152">Als angegebenen *"true"* oder *"false"* (Standard).</span><span class="sxs-lookup"><span data-stu-id="72ea8-152">Specified as *true* or *false* (default).</span></span> |
| <span data-ttu-id="72ea8-153">NUGET_XMLDOC_MODE</span><span class="sxs-lookup"><span data-stu-id="72ea8-153">NUGET_XMLDOC_MODE</span></span> | <span data-ttu-id="72ea8-154">Bestimmt, wie Assemblys XML-Dokumentation Datei extrahieren behandelt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="72ea8-154">Determines how assemblies XML documentation file extraction should be handled.</span></span> | <span data-ttu-id="72ea8-155">Sind Sie unterstützten Modi *überspringen* (XML-Dokumentationsdateien nicht extrahieren), *komprimieren* (Speichern von XML-Dokumentationsdateien als Zip-Archiv) oder *keine* (default, XML-Dokumentationsdateien als reguläre behandeln -Dateien).</span><span class="sxs-lookup"><span data-stu-id="72ea8-155">Supported modes are *skip* (do not extract XML documentation files), *compress* (store XML doc files as a zip archive) or *none* (default, treat XML doc files as regular files).</span></span> |