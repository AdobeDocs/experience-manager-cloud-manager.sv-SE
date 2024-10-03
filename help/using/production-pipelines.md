---
title: Lägg till en produktionspipeline
description: Lär dig hur du använder Cloud Manager för att skapa och konfigurera produktionsledningar för att distribuera din kod.
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 1209faf71edbd74cd87acfe24ec438b98ddd4a3a
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---


# Lägg till en produktionspipeline {#configuring-production-pipelines}

Lär dig hur du använder Cloud Manager för att skapa och konfigurera produktionsledningar för att distribuera din kod. Om du först vill ha en mer konceptuell översikt över hur rörledningar fungerar i Cloud Manager kan du läsa [CI/CD-pipelines](/help/overview/ci-cd-pipelines.md).

## Ökning {#overview}

Med panelen **Inställningar för pipeline** i [!UICONTROL Cloud Manager] kan du skapa två olika typer av pipelines.

* **Produktionspipelines** - En produktionspipeline är en specialbyggd pipeline som består av en serie samordnade steg för att ta källkod från din Git-databas hela vägen in i produktionen.
* **Icke-produktionsförlopp** - En icke-produktionsförlopp används främst för att köra kodkvalitetsgenomsökningar eller för att distribuera källkod till en utvecklingsmiljö.

Det här dokumentet fokuserar på produktionsrörledningar. Mer information om hur du konfigurerar icke-produktionspipelines finns i dokumentet [Konfigurera icke-produktionspipelines](/help/using/non-production-pipelines.md).

Rollen **Distributionshanteraren** ansvarar för att ställa in pipeline. Pipeline-konfigurationen består av:

1. Definierar den utlösare som startar pipelinen.
1. Definiera parametrarna som styr produktionsdistributionen.
1. Konfigurerar prestandatestparametrarna.

>[!NOTE]
>
>Det går inte att konfigurera en pipeline förrän dess associerade Git-databas har minst en gren och [programkonfigurationen](/help/getting-started/program-setup.md) är klar.

## Lägg till en ny produktionspipeline {#adding-production-pipeline}

När du har använt användargränssnittet för [!UICONTROL Cloud Manager] för att konfigurera programmet och har minst en miljö är du redo att lägga till en produktionspipeline.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.

1. Klicka på **+Lägg till** och välj sedan **Lägg till produktionspipeline**.

   ![Lägg till en produktionspipeline](/help/assets/configure-pipelines/add-prod1.png)

