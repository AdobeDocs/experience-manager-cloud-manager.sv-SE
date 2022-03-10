---
title: Konfigurera icke-produktionsförlopp
description: Lär dig hur du använder Cloud Manager för att skapa och konfigurera rörledningar som inte är avsedda för produktion för att distribuera koden.
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 154b95e1b43717097b9ae9076a15792517dd613d
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Konfigurera icke-produktionsförlopp {#configuring-non-production-pipelines}

Lär dig hur du använder Cloud Manager för att skapa och konfigurera rörledningar som inte är avsedda för produktion för att distribuera koden. Om du först vill ha en mer begreppsmässig översikt över hur rörledningar fungerar i Cloud Manager kan du läsa [Översiktsdokumentation för CI/CD-pipeline.](ci-cd-pipeline.md)

>[!NOTE]
>
>Mer information om hur du konfigurerar CI/CD-pipelines för Cloud Manager på AEM as a Cloud Service finns i [AEMaaCS-dokumentationen.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html#using-cloud-manager)

## Översikt {#understanding-the-flow}

The **Distributionshanteraren** rollen ansvarar för att ställa in pipeline med **Pipelines** i [!UICONTROL Cloud Manager] Gränssnitt.

Du kan skapa två olika typer av rörledningar.

* **Produktionsförlopp** - En produktionsledning är en konstruerad rörledning som består av en serie samordnade steg för att ta källkod hela vägen in i produktionen.
* **Icke-produktionsförlopp** - Ett icke-produktionsflöde som främst används för att utföra kodkvalitetsinläsningar eller för att distribuera källkod till en utvecklingsmiljö.

Detta dokument fokuserar på icke-produktionsrörledningar. Mer information om hur du konfigurerar icke-produktionsrörledningar finns i dokumentet [Konfigurerar icke-produktionsförlopp.](configuring-non-production-pipelines.md)

Det finns två typer av icke-produktionsrörledningar:

* **Kodkvalitetsförlopp** - Dessa kör kodkvalitetskontroller i koden i en Git-gren och utför stegen för bygg- och kodkvalitet.
* **Distributionsförlopp** - Förutom att utföra steg för bygg- och kodkvalitet, som till exempel pipelines för kodkvalitet, distribuerar dessa pipelines koden till en icke-produktionsmiljö.

>[!NOTE]
>
>En pipeline kan inte konfigureras förrän dess associerade Git-databas har minst en gren och [programinställningar](setting-up-program.md) är klar. Se [Lägga till och hantera databaser](cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

## Videosjälvstudiekurs {#video-tutorial-two}

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

## Lägga till en icke-produktionspipeline {#add-non-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet i Cloud Manager är du redo att lägga till en icke-produktionsprocess genom att följa de här stegen.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välja lämplig organisation och lämpligt program.

1. Gå till Pipelines-kortet från startskärmen i Cloud Manager. Klicka på **Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. På **Konfiguration** -fliken i **Lägg till icke-produktionsförlopp** väljer du den typ av pipeline som du vill skapa, antingen en **Kodkvalitetspipeline** eller en **Distributionsförlopp**.


   ![Välj pipelinetyp](/help/using/assets/configure-pipelines/add-non-production-pipeline.png)

1. Ange en beskrivning av din pipeline i **Namn på icke-produktionsförlopp** fält.

1. Om du valde att lägga till en **Distributionsförlopp** väljer du måldistributionsmiljön i **Berättigade driftsättningsmiljöer** listruta.

1. Ange den databas där pipeline ska hämta koden.

   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.
   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.

1. Definiera distributionsalternativen.

   1. Under **Utlösare för distribution** definierar du vilken händelse som aktiverar pipelinen.

      * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
      * **Vid Git-ändringar** - Det här alternativet startar pipelinen när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.
   1. För distribution av rörledningar, under **Beteende vid viktiga måttfel** definierar du hur rörledningen fungerar när ett viktigt fel inträffar i någon av kvalitetsportarna.

      * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
      * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
      * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Klicka **Spara** för att spara ditt flöde.

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Se dokumentet [Distribuera koden](deploying-code.md) för mer information.
