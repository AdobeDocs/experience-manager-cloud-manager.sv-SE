---
title: Versionsinformation för 2020.4.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.4.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.4.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.4.0
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# Versionsinformation för 2020.4.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.4.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.4.0 är 9 april 2020.

## Nyheter {#whats-new}

* Ändringar i navigeringens CM-översiktssida som gör att användaren kan redigera eller växla program från CM-översiktssidan.
* Ändringar som gör att användaren kan redigera program från programkortet på CM-startsidan.
* Den nya pipeline-statusen &quot;Pipeline Running&quot; visas mot den miljö som den är associerad med.
* Förbättringar av förståelsen av sidan för att implementera pipeline. Detta inkluderar visning av Pipeline-namn (endast icke-produktionspipeline) och Type, och ett märke som anger om pipelinestatusen pågår/avbryts/misslyckades.
* Processen som används för att generera Git-lösenord har gjorts mer flexibel mot problem i det underliggande tjänstskiktet.

## Felkorrigeringar {#bug-fixes}

* Övervakningsuppgifterna kan ibland visas på ett felaktigt sätt eller inte alls baserat på mindre avvikelser i de tekniska värdena.
* Den Maven-konfiguration som används i byggbehållaren har uppdaterats för att undvika dödlägen när artefaktmetadata hämtas.
* Prestandatestningsprocessen för Assets kunde ibland inte dekryptera AEM-lösenordet, vilket medförde att testningen misslyckades.
* Vissa topologier med standby-instanser kan ha falska negativ vid säkerhetstestning.
* Om scenmiljön innehåller en stoppad instans kan säkerhetstestningssteget ibland misslyckas.
* Experience Cloud-meddelanden togs inte emot konsekvent.

