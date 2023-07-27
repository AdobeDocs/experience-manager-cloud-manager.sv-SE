---
title: Introduktion till Cloud Manager för AMS
description: Börja här för att lära känna Cloud Manager för Adobe Managed Services (AMS) och hur den gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet.
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: a2cea28061304d109a3c9a48650d01255579443c
workflow-type: tm+mt
source-wordcount: '1298'
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
>Motsvarande dokumentation för AEM as a Cloud Service finns i [AEM as a Cloud Service dokumentation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/home.html)

Med Cloud Manager får ditt utvecklingsteam följande funktioner:

* Kontinuerlig integrering/kontinuerlig leverans (CI/CD) av kod för att minska time to market från månader/veckor till dagar/timmar

* Kodinspektion, prestandatestning och säkerhetsvalidering baserade på bästa praxis innan produktionen påbörjas för att minimera produktionsstörningar

* API-anslutning som komplement till befintliga DevOps-processer

* Automatisk skalning som intelligent upptäcker behovet av ökad kapacitet och automatiskt tar med ytterligare Dispatcher-/publiceringssegment online

Den här bilden visar CI/CD-processflödet som används i [!UICONTROL Cloud Manager]:

![CI/CD-flöde](/help/assets/screen_shot_2018-05-12at73843pm.png)

## Viktiga funktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Här följer en djupdykning i de viktigaste funktionerna i Cloud Manager.

### Självbetjäningsgränssnitt {#self-service-interface}

Användargränssnittet (UI) för [!UICONTROL Cloud Manager] gör att du enkelt kan komma åt och hantera molnmiljön och CI/CD-flödet för dina Adobe Experience Manager-program.

Du definierar programspecifika nyckeltal (KPI) (t.ex. toppsidor per minut och förväntad svarstid för en sidinläsning) som utgör grunden för mätning av en lyckad distribution. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Med självbetjäningsgränssnittet får du kontroll, men det ger även länkar till resurser för god praxis och tillgång till experter i Adobe som kan ge den vägledning du behöver.

Utforska och komma igång med [!UICONTROL Cloud Manager]Användargränssnitt, se dokumentet [Första gången du loggar in.](/help/getting-started/first-time-login.md)

### CI/CD-pipeline {#ci-cd-pipeline}

En av de viktigaste funktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda en optimerad CI/CD-pipeline för att snabba upp leveransen av anpassad kod eller uppdateringar som att lägga till nya komponenter på webbplatsen.

Via [!UICONTROL Cloud Manager] I -gränssnittet kan du konfigurera och starta upp CI/CD-flödet. Som en del av denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program överförs till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från [!UICONTROL Cloud Manager]Användargränssnitt, se dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurerar icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] erbjuder flexibla och konfigurerbara driftsättningslägen så att ni kan leverera upplevelser efter förändrade affärskrav.

Med ett automatiskt utlösarläge distribueras kod automatiskt till en miljö baserat på specifika händelser, till exempel kodinsättning. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av distributionsutlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinekörningen varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning, som alla levereras utan att du eller dina partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i dokumentet [Distribuerar kod.](/help/using/code-deployment.md)

## Valfria funktioner i Cloud Manager {#optional-features-in-cloud-manager}

Cloud Manager har ytterligare, avancerade funktioner som kan vara till nytta för ditt projekt beroende på din specifika miljökonfiguration och dina behov. Om dessa funktioner är av intresse för dig kan du kontakta en Customer Success Engineer (CSE) eller Adobe för att diskutera mer.

### Automatisk skalning {#autoscaling}

När produktionsmiljön utsätts för ovanligt hög belastning, [!UICONTROL Cloud Manager] upptäcker behovet av extra kapacitet och tillför automatiskt ytterligare kapacitet online med funktionen för autoskalning.

I sådana fall [!UICONTROL Cloud Manager] aktiverar automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskaleringshändelsen och lägger till ytterligare kapacitet online inom några minuter. Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma region(er) och matchar samma systemspecifikationer som de Dispatcher-/publiceringsnoder som körs.

Funktionen för autoskalning gäller bara Dispatcher/publishing-skiktet och körs med en vågrät skalförändringsmetod, med minst ytterligare ett segment i Dispatcher/publishing-paret upp till högst tio segment. Eventuell ytterligare kapacitet som tillhandahålls kommer att skalas in manuellt inom tio arbetsdagar enligt CSE (Customer Success Engineer).

>[!NOTE]
>
>Om du är intresserad av att ta reda på om autoskalning är lämpligt för ditt program kan du kontakta din CSE- eller Adobe-representant.

### Blå/gröna distributioner {#blue-green}

Blå/grön driftsättning är en teknik som minskar driftavbrott och risker genom att köra två identiska produktionsmiljöer som kallas blå och grön.

När som helst är det bara en av miljöerna som är aktiv, där den aktiva miljön betjänar all produktionstrafik. I allmänhet är blått den aktiva miljön och grönt är inaktivt.

* Blue/green deployment is an add-on to Cloud Manager CI/CD pipelines in which a second set of publish and Dispatcher instances (green) is created and used for deployments. De gröna instanserna kopplas sedan till produktionsbelastningsutjämnaren och de gamla instanserna (blå) tas bort och avslutas.
* Den här implementeringen av blått/grönt behandlar instanser som övergångar och varje upprepning av en blå/grön pipeline skapar en ny uppsättning publicerings- och Dispatcher-servrar.
* En grön belastningsutjämnare skapas som en del av konfigurationen. Den här belastningsutjämnaren ändras aldrig och det är den som du ska peka på den gröna URL:en eller &quot;test&quot;-URL:en på.
* Under en blå/grön distribution skapas en exakt kopia av de befintliga publicerings-/Dispatcher-lagren.

#### Blått/grönt distributionsflöde {#flow}

När blå/grön distribution är aktiverat skiljer sig distributionsflödet från standardflödet för distribution av Cloud Service.

| Steg | Blå/grön driftsättning | Standarddistribution |
|---|---|---|
| 1 | Distribution till författare | Distribution till författare |
| 2 | Pausa för testning | - |
| 3 | Grön infrastruktur skapas | - |
| 4 | Distribution till gröna publicerings-/dispatchernivåer | Distribution till utgivare |
| 5 | Paus för testning (upp till 24 timmar) | - |
| 6 | Grön infrastruktur läggs till i produktionsbelastningsutjämnaren | - |
| 7 | Blå infrastruktur tas bort från produktionsbelastningsutjämnaren - |
| 8 | Pausa för slutsignering (upp till 24 timmar) | - |
| 9 | Blå infrastruktur avslutas automatiskt | - |
| 10 | Pipelinen har slutförts | - |

#### Implementerande blå/grön {#implementing}

Alla AMS-användare som använder Cloud Manager för produktionsdistributioner är berättigade att använda blå/grön distribution. Användningen av blå/grön driftsättning kräver dock ytterligare validering av dina miljöer och konfiguration av Adobe CSE.

Om du är intresserad av blå/grön driftsättning bör du tänka på följande krav och begränsningar och kontakta din CSE.

#### Krav och begränsningar {#limitations}

* Blå/grön är bara tillgängligt för publicerings-/utskickspar.
* Preview Dispatcher/publish-par är inte en del av blue/green-distributioner.
* Alla Dispatcher/publish-par är identiska med alla Dispatcher/publish-par.
* Blå/grön finns endast i produktionsmiljön.
* Blå/grön finns i både AWS och Azure.
* Blå/grön är inte tillgängligt för Assets-kunder.
