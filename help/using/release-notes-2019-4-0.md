---
title: Versionsinformation för 2019.4.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.4.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.4.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.4.0.
translation-type: tm+mt
source-git-commit: b368c46c2a9f40d0c3867db6eb2a333bd71fe22a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Versionsinformation för 2019.4.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0-versionen innehåller inga betydande funktionsändringar. Mer information finns i avsnitten nedan.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.4.0 är 18 april 2019.

## Nyheter {#whats-new}

* Användargränssnittet för Cloud Manager finns nu på engelska, franska, tyska och japanska.
* Distributionsstegen innehåller nu den process som körs, det vill säga när en säkerhetskopiering körs, paket installeras och belastningsutjämnare konfigureras om

## Felkorrigeringar {#bug-fixes}

* Den distributionsmetod som används för Dispatcher-ändringar har förbättrats för att hantera fler användningsfall.
* Vissa instansstorlekstyper visades inte korrekt på sidan Miljöer.
* Kodkvalitetsreglerna för CQBP-84-beroenden genererade falska positiva värden för inbäddade Adobe-bibliotek som WCM Core Components och Asset Share Commons.
* Knappen med information för kodskanningssteget aktiverades när informationen inte var tillgänglig.
* Felmeddelandet när ett ogiltigt värde angavs för KPI för sidvyer per minut hade fel nedre gräns.
* Distributionskategorin på en icke-produktionspipeline kapitaliserades felaktigt.
* Anropet till åtgärdskortet på sidan **Översikt** innehöll felaktig text när Git-databasen inte var korrekt konfigurerad.

## Kända fel {#known-issues}

* SLA-värden kan vara felaktigt avrundade.
