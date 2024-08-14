---
title: Pipeline med endast scener och endast prod
description: Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.
exl-id: b7dd0021-d346-464a-a49e-72864b01cce3
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Rörledningar endast för scener och produktion {#stage-prod-only}

Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet](/help/release-notes/current.md#early-adoption).

## Ökning {#overview}

Mellanlagrings- och produktionsmiljöer är nära kopplade. Som standard är distributioner till dem länkade till en enda pipeline. Det är en driftsättningspipeline som distribueras till både testnings- och produktionsmiljöerna i det programmet. Även om denna koppling normalt är lämplig, finns det vissa användningsområden där det finns nackdelar:

* Om du vill distribuera till enbart scenen kan du bara göra detta genom att avvisa steget **Befordra till produktion** i pipeline. Körningen markeras dock som avbruten.
* Om du vill distribuera den senaste koden i en staging-miljö till produktion måste du distribuera om hela pipelinen inklusive staging-distributionen även om ingen kod har ändrats där.
* Eftersom miljöer inte kan uppdateras under distributioner och du vill pausa och testa i staging-miljön i flera dagar innan du marknadsför till produktion, kan produktionsmiljön inte uppdateras. Detta gör icke-beroende aktiviteter som att uppdatera [miljövariabler](/help/getting-started/build-environment.md#environment-variables) omöjliga.

Enkla rörledningar för scener och enbart för produkter erbjuder lösningar för dessa användningsområden genom att tillhandahålla dedikerade driftsättningsalternativ.

* **Distributionsförlopp med endast scener** distribuerar bara till en staging-miljö där körningen är klar när distributionen och testerna är klara.
   * En pipeline som bara är i ett steg fungerar på samma sätt som den standardkopplade kompletta stackproduktionskanalen, men utan stegen för produktionsdistribution (godkännande, schema, driftsättning).
* **Driftsättningspipelines för enbart produkter** distribuerar bara till en produktionsmiljö med möjlighet att välja en körning som har slutförts och validerats på scenen och distribuera dess artefakter på produkten.
   * Med rörledningar som endast är avsedda för produktion återanvänds artefakterna från scendistributionerna, och byggnadsfasen hoppas över.

Vare sig rörledningar som bara är i stadiet eller endast i drift kommer att utföras medan en produktionsprocess med en hel hög körs och vice versa. Om utlösaren **On Git Changes** är konfigurerad för både produktionsflödet för enbart scenen och hela stacken och pekar på samma gren och databas, startas endast den enbart för scenen automatiskt. Rörledningar som endast är avsedda för produktion startas inte **vid Git-ändringar** eftersom de inte är direkt länkade till en databas.

De här dedikerade rörledningarna ger större flexibilitet, men du bör notera följande detaljer om drift och rekommendationer.

>[!NOTE]
>
>I rörledningar som endast är avsedda för produktion används alltid artefakter från rörledningen som endast är i stadiet, oavsett vad som under tiden kan ha driftsatts på scenen via den kopplade standardproduktionsledningen.
>
>* Detta kan leda till oönskade kodåterställningar.
>* Adobe rekommenderar att du slutar använda den standardiserade kopplade produktionskanalen när du väl har börjat använda pipelines som bara är för prod och enbart för stage.
>* Om du fortfarande bestämmer dig för att köra både standardrörledningarna och rörledningar för scen/endast för produkt, bör du tänka på att artefakter återanvänds för att undvika att koda om.

## Skapa pipeline {#pipeline-creation}

Rörledningar som endast är avsedda för produktion och endast för scenen skapas på ungefär samma sätt som standardanslutna [produktionspipelines](/help/using/production-pipelines.md) och [icke-produktionspipelines](/help/using/non-production-pipelines.md). Mer information finns i de dokumenten.

1. Klicka på **Lägg till pipeline** i fönstret **Pipelines**.

   * Välj **Lägg till icke-produktionsförlopp** om du vill skapa en pipeline som bara är avsedd för scenen.
   * Välj **Lägg till endast produktion i pipeline** om du vill skapa en pipeline som endast är avsedd för produktion.

   ![Skapar en pipeline enbart för produkt/scen](/help/assets/configure-pipelines/prod-stage-pipelines.png)

>[!NOTE]
>
>Vissa alternativ kan vara nedtonade om motsvarande rörledningar redan finns.
>
>* **Lägg till endast produktion i pipeline** är inte tillgängligt om det inte finns någon pipeline som bara är för stadiet än.
>* **Lägg till produktionspipeline** är inte tillgängligt om det redan finns en kopplad standardpipeline.
>* Endast en prod- och endast en fasledning tillåts per program.

### Enbart Stage-rörledningar {#stage-only}

1. När du har valt alternativet **Lägg till icke-produktionsförlopp** öppnas dialogrutan **Lägg till icke-produktionsförlopp** .
1. Om du vill skapa en pipeline som bara är för ett stadium väljer du scenmiljön i fältet **Godtagbara distributionsmiljöer** för din pipeline. Fyll i återstående fält och klicka på **Fortsätt**.

   ![Skapar en pipeline enbart för scenen](/help/assets/configure-pipelines/stage-only.png)

1. På fliken **Scentestning** kan du definiera testning som ska utföras i mellanlagringsmiljön. Klicka på **Spara** för att spara din nya pipeline.

   ![Testparametrar för en pipeline som bara är för scenen](/help/assets/configure-pipelines/stage-only-test.png)

### Rörledningar som endast är avsedda för produktion {#prod-only}

1. När du har valt alternativet **Lägg till endast produktion i pipeline** öppnas dialogrutan **Lägg till endast produktion i pipeline**.
1. Ange ett **pipelinenamn**. De återstående alternativen och funktionerna i dialogrutan fungerar på samma sätt som i den vanliga dialogrutan för att skapa kopplad pipeline. Klicka på **Spara** för att spara pipeline.

   ![Skapar en pipeline som endast är avsedd för produktion](/help/assets/configure-pipelines/prod-only-pipeline.png)

## Köra prod- och stage-only-pipelines {#running}

Rörledningar med endast prod och scenen körs på samma sätt som [alla andra pipelines körs](/help/using/managing-pipelines.md#running-pipelines). Mer information finns i den dokumentationen.

Dessutom kan en pipelinekörning som bara är avsedd för produktion aktiveras direkt från körningsinformationen för en pipeline som bara är avsedd för en viss fas.

### Enbart Stage-rörledningar {#stage-only-run}

En rörledning som bara fungerar på en scen fungerar på nästan samma sätt som vanliga kopplade rörledningar. Efter testningsstegen kan du emellertid med en **Promote Build**-knapp i slutet av körningen starta en produktspecifik pipeline-körning som använder artefakter som distribuerats på scenen av den här körningen och distribuerar dem i produktionen.

![En pipeline som endast är för scenen körs](/help/assets/configure-pipelines/stage-only-pipeline-run.png)

Knappen **Befordra bygge** visas bara om du är på den senaste pipelinekörningen som bara fungerar på scenen. När du klickat uppmanas du att bekräfta körningen av den produktspecifika pipelinen eller att skapa en produktbaserad pipeline om det inte redan finns en.

### Rörledningar som endast är avsedda för produktion {#prod-only-run}

För rörledningar som endast är avsedda för produktion är det viktigt att identifiera de källartefakter som ska distribueras till produktionen. Den här informationen finns i steget **Förberedelse av felaktigheter**. Du kan navigera till dessa körningar för mer information och loggar.

![Information om felaktigheter](/help/assets/configure-pipelines/prod-only-pipeline-run.png)
