---
title: Versionsinformation för 2021.3.0
seo-title: Versionsinformation om AEM Cloud Manager för 2021.3.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.3.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2021.3.0
translation-type: tm+mt
source-git-commit: fde8cbd22ff36e0d30409f68e8a0523c814ccf90
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versionsinformation för 2021.3.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.3.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.3.0 är 11 mars 2021.
Nästa version är planerad till den 8 april 2021.

## Nyheter {#whats-new}

* Användare med nödvändig behörighet kan nu redigera program och göra följande på ett självbetjäningssätt:

   * Lägg till Sites-lösning i ett befintligt program med Assets (eller vice versa).
   * Ta bort platser (eller resurser) från ett befintligt program med både platser och resurser.
   * Du kan lägga till (tillbaka) en lösning till det befintliga programmet eller som ett nytt program.

* Ett nytt kodkvalitetsverktyg [Dispatcher Optimization Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) har introducerats för att validera kunddispatcherkonfigurationen.

* Användarna kan nu se sin molnhanterarroll(er) genom att välja alternativet **Visa molnhanterarroll(er)** efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten **Ansökan om godkännande** har ändrats till **Produktionsgodkännande** för större tydlighet.

* **Versionsetiketten** har ändrats till **Git-tagg** på körningsskärmen för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende - **Avbryt omedelbart** och **Godkänn omedelbart**. Mer information finns i [Konfigurera förloppsinställningarna](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager).

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service-SDK.

## Felkorrigeringar {#bug-fixes}

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.