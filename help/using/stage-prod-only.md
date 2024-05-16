---
title: Pipeline med endast scener och endast prod
description: Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.
source-git-commit: c09fbf30270523018a36b128d43cbf10e65daf54
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---


# Pipeline med endast scener och endast produktion {#stage-prod-only}

Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopteringsprogrammet.](/help/release-notes/current.md#early-adoption)

## Ökning {#overview}

Mellanlagrings- och produktionsmiljöer är nära kopplade. Som standard är distributioner till dem länkade till en enda pipeline. Det är en driftsättningspipeline som distribueras till både testnings- och produktionsmiljöerna i det programmet. Även om denna koppling normalt är lämplig, finns det vissa användningsområden där det finns nackdelar:

* Om du vill distribuera till enbart scenen kan du bara göra detta genom att avvisa **Befordra till produkt** steg i pipeline. Körningen markeras dock som avbruten.
* Om du vill distribuera den senaste koden i en staging-miljö till produktion måste du distribuera om hela pipelinen, inklusive staging-distributionen, även om ingen kod har ändrats där.
* Eftersom miljöer inte kan uppdateras under distributioner och du vill pausa och testa i staging-miljön i flera dagar innan du marknadsför till produktion, kan produktionsmiljön inte uppdateras. Detta gör icke-beroende uppgifter som att uppdatera [miljövariabler](/help/getting-started/build-environment.md#environment-variables) omöjlig.

Enkla rörledningar för scener och enbart för produkter erbjuder lösningar för dessa användningsområden genom att tillhandahålla dedikerade driftsättningsalternativ.

* **Distributionsförlopp endast för scenen** distribuera endast till en staging-miljö där körningen är klar när distributionen och testerna är klara.
   * En pipeline som bara är i ett steg fungerar på samma sätt som den standardkopplade kompletta stackproduktionskanalen, men utan stegen för produktionsdistribution (godkännande, schema, driftsättning).
* **Distributionsförlopp endast för produkter** distribuera endast till en produktionsmiljö med möjlighet att välja en körning som har slutförts och validerats på scenen och distribuera dess artefakter på produkten.
   * Med rörledningar som endast är avsedda för produktion återanvänds artefakterna från scendistributionerna, och byggnadsfasen hoppas över.

Vare sig rörledningar som bara är i stadiet eller endast i drift kommer att utföras medan en produktionsprocess med en hel hög körs och vice versa.

De här dedikerade rörledningarna ger större flexibilitet, men notera följande detaljer om drift och rekommendationer.

>[!NOTE]
>
>I rörledningar som endast är avsedda för produktion används alltid artefakter från rörledningen som endast är i stadiet, oavsett vad som under tiden kan ha driftsatts på scenen via den kopplade standardproduktionsledningen.
>
>* Detta kan leda till oönskade kodåterställningar.
>* Adobe rekommenderar att du slutar använda den standardiserade kopplade produktionskanalen när du väl har börjat använda pipelines som bara är för prod och enbart för stage.
>* Om du fortfarande bestämmer dig för att köra både standardrörledningarna och rörledningar för scen/endast för produkt, bör du tänka på att artefakter återanvänds för att undvika att koda om.

## Skapa pipeline {#pipeline-creation}

Rörledningar som endast är avsedda för produktion och enbart för scenen skapas på ungefär samma sätt som standardrörledningar som är kopplade [produktionsrörledningar](/help/using/production-pipelines.md) och [rörledningar för icke-produktion.](/help/using/non-production-pipelines.md) Mer information finns i dessa dokument.

1. I **Pipelines** fönster, trycka eller klicka **Lägg till pipeline**.

   * Välj **Lägg till icke-produktionsförlopp** om du vill skapa en pipeline som bara innehåller en scen.
   * Välj **Lägg endast till produktionsförlopp** för att skapa en pipeline som bara är avsedd för produktion.

   ![Skapa en pipeline enbart för produkt/scen](/help/assets/configure-pipelines/prod-stage-pipelines.png)

>[!NOTE]
>
>Vissa alternativ kan vara nedtonade om motsvarande rörledningar redan finns.
>
>* **Lägg endast till produktionsförlopp** kommer inte att vara tillgängligt om det inte finns någon pipeline som bara är för ett steg.
>* **Lägg till produktionspipeline** kommer inte att vara tillgängligt om det redan finns en kopplad standardpipeline.
>* Endast en prod- och endast en fasledning tillåts per program.

### Enbart Stage-förlopp {#stage-only}

1. När du valt **Lägg till icke-produktionsförlopp** alternativ, **Lägg till icke-produktionsförlopp** öppnas.
1. Om du vill skapa en pipeline som bara är för en scen väljer du scenmiljön i **Berättigade driftsättningsmiljöer** -fält för din pipeline. Fyll i återstående fält och tryck eller klicka **Fortsätt**.

   ![Skapa en pipeline som bara är för scenen](/help/assets/configure-pipelines/stage-only.png)

1. På **Scentestning** kan du sedan definiera testning som ska utföras i mellanlagringsmiljön. Tryck eller klicka **Spara** för att spara din nya pipeline.

   ![Testparametrar för en pipeline som bara är en del av ett steg](/help/assets/configure-pipelines/stage-only-test.png)

### Prod-Only Pipelines {#prod-only}

1. När du valt **Lägg endast till produktionsförlopp** alternativ, **Lägg endast till produktionsförlopp** öppnas.
1. Ange en **Pipelinenamn**. De återstående alternativen och funktionerna i dialogrutan fungerar på samma sätt som i den vanliga dialogrutan för att skapa kopplad pipeline. Tryck eller klicka **Spara** för att spara rörledningen.

   ![Skapa en pipeline som bara är avsedd för produktion](/help/assets/configure-pipelines/prod-only-pipeline.png)

## Köra endast prod- och Stage-pipelines {#running}

Rörledningar som endast fungerar som prod och enbart scener körs på samma sätt som [alla andra rörledningar är i drift.](/help/using/managing-pipelines.md#running-pipelines) Mer information finns i den dokumentationen.

Dessutom kan en pipelinekörning som bara är avsedd för produktion aktiveras direkt från körningsinformationen för en pipeline som bara är avsedd för en viss fas.

### Enbart Stage-förlopp {#stage-only-run}

En rörledning som bara fungerar på en scen fungerar på nästan samma sätt som vanliga kopplade rörledningar. När du är klar med körningen, efter teststegen, kan du **Promote Build** Med knappen kan du påbörja en produkts-only-pipeline-körning som använder artefakter som distribueras på scenen av den här körningen och distribuerar dem i produktionen.

![Körning av endast Stage-pipeline](/help/assets/configure-pipelines/stage-only-pipeline-run.png)

The **Promote Build** visas bara om du använder den senaste pipelinekörningen som bara fungerar på scenen. När du har tryckt eller klickat uppmanas du att bekräfta körningen av den produktspecifika pipelinen eller att skapa en produktbaserad pipeline om det inte redan finns en.

### Prod-Only Pipelines {#prod-only-run}

För rörledningar som endast är avsedda för produktion är det viktigt att identifiera de källartefakter som ska distribueras till produktionen. Den här informationen finns i **Förberedelse av felaktigheter** steg. Du kan navigera till dessa körningar för mer information och loggar.

![Artefaktdetaljer](/help/assets/configure-pipelines/prod-only-pipeline-run.png)
