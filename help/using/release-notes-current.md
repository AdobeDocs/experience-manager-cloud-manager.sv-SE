---
title: Versionsinformation för 2021.3.0
seo-title: Versionsinformation om AEM Cloud Manager för 2021.3.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.3.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2021.3.0
translation-type: tm+mt
source-git-commit: b5233e1932888b515d8dc26a6493cbd26686bc3c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Versionsinformation för 2021.3.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.3.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.3.0 är 11 mars 2021.

## Nyheter {#whats-new}

* Ett nytt kodkvalitetsverktyg har introducerats för att validera kunddispatcherkonfigurationen (Dispatcher Optimization Tool).

* Användarna kan nu se sin molnhanterarroll(er) genom att välja alternativet **Visa molnhanterarroll(er)** efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten **Ansökan om godkännande** har ändrats till **Produktionsgodkännande** för större tydlighet.

* **Versionsetiketten** har ändrats till **Git-tagg** på körningsskärmen för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende - Avbryt omedelbart och godkänn omedelbart.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service-SDK.

## Felkorrigeringar {#bug-fixes}

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.