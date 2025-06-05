---
title: Hantera pipelines
description: Lär dig hur du hanterar befintliga rörledningar, inklusive att köra, redigera och ta bort dem.
exl-id: e36420d2-57c5-4375-99fb-dd47c1c8bffd
source-git-commit: 91eda02d55134fba167f30830a142a80717e9083
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---


# Hantera rörledningar {#managing-pipelines}

Lär dig hur du hanterar befintliga rörledningar, inklusive att köra, redigera och ta bort dem.

## Förloppskort {#pipeline-card}

Kortet **Pipelines** på sidan **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/assets/configure-pipelines/pipelines-card.png)

Genom att klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid varje pipeline, kan du utföra följande åtgärder:

* [Kör pipeline](#running-pipelines).
* [Redigera pipeline](#editing-pipelines).
* [Ta bort pipelinen](#deleting-pipelines).
* [Visa information](#view-details).

Längst ned i listan med rörledningar finns följande allmänna alternativ.

* **Lägg till** - Om du vill [lägga till en ny produktionspipeline](/help/using/production-pipelines.md) eller [lägga till en ny icke-produktionspipeline](/help/using/non-production-pipelines.md).
* **Visa alla** - Tar användaren till skärmen **Pipelines** för att visa alla pipelines i en mer detaljerad tabell.
* **Åtkomst till replikinformation** - Visar den information som krävs för åtkomst till Cloud Manager Git-databasen.
* **Läs mer** - Navigerar till resurser för pipeline-dokumentation för CI/CD.

## Sidan Pipelines {#pipelines}

Sidan **Pipelines** visar en fullständig lista över alla pipelines för det valda programmet. Den här listan är användbar eftersom den innehåller mer omfattande information än vad som är tillgängligt på [pipelines-kortet](#pipeline-card).

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** klickar du på fliken **Pipelines** för att växla till sidan **Pipelines** .

1. Här visas en lista med alla pipelines för programmet och du kan starta och stoppa pipelinekörning på samma sätt som i **pipelines-kortet**.

Om du klickar på ikonen `i` visas information om den senaste eller aktuella körningen av pipelinen.

![Information om pipeline-körning](/help/assets/configure-pipelines/pipeline-status.png)

Om du klickar på **Visa information** visas [information om pipelinekörningen](#view-details).

### Markera pipeline-favoriter{#pipeline-favorites}

Du kan markera specifika pipelines som favoriter så att de visas högst upp i listan på sidan **Pipelines** . Detta gör det enklare att hitta och köra rörledningar som du ofta använder.

**Så här markerar du pipeline-favoriter:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. På sidan **Programöversikt** klickar du på fliken ![Pipeline - ikonen Arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipelines** .
1. Klicka på ![Stjärndispositionsikonen ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_StarOutline_18_N.svg) till vänster om ett pipelinenamn och en pipelinetyp på sidan **Pipelines** för att lägga till den i din favoritlista.
Du kan också klicka på ikonen ![Stjärna för en favoritpipeline](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Star_18_N.svg) om du vill ta bort pipelinen från favoritlistan.


## Aktivitetssida {#activity}

På sidan **Aktiviteter** visas en fullständig lista över alla pipelines-körningar för det valda programmet.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** klickar du på fliken **Aktivitet** för att växla till sidan **Aktivitet** .

1. Här visas en lista över alla pipeline-körningar för programmet, inklusive aktuella och historiska körningar.

Om du klickar på ikonen `i` visas information om körningen av den valda pipeline-körningen.

![Information om pipeline-körning](/help/assets/configure-pipelines/pipeline-activity.png)

Klicka på **Visa information** om du vill granska [information om pipelinekörningen](#view-details).

## Köra en pipeline {#run-one-pipeline}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.
1. Klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör och klicka sedan på **Kör**.

   Statuskolumnen anger när pipeline-körningen börjar.

   Du kan visa information om körningen genom att klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) igen och klicka på **[Visa information](#view-details)**.

   Beroende på vilken typ av pipeline det gäller kan du eventuellt avbryta körningen genom att klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) igen och klicka på **Avbryt**.

## Köra flera rörledningar {#run-multiple-pipelines}

Med Cloud Manager kan du köra flera olika rörledningar samtidigt, vilket förbättrar driftsättningseffektiviteten för Adobe Managed Services-kunder (AMS). Med funktionen **Kör markerad** kan du markera flera pipelines och utlösa dem för körning samtidigt. Det minskar det manuella arbetet med att behöva köra rörledningar individuellt och optimerar arbetsflödena för att bygga och driftsätta.

**Så här kör du flera pipelines:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Klicka på ikonen ![Arbetsflöde ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Förberedelser** på den vänstra menyn.
1. Markera kryssrutorna intill de rörledningar du vill köra i tabellen på sidan **Rörledning**.
Om det behövs klickar du på ![Filterikon, tratt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Filter_18_N.svg) **Filter** för att sortera pipelines efter namn, miljö, distribuerad kodtyp eller en kombination av alla tre.
1. Klicka på **Kör markerat (x)** i sidans övre högra hörn.
1. Klicka på **Kör (x)** i dialogrutan **Kör markerade pipelines (x)**.

   Knappen **Kör** visar antalet pipelines som kan fortsätta. Du kan t.ex. ha valt fyra rörledningar, men en är redan igång. En miljö som är länkad till en vald pipeline finns inte längre. I sådana fall justeras systemet därefter. Knappen uppdateras till &quot;Kör (3)&quot; för att ange att tre rörledningar kan fortsätta.

1. Pipelines börjar köras och deras status uppdateras i listan **Pipelines**.

## Redigera rörledningar {#editing-pipelines}

Du kan inte redigera en pipeline som körs.

**Så här redigerar du pipelines:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera från sidan **Programöversikt** till kortet **Pipelines**.

1. Klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du vill redigera och klicka sedan på **Redigera**.

1. I dialogrutorna **Redigera produktionspipeline** eller **Redigera icke-produktionspipeline** kan du redigera samma information som du angav när du skapade pipeline.

   Mer information om fälten och konfigurationsalternativen som är tillgängliga för pipelines finns i [Konfigurera produktionsförgreningar](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

1. Klicka på **Uppdatera** när du är klar.

## Ta bort rörledningar {#deleting-pipelines}

Du kan inte ta bort en pågående pipeline.

**Så här tar du bort pipelines:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera från sidan **Programöversikt** till kortet **Pipelines**.

1. Klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör och klicka sedan på **Ta bort**.


## Visa försäljningsförloppsinformation {#view-details}

Du kan bara visa information om en pipeline som körs eller har körts minst en gång.

**Så här visar du pipeline-information:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera från sidan **Programöversikt** till kortet **Pipelines**.

1. Klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör och klicka sedan på **Visa information**.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

![Information om pipeline](/help/assets/configure-pipelines/pipeline-running-details.png)

Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Mer information finns i dokumentet [Koddistribution](/help/using/code-deployment.md).

Alla steg i en pipeline-körning visas med de som ännu inte har startats nedtonade. De färdiga stegen visar varaktigheten.

När ett pipeline-steg är klart visas en sammanfattning.

![Stegsammanfattning](/help/assets/configure-pipelines/pipeline-step.png)

Klicka på länken **Visa information** för att visa avsnittet **Varaktighet**. Detta avsnitt innehåller den genomsnittliga rörledningens varaktighet på grundval av den historiska trenden för det programmet.

![Varaktighet](/help/assets/configure-pipelines/duration.png)

Om din pipeline innehöll ett **kodskanningssteg**, vilket gav upphov till problem, kan du klicka på **Hämta information** för att visa en lista över [kodkvalitetstester](/help/using/code-quality-testing.md) som inte godkänts.

![Kodkvalitetsproblem](assets/managing-pipelines-code-quality-issues.png)

Det finns en **projektfilsplats**-kolumn i CSV-filen som anger platsen för den felaktiga koden. Den här kolumnen är den projektrelativa sökvägen, medan kolumnen **Filplats** är Maven-genererad.

![Information om problem med genomsökning av projektkod](assets/managing-pipelines-code-quality-details.png)
