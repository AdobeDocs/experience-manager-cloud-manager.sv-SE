---
title: Versionsinformation för 2020.11.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.11.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.11.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.11.0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 1%

---

# Versionsinformation för 2020.11.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.11.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.11.0 är 12 november 2020.

## Nyheter {#whats-new}

* Fliken **Lär dig** i Cloud Manager uppdateras med nya bilder i användargränssnittet.

## Felkorrigeringar {#bug-fixes}

* Vissa kundrelaterade distributionsfel kommer nu att upptäckas explicit i distributionsloggarna.

* Inläsningen av beroenden som gjorts före körningen av bygget krävde hämtning av ett Maven-plugin-program.

* Länken från molnhanterarens sidfot för att välja ett språk navigerar nu till rätt plats.

* Ibland startar inte SonarQube-processen under kodskanningen. Detta identifieras nu automatiskt och ett omstartsförsök görs.

* Under processen för crawlning av webbplatser som används i prestandatestning kommer begäranden som går ut under de tre första djupgenomgången automatiskt att provas igen.