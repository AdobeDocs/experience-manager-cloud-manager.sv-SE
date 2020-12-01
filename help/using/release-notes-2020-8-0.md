---
title: Versionsinformation för 2020.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.8.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.8.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.8.0
translation-type: tm+mt
source-git-commit: c1d07c95088a279376ef495001a5165c7e459642
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 1%

---

# Versionsinformation för 2020.8.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.8.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

## Nyheter {#whats-new}

Stöd finns nu för autentiseringsbundna privata Maven-databaser.

## Felkorrigeringar {#bug-fixes}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* När du distribuerar till topologier med en enda publicering, en enda dispatcher och en kall skapare i vänteläge togs dispatchern felaktigt bort från belastningsutjämnaren.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Pipeline-körningar får ibland *fastna* på grund av interna kommunikationsproblem.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Det fanns ett färgmatchningsfel på sidan **Översikt**.

* Testning av webbplatsprestanda har nu stöd för valfri användning av autentisering.

* Dispatcher-cacheminnen för författarinstanser rensas automatiskt när dispatcherkonfigurationer distribueras via Cloud Manager.

