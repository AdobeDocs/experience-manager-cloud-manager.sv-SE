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
source-git-commit: 6ff4b6e950e153c98b6981ec09dfa0648809c693
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 8%

---


# Introduktion till [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Introduktion till Cloud Manager"
>abstract="Organisationer kan själva hantera Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="Skapa program"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="Skapa miljöer"

## Introduktion {#introduction}

[!UICONTROL Cloud Manager], som ingår i Adobe Experience Manager (AEM) i Cloud, gör det möjligt för organisationer att självhantera Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

**Organisationer** kan utföra/utnyttja följande med hjälp av självbetjäningsportalen:[!UICONTROL Cloud Manager]

* **Kontinuerlig integrering/kontinuerlig** leverans av kod för att minska time to market från månader/veckor till dagar/timmar.
* **Code Inspection, performance testing and security** validering based on best practices before push to production to minimize production ruption.
* **Automatisk, schemalagd eller manuell** driftsättning även utanför kontorstid för maximal flexibilitet och kontroll.
* **Funktionen** Automatisk skalförändring upptäcker behovet av ökad kapacitet och lägger automatiskt till ytterligare Dispatcher/Publish-segment online.

Följande bild visar CI/CD-processflödet som används i [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Nyckelfunktioner i [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Organisationer kan utnyttja följande funktioner med [!UICONTROL Cloud Manager]:

### Självbetjäningsgränssnitt {#self-service-interface}

Med användargränssnittet för [!UICONTROL Cloud Manager] kan kunderna enkelt komma åt och hantera molnmiljön och CI/CD-flödet för Experience Manager-programmen.

Kunderna definierar programspecifika KPI:er (Key Performance Indicators) - toppmoderna sidvisningar per minut och förväntad svarstid för en sidinläsning, som i slutänden utgör grunden för att mäta en lyckad driftsättning. Roller och behörigheter för olika teammedlemmar kan enkelt definieras. Det nya självbetjäningsgränssnittet ger dig kontrollen tillbaka, men det ger även länkar till bästa praxis och tillgång till experter i Adobe som kan ge den vägledning du behöver.

Information om hur du utforskar och kommer igång med användargränssnittet i [!UICONTROL Cloud Manager] finns i [Första gången du loggar in](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD-pipeline {#ci-cd-pipeline}

En av de viktigaste funktionerna i [!UICONTROL Cloud Manager] är möjligheten att använda en optimerad CI/CD-pipeline för att snabba upp leveransen av anpassad kod eller uppdateringar som att lägga till nya komponenter på webbplatsen.

Genom [!UICONTROL Cloud Manager]-gränssnittet kan kunderna konfigurera och starta sin CI/CD-pipeline. Under denna pipeline utförs en grundlig kodgenomsökning för att säkerställa att endast högkvalitativa program skickas vidare till produktionsmiljön.

Mer information om hur du konfigurerar pipeline från användargränssnittet för [!UICONTROL Cloud Manager] finns i [Konfigurera CI/CD-pipeline](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html).

### Flexibla driftsättningslägen {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] ger kunderna flexibla och konfigurerbara driftsättningslägen så att de kan leverera upplevelser efter förändrade affärskrav.

Med ett automatiskt utlösarläge distribueras koden automatiskt till en miljö baserat på specifika händelser, till exempel kodinsättning. Du kan också schemalägga koddistributioner under angivna tidsramar, även utanför kontorstid.

Oberoende av utlösaren utförs kvalitetskontroller alltid som en del av CI/CD-pipelinen, varje gång en distribution aktiveras. Kvalitetskontrollerna omfattar bland annat kodkontroll, säkerhetstestning och prestandatestning som levereras direkt vid leverans utan att kunderna eller deras partners behöver göra något.

Mer information om hur du distribuerar kod och kvalitetskontroller finns i [Distribuera koden](deploying-code.md)

### Automatisk skalning {#autoscaling}

[!UICONTROL Cloud Manager] upptäcker behovet av extra kapacitet när produktionsmiljön är ovanligt hög och automatiskt lägger till ytterligare kapacitet online via funktionen för autoskalning.

Under en autoskalningshändelse utlöser [!UICONTROL Cloud Manager] automatiskt provisioneringsprocessen för autoskalning, skickar ett meddelande om autoskaleringshändelsen och lägger till ytterligare kapacitet online på några minuter. Den extra kapaciteten tillhandahålls i produktionsmiljön, i samma region(er) och matchar samma systemspecifikationer som de Dispatcher-/Publish-noder som körs.

Funktionen för autoskalning gäller bara skiktet Dispatcher/Publish och kommer alltid att utföras med en vågrät skalförändringsmetod, med minst ett ytterligare segment i paret Dispatcher/Publish och upp till högst tio segment. Eventuell ytterligare kapacitet som tillhandahålls kommer att skalas in manuellt inom tio arbetsdagar enligt CSE (Customer Success Engineer).

>[!NOTE]
>Kunder som vill ta reda på om autoskalning är lämpligt för respektive program måste kontakta sin CSE- eller Adobe-representant.
