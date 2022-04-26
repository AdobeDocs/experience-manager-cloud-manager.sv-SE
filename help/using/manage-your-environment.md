---
title: Hantera dina miljöer
seo-title: Manage your Environments
description: Läs om Cloud Manager-miljön
seo-description: Follow this page to view the list of production and non-production environments that are used for setting up and running the CI/CD pipeline in Cloud Manager.
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: Environments
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 6ff704ec11dd4a5f73d5b5df5721c4fee649527b
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Hantera dina miljöer {#manage-your-environments}

>[!NOTE]
>Mer information om hur du hanterar miljöer för Cloud Manager AEM as a Cloud Service finns i [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#using-cloud-manager).

The **Översikt** sidan med Cloud Manager innehåller **Miljö** panel som visar alla hanterade AEM.

Var och en av miljöerna i listan visar sin associerade status.

![](assets/Manage-Environ-Overview.png)

## Videosjälvstudiekurs {#video-tutorial}

### Översikt över Cloud Manager-miljön {#environ-video}

Följande video ger en översikt till Cloud Manager-miljöer som består av instanser av AEM Author, AEM Publish och Dispatcher.

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## Åtkomst till miljöer i Cloud Manager {#accessing-environments-in-cloud-manager}

The **Miljö** I rutan visas de produktions- och scenmiljöer som ingår i programmet tillsammans med statusen.

Statusen är det sammanslagna energiläget över alla noder i miljön. Det är grönt om alla noder körs, rött om till och med en nod stoppas, blått om till och med en nod kommer upp och gult om även en nod har ett energiläge som inte är tillgängligt (i den här prioritetsordningen).

![](assets/Environments-card-new.png)

### Miljöer {#environments}

Klicka **Hantera** för att visa **Miljö** skärm.

The **Miljö** visas ett kort för *Produktion* och *Scen* miljöer (beroende på vad som är tillämpligt) i ditt program. Miljönamnet visas ovanför varje kort. Kortet innehåller en tabell med noder i miljön tillsammans med t-shirtstorleken för processorn, lagringsutrymmet, regionen och statusen.

>[!NOTE]
>
>The **STATUS** av noden representerar den virtuella datorns energiläge och återspeglar inte statusen för AEM på servern. Status kan vara **Körs** (grön cirkel), **Stoppad** (röd cirkel), **Kommer upp** (blå cirkel) eller **Otillgänglig** (gul cirkel).

![](assets/Environments-tab.png)

>[!NOTE]
>
>Om du behöver dina miljöloggar kan de begäras via din Customer Success Engineer.
