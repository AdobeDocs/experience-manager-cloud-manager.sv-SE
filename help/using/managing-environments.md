---
title: Hantera miljöer
description: Lär dig hur du använder Cloud Manager för att hantera dina miljöer.
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 80f8707e00357f5a08dd835b846c9ee610f3e573
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---


# Hantera miljöer {#managing-environments}

Lär dig hur du använder Cloud Manager för att hantera dina miljöer.

## Översikt {#overview-page}

The **Översikt** sidan med Cloud Manager innehåller **Miljö** panel som visar alla hanterade AEM.

Var och en av miljöerna i listan visar sin associerade status.

![Översiktssida](/help/assets/Manage-Environ-Overview.png)

## Miljöpanel {#environments-tile}

The **Miljö** visas de produktions- och staging-miljöer som ingår i programmet tillsammans med status.

Status är det sammanslagna energiläget över noderna i miljön i följande prioriteringsordning.

* Grön - Alla noder körs
* Röd - En eller flera noder har stoppats.
* Blå - en eller flera noder närmar sig.
* Gul - En eller flera noder har ett energisparläge som inte är tillgängligt.

![Miljöer](/help/assets/Environments-card-new.png)

## Hantera miljöer {#managing-environments-with-cloud-manager}

På **Miljö** platta, klicka **Hantera** för att visa **Miljö** skärm.

The **Miljö** visas ett kort för varje produktions- och testmiljöer (beroende på vad som är tillämpligt) i programmet. Miljönamnet visas ovanför varje kort. Kortet innehåller en tabell med noder i miljön tillsammans med t-shirtstorleken för processorn, lagringsutrymmet, regionen och statusen.

>[!NOTE]
>
>The **STATUS** av noden representerar den virtuella datorns energiläge och återspeglar inte statusen för AEM på servern. Status kan vara:

* Grön - löpande
* Röd - stoppad
* Blå - kommer upp
* Gul - ej tillgänglig

![Fliken Miljö](/help/assets/Environments-tab.png)

>[!NOTE]
>
>Om du behöver dina miljöloggar kan de begäras via din Customer Success Engineer.

## Videosjälvstudiekurs {#video-tutorial}

Den här videon ger en översikt till Cloud Manager-miljöer som består av AEM för redigering, publicering och Dispatcher.

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
