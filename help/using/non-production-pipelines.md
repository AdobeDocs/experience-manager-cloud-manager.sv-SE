---
title: Konfigurera icke-produktionsförlopp
description: Lär dig hur du använder Cloud Manager för att skapa och konfigurera rörledningar för icke-produktion för att distribuera koden.
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Konfigurera icke-produktionsrörledningar {#configuring-non-production-pipelines}

Lär dig hur du använder Cloud Manager för att skapa och konfigurera rörledningar för icke-produktion för att distribuera koden. Om du först vill ha en mer konceptuell översikt över hur rörledningar fungerar i Cloud Manager kan du läsa [CI/CD-pipelines](/help/overview/ci-cd-pipelines.md).

## Ökning {#overview}

Med **pipelines** i [!UICONTROL Cloud Manager] kan **Distributionshanteraren** skapa två olika typer av pipelines.

* **Produktionspipelines** - En produktionspipeline är en specialbyggd pipeline som består av en serie samordnade steg för att ta källkod hela vägen in i produktionen.
* **Icke-produktionsförlopp** - En icke-produktionsförlopp används främst för att köra kodkvalitetsgenomsökningar eller för att distribuera källkod till en utvecklingsmiljö.

Detta dokument fokuserar på icke-produktionsrörledningar. Mer information om hur du konfigurerar produktionspipelines finns i dokumentet [Konfigurera produktionspipelines](/help/using/production-pipelines.md).

Det finns två typer av icke-produktionsrörledningar:

* **Kodkvalitetsförgreningar** - Dessa kör kodkvalitet genom att skanna koden i en Git-gren och kör stegen för bygg- och kodkvalitet.
* **Distributionspipeliner** - Förutom att utföra steg för bygg- och kodkvalitet, som till exempel pipelines för kodkvalitet, distribuerar dessa pipelines även koden till en icke-produktionsmiljö.

>[!NOTE]
>
>Det går inte att konfigurera en pipeline förrän dess associerade Git-databas har minst en gren och [programkonfigurationen](/help/getting-started/program-setup.md) är klar. Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/managing-code/managing-repositories.md).

## Lägg till en icke-produktionspipeline {#add-non-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med Cloud Manager UI är du redo att lägga till en icke-produktionsprocess genom att följa de här stegen.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välj rätt organisation och program.

1. Gå till Pipelines-kortet från Cloud Manager hemskärm. Klicka på **Lägg till** och välj sedan **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionspipeline** väljer du den typ av pipeline som du vill skapa, antingen en **kodkvalitetspipeline** eller en **distributionspipeline**.

   ![Välj pipeline-typ](/help/assets/configure-pipelines/add-non-production-pipeline.png)

1. Ange en beskrivning av din pipeline i fältet **Namn på icke-produktionsförlopp**.

1. Om du väljer att lägga till en **distributionspipeline** väljer du måldistributionsmiljön i listrutan **Godtagbara distributionsmiljöer**.

1. Ange den databas där pipeline ska hämta koden.

   * **Databas** - Definierar från vilken Git-repo som pipelinen ska hämta koden.
   * **Git-grenen** - Definierar från vilken gren i Git som den valda pipelinen ska hämta koden.

1. Definiera distributionsalternativen.

   1. Under **Distributionutlösare** definierar du vilken händelse som aktiverar pipelinen.

      * **Manuell** - Du kan starta pipelinen manuellt.
      * **Vid Git-ändringar** - Startar pipelinen när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   1. För distributionspipelines definierar du, under **Beteende för viktiga mätfel**, beteendet för pipelinen när ett viktigt fel påträffas i någon av kvalitetsportarna.

      * **Fråga varje gång** - Standardinställningen och kräver manuell åtgärd vid viktiga fel.
      * **Misslyckades omedelbart** - pipelinen avbryts när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt avvisar varje fel.
      * **Fortsätt omedelbart** - pipelinen fortsätter automatiskt när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt godkänner varje fel.

   1. **Dispatcher-konfiguration** - Rollen **Distributionshanteraren** kan konfigurera en uppsättning innehållssökvägar som antingen är ogiltiga eller tömda från AEM Dispatcher-cache när en pipeline körs. Dessa cacheåtgärder utförs som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM Dispatcher standardbeteende. Konfigurera:

      1. Under **PATH** anger du en innehållssökväg.
      1. Under **TYP** väljer du vilken åtgärd som ska utföras på sökvägen.

         * **Rensa** - Utför en cacheborttagning.
         * **Invalidera** - Utför en cacheogiltigförklaring, ungefär som när innehåll aktiveras från en redigeringsinstans till en publiceringsinstans.

      1. Klicka på **Lägg till sökväg** för att lägga till den angivna sökvägen. Du kan lägga till upp till 100 sökvägar per miljö.

1. Klicka på **Spara**.

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline kan du distribuera koden. Mer information finns i [Koddistribution](/help/using/code-deployment.md).

## Videosjälvstudie {#video-tutorial}

Den här videon ger en översikt över processen att skapa pipeline, som beskrivs i det här dokumentet.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)
