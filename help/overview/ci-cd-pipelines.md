---
title: CI/CD-rör
description: Lär dig mer om CI/CD-pipelines och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Rörledningar för CI/CD {#ci-cd-pipeline}

Lär dig mer om CI/CD-pipelines och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.

## Ökning {#overview}

[!UICONTROL Cloud Manager] innehåller ett ramverk för kontinuerlig integrering/kontinuerlig leverans (CI/CD) som gör att implementeringsteamen kan testa snabbt och leverera ny eller uppdaterad kod. Implementeringsteamen kan konfigurera, konfigurera och starta en automatiserad CI/CD-pipeline. Detta tillvägagångssätt följer de bästa metoderna för kodning i Adobe för att utföra en omfattande kodskanning och säkerställa högsta kodkvalitet.

CI/CD-pipeline automatiserar också enhets- och prestandatestningsprocesser för att öka driftsättningseffektiviteten och proaktivt identifiera kritiska problem som är dyra att åtgärda efter driftsättningen. Implementeringsteamen kan få tillgång till en omfattande rapport om kodprestanda för att få insyn i möjliga konsekvenser för nyckeltal och kritiska säkerhetsvalideringar om koden distribueras till produktionen.

## Om pipeline-processen {#pipeline-process}

I följande diagram visas vad som händer när en release aktiveras i [!UICONTROL Cloud Manager] med hjälp av en pipeline.

![Pipeline-processen](/help/assets/screen_shot_2018-05-30at82457pm.png)

| Steg för pipeline | Beskrivning |
| --- | --- |
| 1. Starta en release | En distributionshanterare utlöser en release antingen manuellt, med en Git-implementering eller baserat på ett återkommande schema. |
| 2. Skapa en lanseringstagg | [!UICONTROL Cloud Manager] skapar en Git-tagg som markerar releasen med ett automatiskt genererat versionsnummer, till exempel `2018.531.245527.0000001222`. |
| 3. Skapad som release med autogenererad version | [!UICONTROL Cloud Manager] skapar programmet med det nytilldelade versionsnumret. |
| 4. Utvärdera kodkvaliteten | [!UICONTROL Cloud Manager] skannar källkoden och ger en sammanfattning innan koden kan distribueras till mellanlagringsmiljön. |
| 5. Versionskonstanser lagrade | Versionsartefakterna lagras för senare användning i distributionsstegen. |
| 6. Automatisk distribution av artefakter till AMS-AEM | Frisläppningsartefakten distribueras till testmiljön. |
| 7. Utlösa automatiska tester | [!UICONTROL Cloud Manager] kör prestanda- och säkerhetstester på artefakten. |
| 8. Distribution av produktionsutlösare | När de automatiserade testerna har slutförts startar [!UICONTROL Cloud Manager] distributionen till produktionen. |
| 9. [!UICONTROL Cloud Manager] får artefakter att distribuera | [!UICONTROL Cloud Manager] hämtar lagrade versionsartefakter. |
| 10. Distribuera artefakter till produktion | Artefakterna distribueras till produktionsmiljön. |

### Konfigurera en CI/CD-pipeline {#how-to-setup-a-ci-cd-pipeline}

Mer information om pipelinekonfigurationen finns i dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

## Kvalitetsportar {#quality-gates}

CI/CD-pipeline innehåller kvalitetsportar eller acceptanskriterier som måste uppfyllas innan koden kan flyttas från mellanlagringsmiljön till distributionsmiljön. Det finns tre portar i pipeline:

* Kodkvalitet
* Prestandatestning
* Säkerhetstestning

För var och en av dessa portar finns det tre problemnivåer som kan identifieras:

* **Kritisk** - Kritiska problem som identifieras av portalen orsakar ett omedelbart fel i pipeline.
* **Viktigt** - Viktiga problem som identifieras av portalen gör att pipelinen försätts i pausat läge. Distributionshanteraren, projektledaren eller företagsägaren kan åsidosätta problemen, vilket gör att pipeline kan fortsätta. Alternativt kan de acceptera problemen, vilket gör att pipelinen avbryts om ett fel uppstår.
* **Information** - Informationsproblem som identifieras av porten tillhandahålls endast i informationssyfte och påverkar inte pipeline-körningen.

Följande är ett exempel på en kodsökning där problem identifieras.

![Exempel på kodsökning](/help/assets/quality-gate-failed.png)

### Konfigurera portar {#how-to-setup-gates}

Mer information om hur du ställer in kod, kvalitet och prestanda finns i dokumentet [Configuring Production Pipelines](/help/using/production-pipelines.md).
