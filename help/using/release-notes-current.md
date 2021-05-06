---
title: Versionsinformation för 2021.5.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.5.0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: 3d6f9a760a1e5bafdae6ece5627358524467a0d2
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Versionsinformation för 2021.5.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.5.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.5.0 är 6 maj 2021.
Nästa version är planerad till 3 juni 2021.

## Nyheter {#whats-new}

* Kvalitetsregeln PackageOverlaps identifierar nu fall där samma paket har distribuerats flera gånger, dvs. på flera inbäddade platser, i samma distribuerade paketuppsättning.

* Databasslutpunkten i det offentliga API:t innehåller nu Git-URL:en.

* I arbetsflödet Redigera program kan användaren bara ange icke-decimala KPI-värden.

* Intermittenta fel som påträffades när kod skickades till Adobe Git har nu åtgärdats.

* Redigeringsprogrammet har uppdaterats.

## Felkorrigeringar {#bug-fixes}

* Ibland kan användaren se en grön *aktiv*-status bredvid ett IP-Tillåtelselista även när den konfigurationen inte har distribuerats.

* I stället för att ta bort &quot;borttagna&quot;-variabler skulle API:t för pipelines-variablerna bara markera dem med statusen &quot;DELETED&quot;.

* Vissa problem med saklig kodkvalitet påverkade felaktigt tillförlitlighetsgraderingen.

* När en pipeline-körning startades mellan midnatt och kl. 1 UTC garanterades inte artefaktversionen som genererades av Cloud Manager att vara större än en version som skapades föregående dag.
