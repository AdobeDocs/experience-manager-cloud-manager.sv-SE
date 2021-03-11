---
title: Versionsinformation för 2021.2.0
seo-title: Versionsinformation om AEM Cloud Manager för 2021.2.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.2.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2021.2.0
translation-type: tm+mt
source-git-commit: b5233e1932888b515d8dc26a6493cbd26686bc3c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Versionsinformation för 2021.2.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.2.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.2.0 är 11 februari 2021.

## Nyheter {#whats-new}

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* Produktionsdistributioner distribueras nu parallellt till de kopplade publicerings- och dispatcherinstanserna.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar-regeln `squid:S2142`. Detta kommer inte längre att orsaka en konflikt med kontroller för trådavbrott.

* Egenskaper som angetts i kundens `pom.xml`-filer som har prefixats med sonar kommer nu att tas bort dynamiskt för att undvika problem med bygg- och kvalitetsskanning.

* Ytterligare regler för kodkvalitet har lagts till för att täcka problem med Cloud Servicens kompatibilitet.

## Felkorrigeringar {#bug-fixes}

* Ibland misslyckades CI/CD-pipeline (distribution) under ett prestandateststeg på grund av att en behållare som kör inläsningstestet påträffade ett fel.

* Ibland kan inläsningstestbehållaren rapportera körningen som misslyckad även om bara ett undantag inträffar. Felet rapporteras bara om testprocessen inte kan återställas.

* Vissa felmatchningar i hur miljönamn lagrades skulle leda till prestandatestningsfel.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.