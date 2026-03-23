---
title: Lägg till en icke-produktionspipeline
description: Lär dig hur du använder Cloud Manager för att skapa och konfigurera rörledningar för icke-produktion för att distribuera koden.
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 57de7b00b382e4fb65ad3e03948960022ec02de1
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---

# Lägg till en icke-produktionspipeline {#configuring-non-production-pipelines}

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

## Lägg till en ny icke-produktionspipeline {#add-non-production-pipeline}

När du har konfigurerat ett program och har minst en miljö med Cloud Manager UI kan du lägga till icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välj rätt organisation och program.

1. Gå till Pipelines-kortet från Cloud Manager hemskärm. Klicka på **Lägg till** och välj sedan **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionspipeline** väljer du den typ av pipeline som du vill skapa, något av följande:

   * **Kodkvalitetspipeline** - Skapar en pipeline som bygger koden, kör enhetstester och utvärderar kodkvaliteten utan att distribuera den till någon miljö.
   * **Distributionspipeline** - Skapar en pipeline som bygger koden, kör enhetstester, utvärderar kodkvaliteten och distribuerar till en miljö.

   ![Välj pipeline-typ](/help/using/assets/add-non-production-pipeline-cm-ams.png)

>[!BEGINTABS]

>[!TAB Kodkvalitetspipeline - fliken Konfiguration]

| Avsnitt | Alternativ | Beskrivning |
| --- | --- | --- |
| **Pipelinekonfiguration** | **Pipelinenamn som inte är i produktion** | Ange en beskrivning av din pipeline i fältet **Namn på icke-produktionsförlopp**. |
|  | **Testar** | Synlig endast när du redigerar en icke-produktionspipeline.<br>Gränssnittet visar testkategorierna som pipeline kör som en del av kodkvalitetsvalideringen.<ul><li>**Statisk kodtestning** - Analyserar koden för problem med kvalitet och korrekthet.<li>**Load/Performance Testing** - Utvärderar prestandarelaterat beteende som en del av pipeline-testningen.<li>**Säkerhetstestning** - Kontrollerar kod- och pipeline-utdata för säkerhetsrelaterade problem. |
| **Distributionsalternativ** | **Utlösare för distribution** | <ul><li>**Manuell** - Du kan starta pipelinen manuellt.<li>**Vid Git-ändringar** - Startar pipelinen när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov. |
|  | **Beteende vid viktiga måttfel** | <ul><li>**Fråga varje gång** - Det här beteendet är standardinställningen och kräver manuell åtgärd vid viktiga fel.<li>**Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Det emulerar i stort sett en användare som manuellt avvisar varje fel.<li>**Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Det emulerar i stort sett en användare som manuellt godkänner varje fel.</li></ul> |
|  | Kryssrutan **Godkänn efter scendistribution** | Synlig endast när du redigerar en icke-produktionspipeline.<br>Välj det här alternativet om du vill kräva godkännande efter distributionen till scenmiljön innan pipeline kan fortsätta. Om det här alternativet inte är markerat fortsätter pipelinen baserat på det konfigurerade beteendet. |

>[!TAB Distributionspipeline - fliken Konfiguration]

