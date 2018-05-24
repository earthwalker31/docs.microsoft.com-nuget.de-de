---
title: Referenz zu PowerShell-Sync-NuGet-Pakets
description: Referenz für die Sync-Paket-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="dbbfa-103">Sync-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="dbbfa-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dbbfa-104">*Version 3.0 +; verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="dbbfa-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="dbbfa-105">Ruft die Version des installierten Pakets aus einer angegebenen (oder Standard)-Projekt und synchronisiert die Version mit den restlichen Projekten in der Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="dbbfa-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="dbbfa-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="dbbfa-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="dbbfa-107">Parameters</span></span>

| <span data-ttu-id="dbbfa-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="dbbfa-108">Parameter</span></span> | <span data-ttu-id="dbbfa-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dbbfa-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dbbfa-110">Id</span><span class="sxs-lookup"><span data-stu-id="dbbfa-110">Id</span></span> | <span data-ttu-id="dbbfa-111">(Erforderlich) Der Bezeichner des Pakets zu synchronisieren. Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="dbbfa-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="dbbfa-112">IgnoreDependencies</span></span> | <span data-ttu-id="dbbfa-113">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="dbbfa-114">ProjektName</span><span class="sxs-lookup"><span data-stu-id="dbbfa-114">ProjectName</span></span> | <span data-ttu-id="dbbfa-115">Das Projekt, um das Paket aus, auf das Standardprojekt direktionales zu synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="dbbfa-116">Version</span><span class="sxs-lookup"><span data-stu-id="dbbfa-116">Version</span></span> | <span data-ttu-id="dbbfa-117">Die Version des Pakets zu synchronisieren, die derzeit installierte Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="dbbfa-118">Quelle</span><span class="sxs-lookup"><span data-stu-id="dbbfa-118">Source</span></span> | <span data-ttu-id="dbbfa-119">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="dbbfa-120">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="dbbfa-121">Wenn nicht angegeben, `Sync-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="dbbfa-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="dbbfa-122">IncludePrerelease</span></span> | <span data-ttu-id="dbbfa-123">Enthält vorabversionspakete in die Synchronisierung.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="dbbfa-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="dbbfa-124">FileConflictAction</span></span> | <span data-ttu-id="dbbfa-125">Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="dbbfa-126">Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *(3.0 und höher)* *' ignoreall '*.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="dbbfa-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="dbbfa-127">DependencyVersion</span></span> | <span data-ttu-id="dbbfa-128">Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="dbbfa-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="dbbfa-129">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="dbbfa-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="dbbfa-130">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="dbbfa-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="dbbfa-131">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="dbbfa-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="dbbfa-132">*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="dbbfa-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="dbbfa-133">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="dbbfa-134">"WhatIf"</span><span class="sxs-lookup"><span data-stu-id="dbbfa-134">WhatIf</span></span> | <span data-ttu-id="dbbfa-135">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung ausführen.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="dbbfa-136">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dbbfa-137">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="dbbfa-137">Common Parameters</span></span>

<span data-ttu-id="dbbfa-138">`Sync-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dbbfa-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dbbfa-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="dbbfa-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```