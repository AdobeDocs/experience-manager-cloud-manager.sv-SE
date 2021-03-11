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
source-git-commit: b5233e1932888b515d8dc26a6493cbd26686bc3c
workflow-type: tm+mt
source-wordcount: '3622'
ht-degree: 4%

---


# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager och som baseras på de bästa metoderna från AEM.

>[!NOTE]
>De kodexempel som anges här är endast avsedda som illustrationer. Mer information om SonarQube-koncept och kvalitetsregler finns i [Concepts](https://docs.sonarqube.org/7.4/user-guide/concepts/).

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

När du kör HTTP-begäranden inifrån ett AEM-program är det viktigt att se till att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr är standardbeteendet för både Java:s standard-HTTP-klient (java.net.HttpUrlConnection) och den vanligaste Apache HTTP Components-klienten att aldrig timeout, så timeout måste anges explicit. Dessutom bör dessa timeout inte vara längre än 60 sekunder.

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

Gränssnitt (och klasser) som endast är avsedda att implementeras av AEM kommenteras med *org.osgi.annotation.versioning.ProviderType* (eller, i vissa fall, en liknande äldre anteckning *Qute.bnd.annotation.ProviderType*). Den här regeln identifierar de fall där ett sådant gränssnitt implementeras (eller där en klass utökas) med anpassad kod.

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

Så som beskrivs i [Sling-dokumentationen](http://sling.apache.org/documentation/the-sling-engine/servlets.html) rekommenderas inte bindningsservrar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Icke-kompatibel kod {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Undantag som fångats upp ska loggas eller kastas, men inte både {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

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

### Undvik att ha en loggsats som omedelbart följs av en throw-sats {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

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

### Undvik att logga vid INFO när du hanterar förfrågningar från GET eller HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och AEM är som standard konfigurerad för att logga på INFO-nivå eller högre. Metoderna GET och HEAD bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. Loggning vid hantering av GET- eller HEAD-begäranden bör finnas antingen på WARN- eller FEL-nivå när något har gått fel eller på DEBUG- eller TRACE-nivå om mer detaljerad felsökningsinformation skulle vara till hjälp.

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

Java-undantag ska alltid användas i *exceptionella*-situationer, vilket namnet föreslår. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp - antingen WARN eller ERROR. Detta garanterar att meddelandena visas korrekt i loggarna.

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

Som vi nämnt är sammanhang viktigt när du ska förstå loggmeddelanden. Om du använder Exception.printStackTrace() genereras **endast** stackspårningen som utdata till standardfelströmmen och därmed förlorar all kontext. I ett program med flera trådar, som AEM om flera undantag skrivs ut med den här metoden parallellt, kan stackspårningarna överlappa vilket kan skapa en betydande förvirring. Undantag bör endast loggas via loggningsramverket.

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

### Exportera inte till standardutdata eller standardfel {#do-not-output-to-standard-output-or-standard-error}

**Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2018.4.0

Loggning AEM alltid ske via loggningsramverket (SLF4J). Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket och kan i vissa fall orsaka prestandaproblem.

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

### Undvik hårdkodade /appar och /libs-sökvägar {#avoid-hardcoded-apps-and-libs-paths}

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

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

Sling Scheduler får inte användas för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Läs [Apache Sling Eventing och Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om du vill veta mer om hur Sling-jobb hanteras i klustrade miljöer.

### AEM inaktuella API:er ska inte användas {#sonarqube-aem-deprecated}

**Nyckel**: AMSCORE-553

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

AEM API-yta är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

I många fall är dessa API:er föråldrade med Java-standardanteckningen *@Undertryckt* och, som sådana, enligt `squid:CallToDeprecatedMethod`.

Det finns emellertid fall där ett API är inaktuellt i AEM men inte i andra sammanhang. Den här regeln identifierar den andra klassen.

## OakPAL-innehållsregler {#oakpal-rules}

Nedan finns de OakPAL-kontroller som körs av Cloud Manager.

>[!NOTE]
>
>OakPAL är ett ramverk som utvecklats av en AEM partner (och vinnare av 2019 AEM Rockstar North America) som validerar innehållspaket med en fristående Oak-databas.

### Kundpaket ska inte skapa eller ändra noder under /libs {#oakpal-customer-package}

**Nyckel**: BannedPaths

**Typ**: Fel

**Allvarlighetsgrad**: Blockera

**Sedan**: Version 2019.6.0

Det har varit en god praxis sedan länge att innehållsträdet /libs i AEM ska betraktas som skrivskyddat av kunderna. Att ändra noder och egenskaper under */libs* skapar en betydande risk för större och mindre uppdateringar. Ändringar av */libs* ska endast göras av Adobe via officiella kanaler.

### Paket får inte innehålla dubbletter av OSGi-konfigurationer {#oakpal-package-osgi}

**Nyckel**: DuplicateOsgiConfigurations

**Typ**: Fel

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Detta skapar en tvetydighet om vilken konfiguration som kan användas. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge (eller en kombination av körningslägen).

#### Icke-kompatibel kod {#non-compliant-code-osgi}

```
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Kompatibel kod {#compliant-code-osgi}

```
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Konfigurations- och installationsmappar får endast innehålla OSGi-noder {#oakpal-config-install}

**Nyckel**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Typ**: Fel

**Allvarlighetsgrad**: Viktigt

**Sedan**: Version 2019.6.0

Av säkerhetsskäl kan sökvägar som innehåller */config/ och /install/* bara läsas av administrationsanvändare i AEM och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda noder med namnet `config` i komponentdialogrutor eller när du anger RTF-redigerarkonfigurationen för infogad redigering. För att lösa detta bör den felande noden byta namn till ett kompatibelt namn. Använd egenskapen `configPath` på noden `cq:inplaceEditing` för att ange den nya platsen för konfigurationen av textredigeraren.

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

På samma sätt som *Paket ska inte innehålla dubbletter av OSGi-konfigurationer* är detta ett vanligt problem i komplexa projekt där samma nodsökväg skrivs till av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara klassiskt användargränssnitt {#oakpal-default-authoring}

**Nyckel**: KlassisktUIAuthoringMode

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i AEM. Eftersom det klassiska användargränssnittet har tagits bort sedan AEM 6.4 kommer ett problem nu att uppstå när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha Touch UI-dialogrutor {#oakpal-components-dialogs}

**Nyckel**: ComponentWithOnlyClassicUIDialog

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

AEM som har en klassisk användargränssnittsdialogruta ska alltid ha en motsvarande användargränssnittsdialogruta för att både tillhandahålla en optimal redigeringsupplevelse och vara kompatibel med distributionsmodellen för Cloud Servicen, där det klassiska användargränssnittet inte stöds. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk gränssnittsdialogruta (d.v.s. en underordnad dialogrutenod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en underordnad `cq:dialog`-nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (d.v.s. en design_dialog-nod) måste ha en motsvarande dialogruta för användargränssnittsdesign (d.v.s. en `cq:design_dialog`-underordnad nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för AEM Moderniseringsverktyg innehåller dokumentation och verktyg för hur du konverterar komponenter från det klassiska gränssnittet till Touch-gränssnittet. Mer information finns i [Verktygen för AEM (a1/>).](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html)

### Paket får inte blandas med muterbart och oföränderligt innehåll {#oakpal-packages-immutable}

**Nyckel**: ImmutableMutableMixedPackage

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

För att vara kompatibel med databasens distributionsmodell måste enskilda innehållspaket innehålla antingen innehåll för de oföränderliga områdena i databasen (d.v.s. `/apps and /libs, although /libs` ska inte ändras av kundkoden och orsaka en separat överträdelse) eller det ändringsbara området (d.v.s. allt annat), men inte båda. Ett paket som innehåller både `/apps/myco/components/text and /etc/clientlibs/myco` är till exempel inte kompatibelt med Cloud Service och orsakar att ett problem rapporteras.

Mer information finns i [AEM projektstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html).

### Omvända replikeringsagenter ska inte användas {#oakpal-reverse-replication}

**Nyckel**: ReverseReplication

**Typ**: Kompatibilitet med kodmeddelanden/Cloud Service

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i distributioner av Cloud Service, vilket beskrivs i [Versionsinformation: Borttagning av replikeringsagenter](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents).

Kunder som använder omvänd replikering bör kontakta Adobe för att få alternativa lösningar.

### OakPAL - Resurser i proxyaktiverade klientbibliotek ska finnas i en mapp med namnet resources {#oakpal-resources-proxy}

**Nyckel**: ClientlibProxyResource

**Typ**: Fel

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM klientbibliotek kan innehålla statiska resurser som bilder och teckensnitt. Så som beskrivs i [Använda preprocessorer](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=en#using-preprocessors), måste dessa statiska resurser finnas i en underordnad mapp med namnet resources för att effektivt kunna refereras till på publiceringsinstanserna när proxierade klientbibliotek används.

#### Icke-kompatibel kod {#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Kompatibel kod {#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL - Användning av Cloud Service-inkompatibla arbetsflödesprocesser {#oakpal-usage-cloud-service}

**Nyckel**: CloudServiceIncompatibleWorkflowProcess

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för tillgångsbearbetning på AEM Cloud Service har flera arbetsflödesprocesser som användes på plats och i AMS-versioner av AEM blivit antingen ostödda eller onödiga. Migreringsverktyget på [aem-cloud-migration](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller vid migrering AEM Cloud Servicen.

### OakPAL - Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

**Nyckel**: StaticTemplateUsage

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

Det har tidigare varit mycket vanligt att använda statiska mallar i AEM projekt, men redigerbara mallar rekommenderas eftersom de ger den flexibilitet och stöder ytterligare funktioner som inte finns i statiska mallar. Mer information finns i [Sidmallar - Redigerbar](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html?lang=en). Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL - Användning av äldre Foundation-komponenter rekommenderas inte {#oakpal-usage-legacy}

**Nyckel**: LegacyFoundationComponentUsage

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

De äldre grundkomponenterna (d.v.s. komponenter under `/libs/foundation`) har ersatts för flera AEM-versioner till förmån för WCM Core Components. Användning av de äldre grundkomponenterna som grund för anpassade komponenter, oavsett om det är genom övertäckning eller arv, rekommenderas inte och bör konverteras till motsvarande kärnkomponent. Konverteringen kan underlättas med [AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL - Endast körlägesnamn och -ordning som stöds ska användas {#oakpal-supported-runmodes}

**Nyckel**: SupportedRunmode

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service använder en strikt namngivningsprincip för körningslägesnamn och en strikt ordning för dessa körningslägen. En lista över körningslägen som stöds finns på [Runmodes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes) och eventuella avvikelser från detta identifieras som ett problem.

### OakPAL - Definitionsnoder för anpassade sökindex måste vara direkt underordnade /oak:index {#oakpal-custom-search}

**Nyckel**: OakIndexLocation

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen oak:QueryIndexDefinition) är direkta underordnade noder till `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med AEM Cloud Service. Mer information om sökindex finns i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL - Definitionsnoder för anpassade sökindex måste ha en compatVersion på 2 {#oakpal-custom-search-compatVersion}

**Nyckel**: IndexCompatVersion

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen oak:QueryIndexDefinition) måste ha egenskapen compatVersion inställd på 2. Andra värden stöds inte av AEM Cloud Service. Mer information om sökindex finns i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL - Beroende noder för anpassade sökindexdefinitionsnoder måste vara av typen nt:undefined {#oakpal-descendent-nodes}

**Nyckel**: IndexDescendantNodeType

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

Det är svårt att felsöka problem när en anpassad sökindexdefinitionsnod har oordnade underordnade noder. För att undvika dessa bör alla underordnade noder för en `oak:QueryIndexDefinition`-nod vara av typen nt:undefined.

### OakPAL - Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet indexRules som har underordnade {#oakpal-custom-search-index}

**Nyckel**: IndexRulesNode

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

En korrekt definierad definitionsnod för ett anpassat sökindex måste innehålla en underordnad nod med namnet indexRules som i sin tur måste ha minst en underordnad nod. Mer information finns i [Oak Documentation](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### OakPAL - Definitionsnoder för anpassade sökindex måste följa namngivningskonventioner {#oakpal-custom-search-definitions}

**Nyckel**: IndexName

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste namnges efter ett specifikt mönster som beskrivs i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL - Definitionsnoder för anpassade sökindex måste använda indextyplucen {#oakpal-index-type-lucene}

**Nyckel**: IndexType

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen oak:QueryIndexDefinition) har en type-egenskap med värdet **lucene**. Indexering med äldre indextyper måste uppdateras innan migrering till AEM Cloud Service. Mer information finns i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL - Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet seed {#oakpal-property-name-seed}

**Nyckel**: IndexSeedProperty

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller en egenskap med namnet seed. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud Service. Mer information finns i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL - Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet reindex {#oakpal-reindex-property}

**Nyckel**: IndexReindexProperty

**Typ**: Code Smell

**Allvarlighetsgrad**: Mindre

**Sedan**: Version 2021.2.0

AEM Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskapen reindex. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud Service. Mer information finns i [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

## Dispatcher Optimization Tool {#dispatcher-optimization-tool-rules}

I följande avsnitt beskrivs de DOT-kontroller som körs av Cloud Manager:

* [DOT - Tolkningsfel - Dispatcher-konfiguration Oväntade token](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [DOT - Tolkningsfel - Dispatcher-konfiguration omatchad offert](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [DOT - Tolkningsfel - Dispatcher-konfiguration saknar parentes](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [DOT - Tolkningsfel - Dispatcher Configuration Extra Brace](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [DOT - Tolkningsfel - Dispatcher-konfiguration saknar obligatorisk egenskap](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [DOT - Tolkningsfel - inaktuell egenskap för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [DOT - Tolkningsfel - Dispatcher-konfigurationen hittades inte](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [DOT - Tolkningsfel - HTTP-konfiguration Inkluderingsfil hittades inte](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [DOT - Analysfel - Dispatcher-konfiguration allmän](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [DOT - Dispatcher-publiceringsgruppens cache ska ha serverStaleOnError aktiverat](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [DOT - Dispatcher-filtren för publiceringsgrupper ska innehålla standardreglerna för att neka i 6.x.x-versionen av den AEM arkivtypen](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [DOT - Statusnivåegenskapen för Dispatcher-publiceringsservergruppens cache ska vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [DOT - Egenskapen GracePeriod för publiceringsservergruppen för Dispatcher ska vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [DOT - Varje Dispatcher-servergrupp ska ha ett unikt namn](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [DOT - Dispatcher-publiceringsservergruppens cache ska ha sina ignoreUrlParams-regler konfigurerade på tillåtelselista](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [DOT - Dispatcher-filtren för publiceringsgrupper ska ange tillåtna Sling-väljare på tillåtelselista-sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [DOT - Dispatcher-filtren för publiceringsgrupper ska ange tillåtna Sling-suffixmönster på tillåtelselista sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [DOT - Direktivet Kräv alla beviljade ska inte användas i ett VirtualHost-katalogavsnitt med en rotkatalogsökväg](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)

