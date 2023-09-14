---
title: Versionsinformation för 2023.9.0
description: Detta är versionsinformationen för Cloud Manager version 2023.9.0.
feature: Release Information
source-git-commit: a3e926fa13d54da1322f3a5219519fae07ddb273
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# Versionsinformation för Cloud Manager version 2023.9.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2023.9.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Utgivningsdatum för [!UICONTROL Cloud Manager] version 2023.9.0 är 14 september 2023. Nästa version är planerad till den 5 oktober 2023.

## Nyheter {#what-is-new}

* Den här versionen består endast av felkorrigeringar för Cloud Manager.

## Felkorrigeringar {#bug-fixes}

* När ett program tas bort tas även associerade, pågående pipeline bort, vilket säkerställer att pipelinen inte felaktigt har angetts som misslyckad status.
* När alla steg i en pipeline-körning är&quot;slutförda&quot; betraktas status för pipelinen som&quot;igång&quot;, vilket gör att den verkar vara i ett fast läge. Den ses nu som&quot;fullständig&quot;.
* För databasförgreningar som genereras med kodgeneratorns arketyp misslyckas CI/CD-pipeline.
