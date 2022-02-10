---
title: Versionsinformation för 2018.6.0
seo-title: AEM Cloud Manager Release Notes for 2018.6.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.6.0.
seo-description: Follow this page to get information for AEM Cloud Manager Release 2018.6.0.
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
feature: Release Information
exl-id: 456f7892-c64c-4b3f-b845-15682d034aaa
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Versionsinformation för 2018.6.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] Version 2018.6.0 och ger stöd för invalidering av dispatcher vid distributioner, ytterligare meddelanden och förbättringar av användbarheten.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] Version 2018.6.0 är 9 augusti 2018.

## Nyheter {#what-s-new}

* **CI/CD-pipeline** - Konfigurerbar invalidering av Dispatcher och Cache-tömning på både scenen och produktionen under CI/CD Pipeline-körning. Se dokumentet [Konfigurera produktionsförlopp](configuring-production-pipelines.md) om du vill veta mer.

* **CI/CD-pipeline** - Under pipeline-konfigurationen är det nu möjligt att definiera hur pipelinen ska bete sig när ett viktigt fel upptäcks i en av kvalitetsportarna. Se dokumentet [Konfigurera produktionsförlopp](configuring-production-pipelines.md) om du vill veta mer.

* **CI/CD-pipeline** - Under pipeline-konfigurationen är det nu möjligt att välja om du vill att CSE Oversight ska utföras av din CSE eller någon tillgänglig CSE. Se dokumentet [Konfigurera produktionsförlopp](configuring-production-pipelines.md) om du vill veta mer.

* **CI/CD-pipeline** - När CI/CD-pipeline når affärsgodkännandesteget skickas ett meddelande till användare som har behörighet att godkänna distributionen. Se [Meddelanden](notifications.md) om du vill veta mer.

* **CI/CD-pipeline** - När CI/CD-pipeline når det angivna schemat skickas ett meddelande till användare som är behöriga att ange schemat. Se [Meddelanden](notifications.md) om du vill veta mer.

* **Kodkvalitetsanalys** - Nya regler för att identifiera felaktigt konfigurerade utgående HTTP/HTTPS-begäranden. Se [Anpassade regler för kodkvalitet](custom-code-quality-rules.md) om du vill veta mer.

## Felkorrigeringar {#bug-fixes}

* I vissa fall distribuerades prestandatestet inte fullständigt över flera dispatcher och publiceringsinstanser.
* Sidhuvudsnavigeringen försvann i smala webbläsarfönster.
* Vissa pipeline-inställningar inaktiverades inte medan pipeline kördes.
* Länkar till AEM och övervakning från programlistskärmen ersatte både den aktuella webbläsarfliken och öppnade en ny flik.
* Under vissa omständigheter kan en lång godkännandeperiod leda till en misslyckad distribution.
