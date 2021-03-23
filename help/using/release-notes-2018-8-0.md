---
title: Versionsinformation för 2018.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2018.8.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.8.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2018.8.0.
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---


# Versionsinformation för 2018.8.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0-versionen har stöd för att automatiskt aktivera CI/CD-flödet när Git implementeras och en ny guide för att skapa programprojekt i Git baserat på AEM Project Archetype.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.8.0 är 4 oktober 2018.

## Nyheter {#what-s-new}

* **Programinstallation**  - Ny guide för att skapa ett programprojekt i Git med hjälp av AEM Project Archetype

* **CI/CD Pipeline**  - Följande ändringar läggs till i CI/CD Pipeline. Mer information finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md).

   * Vid Git Changes-utlösaren, som startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen.
   * Kort på startskärmen har nu en djup länk till specifika avsnitt på sidan för att köra pipeline.
   * Aktivitetssidan visar nu den specifika gren som används för varje körning.
   * Aktivitetssidan visar nu varaktigheten i timmar och minuter.
   * Sidan för körning av pipeline visar nu version-/taggnamnet som skapades för körningen.
   * Apache Maven version uppdaterad till 3.5.3.

* **Navigering**  - Följande ändringar har lagts till i  [!UICONTROL Cloud Manager].

   * Resurslänken i den globala navigeringen kommer att navigera till Runbook i Sharepoint.
   * Hjälpmenyn har ordnats om för att innehålla mer [!UICONTROL Cloud Manager]-specifikt innehåll.

## Felkorrigeringar {#bug-fixes}

* Vissa detaljer i dialogrutan Prestandatestning var inte synliga i Firefox.
* Timeout mellan interna system kan ibland leda till att distributionsfel rapporteras.
* Ikonfärgen på aktivitetssidan var inte korrekt för vissa lyckade pipeline-körningar.
* I vissa fall listades samma mått flera gånger i dialogrutan Prestandatestning.
* Om en ny instans lades till efter att CI/CD-pipeline hade startats kommer distributionen inte att utföras på den nyligen skapade instansen.

## Kända fel {#known-issues}

* Förgreningar som har skapats med programprojektguiden får inte innehålla streck.
* Sidlisten för [!UICONTROL Experience Cloud]-meddelanden kan inte läsa in meddelanden konsekvent. Meddelanden visas emellertid i [!UICONTROL Experience Cloud] och, om de är konfigurerade, skickas de fortfarande via e-post.

