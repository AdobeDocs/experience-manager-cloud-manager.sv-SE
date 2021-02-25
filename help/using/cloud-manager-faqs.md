---
title: Vanliga frågor om Cloud Manager
seo-title: Vanliga frågor om Cloud Manager
description: Se Vanliga frågor om Cloud Manager för att få felsökningstips
seo-description: Följ den här sidan för att få svar på vanliga frågor om Cloud Manager
translation-type: tm+mt
source-git-commit: 0db6a6a4e430cd2619db1739fd322224e4e129e7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Följande avsnitt innehåller svar på vanliga frågor om Cloud Manager.

## Går det att använda Java 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

Det går inte att skapa AEM Cloud Manager när du försöker byta från Java 8 till 11. Problemet kan ha många orsaker och de vanligaste är beskrivna nedan:

* Lägg till maven-toolchains-plugin med rätt inställningar för Java 11 enligt [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Se till exempel [exempelprojektkoden](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Om du råkar ut för felet nedan måste du ta bort användningen av `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar. Mer information finns i [här](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* För Cloud Manager-byggen misslyckas plugin-programmet för stavningskontroll med felet `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Det här är ett känt fel som beror på att Cloud Manager använder en annan version av Java för att köra maven-kommandot jämfört med att kompilera kod. Utelämna `requireJavaVersion` från dina Maven-enforcement-plugin-konfigurationer.

## Distributionen stoppas eftersom kodkvalitetskontrollen misslyckades. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Alla kodkvalitetsfel utom *Säkerhetsgradering* är icke-kritiska mått, så de kan kringgås genom att objekten i resultatgränssnittet expanderas.

En användare med [Distributionshanteraren, Project Manager eller Business Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)-rollen kan åsidosätta problemen. I så fall fortsätter pipeline eller så kan de acceptera problemen. I så fall avbryts pipeline med ett fel.  Mer information finns i [Tre-nivåportar när du kör en pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use).

## Cloud Manager-distributioner misslyckas vid prestandateststeget i Adobe Managed Services-miljöer. Hur felsöker vi detta för att skicka kritiska mätvärden? {#debug-critical-metrics}

Se [Förstå testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) för att förstå resultaten.

Anteckningar om prestandateststeget:

* *Prestandasteget* är ett webbprestandasteg, d.v.s. den tid det tar att läsa in sidan med en webbläsare.
* De URL:er som anges i resultatet *CSV*-filen läses in i en Chrome-webbläsare i Cloud Manager-infrastrukturen under testet.
* Ett vanligt mått som misslyckas är *felfrekvensen*. För att en URL ska kunna skickas måste huvud-URL:en läsas in med `200`-status och på mindre än `20` sekunder. Sidinläsningar som överskrider `20` sekunder markeras som `504`-fel.
* Om din plats kräver användarautentisering läser du [Autentiserad prestandatestning](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) för att konfigurera testet för autentisering till din plats.

## Får vi använda SNAPSHOT i den version av projektet Maven? Hur fungerar versionshantering av paketen och källfilerna för driftsättning av scener och produktion? {#snapshot-version}

1. För utvecklardistributioner måste Git-grenen `pom.xml`-filerna innehålla `-SNAPSHOT` i slutet av `<version>`-värdet. Detta gör att efterföljande distribution där versionen inte ändras kan installeras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

1. I scen- och produktionsdistributionen genereras en automatisk version enligt [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. För anpassad versionshantering i Stage- och Production-distributioner anger du en korrekt maven-version på 3 delar som `1.0.0`. Öka versionen varje gång du ska göra en ny distribution till produktion.

1. Cloud Manager lägger automatiskt till sin version i Stage- och Production-byggen och skapar till och med en Git-gren. Ingen särskild konfiguration krävs. Om steg 3 ovan hoppas över fungerar distributionen ändå som den ska och en version ställs in automatiskt.

1. Om du lämnar versionen med `-SNAPSHOT` för scen- och produktionsbyggen eller distributioner är även det OK. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg åt dig i Git. Om det behövs kan du hänvisa till den här taggen senare.

1. Om du vill testa experimentell kod i utvecklingsmiljön kan du skapa en ny Git-gren och ställa in pipeline så att den använder den andra grenen. Detta är användbart när distributioner börjar misslyckas och du vill testa med äldre versioner av koden för att se när den gick sönder.

   Git-kommandot nedan skapar en fjärrgren med namnet *testbranch1* mot en specifik befintlig implementering `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Den här speciella grenen kan användas i Cloud Manager utan att påverka andra grenar:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Mer information finns i [Git-dokumentationen](https://git-scm.com/book/en/v2/Git-Internals-Git-References).

   Om du vill ta bort testgrenen senare använder du kommandot delete:

   `git push origin --delete testbranch1`

## Det går inte att skapa Maven i Cloud Manager, men det byggs lokalt utan fel. Hur felsöker jag? {#maven-build-fail}

Mer information finns i [Git-resurs](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Det går inte att ange en variabel via aio cloud manager för att ange pipeline-variabler. Hur felsöker man dessa problem? {#set-variable}

Om du får ett `403`-fel när du försöker lista eller ange pipeline-variabler med kommandon som liknar dem nedan, måste du läggas till som en *Deployment Manager* Cloud Manager-produktroll i Admin Console.\
Mer information finns i [API-behörigheter](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md).

Relaterade kommandon och fel:

`$ aio cloudmanager:list-pipeline-variables 222`

*Fel*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Fel*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
