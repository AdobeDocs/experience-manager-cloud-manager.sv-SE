---
title: Koddistribution
description: Lär dig hur du distribuerar kod och vad som händer i Cloud Manager när du gör det.
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: b98e1711f1f98f52977dd6cb4cd2bc834d81a360
workflow-type: tm+mt
source-wordcount: '1636'
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

Du kan granska stegen från olika distributionsprocesser genom att visa loggar eller granska resultaten för testvillkoren.

## Distributionssteg {#deployment-steps}

Ett antal åtgärder inträffar under varje steg i distributionen, vilket beskrivs i det här avsnittet. Mer teknisk information om hur själva koden distribueras bakom scenerna finns i [Information om distributionsprocess](#deployment-process) .

### Steg för driftsättning {#stage-deployment}

Steg **Scendistribution** innehåller följande åtgärder:

* **Validering**: Detta steg säkerställer att pipeline är konfigurerad att använda de tillgängliga resurserna. Till exempel att den konfigurerade grenen finns och att miljöerna är tillgängliga.
* **Build &amp; Unit Testing**: Det här steget kör en innehållsstyrd byggprocess. Mer information finns i [Build Environment](/help/getting-started/build-environment.md).
* **Kodsökning**: I det här steget utvärderas kvaliteten på programkoden. Mer information om testprocessen finns i [Förstå testresultat](/help/using/code-quality-testing.md).
* **Distribuera till scenen**

![Scendistribution](/help/assets/Stage_Deployment1.png)

### Steg för testning {#stage-testing}

**Scentestningen** omfattar följande åtgärder:

* **Säkerhetstestning**: I det här steget utvärderas kodens säkerhetseffekt i AEM-miljön. Mer information om testprocessen finns i dokumentet [Förstå testresultat](/help/using/code-quality-testing.md).
   * **Prestandatestning**: I det här steget utvärderas kodens prestanda. Mer information om testprocessen finns i [Förstå testresultat](/help/using/code-quality-testing.md).

### Distributionssteg för produktion {#production-deployment}

Steget **Produktionsdistribution** innehåller följande åtgärder:

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

1. Cloud Manager avgör om varje artefakt är ett AEM- eller Dispatcher-paket.
1. Cloud Manager tar bort alla utskickare från belastningsutjämnaren för att isolera miljön under distributionen.

   * Om inget annat anges kan du hoppa över ändringar i belastningsutjämnaren i distributionen av utveckling och testning. Det vill säga, när det gäller utvecklingsmiljön, frigöra och knyta ihop steg i både icke-produktionsrörledningar och för mellanlagringsmiljön i produktionsflödet.

   ![Hoppa över belastningsutjämnare](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >1-1-1-1-kunder förväntas använda den här funktionen.

1. Varje AEM-artefakt distribueras till varje AEM-instans via API:er för Package Manager, där paketberoenden avgör distributionsordningen.

   * Läs mer om hur du kan använda paket för att installera nya funktioner, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll. Se [Package Manager](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

   >[!NOTE]
   >
   >Alla AEM-artefakter distribueras till både författaren och utgivaren. Körningslägena bör utnyttjas när nodspecifika konfigurationer krävs. Om du vill veta mer om hur körningslägena gör att du kan trimma din AEM-instans för ett visst ändamål kan du läsa avsnittet [Körningslägen i dokumentet Distribuera till AEM as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/deploying/overview#runmodes).

1. Dispatcher-artefakten distribueras till alla Dispatcher enligt följande:

   1. Aktuella konfigurationer säkerhetskopieras och kopieras till en tillfällig plats.
   1. Alla konfigurationer tas bort utom de oföränderliga filerna. Mer information finns i [Dispatcher Configurations](/help/getting-started/dispatcher-configurations.md). På så sätt rensas katalogerna så att inga överblivna filer lämnas kvar.
   1. Artefakten extraheras till katalogen `httpd`. Oändringsbara filer skrivs inte över. Alla ändringar du gör i oföränderliga filer i Git-databasen ignoreras vid distributionen. Dessa filer är viktiga för AMS Dispatcher-ramverket och kan inte ändras.
   1. Apache utför ett konfigurationstest. Om inga fel hittas läses tjänsten in igen. Om fel hittas återställs konfigurationerna från en säkerhetskopia, tjänsten läses in igen och felet rapporteras tillbaka till Cloud Manager.
   1. Alla sökvägar som anges i pipeline-konfigurationen görs ogiltiga eller tömda från Dispatcher-cachen.

   >[!NOTE]
   >
   >Cloud Manager förväntar sig att Dispatcher-artefakten ska innehålla hela filuppsättningen. Alla Dispatcher-konfigurationsfiler måste finnas i Git-databasen. Saknade filer eller mappar leder till distributionsfel.

1. När alla AEM- och Dispatcher-paket har distribuerats till alla noder läggs de som skickar paketen tillbaka till belastningsutjämnaren och distributionen är klar.

   >[!NOTE]
   >
   >Du kan hoppa över ändringar av belastningsutjämnare i utveckling och mellanlagringsdistributioner. Det vill säga, när det gäller utvecklingsmiljön, frigöra och knyt ihop steg i både icke-produktionsrörledningar och för mellanlagringsmiljön i produktionsflödet.

### Distribution till produktionsfas {#deployment-production-phase}

Processen för att distribuera till produktionstopologier skiljer sig något för att minimera påverkan för besökare på AEM webbplats.

Produktionsinstallationer följer i allmänhet samma steg som ovan, men på ett rullande sätt:

1. Distribuera AEM-paket till författaren.
1. Koppla loss dispatcher1 från belastningsutjämnaren.
1. Distribuera AEM-paket för att publicera1 och Dispatcher-paketet för att skicka1 parallellt, tömma Dispatcher-cachen.
1. Placera dispatcher1 i belastningsutjämnaren igen.
1. När dispatcher1 är tillbaka i tjänst frigör du dispatcher2 från belastningsutjämnaren.
1. Distribuera AEM-paket för att publicera2 och Dispatcher-paketet till dispatcher2 parallellt, rensa Dispatcher-cachen.
1. Placera dispatcher2 i belastningsutjämnaren igen.

Den här processen fortsätter tills distributionen har nått alla utgivare och utgivare i topologin.

## Körningsläge för nödrörledning {#emergency-pipeline}

I kritiska situationer kan Adobe Managed Services-kunder behöva driftsätta kodändringar direkt i sina scen- och produktionsmiljöer. Detta gör att de kan kringgå hela Cloud Manager testcykel.

För att åtgärda dessa situationer kan Cloud Manager produktionsflöde genomföras i nödläge. När det här läget används utförs inte stegen för säkerhets- och prestandatestning. Alla andra steg, inklusive konfigurerade godkännandesteg, körs som i det normala körningsläget för pipeline.

>[!NOTE]
>
>Funktionen för driftsättning av nödpipeline aktiveras program för program. Aktiveringen görs av Customer Success Engineers.

### Använd körningsläge för nödsituationer {#using-emergency-pipeline}

När du startar en körning av en produktionspipeline kan du välja mellan normalt läge eller nödläge i en dialogruta. Det här alternativet är tillgängligt om funktionen för körning av nödpipeline är aktiverad för programmet. Det här alternativet är tillgängligt när funktionen är aktiverad.

![Kör pipeline-alternativ](/help/assets/execution-emergency1.png)

När du visar informationssidan om pipelinekörning för en körning i nödläge visar de synliga kolumnerna högst upp på skärmen en indikation på att pipelinen körs i nödläge.

![Felmeddelanden i nödläge](/help/assets/execution-emergency2.png)

Körning av en pipeline i nödläge kan också göras via Cloud Manager API eller CLI. Om du vill starta en körning i nödläge skickar du en `PUT`-begäran till pipelinens körningsslutpunkt med frågeparametern `?pipelineExecutionMode=EMERGENCY` eller, när CLI används:

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## Köra om en produktionsdistribution {#reexecute-deployment}

I sällsynta fall kan produktionsdistributionsstegen misslyckas av tillfälliga orsaker. I dessa fall kan du köra produktionsdistributionssteget igen så länge det har slutförts, oavsett om det lyckades, avbröts eller misslyckades. Återkörning stöds genom att använda samma pipeline som består av följande tre steg:

1. **Valideringssteget** - Samma validering som sker under en normal pipeline-körning.
1. **Byggsteget** - I samband med en omkörning kopierar byggsteget artefakter och utför inte någon ny byggprocess.
1. **Produktionsdistributionssteget** - Använder samma konfiguration och alternativ som produktionsdistributionssteget i en normal pipeline-körning.

I sådana fall där en omkörning är möjlig visas statussidan för produktionsflödet med alternativet **Kör om** bredvid det vanliga alternativet **Hämta bygglogg**.

![Alternativet Kör igen i översiktsfönstret för pipeline](/help/assets/re-execute.png)

>[!NOTE]
>
>I en omkörning markeras byggsteget i användargränssnittet för att reflektera att det är kopieringsartefakter och inte återskapande.

### Begränsningar {#limitations}

* Det går bara att köra produktionsdistributionssteget på nytt för den senaste körningen.
* Omkörning är inte tillgängligt för återställningskörningar eller push-uppdateringskörningar.
* Om den senaste körningen misslyckades någon gång före produktionsdistributionssteget går det inte att utföra om.


### Kör om API {#reexecute-api}

Förutom att vara tillgänglig i användargränssnittet kan du använda [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) för att utlösa omkörningar och identifiera körningar som utlösts som omkörningar.

#### Utlösa en omkörning {#triggering}

Om du vill utlösa en omkörning måste en `PUT`-begäran göras till HAL-länken `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` i tillståndet för produktionsdistributionssteget.

* Om den här länken finns kan körningen startas om från det steget.
* Om den inte finns kan inte körningen startas om från det steget.

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

Om en `PUT`-begäran skickas till den här slutpunkten returneras ett `201`-svar om det lyckas. Svarstexten är representationen av den nya körningen. Den här funktionaliteten liknar att starta en vanlig körning via API:t.

#### Identifiera en körd exekvering {#identifying}

Systemet identifierar körningar som gjorts om av värdet `RE_EXECUTE` i utlösarfältet.