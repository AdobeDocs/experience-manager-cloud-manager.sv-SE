---
title: Versionsinformation för 2018.6.0
seo-title: Versionsinformation om AEM Cloud Manager för 2018.6.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.6.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2018.6.0.
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Versionsinformation för 2018.6.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2018.6.0 och den innehåller stöd för inaktivering av dispatcher under distributioner, ytterligare meddelanden och förbättringar av användbarheten.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.6.0 är 9 augusti 2018.

## Nyheter {#what-s-new}

* **CI/CD Pipeline**  - Konfigurerbar Dispatcher Invalidation och Cache Flushing på både scenen och produktionen under CI/CD Pipeline-körning. Mer information finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md).

* **CI/CD-pipeline**  - Under pipeline-konfigurationen är det nu möjligt att definiera hur pipelinen ska fungera när ett viktigt fel upptäcks i en av kvalitetsportarna. Mer information finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md).

* **CI/CD-pipeline**  - Under pipeline-konfigurationen går det nu att välja om du vill att CSE Oversight ska utföras av din CSE eller någon tillgänglig CSE. Mer information finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md).

* **CI/CD-pipeline** - När CI/CD-pipeline når affärsgodkännandesteget skickas ett meddelande till användare som har behörighet att godkänna distributionen. Mer information finns i [Meddelanden](notifications.md).

* **CI/CD Pipeline**  - När CI/CD-pipeline når schemauppsättningen skickas ett meddelande till användare som är behöriga att ange schemat. Mer information finns i [Meddelanden](notifications.md).

* **Kodkvalitetsanalys**  - Nya regler för att identifiera felaktigt konfigurerade utgående HTTP/HTTPS-begäranden. Mer information finns i [Anpassade regler för kodkvalitet](custom-code-quality-rules.md).

## Felkorrigeringar {#bug-fixes}

* I vissa fall distribuerades prestandatestet inte fullständigt över flera dispatcher och publiceringsinstanser.
* Sidhuvudsnavigeringen försvann i smala webbläsarfönster.
* Vissa pipeline-inställningar inaktiverades inte medan pipeline kördes.
* Länkar till AEM och övervakning från programlistskärmen ersatte både den aktuella webbläsarfliken och öppnade en ny flik.
* Under vissa omständigheter kan en lång godkännandeperiod leda till en misslyckad distribution.
