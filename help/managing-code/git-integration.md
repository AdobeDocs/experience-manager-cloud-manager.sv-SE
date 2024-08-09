---
title: Git-integrering med Adobe Cloud Manager
description: I den här videoserien går vi igenom hur en kundhanterad (lokal) Git-databas installeras och integreras med Adobe Cloud Manager.
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Git-integrering med Adobe Cloud Manager

Adobe Cloud Manager levereras med en enda Git-databas som används för att distribuera kod med Cloud Manager CI/CD-pipelines. Du kan använda Cloud Manager Git-databas utan att vara i drift eller också kan du integrera en lokal eller kundhanterad Git-databas med Cloud Manager.

## Git-integrering - översikt

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

I den här videoserien utforskas flera användningsexempel för att integrera en kundhanterad Git-databas med Cloud Manager.

* [Inledande synkronisering](#initial-sync)
* [Grundläggande förgreningsstrategi](#branching-strategy)
* [Funktionsutveckling](#feature-development)
* [Produktionsdistribution](#production-deployment)
* [Synkroniserar versionstaggar](#sync-tags)

I den här videoserien förutsätts grundläggande kunskaper i Git och hantering av källkontroll. Mer information om Git finns i [ytterligare resurser nedan](#additional-resources).

Stegen och namnkonventioner som beskrivs i den här videoserien är några av de bästa sätten att arbeta med en kundhanterad Git-databas och Cloud Manager. Konventioner och arbetsflöden som skildras förväntas anpassas för enskilda utvecklingsteam.

En fullständig översikt över Cloud Manager finns i [Introduktion till Cloud Manager](/help/introduction.md).

## Inledande synkronisering {#initial-sync}

Första steget för att synkronisera en kundhanterad Git-databas med Cloud Manager Git-databas.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Grundläggande förgreningsstrategi {#branching-strategy}

Konfigurera en grundläggande förgreningsstrategi för att kunna dra nytta av Cloud Manager [produktions](/help/using/production-pipelines.md)- och [icke-produktionspipelines](/help/using/non-production-pipelines.md).

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Funktionsutveckling {#feature-development}

Använd en funktionsgren för att isolera kodändringar i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att använda en icke-produktionsprocess för kodkvalitets- och valideringstestning.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Produktionsdistribution {#production-deployment}

Förbered kod för en produktionsrelease i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att distribuera till testnings- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Synkroniserar versionstaggar {#sync-tags}

Synkronisera versionstaggar från en Cloud Manager Git-databas i en kundhanterad Git-databas för att ge en bild av vilken kod som har distribuerats till staging- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Ytterligare resurser {#additional-resources}

* [Cloud Manager Introduktion](/help/introduction.md)
* [GitHub-resurser](https://try.github.io)
* [Atlassisk Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
