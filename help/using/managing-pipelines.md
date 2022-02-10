---
title: Hantera pipeline
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
index: true
source-git-commit: 099a4490e3a8578b9f3485fd1514d1e97db977ab
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Hantera pipeline {#managing-pipelines}

Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.

## Pipeline-kort {#pipeline-card}

The **Pipelines** på **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/using/assets/configure-pipelines/pipelines-card.png)

Genom att klicka på ellipsknappen bredvid varje pipeline kan du utföra följande åtgärder.

* [Kör pipeline](#running-pipelines)
* [Redigera pipeline](#editing-pipelines)
* [Ta bort pipeline](#deleting-pipelines)
* [Visa detaljer](#view-details)

Längst ned i listan med rörledningar finns allmänna alternativ.

* **Lägg till** - Till [lägg till en ny produktionspipeline](configuring-production-pipelines.md) eller [lägga till ny icke-produktionspipeline](configuring-non-production-pipelines.md)
* **Visa alla** - Tar användaren till **Pipelines** om du vill visa alla rörledningar i en mer detaljerad tabell.
* **Åtkomst till svarsinformation** - Visar den information som krävs för att komma åt Cloud Managers Git-databas
* **Läs mer** - Navigerar till CI/CD pipeline-dokumentationsresurser.

## Löpande rörledningar {#running-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Kör** på menyn.

1. Pipeline-körningen börjar och anges av **Status** kolumn.

Du kan se information om körningen genom att klicka på ellipsknappen igen och välja **[Visa information.](#view-details)**

Beroende på typen av pipeline kan du eventuellt avbryta körningen genom att klicka på ellipsknappen igen och välja **Avbryt**.

## Redigera rörledningar {#editing-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du vill redigera och välj sedan **Redigera** på menyn.

1. The **Redigera produktionspipeline** eller **Redigera icke-produktionsförlopp** visas så att du kan redigera samma information som du angav när du skapade pipelinen.

   * På följande sidor finns mer information om alla fält och konfigurationsalternativ som är tillgängliga för pipelines.
      * [Konfigurera produktionsförlopp](configuring-production-pipelines.md)
      * [Konfigurera icke-produktionsförlopp](configuring-non-production-pipelines.md)

1. Klicka på **Uppdatera** när du är klar med redigeringen.

>[!NOTE]
>
>Du kan inte redigera en pågående pipeline.

## Tar bort pipelines {#deleting-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Ta bort** på menyn.

>[!NOTE]
>
>Du kan inte ta bort en pågående pipeline.

## Visa detaljer {#view-details}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Visa detaljer** på menyn.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

![Information om pipeline](/help/using/assets/configure-pipelines/pipeline-running-details.png)

Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Se dokumentet [Distribuera koden](deploying-code.md) för mer information.

>[!NOTE]
>
>Du kan bara visa information om en pipeline som körs eller har körts minst en gång.