| Avsnitt | Alternativ | Beskrivning |
| --- | --- | --- |
| **Pipelinekonfiguration** | **Pipelinenamn som inte är i produktion** | Ange en beskrivning av din pipeline i fältet **Namn på icke-produktionsförlopp**. |
|   | **Kvalificerad distributionsmiljö** | Om din pipeline är en distributionsprocess måste du välja vilka miljöer Cloud Manager distribuerar koden i. |
|   | **Testar** | Synlig endast när du redigerar en icke-produktionspipeline.<br>Gränssnittet visar testkategorierna som pipeline kör som en del av kodkvalitetsvalideringen.<ul><li>**Statisk kodtestning** - Analyserar koden för problem med kvalitet och korrekthet.<li>**Load/Performance Testing** - Utvärderar prestandarelaterat beteende som en del av pipeline-testningen.<li>**Säkerhetstestning** - Kontrollerar kod- och pipeline-utdata för säkerhetsrelaterade problem.</li></ul> |
| **Distributionsalternativ** | **Utlösare för distribution** | <ul><li>**Manuell** - Du kan starta pipelinen manuellt.<li>**Vid Git-ändringar** - Startar pipelinen när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov. |
|   | **Beteende vid viktiga måttfel** | <ul><li>**Fråga varje gång** - Standardinställningen och uppmanar användaren att bestämma hur ett viktigt mätvärde ska fortsätta när det inte fungerar.<li>**Misslyckades omedelbart** - pipelinen avbryts när ett viktigt mätvärde misslyckas. Det emulerar i princip en användare som manuellt avvisar varje fel.<li>**Fortsätt omedelbart** - pipelinen fortsätter automatiskt när ett viktigt mätvärde misslyckas. Det emulerar i princip en användare som manuellt godkänner varje fel.</li></ul> |
|  | Kryssrutan **Godkänn efter scendistribution** | Synlig endast när du redigerar en icke-produktionspipeline.<br>Välj det här alternativet om du vill kräva godkännande efter distributionen till scenmiljön innan pipeline kan fortsätta. Om det här alternativet inte är markerat fortsätter pipelinen baserat på det konfigurerade beteendet. |
|  | Kryssrutan **Hoppa över ändringar av belastningsutjämnare** | Välj det här alternativet om du inte vill att pipeline ska kunna göra belastningsutjämningsändringar under distributionen. |
|  | **Dispatcher-konfiguration** | Rollen **Distributionshanteraren** kan konfigurera en uppsättning innehållssökvägar som antingen är ogiltiga eller tömda från AEM Dispatcher-cachen när en pipeline körs. Dessa cacheåtgärder utförs som en del av distributionssteget, precis efter att innehållspaket har distribuerats. De här inställningarna använder AEM Dispatcher standardbeteende. Så här konfigurerar du `Dispatcher`:<ul><li>Under **PATH** anger du en innehållssökväg som du vill att pipelinen ska tömmas eller göras ogiltig.<li>Under **TYP** väljer du vilken åtgärd som ska utföras på sökvägen.<ul><li>**Rensa** - Utför en cacheborttagning på den angivna sökvägen.</li><li>**Invalidera** - Utför en cacheogiltigförklaring, ungefär som när innehåll aktiveras från en redigeringsinstans till en publiceringsinstans.</li><li>Klicka på **Lägg till sökväg** för att lägga till den angivna sökvägen. Du kan lägga till upp till 100 sökvägar per miljö.</li></ul> |
| **Rörledning** | Kryssrutan **Experience Audit** | Välj det här alternativet om du vill inkludera ett Experience Audit-steg i pipeline. När det här alternativet är aktiverat innehåller pipeline steget Experience Audit efter fliken Source Code. |

>[!ENDTABS]

1. Klicka på **Fortsätt** i det nedre högra hörnet av dialogrutan **Lägg till icke-produktionsförlopp** .
1. Välj den typ av kod som pipeline är konfigurerad för att bygga och distribuera.

>[!BEGINTABS]

>[!TAB Source Code tab - Full Stack Code]

Distribuerar hela AEM-programmet, inklusive programkod och som standard webbnivåkonfiguration.

