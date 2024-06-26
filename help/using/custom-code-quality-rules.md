---
title: Anpassade regler för kodkvalitet
description: Lär dig mer om de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av testningen av kodkvalitet, baserat på bästa praxis från AEM Engineering.
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 48ae41cb23f6a94fbaf31423f9c5cea3bfd45020
workflow-type: tm+mt
source-wordcount: '3513'
ht-degree: 1%

---


# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

Läs mer om de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av [testning av kodkvalitet,](/help/using/code-quality-testing.md) baserat på bästa praxis från AEM.

>[!NOTE]
>
>Kodexemplen här är endast avsedda som illustrationer. Se [SonarQube&#39;s Concepts-dokumentation](https://docs.sonarqube.org/latest/) för att lära sig mer om dess koncept och kvalitetsregler.

>[!NOTE]
>
>Fullständiga SonarQube-regler kan inte laddas ned på grund av Adobe egna information. Du kan hämta den fullständiga listan med regler [med den här länken.](/help/assets/CodeQuality-rules-latest-AMS.xlsx) Fortsätt läsa det här dokumentet för beskrivningar och exempel på reglerna.

## SonarQube-regler {#sonarqube-rules}

Följande avsnitt innehåller information om SonarQube-regler som körs av Cloud Manager.

### Använd inte potentiellt farliga funktioner {#do-not-use-potentially-dangerous-functions}

* **Nyckel**: CQRules:CWE-676
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Metoderna `Thread.stop()` och `Thread.interrupt()` kan ge upphov till problem som inte går att reproducera och ibland även säkerhetsluckor. Deras användning bör övervakas noggrant och valideras. I allmänhet är meddelandeöverföring ett säkrare sätt att uppnå samma sak.

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

### Använd inte formatsträngar som kan vara externt styrda {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Nyckel**: CQRules:CWE-134
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Om du använder en formatsträng från en extern källa (till exempel en begärandeparameter eller användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

#### Icke-kompatibel kod {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP-begäranden ska alltid ha socket- och anslutningstimeout {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Nyckel**: CQRules:ConnectionTimeoutMechanism
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.6.0

När du kör HTTP-begäranden inifrån ett AEM-program är det viktigt att se till att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr är standardbeteendet för båda Java™:s standard-HTTP-klient, `java.net.HttpUrlConnection`och den vanligaste Apache HTTP Components-klienten är att aldrig timeout, så timeout måste anges explicit. Det bästa sättet är att dessa tidsgränser inte överskrider 60 sekunder.

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

### ResourceResolver-objekt ska alltid stängas {#resourceresolver-objects-should-always-be-closed}

* **Nyckel**: CQRules:CQBP-72
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

`ResourceResolver` objekt som hämtas från `ResourceResolverFactory` förbruka systemresurser. Även om det finns åtgärder för att återkräva dessa resurser när en `ResourceResolver` används inte längre, det är mer effektivt att uttryckligen stänga alla öppna `ResourceResolver` objekt genom att anropa `close()` -metod.

En vanlig missuppfattning är att `ResourceResolver` objekt som skapats med en befintlig JCR-session ska inte stängas explicit eller så stängs den underliggande JCR-sessionen. Detta är inte fallet. Oavsett hur `ResourceResolver` öppnas, ska den stängas när den inte längre används. Sedan `ResourceResolver` implementerar `Closeable` -gränssnittet kan du också använda `try-with-resources` syntax i stället för explicit anrop `close()`.

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

### Använd inte SSLING-serversökvägar för att registrera servrar {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Nyckel**: CQRules:CQBP-75
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Enligt beskrivningen i [Sling-dokumentation](https://sling.apache.org/documentation/the-sling-engine/servlets.html), rekommenderas inte bindningsservrar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Icke-kompatibel kod {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Infångade undantag ska vara antingen loggade eller utlösta, inte båda {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Nyckel**: CQRules:CQBP-44—CatchAndeitherLogOrThrow
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

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

### Undvik loggsatser som följs av Throw-satser {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Nyckel**: CQRules:CQBP-44—ConsecutiousLogAndThrow
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

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

### Undvik inloggning vid INFO vid hantering av GET- eller HEAD-förfrågningar {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och AEM är som standard konfigurerad för att logga på INFO-nivå eller högre. Metoderna GET och HEAD bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. Loggning vid hantering av GET- eller HEAD-begäranden bör finnas antingen på WARN- eller FEL-nivå när något har gått fel eller på DEBUG- eller TRACE-nivå om mer detaljerad felsökningsinformation skulle vara till hjälp.

>[!NOTE]
>
>Detta gäller inte loggning av access.log-typ för varje begäran.

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

* **Nyckel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Kontexten kan också bestämmas med stackspår, men i allmänhet blir loggmeddelandet lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet innehåller det som gick fel medan loggmeddelandet bör användas för att tala om för en loggläsare vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet är fortfarande loggat. Genom att ange ett eget meddelande blir loggarna lättare att förstå.

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

### Loggning in Catch Blocks Should at the WARN or ERROR Level {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Nyckel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som namnet antyder bör Java™-undantag alltid användas i undantagsfall. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp: antingen WARN eller ERROR. Detta garanterar att meddelandena visas korrekt i loggarna.

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

* **Nyckel**: CQRules:CQBP-44—ExceptionPrintStackTrace
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Kontext är viktig när du ska förstå loggmeddelanden. Använda `Exception.printStackTrace()` gör att endast stackspårningen matas ut till standardfelströmmen och förlorar all kontext. I ett program med flera trådar, som AEM om flera undantag skrivs ut med den här metoden parallellt, kan stackspårningarna överlappa vilket kan skapa en betydande förvirring. Undantag bör endast loggas via loggningsramverket.

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

### Utdata inte till standardutdata eller standardfel {#do-not-output-to-standard-output-or-standard-error}

* **Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Loggning AEM alltid ske via loggningsramverket SLF4J. Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket och kan ibland orsaka prestandaproblem.

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

### Undvik hårdkodade/program- och /libs-sökvägar {#avoid-hardcoded-apps-and-libs-paths}

* **Nyckel**: CQRules:CQBP-71
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Vanligtvis banor som börjar med `/libs` och `/apps` ska inte hårdkodas eftersom sökvägarna som de refererar till vanligtvis lagras som sökvägar i förhållande till sökbanan för Sling (som är inställd på `/libs,/apps` som standard). Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

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

* **Nyckel**: CQRules:AMSCORE-554
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Använd inte Sling Scheduler för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Se [Dokumentation för Apache Sling Eventing och Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om du vill veta mer om hur Sling Jobs hanteras i klustrade miljöer.

### AEM inaktuella API:er ska inte användas {#sonarqube-aem-deprecated}

* **Nyckel**: AMSCORE-553
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM API-yta är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

Dessa API:er är ofta föråldrade med Java™-standarden *@Undertryckt* anteckning och, som sådan, identifierad av `squid:CallToDeprecatedMethod`.

Det finns dock fall där en API är föråldrad i sammanhanget för AEM men inte i andra sammanhang. Den här regeln identifierar den andra klassen.

## OakPAL-innehållsregler {#oakpal-rules}

Följande avsnitt innehåller information om de OakPAL-kontroller som körs av Cloud Manager.

>[!NOTE]
>
>OakPAL är ett ramverk som validerar innehållspaket med en fristående Oak-databas. Den utvecklades av en AEM partner och vinnare av 2019 AEM Rockstar North America-priset.

### Produkt-API:er som antecknas med @ProviderType ska inte implementeras eller utökas av kunder {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Nyckel**: CQBP-84
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.7.0

AEM-API:t innehåller Java™-gränssnitt och -klasser som endast är avsedda att användas, men inte implementeras, av anpassad kod. Gränssnittet `com.day.cq.wcm.api.Page` implementeras endast av AEM.

När nya metoder läggs till i dessa gränssnitt påverkar inte dessa ytterligare metoder befintlig kod som använder dessa gränssnitt, och därför anses tillägg av nya metoder i dessa gränssnitt vara bakåtkompatibelt. Men om anpassad kod implementerar ett av dessa gränssnitt har den anpassade koden introducerat en bakåtkompatibilitetsrisk för kunden.

Gränssnitt och klasser som endast är avsedda att implementeras av AEM kommenteras med `org.osgi.annotation.versioning.ProviderType` eller ibland en liknande äldre anteckning `aQute.bnd.annotation.ProviderType`. Den här regeln identifierar de fall där ett sådant gränssnitt implementeras eller en klass utökas av anpassad kod.

#### Icke-kompatibel kod {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Kundpaket får inte skapa eller ändra noder under /libs {#oakpal-customer-package}

* **Nyckel**: BannedPath
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2019.6.0

Det har länge varit en god praxis att `/libs` innehållsträdet i AEM innehållsarkiv ska betraktas som skrivskyddat av kunderna. Ändra noder och egenskaper under `/libs` innebär en betydande risk för större och mindre uppdateringar. Ändringar av `/libs` tillverkas endast av Adobe via officiella kanaler.

### Paket får inte innehålla dubbletter av OSGi-konfigurationer {#oakpal-package-osgi}

* **Nyckel**: DuplicateOsgiConfigurations
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Detta skapar en tvetydighet om vilken konfiguration som kan användas. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge eller en kombination av körningslägen.

#### Icke-kompatibel kod {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Kompatibel kod {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Konfigurations- och installationsmappar får endast innehålla OSGi-noder {#oakpal-config-install}

* **Nyckel**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Av säkerhetsskäl innehåller sökvägar `/config/` och `/install/` kan endast läsas av administrativa användare i AEM och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda namngivna noder `config` i komponentdialogrutor eller när du anger RTF-redigeringskonfigurationen för infogad redigering. För att lösa detta bör den felaktiga noden namnändras till ett kompatibelt namn. För RTF-redigerarkonfigurationen använder du `configPath` -egenskapen på `cq:inplaceEditing` nod som anger den nya platsen.

#### Icke-kompatibel kod {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Kompatibel kod {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Paket får inte överlappa {#oakpal-no-overlap}

* **Nyckel**: PackageOverlaps
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Liknar [Paket får inte innehålla en dubblettregel för OSGi-konfigurationer,](#oakpal-package-osgi)  detta är ett vanligt problem i komplexa projekt där samma nodsökväg skrivs av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara ett klassiskt användargränssnitt {#oakpal-default-authoring}

* **Nyckel**: ClassicUIAuthoringMode
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i AEM. Eftersom det klassiska användargränssnittet har tagits bort sedan AEM 6.4, uppstår nu ett problem när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha gränssnittsdialogrutor med pekskärmar {#oakpal-components-dialogs}

* **Nyckel**: ComponentWithOnlyClassicUIDialog
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM som har en klassisk användargränssnittsdialogruta ska alltid ha en motsvarande användargränssnittsdialogruta för att både tillhandahålla en optimal redigeringsupplevelse och vara kompatibel med distributionsmodellen för Cloud Servicen, där det klassiska användargränssnittet inte stöds. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk användargränssnittsdialogruta (d.v.s. en `dialog` underordnad nod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en `cq:dialog` underordnad nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (dvs. en `design_dialog` nod) måste ha en motsvarande dialogruta för Touch UI-design (d.v.s. en `cq:design_dialog` underordnad nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för AEM finns information och verktyg för hur du konverterar komponenter från det klassiska gränssnittet till Touch-gränssnittet. Se [Dokumentation för AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/) för mer information.

### Omvända replikeringsagenter ska inte användas {#oakpal-reverse-replication}

* **Nyckel**: ReverseReplication
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i distributioner av Cloud Service, vilket beskrivs i [Versionsinformation: Borttagning av replikeringsagenter.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html#replication-agents)

Kunder som använder omvänd replikering bör kontakta Adobe för att få alternativa lösningar.

### Resurser i proxyaktiverade klientbibliotek bör finnas i en mapp med namngivna resurser {#oakpal-resources-proxy}

* **Nyckel**: ClientlibProxyResource
* **Typ**: Fel
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM klientbibliotek kan innehålla statiska resurser som bilder och teckensnitt. Enligt beskrivningen i [Med hjälp av dokumentationen för klientbiblioteken](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html#using-preprocessors) när du använder proxyanslutna klientbibliotek måste dessa statiska resurser finnas i en underordnad mapp med namnet `resources` för att effektivt kunna referera till publiceringsinstanserna.

#### Icke-kompatibel kod {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Kompatibel kod {#compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Användning av Cloud Service som inte är kompatibla arbetsflödesprocesser {#oakpal-usage-cloud-service}

* **Nyckel**: CloudServiceIncompatibleWorkflowProcess
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för bearbetning av tillgångar på AEM Cloud Service har flera arbetsflödesprocesser som användes i anläggningsversioner och AMS-versioner av AEM blivit antingen ostödda eller onödiga.

Migreringsverktyget i [AEM Assets as a Cloud Service GitHub-databas](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller under migrering till AEM as a Cloud Service.

### Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

* **Nyckel**: StaticTemplateUsage
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det har tidigare varit vanligt att använda statiska mallar i AEM projekt, men redigerbara mallar rekommenderas eftersom de ger den flexibilitet och stöder ytterligare funktioner som inte finns i statiska mallar. Mer information finns i [Sidmallar - Redigerbar dokumentation.](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html)

Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [AEM moderniseringsverktyg.](https://opensource.adobe.com/aem-modernize-tools/)

### Användning av äldre Foundation-komponenter rekommenderas inte {#oakpal-usage-legacy}

* **Nyckel**: LegacyFoundationComponentUsage
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

De äldre Foundation Components (dvs. komponenter under `/libs/foundation`) har ersatts i flera AEM versioner till förmån för [Kärnkomponenter.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) Användning av de äldre Foundation-komponenterna som bas för anpassade komponenter, oavsett om det är genom övertäckning eller arv, rekommenderas inte och bör konverteras till motsvarande kärnkomponent.

Den här konverteringen kan underlättas av [AEM moderniseringsverktyg.](https://opensource.adobe.com/aem-modernize-tools/)

### Definitionsnoder för anpassade sökindex måste vara direkt underordnade /oak:index {#oakpal-custom-search}

* **Nyckel**: OakIndexLocation
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (dvs. noder av typen `oak:QueryIndexDefinition`) be direct child nodes of `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med AEM Cloud Service. Mer information om sökindex finns i [Dokumentation för innehållssökning och indexering.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### Definitionsnoder för anpassade sökindex måste ha en compatVersion av 2 {#oakpal-custom-search-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (dvs. noder av typen `oak:QueryIndexDefinition`) måste ha `compatVersion` egenskap inställd på `2`. Alla andra värden stöds inte av AEM Cloud Service. Mer information om sökindex finns i [Dokumentation för innehållssökning och indexering.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### Underordnade noder för anpassade sökindexdefinitionsnoder måste vara av typen nt:ostrukturerad {#oakpal-descendent-nodes}

* **Nyckel**: IndexDescendantNodeType
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Problem som är svåra att felsöka kan uppstå när en anpassad sökindexdefinitionsnod har oordnade underordnade noder. För att undvika detta rekommenderar vi att alla underordnade noder i en `oak:QueryIndexDefinition` noden är av typen `nt:unstructured`.

### Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet indexRules som har underordnade noder {#oakpal-custom-search-index}

* **Nyckel**: IndexRulesNode
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

En korrekt definierad definitionsnod för ett anpassat sökindex måste innehålla en underordnad nod med namnet `indexRules` som i sin tur måste ha minst ett barn. Mer information finns i [Läs dokumentationen.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Definitionsnoder för anpassade sökindex måste följa namngivningskonventioner {#oakpal-custom-search-definitions}

* **Nyckel**: IndexName
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service kräver anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste namnges efter ett specifikt mönster som beskrivs på [Innehållssökning och indexering.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)

### Indexdefinitionsnoder för anpassade sökningar måste använda indextypsklugin  {#oakpal-index-type-lucene}

* **Nyckel**: IndexType
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service kräver att anpassade sökindexdefinitioner (dvs. noder av typen `oak:QueryIndexDefinition`) har en `type` egenskap med värdet inställt på `lucene`. Indexering med äldre indextyper måste uppdateras innan migrering till AEM Cloud Service. Se [Dokumentation för innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) för mer information.

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet seed {#oakpal-property-name-seed}

* **Nyckel**: IndexSeedProperty
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service tillåter inte anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) som innehåller en egenskap med namnet `seed`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud Service. Se [Dokumentation för innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) för mer information.

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet reindex {#oakpal-reindex-property}

* **Nyckel**: IndexReindexProperty
* **Typ**: Kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud Service tillåter inte anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) som innehåller en egenskap med namnet `reindex`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud Service. Se [Dokumentation för innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) för mer information.

### Indexdefinitionsnoder får inte distribueras i UI-innehållspaket {#oakpal-ui-content-package}

* **Nyckel**: IndexNotUnderUIContent
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte anpassade sökindexdefinitioner (noder av typen `oak:QueryIndexDefinition`) från att distribueras i gränssnittets innehållspaket.

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att rörledningar inte fungerar från [Cloud Manager, augusti 2024-utgåvan.](/help/release-notes/current.md)

### Anpassad heltextindexdefinition av typen damAssetLucene måste ha rätt prefix med damAssetLucene {#oakpal-dam-asset-lucene}

* **Nyckel**: CustomFulltextIndexesOfTheDamAssetCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte anpassade fulltextindexdefinitioner av typen `damAssetLucene` från att vara prefix med något annat än `damAssetLucene`.

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att rörledningar inte fungerar från [Cloud Manager, augusti 2024-utgåvan.](/help/release-notes/current.md)

### Indexdefinitionsnoder får inte innehålla egenskaper med samma namn {#oakpal-index-property-name}

* **Nyckel**: DuplicateNameProperty
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) som innehåller egenskaper med samma namn

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att rörledningar inte fungerar från [Cloud Manager, augusti 2024-utgåvan.](/help/release-notes/current.md)

### Det är förbjudet att anpassa vissa OOTB-indexdefinitioner {#oakpal-customizing-ootb-index}

* **Nyckel**: RestrictIndexCustomization
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte obehöriga ändringar av följande OOTB-index:

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att rörledningar inte fungerar från [Cloud Manager, augusti 2024-utgåvan.](/help/release-notes/current.md)

### Konfigurationen av tokenisererna i analysatorerna ska skapas med namnet tokenizer {#oakpal-tokenizer}

* **Nyckel**: AnalyzerTokenizerConfigCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte att tokeniserare med felaktiga namn skapas i analysatorer. Tokenizers bör alltid definieras som `tokenizer`.

## Dispatcher Optimization Tool {#dispatcher-optimization-tool-rules}

I följande avsnitt visas de DOT-kontroller (Dispatcher Optimization Tool) som körs i Cloud Manager. Följ länkarna för varje kontroll för dess GitHub-definition och information.

* [Oväntade token för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [Dispatcher-konfiguration - omatchad offert](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [Dispatcher-konfiguration saknar parentes](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [Extra parentes för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [Dispatcher-konfiguration saknar obligatorisk egenskap](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [Inaktuell egenskap för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [Dispatcher-konfigurationen hittades inte](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [Det gick inte att hitta filen med Httpd-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [Allmän konfiguration för Dispatcher](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [Cacheminnet för Dispatcher-publiceringsservergruppen ska ha serverStaleOnError aktiverat](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [Filtren för publiceringsgrupper för Dispatcher ska innehålla standardreglerna för att neka i 6.x.x-versionen av den AEM typen](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [Statusfilnivåegenskapen för Dispatcher-publiceringsservergruppens cache måste vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [Egenskapen GracePeriod för publiceringsservergruppen för Dispatcher ska vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [Varje Dispatcher-grupp ska ha ett unikt namn](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [Dispatcher-publiceringsservergruppens cache bör ha sina ignoreUrlParams-regler konfigurerade på ett tillåtelselista-sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [Filtren för publiceringsgruppen Dispatcher ska ange tillåtna Sling-väljare på ett tillåtelselista-sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [Filtren för publiceringsgruppen Dispatcher ska ange tillåtna Sling-suffixmönster på ett tillåtelselista-sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [Använd inte direktivet Kräv alla beviljade i ett VirtualHost-katalogavsnitt med en rotkatalogsökväg](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
