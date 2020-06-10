---
title: Kundresa
seo-title: Adobe AEM Cloud Manager - kundresa
description: Följ den här sidan om du vill veta mer om din resa som kund för att komma igång med Cloud Manager.
seo-description: Följ den här sidan om du vill veta mer om din resa som kund för att komma igång med Adobe AEM Cloud Manager.
uuid: d4468eb6-5bde-48dd-b96e-0cc61e046f96
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: bc9a0d63-ae6b-4fe9-81e5-bf9844f04e54
translation-type: tm+mt
source-git-commit: 77b7e2fc81880a7f1878fa9553ce2ae8078d1b78
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# Kundresa {#customer-journey}

Som kund kan du vara ny i Adobe Experience Manager (AEM), som för närvarande använder AEM 6.4, eller behöva uppgradera till AEM 6.4 för att kunna använda [!UICONTROL Cloud Manager]. Följande scenarier förklarar din resa som en ny eller befintlig kund att komma igång med [!UICONTROL Cloud Manager].

>[!NOTE]
>
>[!UICONTROL Cloud Manager] är endast tillgängligt för Adobe Managed Services-kunder som använder AEM 6.4 eller senare.

## On-boarding to [!UICONTROL Cloud Manager]{#on-boarding-to-cloud-manager}

1. **Ny AEM-kund på Adobes hanterade tjänster**

   Som ny kund kommer du att vara med [!UICONTROL Cloud Manager] i introduktionsprocessen till Adobes hanterade molntjänst.

   URL:en för åtkomst [!UICONTROL Cloud Manager] inkluderas i välkomstmeddelandet tillsammans med instruktionerna för inloggning [!UICONTROL Experience Cloud]och använd Adobe Admin Console för att hantera dina användare och deras respektive behörigheter för de användare som behöver få åtkomst [!UICONTROL Cloud Manager].

1. **Befintlig AEM-kund på Adobes hanterade tjänster**

   Som befintlig kund måste du först uppgradera din befintliga produktion och icke-produktionsmiljöer till AEM 6.4-versionen. Samtidigt som du utför uppgraderingen kommer du att vara ombord och få en URL som du kan komma åt [!UICONTROL Cloud Manager]. Dessutom måste du börja använda Adobe Admin Console för att hantera dina användare och deras respektive behörigheter för de användare som behöver åtkomst [!UICONTROL Cloud Manager].

   Ditt befintliga AEM-projekt måste också följa de rekommenderade bästa metoderna eftersom du börjar använda [!UICONTROL Cloud Manager] för att distribuera nya kodändringar till dina AEM-miljöer.

   Mer information om fördelarna med att uppgradera till AEM 6.4 finns i [Uppgradera till AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html).

## Åtkomst [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

Du får tillgång till [!UICONTROL Cloud Manager] och dina AEM-miljöer genom att helt enkelt logga in på [!UICONTROL Experience Cloud] landningssidan, använda inloggningsuppgifterna för Adobe Identity Management och välja AEM i lösningsväljargränssnittet.

När du har loggat in [!UICONTROL Cloud Manager] för första gången får du tillgång till dina AEM-miljöer direkt från [!UICONTROL Cloud Manager] användargränssnittet. Nu är du redo att utforska alla möjligheter [!UICONTROL Cloud Manager]när du har din första kodgren klar att distribueras till scen- och produktionsmiljöer.

Information om hur du utforskar och kommer igång med [!UICONTROL Cloud Manager]finns i [Första gången du loggar in](first-time-login.md). Mer information om AEM finns i [Komma igång med AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/deploy.html). Mer information finns i [AEM Resources](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&amp;mv=other) .

## Komma igång med [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

När du är inloggad på [!UICONTROL Cloud Manager]är det första du behöver göra att konfigurera koddatabasmiljön, sedan ditt team och dina roller. I synnerhet tilldelas rollmedlemskap genom att användaren läggs till i en [!UICONTROL Cloud Manager] profil med hjälp av användargränssnittet i Admin Console.

Därefter måste du konfigurera dina källkodsgrenar i **Git-databasen**, definiera dina mål i form av belastnings- och KPI:er för prestanda och testscenarier för att kunna distribuera koden till scen- och produktionsmiljöer när alla kvalitetskontroller är klara.

## Heltäckande resa {#end-to-end-journey}

Följande diagram visar kundresan på en hög nivå när du använder [!UICONTROL Cloud Manager] CI/CD-pipeline för att distribuera dina kodändringar till din scen- och produktionsmiljö.

![](assets/screen_shot_2018-05-15at124004pm.png)

