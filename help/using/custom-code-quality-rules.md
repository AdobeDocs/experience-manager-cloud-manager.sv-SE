---
title: Anpassade regler för kodkvalitet
description: Upptäck detaljerna i de anpassade regler för kodkvalitet som körs av Cloud Manager vid kvalitetstestning av kod. Dessa regler bygger på god praxis från AEM Engineering.
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 8388edb5510ed4583a7bc703f3781af03d976948
workflow-type: tm+mt
source-wordcount: '3644'
ht-degree: 0%

---


# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

Läs mer om de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av [kodkvalitetstestningen](/help/using/code-quality-testing.md), baserat på bästa praxis från AEM Engineering.

>[!NOTE]
>
>Kodexemplen här är endast avsedda som illustrationer. Mer information om koncept och kvalitetsregler finns i [SonarQube&#39;s Concepts-dokumentationen](https://docs.sonarsource.com/sonarqube-server/latest/).

Fullständiga SonarQube-regler kan inte laddas ned på grund av Adobe egna information. Du kan hämta den fullständiga listan med regler [med den här länken](/help/assets/CodeQuality-rules-latest-AMS.xlsx). Fortsätt läsa det här dokumentet för beskrivningar och exempel på reglerna.

>[!IMPORTANT]
>
>Från och med torsdagen den 13 februari 2025 (Cloud Manager 2025.2.0) använder Cloud Manager Code Quality en uppdaterad version av SonarQube 9.9 och en uppdaterad lista över regler som du kan [hämta här](/help/assets/CodeQuality-rules-latest-AMS-2024-12-0.xlsx).

## SonarQube-regler {#sonarqube-rules}

Följande avsnitt innehåller information om SonarQube-regler som körs av Cloud Manager.

### Använd inte potentiellt farliga funktioner {#do-not-use-potentially-dangerous-functions}

* **Nyckel**: CQRules:CWE-676
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Metoderna `Thread.stop()` och `Thread.interrupt()` kan skapa problem som är svåra att återge och ibland säkerhetsproblem. Deras användning bör övervakas noggrant och valideras. I allmänhet är meddelandeöverföring ett säkrare sätt att uppnå samma sak.

#### Kod som inte uppfyller kraven {#non-compliant-code}

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

* **Nyckel**: CQRules:CWE-134
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Om du använder en formatsträng från en extern källa (till exempel en begärandeparameter eller användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

#### Kod som inte uppfyller kraven {#non-compliant-code-1}

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

När HTTP-begäranden körs inifrån ett AEM-program är det viktigt att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr har varken Java™ standardklient för HTTP, `java.net.HttpUrlConnection` eller den vanliga Apache HTTP Components-klienten någon standardtimeout. Därför måste timeout konfigureras explicit. Det bästa sättet är att dessa tidsgränser inte överskrider 60 sekunder.

#### Kod som inte uppfyller kraven {#non-compliant-code-2}

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

### Objekten `ResourceResolver` ska alltid stängas {#resourceresolver-objects-should-always-be-closed}

* **Nyckel**: CQRules:CQBP-72
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

`ResourceResolver` objekt som hämtats från `ResourceResolverFactory` använder systemresurser. Även om det finns åtgärder för att återta dessa resurser när `ResourceResolver` inte längre används, är det mer effektivt att stänga öppna `ResourceResolver`-objekt explicit genom att anropa metoden `close()`.

En vanlig missuppfattning är att `ResourceResolver` objekt som skapats med en befintlig JCR-session inte ska stängas explicit. En annan missuppfattning är att när du stänger dessa objekt stängs den underliggande JCR-sessionen. Så är inte fallet. Oavsett hur en `ResourceResolver` öppnas bör den stängas när den inte längre används. Eftersom `ResourceResolver` implementerar gränssnittet `Closeable` går det också att använda syntaxen `try-with-resources` i stället för att anropa `close()` explicit.

#### Kod som inte uppfyller kraven {#non-compliant-code-4}

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

### Använd inte slingserversökvägar för att registrera servrar {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Nyckel**: CQRules:CQBP-75
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Så som beskrivs i [Sling-dokumentationen](https://sling.apache.org/documentation/the-sling-engine/servlets.html) rekommenderas inte bindningsservrar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Kod som inte uppfyller kraven {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Undantag som fångas upp ska loggas eller kastas, inte båda {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Nyckel**: CQRules:CQBP-44—CatchAndeitherLogOrThrow
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

I allmänhet bör ett undantag loggas exakt en gång. Loggningsundantag kan orsaka förvirring eftersom det är oklart hur många gånger ett undantag inträffade. Det vanligaste mönstret som leder till det här problemet är loggning och generering av ett fångat undantag.

#### Kod som inte uppfyller kraven {#non-compliant-code-6}

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

### Undvik loggsatser som följs av throw-satser {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Nyckel**: CQRules:CQBP-44 - ConsecutiousLogAndThrow
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Ett annat vanligt sätt att undvika är att logga ett meddelande och sedan omedelbart generera ett undantag. Det här problemet tyder vanligtvis på att undantagsmeddelandet kommer att dupliceras i loggfiler.

#### Kod som inte uppfyller kraven {#non-compliant-code-7}

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

### Undvik att logga in på INFO när du hanterar förfrågningar från GET eller HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och som standard är AEM konfigurerat för att logga på INFO-nivå eller högre. GET- och HEAD-metoder bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. När du hanterar GET- eller HEAD-begäranden ska loggningen vara på WARN- eller ERROR-nivå om något har gått fel. Mer detaljerad felsökningsinformation finns i loggningen på nivån DEBUG eller TRACE.

>[!NOTE]
>
>Det här arbetsflödet gäller inte loggning av access.log-typ för varje begäran.

#### Kod som inte uppfyller kraven {#non-compliant-code-8}

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

### Använd inte `Exception.getMessage()` som den första parametern i en loggningssats {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Nyckel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Kontexten kan också bestämmas med stackspår, men i allmänhet blir loggmeddelandet lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet ska innehålla detaljerad information om vad som gick fel. Loggmeddelandet bör däremot informera läsaren om vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet är fortfarande loggat. Genom att ange ett eget meddelande blir loggarna lättare att förstå.

#### Kod som inte uppfyller kraven {#non-compliant-code-9}

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

* **Nyckel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som namnet antyder bör Java™-undantag alltid användas i undantagsfall. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp: antingen WARN eller ERROR. På så sätt ser du till att meddelandena visas korrekt i loggarna.

#### Kod som inte uppfyller kraven {#non-compliant-code-10}

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
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Kontext är viktig när du ska förstå loggmeddelanden. Om `Exception.printStackTrace()` används kommer endast stackspårningen att skickas till standardfelströmmen, vilket innebär att all kontext förloras. Om flera undantag skrivs ut med den här metoden parallellt i ett program med flera trådar, som AEM, kan stackspårningarna överlappa, vilket kan skapa stor förvirring. Undantag bör endast loggas via loggningsramverket.

#### Kod som inte uppfyller kraven {#non-compliant-code-11}

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

* **Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Loggning i AEM ska alltid göras via loggningsramverket SLF4J. Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket och kan ibland orsaka prestandaproblem.

#### Kod som inte uppfyller kraven {#non-compliant-code-12}

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

### Undvik hårdkodade `/apps`- och `/libs`-sökvägar {#avoid-hardcoded-apps-and-libs-paths}

* **Nyckel**: CQRules:CQBP-71
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Banor som börjar med `/libs` och `/apps` bör vanligtvis inte hårdkodas. Dessa sökvägar lagras vanligtvis i förhållande till sökvägen till Sling, som har standardvärdet `/libs,/apps`. Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

#### Kod som inte uppfyller kraven {#non-compliant-code-13}

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
* **Typ**: `Code Smell` / Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Använd inte Sling Scheduler för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Läs [dokumentationen om Apache Sling-händelser och jobbhantering](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om du vill veta mer om hur Sling-jobb hanteras i klustrade miljöer.

### API:er som inte används av AEM bör inte användas {#sonarqube-aem-deprecated}

* **Nyckel**: AMSCORE-553
* **Typ**: `Code Smell` / Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM API-yta är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

Dessa API:er är ofta föråldrade med Java™-standardanteckningen *@Deprecated* och identifieras därför av `squid:CallToDeprecatedMethod`.

Det finns dock fall där en API är inaktuell i AEM-sammanhang men inte kan bli inaktuell i andra sammanhang. Den här regeln identifierar den andra klassen.

## OakPAL-innehållsregler {#oakpal-rules}

I följande avsnitt beskrivs de OakPAL-kontroller som utförs av Cloud Manager.

>[!NOTE]
>
>OakPAL är ett ramverk som validerar innehållspaket med en fristående Oak-databas. En AEM-partner och en vinnare av 2019 års AEM Rock Star North America-utmärkelse utvecklade den.

### Kunder bör inte implementera eller utöka produkt-API:er som kommenteras med @ProviderType {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Nyckel**: CQBP-84
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.7.0

AEM-API:t innehåller Java™-gränssnitt och -klasser som endast är avsedda att användas, men inte implementeras, av anpassad kod. Det är till exempel bara AEM som implementerar gränssnittet `com.day.cq.wcm.api.Page`.

Om du lägger till nya metoder i dessa gränssnitt påverkas inte befintlig kod, vilket gör att nya metoder kan läggas till baklänges. Men om anpassad kod implementerar ett av dessa gränssnitt har den anpassade koden introducerat en bakåtkompatibilitetsrisk för kunden.

AEM kommenterar gränssnitt och klasser som endast är avsedda för implementering med `org.osgi.annotation.versioning.ProviderType` eller, ibland, den gamla anteckningen `aQute.bnd.annotation.ProviderType`. Den här regeln identifierar instanser där anpassad kod implementerar ett sådant gränssnitt eller utökar en klass.

#### Kod som inte uppfyller kraven {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Kundpaket ska inte skapa eller redigera noder under `/libs` {#oakpal-customer-package}

* **Nyckel**: BannedPath
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2019.6.0

Det har varit en god vana att innehållsträdet `/libs` i AEM-innehållsarkivet alltid ska betraktas som skrivskyddat av kunder. Att ändra noder och egenskaper under `/libs` innebär en betydande risk för större och mindre uppdateringar. Ändringar i `/libs` görs endast av Adobe via officiella kanaler.

### Paket får inte innehålla dubbla OSGi-konfigurationer {#oakpal-package-osgi}

* **Nyckel**: DuplicateOsgiConfigurations
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Det här problemet skapar en tvetydighet om vilken konfiguration som kan användas. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge eller en kombination av körningslägen.

#### Kod som inte uppfyller kraven {#non-compliant-code-osgi}

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

Av säkerhetsskäl kan sökvägar som innehåller `/config/` och `/install/` bara läsas av administrationsanvändare i AEM och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller de här segmenten, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda noder med namnet `config` i komponentdialogrutor eller när du anger RTF-redigerarkonfigurationen för intern redigering. För att lösa det här problemet bör namnet på den felande noden ändras till ett kompatibelt namn. Använd egenskapen `configPath` på noden `cq:inplaceEditing` för att ange den nya platsen för RTF-redigerarkonfigurationen.

#### Kod som inte uppfyller kraven {#non-compliant-code-config-install}

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

Ungefär som [Paket får inte innehålla regeln för duplicerade OSGi-konfigurationer](#oakpal-package-osgi) är det här problemet ett vanligt problem i komplexa projekt där samma nodsökväg skrivs av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara Classic UI {#oakpal-default-authoring}

* **Nyckel**: ClassicUIAuthoringMode
* **Typ**: `Code Smell` / Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i AEM. Eftersom det klassiska användargränssnittet har tagits bort sedan AEM 6.4 uppstår nu ett problem när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha dialogrutor för användargränssnitt med pekfunktioner {#oakpal-components-dialogs}

* **Nyckel**: ComponentWithOnlyClassicUIDialog
* **Typ**: `Code Smell` / Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM-komponenter med en klassisk gränssnittsdialogruta bör också ha en Touch-dialogruta för optimal redigering och kompatibilitet med Cloud Service distributionsmodell, som inte stöder Classic UI. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk gränssnittsdialogruta (d.v.s. en underordnad `dialog`-nod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en underordnad `cq:dialog`-nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (d.v.s. en `design_dialog`-nod) måste ha en motsvarande designdialogruta för användargränssnittet (d.v.s. en underordnad `cq:design_dialog`-nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för AEM Moderniseringsverktyg innehåller information om och verktyg för hur du konverterar komponenter från det klassiska användargränssnittet till Touch-användargränssnittet. Mer information finns i [dokumentationen för AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### Omvända replikeringsagenter ska inte användas {#oakpal-reverse-replication}

* **Nyckel**: ReverseReplication
* **Typ**: `Code Smell` / Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i Cloud Service-distributioner, vilket beskrivs i [Versionsinformation: Borttagning av replikeringsagenter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes#replication-agents).

Kunder som använder omvänd replikering bör kontakta Adobe för alternativa lösningar.

### Resurser i proxyaktiverade klientbibliotek bör finnas i en mapp med namnet resources {#oakpal-resources-proxy}

* **Nyckel**: ClientlibProxyResource
* **Typ**: Fel
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM klientbibliotek kan innehålla statiska resurser som bilder och teckensnitt. Så som beskrivs i [Använda dokumentationen för klientbibliotek](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/introduction/clientlibs#using-preprocessors) måste dessa statiska resurser finnas i en underordnad mapp med namnet `resources` när du använder proxiderade klientbibliotek för att effektivt kunna refereras till på publiceringsinstanserna.

#### Kod som inte uppfyller kraven {#non-compliant-proxy-enabled}

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

### Användning av Cloud Service inkompatibla arbetsflöden {#oakpal-usage-cloud-service}

* **Nyckel**: CloudServiceIncompatibleWorkflowProcess
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för bearbetning av resurser i AEM Cloud-tjänsten har flera arbetsflödesprocesser som användes i lokala versioner och AMS-versioner av AEM antingen blivit ostödda eller onödiga.

Migreringsverktyget i [AEM Assets as a Cloud Service GitHub-databasen](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller under migrering till AEM as a Cloud Service.

### Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

* **Nyckel**: StaticTemplateUsage
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det har tidigare varit vanligt att använda statiska mallar i AEM Projects, men redigerbara mallar rekommenderas eftersom de ger den flexibilitet och stöd för ytterligare funktioner som inte finns i statiska mallar. Mer information finns i [Sidmallar - redigerbar dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/platform/templates/page-templates-editable).

Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### Användning av äldre baskomponenter rekommenderas inte {#oakpal-usage-legacy}

* **Nyckel**: LegacyFoundationComponentUsage
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

De äldre Foundation-komponenterna (d.v.s. komponenterna under `/libs/foundation`) har ersatts för flera AEM-versioner till förmån för [Core Components](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/introduction). Användning av de äldre Foundation-komponenterna som bas för anpassade komponenter, oavsett om det är genom övertäckning eller arv, rekommenderas inte och bör konverteras till motsvarande kärnkomponent.

[AEM moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/) kan underlätta den här konverteringen.

### Definitionsnoder för anpassade sökindex måste vara direkt underordnade `/oak:index` {#oakpal-custom-search}

* **Nyckel**: OakIndexLocation
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) är direkt underordnade noder till `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med AEM Cloud-tjänsten. Mer information om sökindex finns i [dokumentationen för innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing).

### Definitionsnoder för anpassade sökindex måste ha en compatVersion av 2 {#oakpal-custom-search-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste ha egenskapen `compatVersion` inställd på `2`. AEM Cloud-tjänsten stöder inte något annat värde. Mer information om sökindex finns i [dokumentationen för innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing).

### Underordnade noder för definitionsnoder för anpassade sökindex måste vara av typen `nt:unstructured` {#oakpal-descendent-nodes}

* **Nyckel**: IndexDescendantNodeType
* **Typ**: `Code Smell`
* **&#x200B;**&#x200B;Allvarlighetsgrad: Mindre
* **Sedan**: Version 2021.2.0

Problem som är svåra att felsöka kan uppstå när en definitionsnod för anpassat sökindex har osorterade underordnade noder. För att undvika sådana noder rekommenderar Adobe att alla underordnade noder till en `oak:QueryIndexDefinition` nod är av typen `nt:unstructured`.

### Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet `indexRules` som har underordnade noder {#oakpal-custom-search-index}

* **Nyckel**: IndexRulesNode
* **Typ**: `Code Smell`
* **&#x200B;**&#x200B;Allvarlighetsgrad: Mindre
* **Sedan**: Version 2021.2.0

En korrekt definierad anpassad sökindexdefinitionsnod måste innehålla en underordnad nod med namnet `indexRules` och den här noden måste ha minst en underordnad nod. Mer information finns i [Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Definitionsnoder för anpassade sökindex måste följa namnkonventioner {#oakpal-custom-search-definitions}

* **Nyckel**: IndexName
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste namnges efter ett specifikt mönster som beskrivs i [Innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing#how-to-use).

### Definitionsnoder för anpassade sökindex måste använda indextypen lucen {#oakpal-index-type-lucene}

* **Nyckel**: IndexType
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) har en `type` -egenskap med värdet `lucene`. Indexering med äldre indextyper måste uppdateras före migrering till AEM Cloud-tjänsten. Mer information finns i [dokumentationen för innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla egenskapen `seed` {#oakpal-property-name-seed}

* **Nyckel**: IndexSeedProperty
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller en egenskap med namnet `seed`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud-tjänsten. Mer information finns i [dokumentationen för innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla egenskapen `reindex` {#oakpal-reindex-property}

* **Nyckel**: IndexReindexProperty
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller en egenskap med namnet `reindex`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM Cloud-tjänsten. Mer information finns i [dokumentationen för innehållssökning och indexering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/indexing#how-to-use).

### Indexdefinitionsnoder får inte distribueras i UI-innehållspaket {#oakpal-ui-content-package}

* **Nyckel**: IndexNotUnderUIContent
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (noder av typen `oak:QueryIndexDefinition`) distribueras i UI-innehållspaketet.

>[!WARNING]
>
>Du uppmanas att åtgärda det här problemet så snart som möjligt eftersom det kan orsaka att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/release-notes/current.md).

### Anpassad heltextindexdefinition av typen `damAssetLucene` måste ha rätt prefix med `damAssetLucene` {#oakpal-dam-asset-lucene}

* **Nyckel**: CustomFulltextIndexesOfTheDamAssetCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten förhindrar att anpassade fulltextindexdefinitioner av typen `damAssetLucene` prefix med något annat än `damAssetLucene`.

>[!WARNING]
>
>Du uppmanas att åtgärda det här problemet så snart som möjligt eftersom det kan orsaka att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/release-notes/current.md).

### Indexdefinitionsnoder får inte innehålla egenskaper med samma namn {#oakpal-index-property-name}

* **Nyckel**: DuplicateNameProperty
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskaper med samma namn

>[!WARNING]
>
>Du uppmanas att åtgärda det här problemet så snart som möjligt eftersom det kan leda till att pipelines misslyckas från och med augusti 2024-versionen[&#128279;](/help/release-notes/current.md) av Cloud Manager.

### Det är förbjudet att anpassa vissa färdiga indexdefinitioner {#oakpal-customizing-ootb-index}

* **Nyckel**: RestrictIndexCustomization
* **Typ**: Förbättring
* **&#x200B;**&#x200B;Allvarlighetsgrad: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte obehöriga ändringar av följande OTB-index:

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>Du uppmanas att åtgärda det här problemet så snart som möjligt eftersom det kan leda till att pipelines misslyckas från och med augusti 2024-versionen[&#128279;](/help/release-notes/current.md) av Cloud Manager.

### Konfigurationen av tokeniserare i analysverktyg ska skapas med namnet `tokenizer` {#oakpal-tokenizer}

* **Nyckel**: AnalyzerTokenizerConfigCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

Tjänsten AEM Cloud tillåter inte att tokeniserare med felaktiga namn skapas i analysatorer. Tokenizers ska alltid definieras som `tokenizer`.

### Konfiguration av indexeringsdefinitioner får inte innehålla blanksteg {#oakpal-indexing-definitions-spaces}

* **Nyckel**: PathSpacesCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.7.0

AEM Cloud-tjänsten tillåter inte skapande av indexeringsdefinitioner som innehåller egenskaper med mellanslag.

### Konfiguration av indexeringsdefinitioner får inte innehålla egenskapen haystack0 {#oakpal-indexing-haystack0-property}

* **Nyckel**: HayStackPropertyCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.12.0

AEM Cloud-tjänsten tillåter inte skapande av indexeringsdefinitioner som innehåller höstacksegenskaper.

### Konfiguration av indexeringsdefinitioner får inte innehålla egenskapen: async-previous {#oakpal-indexing-unsupported-async-properties}

* **Nyckel**: IndexUnsupportedAsyncPropertiesCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2025.3.0

AEM Cloud-tjänsten tillåter inte att indexeringsdefinitioner med asynkrona egenskaper som inte stöds skapas.

### Konfiguration av indexeringsdefinitioner bör inte ha samma tagg i flera index {#oakpal-indexing-same-tag-multiple-indexes}

* **Nyckel**: SameTagInMultipleIndex
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2025.3.0

I tjänsten AEM Cloud går det inte att skapa indexdefinitioner som innehåller samma tagg i flera index.

### Konfiguration av indexdefinitioner får inte innehålla lägesersättning för förbjudna sökvägar {#oakpal-xml-mode-analysis}

* **Nyckel**: FilterXmlModeAnalysis
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2025.4.0

Det är inte tillåtet att använda ersättningsläget i filvalvet för sökvägar under /content. Det ska inte användas för sökvägar under /etc och /var.
Läget&quot;ersätt&quot; ersätter allt befintligt innehåll i databasen med det som finns i innehållspaketet, och paket som aktiverar den här åtgärden bör inte ingå i paket som distribueras via CloudManager.

## Dispatcher optimeringsverktyg {#dispatcher-optimization-tool-rules}

I följande avsnitt visas de DOT-kontroller (Dispatcher Optimization Tool) som utförs av Cloud Manager. Följ länkarna för varje kontroll för dess GitHub-definition och information.

* [Oväntade token för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [Omatchat citattecken för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [Dispatcher-konfiguration saknar parentes](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [Extra parentes för Dispatcher-konfiguration](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [Dispatcher-konfigurationen saknar obligatorisk egenskap](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [Egenskapen ](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property) har tagits bort för Dispatcher-konfigurationen

* [Det gick inte att hitta Dispatcher-konfigurationen](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [Det gick inte att hitta filen i HTTP-konfigurationen ](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [Dispatcher-konfiguration allmän](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [Dispatcher publiceringsgruppscache bör ha `serveStaleOnError` aktiverat](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [Dispatcher-filtren för publiceringsgrupper bör innehålla standardreglerna för nekande från version 6.x.x av AEM-typen](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [Dispatcher-publiceringsservergruppens cache `statfileslevel` -egenskap bör vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [Dispatcher-publiceringsservergruppens `gracePeriod`-egenskap bör vara >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [Varje Dispatcher-servergrupp ska ha ett unikt namn](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [Reglerna för Dispatcher-publiceringsservergruppen bör konfigureras `ignoreUrlParams` på ett tillåtelselistesätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [Filtren för publiceringsgruppen i Dispatcher ska ange de tillåtna Sling-väljarna på ett tillåtelselista sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [Filtren för Dispatcher-publiceringsgruppen ska ange de tillåtna Sling-suffixmönstren på ett tillåtelselista sätt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [Använd inte direktivet &quot;Kräv att alla beviljas&quot; i ett VirtualHost Directory-avsnitt med en rotkatalogsökväg](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
