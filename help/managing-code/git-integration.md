---
title: Git-integrering med Adobe Cloud Manager
description: I den här videoserien går vi igenom hur du konfigurerar och integrerar en kundhanterad (lokal) Git-databas med Adobe Cloud Manager.
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 91e909273bf2b21d7f6413731923011915079e45
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Git-integrering med Adobe Cloud Manager

Adobe Cloud Manager levereras med en enda Git-databas som används för att distribuera kod med Cloud Managers CI/CD-pipelines. Du kan använda Cloud Managers Git-databas direkt eller så kan du även integrera en lokal eller kundhanterad Git-databas med Cloud Manager.

## Git-integrering - översikt

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

I den här videoserien utforskas flera användningsexempel som rör integrering av en kundhanterad Git-databas med Cloud Manager.

* [Inledande synkronisering](#initial-sync)
* [Grundläggande förgreningsstrategi](#branching-strategy)
* [Funktionsutveckling](#feature-development)
* [Produktionsdistribution](#production-deployment)
* [Synkroniserar versionstaggar](#sync-tags)

I den här videoserien förutsätts grundläggande kunskaper i Git och hantering av källkontroll. Se [ytterligare resurser nedan](#additional-resources) för mer information om Git.

Stegen och namnkonventioner som beskrivs i den här videoserien är några av de bästa sätten att arbeta med en kundhanterad Git-databas och Cloud Manager. Konventioner och arbetsflöden som skildras förväntas anpassas för enskilda utvecklingsteam.

En fullständig översikt över Cloud Manager finns i dokumentet [Introduktion till Cloud Manager.](/help/introduction.md)

## Inledande synkronisering {#initial-sync}

Första steget för synkronisering av en kundhanterad Git-databas med Cloud Managers Git-databas.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Grundläggande förgreningsstrategi {#branching-strategy}

Konfigurera en grundläggande förgreningsstrategi för att dra nytta av Cloud Managers [produktion](/help/using/production-pipelines.md) och [rörledningar för icke-produktion.](/help/using/non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Funktionsutveckling {#feature-development}

Använd en funktionsgren för att isolera kodändringar i en kundhanterad Git-databas och synkronisera med Cloud Managers Git-databas för att använda en icke-produktionsprocess för kodkvalitets- och valideringstestning.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Produktionsdistribution {#production-deployment}

Förbered kod för en produktionsrelease i en kundhanterad Git-databas och synkronisera med Cloud Managers Git-databas för att distribuera till staging- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Synkroniserar versionstaggar {#sync-tags}

Synkronisera versionstaggar från en Cloud Manager Git-databas till en kundhanterad Git-databas för att ge dig en bild av vilken kod som har distribuerats till staging- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Ytterligare resurser {#additional-resources}

* [Introduktion till Cloud Manager](/help/introduction.md)
* [GitHub-resurser](https://try.github.io)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
