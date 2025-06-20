---
title: Dela endast scenen och endast produktion
description: Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.
exl-id: b7dd0021-d346-464a-a49e-72864b01cce3
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# Dela rörledningar enbart för stadier och endast för produktion {#stage-prod-only}

Du kan dela upp distributioner för staging och produktion med hjälp av dedikerade pipelines.

## Ökning {#overview}

Mellanlagrings- och produktionsmiljöer är nära kopplade. Som standard är distributioner till dem länkade till en enda pipeline. Det vill säga, en driftsättningspipeline distribueras till både testnings- och produktionsmiljöerna i det programmet. Även om denna koppling normalt är lämplig, finns det vissa användningsområden där det finns nackdelar:

* Om du vill distribuera till enbart scenen avvisar du steget **Befordra till produkt** i pipeline. Körningen markeras dock som avbruten.
* Om du vill distribuera den senaste koden i en staging-miljö till produktion måste du distribuera om hela pipelinen inklusive staging-distributionen även om ingen kod har ändrats där.
* Det går inte att uppdatera miljöer under distributioner. Om du pausar för att testa i testmiljön i flera dagar innan du befordrar till produktion, är produktionsmiljön fortfarande låst och kan inte uppdateras. Det här scenariot gör icke-beroende aktiviteter som att uppdatera [miljövariabler](/help/getting-started/build-environment.md#environment-variables) omöjliga.

Enkla rörledningar för scener och enbart för produkter erbjuder lösningar för dessa användningsområden genom att tillhandahålla dedikerade driftsättningsalternativ.

* **Distributionsförlopp endast för scenen:** Distribuerar bara till en staging-miljö där körningen är klar när distributionen och testerna är klara. En pipeline som bara är i ett steg fungerar på samma sätt som den standardkopplade kompletta stackproduktionskanalen, men utan stegen för produktionsdistribution (godkännande, schema, driftsättning).
* **Distributionsförlopp endast för produktion:** Distribuerar endast till produktion genom att välja den senaste lyckade scenkörningen. Distribuera sedan dess artefakter till produktionen. Med rörledningar som endast är avsedda för produktion återanvänds scenens distributionsartefakter, utan att byggfasen slutförs.

Rörledningar med endast scener och endast produkter utförs inte medan en produktionspipeline med fullständig stackproduktion pågår, och vice versa. Om utlösaren **On Git Changes** är konfigurerad för både produktionsflödet för enbart scenen och hela stacken och pekar på samma gren och databas, startas endast den enbart för scenen automatiskt. Skrivskyddade pipelines startar inte **`On Git Changes`** eftersom de inte är direkt länkade till en databas.

Rörledningar som endast är avsedda för produktion aktiveras manuellt eftersom de inte är direkt länkade till en databas för **Vid Git-ändringar**.

De här dedikerade rörledningarna ger större flexibilitet, men du bör notera följande detaljer om drift och rekommendationer.

>[!NOTE]
>
>I rörledningar som endast är avsedda för produktion används alltid artefakter från den pipeline som bara är till för scenen. Detta gäller även om standardproduktionsflödet under tiden har driftsatt något annat på scenen.
>
>* Scenariot kan leda till oönskade kodåterställningar.
>* Adobe rekommenderar att du slutar använda den kopplade standardproduktionskanalen när du väl har börjat använda pipelines som endast är för prod och endast för scenen.
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
1. Om du vill skapa en pipeline som bara är för ett stadium väljer du scenmiljön i fältet **Godtagbara distributionsmiljöer** för din pipeline.
1. Fyll i återstående fält.
1. Klicka på **Fortsätt**.

   ![Skapar en pipeline enbart för scenen](/help/assets/configure-pipelines/stage-only.png)

1. Definiera testningen som ska utföras i mellanlagringsmiljön på fliken **Stage Testing** .
1. Klicka på **Spara**.

   ![Testparametrar för en pipeline som bara är för scenen](/help/assets/configure-pipelines/stage-only-test.png)

### Rörledningar som endast är avsedda för produktion {#prod-only}

1. När du har klickat på **Lägg till endast produktionspipeline** öppnas den tillhörande dialogrutan.
1. Skriv det namn du vill ha i fältet **Pipelinenamn**. De återstående alternativen och funktionerna i dialogrutan fungerar på samma sätt som de alternativ som finns i den standarddialogruta där du skapar en kopplad pipeline.
1. Klicka på **Spara** i dialogrutans nedre högra hörn.

   ![Skapar en pipeline som endast är avsedd för produktion](/help/assets/configure-pipelines/prod-only-pipeline.png)

## Köra prod- och stage-only-pipelines {#running}

Rörledningar med endast prod och scenläge körs i stort på samma sätt som [alla andra pipelines körs](/help/using/managing-pipelines.md#running-pipelines). Mer information finns i den dokumentationen. Det finns dock två nya funktioner i dessa rörledningar.

* Rörledningar som bara är för scenen och endast för produkter erbjuder ett nytt [nödläge](#emergency-mode) för att hoppa över testning.
* En pipeline som endast är avsedd för produktion kan utlösas direkt från körningsinformationen för en pipeline som bara är avsedd för [scenen](#stage-only-run).

### Nödläge {#emergency-mode}

När du startar rörledningar som endast är avsedda för produktion och staging-online uppmanas du att bekräfta start och start.

* **Normalt läge** är en standardkörning och innehåller steg för testning på scenen.
* **Nödläge** hoppar över steg i testningen.

![Nödläge](/help/assets/configure-pipelines/emergency-mode.png)

### Enbart Stage-rörledningar {#stage-only-run}

En rörledning som bara fungerar på en scen fungerar på nästan samma sätt som vanliga kopplade rörledningar. Efter teststegen visas dock en **Befordra bygge**-knapp i slutet av körningen. Med den här knappen kan du påbörja en produkts-only-pipeline-körning med artefakter som distribuerades på scenen i körningen och distribuera dem till produktionen.

![En pipeline som endast är för scenen körs](/help/assets/configure-pipelines/stage-only-pipeline-run.png)

Om du klickar på **Befordra bygge** uppmanas du att bekräfta körningen av den relaterade pipeline som bara är för scenen antingen som vanligt eller i [nödläge](#emergency-mode).

Om det inte finns någon pipeline som endast är avsedd för produktion uppmanas du att skapa en.

### Rörledningar som endast är avsedda för produktion {#prod-only-run}

För rörledningar som endast är avsedda för produktion måste du identifiera de källartefakter som du vill distribuera till produktionen. De här detaljerna finns i steget **Förberedelse av felaktigheter**. Du kan navigera till dessa körningar för mer information och loggar.

![Information om felaktigheter](/help/assets/configure-pipelines/prod-only-pipeline-run.png)

