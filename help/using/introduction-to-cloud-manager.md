---
title: Introduktion till Cloud Manager
seo-title: Introduction to Cloud Manager
description: 'Den här sidan är en startpunkt för utbildning i Cloud Manager. '
seo-description: This page serves as a starting point for learning about Adobe AEM Cloud Manager and highlights the benefits and key features.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
level: Beginner
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 3%

---

# Introduktion till [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Introduktion till Cloud Manager"
>abstract="Organisationer kan själva hantera Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="Skapa program"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="Skapa miljöer"

## Introduktion {#introduction}

[!UICONTROL Cloud Manager] för Adobe Experience Manager ger utvecklare möjlighet att skapa slagkraftiga kundupplevelser genom smidiga arbetsflöden som bygger på Adobe Experience Manager bästa praxis. Med CI/CD-ledningar som är optimerade för Adobe Experience Manager kan du enkelt sammanfoga utvecklingsarbetsflöden genom att checka in koden och flytta hela vägen till produktionsklar. Under byggfasen testas era anpassade koduppdateringar grundligt med beprövade och inlärda metoder för att leverera slagkraftiga digitala upplevelser till era kunder. Cloud Manager använder en öppen API-metod och gör det möjligt att integrera med era system utan att störa befintliga processer och verktyg.

Den här dokumentationswebbplatsen beskriver specifikt funktionerna och funktionerna för kunder med Adobe Managed Services (AMS) i Cloud Manager. Motsvarande dokumentation för AEM as a Cloud Service kunder finns i [Implementera ansökningar för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html?lang=en).

Med Cloud Manager kan ditt utvecklingsteam utnyttja följande:

* Kontinuerlig integrering/kontinuerlig leverans av kod för att minska time to market från månader/veckor till dagar/timmar.

* Code Inspection, performance testing och security validation bygger på bästa praxis innan man övergår till produktion för att minimera produktionsstörningar.

* API Connectivity för att komplettera befintliga DevOps-processer.

* Automatisk skalning upptäcker behovet av ökad kapacitet på ett intelligent sätt och lägger automatiskt till ytterligare Dispatcher/Publish-segment online.

Följande bild visar CI/CD-processflödet som används i [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Viktiga funktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Man kan utnyttja följande funktioner med [!UICONTROL Cloud Manager]:

### Självbetjäningsgränssnitt {#self-service-interface}

Användargränssnittet för [!UICONTROL Cloud Manager] gör det möjligt för kunder att enkelt komma åt och hantera molnmiljön och CI/CD-flödet för sina Experience Manager-program.

Kunderna definierar programspecifika KPI:er (Key Performance Indicators) - toppmoderna sidvisningar per minut och förväntad svarstid för en sidinläsning, som i slutänden utgör grunden för att mäta en lyckad driftsättning. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Det nya självbetjäningsgränssnittet ger dig kontrollen tillbaka, men det ger även länkar till bästa praxis och tillgång till experter i Adobe som kan ge den vägledning du behöver.

Utforska och komma igång med [!UICONTROL Cloud Manager]&#39;s UI, se [Inloggning för första gången](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD-pipeline {#ci-cd-pipeline}

En av de viktigaste funktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda en optimerad CI/CD-pipeline för att snabba upp leveransen av anpassad kod eller uppdateringar som att lägga till nya komponenter på webbplatsen.

Via [!UICONTROL Cloud Manager] UI kan kunderna konfigurera och starta sin CI/CD-pipeline. Under denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program skickas vidare till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från [!UICONTROL Cloud Manager]Användargränssnitt, se dokumenten [Konfigurera produktionsförlopp](configuring-production-pipelines.md) och [Konfigurerar icke-produktionsförlopp.](configuring-non-production-pipelines.md)

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] ger kunderna flexibla och konfigurerbara driftsättningslägen så att de kan leverera upplevelser efter förändrade affärskrav.

Med ett automatiskt utlösarläge distribueras koden automatiskt till en miljö baserat på specifika händelser, till exempel kodinsättning. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av utlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinen, varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning som levereras direkt vid leverans utan att kunderna eller deras partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i [Distribuera koden](deploying-code.md)

### Automatisk skalning {#autoscaling}

[!UICONTROL Cloud Manager] upptäcker behovet av extra kapacitet när produktionsmiljön utsätts för ovanligt hög belastning och automatiskt tillför ytterligare kapacitet online via funktionen för autoskalning.

Under en autoskalningshändelse, [!UICONTROL Cloud Manager] aktiverar automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskaleringshändelsen och lägger in ytterligare kapacitet online inom några minuter. Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma region(er) och matchar samma systemspecifikationer som de Dispatcher-/Publish-noder som körs.

Funktionen för autoskalning gäller bara skiktet Dispatcher/Publish och kommer alltid att utföras med en vågrät skalförändringsmetod, med minst ett ytterligare segment i paret Dispatcher/Publish och upp till högst tio segment. Eventuell ytterligare kapacitet som tillhandahålls kommer att skalas in manuellt inom tio arbetsdagar enligt CSE (Customer Success Engineer).

>[!NOTE]
>Kunder som vill ta reda på om autoskalning är lämpligt för respektive program måste kontakta sin CSE- eller Adobe-representant.
