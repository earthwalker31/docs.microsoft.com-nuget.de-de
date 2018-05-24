---
title: NuGet-3,0 Beta-Anmerkungen zu dieser Version
description: Versionshinweise für NuGet 3.0 Beta, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="99451-103">NuGet-3,0 Beta-Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="99451-103">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="99451-104">[Anmerkungen zur Version von NuGet-3.0-Vorschau](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC-Versionsanmerkungen](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="99451-104">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="99451-105">NuGet-3.0 Beta wurde für die Version von Visual Studio 2015 CTP-Version 6 auf 23 Februar 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="99451-105">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="99451-106">Diese Version bedeutet, dass viel unseres Teams wie wir eine Reihe von Architektur und Performance zur Freigabe haben, und wir freuen uns zum Starten der Optimierung der Leistungseinstellungen auf unseren nuget.org-Dienst.</span><span class="sxs-lookup"><span data-stu-id="99451-106">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="99451-107">Es wird dringend empfohlen, dass eine frühere Version der Erweiterung NuGet Visual Studio 2015 deinstallieren, bevor Sie diese neue Version installieren.</span><span class="sxs-lookup"><span data-stu-id="99451-107">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="99451-108">Wenn Sie Probleme mit dieser Version der Erweiterung auftreten, sollten Sie Sie wiederherstellen, um die [Vorgängerversionen](http://nuget.codeplex.com/downloads/get/909582) für die Verwendung mit Visual Studio 2015 Preview.</span><span class="sxs-lookup"><span data-stu-id="99451-108">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="99451-109">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="99451-109">Visual Studio 2012+</span></span>

<span data-ttu-id="99451-110">Dieses NuGet-3.0 Beta ist für die Installation in der Visual Studio 2015 CTP-Version 6 Erweiterung Gallery verfügbar.</span><span class="sxs-lookup"><span data-stu-id="99451-110">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="99451-111">Wir arbeiten daran, löscht der Preview für Visual Studio 2012 und Visual Studio 2013 sehr schnell abzurufen.</span><span class="sxs-lookup"><span data-stu-id="99451-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="99451-112">Wir haben unsere versucht, eine zuvor freigegeben [Updates für Visual Studio 2010 eingestellt](http://blog.nuget.org/20141002/visual-studio-2010.html), und wir haben diese schwierige Entscheidung vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="99451-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="99451-113">Neue Client/Server-API</span><span class="sxs-lookup"><span data-stu-id="99451-113">New Client/Server API</span></span>

<span data-ttu-id="99451-114">Wir haben einige Implementierungsdetails für NuGet Client/Server-Protokoll gearbeitet.</span><span class="sxs-lookup"><span data-stu-id="99451-114">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="99451-115">Unsere Arbeit ist die Erstellung von "API v3" für NuGet, das entworfen wurde, um hohe Verfügbarkeit für kritische Szenarien wie paketwiederherstellung und Installieren von Paketen.</span><span class="sxs-lookup"><span data-stu-id="99451-115">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="99451-116">Die neue API basiert auf REST und Hypermedia und wir ausgewählt haben [JSON-LD](http://json-ld.org) als Ressourcenformat.</span><span class="sxs-lookup"><span data-stu-id="99451-116">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="99451-117">Die Bits NuGet 3.0 Beta finden Sie unter neue Paketquelle "api.nuget.org" in der Dropdownliste der Paket-Quelle aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="99451-117">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="99451-118">Bei Auswahl dieser Paketquelle verwenden wir unserer neuen API zur Verbindung mit nuget.org. In NuGet 3.0 RC ersetzt dieser neuen API v3-basierte Paketquelle die Paketquelle v2-basierte "nuget.org".</span><span class="sxs-lookup"><span data-stu-id="99451-118">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="99451-119">Deaktivieren alle anderen öffentlichen Paketquellen sollten und behalten Sie Ihr nur öffentliche paketrepository nur api.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="99451-119">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="99451-120">Wir haben viel Zeit in die Erstellung unserer API v3 abgelegt und weiterhin die standard-v2-API für die alten Clients zum Zugriff auf die öffentlichen Repositorys Suchvorgänge zu pflegen.</span><span class="sxs-lookup"><span data-stu-id="99451-120">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="99451-121">Aktualisierte Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="99451-121">Updated UI</span></span>

<span data-ttu-id="99451-122">Wir haben die Benutzeroberfläche in dieser Version ein Kombinationsfeld-Steuerelement einfügen können Sie zum Auswählen einer Aktion für das Paket ausführen und die Schaltfläche "Vorschau" eines Spiegels noch ein Kontrollkästchen im Bereich des Bildschirms verbessert.</span><span class="sxs-lookup"><span data-stu-id="99451-122">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="99451-123">Bereich "Optionen" ist nicht mehr reduzierbare und bietet nun einen Hilfelink klicken, beschreibt die verfügbaren Optionen.</span><span class="sxs-lookup"><span data-stu-id="99451-123">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![Die neue NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="99451-125">Protokollierung</span><span class="sxs-lookup"><span data-stu-id="99451-125">Operation Logging</span></span>

<span data-ttu-id="99451-126">Es entfernt das modale Fenster mit Protokollieren von Informationen, die schnell angezeigt werden würden, und während der Installation oder Deinstallation ausblenden.</span><span class="sxs-lookup"><span data-stu-id="99451-126">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="99451-127">In diesem Fenster hinzugefügt kein Wert aus, wenn tatsächlich finden die Informationen, oder in der Lage, kopieren und Einfügen von ihm werden soll.</span><span class="sxs-lookup"><span data-stu-id="99451-127">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="99451-128">Stattdessen werden wir jetzt alle der Protokollierung in den Paket-Manager-Bereich des Ausgabefensters Ausgabe umleiten.</span><span class="sxs-lookup"><span data-stu-id="99451-128">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="99451-129">Wir glauben, dass dies mehr vertraut und ähnelt einer typischen buildberichtsspeicherort, die Sie untersuchen möchten.</span><span class="sxs-lookup"><span data-stu-id="99451-129">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="99451-130">Konzentrieren Sie sich auf die Leistung</span><span class="sxs-lookup"><span data-stu-id="99451-130">Focus on Performance</span></span>

<span data-ttu-id="99451-131">Wir haben viele Änderungen im Namen Verbessern der Leistung von NuGet-Suchfunktionen und Abrufvorgänge vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="99451-131">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="99451-132">Dies wurde von unseren Kunden unsere höchste relevant, und wir möchten sicher sein, dass wir sie in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="99451-132">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="99451-133">Wir haben unsere Server, erstellt einen neuen CDN optimiert und verbessert die Logik zum Übermitteln von hoffentlich treten bei Ihnen relevanter übereinstimmende Abfrage und schnellere Paket Suchergebnisse.</span><span class="sxs-lookup"><span data-stu-id="99451-133">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="99451-134">Wie wir über diese Phase der Entwicklung von NuGet 3.0 fortfahren, werden wir optimieren und Überwachung den nuget.org-Dienst, um sicherzustellen, dass wir eine verbesserte benutzererfahrung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="99451-134">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="99451-135">Wir keine Einbindung in die Ausfallzeiten, möchten jedoch wird werden hinzufügen und Ressourcen im Dienst ändern.</span><span class="sxs-lookup"><span data-stu-id="99451-135">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="99451-136">Achten Sie auf unserer [twitter-Feed](http://twitter.com/nuget) Details auf, wenn es die Dienstkonfiguration ändern.</span><span class="sxs-lookup"><span data-stu-id="99451-136">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="99451-137">Erstellen von NuGet mit NuGet</span><span class="sxs-lookup"><span data-stu-id="99451-137">Building NuGet with NuGet</span></span>

<span data-ttu-id="99451-138">Wir haben unsere NuGet-Clients in mehreren Komponenten neu entworfen, die selbst wird in NuGet-Pakete erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="99451-138">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="99451-139">Dieser erneuten Verwendung eines eigenen Bibliotheken erzwingt uns um Komponenten zu erstellen, die wiederholt verwendbare sind und ordnungsgemäß verpackt werden können.</span><span class="sxs-lookup"><span data-stu-id="99451-139">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="99451-140">Es wurden doppelte Code eliminiert und haben gelernt, wie Sie unsere Entwicklungsprozesses zur Unterstützung der Notwendigkeit zum Erstellen von Paketen in der gesamten unseren Lösungen für eine bessere Leistung konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="99451-140">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="99451-141">Suchen Sie nach bald einen Blogbeitrag, in denen beschäftigen wir uns wie die Codeprojekte strukturiert sind und zur Funktionsweise von unseren Build-Prozesses.</span><span class="sxs-lookup"><span data-stu-id="99451-141">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="99451-142">Bleiben Sie dran</span><span class="sxs-lookup"><span data-stu-id="99451-142">Stay Tuned</span></span>

<span data-ttu-id="99451-143">Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen für NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="99451-143">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>