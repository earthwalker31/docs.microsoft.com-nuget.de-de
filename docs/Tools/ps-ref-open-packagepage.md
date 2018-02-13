---
title: "NuGet-öffnen-PackagePage-PowerShell-Referenz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für Open PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Open PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d829c-104">Open-PackagePage (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d829c-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d829c-105">*In 3.0 veraltet. verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="d829c-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d829c-106">Startet den Standardbrowser mit dem Projekt, Lizenzen oder Missbrauch Berichts-URL für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="d829c-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d829c-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="d829c-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d829c-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="d829c-108">Parameters</span></span>

| <span data-ttu-id="d829c-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="d829c-109">Parameter</span></span> | <span data-ttu-id="d829c-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d829c-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d829c-111">Id</span><span class="sxs-lookup"><span data-stu-id="d829c-111">Id</span></span> | <span data-ttu-id="d829c-112">Die Paket-ID mit dem gewünschten Paket.</span><span class="sxs-lookup"><span data-stu-id="d829c-112">The package ID of the desired package.</span></span> <span data-ttu-id="d829c-113">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="d829c-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d829c-114">Version</span><span class="sxs-lookup"><span data-stu-id="d829c-114">Version</span></span> | <span data-ttu-id="d829c-115">Die Version des Pakets, auf die neueste Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="d829c-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d829c-116">Quelle</span><span class="sxs-lookup"><span data-stu-id="d829c-116">Source</span></span> | <span data-ttu-id="d829c-117">Die ausgewählte Quelle in der Quelle Dropdownelement direktionales Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="d829c-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d829c-118">Lizenz</span><span class="sxs-lookup"><span data-stu-id="d829c-118">License</span></span> | <span data-ttu-id="d829c-119">Öffnet den Browser, um des Pakets Lizenz-URL an.</span><span class="sxs-lookup"><span data-stu-id="d829c-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d829c-120">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="d829c-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d829c-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d829c-121">ReportAbuse</span></span> | <span data-ttu-id="d829c-122">Öffnet den Browser, um des Pakets Berichts Missbrauch-URL an.</span><span class="sxs-lookup"><span data-stu-id="d829c-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d829c-123">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="d829c-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d829c-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="d829c-124">PassThru</span></span> | <span data-ttu-id="d829c-125">Zeigt die URL an. Verwenden Sie mit "-WhatIf" unterdrückt werden, öffnen den Browser.</span><span class="sxs-lookup"><span data-stu-id="d829c-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d829c-126">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="d829c-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d829c-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="d829c-127">Common Parameters</span></span>

<span data-ttu-id="d829c-128">`Open-PackagePage`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d829c-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d829c-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d829c-129">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```