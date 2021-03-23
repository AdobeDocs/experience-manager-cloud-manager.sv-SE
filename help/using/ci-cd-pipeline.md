---
title: CI/CD-pipeline
seo-title: CI/CD-pipeline
description: Översikt över CI/CD Pipeline, som hanterar distributioner till scener och produktion i Cloud Manager
seo-description: Följ det här avsnittet för att lära dig mer om CI/CD-flödet, som hanterar distributioner till scenen och produktionen i Cloud Manager
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
feature: CI-CD-pipeline
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# CI/CD-pipeline {#ci-cd-pipeline}

## Översikt över pipeline {#pipeline-overview}

[!UICONTROL Cloud Manager] innehåller ett ramverk för kontinuerlig integrering (CI) och Continuous Delivery (CD) som gör att implementeringsteamen snabbt kan testa och leverera ny eller uppdaterad kod. Implementeringsteamen kan till exempel konfigurera, konfigurera och starta en automatiserad CI/CD-pipeline som utnyttjar de bästa metoderna för kodning i Adobe för att utföra en grundlig kodsökning och säkerställa högsta kodkvalitet.

CI/CD-pipeline automatiserar också enhets- och prestandatestningsprocesser för att öka driftsättningseffektiviteten och proaktivt identifiera kritiska problem som är dyra att åtgärda efter driftsättningen. Implementeringsteamen kan få tillgång till en omfattande rapport om kodprestanda för att få insyn i möjliga konsekvenser för nyckeltal och kritiska säkerhetsvalideringar om koden distribueras till produktionen.

## Förloppsprocess {#pipeline-process}

I följande diagram visas vad som händer när en release aktiveras i [!UICONTROL Cloud Manager]. I tabellen förklaras varje steg i arbetsflödet.

![](assets/screen_shot_2018-05-30at82457pm.png)

Följande tabell visar vad som pågår under varje steg i processen:

| Processsteg för pipeline | Vad är det som pågår? |
|---|---|
| 1. Starta en release | En distributionshanterare utlöser en release antingen manuellt, med en Git-implementering eller baserat på ett återkommande schema. |
| 2. Skapa öppningstagg | [!UICONTROL Cloud Manager] skapar en Git-tagg som markerar releasen med ett automatiskt genererat versionsnummer. Till exempel: 2018.531.245527.000001222 |
| 3. Skapad som release med autogenererad version | [!UICONTROL Cloud Manager] skapar programmet med det nytilldelade versionsnumret. |
| 4. Utvärdera kodkvalitet | [!UICONTROL Cloud Manager] söker igenom källkoden och ger en sammanfattning innan koden kan distribueras till scenmiljön |
| 5. Versioniserade artefakter lagrade | Versionsartefakter lagras för senare användning i distributionsstegen. |
| 6. Automatisk distribution av felaktigheter till AMS-AEM | Artefakten distribueras till scenmiljön. |
| 7. Utlös automatiska tester | [!UICONTROL Cloud Manager] kör test av prestanda och säkerhet på artefakten. |
| 8. Driftsättning av produktionstrigger | När de automatiska testerna är klara [!UICONTROL Cloud Manager] startar distributionen till produktionen. |
| 9. [!UICONTROL Cloud Manager] hämtar artefakter att distribuera | [!UICONTROL Cloud Manager] hämtar lagrade versionsartefakter. |
| 10. Skicka artefakter till produktion | Versionsartefakterna distribueras till produktionsmiljön. |

### Konfigurera en CI/CD-pipeline {#how-to-setup-a-ci-cd-pipeline}

Mer information om pipelinekonfigurationen finns i [konfigurera pipeline](configuring-pipeline.md).

## Kvalitetsportar {#quality-gates}

CI/CD-pipeline innehåller kvalitetsportar eller acceptanskriterier som måste uppfyllas innan koden kan flyttas från scenmiljön till distributionsmiljön. Det finns tre portar i pipeline:

* Kodkvalitet
* Prestandatestning
* Säkerhetstestning

För var och en av dessa portar har tre olika problemnivåer identifierats:

* **Kritiska**  problem som identifieras av porten och som orsakar ett omedelbart fel i rörledningen.
* **Viktigt**  - fel som identifieras av porten som gör att pipelinen försätts i pausat läge. Distributionshanteraren, projektledaren eller företagsägaren kan antingen åsidosätta problemen, i vilket fall pipeline fortsätter, eller så kan de acceptera problemen. I så fall upphör pipeline med ett fel.
* **Information**  - frågor som identifieras av portalen och som endast tillhandahålls i informationssyfte och som inte har någon inverkan på ledningen.

Följande är ett exempel på en kodsökning med problem som identifierats för koden:

![](assets/quality-gate-failed.png)

### Konfigurera portar {#how-to-setup-gates}

Mer information om hur du konfigurerar kod, kvalitet och prestanda finns i **[Konfigurera portar](configuring-pipeline.md)**.
