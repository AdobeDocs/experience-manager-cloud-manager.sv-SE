---
title: GitHub-kontrollanteckningar
description: Lär dig hur GitHub kontrollerar annonser för dina privata databaser för att ge dig användbar feedback.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: 210d40a5e12b40fd84efc461c6a1c48559120837
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# GitHub-kontrollanteckningar {#github-annotations}

Lär dig hur GitHub kontrollerar annonser för dina privata databaser för att ge dig användbar feedback.

## Ökning {#overview}

Om du använder [privata databaser](private-repositories.md) för ditt Cloud Manager-program körs kontroller i GitHub automatiskt för varje pull-begäran. Dessa kommentarer innehåller användbar information som hjälper dig att förstå eventuella problem med koden så snart som möjligt.

![Exempel på GitHub-kontrollanteckningar](assets/github-check-annotations.png)

[Kodkvalitet](/help/using/code-quality-testing.md) problem upptäckta av [SonarQube](/help/using/custom-code-quality-rules.md) är tydligt angivna.

![Exempel på kommentar om kodproblem](assets/github-check-annotations-example.png)

Den exakta kodraden med problemet anges och du kan klicka på den för att visa relevant kod. De här anteckningarna tillhandahålls för alla kodproblem, inte bara de som har ändrats i pull-begäran.

![Exempel på kommentar om kodproblem](assets/github-check-annotations-example-code.png)

Alla kommenterade rader sammanställs på **Ändrade filer** -fliken i GitHub pull-begäran. Anteckningar för filer som inte har ändrats i pull-begäran visas i sina egna avsnitt.

![Exempel på anteckningar i filer har ändrats](assets/github-check-annotations-files-changed.png)

## Kodkvalitetsförlopp {#code-quality-pipelines}

The [kodkvalitet](/help/using/code-quality-testing.md) resultaten visas också i pipeline, som automatiskt aktiveras av Cloud Manager längst ned i **Kontroller** -fliken. Den kan också nås via **Information** av kontrollen av pull-begäran.

![Exempel på anteckningar](assets/github-check-annotations-code-quality.png)

![Exempel på anteckningar](assets/github-check-annotations-code-quality-2.png)

Du kan även visualisera problemen i form av en CSV-fil. Detta kan hämtas av [visa information om pipeline-körningen i Cloud Manager.](/help/using/managing-pipelines.md)
