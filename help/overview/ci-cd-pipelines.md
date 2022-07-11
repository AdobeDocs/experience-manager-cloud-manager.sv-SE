---
title: CI/CD-rör
description: Lär dig mer om rörledningar för CI/CD och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# CI/CD-rör {#ci-cd-pipeline}

Lär dig mer om rörledningar för CI/CD och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.

## Översikt {#overview}

[!UICONTROL Cloud Manager] innehåller ett ramverk för kontinuerlig integrering/kontinuerlig leverans (CI/CD) som gör att implementeringsteamen snabbt kan testa och leverera ny eller uppdaterad kod. Implementeringsteamen kan till exempel konfigurera, konfigurera och starta en automatiserad CI/CD-pipeline som utnyttjar de bästa metoderna för kodning i Adobe för att utföra en grundlig kodsökning och säkerställa högsta kodkvalitet.

CI/CD-pipeline automatiserar också enhets- och prestandatestningsprocesser för att öka driftsättningseffektiviteten och proaktivt identifiera kritiska problem som är dyra att åtgärda efter driftsättningen. Implementeringsteamen kan få tillgång till en omfattande rapport om kodprestanda för att få insyn i möjliga konsekvenser för nyckeltal och kritiska säkerhetsvalideringar om koden distribueras till produktionen.

## Pipeline-processen {#pipeline-process}

Bilden visar vad som händer när en release aktiveras i [!UICONTROL Cloud Manager] med hjälp av en pipeline.

![Försäljningsförloppet](/help/assets/screen_shot_2018-05-30at82457pm.png)

| Steg för pipeline | Beskrivning |
|---|---|
| 1. Starta en release | En distributionshanterare utlöser en release antingen manuellt, med en Git-implementering eller baserat på ett återkommande schema. |
| 2. Skapa lanseringstagg | [!UICONTROL Cloud Manager] skapar en Git-tagg som markerar releasen med ett automatiskt genererat versionsnummer, t.ex. `2018.531.245527.0000001222`. |
| 3. Byggd som släppt med autogenererad version | [!UICONTROL Cloud Manager] skapar programmet med det nytilldelade versionsnumret. |
| 4. Utvärdera kodkvaliteten | [!UICONTROL Cloud Manager] söker igenom källkoden och ger en sammanfattning innan koden kan distribueras till staging-miljön. |
| 5. Lagrade versionshanteringsartefakter | Versionsartefakterna lagras för senare användning i distributionsstegen. |
| 6. Automatisk distribution av felaktigheter till AMS-AEM | Frisläppningsartefakten distribueras till testmiljön. |
| 7. Utlösa automatiska tester | [!UICONTROL Cloud Manager] kör prestanda- och säkerhetstester på artefakten. |
| 8. Driftsättning av produktionsutlösare | När de automatiska testerna är klara [!UICONTROL Cloud Manager] börjar distributionen till produktionen. |
| 9. [!UICONTROL Cloud Manager] hämtar artefakter att distribuera | [!UICONTROL Cloud Manager] hämtar lagrade versionsartefakter. |
| 10. Distribuera artefakter till produktion | Artefakterna distribueras till produktionsmiljön. |

### Konfigurera en CI/CD-pipeline {#how-to-setup-a-ci-cd-pipeline}

Mer information om pipelinekonfigurationen finns i dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurerar icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

## Kvalitetsportar {#quality-gates}

CI/CD-pipeline innehåller kvalitetsportar eller acceptanskriterier som måste uppfyllas innan koden kan flyttas från mellanlagringsmiljön till distributionsmiljön. Det finns tre portar i pipeline:

* Kodkvalitet
* Prestandatestning
* Säkerhetstestning

För var och en av dessa portar finns det tre problemnivåer som kan identifieras:

* **Kritisk** - Kritiska problem som identifieras av portalen orsakar ett omedelbart fel i rörledningen.
* **Viktigt** - Viktiga problem som identifieras av porten gör att pipelinen försätts i pausat läge. Distributionshanteraren, projektledaren eller företagsägaren kan antingen åsidosätta problemen, i vilket fall pipeline fortsätter, eller så kan de acceptera problemen. I så fall upphör pipeline med ett fel.
* **Information** - Informationsfrågor som identifieras av portalen tillhandahålls endast i informationssyfte och har ingen inverkan på ledningen.

Detta är ett exempel på en kodsökning där problem har identifierats.

![Exempel på kodsökning](/help/assets/quality-gate-failed.png)

### Konfigurera portar {#how-to-setup-gates}

Se dokumentet [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) om du vill ha mer information om hur du ställer in kod, kvalitet och prestanda.
