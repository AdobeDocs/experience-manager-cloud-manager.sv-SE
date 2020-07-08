---
title: Versionsinformation för 2018.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2018.8.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.8.0.
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2018.8.0.
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
translation-type: tm+mt
source-git-commit: cdf2c82192c2e9c375316ae6e28646594ba2a462
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Versionsinformation för 2018.8.0 {#release-notes-for}

I version [!UICONTROL Cloud Manager] 2018.8.0 finns stöd för att automatiskt aktivera CI/CD-flödet när Git implementeras och en ny guide för att skapa programprojekt i Git baserat på AEM Project Archetype.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.8.0 är 4 oktober 2018.

## What&#39;s New {#what-s-new}

* **Programinstallation** - Ny guide för att skapa ett programprojekt i Git med hjälp av AEM Project Archetype Mer information finns i [Skapa ett AEM Application Project](/help/using/create-an-application-project.md) .

* **CI/CD Pipeline** - Följande ändringar läggs till i CI/CD Pipeline. Mer information finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md) .

   * Vid Git Changes-utlösaren, som startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen.
   * Kort på startskärmen har nu en djup länk till specifika avsnitt på sidan för att köra pipeline.
   * Aktivitetssidan visar nu den specifika gren som används för varje körning.
   * Aktivitetssidan visar nu varaktigheten i timmar och minuter.
   * Sidan för körning av pipeline visar nu version-/taggnamnet som skapades för körningen.
   * Apache Maven version uppdaterad till 3.5.3.

* **Navigering** - Följande ändringar har lagts till i [!UICONTROL Cloud Manager].

   * Resurslänken i den globala navigeringen kommer att navigera till Runbook i Sharepoint.
   * Hjälpmenyn har ordnats om så att den innehåller mer [!UICONTROL Cloud Manager]specifikt innehåll.

## Bug Fixes {#bug-fixes}

* Vissa detaljer i dialogrutan Prestandatestning var inte synliga i Firefox.
* Timeout mellan interna system kan ibland leda till att distributionsfel rapporteras.
* Ikonfärgen på aktivitetssidan var inte korrekt för vissa lyckade pipeline-körningar.
* I vissa fall listades samma mått flera gånger i dialogrutan Prestandatestning.
* Om en ny instans lades till efter att CI/CD-pipeline hade startats kommer distributionen inte att utföras på den nyligen skapade instansen.

## Kända fel {#known-issues}

* Förgreningar som har skapats med programprojektguiden får inte innehålla streck.
* Det går inte att läsa in meddelanden konsekvent med hjälp av sidofältet för meddelanden. [!UICONTROL Experience Cloud] Meddelanden visas dock i [!UICONTROL Experience Cloud] och, om de är konfigurerade, skickas de fortfarande via e-post.

