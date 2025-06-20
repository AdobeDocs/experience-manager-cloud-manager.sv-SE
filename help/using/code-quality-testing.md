---
title: Testning av kodkvalitet
description: Lär dig hur kodkvalitetstestning av rörledningar fungerar och hur det kan förbättra kvaliteten på dina distributioner.
exl-id: 6a574858-a30e-4768-bafc-8fe79f928294
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '2779'
ht-degree: 0%

---


# Kodkvalitetstestning {#code-quality-testing}

Lär dig hur kodkvalitetstestning av rörledningar fungerar och hur det kan förbättra kvaliteten på dina distributioner.

## Introduktion {#introduction}

Under pipeline-körningen hämtar programvaran ett antal mätvärden. Dessa mått jämförs sedan med nyckeltal (KPI) som definieras av företagsägaren. Eller så jämförs de med standarder som fastställts av Adobe Managed Services.

Dessa resultat rapporteras med ett klassificeringssystem med tre nivåer.

## Betyg med tre nivåer {#three-tiered-ratings}

Det finns tre portar i pipeline:

* Kodkvalitet
* Prestandatestning
* Säkerhetstestning

För var och en av dessa portar finns det en struktur på tre nivåer för problem som identifieras av porten.

* **Kritisk** - Problem som orsakar ett omedelbart fel i pipeline.
* **Viktigt** - Problem som gör att pipeline försätts i pausat läge. Distributionshanteraren, projektledaren eller företagsägaren kan åsidosätta problemen. Om de gör det fortsätter rörledningen som avsett. Alternativt kan de acceptera problemen, vilket gör att pipelinen avbryts om ett fel uppstår. Åsidosättning av viktiga fel sker enligt en [timeout](/help/using/code-deployment.md#timeouts).
* **Info** - Problem som tillhandahålls endast i informationssyfte och som inte påverkar pipeline-körningen.

>[!NOTE]
>
>I en pipeline med enbart kodkvalitet kan viktiga fel i kodkvalitetsgaten inte åsidosättas eftersom teststeget för kodkvalitet är det sista steget i pipeline.

## Kodkvalitetstestning {#code-quality-testing-step}

I det här teststeget utvärderas kvaliteten på programkoden, som är huvudsyftet med en pipeline som enbart innehåller kod. Den utförs omedelbart efter byggsteget i alla icke-produktions- och produktionspipelinor. Om du vill ha mer information går du till [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

Kodkvalitetstestning söker igenom källkoden för att säkerställa att den uppfyller vissa kvalitetskriterier.

Programmet implementerar det med en kombination av SonarQube-analys, innehållspaketgranskning med OakPAL och Dispatcher-validering med Dispatcher Optimization Tool.

Det finns mer än 100 regler som kombinerar generiska Java-regler och AEM-specifika regler. Vissa av de AEM-specifika reglerna skapas baserat på bästa praxis från AEM Engineering och kallas [Anpassade regler för kodkvalitet](/help/using/custom-code-quality-rules.md).

Du kan hämta den aktuella fullständiga listan med regler [med den här länken](/help/assets/CodeQuality-rules-latest-AMS.xlsx).

>[!IMPORTANT]
>
>Från och med torsdagen den 13 februari 2025 (Cloud Manager 2025.2.0) använder Cloud Manager Code Quality en uppdaterad version av SonarQube 9.9 och en uppdaterad lista över regler som du kan [hämta här](/help/assets/CodeQuality-rules-latest-AMS-2024-12-0.xlsx).

Resultaten av kodkvalitetstestningen levereras som en klassificering enligt sammanfattningen i denna tabell.

| Namn | Definition | Kategori | Feltröskel |
| --- | --- | --- | --- |
| Säkerhetsbedömning | A = Ingen sårbarhet<br/>B = Minst 1 mindre sårbarhet<br/>C = Minst 1 större sårbarhet<br/>D = Minst 1 allvarlig sårbarhet<br/>E = Minst 1 blockerarsårbarhet | Kritisk | &lt; B |
| Tillförlitlighetsgrad | A = Inga buggar<br/>B = Minst ett mindre fel <br/>C = Minst ett större fel <br/>D = Minst ett kritiskt fel <br/>E = Minst ett fel i en blockerare | Viktigt | &lt; C |
| Underhållskvalitet | Definieras av den utestående reparationskostnaden för kod luktar som en procentandel av den tid som redan har gått in i programmet <br/><ul><li>A = &lt;=5%</li><li>B = 6-10 %</li><li>C = 11-20 %</li><li>D = 21-50 %</li><li>E = >50 %</li></ul> | Viktigt | &lt; A |
| Täckning | Definieras av en blandning av radens täckning och villkorstäckning med formeln: <br/>`Coverage = (CT + CF + LC) / (2 * B + EL)`  <ul><li>`CT` = Villkor som har utvärderats som `true` minst en gång under körning av enhetstester</li><li>`CF` = Villkor som har utvärderats som `false` minst en gång under körning av enhetstester</li><li>`LC` = Täckta rader = lines_to_cover - uncover_lines</li><li>`B` = totalt antal villkor</li><li>`EL` = totalt antal körbara rader (lines_to_cover)</li></ul> | Viktigt | &lt; 50 % |
| Överhoppade enhetstester | Antal överhoppade enhetstester | Info | > 1 |
| Öppna ärenden | Generella problemtyper - sårbarheter, fel och kodmellanslag | Info | > 0 |
| Duplicerade rader | Definieras som antalet rader som ingår i duplicerade block. Ett kodblock anses duplicerat under följande villkor.<br>Projekt som inte är Java:<ul><li>Det ska finnas minst 100 efterföljande och duplicerade tokens.</li><li>Dessa variabler bör spridas över åtminstone </li><li>30 kodrader för COBOL </li><li>20 kodrader för ABAP </li><li>10 kodrader för andra språk</li></ul>Java-projekt:<ul></li><li> Det ska finnas minst 10 efterföljande och duplicerade satser oavsett antalet tokens och rader.</li></ul>Skillnader i indrag och i stränglitteraler ignoreras när dubbletter identifieras. | Info | > 1 % |
| Cloud Service-kompatibilitet | Antal identifierade Cloud Service-kompatibilitetsproblem | Info | > 0 |

>[!NOTE]
>
>Mer detaljerad information finns i [SonarQube måttdefinitioner](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/).

>[!NOTE]
>
>Mer information om anpassade regler för kodkvalitet som körs av [!UICONTROL Cloud Manager] finns i [Anpassade regler för kodkvalitet](custom-code-quality-rules.md).

### Hantera falskt positiva {#dealing-with-false-positives}

Kvalitetsskanningsprocessen är inte perfekt och identifierar ibland felaktigt problem som inte är problematiska. Detta scenario kallas för falskt positivt.

I dessa fall kan källkoden antecknas med Java `@SuppressWarnings`-standardanteckningen som anger regel-ID som anteckningsattribut. En vanlig positiv sak är att SonarQube-regeln för att identifiera hårdkodade lösenord kan vara aggressiv om hur ett hårdkodat lösenord identifieras.

Följande kod är ganska vanlig i ett AEM-projekt, som har kod för att ansluta till en extern tjänst.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube utlöser sedan en sårbarhet som kan leda till blockering. Men när du har granskat koden inser du att det här problemet inte är någon sårbarhet och kan kommentera koden med rätt regel-ID.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Om koden i själva verket var följande:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Den rätta lösningen är sedan att ta bort det hårdkodade lösenordet.

>[!NOTE]
>
>Det är bäst att göra `@SuppressWarnings`-anteckningen så specifik som möjligt. Anteckna bara den specifika programsats eller det block som orsakar problemet. Det går dock att göra anteckningar på klassnivå. Om du gör det kan du undertrycka varningarna i större utsträckning.

## Säkerhetstestning {#security-testing}

[!UICONTROL Cloud Manager] kör de befintliga AEM Security Health Checks i mellanlagringsmiljön efter distributionen och rapporterar statusen via användargränssnittet. Resultaten sammanställs från alla AEM-instanser i miljön.

Samma hälsokontroller kan utföras när som helst via webbkonsolen eller kontrollpanelen för åtgärder.

Om någon av instanserna rapporterar ett fel för en viss hälsokontroll misslyckas hälsokontrollen i hela miljön. Precis som för kodkvalitets- och prestandatestning är dessa hälsokontroller ordnade i kategorier och rapporterade med hjälp av ett system med tre nivåer. Den enda skillnaden är att det inte finns något tröskelvärde om det finns säkerhetstester. Alla hälsokontroller godkänns eller misslyckas.

I följande tabell visas hälsokontrollerna.

| Namn | Implementering av hälsokontroll | Kategori |
|---|---|---|
| Brandväggsberedskap för Attach API för deserialisering är i ett godtagbart tillstånd. | [Brandväggs API-beredskap för deserialisering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/mitigating-serialization-issues#security) | Kritisk |
| Brandväggen för deserialisering fungerar. | [Brandväggsfunktion för deserialisering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/mitigating-serialization-issues#security) | Kritisk |
| Brandväggen för deserialisering har lästs in. | [Brandvägg för deserialisering har lästs in](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/mitigating-serialization-issues#security) | Kritisk |
| Implementeringen av `AuthorizableNodeName` visar inte auktoriseringsbart ID i nodens namn/sökväg. | [Generering av auktoriseringsbart nodnamn](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/security-checklist#security) | Kritisk |
| Standardlösenordet har ändrats. | [Standardinloggningskonton](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/security#users-and-groups-in-aem) | Kritisk |
| GET-standardserver `Sling` är skyddad från DOS-attacker. | `Sling Get`-servlet | Kritisk |
| JavaScript-hanteraren `Sling` har konfigurerats korrekt. | `Sling` JavaScript-hanterare | Kritisk |
| JSP-skripthanteraren `Sling` har konfigurerats korrekt. | `Sling` JSP-skripthanterare | Kritisk |
| SSL är korrekt konfigurerat. | SSL-konfiguration | Kritisk |
| Inga uppenbart osäkra profiler för användarprofiler hittades. | Standardåtkomst för användarprofil | Kritisk |
| Refererarfiltret `Sling` har konfigurerats för att förhindra CSRF-attacker. | [Sling Referer-filter](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/security-checklist#security) | Viktigt |
| Adobe Granite HTML Library Manager är korrekt konfigurerat. | CQ HTML Library Manager Config | Viktigt |
| Supportpaketet för CRXDE är inaktiverat. | Stöd för CRXDE | Viktigt |
| `Sling` DavEx-paket och -servlet är inaktiverade. | DavEx-hälsokontroll | Viktigt |
| Exempelinnehåll är inte installerat. | Exempel på innehållspaket | Viktigt |
| Både WCM-begärandefiltret och WCM-felsökningsfiltret är inaktiverade. | [Konfiguration av WCM-filter](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/configuring/osgi-configuration-settings#configuring) | Viktigt |
| `Sling` WebDAV-paket och -servlet har konfigurerats korrekt. | WebDAV-hälsokontroll | Viktigt |
| Webbservern är konfigurerad för att förhindra clickjacking. | Konfiguration av webbserver | Viktigt |
| Replikeringen använder inte användaren `admin`. | Replikerings- och transportanvändare | Info |

## Prestandatestning {#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager kör prestandatestning för AEM Sites-program. Prestandatestet körs i cirka 30 minuter genom att virtuella användare (behållare) som simulerar att faktiska användare kommer åt sidor i stagningsmiljöer för att simulera trafik snurras. Dessa sidor hittas med en crawler.

#### Virtuella användare {#virtual-users}

Cloud Manager snurrar upp virtuella användare eller behållare baserat på nyckeltal (svarstid och sidvisningar/min) som angetts av rollen **Affärsägare**. Dessa KPI:er anges när [skapar eller redigerar programmet](/help/getting-started/program-setup.md).

Utifrån definierade KPI:er rensas upp till tio behållare som simulerar verkliga användare. De sidor som väljs för testning delas upp och tilldelas varje virtuell användare.

#### Crawler {#crawler}

Innan testperioden på 30 minuter inleds crawlar Cloud Manager testmiljön med en uppsättning av en eller flera URL:er som konfigurerats av kundens Success Engineer. Med utgångspunkt från dessa URL:er granskas HTML för varje sida och länkarna gås igenom på bredden först.

* Denna crawlningsprocess är som standard begränsad till högst 5 000 sidor.
* Det maximala antalet sidor som ska testas kan skrivas över genom att ange [pipeline-variabeln](/help/getting-started/build-environment.md#pipeline-variables) `CM_PERF_TEST_CRAWLER_MAX_PAGES`.
   * Tillåtna värden är `2000` - `7000`.
* Begäranden från crawlern har en fast tidsgräns på 10 sekunder.

#### Siduppsättningar för testning {#page-sets}

Tre siduppsättningar markerar sidorna. Cloud Manager använder åtkomstloggarna från AEM-instanserna i olika produktions- och stagingmiljöer för att fastställa följande områden.

* **Populära Live-sidor** - Ser till att de populäraste sidorna som besökarna kommer åt testas. Cloud Manager läser åtkomstloggen och fastställer de 25 mest använda sidorna för live-kunder för att generera en lista över de `Popular Live Pages` översta. Skärningspunkten mellan dessa sidor, som också finns i mellanlagringsmiljön, crawlas sedan i mellanlagringsmiljön.

* **Andra Live-sidor** - Säkerställer att de sidor som ligger utanför de 25 populära live-sidorna som kanske inte är populära, men som är viktiga att testa, testas. Ungefär som populära aktiva sidor extraheras de från åtkomstloggen och måste också finnas i mellanlagringsmiljön.

* **Nya sidor** - Testar nya sidor som bara har distribuerats till mellanlagringen och som ännu inte har distribuerats till produktionen, men som måste testas.

##### Distribution av trafik mellan valda siduppsättningar {#distribution-of-traffic}

Du kan välja var som helst från en till alla tre uppsättningar på fliken **Testing** i din [pipeline-konfiguration](/help/using/production-pipelines.md). Trafikfördelningen baseras på antalet valda uppsättningar. Det innebär att om alla tre är markerade placeras 33 % av det totala antalet sidvisningar i varje uppsättning. Om två är markerade går 50 % till varje uppsättning. Om du väljer en sådan går 100 % av trafiken till den uppsättningen.

Låt oss titta på det här exemplet.

* Det är 50/50 som delas mellan populära aktiva sidor och nya siduppsättningar.
* Andra live-sidor används inte.
* Den nya siduppsättningen innehåller 3 000 sidor.
* KPI:n *för sidvisningar per minut* är inställd på 200.

Under 30 minuters testperiod:

* Var och en av de 25 sidorna i den populära aktiva siduppsättningen nås 120 gånger: `((200 * 0.5) / 25) * 30 = 120`
* Var och en av de 3 000 sidorna i den nya siduppsättningen kommer en gång: `((200 * 0.5) / 3000) * 30 = 1`

#### Testa och rapportera {#testing-reporting}

Cloud Manager kör prestandatestning för AEM Sites-program genom att begära sidor som en oautentiserad användare som standard på publiceringsservern för testperioden i 30 minuter. Den mäter de värden som genereras av virtuella användare (svarstid, felfrekvens, vyer per minut och så vidare) för varje sida och olika mätvärden på systemnivå (CPU, minne, nätverksdata) för alla instanser.

I följande tabell sammanfattas prestandatestmatrisen med hjälp av ett gating-system med tre skikt.

| Mått | Kategori | Feltröskel |
|---|---|---|
| Felfrekvens för sidbegäran | Kritisk | >= 2 % |
| CPU utnyttjandegrad | Kritisk | >= 80 % |
| Väntetid för disk-I/O | Kritisk | >= 50 % |
| 95:e procentig svarstid | Viktigt | >= KPI på programnivå |
| Tid för högsta svar | Viktigt | >= 18 sekunder |
| Sidvyer per minut | Viktigt | &lt; KPI på programnivå |
| Användning av diskbandbredd | Viktigt | >= 90 % |
| Utnyttjande av nätverksbandbredd | Viktigt | >= 90 % |
| Begäranden per minut | Info | >= 6000 |

Mer information om hur du använder grundläggande autentisering för prestandatestning för platser och Assets finns i [Autentiserad prestandatestning](#authenticated-performance-testing).

>[!NOTE]
>
>Både författare och publiceringsinstanser övervakas under testet. Om något mått för en instans inte hämtas rapporteras det måttet som okänt och motsvarande steg misslyckas.

#### Autentiserad prestandatestning {#authenticated-performance-testing}

Om det behövs kan AMS-kunder med autentiserade webbplatser ange ett användarnamn och lösenord som Cloud Manager använder för att få tillgång till webbplatsen under webbplatstestningen.

Användarnamnet och lösenordet anges som pipeline-variabler med namnen `CM_PERF_TEST_BASIC_USERNAME` och `CM_PERF_TEST_BASIC_PASSWORD`.

Användarnamnet lagras i en `string`-variabel och lösenordet lagras i en `secretString`-variabel. Om båda dessa variabler anges innehåller varje begäran från crawlern för prestandatestning och de virtuella testanvändarna dessa autentiseringsuppgifter som grundläggande HTTP-autentisering.

Om du vill ställa in dessa variabler med Cloud Manager CLI kör du:

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

Se [Laga användarens pipeline-variabler](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchPipelineVariables) API-dokumentation för att lära dig hur du använder API:t.

### AEM Assets {#aem-assets}

Cloud Manager kör prestandatestning för AEM Assets-program genom att överföra resurser upprepade gånger i 30 minuter.

#### Krav på registrering {#onboarding-requirement}

För prestandatestning i Assets skapar din Customer Success Engineer en `cloudmanager`-användare och ett lösenord när författaren kommer till mellanlagringsmiljön. Prestandateststegen kräver en användare med namnet `cloudmanager` och det associerade lösenordet som har konfigurerats av din CSE.

Den här metoden ska vara kvar i författarinstansen med sina behörigheter oförändrade. Om du ändrar eller tar bort den kan Assets prestandatestning misslyckas.

#### Bilder och Assets för testning {#assets-for-testing}

Kunderna kan överföra egna resurser för testning. Den här processen kan utföras från skärmen **Inställningar för pipeline** eller **Redigera**. Vanliga bildformat som JPEG, PNG, GIF och BMP stöds tillsammans med Photoshop-, Illustrator- och Postscript-filer.

Om inga bilder överförs använder Cloud Manager en standardbild och PDF-dokument för testning.

#### Distribution av Assets för testning {#distribution-of-assets}

Distributionen av hur många resurser av varje typ som överförs per minut anges på skärmen **Inställningar för pipeline** eller **Redigera**.

Om exempelvis en delning på 70/30 används och det finns 10 resurser överförda per minut, överförs 7 bilder och 3 dokument per minut.

#### Testa och rapportera {#testing-and-reporting}

Cloud Manager skapar en mapp på författarinstansen med det användarnamn och lösenord som CSE-installationen använder. Assets överförs sedan till mappen med ett bibliotek med öppen källkod. Testen som körs av Assets teststeg har skrivits med ett [bibliotek med öppen källkod](https://github.com/adobe/toughday2). Både bearbetningstiden för varje resurs och olika mätvärden på systemnivå mäts under testperioden på 30 minuter. Den här funktionen kan överföra både bilder och PDF-dokument.

>[!TIP]
>
>Mer information finns i [Konfigurera produktionspipelines](/help/using/production-pipelines.md). Mer information om hur du konfigurerar programmet och definierar nyckeltal finns i [Programinställningar](/help/getting-started/program-setup.md).

### Resultatdiagram för prestandatestning {#performance-testing-results-graphs}

Ett antal mätvärden är tillgängliga i dialogrutan **Prestandatest**.

![Lista med mätvärden](/help/assets/understand_test-results-screen1.png)

Måttpanelerna kan expanderas för att visa ett diagram, ge en länk till en hämtning eller båda.

![Mätvärden utökade som diagram](/help/assets/screen_shot_2018-09-05at83933pm.png)

Den här funktionen är tillgänglig för följande mätvärden.

* **CPU-användning** - Ett diagram över CPU-användning under testperioden

* **Diskens I/O-väntetid** - Ett diagram över diskens I/O-väntetid under testperioden

* **Sidfelsfrekvens** - Ett diagram över sidfel per minut under testperioden
   * En CSV-fil med en lista över sidor som genererat ett fel under testet

* **Användning av diskbandbredd** - Ett diagram över användning av diskbandbredd under testperioden

* **Utnyttjande av nätverksbandbredd** - Ett diagram över utnyttjande av nätverksbandbredd under testperioden

* **Maximal svarstid** - Ett diagram över maximal svarstid per minut under testperioden

* **95th Percentile Response Time** - Ett diagram över 95:e percentils responstid per minut under testperioden
   * En CSV-fil med en lista över sidor vars 95:e percentilsvarstid har överskridit den definierade KPI:n

## Optimering av skanning av innehållspaket {#content-package-scanning-optimization}

Som en del av kvalitetsanalysprocessen gör Cloud Manager en analys av de innehållspaket som skapats av Maven-bygget. Cloud Manager erbjuder optimeringar som snabbar upp denna process, som är effektiv när vissa paketeringsbegränsningar iakttas.

Nyckeloptimeringen är för projekt som genererar ett enda&quot;all&quot;-paket som innehåller andra innehållspaket som skapats av bygget, som markeras som överhoppade. När Cloud Manager identifierar detta scenario, i stället för att packa upp&quot;all&quot;-paketet, skannas de enskilda innehållspaketen direkt och sorteras baserat på beroenden. Ta till exempel följande byggutdata.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (innehållspaket)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (överhoppat innehållspaket)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (överhoppat innehållspaket)

Om de enda objekten i `myco-all-1.0.0-SNAPSHOT.zip` är de två överhoppade innehållspaketen skannas de två inbäddade paketen i stället för innehållspaketet &quot;all&quot;.

För projekt som producerar dussintals inbäddade paket har den här optimeringen visat sig spara upp till 10 minuter per pipeline-körning.

Ett specialfall kan inträffa när innehållspaketet &quot;all&quot; innehåller en kombination av överhoppade innehållspaket och OSGi-paket. Om `myco-all-1.0.0-SNAPSHOT.zip` till exempel innehåller de två inbäddade paketen som nämndes tidigare och ett eller flera OSGi-paket, skapas ett nytt, minimalt innehållspaket med endast OSGi-paketen. Det här paketet har alltid namnet `cloudmanager-synthetic-jar-package` och de inkluderade paketen placeras i `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* Optimeringen påverkar inte paket som distribueras till AEM.
>* Matchning mellan inbäddade och överhoppade innehållspaket baseras på filnamn. Optimeringen misslyckas om flera överhoppade innehållspaket delar samma filnamn eller om filnamnet ändras under inbäddningen.
