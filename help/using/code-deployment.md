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

1. Klicka **Distribuera** från Cloud Manager för att starta distributionsprocessen.

   ![Knappen Distribuera](/help/assets/Deploy1.png)

1. The **Körning av pipeline** visas. Klicka **Bygge** för att starta processen.

   ![Knappen Skapa](/help/assets/Deploy2.png)

Byggprocessen startar koddistributionsprocessen med följande steg:

* Scendistribution
* Stage testing
* Produktionsdistribution

Du kan granska stegen från olika distributionsprocesser genom att visa loggar eller granska resultaten för att se testvillkoren.

## Distributionssteg {#deployment-steps}

Ett antal åtgärder inträffar under varje steg i distributionen, som beskrivs i det här avsnittet. Se avsnittet [Information om distributionsprocess](#deployment-process) om du vill ha teknisk information om hur själva koden används bakom kulisserna.

### Steg för driftsättning {#stage-deployment}

The **Scendistribution** omfattar följande åtgärder:

* **Validering**: Detta steg säkerställer att pipeline är konfigurerad att använda de tillgängliga resurserna, t.ex. att den konfigurerade grenen finns och att miljöerna är tillgängliga.
* **Build &amp; Unit Testing**: Det här steget kör en innesluten byggprocess. Se dokumentet [Byggmiljön](/help/getting-started/build-environment.md) för mer information.
* **Kodskanning**: Det här steget utvärderar kvaliteten på programkoden. Se dokumentet [Förstå testresultat](/help/using/code-quality-testing.md) om du vill ha mer information om testprocessen.
* **Distribuera till scenen**

![Scendistribution](/help/assets/Stage_Deployment1.png)

### Steg för testning {#stage-testing}

The **Stage testing** omfattar följande åtgärder:

* **Säkerhetstestning**: Det här steget utvärderar hur koden påverkar säkerheten i AEM. Se dokumentet [Förstå testresultat](/help/using/code-quality-testing.md) om du vill ha mer information om testprocessen.
   * **Prestandatestning**: Det här steget utvärderar hur koden fungerar. Se [Förstå testresultat](/help/using/code-quality-testing.md) om du vill ha mer information om testprocessen.

### Produktionsdistributionssteg {#production-deployment}

The **Produktionsdistribution** omfattar följande åtgärder:

* **Ansökan om godkännande**
   * Det här alternativet aktiveras när pipeline konfigureras.
   * Med det här alternativet kan du antingen schemalägga din produktionsdistribution eller klicka på **Nu** för att genomföra produktionsdistributionen omedelbart.
* **Schemalägg produktionsdistribution**
   * Det här alternativet aktiveras när pipeline konfigureras.
   * Det schemalagda datumet och den schemalagda tiden anges i användarens tidszon.
     ![Schemalägg distribution](/help/assets/Production_Deployment1.png)
* **Stöd för CSE** (om aktiverat)
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

När Cloud Manager distribuerar till icke-produktionstopologier är målet att slutföra distributionen så snabbt som möjligt och artefakterna distribueras därför till alla noder samtidigt enligt följande:

1. Cloud Manager avgör om varje artefakt är ett AEM- eller dispatcherpaket.
1. Cloud Manager tar bort alla utskickare från belastningsutjämnaren för att isolera miljön under distributionen.

   * Om inget annat anges kan du hoppa över ändringar av belastningsutjämnaren i distributionen av utveckling och staging, dvs. för utvecklingsmiljön, koppla loss och bifoga steg i både icke-produktionspipelines och för produktionsflödet i mellanlagringsmiljön.

   ![Hoppa över belastningsutjämnare](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >Den här funktionen förväntas främst användas av 1-1-1-kunder.

1. Varje AEM-artefakt distribueras till varje AEM-instans via API:er för Package Manager, där paketberoenden avgör distributionsordningen.

   * Mer information om hur du kan använda paket för att installera nya funktioner, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll finns i dokumentet [Pakethanteraren.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)

   >[!NOTE]
   >
   >Alla AEM artefakter distribueras till både författaren och utgivaren. Körningslägena bör utnyttjas när nodspecifika konfigurationer krävs. Om du vill veta mer om hur körningslägena gör att du kan trimma AEM för ett visst ändamål kan du läsa [Avsnittet Körningslägen i dokumentet Distribuera till AEM as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)

1. Dispatchartefakten distribueras till varje dispatcher enligt följande:

   1. Aktuella konfigurationer säkerhetskopieras och kopieras till en tillfällig plats.
   1. Alla konfigurationer tas bort utom de oföränderliga filerna. Se dokumentet [Dispatcher Configurations](/help/getting-started/dispatcher-configurations.md) för mer information. Detta rensar katalogerna för att säkerställa att inga överblivna filer lämnas kvar.
   1. Artefakten extraheras till `httpd` katalog. Oändringsbara filer skrivs inte över. Alla ändringar du gör i oföränderliga filer i Git-databasen ignoreras vid distributionen. Dessa filer är viktiga för AMS-dispatcherramverket och kan inte ändras.
   1. Apache utför ett konfigurationstest. Om inga fel hittas läses tjänsten in igen. Om ett fel inträffar återställs konfigurationerna från en säkerhetskopia, tjänsten läses in igen och felet rapporteras tillbaka till Cloud Manager.
   1. Varje sökväg som anges i pipeline-konfigurationen görs ogiltig eller töms från dispatchercachen.

   >[!NOTE]
   >
   >Dispatcher-artefakten förväntas innehålla den fullständiga filuppsättningen. Alla konfigurationsfiler för dispatcher måste finnas i Git-databasen. Om filer eller mappar saknas kommer distributionen att misslyckas.

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

I kritiska situationer kan Adobe Managed Services-kunder behöva driftsätta kodändringar i sina scen- och produktionsmiljöer utan att vänta på att en fullständig testcykel för Cloud Manager ska köras.

För att hantera dessa situationer kan produktionsflödet i Cloud Manager köras i ett nödläge. När det här läget används utförs inte stegen för säkerhets- och prestandatestning. Alla andra steg, inklusive konfigurerade godkännandesteg, körs som i det normala körningsläget för pipeline.

>[!NOTE]
>
>Funktionen för driftsättning av beredskapsled aktiveras program för program av Customer Success Engineers.

### Använda körningsläge för nödpipeline {#using-emergency-pipeline}

När du startar en körning av en produktionspipeline kan du starta körningen i normalt läge eller nödläge från en dialogruta om funktionen för körning av nödpipeline har aktiverats för programmet.

![Köra pipelinealternativ](/help/assets/execution-emergency1.png)

När du visar informationssidan om pipelinekörning för en körning i nödläge visar de synliga kolumnerna högst upp på skärmen en indikation på att pipelinen körs i nödläge.

![Felsökningslägen](/help/assets/execution-emergency2.png)

Du kan även köra en pipeline i nödläge via Cloud Manager API eller CLI. Om du vill starta en körning i nödläge skickar du en `PUT` begäran till pipelinens körningsslutpunkt med frågeparametern `?pipelineExecutionMode=EMERGENCY` eller, när CLI används:

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## Köra om en produktionsdistribution {#reexecute-deployment}

I sällsynta fall kan produktionsdistributionsstegen misslyckas av tillfälliga orsaker. I sådana fall stöds omkörning av produktionsdistributionssteget så länge produktionsdistributionssteget har slutförts, oavsett typ av slutförande (t.ex. slutfört, avbrutet eller misslyckat). Omkörning skapar en ny körning med samma pipeline som består av tre steg.

1. **Valideringssteget** - Detta är i stort sett samma validering som sker under en normal pipeline-körning.
1. **Byggsteget** - I samband med en omkörning kopierar byggsteget artefakter och utför inte någon ny byggprocess.
1. **Produktionsdistributionssteget** - Detta använder samma konfiguration och alternativ som produktionsdistributionssteget i en normal pipeline-körning.

I sådana fall där ett återgenomförande är möjligt visas statussidan för produktionsflödet på sidan med **Kör igen** alternativ bredvid det vanliga **Hämta bygglogg** alternativ.

![Alternativet Kör igen i översiktsfönstret för pipeline](/help/assets/re-execute.png)

>[!NOTE]
>
>I en omkörning markeras byggsteget i användargränssnittet för att reflektera att det är kopieringsartefakter och inte återskapande.

### Begränsningar {#limitations}

* Det går bara att köra produktionsdistributionssteget på nytt för den senaste körningen.
* Omkörning är inte tillgängligt för återställningskörningar eller push-uppdateringskörningar.
* Om den senaste körningen misslyckades någon gång före produktionsdistributionssteget går det inte att utföra om.


### Kör API igen {#reexecute-api}

Förutom att vara tillgänglig i användargränssnittet kan du använda [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) för att utlösa omkörningar samt identifiera körningar som utlöstes som omkörningar.

#### Utlösa en omkörning {#triggering}

Om du vill utlösa en omkörning `PUT` begäran måste göras till HAL Link `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` i produktionsdistributionssteget.

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

Syntaxen för HAL-länkens `href` värdet är bara ett exempel och det faktiska värdet ska alltid läsas från HAL-länken och inte genereras.

Skicka ett `PUT` begäran till den här slutpunkten resulterar i `201` om svaret lyckas och svarsorganet är representationen av den nya exekveringen. Det liknar att starta en vanlig körning via API:t.

#### Identifiera en körning {#identifying}

Körda körningar kan identifieras av värdet `RE_EXECUTE` i `trigger` fält.
