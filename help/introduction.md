---
title: Introduktion till Cloud Manager för AMS
description: Börja här för att lära känna Cloud Manager för Adobe Managed Services (AMS) och hur den gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet.
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 3%

---


# Introduktion till [!UICONTROL Cloud Manager] för AMS {#introduction-to-cloud-manager}

Börja här för att lära känna Cloud Manager för Adobe Manage Services (AMS) och hur den gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet.

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Introduktion till Cloud Manager för AMS"
>abstract="Organisationer kan själva hantera Adobe Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="Skapa program"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="Skapa miljöer"

## Introduktion {#introduction}

[!UICONTROL Cloud Manager] för Adobe Experience Manager ger utvecklare möjlighet att skapa slagkraftiga kundupplevelser genom smidiga arbetsflöden som bygger på Adobe Experience Manager bästa praxis. Med CI/CD-ledningar som är optimerade för Adobe Experience Manager kan du enkelt sammanfoga arbetsflöden för utveckling genom att helt enkelt checka in koden som sedan kan flyttas hela vägen till produktionsklart läge. Under konstruktionsfasen testas era anpassade koduppdateringar noga mot bästa praxis för att kunna leverera tillförlitliga program till era kunder. Cloud Manager använder en öppen API-metod och gör det möjligt att integrera med era system utan att störa befintliga processer och verktyg.

>[!NOTE]
>
>I den här dokumentationen beskrivs funktionerna och funktionerna i Cloud Manager för Adobe Managed Services (AMS).
>
>Motsvarande dokumentation för AEM as a Cloud Service finns i [AEM as a Cloud Service dokumentation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html)

Med Cloud Manager får ditt utvecklingsteam tillgång till följande funktioner:

* Kontinuerlig integrering/kontinuerlig leverans (CI/CD) av kod för att minska time to market från månader/veckor till dagar/timmar

* Kodinspektion, prestandatestning och säkerhetsvalidering baserade på bästa praxis innan produktionen påbörjas för att minimera produktionsstörningar

* API-anslutning som komplement till befintliga DevOps-processer

* Automatisk skalning som på ett intelligent sätt upptäcker behovet av ökad kapacitet och automatiskt ger tillgång till ytterligare webb-/publiceringssegment

Den här bilden visar CI/CD-processflödet som används i [!UICONTROL Cloud Manager]:

![CI/CD-flöde](/help/assets/screen_shot_2018-05-12at73843pm.png)

## Viktiga funktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Här följer en djupdykning i de viktigaste funktionerna i Cloud Manager.

### Självbetjäningsgränssnitt {#self-service-interface}

Användargränssnittet för [!UICONTROL Cloud Manager] gör att du enkelt kan komma åt och hantera molnmiljön och CI/CD-flödet för dina Adobe Experience Manager-program.

Du definierar programspecifika nyckeltal (KPI) (t.ex. toppsidor per minut och förväntad svarstid för en sidinläsning) som utgör grunden för mätning av en lyckad distribution. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Med självbetjäningsgränssnittet får du kontroll, men det ger även länkar till resurser för god praxis och tillgång till experter i Adobe som kan ge den vägledning du behöver.

Utforska och komma igång med [!UICONTROL Cloud Manager]Användargränssnitt, se dokumentet [Första gången du loggar in.](/help/getting-started/first-time-login.md)

### CI/CD-pipeline {#ci-cd-pipeline}

En av de viktigaste funktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda en optimerad CI/CD-pipeline för att snabba upp leveransen av anpassad kod eller uppdateringar som att lägga till nya komponenter på webbplatsen.

Via [!UICONTROL Cloud Manager] I -gränssnittet kan du konfigurera och starta upp CI/CD-flödet. Som en del av denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program överförs till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från [!UICONTROL Cloud Manager]Användargränssnitt, se dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurerar icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] erbjuder flexibla och konfigurerbara driftsättningslägen så att ni kan leverera upplevelser efter förändrade affärskrav.

Med ett automatiskt utlösarläge distribueras kod automatiskt till en miljö baserat på specifika händelser, t.ex. kodimplementering. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av distributionsutlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinekörningen varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning, som alla levereras utan att du eller dina partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i dokumentet [Distribuerar kod.](/help/using/code-deployment.md)

### Automatisk skalning {#autoscaling}

när produktionsmiljön utsätts för ovanligt hög belastning, [!UICONTROL Cloud Manager] upptäcker behovet av extra kapacitet och tillför automatiskt ytterligare kapacitet online med funktionen för autoskalning.

I sådana fall [!UICONTROL Cloud Manager] aktiverar automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskaleringshändelsen och lägger till ytterligare kapacitet online inom några minuter. Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma region(er) och matchar samma systemspecifikationer som de körda dispatcher-/publiceringsnoderna.

Funktionen för autoskalning gäller bara för dispatcher/publiceringsskiktet och körs med en vågrät skalförändringsmetod, med minst ytterligare ett segment i ett dispatcher-/publiceringspar på högst tio segment. Eventuell ytterligare kapacitet som tillhandahålls kommer att skalas in manuellt inom tio arbetsdagar enligt CSE (Customer Success Engineer).

>[!NOTE]
>
>Kunder som vill ta reda på om autoskalning är lämpligt för respektive program bör kontakta sin CSE- eller Adobe-representant.
