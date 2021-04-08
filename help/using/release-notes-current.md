---
title: Versionsinformation för 2021.4.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.4.0
feature: Versionsinformation
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
translation-type: tm+mt
source-git-commit: 0c33fd9f1af4c98564c9fd14a468fc3bf27744ee
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 1%

---

# Versionsinformation för 2021.4.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.4.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] Version 2021.4.0 är 8 april 2021.
Nästa version är planerad till 6 maj 2021.

## Nyheter {#whats-new}

* Timeout för begäran för virtuella användare för prestandatestning har ökats från 20 sekunder till 60 sekunder.

* Knappen Hantera Git visas på pipelines-kortet även när inga pipelines har konfigurerats.

* Under distributionssteget på körningssidan för pipeline kommer användaren att kunna se de slutförda och framtida distributionsstegen utöver det aktuella steget i användargränssnittet för tillståndet *Pågår*.

* Den version av AEM projekttyp som används av Cloud Manager har uppdaterats till version 27.

* Felmeddelandet när en pipeline startades när en miljö togs bort har klargjorts.

* OSGi-paket som tillhandahålls av Eclipse-projekt är nu uteslutna från regeln.

## Felkorrigeringar {#bug-fixes}

* Sällsynta, övergående fel som kan uppstå vid Assets Test-steget i produktionsflödet.

* Ett avslutande snedstreck i produktionsflödet Load Test orsakade ett 404-fel.

* `Runmode`-kontrollen genererade falskt positiva värden på noder som inte finns i mappen.