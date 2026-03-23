---
title: CI/CD-rör
description: Lär dig mer om CI/CD-pipelines och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: b7e651b72d1943aef69c1c69915d4752a6163931
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---


# Rörledningar för CI/CD {#ci-cd-pipeline}

Lär dig mer om CI/CD-pipelines och hur de hanterar distributioner till miljöer för staging och produktion i Cloud Manager.

## Ökning {#overview}

[!UICONTROL Cloud Manager] innehåller ett ramverk för kontinuerlig integrering/kontinuerlig leverans (CI/CD) som gör att implementeringsteamen kan testa snabbt och leverera ny eller uppdaterad kod. Implementeringsteamen kan konfigurera, konfigurera och starta en automatiserad CI/CD-pipeline. Detta tillvägagångssätt följer de bästa metoderna för Adobe-kodning för att utföra en omfattande kodskanning och säkerställa högsta kodkvalitet.

CI/CD-pipeline automatiserar också enhets- och prestandatestningsprocesser för att öka driftsättningseffektiviteten och proaktivt identifiera kritiska problem som är dyra att åtgärda efter driftsättningen. Implementeringsteamen kan få tillgång till en omfattande rapport om kodprestanda för att få insyn i möjliga konsekvenser för nyckeltal och kritiska säkerhetsvalideringar om koden distribueras till produktionen.

## Om pipeline-processen {#pipeline-process}

I följande diagram visas vad som händer när en release aktiveras i [!UICONTROL Cloud Manager] med hjälp av en pipeline.

![Pipeline-processen](/help/assets/screen_shot_2018-05-30at82457pm.png)

| Steg för pipeline | Beskrivning |
| --- | --- |
| &#x200B;1. Starta en release | En distributionshanterare utlöser en release antingen manuellt, med en Git-implementering eller baserat på ett återkommande schema. |
| &#x200B;2. Skapa en lanseringstagg | [!UICONTROL Cloud Manager] skapar en Git-tagg som markerar releasen med ett automatiskt genererat versionsnummer, till exempel `2018.531.245527.0000001222`. |
| &#x200B;3. Byggd som släppt med autogenererad version | [!UICONTROL Cloud Manager] skapar programmet med det nytilldelade versionsnumret. |
| &#x200B;4. Utvärdera kodkvaliteten | [!UICONTROL Cloud Manager] skannar källkoden och ger en sammanfattning innan koden kan distribueras till mellanlagringsmiljön. |
| &#x200B;5. Lagrade versionsobjekt | Versionsartefakterna lagras för senare användning i distributionsstegen. |
| &#x200B;6. Automatisk distribution av artefakter till AMS AEM-testning | Frisläppningsartefakten distribueras till testmiljön. |
| &#x200B;7. Utlösa automatiska tester | [!UICONTROL Cloud Manager] kör prestanda- och säkerhetstester på artefakten. |
| &#x200B;8. Driftsättning av produktionsutlösare | När de automatiserade testerna har slutförts startar [!UICONTROL Cloud Manager] distributionen till produktionen. |
| &#x200B;9. [!UICONTROL Cloud Manager] hämtar artefakter att distribuera | [!UICONTROL Cloud Manager] hämtar lagrade versionsartefakter. |
| &#x200B;10. Distribuera artefakter till produktion | Artefakterna distribueras till produktionsmiljön. |

### Snabbare byggen med Smart Build {#use=smart-build}

Cloud Manager använder nu en optimerad byggstrategi som kallas **Smart Build** som använder cachelagring på modulnivå för att snabba upp byggprocessen. Under varje bygge återskapas endast moduler som har ändrats, medan oförändrade moduler återanvänds från cachen.

Smart Build är endast tillgängligt för pipelines för kodkvalitet och Dev Full Stack-distribution.

Se [Lägga till en icke-produktionspipeline](/help/using/non-production-pipelines.md#add-non-production-pipeline) och [Om att använda Smart Build i en icke-produktionspipeline](/help/using/non-production-pipelines.md#about-smart-build).


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
