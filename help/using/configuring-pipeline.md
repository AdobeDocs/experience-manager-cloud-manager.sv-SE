---
title: Konfigurera CI/CD-pipeline
seo-title: Configure your CI/CD Pipeline
description: Följ den här sidan om du vill konfigurera dina pipeline-inställningar från Cloud Manager.
seo-description: Before you start to deploy your code, you must configure your pipeline settings from the AEM Cloud Manager.
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 2be8f290b58fff2991f876c37dd1b499bc6c5352
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Konfigurera CI/CD-pipeline {#configure-your-ci-cd-pipeline}

>[!NOTE]
>Mer information om hur du konfigurerar CI/CD-pipeline för Cloud Manager på AEM as a Cloud Service finns i [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager).

På följande sida förklaras hur du konfigurerar **Pipeline**. Mer information om hur rörledningen fungerar finns i [Översikt över pipeline för CI/CD](ci-cd-pipeline.md).


## Förstå flödet {#understanding-the-flow}

Du kan konfigurera pipeline från panelen **Pipeline-inställningar** i [!UICONTROL Cloud Manager].

Distributionshanteraren ansvarar för att ställa in pipeline. När du gör det väljer du först en gren i **Git-databas**. Pipeline-konfigurationen består av:

* definiera den utlösare som ska starta pipelinen.
* definiera parametrarna som styr produktionsdistributionen.
* konfigurera prestandatestparametrarna.

## Videosjälvstudiekurs {#video-tutorial-one}

### Konfigurera pipeline i Cloud Manager {#config-pipeline-video}

CI/CD Production Pipeline-konfigurationen definierar den utlösare som initierar pipelinen, parametrar som styr produktionsdistributionen och parametrar för prestandatestning.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## Konfigurera pipeline {#setting-up-the-pipeline}

>[!CAUTION]
>
>Det går inte att konfigurera pipelinen förrän Git-databasen har minst en gren och [Programinställningar](setting-up-program.md) är klar.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan ändra pipeline-inställningarna efter den första konfigurationen.

### Lägga till en ny produktionspipeline från ett pipelines-kort {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö som använder [!UICONTROL Cloud Manager] UI, du är redo att lägga till en produktionspipeline.

Så här konfigurerar du beteendet och inställningarna för produktionsflödet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **+Lägg till** och markera **Lägg till produktionspipeline**.

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **Lägg till produktionspipeline** visas.

   1. Ange **Pipelinenamn**. Du kan välja **Databas** och **Git-gren**.

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. Du kan konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**.

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      Du kan tilldela följande distributionsutlösare för att starta pipelinen:

      * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
      * **Vid Git-ändringar** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

      Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

      Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

      * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
      * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
      * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.
   1. Välj **Distributionsalternativ**.

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **Godkänn efter scendistribution** funktioner som liknar godkännandet före driftsättningen, men som inträffar omedelbart efter driftsättningssteget, det vill säga innan någon provning utförs, jämfört med godkännandet före driftsättningen, som görs när all testning är slutförd.

      * **Hoppa över ändringar i belastningsutjämnaren** hoppar över ändringarna.
   1. Välj **Dispatcher-konfiguration** för Stage. Ange sökvägen och välj åtgärd från **Typ** och klicka **Lägg till bana**. Du kan ange upp till 100 sökvägar per miljö.

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. Välj **Distributionsalternativ** för produktion. Nu definierar du parametrarna som styr produktionsdistributionen.

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      De tre tillgängliga alternativen är följande:

      * **Använd Go Live Approval** - En distribution måste godkännas manuellt av en företagsägare, projektledare eller driftsättningshanterare via [!UICONTROL Cloud Manager] Gränssnitt.

      * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

         >[!NOTE]
         >If **Schemalagd** om du väljer det här alternativet kan du schemalägga din produktionsdistribution till pipeline **efter** distributionen av scenen (och **Använd GoLive för godkännande**, om detta har aktiverats) för att vänta på att ett schema ska anges. Användaren kan också välja att köra produktionsdistributionen direkt.
         >
         >Se [Distribuera koden](deploying-code.md), för att ställa in distributionsschemat eller köra produktionen direkt.

         * **Använd CSE-översikt** - En CSE håller på att starta driftsättningen. Under pipeline-konfiguration eller redigering när CSE Oversight är aktiverat kan Distributionshanteraren välja:

            * **Alla ärenden**: refererar till en tillgänglig CSE
            * **Mitt ärende**: avser en specifik CSE som tilldelats kunden eller deras säkerhetskopia, om CSE-enheten är utanför kontoret
   1. Konfigurera **Dispatcher Configurations** för produktion. Ange sökvägen och välj åtgärd från **Typ** och klicka **Lägg till bana**. Du kan ange upp till 100 sökvägar per miljö.

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      Som distributionshanterare kan du konfigurera en uppsättning innehållssökvägar som antingen **ogiltigförklarad** eller **tömd** från AEM Dispatcher-cachen för publiceringsinstanser när du ställer in eller redigerar pipeline.

      Du kan konfigurera en separat uppsättning sökvägar för Stage- och Production-distribution. Om den är konfigurerad kommer dessa cacheåtgärder att utföras som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM standard-Dispatcher-beteende - invalidate utför en cacheogiltigförklaring, på samma sätt som när innehåll aktiveras från författaren till publiceringen. rensning utför en cacheborttagning.

      I allmänhet är det bättre att använda åtgärden invalidate, men det kan finnas fall där det krävs tömning, särskilt när du använder AEM HTML Client Libraries.

      >[!NOTE]
      >
      >Se [Dispatcher - översikt](dispatcher-configurations.md) få mer information om Dispatcher-cachning.





1. Klicka på **Fortsätt** när du har valt alla alternativ.

1. Välj alternativ på **Scentestning** steg. Du kan konfigurera *AEM Sites* och *AEM Assets* Prestandatestning, beroende på vilka produkter du har licensierat. Se [Prestandatestning](understand-your-test-results.md#performance-testing) för mer information.

   1. Välj alternativ bland **Platsinnehållsleverans/distribuerad lastvikt**. Se [AEM Sites i prestandatestning](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites) för mer information.

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. Välj alternativ bland **Distribution av prestandatestning av resurser**. Se [AEM Assets i prestandatestning](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets) för mer information.

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. Klicka på **Spara** för att lägga till produktionsflöde.

### Redigera en produktionspipeline {#editing-prod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Programöversikt** sida.

Följ stegen nedan för att redigera den konfigurerade pipeline:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Redigera**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. The **Redigera produktionspipeline** visas.

   1. The **Konfiguration** kan du uppdatera **Pipelinenamn**, **Databas**, **Git-gren**, **Utlösare för distribution**, **Beteende vid fel i viktiga mått**, **Distributionsalternativ** och **Dispatcher Configurations**.

      >[!NOTE]
      >Se [Lägga till och hantera databaser](/help/using/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.


   1. The **Scentestning** -fliken ger dig ett alternativ att välja om dina alternativ från **Platsinnehållsleverans/distribuerad lastvikt** och **Distribution av prestandatestning av resurser**.

1. Klicka på **Uppdatera** när du är klar med redigeringen.

### Ytterligare produktionsförloppsåtgärder {#additional-prod-actions}

#### Köra en produktionspipeline {#run-prod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### Ta bort en produktionspipeline {#delete-prod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

   >[!NOTE]
   >En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via **Ta bort** från Pipeline-kortet.

## Icke-produktion och endast kodkvalitet, rörledningar

Förutom den huvudsakliga rörledningen som distribuerar till scenen och produktionen kan kunderna även lägga upp ytterligare rörledningar, så kallade **Icke-produktionsförlopp**. Dessa pipelines kör alltid stegen för bygg- och kodkvalitet. De kan också distribuera till Adobes miljö för hanterade tjänster.

## Videosjälvstudiekurs {#video-tutorial-two}

### Cloud Manager - endast icke-produktion- och kodkvalitet - pipelines {#non-prod-video}

Rörledningar för komprimerad/cd-produktion delas upp i två kategorier, nämligen pipelines för kodkvalitet och distributionsrörledningar. Kodkvalitetsledningarna genererar all kod från en Git-gren och utvärderas mot Cloud Managers skanning av kodkvalitet.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### Lägga till en icke-produktionspipeline {#add-non-production-pipeline}

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Öppna **Pipelines** från startskärmen i Cloud Manager. Klicka på **+Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **Lägg till icke-produktionsförlopp**  visas. Välj den typ av pipeline som du vill skapa, antingen **Kodkvalitetspipeline** eller **Distributionsförlopp**.

   Dessutom kan du konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. Den nyligen skapade icke-produktionsflödet visas nu i **Pipelines** kort.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en icke-produktionspipeline {#editing-nonprod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Förloppskort** från **Programöversikt** sida.

Följ stegen nedan för att redigera den konfigurerade icke-produktionsflödet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Välj icke-produktionsflödet och klicka på **...**. Klicka på **Redigera**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. The **Redigera produktionspipeline** visas där du kan uppdatera **Pipelinenamn**, **Databas**, **Git-gren**, **Utlösare för distribution** och **Beteende vid fel i viktiga mått**.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >Se [Lägga till och hantera databaser](/help/using/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   Du kan tilldela följande distributionsutlösare för att starta pipelinen:

   * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
   * **Vid Git-ändringar** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

   Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna. Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Klicka på **Uppdatera** när du är klar med redigeringen av icke-produktionsflödet.

### Ytterligare icke-produktionsförloppsindikatorer {#additional-nonprod-actions}

#### Köra en icke-produktionspipeline {#run-nonprod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/nonprod-run1.png)

#### Ta bort en icke-produktionspipeline {#delete-nonprod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/using/assets/configure-pipelines/nonprod-delete.png)


## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Se [Distribuera koden](deploying-code.md) för mer information.
