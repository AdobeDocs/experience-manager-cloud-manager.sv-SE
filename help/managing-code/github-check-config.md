---
title: GitHub-kontrollkonfiguration för privata databaser
description: Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.
exl-id: 29c9e487-e196-411a-8cda-6751b0a56066
source-git-commit: e93285f7c7495ec9d2f11d289adaf6aaba7e58ea
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# GitHub-kontrollkonfiguration för privata databaser {#github-check-config}

Lär dig hur du styr de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas.

## Konfiguration av GitHub-kontroller {#configuration}

När du använder [privata databaser ](private-repositories.md#using) skapas en [pipeline för full stackkodkvalitet](/help/overview/ci-cd-pipelines.md) automatiskt. Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

Du kan kontrollera dessa kontroller genom att skapa en `.cloudmanager/pr_pipelines.yml`-fil i standardgrenen i den privata databasen.

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| Parameter | Möjliga värden | Standard | Beskrivning |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` eller `false` | `false` | Om bara den sista kommentaren med kodskanningen ska behållas i denna GitHub-pull-begäran eller om alla ska behållas |
| `type` | `CI_CD` | n/a | Definierar beteendet för en CI/CD-pipeline |
| `template.programID` | Heltal | Inga pipeline-variabler återanvänds | Kan användas för att återanvända de [pipeline-variabler](/help/getting-started/build-environment.md#pipeline-variables) som anges på en av de befintliga pipelines som skapas automatiskt av varje PR. |
| `template.pipelineID` | Heltal | Inga pipeline-variabler återanvänds | Kan användas för att återanvända de [pipeline-variabler](/help/getting-started/build-environment.md#pipeline-variables) som anges på en av de befintliga pipelines som skapas automatiskt av varje PR. |
| `namePrefix` | Sträng | `Full Stack Code Quality Pipeline for PR` | Används för att ange namnet på den pipeline som skapas automatiskt |
| `importantMetricsFailureBehavior` | `CONTINUE` eller `FAIL` eller `PAUSE` | `CONTINUE` | Anger det viktiga måttbeteendet för pipelinen <br>`CONTINUE` = Om ett viktigt mätresultat misslyckas, flyttas pipelinen automatiskt framåt <br>`FAIL` = pipelinen avslutas med en FAILED-status om ett viktigt mätresultat misslyckas<br>`PAUSE` = Kodsökningssteget får en VÄNTNINGSstatus när ett viktigt mätresultat misslyckas och måste återupptas manuellt |
