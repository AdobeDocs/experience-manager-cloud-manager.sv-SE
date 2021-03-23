---
title: Versionsinformation för 2018.7.0
seo-title: Versionsinformation för 2018.7.0
description: Läs om Cloud Manager version 2018.7.0
seo-description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.7.0.
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---


# Versionsinformation för 2018.7.0 {#release-notes-for}

I följande avsnitt beskrivs [!UICONTROL Cloud Manager] 2018.7.0-versionen som innehåller *funktionen autoskalning*.

**Automatisk** skalning aktiveras via horisontell skalning av  `Dispatcher/Publish` segment i produktionsmiljön för att ge stöd åt en plötslig ökning av belastning, volym, åtkomst och andra definierade övervakade mätvärden.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.7.0 är 10 september 2018.

## Nyheter {#what-s-new}

* **Provisioning**  -  [!UICONTROL Cloud Manager] kan nu automatiskt skala upp produktionsmiljön i kundprogrammet genom att skala ut horisontellt med segmenten Dispatcher/Publish. Nytt i användargränssnittet är provisioneringsavsnittet i Programinställningar som visas om autoskalning är aktiverat i kundprogrammet. Mer information finns i [Konfigurera ditt program](setting-up-program.md).

* **Miljö**  - Det går nu att se en detaljerad översikt över produktions- och scenmiljöer tillsammans med storlek, lagring, region och status för de noder som är kopplade till varje miljö. Mer information finns i [Hantera dina miljöer](manage-your-environment.md).

* **Kodkvalitetsanalys**  - Ny regel som identifierar felaktig API-användning. Mer information finns i [Anpassade regler för kodkvalitet](custom-code-quality-rules.md).

* **Prestandatestning**  - När du visar prestandatestresultat finns det diagram för CPU-användning, disk-I/O-väntetid, sidfelsfrekvens, användning av diskbandbredd, användning av nätverksbandbredd, svarstid för toppsida och 95:e procentig sidsvarstid. Se avsnittet *Prestandatestning* på [Förstå sidan Testresultat](understand-your-test-results.md).

* **Prestandatestning**  - När du visar prestandatestresultat kan du hämta en lista över sidfel och långsamma begäranden. Se avsnittet *Prestandatestning* på [Förstå sidan Testresultat](understand-your-test-results.md).

## Felkorrigeringar {#bug-fixes}

* Under vissa omständigheter misslyckades den interna systemsynkroniseringen felaktigt, vilket leder till inkonsekventa datavyer.
* I vissa fall valdes inte den manuella utlösaren automatiskt vilket ledde till formulärvalideringsproblem.
* Specifika skript för kundbygge kan orsaka fel under konstruktionssteget baserat på inkompatibiliteter med plugin-program.

## Kända fel {#known-issues}

* Även om kunderna kan välja en utlösare för implementering, kanske inte pipelinen faktiskt börjar baserat på nya implementeringar.
* Sidlisten för [!UICONTROL Experience Cloud]-meddelanden kan inte läsa in meddelanden konsekvent. Meddelanden visas emellertid i [!UICONTROL Experience Cloud] och, om de är konfigurerade, skickas de fortfarande via e-post.

