---
title: Hantera miljöer
description: Lär dig hur du använder Cloud Manager för att hantera miljöer.
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 116a930eea08b2bb9d288ec153519699754e0374
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Hantera miljöer {#managing-environments}

Lär dig hur du använder Cloud Manager för att hantera miljöer.

## Översikt {#overview-page}

Sidan **Översikt** i Cloud Manager innehåller rutan **Miljö** med en lista över alla hanterade AEM.

Var och en av miljöerna i listan visar sin associerade status.

![Översiktssida](/help/assets/Manage-Environ-Overview.png)

## Miljöpanel {#environments-tile}

Platsen **Miljöer** visar produktions- och mellanlagringsmiljöerna som har etablerats i programmet tillsammans med statusen.

Status är det sammanslagna energiläget över noderna i miljön i följande prioriteringsordning.

* Grön - Alla noder körs
* Röd - En eller flera noder har stoppats.
* Blå - en eller flera noder närmar sig.
* Gul - En eller flera noder har ett energisparläge som inte är tillgängligt.

![Miljöpanel](/help/assets/Environments-card-new.png)

## Hantera miljöer {#managing-environments-with-cloud-manager}

Tryck eller klicka på raden i en miljö för att visa skärmen **Miljöer** på panelen **Miljöer**.

Skärmen **Miljö** visar alla produktions- och mellanlagringsmiljöer i programmet. Miljönamnet visas ovanför varje kort. Kortet innehåller en tabell med noder i miljön tillsammans med t-shirtstorleken för processorn, lagringsutrymmet, regionen och statusen.

>[!NOTE]
>
>**STATUS** för noden representerar den virtuella datorns energiläge och återspeglar inte statusen för AEM på servern. Status kan vara:

* Grön - löpande
* Röd - stoppad
* Blå - kommer upp
* Gul - ej tillgänglig

![Fliken Miljö](/help/assets/Environments-tab.png)

>[!NOTE]
>
>Miljöinformation som namn kan inte ändras när de har etablerats.

>[!NOTE]
>
>Om du behöver dina miljöloggar kan de begäras via din Customer Success Engineer.

## Videosjälvstudie {#video-tutorial}

I den här videon får du en översikt över Cloud Manager-miljöer som består av AEM, publicering och Dispatcher-instanser.

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
