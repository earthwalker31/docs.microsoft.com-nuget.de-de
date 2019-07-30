---
title: PowerShell-Referenz zu nuget-PowerShell-Paketen
description: Referenz für den PowerShell-Befehl "Find-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327387"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="18e1f-103">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="18e1f-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="18e1f-104">*Version 3.0 und höher in diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Find-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="18e1f-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="18e1f-105">Ruft den Satz von Remote Paketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="18e1f-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="18e1f-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="18e1f-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="18e1f-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="18e1f-107">Parameters</span></span>

| <span data-ttu-id="18e1f-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="18e1f-108">Parameter</span></span> | <span data-ttu-id="18e1f-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="18e1f-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18e1f-110">ID &lt;-Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="18e1f-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="18e1f-111">Benötigten Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="18e1f-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="18e1f-112">Verwenden Sie-exactMatch, um nur Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="18e1f-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="18e1f-113">Wenn keine Schlüsselwörter angegeben werden `Find-Package` , wird von eine Liste mit den Top 20 Paketen nach Downloads oder der durch-First angegebenen Zahl zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="18e1f-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="18e1f-114">Beachten Sie, dass-ID optional und ein No-op-Wert ist.</span><span class="sxs-lookup"><span data-stu-id="18e1f-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="18e1f-115">Source</span><span class="sxs-lookup"><span data-stu-id="18e1f-115">Source</span></span> | <span data-ttu-id="18e1f-116">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="18e1f-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="18e1f-117">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="18e1f-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="18e1f-118">Wenn kein Wert `Find-Package` angezeigt wird, wird die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="18e1f-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="18e1f-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="18e1f-119">AllVersions</span></span> | <span data-ttu-id="18e1f-120">Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an.</span><span class="sxs-lookup"><span data-stu-id="18e1f-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="18e1f-121">Erster</span><span class="sxs-lookup"><span data-stu-id="18e1f-121">First</span></span> | <span data-ttu-id="18e1f-122">Die Anzahl der Pakete, die ab dem Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="18e1f-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="18e1f-123">Skip</span><span class="sxs-lookup"><span data-stu-id="18e1f-123">Skip</span></span> | <span data-ttu-id="18e1f-124">Lässt die ersten &lt;int&gt; -Pakete aus der angezeigten Liste aus.</span><span class="sxs-lookup"><span data-stu-id="18e1f-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="18e1f-125">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="18e1f-125">IncludePrerelease</span></span> | <span data-ttu-id="18e1f-126">Schließt vorab Pakete in die Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="18e1f-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="18e1f-127">"ExactMatch"</span><span class="sxs-lookup"><span data-stu-id="18e1f-127">ExactMatch</span></span> | <span data-ttu-id="18e1f-128">Wird angegeben, &lt;um&gt; Schlüsselwörter als Paket-ID zu verwenden</span><span class="sxs-lookup"><span data-stu-id="18e1f-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="18e1f-129">Startmit</span><span class="sxs-lookup"><span data-stu-id="18e1f-129">StartWith</span></span> | <span data-ttu-id="18e1f-130">Gibt Pakete zurück, deren Paket- &lt;ID&gt;mit Schlüsselwörtern beginnt.</span><span class="sxs-lookup"><span data-stu-id="18e1f-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="18e1f-131">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="18e1f-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="18e1f-132">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="18e1f-132">Common Parameters</span></span>

<span data-ttu-id="18e1f-133">`Find-Package`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="18e1f-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="18e1f-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="18e1f-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```