---
title: Introduktion till Cloud Manager
seo-title: Introduktion till Cloud Manager
description: 'Den här sidan är en startpunkt för utbildning i Cloud Manager. '
seo-description: 'Den här sidan är en startpunkt för utbildning i Adobe AEM Cloud Manager och visar på fördelarna och de viktigaste funktionerna. '
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: 213d1b2ee52496cc8cf6bc699488d9da9f7b9946
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 4%

---


# Introduktion till [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## Introduktion {#introduction}

[!UICONTROL Cloud Manager], som ingår i Adobe Experience Manager (AEM) i Cloud, gör det möjligt för organisationer att självhantera Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

Med hjälp av kundportalen för [!UICONTROL Cloud Manager] självbetjäning kan **organisationer** utföra/utnyttja följande:

* **Kontinuerlig integrering/kontinuerlig leverans** av kod för att minska time to market från månader/veckor till dagar/timmar.
* **Kodinspektion, prestandatestning och säkerhetsvalidering** baserad på bästa praxis innan produktionen påbörjas för att minimera produktionsstörningar.
* **Automatisk, schemalagd eller manuell driftsättning** även utanför kontorstid för maximal flexibilitet och kontroll.
* **Funktionen för autoskalning** upptäcker på ett intelligent sätt behovet av ökad kapacitet och lägger automatiskt till ytterligare Dispatcher/Publish-segment online.

Följande bild visar CI/CD-processflödet som används i [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Viktiga funktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Man kan utnyttja följande funktioner: [!UICONTROL Cloud Manager]:

### Självbetjäningsgränssnitt {#self-service-interface}

Med användargränssnittet för [!UICONTROL Cloud Manager] kan kunderna enkelt komma åt och hantera molnmiljön och CI/CD-flödet för sina Experience Manager-program.

Kunderna definierar programspecifika KPI:er (Key Performance Indicators) - toppmoderna sidvisningar per minut och förväntad svarstid för en sidinläsning, som i slutänden utgör grunden för att mäta en lyckad driftsättning. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Det nya självbetjäningsgränssnittet ger dig kontrollen tillbaka, men det ger även länkar till bästa praxis och tillgång till experter i Adobe som kan ge den vägledning du behöver.

Information om hur du utforskar och kommer igång med [!UICONTROL Cloud Manager]användargränssnittet finns i [Första gången du loggar in](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD-pipeline {#ci-cd-pipeline}

En av de viktigaste funktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda optimerade CI/CD-flöden för att snabba upp leveransen av anpassad kod eller uppdateringar, som att lägga till nya komponenter på webbplatsen.

Genom [!UICONTROL Cloud Manager] användargränssnittet kan kunderna konfigurera och starta sin CI/CD-pipeline. Under denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program skickas vidare till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från [!UICONTROL Cloud Manager]användargränssnittet finns i [Konfigurera CI/CD-pipeline](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html).

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] ger kunderna flexibla och konfigurerbara driftsättningslägen så att de kan leverera upplevelser efter förändrade affärskrav.

Med ett automatiskt utlösarläge distribueras koden automatiskt till en miljö baserat på specifika händelser, till exempel kodinsättning. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av utlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinen, varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning som levereras direkt vid leverans utan att kunderna eller deras partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i [Distribuera kod](deploying-code.md)

### Automatisk skalning {#autoscaling}

[!UICONTROL Cloud Manager] upptäcker behovet av extra kapacitet när produktionsmiljön utsätts för ovanligt hög belastning och automatiskt tillför ytterligare kapacitet online via funktionen för autoskalning.

Under en autoskalningshändelse utlöser automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskalningshändelsen och lägger till ytterligare kapacitet online på några minuter. [!UICONTROL Cloud Manager] Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma region(er) och matchar samma systemspecifikationer som de Dispatcher-/Publish-noder som körs.

Funktionen för autoskalning gäller bara skiktet Dispatcher/Publish och kommer alltid att utföras med en vågrät skalförändringsmetod, med minst ett ytterligare segment i paret Dispatcher/Publish och upp till högst tio segment. Eventuell ytterligare kapacitet som tillhandahålls kommer att skalas in manuellt inom tio arbetsdagar enligt CSE (Customer Success Engineer).

>[!NOTE]
>Kunder som vill ta reda på om autoskalning är lämpligt för respektive program måste kontakta sin CSE- eller Adobe-representant.
