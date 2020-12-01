---
title: Versionsinformation för 2018.5.0
seo-title: Versionsinformation om AEM Cloud Manager för 2018.5.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.5.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2018.5.0.
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---


# Versionsinformation för 2018.5.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2018.5.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.5.0 är 12 juli 2018.

## Nyheter {#what-s-new}

* **CI/CD Pipeline-meddelanden**  - Användare ser nu  [!UICONTROL Experience Cloud] meddelanden om pipeline-händelser. Mer information finns i [Notifications](notifications.md).

* **Schemalagda produktionsdistributioner**  - Användarna kan nu schemalägga datum och tid för produktionsdistributioner. Mer information finns i [Distribuera koden](deploying-code.md).

* **Statuspage** som har  **titeln Activity**.

* Mer specifik information som visas på startsidan för problem som påträffas vid körning av pipeline.
* Förbättrad infrastruktur för prestandatestning.

## Felkorrigeringar {#bug-fixes}

* Under vissa omständigheter användes den felaktiga SonarQube-profilen, vilket ledde till felaktiga kvalitetsmått för kod.
* SonarQube check CQBP-75 ignorerade vissa OSGi-anteckningar.
* När CI/CD-pipeline avbröts visades inte läget enhetligt.

## Kända fel {#known-issues}

* Länkar till **AEM** och **Övervakning** från programlistskärmen ersätter både den aktuella webbläsarfliken och öppnar en ny flik.

