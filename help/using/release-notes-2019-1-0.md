---
title: Versionsinformation för 2019.1.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.1.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.1.0.
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2019.1.0.
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 12d787ef2f9b2dd229b8ed0f8c602fbf5c06aa80

---


# Versionsinformation för 2019.1.0 {#release-notes-for}

I version [!UICONTROL Cloud Manager] 2018.9.0 finns stöd för testning av AEM Assets-program samt ytterligare pipeline-typer som kör stegen för bygg- och kodkvalitet, och som kan distribueras till en icke-produktionsmiljö.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.1.0 är 17 januari 2019.

## Nyheter {#whats-new}

* Stöd för prestandatestning av AEM Assets har lagts till. Mer information finns i Konfigurera [CI/CD-](configuring-pipeline.md)pipeline.
* Stöd för rörledningar som endast kör steg för bygg- och kodkvalitet samt rörledningar som driftsätts i icke-produktionsmiljöer. Mer information finns i avsnittet **Icke-produktion och Endast kvalitet för pipeline** i [Konfigurera CI/CD-pipeline](configuring-pipeline.md) .
* Stöd för anpassade miljövariabler i byggmiljön har lagts till. Mer information finns i [Skapa ett AEM-programprojekt](create-an-application-project.md) .
* För kunder med flera stadier eller produktionsmiljöer kan du välja vilken miljö som ska distribueras som en del av produktionsflödet på sidan [Konfigurera CI/CD-pipeline](configuring-pipeline.md) .
* httxt2dbm har lagts till för att skapa behållare.
* Alla hjälpmenyalternativ öppnar en ny flik.

## Felkorrigeringar {#bug-fixes}

* När du redigerade ett program var det möjligt att avmarkera alla siduppsättningar.
* Godkännandesteget hade fel namn.
* I vissa situationer har programlogotypen felaktigt matats in.
* Om bara konfigurationspaketet för dispatcher skapades misslyckas distributionssteget.
* Miljöer som innehöll instanser för kallstart hanterades inte korrekt.
* Vissa avslutade program visades i programväljaren.
* Om en ny förgrening lades till i Git-databasen när pipelinen redigerades kanske den inte kunde markeras omedelbart.
* På vissa skärmar var ikonen Developer Connection (Anslutning till utvecklare) på Hjälp-menyn inte synlig.
* Fliknyckeln hanterades inte korrekt i dialogrutan för tömning av dispatcher.

## Kända fel {#known-issues}

* När du öppnar ett program som har Sites, men inte Assets, KPI:er, visas ett anrop till åtgärdskortet med en **Setup Program** -knapp. Det är dock bara användare med rollen Business Owner som kan klicka på knappen **Setup Program** .