---
title: GitHub-kontrollanteckningar
description: Lär dig hur GitHub kontrollerar annonser för dina privata databaser för att ge dig användbar feedback.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# GitHub-kontrollanteckningar {#github-annotations}

Lär dig hur GitHub kontrollerar annonser för dina privata databaser för att ge dig användbar feedback.

## Ökning {#overview}

Om du använder [privata databaser](private-repositories.md) för ditt Cloud Manager-program körs kontroller i GitHub automatiskt för varje pull-begäran. Dessa kommentarer innehåller användbar information som hjälper dig att förstå eventuella problem med koden så snart som möjligt.

![Exempel på GitHub-kontrollanteckningar](assets/github-check-annotations.png)

[Problem med kodkvalitet](/help/using/code-quality-testing.md) som upptäckts av [SonarQube](/help/using/custom-code-quality-rules.md) visas tydligt.

![Exempel på kommentar om kodproblem](assets/github-check-annotations-example.png)

Den exakta kodraden med problemet anges och du kan klicka på den för att visa relevant kod. De här anteckningarna tillhandahålls för alla kodproblem, inte bara de som har ändrats i pull-begäran.

![Exempel på kommentar om kodproblem](assets/github-check-annotations-example-code.png)

Alla kommenterade rader samlas på fliken **Filer ändrade** i GitHub-pull-begäran. Anteckningar för filer som inte har ändrats i pull-begäran visas i sina egna avsnitt.

![Exempel på anteckningar i filer har ändrats på fliken ](assets/github-check-annotations-files-changed.png)

## Kodkvalitetsförlopp {#code-quality-pipelines}

Resultat av [kodkvalitet](/help/using/code-quality-testing.md) visas också i pipeline som automatiskt aktiveras av Cloud Manager längst ned på fliken **Checks**. Den är också tillgänglig från **Information** vid kontrollen av pull-begäran.

![Exempel på anteckningar](assets/github-check-annotations-code-quality.png)

![Exempel på anteckningar](assets/github-check-annotations-code-quality-2.png)

Du kan även visualisera problemen i form av en CSV-fil. Detta kan hämtas genom att [visa information om pipelinekörningen i Cloud Manager](/help/using/managing-pipelines.md).
