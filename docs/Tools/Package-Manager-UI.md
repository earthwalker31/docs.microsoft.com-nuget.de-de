---
title: "Benutzeroberflächenreferenz für NuGet-Paket-Manager | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "Anweisungen für die Verwendung der NuGet-Paket-Manager-UI in Visual Studio für die Arbeit mit NuGet-Pakete."
keywords: "NuGet UI, NuGet-Paket-Manager NuGet in Visual Studio, Verwalten von NuGet-Pakete, die NuGet-Benutzeroberfläche, die Paket-Manager in Visual Studio-Benutzeroberfläche"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 35bb856ccff43c77af7eac67da4614d83dcdc533
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-package-manager-ui"></a>NuGet-Paket-Manager-Benutzeroberfläche

Die NuGet-Paket-Manager-UI in Visual Studio unter Windows können Sie problemlos installieren, deinstallieren und Aktualisieren von NuGet-Pakete in Projekten und Projektmappen. Die Erfahrung in Visual Studio für Mac, finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough). Die Paket-Manager-UI kann nicht mit Visual Studio-Code enthalten ist.

In diesem Thema:

- [Suchen und installieren ein Paket (Registerkarte "Durchsuchen")](#finding-and-installing-a-package)
- [Deinstallieren ein Paket (Registerkarte "installiert")](#uninstalling-a-package)
- [Aktualisieren eines Pakets (Registerkarten installiert und Updates)](#updating-a-package) (enthält die ["Implizit auf die verwiesen wird durch ein SDK" oder "AutoReferenced" Nachricht](#implicit_reference))
- [Verwalten von Paketen für die Projektmappe](#managing-packages-for-the-solution) (Arbeiten mit mehreren Projekten gleichzeitig).
- [Paketquellen](#package-sources)
- [Paket-Manager-Optionen steuern](#package-manager-options-control)

> [!Note]
> Wenn Sie das NuGet-Paket-Manager in Visual Studio 2015 nicht vorhanden sind, überprüfen Sie **Tools > Erweiterungen und Updates...**  , suchen Sie nach der *NuGet Package Manager* Erweiterung. Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, laden Sie die Erweiterung direkt aus [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> In Visual Studio 2017 werden NuGet und NuGet-Paket-Manager automatisch mit installiert. NET-bezogenen Arbeitslasten. Dazu einzeln Installieren der **Einzelkomponenten > Code Extras > NuGet-Paket-Manager** -Option in Visual Studio 2017 Installationsprogramm.

## <a name="finding-and-installing-a-package"></a>Suchen und Installieren eines Pakets

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder ein Projekt, und wählen **NuGet-Pakete verwalten...** .

    ![Menüoption für NuGet-Pakete verwalten](media/ManagePackagesUICommand.png)

1. Die **Durchsuchen** Registerkarte zeigt die Pakete nach verwendungshäufigkeit von der aktuell ausgewählten Quelle (finden Sie unter [Paket Quellen](#package-sources)). Suchen Sie nach einem bestimmten Paket mithilfe des Suchfelds auf der linken oberen Ecke. Wählen Sie ein Paket aus der Liste, um dessen Informationen anzuzeigen, wodurch die können auch die **installieren** zusammen mit einem Versionsauswahl Dropdown-Schaltfläche.

    ![Verwalten von NuGet-Pakete Dialogfeld Durchsuchen Registerkarte](media/Search.png)

1. Wählen Sie die gewünschte Version aus der Dropdownliste aus, und wählen Sie **installieren**. Visual Studio installiert das Paket und seine Abhängigkeiten im Projekt. Möglicherweise werden Sie aufgefordert, Lizenzbedingungen zu akzeptieren. Nach Abschluss der Installation zusätzliche Pakete angezeigt werden, auf die **installiert** Registerkarte. Pakete werden ebenfalls aufgeführt, der **Verweise** Knoten des Projektmappen-Explorer, der angibt, dass Sie im Projekt die darauf verweisen können `using` Anweisungen.

    ![Verweise im Projektmappen-Explorer](media/References.png)

> [!Tip]
    > Vorabversionen in die Suche einbeziehen und Vorabversionen Dropdown-in der Version verfügbar machen möchten, wählen Sie die **Vorabversion einschließen** Option.

## <a name="uninstalling-a-package"></a>Deinstallieren eines Pakets

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Select **NuGet-Pakete verwalten...** .
1. Wählen Sie die **installiert** Registerkarte.
1. Wählen Sie das Paket deinstallieren (mithilfe der Suche zum Filtern der Liste aus, falls erforderlich), und wählen **Deinstallieren**.

    ![Deinstallieren eines Pakets](media/UninstallPackage.png)

1. Beachten Sie, dass die **Include Vorabversion** und **Paketquelle** Steuerelemente haben keine Auswirkungen, wenn Sie Pakete zu deinstallieren.

## <a name="updating-a-package"></a>Aktualisieren eines Pakets

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Select **NuGet-Pakete verwalten...** . (Websiteprojekte, mit der Maustaste die **"bin"** Ordner.)
1. Wählen Sie die **Updates** Registerkarte ", um Pakete anzuzeigen, die aus der ausgewählten Paketquellen verfügbaren Updates verfügen. Wählen Sie **Vorabversion einschließen** Vorabversionen von Paketen in der Updateliste eingeschlossen werden sollen.
1. Wählen Sie das Paket zu aktualisieren, wählen die gewünschte Version aus der Dropdownliste auf der rechten Seite, und wählen Sie **aktualisieren**.

    ![Aktualisieren eines Pakets](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Für einige Pakete die **Update** Schaltfläche ist deaktiviert, und eine Meldung angezeigt, die besagt, dass "implizit ein SDK verweist" (oder "AutoReferenced"). Die Meldung gibt an, dass das Paket, z. B. Microsoft.NETCore.App oder Microsoft.NETStandard.Library, Teil eines größeren Framework oder SDK ist und nicht unabhängig voneinander aktualisiert werden sollten. (Solche Pakete sind intern mit markierten `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Um das Paket zu aktualisieren, aktualisieren Sie das SDK zu dem er gehört.

    ![Beispielpaket als implizit gekennzeichnet sein, Verweise oder AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Um mehrere Pakete auf die neuesten Version zu aktualisieren, wählen sie in der Liste aus und wählen Sie die **aktualisieren** Schaltfläche über der Liste.
1. Sie können auch ein einzelnes Paket aus Aktualisieren der **installiert** Registerkarte. In diesem Fall enthalten die Details für das Paket einen Selektor Version (unterliegen die **Include Vorabversion** Option) und ein **Update** Schaltfläche.

## <a name="managing-packages-for-the-solution"></a>Verwalten von Paketen für die Projektmappe

Verwalten von Paketen für eine Projektmappe ist eine bequeme Möglichkeit gleichzeitig mit mehreren Projekten arbeiten.

1. Wählen Sie die **Extras > NuGet-Paket-Manager > NuGet-Pakete für Projektmappe verwalten...**  Menü-Befehls oder mit der rechten Maustaste in der Projektmappe, und wählen Sie **NuGet-Pakete verwalten...** :

    ![Verwalten von NuGet-Pakete für die Projektmappe](media/ManagePackagesSolutionUICommand.png)

1. Wenn Sie Pakete für die Projektmappe zu verwalten, kann die Benutzeroberfläche Sie die Projekte auswählen, die von den Vorgängen betroffen sind:

    ![Projekt-Selektor beim Verwalten von Paketen für die Projektmappe](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Registerkarte "Konsolidieren

Entwickler halten es in der Regel nicht üblich, verschiedene Versionen desselben NuGet-Pakets über verschiedene Projekte in der gleichen Projektmappe verwenden. Wenn Sie zum Verwalten von Paketen für eine Projektmappe auswählen, die Paket-Manager-UI bietet eine **konsolidieren** Registerkarte auf dem können Sie problemlos nachvollziehen, in denen Pakete mit unterschiedlichen Versionsnummern von verschiedenen Projekten in der Projektmappe verwendet werden:

![Paket-Manager-Benutzeroberfläche konsolidieren Registerkarte](media/ConsolidateTab.png)

In diesem Beispiel wird das Projekt "ClassLibrary1" EntityFramework 6.2.0 fest, verwendet, wohingegen ConsoleApp1 EntityFramework 6.1.0 verwendet wird. Führen Sie folgende Schritte aus, um Paketversionen zu konsolidieren:

- Wählen Sie die Projekte in der Projektliste aktualisieren.
- Wählen Sie die Version, verwenden Sie diese Projekte in der **Version** Kontrolle, z. B. EntityFramework 6.2.0 fest.
- Wählen Sie die **installieren** Schaltfläche.

Die Paket-Manager installiert die Version des ausgewählten Pakets in allen ausgewählten Projekte nach dem das Paket nicht mehr angezeigt wird auf die **konsolidieren** Registerkarte.

## <a name="package-sources"></a>Paketquellen

Wählen Sie eine aus dem Quell-Selektor Schritte aus, um die Quelle zu ändern, aus dem Visual Studio ruft Pakete ab:

![Paket-Quelle-Selektor in der Paket-Manager-Benutzeroberfläche](media/PackageSourceDropDown.png)

So verwalten Sie die Paketquellen überein:

1. Wählen Sie die **Einstellungen** Symbol in der Paket-Manager-UI unten beschriebenen, oder verwenden Sie die **Tools > Optionen** Befehl und einen Bildlauf zu **NuGet Package Manager**:

    ![Symbol "Einstellungen" Paket-Manager-Benutzeroberfläche](media/PackageSourceSettings.png)

1. Wählen Sie die **Paketquellen** Knoten:

    ![Quellen Paketoptionen](media/options.png)

1. Wählen Sie zum Hinzufügen einer Quelle  **+** , bearbeiten Sie den Namen, geben Sie die URL oder Pfad in der **Quelle** Steuerelement, und wählen Sie **Update**. Die Quelle wird jetzt in der Dropdownliste angezeigt.
1. Um eine Paketquelle zu ändern, wählen Sie ihn, nehmen Sie Änderungen vor, in der **Namen** und **Quelle** ein, und wählen Sie **Update**.
1. Um eine Paketquelle zu deaktivieren, deaktivieren Sie das Kontrollkästchen links neben dem Namen in der Liste aus.
1. Um eine Paketquelle zu entfernen, wählen Sie ihn, und wählen Sie dann die **X** Schaltfläche.
1. Verwenden Sie die nach-oben und nach-unten Sie-Pfeile, um die Prioritätsreihenfolge der Paketquellen überein ändern. Visual Studio sucht diese Quellen in der Reihenfolge ihrer Priorität beim Wiederherstellen von Paketen für ein Projekt. Weitere Informationen finden Sie unter [paketwiederherstellung](../consume-packages/package-restore.md).

> [!Tip]
> Wenn Sie eine Paketquelle erneut angezeigt wird, nach dem Löschen, kann es in einer Computerebene oder Benutzerebene aufgeführt `NuGet.Config` Dateien. Finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md) für den Speicherort dieser Dateien, entfernen Sie Sie dann die Quelle, indem Sie die Dateien manuell zu bearbeiten oder die [Nuget Datenquellen Befehl](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Paket-Manager-Optionen steuern

Wenn ein Paket ausgewählt ist, zeigt der Paket-Manager-UI ein kleines erweiterbare **Optionen** Steuerelement unterhalb der Version-Selektor (hier gezeigten sowohl reduziert und erweitert). Beachten Sie, die für einige Projekt nur Typen der **Vorschaufenster anzeigen** angegeben wird.

![Optionen des Paket-manager](media/PackageManagerUIOptions.png)

Den folgenden Abschnitten werden diese Optionen.

### <a name="show-preview-window"></a>Vorschaufenster anzeigen

Bei Auswahl dieser Option zeigt ein modales Fenster die die Abhängigkeiten eines ausgewählten Pakets vor der Installation des Pakets:

![Beispiel-Vorschaudialogfeld](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installations- und Aktualisierungsoptionen

(Nicht verfügbar für alle Projekttypen.)

**Das abhängigkeitsverhalten** konfiguriert wie NuGet entscheidet sich, welche Versionen der abhängigen Pakete zu installieren:

- *Ignorieren Sie Abhängigkeiten* überspringt, installieren alle Abhängigkeiten, die zu installierende Paket in der Regel unterbricht.
- *Niedrigste* [Standard] installiert die Abhängigkeit mit der minimalen Versionsnummer, die die Anforderungen des ausgewählten Pakets primären erfüllt.
- *Höchste Patch* die Version mit der gleichen Haupt-und Nebenversionsnummern Zahlen, aber die höchste Anzahl der Patch installiert. Z. B. wenn Version 1.2.2 angegeben wird die höchste Version, die mit 1.2 beginnt installiert werden
- *Höchste Nebenversion* die Version mit der gleichen Hauptversionsnummer nur den höchsten Nebenversionsnummer und die Anzahl der Patch installiert. Wenn Version 1.2.2 angegeben ist, wird die höchste Version, die mit 1 beginnt installiert werden
- *Höchste* installiert die höchste verfügbare Version des Pakets.

**Datei Konflikt Aktion** gibt an, wie NuGet Pakete behandeln soll, die bereits im Projekt oder lokalen Computer vorhanden sind:

- *Prompt* weist NuGet zu Fragen, ob beibehalten oder überschreiben vorhandene Pakete.
- *Ignorieren Sie alle* weist NuGet zum Überschreiben aller vorhandenen Pakete überspringen.
- *Überschreiben Sie alle* weist NuGet, um vorhandene Pakete zu überschreiben.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Deinstallationsoptionen

(Nicht verfügbar für alle Projekttypen.)

**Entfernen Sie Abhängigkeiten**: Bei Auswahl dieser Option entfernt alle abhängigen Pakete auf, wenn diese nicht an anderer Stelle im Projekt verwiesen wird.

**Deinstallation erzwingen, auch wenn Abhängigkeiten vorhanden sind, darauf**: Bei Auswahl dieser Option wird ein Paket deinstalliert, selbst wenn darauf noch im Projekt verwiesen wird. Dies wird normalerweise verwendet, in Kombination mit **Abhängigkeiten entfernen** So entfernen Sie ein Paket und alle von Ihnen gewünschten Abhängigkeiten, die es installiert. Mit dieser Option kann jedoch zu fehlerhaften Verweise im Projekt führen. In solchen Fällen müssen Sie möglicherweise auf [installieren Sie die anderen Pakete](../consume-packages/reinstalling-and-updating-packages.md).