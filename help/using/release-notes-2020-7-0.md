---
title: Versionsinformation för 2020.7.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.7.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.7.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.7.0
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%

---

# Versionsinformation för 2020.7.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.7.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

## Nyheter {#whats-new}

* Det går nu mer konsekvent att frigöra och koppla dispatcherinstanser från belastningsutjämnarna under produktionsdistributioner.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.

* Molnhanterarens pipelines har nu stöd för kundspecifika variabler och hemligheter.
Mer information finns i [Pipeline Variables](/help/using/build-environment-details.md#pipeline-variables).

## Felkorrigeringar {#bug-fixes}

* Alternativen **Avbryt** och **Spara** på sidan Redigera icke-produktionsförlopp var inte alltid synliga.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

## Kända fel {#known-issues}

* När en AMS-miljö innehåller en standby-instans anger det loggade meddelandet att instansen är nere i stället för i standby-läge.

* På grund av en förändring i hur kodens täckning beräknas är versionen _minimum_ av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.
