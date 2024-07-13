---
title: Koddistribution
description: Lär dig hur du distribuerar kod och vad som händer i Cloud Manager när du gör det.
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: ab527beb706ab73a14cc933a3414873dee6b7a9e
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---


# Koddistribution {#code-deployment}

Lär dig hur du distribuerar kod och vad som händer i Cloud Manager när du gör det.

## Distribuera kod med Cloud Manager {#deploying-code-with-cloud-manager}

När du har konfigurerat produktionsflödet, inklusive de nödvändiga databaserna och miljöerna, är du redo att distribuera koden.

1. Klicka på **Distribuera** från Cloud Manager för att starta distributionsprocessen.

   ![Knappen Distribuera](/help/assets/Deploy1.png)

1. Skärmen **Pipeline Execution** visas. Klicka på **Skapa** för att starta processen.

   ![Knappen Skapa](/help/assets/Deploy2.png)

Byggprocessen startar koddistributionsprocessen med följande steg:

* Scendistribution
* Stage testing
* Produktionsdistribution

Du kan granska stegen från olika distributionsprocesser genom att visa loggar eller granska resultaten för att se testvillkoren.

## Distributionssteg {#deployment-steps}

Ett antal åtgärder inträffar under varje steg i distributionen, som beskrivs i det här avsnittet. I avsnittet [Information om distributionsprocess](#deployment-process) finns teknisk information om hur själva koden distribueras bakom scenerna.

### Steg för driftsättning {#stage-deployment}

Steg **Scendistribution** innehåller följande åtgärder:

* **Validering**: Detta steg säkerställer att pipeline är konfigurerad att använda de tillgängliga resurserna, t.ex. att den konfigurerade grenen finns och att miljöerna är tillgängliga.
* **Build &amp; Unit Testing**: Det här steget kör en innehållsstyrd byggprocess. Mer information finns i dokumentet [Build Environment](/help/getting-started/build-environment.md).
* **Kodsökning**: I det här steget utvärderas kvaliteten på programkoden. Mer information om testprocessen finns i dokumentet [Förstå testresultat](/help/using/code-quality-testing.md).
* **Distribuera till scenen**

![Scendistribution](/help/assets/Stage_Deployment1.png)

### Steg för testning {#stage-testing}

**Scentestningen** omfattar följande åtgärder:

* **Säkerhetstestning**: I det här steget utvärderas hur säkerhetseffekten av koden påverkar AEM. Mer information om testprocessen finns i dokumentet [Förstå testresultat](/help/using/code-quality-testing.md).
   * **Prestandatestning**: I det här steget utvärderas kodens prestanda. Mer information om testprocessen finns i [Förstå testresultat](/help/using/code-quality-testing.md).

### Produktionsdistributionssteg {#production-deployment}

Stegen **Produktionsdistribution** innehåller följande åtgärder:

* **Ansökan om godkännande**
   * Det här alternativet aktiveras när pipeline konfigureras.
   * Med det här alternativet kan du antingen schemalägga din produktionsdistribution eller klicka på **nu** för att köra produktionsdistributionen direkt.
* **Schemalägg produktionsdistribution**
   * Det här alternativet aktiveras när pipeline konfigureras.
   * Det schemalagda datumet och den schemalagda tiden anges i användarens tidszon.
     ![Schemalägg distribution](/help/assets/Production_Deployment1.png)
* **CSE-stöd** (om aktiverat)
* **Distribuera till produktion**

![Produktionsdistribution](/help/assets/Prod_Deployment1.png)

När distributionen är klar finns koden i målmiljön och du kan visa loggarna.

![Distributionen har slutförts](/help/assets/Production_Deployment2.png)

## Timeout {#timeouts}

Följande steg gör timeout om du väntar på användarfeedback:

| Steg | Timeout |
|--- |--- |
| Testning av kodkvalitet | 7 dagar |
| Säkerhetstestning | 7 dagar |
| Prestandatestning | 7 dagar |
| Ansökan om godkännande (steg) | 7 dagar |
| Ansökan om godkännande (produktion) | 14 dagar |
| Schemalägg produktionsdistribution | 14 dagar |
| Hanterad produktionsdistribution | 14 dagar |

## Information om distributionsprocess {#deployment-process}

Cloud Manager överför alla mål-/*.zip-filer som skapas i byggprocessen till en lagringsplats. Dessa artefakter hämtas från den här platsen under pipelinens distributionsfaser.

När Cloud Manager använder icke-produktionstopologier är målet att slutföra distributionen så snabbt som möjligt och artefakterna distribueras därför på alla noder samtidigt enligt följande:

1. Cloud Manager avgör om varje artefakt är ett AEM- eller dispatcherpaket.
1. Cloud Manager tar bort alla utskickare från belastningsutjämnaren för att isolera miljön under distributionen.

   * Om inget annat anges kan du hoppa över ändringar av belastningsutjämnaren i distributionen av utveckling och staging, dvs. för utvecklingsmiljön, koppla loss och bifoga steg i både icke-produktionspipelines och för produktionsflödet i mellanlagringsmiljön.

   ![Hoppa över belastningsutjämnare](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >Den här funktionen förväntas främst användas av 1-1-1-kunder.

1. Varje AEM-artefakt distribueras till varje AEM-instans via API:er för Package Manager, där paketberoenden avgör distributionsordningen.

   * Mer information om hur du kan använda paket för att installera nya funktioner, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll finns i dokumentet [Package Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)

   >[!NOTE]
   >
   >Alla AEM artefakter distribueras till både författaren och utgivaren. Körningslägena bör utnyttjas när nodspecifika konfigurationer krävs. Om du vill veta mer om hur körningslägena gör att du kan trimma AEM för ett visst ändamål kan du läsa avsnittet [Körningslägen i dokumentet Distribuera till AEM as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)

1. Dispatchartefakten distribueras till varje dispatcher enligt följande:

   1. Aktuella konfigurationer säkerhetskopieras och kopieras till en tillfällig plats.
   1. Alla konfigurationer tas bort utom de oföränderliga filerna. Mer information finns i dokumentet [Dispatcher Configurations](/help/getting-started/dispatcher-configurations.md). Detta rensar katalogerna för att säkerställa att inga överblivna filer lämnas kvar.
   1. Artefakten extraheras till katalogen `httpd`. Oändringsbara filer skrivs inte över. Alla ändringar du gör i oföränderliga filer i Git-databasen ignoreras vid distributionen. Dessa filer är viktiga för AMS-dispatcherramverket och kan inte ändras.
   1. Apache utför ett konfigurationstest. Om inga fel hittas läses tjänsten in igen. Om ett fel inträffar återställs konfigurationerna från en säkerhetskopia, tjänsten läses in igen och felet rapporteras tillbaka till Cloud Manager.
   1. Varje sökväg som anges i pipeline-konfigurationen görs ogiltig eller töms från dispatchercachen.

   >[!NOTE]
   >
   >Cloud Manager förväntar att dispatcherartefakten ska innehålla hela filuppsättningen. Alla konfigurationsfiler för dispatcher måste finnas i Git-databasen. Om filer eller mappar saknas kommer distributionen att misslyckas.

1. Efter den lyckade distributionen av alla AEM- och dispatcherpaket till alla noder läggs avsändarna tillbaka till belastningsutjämnaren och distributionen är klar.

   >[!NOTE]
   >
   >du kan hoppa över ändringar av belastningsutjämnare i utveckling och staging-distributioner, dvs. för utvecklingsmiljön, koppla loss och bifoga steg i både icke-produktionspipelines och för staging-miljön i produktionsflödet.

### Distribution till produktionsfas {#deployment-production-phase}

Processen för att distribuera till produktionstopologier skiljer sig något för att minimera påverkan för AEM besökare.

Produktionsinstallationer följer i allmänhet samma steg som ovan, men på ett rullande sätt:

1. Distribuera AEM som ska författas.
1. Koppla loss dispatcher1 från belastningsutjämnaren.
1. Distribuera AEM paket till publish1 och dispatcherns paket till dispatcher1 parallellt, tömma dispatchercachen.
1. Placera dispatcher1 i belastningsutjämnaren igen.
1. När dispatcher1 är tillbaka i tjänst frigör du dispatcher2 från belastningsutjämnaren.
1. Distribuera AEM paket för att publicera2 och dispatcherpaketet till dispatcher2 parallellt, tömma dispatchercachen.
1. Placera dispatcher2 i belastningsutjämnaren igen.

Den här processen fortsätter tills distributionen har nått alla utgivare och utgivare i topologin.

## Körningsläge för nödrörledning {#emergency-pipeline}

I kritiska situationer kan Adobe Managed Services-kunder behöva driftsätta kodändringar i sina scen- och produktionsmiljöer utan att vänta på att en fullständig testcykel från Cloud Manager ska köras.

För att åtgärda dessa situationer kan Cloud Manager produktionsflöde genomföras i nödläge. När det här läget används utförs inte stegen för säkerhets- och prestandatestning. Alla andra steg, inklusive konfigurerade godkännandesteg, körs som i det normala körningsläget för pipeline.

>[!NOTE]
>
>Funktionen för driftsättning av beredskapsled aktiveras program för program av Customer Success Engineers.

### Använda körningsläge för nödpipeline {#using-emergency-pipeline}

När du startar en körning av en produktionspipeline kan du starta körningen i normalt läge eller nödläge från en dialogruta om funktionen för körning av nödpipeline har aktiverats för programmet.

![Kör pipeline-alternativ](/help/assets/execution-emergency1.png)

När du visar informationssidan om pipelinekörning för en körning i nödläge visar de synliga kolumnerna högst upp på skärmen en indikation på att pipelinen körs i nödläge.

![Felmeddelanden i nödläge](/help/assets/execution-emergency2.png)

Körning av en pipeline i nödläge kan också göras via Cloud Manager API eller CLI. Om du vill starta en körning i nödläge skickar du en `PUT`-begäran till pipelinens körningsslutpunkt med frågeparametern `?pipelineExecutionMode=EMERGENCY` eller, när CLI används:

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## Köra om en produktionsdistribution {#reexecute-deployment}

I sällsynta fall kan produktionsdistributionsstegen misslyckas av tillfälliga orsaker. I sådana fall stöds omkörning av produktionsdistributionssteget så länge produktionsdistributionssteget har slutförts, oavsett typ av slutförande (t.ex. slutfört, avbrutet eller misslyckat). Omkörning skapar en ny körning med samma pipeline som består av tre steg.

1. **Verifiera steg** - Detta är i stort sett samma validering som sker under en normal pipeline-körning.
1. **Byggsteget** - I samband med en omkörning kopierar byggsteget artefakter och utför inte någon ny byggprocess.
1. **Produktionsdistributionssteget** - Detta använder samma konfiguration och alternativ som produktionsdistributionssteget i en normal pipeline-körning.

I sådana fall där en omkörning är möjlig visas statussidan för produktionsflödet med alternativet **Kör om** bredvid det vanliga alternativet **Hämta bygglogg**.

![Alternativet Kör igen i översiktsfönstret för pipeline](/help/assets/re-execute.png)

>[!NOTE]
>
>I en omkörning markeras byggsteget i användargränssnittet för att reflektera att det är kopieringsartefakter och inte återskapande.

### Begränsningar {#limitations}

* Det går bara att köra produktionsdistributionssteget på nytt för den senaste körningen.
* Omkörning är inte tillgängligt för återställningskörningar eller push-uppdateringskörningar.
* Om den senaste körningen misslyckades någon gång före produktionsdistributionssteget går det inte att utföra om.


### Kör API igen {#reexecute-api}

Förutom att vara tillgänglig i användargränssnittet kan du använda [Cloud Manager-API:t](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) för att utlösa omkörningar samt identifiera körningar som utlösts som omkörningar.

#### Utlösa en omkörning {#triggering}

Om du vill utlösa en omkörning måste en `PUT`-begäran göras till HAL-länken `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` i tillståndet för produktionsdistributionssteget.

* Om den här länken finns kan körningen startas om från det steget.
* Om den inte finns kan körningen inte startas om från det steget.

Länken är bara tillgänglig för produktionsdistributionssteget.

```javascript
 {
  "_links": {
    "http://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```

Syntaxen för HAL-länkens `href`-värde är bara ett exempel och det faktiska värdet ska alltid läsas från HAL-länken och inte genereras.

Om en `PUT`-begäran skickas till den här slutpunkten resulterar det i ett `201`-svar om det lyckas och svarstexten är representationen av den nya körningen. Det liknar att starta en vanlig körning via API:t.

#### Identifiera en körning {#identifying}

Körda körningar kan identifieras av värdet `RE_EXECUTE` i fältet `trigger`.
