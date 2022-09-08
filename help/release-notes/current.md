---
title: Versionsinformation för 2022.9.0
description: Detta är versionsinformationen för Cloud Manager version 2022.9.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: e74d386d0b2d50a7e276bb7ead7594ef448742ae
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# Versionsinformation om Cloud Manager version 2022.9.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2022.9.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.9.0 är 8 september 2022. Nästa version är planerad till den 6 oktober 2022.

## Nyheter {#what-is-new}

* Molnhanteraren har stöd för horisontell automatisk skalning av flera regioner.
* Nytt välkomstsidkort anpassat för användare som bara har en användarroll i Cloud Manager som vägleder dem när det gäller navigering till AEM och begränsad programåtkomst.
* Kunder som inte har någon Cloud Manager-roll kommer inte att kunna komma åt programinformation. De kan dock navigera till Author end points från CM-landningssidan.
* Eliminera misslyckanden i pipeline som beror på misslyckade försök genom att skapa större flexibilitet.

## Felkorrigeringar {#bug-fixes}

* Förbättrad feedback från kunder AEM appbygge när många stöter på anslutningsproblem med privata rapporter.
* I sällsynta fall, när hälsokontrollssystemet inte kan hämta ett giltigt hälsopoäng, utlöses ingen autoskalningshändelse.
