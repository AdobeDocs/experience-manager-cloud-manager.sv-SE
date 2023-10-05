---
title: Versionsinformation för 2023.10.0
description: Detta är versionsinformationen för Cloud Manager version 2023.10.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 851364e74864c28b3bcd9285dfbe06ddb530eb10
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager version 2023.10.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2023.10.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Utgivningsdatum för [!UICONTROL Cloud Manager] version 2023.10.0 är 5 oktober 2023. Nästa version planeras till den 2 november 2023.

## Nyheter {#what-is-new}

* The **Distributionshanteraren** roll kan [konfigurera en uppsättning innehållssökvägar som antingen blir ogiltiga eller tömda från AEM Dispatcher-cachen när en icke-produktionsprocess körs.](/help/using/non-production-pipelines.md)
   * Dessa cacheåtgärder kommer att utföras som en del av distributionssteget, precis efter att innehållspaket har distribuerats.
   * De här inställningarna använder AEM som standard.
* I oktober 2023-versionen av Cloud Manager uppdateras Java-versionerna med en stegvis utrullning.
   * De mindre versionerna för Java 8 och 11 samt Maven har uppdaterats och kommer att lanseras stegvis under de kommande två månaderna. Den nya versionen har flera säkerhetskorrigeringar och felkorrigeringar. De nya versionerna är
   * *Maven: 3.8.8*
   * *Java 8 version: /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11 version: /usr/lib/jvm/jdk-11.0.20*
   * [Se OpenJDK-råden](https://openjdk.org/groups/vulnerability/advisories/) om du vill ha information om säkerhet och felkorrigeringar i dessa JDK-uppdateringar.
