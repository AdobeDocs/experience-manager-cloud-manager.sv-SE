---
title: Användarresa
description: Läs om de olika introduktionsscenarierna och hur du kommer igång med Cloud Manager.
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Användarresa {#user-journey}

Som AEM (Adobe Experience Manager) passar du förmodligen i något av följande scenarier:

* Du är ny i AEM.
* Du använder AEM 6.x.
* Du måste uppgradera till AEM 6.5 för att kunna använda [!UICONTROL Cloud Manager].

I det här dokumentet beskrivs dessa tre scenarier och din resa förklaras för att du ska komma igång med [!UICONTROL Cloud Manager].

>[!NOTE]
>
>[!UICONTROL Cloud Manager] är endast tillgänglig för Adobe Managed Services-kunder (AMS) som använder AEM 6.4 eller senare.

## Onboarding {#onboarding}

Inköpsprocessen skiljer sig åt beroende på om du är ny hos AMS eller redan är en AMS-kund.

### Nybörjare i Adobe Managed Services {#new-to-ams}

Som ny kund kommer du att bli registrerad på [!UICONTROL Cloud Manager] som en del av introduktionsprocessen till Adobe Managed Services.

Som en del av introduktionsprocessen får du ett välkomstmeddelande som innehåller följande:

* Den URL som ska användas för åtkomst till [!UICONTROL Cloud Manager].
* Instruktioner för att logga in på [!UICONTROL Experience Cloud].
* Instruktioner för att använda Admin Console för att hantera dina användare och deras respektive behörigheter så att de kan komma åt [!UICONTROL Cloud Manager] om det behövs.

### Nuvarande Adobe Managed Services-kund {#existing-customer}

Som befintlig AMS-kund måste du först uppgradera dina befintliga produktions- och icke-produktionsmiljöer till AEM 6.4 eller senare.

Under uppgraderingen är du registrerad på Cloud Manager och får en URL för att komma åt [!UICONTROL Cloud Manager]. För de användare som behöver få åtkomst till [!UICONTROL Cloud Manager] måste du dessutom börja använda Admin Console för att hantera dem och deras respektive behörigheter.

Ditt befintliga AEM-projekt måste också följa de rekommenderade bästa metoderna eftersom du börjar använda [!UICONTROL Cloud Manager] för att distribuera nya kodändringar i dina AEM.

Mer information om fördelarna med att uppgradera till AEM 6.5 finns i [Uppgradera till AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/upgrading/upgrade).

## Åtkomst [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

Logga in på [!UICONTROL Experience Cloud]-landningssidan med inloggningsuppgifterna för Adobe Identity Management. Därifrån väljer du AEM från lösningsväljaren för att komma åt [!UICONTROL Cloud Manager] och dina AEM miljöer.

När du har loggat in på [!UICONTROL Cloud Manager] för första gången får du åtkomst till dina AEM direkt från [!UICONTROL Cloud Manager]-gränssnittet. Nu är du redo att utforska alla möjligheter i [!UICONTROL Cloud Manager] och förbereda din första kodgren för att distribueras till din scen- och produktionsmiljö.

Information om hur du kommer igång med [!UICONTROL Cloud Manager] finns i [Första gången du loggar in](/help/getting-started/first-time-login.md).

Mer information om AEM finns i [Distribuera och underhålla](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy).

## Kom igång med [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

När du har loggat in på [!UICONTROL Cloud Manager] kan du komma igång med ditt AEM genom att göra följande:

1. Konfigurera koddatabasmiljön.
1. Konfigurera ditt team och dina roller. Rollmedlemskap tilldelas genom att användaren läggs till i en [!UICONTROL Cloud Manager]-profil med Admin Console.
1. Ställ in dina källkodsgrenar i Git-databasen.
1. Definiera era mål i termer av belastnings- och KPI:er för prestanda (viktiga prestandaindikatorer).
1. Definiera testscenarier för att distribuera koden till scen- och produktionsmiljöer när alla kvalitetskontroller har slutförts.

## Heltäckande resa {#end-to-end-journey}

I det här diagrammet visas kundresan på en hög nivå när du använder CI/CD-pipeline för [!UICONTROL Cloud Manager] för att distribuera dina kodändringar till dina staging- och produktionsmiljöer.

![Heltäckande resa](/help/assets/screen_shot_2018-05-15at124004pm.png)
