---
title: Anpassade regler för kodkvalitet
seo-title: Anpassade regler för kodkvalitet
description: Följ den här sidan för att lära dig mer om de anpassade regler för kodkvalitet som körs av Cloud Manager.
seo-description: Följ den här sidan för att lära dig mer om de anpassade regler för kodkvalitet som körs av Adobe Experience Manager Cloud Manager.
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
translation-type: tm+mt
source-git-commit: 3663bd773c0043282359d690621de5023fa2974c
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 5%

---


# Custom Code Quality Rules {#custom-code-quality-rules}

Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager och som baseras på god praxis från AEM Engineering.

>[!NOTE]
>
>De kodexempel som anges här är endast avsedda som illustrationer.

## SonarQube-regler {#sonarqube-rules}

I följande avsnitt beskrivs SonarQube Rules:

### Använd inte potentiellt farliga funktioner {#do-not-use-potentially-dangerous-functions}

**Nyckel**: CQRules:CWE-676

**Typ**: Sårbarhet

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2018.4.0

Metoderna ***Thread.stop()*** och ***Thread.interrupt()*** kan skapa problem som är svåra att återge och i vissa fall även skapa säkerhetsluckor. Deras användning bör övervakas noggrant och valideras. I allmänhet är meddelandeöverföring ett säkrare sätt att uppnå samma sak.

#### Icke-kompatibel kod {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Kompatibel kod {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### Använd inte formatsträngar som kan vara externt kontrollerade {#do-not-use-format-strings-which-may-be-externally-controlled}

**Nyckel**: CQRules:CWE-134

**Typ**: Sårbarhet

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2018.4.0

