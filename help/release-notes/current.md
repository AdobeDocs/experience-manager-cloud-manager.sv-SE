---
title: Versionsinformation för 2023.9.0
description: Detta är versionsinformationen för Cloud Manager version 2023.9.0.
feature: Release Information
source-git-commit: f15a4b739150ee40b6dc48de0fbc20859093c79c
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager version 2023.9.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2023.9.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Utgivningsdatum för [!UICONTROL Cloud Manager] version 2023.9.0 är 14 september 2023. Nästa version är planerad till den 5 oktober 2023.

## Felkorrigeringar {#bug-fixes}

* När ett program tas bort tas även associerade, pågående pipeline bort.
* Ett tillfälligt fel har korrigerats där alla steg i en pipeline-körning markerades som slutförda, men statusen för pipelinen fortfarande kördes, vilket gav intryck av att ha fastnat.
* Ett fel korrigerades när CI/CD-pipelines misslyckades för databasgrenar som genererade arkivtypen.
