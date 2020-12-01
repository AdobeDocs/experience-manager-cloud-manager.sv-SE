---
title: Versionsinformation för 2020.4.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.4.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.4.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.4.0
translation-type: tm+mt
source-git-commit: 278858465592482449080fedc3c0165805db223d
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Versionsinformation för 2020.4.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.4.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.4.0 är 9 april 2020.

## Nyheter {#whats-new}

* Ändringar i navigeringssidan för Cloud Manager - översikt, så att användare kan redigera eller byta program.
* Ändringar som gör att användaren kan redigera program från programkortet på Cloud Managers startsida.
* Ny pipeline-status **Pipeline som körs** visas mot den miljö som den är associerad med.
* Förbättringar av förståelsen av sidan för att implementera pipeline. Detta inkluderar visning av Pipeline-namn (endast icke-produktionspipeline) och Type, och ett märke som anger om pipelinestatusen pågår/avbryts/misslyckades.
* Processen som används för att generera Git-lösenord har gjorts mer flexibel mot problem i det underliggande tjänstskiktet.

## Felkorrigeringar {#bug-fixes}

* Övervakningsuppgifterna kan ibland visas på ett felaktigt sätt eller inte alls baserat på mindre avvikelser i de tekniska värdena.
* Den Maven-konfiguration som används i byggbehållaren har uppdaterats för att undvika dödlägen när artefaktmetadata hämtas.
* Prestandatestningsprocessen för Assets kunde ibland inte dekryptera AEM lösenord, vilket medförde att testningen misslyckades.
* Vissa topologier med standby-instanser kan ha falska negativ vid säkerhetstestning.
* Om scenmiljön innehåller en stoppad instans kan säkerhetstestningssteget ibland misslyckas.
* Meddelanden från Experience Cloud mottogs inte konsekvent.

