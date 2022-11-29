---
title: Konfigurera produktionsförlopp
description: Lär dig hur du använder Cloud Manager för att skapa och konfigurera produktionsflöden för att distribuera din kod.
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 39b38da17ed1cadf4f2e9633a9e76b537325316f
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---


# Konfigurera produktionsförlopp {#configuring-production-pipelines}

Lär dig hur du använder Cloud Manager för att skapa och konfigurera produktionsflöden för att distribuera din kod. Om du först vill ha en mer begreppsmässig översikt över hur rörledningar fungerar i Cloud Manager kan du läsa dokumentet [CI/CD-ledningar.](/help/overview/ci-cd-pipelines.md)

## Översikt {#overview}

Använda **Inställningar för pipeline** sida vid sida [!UICONTROL Cloud Manager] Du kan skapa två olika typer av rörledningar.

* **Produktionsförlopp** - En produktionsledning är en specialbyggd pipeline som består av en serie samordnade steg för att ta källkod från Git-databasen hela vägen in i produktionen.
* **Icke-produktionsförlopp** - Ett icke-produktionsflöde som främst används för att utföra kodkvalitetsinläsningar eller för att distribuera källkod till en utvecklingsmiljö.

Det här dokumentet fokuserar på produktionsrörledningar. Mer information om hur du konfigurerar icke-produktionsrörledningar finns i dokumentet [Konfigurerar icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

The **Distributionshanteraren** rollen är ansvarig för att ställa in pipeline. Pipeline-konfigurationen består av:

1. Definierar den utlösare som ska starta pipelinen.
1. Definiera parametrarna som styr produktionsdistributionen.
1. Konfigurerar prestandatestparametrarna.

>[!NOTE]
>
>En pipeline kan inte konfigureras förrän dess associerade Git-databas har minst en gren och [programinställningar](/help/getting-started/program-setup.md) är klar.

## Videosjälvstudiekurs {#video-tutorial-one}

Den här videon ger en översikt över processen att skapa pipeline, som beskrivs i det här dokumentet.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## Lägga till en ny produktionspipeline {#adding-production-pipeline}

När du har använt [!UICONTROL Cloud Manager] Gränssnittet för att konfigurera programmet och ha minst en miljö är du redo att lägga till en produktionsprocess.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** sida och klicka på **+Lägg till** och markera **Lägg till produktionspipeline**.

   ![Lägg till en produktionspipeline](/help/assets/configure-pipelines/add-prod1.png)

1. The **Lägg till produktionspipeline** öppnas i **Konfiguration** -fliken där ett antal alternativ för din pipeline måste definieras. Dessa alternativ är grupperade i fällbara avsnitt och beskrivs i följande steg.

   1. Ange ett beskrivande namn för din pipeline i **Pipelinenamn** fält.

   1. Under **Källkod** -avsnittet definierar du var pipelinen hämtar koden som ska bearbetas.

      * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.
      >[!TIP]
      >
      >Se dokumentet [Programinställningar](/help/getting-started/program-setup.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

      * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.

      ![Definiera rapporter för pipeline](/help/assets/configure-pipelines/add-prod2.png)

   1. Under **Miljö** definierar du vilka utlösare en distribution ska ha och hur den ska lanseras per miljö.

      1. I **SCEN** kan du definiera hur pipeline ska distribueras till din staging-miljö.

         * **Utlösare för distribution** - Du har följande alternativ för att definiera distributionsutlösarna för att starta pipeline.

            * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt med hjälp av användargränssnittet i Cloud Manager.
            * **Vid Git-ändringar** - Detta alternativ startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.
         * **Beteende vid viktiga måttfel** - Under pipeline-konfigurationen eller redigeringen kan Deployment Manager definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

            * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
            * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
            * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

         ![Distributionsutlösare](/help/assets/configure-pipelines/add-prod3.png)

         * **Distributionsalternativ** - Du kan snabba upp vissa distributionsuppgifter.

            * **Godkänn efter scendistribution** - Detta godkännande sker efter distributionen till testmiljön innan testningen är klar. Annars sker godkännandet före produktionsdistributionen, vilket sker när all testning är klar.

            * **Hoppa över ändringar i belastningsutjämnaren** - Ändringar i belastningsutjämnaren görs inte.

         ![Distributionsalternativ för mellanlagring](/help/assets/configure-pipelines/add-prod4.png)

         * **Dispatcher-konfiguration** - **Distributionshanteraren** kan konfigurera en uppsättning innehållssökvägar som antingen blir ogiltiga eller tömda från AEM Dispatcher-cachen när en pipeline körs. Dessa cacheåtgärder kommer att utföras som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM som standard. Så här konfigurerar du:

            1. Under **BANA** innehåller en innehållssökväg.
            1. Under **TYP** markerar du den åtgärd som ska utföras på den banan.

               * **Töm** - Utför en cacheborttagning.
               * **Ogiltigförklara** - Utför en cacheogiltigförklaring, ungefär som när innehåll aktiveras från en redigeringsinstans till en publiceringsinstans.
            1. Klicka **Lägg till bana** för att lägga till den angivna sökvägen. Du kan lägga till upp till 100 sökvägar per miljö.

         ![Dispatcher-konfiguration](/help/assets/configure-pipelines/dispatcher-stage.png)

         >[!TIP]
         >
         >I allmänhet är det bättre att använda åtgärden invalidate, men det kan finnas fall där det krävs tömning, särskilt när du använder AEM HTML Client Libraries.

      1. I **PRODUKTION** kan du definiera hur pipeline ska lanseras i din produktionsmiljö.

         * **Distributionsalternativ** - Du kan definiera parametrarna som styr produktionsdistributionen.

            * **Använd Go Live Approval** - En distribution måste godkännas manuellt av en användare med **Företagsägare**, **Projektledare**, eller **Distributionshanteraren** roll via [!UICONTROL Cloud Manager] Gränssnitt.
            * **Schemalagd** - Det här alternativet stoppar pipelinen före produktionsdistributionen så att den kan schemaläggas. Om det här alternativet väljs avbryts pipeline efter distributionen till mellanlagringsmiljön och användaren uppmanas att vidta åtgärden.
               * **Nu** - Det här alternativet distribuerar till produktionen omedelbart och slutför i praktiken pipelinen.
               * **Datum** - Med det här alternativet kan användaren schemalägga en tid när distributionen ska slutföras.
               * **Stoppa körning** - Det här alternativet avbryter distribution till produktion.

            >[!TIP]
            >
            >Se dokumentet [Koddistribution,](/help/using/code-deployment.md) om du vill veta hur du ställer in distributionsschemat eller kör pipelinen direkt.

            * **Använd CSE-översikt** - Om det här alternativet är markerat är en CSE engagerad för att starta distributionen. När du skapar eller redigerar en pipeline när det här alternativet är aktiverat visas **Distributionshanteraren** rollen har följande alternativ.

               * **Alla ärenden** - Med det här alternativet kan alla tillgängliga CSE-instanser starta distributionen.
               * **Mitt ärende** - Det här alternativet tillåter endast den specifika CSE som kunden har tilldelats för att starta distributionen. Detta gäller även för den angivna säkerhetskopian av CSE om den tilldelade CSE inte är tillgänglig.

            ![Alternativ för produktionsdistribution](/help/assets/configure-pipelines/prod-deploymentoptions.png)

         * **Dispatcher-konfiguration** - Definiera dispatcherkonfigurationen för produktionsmiljön. Alternativen är desamma som för mellanlagringsmiljön.










1. Klicka på **Fortsätt** för att gå vidare till **Scentestning** där du kan konfigurera AEM Sites och AEM Assets Performance Testing, beroende på vilka produkter du har licensierat.

   >[!TIP]
   >
   >Se dokumentet [Testning av kodkvalitet](/help/using/code-quality-testing.md#performance-testing) om du vill ha mer information om alternativen på **Scentestning** -fliken.

   1. Under **Platsinnehållsleverans/distribuerad lastvikt** definierar du hur platsens prestandatestning ska konfigureras baserat på vikten av sidförfrågningar mellan de tre siduppsättningarna, som kan aktiveras eller inaktiveras.

      * **Populära Live-sidor**
      * **Andra Live-sidor**
      * **Nya sidor**

      ![Platsens lastvikt](/help/assets/configure-pipelines/add-prod5.png)

   1. Under **Distribution av prestandatestning av resurser** definierar du testdistributionen av bilder och PDF samt definierar dina egna testresurser.

      * **Bilder** - Justera skjutreglaget för att justera testdelningen mellan bilder och PDF.
      * **PDF** - Justera skjutreglaget för att justera testdelningen mellan bilder och PDF.

      * Definiera egna resurser genom att överföra dem.

         1. **FORMAT** - Välj om din anpassade resurs är PDF i en bild.
         1. **FILNAMN** - Använd filläsarknappen för att välja en bild från den lokala datorn.
         1. **Lägg till testfil** - Klicka för att överföra den valda resursen.

      ![Distribution av resurstestning](/help/assets/configure-pipelines/add-prod6.png)



1. Klicka **Spara** för att lägga till produktionsflödet.

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden. Se dokumentet [Koddistribution](/help/using/code-deployment.md) för mer information.
