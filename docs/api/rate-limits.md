---
title: Begrenzung der Datenübertragungsrate NuGet-API
description: Die NuGet-APIs werden erzwungen, um Missbrauch zu verhindern, dass die Begrenzung der Datenübertragungsrate haben.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/17/2018
---
# <a name="rate-limits"></a><span data-ttu-id="ff4cc-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="ff4cc-103">Rate Limits</span></span>

<span data-ttu-id="ff4cc-104">Der NuGet.org-API erzwingt die Begrenzung der Übertragungsrate um Missbrauch zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="ff4cc-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ff4cc-105">Anforderungen, die die Begrenzung überschreiten zurückgegeben der folgende Fehler:</span><span class="sxs-lookup"><span data-stu-id="ff4cc-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ff4cc-106">Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die NuGet.org-API.</span><span class="sxs-lookup"><span data-stu-id="ff4cc-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ff4cc-107">Paket-Suche</span><span class="sxs-lookup"><span data-stu-id="ff4cc-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="ff4cc-108">Es wird empfohlen, sich der NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken.</span><span class="sxs-lookup"><span data-stu-id="ff4cc-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="ff4cc-109">Suchen Sie nach V1 und V2 APIs, die Grenzwerte Followins gelten:</span><span class="sxs-lookup"><span data-stu-id="ff4cc-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="ff4cc-110">API</span><span class="sxs-lookup"><span data-stu-id="ff4cc-110">API</span></span> | <span data-ttu-id="ff4cc-111">Limittyp</span><span class="sxs-lookup"><span data-stu-id="ff4cc-111">Limit Type</span></span> | <span data-ttu-id="ff4cc-112">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="ff4cc-112">Limit Value</span></span> | <span data-ttu-id="ff4cc-113">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ff4cc-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ff4cc-114">**ERHALTEN** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ff4cc-115">IP</span><span class="sxs-lookup"><span data-stu-id="ff4cc-115">IP</span></span> | <span data-ttu-id="ff4cc-116">1000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ff4cc-116">1000 / minute</span></span> | <span data-ttu-id="ff4cc-117">Abfragen von Metadaten von NuGet-Paketen über OData v1 `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ff4cc-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ff4cc-118">**ERHALTEN** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ff4cc-119">IP</span><span class="sxs-lookup"><span data-stu-id="ff4cc-119">IP</span></span> | <span data-ttu-id="ff4cc-120">3000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ff4cc-120">3000 / minute</span></span> | <span data-ttu-id="ff4cc-121">Suchen Sie nach NuGet-Pakete über einen Endpunkt für v1-Suche</span><span class="sxs-lookup"><span data-stu-id="ff4cc-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ff4cc-122">**ERHALTEN** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ff4cc-123">IP</span><span class="sxs-lookup"><span data-stu-id="ff4cc-123">IP</span></span> | <span data-ttu-id="ff4cc-124">20000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ff4cc-124">20000 / minute</span></span> | <span data-ttu-id="ff4cc-125">Abfragen von Metadaten von NuGet-Paketen über OData v2 `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ff4cc-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ff4cc-126">**ERHALTEN** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ff4cc-127">IP</span><span class="sxs-lookup"><span data-stu-id="ff4cc-127">IP</span></span> | <span data-ttu-id="ff4cc-128">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="ff4cc-128">100 / minute</span></span> | <span data-ttu-id="ff4cc-129">Anzahl von NuGet-Paket über v2 OData-Abfrage `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ff4cc-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ff4cc-130">Paket Push-als auch Benutzerauswahl</span><span class="sxs-lookup"><span data-stu-id="ff4cc-130">Package Push and Unlist</span></span>

| <span data-ttu-id="ff4cc-131">API</span><span class="sxs-lookup"><span data-stu-id="ff4cc-131">API</span></span> | <span data-ttu-id="ff4cc-132">Limittyp</span><span class="sxs-lookup"><span data-stu-id="ff4cc-132">Limit Type</span></span> | <span data-ttu-id="ff4cc-133">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="ff4cc-133">Limit Value</span></span> | <span data-ttu-id="ff4cc-134">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ff4cc-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ff4cc-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ff4cc-136">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ff4cc-136">API Key</span></span> | <span data-ttu-id="ff4cc-137">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="ff4cc-137">250 / hour</span></span> | <span data-ttu-id="ff4cc-138">Hochladen Sie über v2-Push-Endpunkt ein neues NuGet-Paket (Version)</span><span class="sxs-lookup"><span data-stu-id="ff4cc-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ff4cc-139">**LÖSCHEN** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ff4cc-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ff4cc-140">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ff4cc-140">API Key</span></span> | <span data-ttu-id="ff4cc-141">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="ff4cc-141">250 / hour</span></span> | <span data-ttu-id="ff4cc-142">NuGet-Paket (Version) über einen Endpunkt v2 Benutzerauswahl</span><span class="sxs-lookup"><span data-stu-id="ff4cc-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 