1. Dialogrutan **Lägg till produktionspipeline** öppnas på fliken **Konfiguration** där ett antal alternativ för din pipeline måste definieras. Dessa alternativ är grupperade i fällbara avsnitt och beskrivs i följande steg.

   1. Ange ett beskrivande namn för pipelinen i fältet **Pipelinenamn**.

   1. Under avsnittet **Source Code** definierar du var pipelinen hämtar koden som bearbetas.

      * **Databas** - Definierar vilken Git-repo som pipelinen ska hämta koden.

      >[!TIP]
      >
      >Läs dokumentet [Programinställningar](/help/getting-started/program-setup.md) om du vill veta mer om hur du lägger till och hanterar databaser i Cloud Manager.

      * **Git-grenen** - Definierar från vilken gren i den valda pipeline som ska hämta koden.
      * **Kodplats** - Definierar sökvägen i grenen för den valda rapporten från vilken pipelinen ska hämta koden.

      ![Definiera repor för pipeline](/help/assets/configure-pipelines/add-prod2.png)

   1. Under avsnittet **Miljö** definierar du vilka som utlöser en distribution och hur den ska introduceras per miljö.

      1. I avsnittet **STAGE** kan du definiera hur pipelinen ska placeras i mellanlagringsmiljön.

         * **Distributionsutlösare** - Du har följande alternativ för att definiera distributionsutlösarna för att starta pipeline.

            * **Manuell** - Starta pipelinen manuellt med Cloud Manager-gränssnittet.
            * **Vid Git-ändringar** - Starta CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

         * **Beteende vid viktiga mätfel** - Under pipeline-konfiguration eller redigering kan Deployment Manager definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

            * **Fråga varje gång** - Standardinställningen och kräver manuell åtgärd vid viktiga fel.
            * **Misslyckades omedelbart** - pipelinen avbryts när ett viktigt fel inträffar. Den emulerar att en användare manuellt avvisar varje fel.
            * **Fortsätt omedelbart** - pipelinen fortsätter automatiskt när ett viktigt fel inträffar. Den emulerar en användare som manuellt godkänner varje fel.

         ![Distributionsutlösare](/help/assets/configure-pipelines/add-prod3.png)

         * **Distributionsalternativ** - Du kan snabba upp vissa distributionsåtgärder.

            * **Godkänn efter scendistribution** - Detta godkännande sker efter distributionen till mellanlagringsmiljön innan testningen är klar. Annars sker godkännandet före produktionsdistributionen, vilket sker när all testning är klar.

            * **Hoppa över ändringar i belastningsutjämnaren** - inga ändringar görs i belastningsutjämnaren.

         ![Alternativ för mellanlagringsdistribution](/help/assets/configure-pipelines/add-prod4.png)

         * **Dispatcher-konfiguration** - Rollen **Distributionshanteraren** kan konfigurera en uppsättning innehållssökvägar som antingen är ogiltiga eller tömda från AEM Dispatcher-cache när en pipeline körs. Dessa cacheåtgärder utförs som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM Dispatcher standardbeteende. Så här konfigurerar du:

            1. Under **PATH** anger du en innehållssökväg.
            1. Under **TYP** väljer du vilken åtgärd som ska utföras på sökvägen.

               * **Rensa** - Utför en cacheborttagning.
               * **Invalidera** - Utför en cacheogiltigförklaring, ungefär som när innehåll aktiveras från en redigeringsinstans till en publiceringsinstans.

            1. Klicka på **Lägg till sökväg** för att lägga till den angivna sökvägen. Du kan lägga till upp till 100 sökvägar per miljö.

         ![Dispatcher-konfiguration](/help/assets/configure-pipelines/dispatcher-stage.png)

         >[!TIP]
         >
         >I allmänhet är det bättre att använda åtgärden invalidate, men det kan finnas fall där det krävs tömning, särskilt när du använder AEM HTML Client Libraries.

      1. I avsnittet **PRODUKTION** kan du definiera hur pipelinen ska placeras i din produktionsmiljö.

         * **Distributionsalternativ** - Du kan definiera parametrarna som styr produktionsdistributionen.

            * **Använd Go Live Approval** - En användare med rollen **Business Owner**, **Project Manager** eller **Deployment Manager** via användargränssnittet i [!UICONTROL Cloud Manager] måste godkänna en distribution manuellt.
            * **Schemalagd** - Stoppar pipelinen före produktionsdistributionen så att den kan schemaläggas. Om det här alternativet väljs avbryts pipeline efter distributionen till mellanlagringsmiljön och användaren uppmanas att vidta åtgärden.
               * **`Now`** - Distribuerar till produktion omedelbart och slutför pipelinen.
               * **Datum** - Användaren kan schemalägga en tidpunkt när distributionen ska slutföras.
               * **Stoppa körning** - Avbryter distributionen till produktionen.

           >[!TIP]
           >
           >Se [Koddistribution](/help/using/code-deployment.md) om du vill veta hur du ställer in distributionsschemat eller kör pipeline direkt.

            * **Använd CSE Oversight** - Om det här alternativet är markerat är en CSE (Customer Success Engineer) engagerad för att starta den faktiska distributionen. När du skapar eller redigerar en pipeline när det här alternativet är aktiverat har rollen **Distributionshanterare** följande alternativ.

               * **Valfri CSE** - Tillåter alla tillgängliga CSE att starta distributionen.
               * **Min CSE** - Endast den specifika CSE som tilldelats kunden kan starta distributionen. Det här alternativet gäller även för den angivna säkerhetskopian av CSE om den tilldelade CSE-filen inte är tillgänglig.

           ![Alternativ för produktionsdistribution](/help/assets/configure-pipelines/prod-deploymentoptions.png)

         * **Dispatcher-konfiguration** - Definiera Dispatcher-konfigurationen för din produktionsmiljö. Alternativen är desamma som alternativen för mellanlagringsmiljön.

1. Klicka på **Fortsätt** om du vill gå vidare till fliken **Stage Testing** där du kan konfigurera AEM Sites och AEM Assets Performance Testing, beroende på vilka produkter du har licensierat.

   >[!TIP]
   >
   >Se [Testning av kodkvalitet](/help/using/code-quality-testing.md#performance-testing) för mer information om de alternativ som finns på fliken **Testning av scenen**.

   1. I avsnittet **Platsinnehållsleverans/Distribuerad lastvikt** konfigurerar du platsprestandatestning baserat på hur sidorna i en sidförfrågan vägs mellan tre siduppsättningar. Du kan aktivera eller inaktivera siduppsättningarna efter behov.

      * **Populära Live-sidor**
      * **Andra Live-sidor**
      * **Nya sidor**

      ![Platsens lastvikt](/help/assets/configure-pipelines/add-prod5.png)

   1. Under avsnittet **Assets Performance Testing Distribution** definierar du testdistributionen av bilder och PDF och definierar dina egna testresurser.

      * **Bilder** - Justera skjutreglaget för att justera testdelningen mellan bilder och PDF.
      * **PDF** - Justera skjutreglaget för att justera testdelningen mellan bilder och PDF.

      * Definiera egna resurser genom att överföra dem.

         1. **FORMAT** - Välj om din anpassade resurs är PDF i en bild.
         1. **FILENAME** - Använd filläsarknappen för att välja en bild från den lokala datorn.
         1. **Lägg till testfil** - Klicka för att överföra den valda resursen.

      ![Assets testdistribution](/help/assets/configure-pipelines/add-prod6.png)

1. Klicka på **Spara** för att lägga till produktionsflödet.

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline distribuerar du koden. Mer information finns i [Koddistribution](/help/using/code-deployment.md).

## Videosjälvstudie {#video-tutorial-one}

Den här videon ger en översikt över processen att skapa pipeline, som beskrivs i det här dokumentet.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)
