---
title: Versionsinformation för 2022.4.0
description: Detta är versionsinformationen för Cloud Manager version 2022.4.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 3d4eea13c0f2e9c4030bbfd3b7c5c25336548498
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager version 2022.4.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2022.4.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.4.0 är 7 april 2022. Nästa version är planerad till den 5 maj 2022.

## Nyheter {#what-is-new}

* Förbättringar av varaktigheten och framgångssiffran för stegen för att konstruera pipeline har implementerats och kommer att introduceras stegvis för alla kunder fram till april-månaden.
* Nu kan du enkelt hitta en Git-gren genom att skriva de första tecknen i namnet i inmatningsfältet i guiden för att lägga till och redigera pipeline och välja bland föreslagna matchningar.
* The **Pipelines** Sidan har nu en sidnumrering som förbättrar användbarheten för program med ett stort antal rörledningar.
   * 50 rader per sida visas i tabellen.
* Versionen av [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) som används av Cloud Manager har uppdaterats till version 36.
* Oracle-JDK är nu standard-JDK för utveckling och drift av AEM program. Molnhanterarens byggprocess växlar automatiskt till att använda Oracle-JDK, även om ett alternativ uttryckligen har valts i Maven-verktygskedjan.
   * Mer information om hur du byter till Oracle-JDK finns i [dokumentationen för byggmiljön.](/help/using/build-environment-details.md#using-java-support)
   * Se [Java-supportpolicyn för Adobe Experience Manager - frågor och svar](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) om du vill ta upp vanliga frågor om den här ändringen.
