---
title: Vanliga frågor om Cloud Manager
description: Det här dokumentet ger svar på de vanligaste frågorna om Cloud Manager för AMS-kunder.
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6be659e02df0657ec7d3dbce8c18c44a327a36f4
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Det här dokumentet ger svar på de vanligaste frågorna om Cloud Manager för AMS-kunder.

## Går det att använda Java 11 med Cloud Manager-byggen? {#java-11}

Ja. Du måste lägga till `maven-toolchains-plugin` med rätt inställningar för Java 11.

* Den här processen dokumenteras [här.](/help/getting-started/using-the-wizard.md)
* Se till exempel [wk-exempelprojektkoden.](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)

## Mitt bygge misslyckas med ett fel om maven-scr-plugin efter byte från Java 8 till Java 11. Vad kan jag göra? {#maven-src-plugin}

Ditt AEM Cloud Manager-bygge kan misslyckas när du försöker byta från Java 8 till 11. Om följande fel uppstår måste du ta bort `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Instruktioner om hur du tar bort det här plugin-programmet [finns här.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## Min version misslyckas med ett fel om RequireJavaVersion efter växling från Java 8 till Java 11. Vad kan jag göra? {#requirejavaversion}

För Cloud Manager-byggen kan `maven-enforcer-plugin` misslyckas med det här felet

```text
[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion
```

Detta är ett känt fel som beror på att Cloud Manager använder en annan version av Java för att köra maven-kommandot jämfört med att kompilera kod. Utelämna helt enkelt `requireJavaVersion` från dina `maven-enforcer-plugin`-konfigurationer.

## Kodkvalitetskontrollen misslyckades och distributionen stoppas. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Ja. Alla fel i kodkvaliteten utom säkerhetsklassificeringar är icke-kritiska mått, så de kan kringgås som en del av en distributionsprocess genom att objekten i resultatgränssnittet expanderas.

En användare med rollen [Distributionshanterare, Projektledare eller Business Owner](/help/requirements/users-and-roles.md#role-definitions) kan åsidosätta problemen. I så fall fortsätter pipeline eller så kan de acceptera problemen. I så fall avbryts pipeline med ett fel.

Mer information finns i dokumenten [Trenivåporter när du kör en pipeline](/help/using/code-quality-testing.md#three-tier-gates-while-running-a-pipeline) och [Konfigurerar icke-produktionsförlopp](/help/using/non-production-pipelines.md#understanding-the-flow).

## Cloud Manager-driftsättningar misslyckas vid prestandateststeget i Adobe Managed Services-miljöer. Hur felsöker vi detta för att skicka kritiska mätvärden? {#debug-critical-metrics}

Det finns inget svar på den här frågan. Men det här är några viktiga punkter om prestandateststeget som du bör tänka på:

* Det här steget är ett webbprestandasteg, d.v.s. tiden för att läsa in sidan med en webbläsare.
* De URL:er som anges i den resulterande CSV-filen läses in i en Chrome-webbläsare i Cloud Manager-infrastrukturen under testet.
* Ett vanligt mått som misslyckas är felfrekvensen.
   * För att en URL ska kunna skickas måste huvud-URL:en läsas in med statusen `200` och på mindre än `20` sekunder.
   * Sidinläsningar som överstiger `20` sekunder markeras som `504` fel.
* Om din webbplats kräver användarautentisering läser du dokumentet [Förstå testresultaten](/help/using/code-quality-testing.md#authenticated-performance-testing) för att konfigurera testet för autentisering till din plats.

Mer information om kvalitetskontroller finns i dokumentet [Förstå testresultat](/help/using/code-quality-testing.md).

## Kan jag använda SNAPSHOT för versionen av Maven-projektet? {#snapshot}

Ja. För utvecklardistributioner måste Git-grenen `pom.xml`-filerna innehålla `-SNAPSHOT` i slutet av `<version>`-värdet.

Detta gör att efterföljande distribution fortfarande kan installeras när versionen inte ändras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

Du kan också ange versionen till `-SNAPSHOT` för fas- och produktionsbyggen eller distributioner. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg i Git. Om det behövs kan du hänvisa till den här taggen senare.

Mer information om versionshantering [finns här.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/project-version-handling.html)

## Hur fungerar paket- och paketversionshantering för driftsättning och produktion? {#staging-production}

I mellanlagrings- och produktionsdistributioner genereras en automatisk version [som beskrivs här.](/help/managing-code/maven-project-version.md)

För anpassad versionshantering i scen- och produktionsdistributioner anger du en korrekt 3-delsversion som `1.0.0`. Öka versionen varje gång du distribuerar till produktionen.

Cloud Manager lägger automatiskt till sin version i scen- och produktionsbyggen och skapar en Git-gren. Ingen särskild konfiguration krävs. Om du inte ställer in en maven-version enligt beskrivningen ovan kommer distributionen fortfarande att lyckas och en version ställs in automatiskt.

## Min maven-konstruktion misslyckas för Cloud Manager-distributioner men den byggs lokalt utan fel. Vad är det för fel? {#maven-build-fail}

Mer information finns i den här [Git-resursen](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Jag kan inte ange en variabel med ett aio-kommando. Vad kan jag göra? {#set-variable}

Du kan få ett 403-fel som följande när du försöker lista eller ange pipeline-variabler med `aio`-kommandon.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

I det här fallet måste användaren som kör kommandona läggas till i rollen **Distributionshanteraren** i Admin Console.

Mer information finns i [API-behörigheter](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/).