| Avsnitt | Alternativ | Beskrivning |
| --- | --- | --- |
| **Source-kod** | **Databas** | I listrutan väljer du Git-databasen som pipelinen använder som källa. Cloud Manager skapar kod från den databas du väljer här. |
|   | **Git-grenen** | I listrutan väljer du vilken gren i den valda databasen som pipeline ska bygga från. Standardvärdet är `main`. I pipeline används den valda grenen som källa för bygge och distribution. Om det behövs klickar du på **Uppdatera** för att uppdatera listan över tillgängliga grenar för den valda databasen. Använd det här alternativet om en nyligen skapad gren inte visas i listan. |
|   | **Skapa strategi** | <ul><li>**Fullständigt bygge** - Bygger alla moduler i databasen varje gång<li>BETA **Smart Build** - Skapar endast moduler som har ändrats sedan den senaste implementeringen.<br>Läs mer om [att använda Smart Build i en icke-produktionsprocess](#about-smart-build).</li></ol>**Viktigt**: Smart Build är bara tillgängligt för pipelines för kodkvalitet och distributionspipelines för fullständig stackkod för Dev. |
|   | Kryssrutan **Ignorera webbnivåkonfiguration** | Välj det här alternativet om du vill hoppa över distributionen av webbnivåkonfigurationen i en fullständig stackkodspipeline. Låt alternativet vara avmarkerat för att distribuera webbnivåkonfigurationen tillsammans med pipeline-koden. |
| **Rörledning** | Kryssrutan **Experience Audit** | Välj det här alternativet om du vill inkludera ett Experience Audit-steg i pipeline. När det här alternativet är aktiverat innehåller pipeline steget Experience Audit efter fliken Source Code. |

>[!TAB Source Code - Web Tier Config]

Distribuerar endast webbnivåkonfiguration, t.ex. Dispatcher-egenskaper som används för att lagra, bearbeta och leverera webbsidor till klienten. När du väljer **Webbnivåkonfiguration** skapar Cloud Manager en pipeline som är dedikerad till distribution av webbnivåkonfiguration.

Om det redan finns en fullständig stackpipeline visar Cloud Manager ett meddelande om att den befintliga fullständiga stackpipelinen ignoreras i konfigurationen av webbnivån när en konfigurationspipeline för webbskikt skapas. När du har skapat konfigurationsflödet för webbnivån hanterar Cloud Manager distributioner av webbnivåkonfigurationer via den pipeline som ingår i stacken i stället för via den fullständiga stackpipeline.

| Avsnitt | Alternativ | Beskrivning |
| --- | --- | --- |
| **Source-kod** | **Databas** | I listrutan väljer du den Git-databas som innehåller webbnivåkonfigurationen. |
|   | **Git-grenen** | Välj den gren i den valda databasen som Cloud Manager använder för distributionen. Om det behövs klickar du på **Uppdatera** för att uppdatera listan över tillgängliga grenar för den valda databasen. Använd det här alternativet om en nyligen skapad gren inte visas i listan. |
|   | **Kodplats** | Ange sökvägen i den valda databasen som innehåller den webbskiktskonfiguration som ska distribueras. Standardplatsen är databasroten (`/`). |

>[!ENDTABS]

1. Klicka på **Spara**.

## Om att använda Smart Build i en icke-produktionsprocess{#about-smart-build}

**Smart Build** i Cloud Manager är en optimerad byggstrategi för icke-produktionspipelines. Smart Build minskar byggtiden genom att cache-lagra moduler och återskapa endast de moduler som har ändrats sedan den senaste körningen. Oförändrade moduler återanvänds från cacheminnet, medan endast ändrade moduler och deras beroenden återskapas, vilket förbättrar effektiviteten för iterativa utvecklingsarbetsflöden.

Smart Build är för närvarande endast tillgängligt för följande:

* Kodkvalitetsledningar.
* Utveckla rörledningar för driftsättning i högklasser.

>[!NOTE]
>
>Den första körningen efter aktiveringen av Smart Build fungerar som en fullständig version eftersom cachen är tom.

Smart Build rekommenderas när du har följande:
* Du utvecklar och implementerar ofta inkrementella förändringar.
* Ditt projekt innehåller flera Maven-moduler.
* Fullversioner tar lång tid.

Smart Build är inte alltid idealiskt när du har följande:
* Din version är starkt beroende av plugin-program som utför åtgärder utanför Maven beroendediagram.
* Du måste verifiera alla versioner av varje körning.

### Förstå byggprestanda{#smart-build-performance}

Den prestandaökning som kan uppnås med Smart Build beror på flera faktorer, bland annat följande:

* Antalet moduler i projektet.
* Kodändringarnas frekvens och omfattning.
* Distributionen av beroenden mellan moduler.

I allmänhet förbättras projekt med många oberoende moduler mest.

### Cacheavanmälan per modul{#smart-build-cache-optout}

Smart Build har finkornig kontroll som gör att du kan inaktivera cachelagring för specifika moduler. Den här funktionen är användbar när vissa moduler:

* Använd plugin-program som `exec-maven-plugin` eller `maven-antrun-plugin`.
* Utför filåtgärder som inte spåras av Maven-beroenden.
* Producera inkonsekventa resultat vid cachelagring.

### Inaktivera cachelagring för en modul{#smart-build-disable-caching}

Du kan lägga till följande egenskap i den påverkade modulens `pom.xml`:

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

Den här syntaxen tvingar modulen att återskapa varje pipeline-körning medan andra moduler fortfarande har nytta av cachelagring.

### Begränsningar och överväganden när Smart Build används{#smart-build-limitations}

Tänk på följande när du använder Smart Build:

* Smart Build bygger på Maven-beroendeanalys.
* Ändringar utanför beroendediagrammet kan inte utlösa rekonstruktioner.
* Vissa plugin-program kanske inte är helt kompatibla med cachning.
* Du kan när som helst växla tillbaka till **Fullständigt bygge** genom att redigera icke-produktionsflödet.

Om du stöter på oväntat byggbeteende bör du inaktivera cachelagring för specifika moduler eller tillfälligt byta din byggstrategi till **Fullständigt bygge**.

### Felsöka problem med Smart Build{#smart-build-troubleshoot}

| Problem | Föreslagna lösningar |
| --- | --- |
| Byggresultaten är inkonsekventa | ・ Inaktivera cachelagring för berörda moduler.<br> ・ verifiera plugin-programmets beteende (särskilt `exec`/`antrun` plugin-program). |
| Ingen prestandaförbättring | ・ Kontrollera att flera körningar har utförts (cacheuppvarning).<br> ・ Kontrollera om de flesta moduler ändras ofta. |
| Oväntade artefakter eller saknade ändringar | ・ Kontrollera om ändringarna ligger utanför Maven-beroendespårning.<br> ・ Använd **Fullständigt bygge** för verifiering. |

Se [Lägg till en icke-produktionsprocess](#add-non-production-pipeline) om du vill aktivera Smart Build.



<!-- 
1. If you chose to add a **Deployment Pipeline**, select the target deployment environment from the **Eligible Deployment Environments** dropdown.

1. Provide the repository where the pipeline should retrieve the code.

   * **Repository** - Defines from which Git repo that the pipeline should retrieve the code.
   * **Git Branch** - Defines from which branch in Git that the selected pipeline should retrieve the code.

1. Define your deployment options.

   1. Under **Deployment Trigger**, define what event activates the pipeline.

      * **Manual** - Lets you manually start the pipeline.
      * **On Git Changes** - Starts the pipeline when commits are added to the configured Git branch. With this option, you can still start the pipeline manually, as required.

   1. For deployment pipelines, under **Important Metric Failures Behavior**, define the behavior of the pipeline when an important failure is encountered in any of the quality gates.

       * **Ask every time** - The default setting and requires manual intervention on any important failure.
       * **Fail Immediately** - The pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
       * **Continue Immediately** - The pipeline proceeds automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

   1. **Dispatcher Configuration** - The **Deployment Manager** role can configure a set of content paths that are either invalidated or flushed from the AEM Dispatcher cache when a pipeline is run. These cache actions are performed as part of the deployment pipeline step, just after any content packages are deployed. These settings use standard AEM Dispatcher behavior. To configure:

      1. Under **PATH** provide a content path.
      1. Under **TYPE**, select the action to be taken on that path.

         * **Flush** - Perform a cache deletion.
         * **Invalidate** - Perform a cache invalidation, similar to when content is activated from an authoring instance to a publishing instance.
         
      1. Click **Add Path** to add your specified path. You can add up to 100 paths per environment.

1. Click **Save**.
-->

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline kan du distribuera koden. Mer information finns i [Koddistribution](/help/using/code-deployment.md).

## Videosjälvstudie {#video-tutorial}

Den här videon ger en översikt över processen att skapa pipeline, som beskrivs i det här dokumentet.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)
