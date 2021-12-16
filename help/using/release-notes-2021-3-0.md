---
title: Versionsinformation för 2021.3.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.3.0
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Versionsinformation för 2021.3.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] Version 2021.3.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] Version 2021.3.0 är 11 mars 2021.
Nästa version är planerad till den 8 april 2021.

## Nyheter {#whats-new}

* Ett nytt kodkvalitetsverktyg [Dispatcher Optimization Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) har introducerats för att validera kunddispatcherkonfigurationen.

* Användarna kan nu se sin molnhanterarroll(er) genom att välja **Visa molnhanterarroll(er)** efter navigering till ikonen Användarprofil (överst till höger) i det enhetliga skalet.

* Etiketten **Ansökan om godkännande** har fått en ny etikett till **Produktionsgodkännande** för större tydlighet.

* The **Version** etiketten har ändrats till **Git-tagg** i körningsfönstret för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende - **Avbryt omedelbart** och **Godkänn omedelbart**. Se [Konfigurera pipeline-inställningarna](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) för mer information.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service SDK.

## Felkorrigeringar {#bug-fixes}

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.
