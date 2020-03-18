---
title: Versionsinformation för 2019.2.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.2.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.2.0.
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2019.2.0.
translation-type: tm+mt
source-git-commit: 98395c4413b1b6bfbb3a565388ffa32dc3880dff

---


# Versionsinformation för 2019.2.0 {#release-notes-for}

I version [!UICONTROL Cloud Manager] 2019.2.0 finns en ny funktion för systemövervakning. På så sätt kan kunderna se hur deras Adobe Managed Services-miljöer är på systemnivå.


## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.2.0 är 21 februari 2019.

## Nyheter {#whats-new}

* Ny systemövervakningsfunktion. Mer information finns i [Övervaka dina miljöer](monitor-your-environments.md) .
* Dispatchmodulen i guidegenererade projekt innehåller nu en README-fil.
* Sorteringsordningen för problem med kodsökning har förbättrats så att den matchar problemprioriteten.
* Sceninstanser återställs nu alltid till belastningsutjämnaren även vid ett distributionsfel.
* Det finns en ny API-utvecklarroll på Admin Console där specifika användare kan få behörighet att skapa integreringar i Adobe I/O-konsolen. Mer information finns i [Hantera utvecklare](https://www.adobe.com/go/aac_api_prod_learn) .
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

   Om du vill formulera den här URL:en följer du mönstret (`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`), till exempel om URL:en för Experience Cloud är (`https://weretailprod.experiencecloud.adobe.com`) är URL:en för SLA-rapporterna (`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`).

   Detta förväntas bli löst i nästa version med tillgång till SLA-rapporter [!UICONTROL Cloud Manager].
