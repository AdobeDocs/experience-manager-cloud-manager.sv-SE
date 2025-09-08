---
title: Introduktion till Cloud Manager för AMS
description: Börja här för att lära känna Cloud Manager för Adobe Managed Services (AMS) och hur det gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet.
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 8f29a06f63b8dc10cb3d28e2f38da1ead84f32f5
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 3%

---


# Introduktion till [!UICONTROL Cloud Manager] för AMS {#introduction-to-cloud-manager}

Börja här för att lära känna Cloud Manager för AMS (Adobe Managed Services) och hur det gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet.

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Introduktion till Cloud Manager för AMS"
>abstract="Organisationer kan själva hantera Adobe Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/cloud-manager/programs#cloud-manager" text="Skapa program"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/cloud-manager/environments#cloud-manager" text="Skapa miljöer"

## Introduktion {#introduction}

[!UICONTROL Cloud Manager] för Adobe Experience Manager ger utvecklare möjlighet att skapa slagkraftiga kundupplevelser genom smidiga arbetsflöden som bygger på Adobe Experience Manager bästa praxis. Med CI/CD-pipelines som är optimerade för Adobe Experience Manager kan du enkelt sammanfoga utvecklingsarbetsflöden genom att bara checka in koden, som sedan kan flyttas hela vägen till produktionsklara arbetsflöden. Under konstruktionsfasen testas era anpassade koduppdateringar noga mot bästa praxis för att kunna leverera tillförlitliga program till era kunder. Cloud Manager använder en öppen API-metod och gör det möjligt att integrera med era system utan att störa befintliga processer och verktyg.

>[!NOTE]
>
>I den här dokumentationen beskrivs funktioner och funktioner i Cloud Manager för Adobe Managed Services (AMS).
>
>Motsvarande dokumentation för AEM as a Cloud Service finns i [AEM as a Cloud Service-dokumentationen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/home).

Med Cloud Manager får ditt utvecklingsteam följande funktioner:

* Kontinuerlig integrering/kontinuerlig leverans (CI/CD) av kod för att minska time to market från månader/veckor till dagar/timmar.
* Kodinspektion, prestandatestning och säkerhetsvalidering baserade på bästa praxis innan produktionen påbörjas för att minimera produktionsstörningar.
* API-anslutning som komplement till befintliga DevOps-processer.
* Automatisk skalning som intelligent upptäcker behovet av ökad kapacitet och automatiskt ger tillgång till ytterligare Dispatcher/publiceringssegment online.

![CI/CD-flöde](/help/assets/screen_shot_2018-05-12at73843pm.png)CI/CD-processflödet som används i [!UICONTROL Cloud Manager].

## Viktiga funktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

I följande avsnitt beskrivs Cloud Manager viktigaste funktioner.

### Självbetjäningsgränssnitt {#self-service-interface}

Information om hur du utforskar och kommer igång med användargränssnittet för [!UICONTROL Cloud Manager] finns i [Första gången du loggar in](/help/getting-started/first-time-login.md).

Med användargränssnittet för [!UICONTROL Cloud Manager] kan du enkelt komma åt och hantera molnmiljön och CI/CD-flödet enkelt för dina Adobe Experience Manager-program.

Du definierar programspecifika nyckeltal (KPI) som toppar sidvisningar per minut eller förväntade sidinläsningstider. Dessa nyckeltal är grunden för att mäta hur framgångsrik driftsättningen är. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Med självbetjäningsgränssnittet får du full kontroll. Där finns också länkar till resurser för god praxis och tillgång till Adobe experter för vägledning när det behövs.

### Rörledning för CI/CD {#ci-cd-pipeline}

En av nyckelfunktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda en optimerad CI/CD-pipeline för att snabba upp leveransen av anpassad kod eller uppdateringar, som att lägga till nya komponenter på webbplatsen.

Med användargränssnittet i [!UICONTROL Cloud Manager] kan du konfigurera och starta din CI/CD-pipeline. Som en del av denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program överförs till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från användargränssnittet för [!UICONTROL Cloud Manager] finns i [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] erbjuder flexibla och konfigurerbara driftsättningslägen så att du kan leverera upplevelser efter förändrade affärsbehov.

Med ett automatiskt utlösarläge distribueras kod automatiskt till en miljö baserat på specifika händelser, till exempel kodinsättning. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av distributionsutlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinekörningen varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning, som alla levereras direkt utan att du eller dina partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i [Distribuera kod](/help/using/code-deployment.md).

