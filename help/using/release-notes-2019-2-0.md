---
title: Versionsinformation för 2019.2.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.2.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.2.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.2.0.
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---


# Versionsinformation för 2019.2.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0-versionen lägger till en ny systemövervakningsfunktion. På så sätt kan kunderna se hur deras Adobe Managed Services-miljöer är på systemnivå.


## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.2.0 är 21 februari 2019.

## Nyheter {#whats-new}

* Ny systemövervakningsfunktion. Mer information finns i [Övervaka dina miljöer](monitor-your-environments.md).
* Dispatchmodulen i guidegenererade projekt innehåller nu en README-fil.
* Sorteringsordningen för problem med kodsökning har förbättrats så att den matchar problemprioriteten.
* Sceninstanser återställs nu alltid till belastningsutjämnaren även vid ett distributionsfel.
* Det finns en ny API-utvecklarroll på Admin Console som gör att specifika användare kan få behörighet att skapa integreringar i Adobe I/O-konsolen. Mer information finns i [Hantera utvecklare](https://www.adobe.com/go/aac_api_prod_learn).
* Versionen av Maven Archetype uppdaterades till version 16.
* Versionen av Maven uppdaterades till version 3.6.0.

## Felkorrigeringar {#bug-fixes}

* Under vissa omständigheter skulle pipelines inte köras när målmiljön var värd för Azure.
* Miljöordningen var inkonsekvent.
* Prestandatestning kan misslyckas när identifierade sidsökvägar innehåller ett kommatecken.
* När en pipeline-körning startades från webbgränssnittet fungerade inte webbläsarens bakåtknapp korrekt.
* Länkarna Läs mer på sidan Översikt öppnade inte en ny flik.
* När du överför en programminiatyrbild kanske den inte var omedelbart synlig.
* I vissa fall misslyckades kodsökningen på grund av en projektspecifik konfiguration.
* Länken Läs mer på icke-produktionskanalerna gick till fel plats.
* När en kvalitetsport åsidosattes visades statusen inkonsekvent.
* Kunder som använder topologier för kallt vänteläge fick felaktiga resultat för säkerhetstester.
* När du skapade ett nytt projekt med guiden gick det inte att skapa en förgrening som innehöll strecktecknet.

## Kända fel {#known-issues}

* När övervakningsdata uppdateras, döljs alla dolda serier.
* Kunder som vill visa sina befintliga SLA-rapporter måste navigera manuellt till nästa version.

   Om URL:en för Experience Cloud är (`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`) följer du mönstret (`https://weretailprod.experiencecloud.adobe.com`) och URL:en för SLA-rapporter är (`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`).

   Detta förväntas bli löst i nästa version med tillgång till SLA-rapporter i [!UICONTROL Cloud Manager].
