---
title: Git-integrering med Adobe Cloud Manager
description: I den här videoserien går vi igenom hur en kundhanterad (lokal) Git-databas installeras och integreras med Adobe Cloud Manager.
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 3671772a1369273d89fde101ba084a6e2f8ce8dc
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Git-integrering med Adobe Cloud Manager

Adobe Cloud Manager levereras med en enda Git-databas som används för att distribuera kod med Cloud Manager CI/CD-pipelines. Du kan använda Cloud Manager Git-databas utan att vara i drift eller också kan du integrera en lokal eller kundhanterad Git-databas med Cloud Manager.

## Översikt över Git-integrering

>[!VIDEO](https://video.tv.adobe.com/v/28710/) (3 minuter, 11 sekunder)

I den här videoserien utforskas flera användningsexempel för integrering av en kundhanterad Git-databas med Cloud Manager.

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

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12) (8 minuter)

## Grundläggande förgreningsstrategi {#branching-strategy}

Konfigurera en grundläggande förgreningsstrategi för att dra nytta av Cloud Manager [produktions](/help/using/production-pipelines.md)- och [icke-produktionspipelines](/help/using/non-production-pipelines.md).

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12) (3 minuter, 48 sekunder)

## Utveckling av funktionsgrenar {#feature-development}

Använd en funktionsgren för att isolera kodändringar i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att använda en icke-produktionsprocess för kodkvalitets- och valideringstestning.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12) (9 minuter)

## Produktionsdistribution {#production-deployment}

Förbered kod för en produktionsrelease i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att distribuera till testnings- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12) (6 minuter, 6 sekunder)

## Synkronisera versionstaggar {#sync-tags}

Du kan synkronisera versionstaggar från en Cloud Manager Git-databas till en kundhanterad Git-databas. Den här funktionen ger synlighet i vilken kod som har distribuerats till både staging- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12) (2 minuter, 57 sekunder)

## Ytterligare resurser {#additional-resources}

* [Cloud Manager Introduktion](/help/introduction.md)
* [GitHub-resurser](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git)
* [Atlassisk Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
