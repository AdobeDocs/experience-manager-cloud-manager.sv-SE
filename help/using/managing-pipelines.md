---
title: Hantera pipelines
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
exl-id: e36420d2-57c5-4375-99fb-dd47c1c8bffd
source-git-commit: ab527beb706ab73a14cc933a3414873dee6b7a9e
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Hantera pipelines {#managing-pipelines}

Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.

## Pipeline-kort {#pipeline-card}

The **Pipelines** på **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/assets/configure-pipelines/pipelines-card.png)

Genom att klicka på ellipsknappen bredvid varje pipeline kan du utföra följande åtgärder.

* [Kör pipeline](#running-pipelines)
* [Redigera pipeline](#editing-pipelines)
* [Ta bort pipeline](#deleting-pipelines)
* [Visa detaljer](#view-details)

Längst ned i listan med rörledningar finns allmänna alternativ.

* **Lägg till** - Till [lägg till en ny produktionspipeline](/help/using/production-pipelines.md) eller [lägga till ny icke-produktionspipeline](/help/using/non-production-pipelines.md)
* **Visa alla** - Tar användaren till **Pipelines** för att visa alla rörledningar i en mer detaljerad tabell
* **Åtkomst till svarsinformation** - Visar den information som krävs för att komma åt Cloud Managers Git-databas
* **Läs mer** - Navigerar till CI/CD pipeline-dokumentationsresurser.

## Fönstret Pipelines {#pipelines}

The **Pipelines** visas en fullständig lista över alla pipelines för det valda programmet. Detta är användbart eftersom det ger mer omfattande information än vad som finns i [Pipelinekort.](#pipeline-card)

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** sida, tryck eller klicka på **Pipelines** för att växla till **Pipelines** -fönstret.

1. Här visas en lista över alla rörledningar för programmet samt start och stopp för pipelinekörning på samma sätt som i **Förloppskort**.

Tryck eller klicka på `i` visas information om den senaste eller aktuella körningen av pipeline.

![Information om pipeline-körning](/help/assets/configure-pipelines/pipeline-status.png)

Tryck eller klicka **Visa detaljer** tar dig till [information om pipelinekörningen.](#view-details)

## Aktivitetsfönster {#activity}

The **Verksamhet** visas en fullständig lista över alla pipelines-körningar för det valda programmet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** sida, tryck eller klicka på **Aktivitet** för att växla till **Aktivitet** -fönstret.

1. Här visas en lista över alla pipeline-körningar för programmet, inklusive aktuella och historiska körningar.

Tryck eller klicka på `i` visas information om körningen av den valda pipeline-körningen.

![Information om pipeline-körning](/help/assets/configure-pipelines/pipeline-activity.png)

Tryck eller klicka **Visa detaljer** tar dig till [information om pipelinekörningen.](#view-details)

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
      * [Konfigurera produktionsförlopp](/help/using/production-pipelines.md)
      * [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md)

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

![Information om pipeline](/help/assets/configure-pipelines/pipeline-running-details.png)

Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Se dokumentet [Koddistribution](/help/using/code-deployment.md) för mer information.

Alla steg i en pipeline-körning visas med de som ännu inte har startats nedtonade. De färdiga stegen visar varaktigheten.

När ett pipeline-steg är klart visas en sammanfattning.

![Stegsammanfattning](/help/assets/configure-pipelines/pipeline-step.png)

Tryck eller klicka på **Visa detaljer** länk för att visa **Varaktighet** -avsnitt. Detta inbegriper den genomsnittliga rörledningens varaktighet på grundval av den historiska trenden för det programmet.

![Varaktighet](/help/assets/configure-pipelines/duration.png)

>[!NOTE]
>
>Du kan bara visa information om en pipeline som körs eller har körts minst en gång.
