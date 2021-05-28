---
title: Versionsinformation för 2021.5.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.5.0
feature: Versionsinformation
source-git-commit: 3f17f252d89a1753c9cb121461b048f619d28415
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Versionsinformation för 2021.5.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.5.0.

>[!NOTE]
>Se [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) för att se den senaste versionsinformationen för Cloud Manager i AEM som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.5.0 är 6 maj 2021.
Nästa version är planerad till 10 juni 2021.

## Nyheter {#whats-new}

* Kvalitetsregeln PackageOverlaps identifierar nu fall där samma paket har distribuerats flera gånger, dvs. på flera inbäddade platser, i samma distribuerade paketuppsättning.

* Databasslutpunkten i det offentliga API:t innehåller nu Git-URL:en.

* I arbetsflödet Redigera program kan användaren bara ange icke-decimala KPI-värden.

* Intermittenta fel som påträffades när kod skickades till Adobe Git har nu åtgärdats.

* Redigeringsprogrammet har uppdaterats.

## Felkorrigeringar {#bug-fixes}

* I stället för att ta bort &quot;borttagna&quot;-variabler skulle API:t för pipelines-variablerna bara markera dem med statusen &quot;DELETED&quot;.

* Vissa problem med saklig kodkvalitet påverkade felaktigt tillförlitlighetsgraderingen.

* När en pipeline-körning startades mellan midnatt och kl. 1 UTC garanterades inte artefaktversionen som genererades av Cloud Manager att vara större än en version som skapades föregående dag.

* Vissa Adobe Managed Services-kunder (AMS) kunde inte skapa nya projekt i Adobe I/O Developer Console med hjälp av Cloud Managers API.