## Ytterligare funktioner i Cloud Manager {#optional-features-in-cloud-manager}

Cloud Manager har ytterligare, avancerade funktioner som kan vara till nytta för ditt projekt beroende på din specifika miljö och dina behov. Om dessa funktioner är av intresse för dig kan du kontakta din Customer Success Engineer (CSE) eller Adobe representant för att diskutera mer.

### Automatisk skalning {#autoscaling}

När produktionsmiljön utsätts för ovanligt hög belastning upptäcker [!UICONTROL Cloud Manager] behovet av extra kapacitet och lägger automatiskt till ytterligare kapacitet online med hjälp av funktionen för autoskalning.

I en sådan händelse utlöser [!UICONTROL Cloud Manager] automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskalningshändelsen och lägger till ytterligare kapacitet online inom några minuter. Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma regioner, och matchar samma systemspecifikationer som de Dispatcher/publiceringsnoder som körs.

Funktionen för autoskalning gäller Dispatcher/publiceringsskiktet, där vågrät skalning används för att lägga till ett till tio segment i Dispatcher/publiceringspar. All ytterligare kapacitet som tillhandahålls skalas in manuellt inom tio arbetsdagar enligt Adobe CSE (Customer Success Engineer).

>[!NOTE]
>
>Om du är intresserad av att ta reda på om autoskalning är lämpligt för ditt program kan du kontakta din CSE- eller Adobe-representant.

### Blågrön/grön distribution {#blue-green}

Blå/grön driftsättning är en teknik som minskar driftavbrott och risker genom att köra två identiska produktionsmiljöer som kallas blå och grön.

När som helst är det bara en av miljöerna som är aktiv, där den aktiva miljön betjänar all produktionstrafik. I allmänhet är blått den aktiva miljön och grönt är inaktivt.

* Blue/green deployment is an add-on to Cloud Manager CI/CD pipelines in which a second set of publish and Dispatcher instances (green) is created and used for deployments. De gröna instanserna kopplas sedan till produktionsbelastningsutjämnaren och de gamla instanserna (blå) tas bort och avslutas.
* Den här implementeringen av blått/grönt behandlar instanser som övergångar och varje upprepning av en blå/grön pipeline skapar en ny uppsättning publicerings- och Dispatcher-servrar.
* En grön belastningsutjämnare skapas som en del av konfigurationen. Den här belastningsutjämnaren ändras aldrig och det är den som du ska peka den gröna URL:en eller &quot;test&quot;-URL:en på.
* Under en blå/grön distribution skapas en exakt kopia av de befintliga Dispatcher-/publiceringsskikten.

#### Blått/grönt distributionsflöde {#flow}

När blå/grön distribution är aktiverat skiljer sig distributionsflödet från Cloud Service standardflöde.

| Steg | Blå/grön driftsättning | Standarddistribution |
| --- | --- | --- |
| 1 | Distribution till författare | Distribution till författare |
| 2 | Pausa för testning | - |
| 3 | Grön infrastruktur skapas | - |
| 4 | Driftsättning till grön publicering/Dispatcher-nivåer | Distribution till utgivare |
| 5 | Paus för testning (upp till 24 timmar) | - |
| 6 | Grön infrastruktur läggs till i produktionsbelastningsutjämnaren | - |
| 7 | Blå infrastruktur tas bort från produktionsbelastningsutjämnaren | - |
| 8 | Pausa för slutsignering (upp till 24 timmar) | - |
| 9 | Blå infrastruktur avslutas automatiskt | - |
| 10 | Pipelinen har slutförts | - |

#### Implementera blå/grön {#implementing}

Alla AMS-användare som använder Cloud Manager för produktionsdistributioner är berättigade att använda den blå/gröna driftsättningen. Användningen av blå/grön driftsättning kräver dock ytterligare validering av dina miljöer och konfiguration av en Adobe CSE.

Om du är intresserad av blå/grön driftsättning bör du tänka på följande krav och begränsningar och kontakta din CSE.

#### Krav och begränsningar {#limitations}

* Blå/grön är bara tillgängligt för Dispatcher/utgivarpar.
* Preview Dispatcher/publish pairs ingår inte i blue/green-distributioner.
* Alla Dispatcher-/publiceringspar är identiska med alla andra Dispatcher-/utgivarpar.
* Blå/grön finns endast i produktionsmiljön.
* Blå/grön finns i AWS och Azure.
* Blå/grön är inte tillgängligt för kunder som bara använder Assets.