Om du använder en formatsträng från en extern källa (t.ex. en begärandeparameter eller ett användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

#### Icke-kompatibel kod {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP-begäranden ska alltid ha socket- och anslutningstimeout {#http-requests-should-always-have-socket-and-connect-timeouts}

**Nyckel**: CQRules:ConnectionTimeoutMechanism

**Typ**: Fel

**Allvarlighetsgrad**: Kritisk

**Sedan**: Version 2018.6.0

När HTTP-begäranden körs inifrån ett AEM-program är det viktigt att se till att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr är standardbeteendet för både Java:s standard-HTTP-klient (java.net.HttpUrlConnection) och den vanligaste Apache HTTP Components-klienten att aldrig timeout, så timeout måste anges explicit. Dessutom bör dessa timeout inte vara längre än 60 sekunder.

#### Icke-kompatibel kod {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Kompatibel kod {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Produkt-API:er som annoterats med @ProviderType ska inte implementeras eller utökas av kunder {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**Nyckel**: CQBP-84, CQBP-84-beroenden

**Typ**: Fel

**Allvarlighetsgrad**: Kritisk

**Sedan**: Version 2018.7.0

API:t för AEM innehåller Java-gränssnitt och -klasser som bara är avsedda att användas, inte implementeras, av anpassad kod. Gränssnittet *com.day.cq.wcm.api.Page* är till exempel utformat att implementeras av ***enbart AEM***.

När nya metoder läggs till i dessa gränssnitt påverkar inte dessa ytterligare metoder befintlig kod som använder dessa gränssnitt, och därför anses tillägg av nya metoder i dessa gränssnitt vara bakåtkompatibelt. Men om anpassad kod ***implementerar*** ett av dessa gränssnitt har den anpassade koden skapat en risk vad gäller bakåtkompatibilitet för kunden.

Gränssnitt (och klasser) som endast är avsedda att implementeras av AEM kommenteras med *org.osgi.annotation.versioning.ProviderType* (eller, i vissa fall, en liknande äldre anteckning *aQute.bnd.annotation.ProviderType*). Den här regeln identifierar de fall där ett sådant gränssnitt implementeras (eller där en klass utökas) med anpassad kod.

#### Icke-kompatibel kod {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver-objekt ska alltid stängas {#resourceresolver-objects-should-always-be-closed}

**Nyckel**: CQRules:CQBP-72

**Typ**: Code Smell

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2018.4.0

ResourceResolver-objekt som hämtats från ResourceResolverFactory förbrukar systemresurser. Även om det finns åtgärder för att återta dessa resurser när en ResourceResolver inte längre används, är det mer effektivt att uttryckligen stänga alla öppna ResourceResolver-objekt genom att anropa metoden close().

En ganska vanlig missuppfattning är att ResourceResolver-objekt som skapats med en befintlig JCR-session inte uttryckligen ska stängas eller att det kommer att stänga den underliggande JCR-sessionen. Detta är inte fallet - oavsett hur en ResourceResolver öppnas bör den stängas när den inte längre används. Eftersom ResourceResolver implementerar gränssnittet Closeable går det också att använda syntaxen try-with-resources i stället för att explicit anropa close().

#### Icke-kompatibel kod {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Kompatibel kod {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Använd inte SSLING-serversökvägar för att registrera servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

**Nyckel**: CQRules:CQBP-75

**Typ**: Code Smell

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2018.4.0

Så som beskrivs i [Sling-dokumentationen](http://sling.apache.org/documentation/the-sling-engine/servlets.html)rekommenderas inte bindningar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Icke-kompatibel kod {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Undantag som fångats upp ska loggas eller kastas, men inte båda {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Nyckel**: CQRules:CQBP-44—CatchAndeitherLogOrThrow

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

I allmänhet bör ett undantag loggas exakt en gång. Om du loggar undantag flera gånger kan det leda till missförstånd eftersom det är oklart hur många gånger ett undantag inträffade. Det vanligaste mönstret som leder till detta är loggning och generering av ett fångat undantag.

#### Icke-kompatibel kod {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Kompatibel kod {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Undvik att ha en log-programsats omedelbart följt av en throw-programsats {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Nyckel**: CQRules:CQBP-44 - ConsecutiousLogAndThrow

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Ett annat vanligt sätt att undvika är att logga ett meddelande och sedan omedelbart generera ett undantag. Detta innebär vanligtvis att undantagsmeddelandet kommer att dupliceras i loggfiler.

#### Icke-kompatibel kod {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Kompatibel kod {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Undvik att logga på INFO när du hanterar GET- eller HEAD-begäranden {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och som standard är AEM konfigurerad för att logga på INFO-nivå eller högre. GET- och HEAD-metoder bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. Loggning vid hantering av GET- eller HEAD-begäranden bör finnas antingen på WARN- eller ERROR-nivå när något har gått fel eller på DEBUG- eller TRACE-nivå om mer detaljerad felsökningsinformation skulle vara till hjälp.

>[!CAUTION]
>
>Detta gäller inte för access.log-type-loggning för varje begäran.

#### Icke-kompatibel kod {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Kompatibel kod {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Använd inte Exception.getMessage() som första parameter i en loggningssats {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**Nyckel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Även om kontexten kan avgöras genom att stackspårningar används, kommer loggmeddelandet i allmänhet att vara lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet innehåller det som gick fel, medan loggmeddelandet bör användas för att tala om för en loggläsare vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet kommer fortfarande att loggas; genom att ange ett eget meddelande blir loggarna enklare att förstå.

#### Icke-kompatibel kod {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Kompatibel kod {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Inloggning av catch-block ska ske på WARN- eller ERROR-nivå {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Nyckel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Som namnet antyder bör Java-undantag alltid användas i *undantagsfall* . Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp - antingen WARN eller ERROR. Detta garanterar att meddelandena visas korrekt i loggarna.

#### Icke-kompatibel kod {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Kompatibel kod {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Skriv inte ut stackspår till konsolen {#do-not-print-stack-traces-to-the-console}

**Nyckel**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Som vi nämnt är sammanhang viktigt när du ska förstå loggmeddelanden. Om du använder Exception.printStackTrace() genereras **endast** stackspårningen som utdata till standardfelströmmen och därmed förlorar all kontext. I ett program med flera trådar, som AEM, kan dessutom stackspårningarna överlappa varandra om flera undantag skrivs ut med den här metoden parallellt, vilket kan skapa stor förvirring. Undantag bör endast loggas via loggningsramverket.

#### Icke-kompatibel kod {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Kompatibel kod {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Skriv inte ut till standardutdata eller standardfel {#do-not-output-to-standard-output-or-standard-error}

**Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Inloggning med AEM bör alltid göras via loggningsramverket (SLF4J). Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket och kan i vissa fall orsaka prestandaproblem.

#### Icke-kompatibel kod {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Kompatibel kod {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Undvik hårdkodade/appar- och/libs-sökvägar {#avoid-hardcoded-apps-and-libs-paths}

**Nyckel**: CQRules:CQBP-71

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Vanligtvis ska sökvägar som börjar med /libs och /apps inte vara hårdkodade eftersom de sökvägar de refererar till vanligtvis lagras som sökvägar i förhållande till sökvägen Sling (som är inställd på /libs,/apps som standard). Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

#### Icke-kompatibel kod {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Kompatibel kod {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Sling Scheduler ska inte användas {#sonarqube-sling-scheduler}

**Nyckel**: CQRules:AMSCORE-554

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

Sling Scheduler får inte användas för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Läs mer om hur [Sling-jobb hanteras i klustermiljöer i](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) Apache Sling-händelser och jobbhantering.

### AEM-inaktuella API:er får inte användas {#sonarqube-aem-deprecated}

**Nyckel**: AMSCORE-553

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

AEM API-ytan är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

I många fall används standardanteckningen Java *@Deprecated* , som identifieras av `squid:CallToDeprecatedMethod`.

Det finns emellertid fall där ett API är inaktuellt i AEM-kontexten men inte kan bli inaktuellt i andra sammanhang. Den här regeln identifierar den andra klassen.

## OakPAL-innehållsregler {#oakpal-rules}

Nedan finns de OakPAL-kontroller som körs av Cloud Manager.

>[!NOTE]
>OakPAL är ett ramverk som utvecklats av en AEM-partner (och vinnare av 2019 AEM Rockstar North America) som validerar innehållspaket med en fristående Oak-databas.

### Kundpaket får inte skapa eller ändra noder under /libs {#oakpal-customer-package}

**Nyckel**: BannedPaths

**Typ**: Fel

**Allvarlighetsgrad**: Blockera

**Sedan**: Version 2019.6.0

Det har varit en god praxis sedan länge att /libs-innehållsträdet i AEM-innehållsarkivet ska betraktas som skrivskyddat av kunderna. Att ändra noder och egenskaper under */libs* skapar en betydande risk för större och mindre uppdateringar. Modifieringar av */libs* får endast göras av Adobe via officiella kanaler.

### Paket får inte innehålla dubbletter av OSGi-konfigurationer {#oakpal-package-osgi}

**Nyckel**: DuplicateOsgiConfigurations

**Typ**: Fel

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Detta skapar en tvetydighet om vilken konfiguration som kan användas. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge (eller en kombination av körningslägen).

#### Icke-kompatibel kod {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Kompatibel kod {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Konfigurations- och installationsmappar får endast innehålla OSGi-noder {#oakpal-config-install}

**Nyckel**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Typ**: Fel

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2019.6.0

Av säkerhetsskäl kan sökvägar som innehåller */config/ och /install/* endast läsas av administrationsanvändare i AEM och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda noder som namnges `config` i komponentdialogrutor eller när du anger RTF-redigeringskonfigurationen för infogad redigering. För att lösa detta bör den felande noden byta namn till ett kompatibelt namn. För RTF-redigerarkonfigurationen använder du egenskapen `configPath` på `cq:inplaceEditing` noden för att ange den nya platsen.

#### Icke-kompatibel kod {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Kompatibel kod {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Paket får inte överlappa {#oakpal-no-overlap}

**Nyckel**: PackageOverlaps

**Typ**: Fel

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2019.6.0

På liknande sätt som *Paket bör inte innehålla duplicerade OSGi-konfigurationer* är detta ett vanligt problem i komplexa projekt där samma nodsökväg skrivs till av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara ett klassiskt användargränssnitt {#oakpal-default-authoring}

**Nyckel**: KlassisktUIAuthoringMode

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i AEM. Eftersom det klassiska användargränssnittet har tagits bort sedan AEM 6.4 kommer ett problem nu att uppstå när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha gränssnittsdialogrutor med pekskärmar {#oakpal-components-dialogs}

**Nyckel**: ComponentWithOnlyClassicUIDialog

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

AEM-komponenter som har en klassisk gränssnittsdialogruta bör alltid ha en motsvarande Touch-gränssnittsdialogruta, både för att ge en optimal redigeringsupplevelse och för att vara kompatibel med distributionsmodellen för molntjänsten, där Classic UI inte stöds. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk gränssnittsdialogruta (d.v.s. en underordnad dialogrutenod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en underordnad nod). `cq:dialog`
* En komponent med en klassisk dialogruta för användargränssnittsdesign (d.v.s. en design_dialog-nod) måste ha en motsvarande designdialogruta för användargränssnittet (d.v.s. en `cq:design_dialog` underordnad nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för AEM Modernization Tools innehåller dokumentation och verktyg för hur du konverterar komponenter från Classic UI till Touch UI. Mer information finns [i AEM Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) .

### Paketen får inte innehålla blandbart och oföränderligt innehåll {#oakpal-packages-immutable}

**Nyckel**: ImmutableMutableMixedPackage

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

För att vara kompatibel med driftsättningsmodellen för molntjänster måste enskilda innehållspaket innehålla antingen innehåll för de oföränderliga områdena i databasen (d.v.s. inte ändras av kundkoden och orsakar en separat överträdelse) eller det ändringsbara området (d.v.s. allt annat), men inte båda. `/apps and /libs, although /libs` Ett paket som innehåller båda `/apps/myco/components/text and /etc/clientlibs/myco` är till exempel inte kompatibelt med molntjänsten och orsakar att ett problem rapporteras.

Mer information finns i [AEM-projektstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) .

### Omvända replikeringsagenter ska inte användas {#oakpal-reverse-replication}

**Nyckel**: ReverseReplication

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i distributioner av molntjänster, vilket beskrivs i [versionsinformationen: Borttagning av replikeringsagenter](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents).

Kunder som använder omvänd replikering bör kontakta Adobe för att få alternativa lösningar.





