---
title: Vanliga frågor om Cloud Manager
seo-title: Cloud Manager FAQs
description: Se Vanliga frågor om Cloud Manager för att få felsökningstips
seo-description: Follow this page to get answers on Cloud Manager FAQs
feature: Getting Started
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6dce1f48b66c6970c3ba025031f0adcbd01195dd
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Följande avsnitt innehåller svar på vanliga frågor om Cloud Manager.

## Går det att använda Java 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

Det går inte att skapa AEM Cloud Manager när du försöker byta från Java 8 till 11. Problemet kan ha många orsaker och de vanligaste är beskrivna nedan:

* Lägg till maven-toolchains-plugin med rätt inställningar för Java 11 enligt dokumenterad [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Se till exempel [wk-exempelprojektkod](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Om du råkar ut för felet nedan måste du ta bort användningen av `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar. Instruktioner finns i [här](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* För Cloud Manager-byggen misslyckas plugin-programmet för stavningskontroll med fel `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Det här är ett känt fel som beror på att Cloud Manager använder en annan version av Java för att köra maven-kommandot jämfört med att kompilera kod. Utelämna för tillfället `requireJavaVersion` från dina Maven-enforcement-plugin-konfigurationer.

## Driftsättningen stoppas eftersom kodkvalitetskontrollen misslyckades. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Ja. Alla fel i kodkvaliteten utom *Säkerhetsklassificering* är icke-kritiska mätvärden, så de kan kringgås som en del av en distributionsprocess genom att objekten i resultatgränssnittet expanderas.

En användare med [Distributionshanteraren, Project Manager eller Business Owner](/help/using/setting-up-users-and-roles.md#role-definitions) rollerna kan åsidosätta problemen. I så fall fortsätter pipelinen eller så kan de acceptera problemen. I så fall upphör pipeline med ett fel.

Se dokumenten [Tre nivåportar under körning av en pipeline](/help/using/understand-your-test-results.md#three-tier-gates-while-running-a-pipeline) och [Konfigurera icke-produktionsförlopp](/help/using/configuring-non-production-pipelines.md#understanding-the-flow) för mer information.

## Cloud Manager-distributioner misslyckas vid prestandateststeget i Adobe Managed Services-miljöer. Hur felsöker vi detta för att skicka kritiska mätvärden? {#debug-critical-metrics}

Se [Förstå testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) för att förstå resultaten.

Anteckningar om prestandateststeget:

* The *Prestandasteg* är ett webbprestandasteg, det vill säga det är dags att läsa in sidan med en webbläsare.
* URL:erna som anges i resultatet *CSV* filen läses in i en Chrome-webbläsare i Cloud Manager-infrastrukturen under testet.
* Ett vanligt mått som misslyckas är *felfrekvens*. För att en URL ska kunna skickas måste huvud-URL:en läsas in med `200` status och i mindre än `20` sekunder. Sidinläsningar som överskrider `20` sekunder markeras som `504` fel.
* Om din webbplats kräver användarautentisering läser du dokumentet [Förstå testresultaten](understand-your-test-results.md#authenticated-performance-testing) för att konfigurera testet för autentisering till din plats.

## Får vi använda SNAPSHOT i den version av projektet Maven? Hur fungerar versionshantering av paketen och paketburkfilerna för Stage- och Production-distributioner? {#snapshot-version}

Titta på följande scenarier för att lära dig mer om versionshantering av paketen och källfilerna för Stage- och Production-distributioner:

1. Git-grenen för utvecklardistributioner `pom.xml` måste innehålla `-SNAPSHOT` i slutet av `<version>` värde. Detta gör att efterföljande distribution där versionen inte ändras kan installeras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

1. I scen- och produktionsdistributionen genereras en automatisk version enligt dokumenteringen [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. För anpassad versionshantering i Stage- och Production-distributioner ställer du in en korrekt maven-version på 3 delar som `1.0.0`. Öka versionen varje gång du ska göra en ny distribution till produktion.

1. Cloud Manager lägger automatiskt till sin version i Stage- och Production-byggen och skapar till och med en Git-gren. Ingen särskild konfiguration krävs. Om steg 3 ovan hoppas över fungerar distributionen ändå som den ska och en version ställs in automatiskt.

1. Det finns inga problem om du lämnar versionen med `-SNAPSHOT` för byggen eller driftsättningarna av Stage och Production. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg åt dig i Git. Om det behövs kan du hänvisa till den här taggen senare.

1. Om du vill testa experimentell kod i utvecklingsmiljön kan du skapa en ny Git-gren och ställa in pipeline så att den använder den andra grenen. Detta är användbart när distributioner börjar misslyckas och du vill testa med äldre versioner av koden för att se när den gick sönder.

   Git-kommandot nedan skapar en fjärrgren med namnet *testbranch1* mot en specifik befintlig implementering `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Den här speciella grenen kan användas i Cloud Manager utan att påverka andra grenar:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Se [Git-dokumentation](https://git-scm.com/book/en/v2/Git-Internals-Git-References) för mer information.

   Om du vill ta bort testgrenen senare använder du kommandot delete:

   `git push origin --delete testbranch1`

## Det går inte att skapa Maven i Cloud Manager, men det byggs lokalt utan fel. Hur felsöker jag? {#maven-build-fail}

Se [Git-resurs](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) för mer information.

## Det går inte att ange en variabel via aio cloud manager för att ange pipeline-variabler. Hur felsöker man dessa problem? {#set-variable}

Om du får en `403` fel vid försök att lista eller ange pipeline-variabler med kommandon som liknar de nedan, måste du läggas till som *Distributionshanteraren* Cloud Managers produktroll i Admin Console.\
Se [API-behörigheter](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) för mer information.

Relaterade kommandon och fel:

`$ aio cloudmanager:list-pipeline-variables 222`

*Fel*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Fel*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
