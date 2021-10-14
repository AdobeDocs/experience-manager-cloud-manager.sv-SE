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
source-git-commit: e748383fb627ac6ecf69f1b6e313bb5710fbf444
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Konfigurera CI/CD-pipeline {#configure-your-ci-cd-pipeline}

>[!NOTE]
>Mer information om hur du konfigurerar CI/CD-pipeline för Cloud Manager på AEM as a Cloud Service finns i [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager).

På följande sida beskrivs hur du konfigurerar **pipeline**. Mer konceptuell information om hur pipeline fungerar finns i [CI/CD pipeline overview](ci-cd-pipeline.md).

## Videosjälvstudiekurs {#video-tutorial-one}

### Konfigurera pipeline i Cloud Manager {#config-pipeline-video}

CI/CD Production Pipeline-konfigurationen definierar den utlösare som initierar pipelinen, parametrar som styr produktionsdistributionen och parametrar för prestandatestning.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## Förstå flödet {#understanding-the-flow}

Du kan konfigurera pipeline från panelen **Pipeline-inställningar** i [!UICONTROL Cloud Manager].

Distributionshanteraren ansvarar för att ställa in pipeline. När du gör det väljer du först en gren i **Git-databasen**. Pipeline-konfigurationen består av:

* definiera den utlösare som ska starta pipelinen.
* definiera parametrarna som styr produktionsdistributionen.
* konfigurera prestandatestparametrarna.

## Konfigurera pipeline {#setting-up-the-pipeline}

>[!CAUTION]
>
>Det går inte att konfigurera pipelinen förrän Git-databasen har minst en gren och [Programinställningar](setting-up-program.md) är slutförda.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan ändra pipeline-inställningarna efter den första konfigurationen.

### Konfigurera förloppsinställningarna från [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

När du har konfigurerat ditt program med [!UICONTROL Cloud Manager]-gränssnittet är du redo att konfigurera din pipeline.

Följ de här stegen för att konfigurera beteendet och inställningarna för din pipeline:

1. Klicka på **Konfigurera pipeline** för att konfigurera och konfigurera din pipeline.

   ![](assets/Setup-Pipeline.png)

1. Skärmen **Setup Pipeline** visas.

   Med guiden i tre steg kan du konfigurera din **gren**, **miljö** och **testmiljö**.
Välj din Git-gren och klicka på **Nästa**.

   >[!NOTE]
   >
   >Förgreningar som hittas i Git-databasen är länkade till ditt program.


1. Gå till fliken **Miljöer** och välj alternativen **Stage** och **Produktion**.

   Du kan definiera utlösaren för att starta pipelinen:

   * **På Git Changes**  - startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.
   * **Manuell**  - använd gränssnittet för att starta pipelinen manuellt.

   Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel inträffar i någon av kvalitetsportarna, till exempel kodkvalitet, säkerhetstestning och prestandatestning.

   Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

* **Fråga varje gång**  - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
* **Avbryt omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
* **Godkänn omedelbart**  - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

   Nu definierar du parametrarna som styr produktionsdistributionen. De tre tillgängliga alternativen är följande:

* **Använd Go Live Approval**  - en distribution måste godkännas manuellt av en företagsägare, projektledare eller driftsättningshanterare via  [!UICONTROL Cloud Manager] användargränssnittet.
* **Använd CSE Oversight**  - en CSE är engagerad för att starta distributionen. Under pipeline-konfiguration eller redigering när CSE Oversight är aktiverat kan Distributionshanteraren välja:

   * **Alla fall**: refererar till en tillgänglig CSE
   * **Mitt fall**: avser en specifik CSE som tilldelats kunden eller deras säkerhetskopia, om CSE-enheten är utanför kontoret

* **Schemalagd**  - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

>[!NOTE]
>Om du väljer alternativet **Schemalagd** kan du schemalägga din produktionsdistribution till pipelinen **efter** scendistributionen (och **Använd GoLive Approval**, om detta har aktiverats) för att vänta på att ett schema ska anges. Användaren kan också välja att köra produktionsdistributionen direkt.
>
>Se [**Distribuera koden**](deploying-code.md) för att ställa in distributionsschemat eller köra produktionen direkt.

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>Alternativet **Använd CSE Oversight** är inte tillgängligt för alla kunder.

**Godkänn efter scendistribution**

Det finns ett valfritt steg **Godkänn efter scendistributionen** som kan konfigureras i produktionspipelinen.
Detta aktiveras i ett nytt alternativ på **skärmen Redigera pipeline**:

![](assets/post_deployment1.png)

Det visas sedan som ett separat steg under pipeline-körningen:

![](assets/post_deployment2.png)

>[!NOTE]
>
>**Godkänn efter** driftsättningsfunktioner som liknar godkännandet före driftsättningen, men inträffar omedelbart efter driftsättningssteget, det vill säga innan testningen är klar, jämfört med godkännandet före driftsättningen, som görs när all testning är klar.

**Dispatcher Invalidation**

Som distributionshanterare kan du konfigurera en uppsättning innehållssökvägar som antingen **ogiltigförklaras** eller **tömts** från AEM Dispatcher-cachen för publiceringsinstanser när du konfigurerar eller redigerar pipeline.

Du kan konfigurera en separat uppsättning sökvägar för Stage- och Production-distribution. Om den är konfigurerad kommer dessa cacheåtgärder att utföras som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM standard-Dispatcher-beteende - invalidate utför en cacheogiltigförklaring, på samma sätt som när innehåll aktiveras från författaren till publiceringen. rensning utför en cacheborttagning.

I allmänhet är det bättre att använda åtgärden invalidate, men det kan finnas fall där det krävs tömning, särskilt när du använder AEM HTML Client Libraries.

>[!NOTE]
>
>Mer information om Dispatcher-cachning finns i [Dispatcher Overview](dispatcher-configurations.md).

Följ stegen nedan för att konfigurera Dispatcher Invalidations:

1. Klicka på **Konfigurera** under rubriken Dispatcher Configuration

   ![](assets/image2018-8-7_14-53-24.png)

1. Ange sökvägen, välj åtgärden från **Skriv** och klicka på **Lägg till**. Du kan ange upp till 100 sökvägar per miljö. När du har lagt till sökvägarna klickar du på **Använd**.

   ![](assets/image2018-8-7_14-58-11.png)

1. När du är tillbaka på sidan **Inställningar för pipeline** visas en uppdaterad sammanfattning av valen.

   Klicka på **Spara** om du vill behålla den här konfigurationen.

   ![](assets/image2018-8-7_15-4-30.png)

1. Gå till fliken **Testning** för att definiera testvillkoren för programmet. Du kan nu konfigurera prestandatestparametrarna.

   Du kan konfigurera *AEM Sites* och *AEM Assets* Performance Testing, beroende på vilka produkter du har licensierat. Mer information finns i [Prestandatestning](understand-your-test-results.md#performance-testing).

1. Klicka på **Spara** för att slutföra konfigurationen av pipeline-processen.

   >[!NOTE]
   >När du har konfigurerat pipelinen kan du dessutom fortfarande redigera inställningar för den med **Inställningar för produktionspipeline** i [!UICONTROL Cloud Manager]-gränssnittet.

   ![](assets/Production-Pipeline.png)


## Icke-produktion och endast kodkvalitet, rörledningar

Förutom den huvudsakliga rörledningen som distribueras till stadium och produktion kan kunderna lägga upp ytterligare rörledningar, som kallas **icke-produktionsförlopp**. Dessa pipelines kör alltid stegen för bygg- och kodkvalitet. De kan också distribuera till Adobes miljö för hanterade tjänster.

## Videosjälvstudiekurs {#video-tutorial-two}

### Cloud Manager - endast icke-produktion- och kodkvalitet - pipelines {#non-prod-video}

Rörledningar för komprimerad/cd-produktion delas upp i två kategorier, nämligen pipelines för kodkvalitet och distributionsrörledningar. Kodkvalitetsledningarna genererar all kod från en Git-gren och utvärderas mot Cloud Managers skanning av kodkvalitet.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### Lägga till en icke-produktionspipeline {#add-non-production-pipeline}

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Gå till **Pipelines**-kortet från startskärmen i Cloud Manager. Klicka på **+Lägg till** och välj **Lägg till icke-produktionsförlopp**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **Dialogrutan Lägg till icke-produktionsförlopp**  visas. Välj den typ av pipeline som du vill skapa, antingen **Kodkvalitetspipeline** eller **Distributionspipeline**.

   Dessutom kan du ställa in **Distributionutlösare** och **Viktigt felbeteende** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. Den nyligen skapade icke-produktionspipelinen visas nu på **pipelines**-kortet.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till**  - tillåter tillägg av en ny pipeline.
   * **Åtkomst till replikinformation**  - gör att användaren kan få den information som behövs för att komma åt Cloud Manager Git-databasen.
   * **Lär dig mer**  - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en icke-produktionspipeline {#editing-nonprod-pipeline}

Du kan redigera pipelinekonfigurationerna från sidan **Pipelines card** från **Program Overview**.

Följ stegen nedan för att redigera den konfigurerade icke-produktionsflödet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Markera produktionsflödet och klicka på **..**. Klicka på **Redigera**, vilket visas i bilden nedan.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. Dialogrutan **Redigera produktionspipeline** innehåller information om hur du kan uppdatera **pipelinenamnet**, **databasen**, **Git-grenen**, **distributionsutlösare** och **Viktiga mätningsfel havior**.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).


1. Klicka på **Uppdatera** när du är klar med redigeringen av produktionsflödet.


## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Mer information finns i [Distribuera koden](deploying-code.md).
