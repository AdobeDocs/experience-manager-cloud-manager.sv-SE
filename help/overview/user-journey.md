---
title: Användarresa
description: I det här dokumentet beskrivs de olika introduktionsscenarierna och hur du kommer igång med Cloud Manager.
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Användarresa {#user-journey}

Som Adobe Experience Manager-användare kan du

* Var ny i AEM.
* Använd AEM 6.x.
* Måste uppgradera till AEM 6.5 för att kunna använda [!UICONTROL Cloud Manager].

I det här dokumentet beskrivs dessa scenarier och hur du kan komma igång med [!UICONTROL Cloud Manager].

>[!NOTE]
>
>[!UICONTROL Cloud Manager] är endast tillgängligt för Adobe Managed Services-kunder (AMS) som använder AEM 6.4 eller senare.

## Onboarding {#onboarding}

Inköpsprocessen skiljer sig åt beroende på om du är ny hos AMS eller redan är en AMS-kund.

### Nyheter i Adobes hanterade tjänster {#new-to-ams}

Som ny kund kommer du att bli [!UICONTROL Cloud Manager] som en del av introduktionsprocessen till Adobes hanterade tjänster.

Som en del av introduktionsprocessen får du ett välkomstmeddelande som innehåller:

* Den URL som ska användas [!UICONTROL Cloud Manager]
* Instruktioner för att logga in på [!UICONTROL Experience Cloud]
* Instruktioner om hur du använder Admin Console för att hantera dina användare och deras respektive behörigheter så att de kan komma åt dem [!UICONTROL Cloud Manager] vid behov.

### Befintlig Adobe Managed Services-kund {#existing-customer}

Som befintlig AMS-kund måste ni först uppgradera era befintliga produktions- och icke-produktionsmiljöer till AEM 6.4 eller senare.

När du utför uppgraderingen kommer du att bli anmäld till Cloud Manager och få en URL som du kan använda [!UICONTROL Cloud Manager]. Dessutom, för de användare som behöver åtkomst [!UICONTROL Cloud Manager]måste du börja använda Admin Console för att hantera dem och deras respektive behörigheter.

Ditt befintliga AEM måste också följa de rekommenderade bästa metoderna eftersom du börjar använda [!UICONTROL Cloud Manager] för att driftsätta nya kodändringar i era AEM.

Mer information om fördelarna med att uppgradera till AEM 6.5 finns i dokumentet [Uppgraderar till AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)

## Åtkomst [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

Du får åtkomst till [!UICONTROL Cloud Manager] och dina AEM miljöer genom att helt enkelt logga in på [!UICONTROL Experience Cloud] landningssida med inloggningsuppgifterna för Adobe Identity Management och AEM i lösningsväljargränssnittet.

Efter inloggning [!UICONTROL Cloud Manager] För första gången får du tillgång till dina AEM direkt från [!UICONTROL Cloud Manager] Gränssnitt. Nu är du redo att utforska alla möjligheter som [!UICONTROL Cloud Manager] och förbered din första kodgren för att driftsättas i scen- och produktionsmiljöer.

Så här kommer du igång med [!UICONTROL Cloud Manager], se dokumentet [Inloggning för första gången](/help/getting-started/first-time-login.md).

Mer information om AEM finns i dokumentet [Driftsättning och underhåll.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

## Komma igång med [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

När du är inloggad på [!UICONTROL Cloud Manager] kan du komma igång med ditt AEM projekt genom att:

1. Konfigurera koddatabasmiljön.
1. Konfigurera ditt team och dina roller.
   * Rollmedlemskap tilldelas genom att användaren läggs till i en [!UICONTROL Cloud Manager] profil med Admin Console.
1. Konfigurera dina källkodsgrenar i Git-databasen.
1. Definiera era mål i termer av belastning och nyckeltal för prestanda.
1. Definiera testscenarier för att distribuera koden till scen- och produktionsmiljöer när alla kvalitetskontroller har slutförts.

## Heltäckande resa {#end-to-end-journey}

Bilden visar kundresan på en hög nivå när man använder [!UICONTROL Cloud Manager] CI/CD-pipeline för distribution av kodändringar till dina staging- och produktionsmiljöer.

![Heltäckande resa](/help/assets/screen_shot_2018-05-15at124004pm.png)
