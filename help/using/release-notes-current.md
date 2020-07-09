---
title: Versionsinformation för 2020.7.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.7.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.7.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.7.0
translation-type: tm+mt
source-git-commit: a0917f5cecbe552807d9147cd20316e02c2dd1a0
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# Versionsinformation för 2020.7.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.7.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

## What&#39;s New {#whats-new}

* Det går nu mer konsekvent att frigöra och koppla dispatcherinstanser från belastningsutjämnarna under produktionsdistributioner.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.

## Bug Fixes {#bug-fixes}

* Alternativen **Avbryt** och **Spara** på sidan Redigera i icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

## Kända fel {#known-issues}

* När en AMS-miljö innehåller en standby-instans anger det loggade meddelandet att instansen är nere i stället för i standby-läge.
