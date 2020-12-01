---
title: Versionsinformation för 2019.7.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.7.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.7.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.7.0.
translation-type: tm+mt
source-git-commit: 365cd6dfe65059c0c529f774bbcda946d47b0db5
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# Versionsinformation för 2019.7.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.7.0-utgåvan lägger till uppdateringar i Experience Cloud-meddelanden och förbättringar som felkorrigeringar. Mer information finns i avsnitten nedan.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.7.0 är 18 juli 2019.

## Nyheter {#whats-new}

Nu skickas ett Experience Cloud-meddelande i början av en produktionsdistribution.

## Felkorrigeringar {#bug-fixes}

* I vissa fall utför Cloud Manager statiska kodanalyser på Python- och PHP-filer.
* Paket som innehöll FileVault InstallHooks kördes inte konsekvent genom kodkvalitetssteget.
* I vissa kombinationer sorterades inte problem med kodkvalitet konsekvent.
* Det fanns några visuella problem på sidan för pipeline-körning.
* Prestandatestningen kan misslyckas slumpmässigt ibland på grund av resursbegränsningar från den underliggande molninfrastrukturen.
* Vissa kundbyggen misslyckas på grund av nätverksproblem.