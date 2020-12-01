---
title: Versionsinformation för 2019.12.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.12.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.12.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.12.0.
translation-type: tm+mt
source-git-commit: 0fa1fedccb013e82c8df5838a612ce26a1efb7e8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Versionsinformation för 2019.12.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] Release 2019.12.0 och lägger till uppdateringar i pipeline-körning och förbättringar av kodkvalitetsinläsningar.
Mer information finns i avsnitten nedan.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.12.0 är 12 december 2019.

## Nyheter {#whats-new}

* Steg i pipeline-körningen visar nu tidsstämpeln för slutförande för varje steg.
* Kodkvalitetsgenomsökningar för projekt som inte innehåller Java-kod rapporterar nu en kodsatser på 100 %.
* Hälsokontrollen för CQ Dispatcher Configuration har tagits bort.

## Felkorrigeringar {#bug-fixes}

* Datum visades inte korrekt i vissa webbläsare.
* I sällsynta fall flyttades produktionsflödet till godkännandesteget medan prestandatestningen fortfarande var igång.
* I vissa lägen justerades knapparna i överdelen av översiktssidan inte korrekt.
* Under vissa omständigheter såg obehöriga användare en knapp för att starta pipelinen, även om själva knappen inte var klickbar.
* Åtgärdsknapparna för icke-produktionsledningar visas ibland på fel plats.
* Paket med nodtypen granite:Ranking kunde inte genomsökas efter vissa kvalitetsregelöverträdelser.
* Vissa fel i kodkvalitetsprocessen räknas felaktigt som fel.
* Det gick inte att läsa in övervakningsdata för vissa topologier.
