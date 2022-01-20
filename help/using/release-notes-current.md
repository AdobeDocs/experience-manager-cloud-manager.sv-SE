---
title: Versionsinformation för 2022.01.0
description: Detta är versionsinformationen för Cloud Manager version 2022.01.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: ebbbbdca2bfd834bc3dc0ff06ffb318df42713ee
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---

# Versionsinformation för Cloud Manager version 2021.12.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2022.01.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.01.0 är den 20 januari 2022. Nästa version är planerad till den 10 februari 2022.

## Nyheter {#whats-new}

* Cloud Manager kommer att [undvika att återskapa kodbasen när den upptäcker att samma Git-implementering används](/help/using/setting-up-project.md#build-artifact-reuse) i flera körningar av rörledningar i en hel stack.
* När du genererar ett Git-lösenord visas förfallodatumet.

## Felkorrigeringar {#bug-fixes}

* Sällsynta fall av falska positiva pipeline-fel har åtgärdats.
* För program med endast en databas visas databasens namn på körningsskärmen för pipeline.
