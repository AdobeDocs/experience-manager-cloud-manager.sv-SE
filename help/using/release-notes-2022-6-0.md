---
title: Versionsinformation för 2022.6.0
description: Detta är versionsinformationen för Cloud Manager version 2022.6.0.
feature: Release Information
source-git-commit: f202b245f35bcffa56b43f26a13b97d42fdb474e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---


# Versionsinformation om Cloud Manager version 2022.6.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2022.6.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.6.0 är 9 juni 2022. Nästa version är planerad till den 30 juni 2022.

## Nyheter {#what-is-new}

* Ett nytt välkomstkort på Cloud Managers landningssida ger användarna snabb tillgång till självstudiekurser och förloppsstatistik för klientorganisationen.
   * Den här funktionen kommer att introduceras stegvis under veckan efter version 2022.06.0.
* [Artefakter kan nu återanvändas](/help/using/setting-up-project.md#build-artifact-reuse) när Git-spegling används.

## API-ändringar {#api-changes}

* The [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API har tagits bort och [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) ska användas istället.
   * `List Programs` fortsätter att fungera, men användningen genererar varningsmeddelanden i loggar.
   * Det kommer inte längre att stödjas efter tre månader.