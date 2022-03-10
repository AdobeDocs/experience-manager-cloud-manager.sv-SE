---
title: Versionsinformation för 2022.3.0
description: Detta är versionsinformationen för Cloud Manager version 2022.3.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 6e98f9d2fcd69799bad86d1e247212b26273bd0b
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Versionsinformation för Cloud Manager version 2022.3.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2022.3.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.3.0 är 10 mars 2022. Nästa version är planerad till den 7 april 2022.

## Nyheter {#what-is-new}

* [The `reliability_rating` kritiskt mått](understand-your-test-results.md) har inaktiverats.
* En användare kan nu sortera kolumnerna i **Pipelines** i Cloud Manager.

## Felkorrigeringar {#bug-fixes}

* [The **Hoppa över ändringar i belastningsutjämnaren** option](configuring-production-pipelines.md#adding-production-pipeline) kan nu inaktiveras korrekt.
* [The **Hoppa över ändringar i belastningsutjämnaren** option](configuring-production-pipelines.md#adding-production-pipeline) visas nu för arbetsflödet för redigering av distributionspipeline.
* En delmängd av manuellt skapade Git-databaser hade felaktiga namnvärden som påverkades [återanvändningsfunktionen för build-felaktigheter.](setting-up-project.md#build-artifact-reuse) Namnen på dessa databaser har ändrats och användarna ser det korrigerade namnet i Cloud Manager API/UI.
* [När du lägger till eller redigerar en pipeline för kodkvalitet](configuring-non-production-pipelines.md) alternativen för att hantera mätfel visas inte längre.
* Oväntade rörliga variabelkonfigurationer orsakar inte längre fel i byggsteget.
