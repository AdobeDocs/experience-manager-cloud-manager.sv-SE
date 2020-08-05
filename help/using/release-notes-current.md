---
title: Versionsinformation för 2020.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.8.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.8.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.8.0
translation-type: tm+mt
source-git-commit: 3be958aa21d5423ddf371c286825d01afd554c4b
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Versionsinformation för 2020.8.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.8.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

## What&#39;s New {#whats-new}

* Testning av webbplatsprestanda har nu stöd för valfri användning av autentisering.

   Mer information finns i.

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

## Bug Fixes {#bug-fixes}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* När du distribuerar till topologier med en enda publicering, en enda dispatcher och en kall skapare i vänteläge togs dispatchern felaktigt bort från belastningsutjämnaren.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Körningar av rörledningar *fastnar* ibland på grund av interna kommunikationsproblem.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Översiktssidan innehöll en färgmatchning.

## Kända fel {#known-issues}

* När en AMS-miljö innehåller en standby-instans anger det loggade meddelandet att instansen är nere i stället för i standby-läge.

* På grund av en förändring i hur kodens täckning beräknas är den _lägsta_ versionen av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.
