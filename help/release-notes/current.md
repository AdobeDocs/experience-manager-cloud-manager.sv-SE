---
title: Versionsinformation för 2024.1.0
description: Detta är versionsinformationen för Cloud Manager version 2024.1.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b5907179d3de329e8b86546bb8aa99608a5b351a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager version 2024.1.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2024.1.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Utgivningsdatum för [!UICONTROL Cloud Manager] version 2024.1.0 är 17 januari 2024. Nästa version är planerad till den 16 februari 2024.

## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner

### Hämta din egen GitHub {#byo-github}

Om du använder GitHub för att hantera dina databaser, [du kan nu validera kod direkt i dina GitHub-databaser via Cloud Manager.](/help/managing-code/byo-github.md) Integreringen eliminerar behovet av att konsekvent synkronisera kod med Adobe-databasen och gör att du kan verifiera pull-begäranden innan du sammanfogar dem i huvudgrenarna. Den här funktionen är exklusiv för public GitHub. Det finns inget stöd för GitHub som är självvärd.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-CloudManager_BYOG@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

## Felkorrigeringar {#bug-fixes}

* Ett fel korrigerades för vissa hörnfall där hämtningen misslyckades på grund av hur testprogrammet tolkar data, vilket medförde att den totala felprocenten inte klarade testet.
* När ett byggsteg avslutas med status `FAILED` på grund av `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR`, beskrivs det nu korrekt som ett fel på grund av sammanslagningskonflikter med målgrenen.
