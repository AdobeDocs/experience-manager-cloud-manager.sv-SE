---
title: Versionsinformation för 2024.7.0
description: Detta är versionsinformationen för Cloud Manager version 2024.7.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: d7c4c87bbc3c66ca9517c4d0c97e25a2302e1e8a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager version 2024.7.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2024.7.0.

>[!NOTE]
>
>Den senaste versionsinformationen för Cloud Manager i AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2024.7.0 är 18 juli 2024. Nästa version är planerad till den 12 augusti 2024.

## Nyheter {#what-is-new}

* Produktionspipeline ](/help/using/production-pipelines.md#adding-production-pipeline) och [icke-produktionspipeline](/help/using/non-production-pipelines.md#adding-non-production-pipeline) utlöser **Vid Git-ändringar** för att starta pipelinen vid en implementering är nu tillgängliga för [privata databaser.](/help/managing-code/private-repositories.md)[
* En förproduktionspipeline kan bara aktiveras manuellt och kan inte konfigureras som **Vid Git-ändringar**.
* För rörledningar som endast är avsedda för produktion omfattar listan över befordrbara exekveringar de som har en artefaktversion som är större än artefaktversionen som är distribuerad i produktionsmiljön.
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) har uppdaterats till [version 49.](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49)


## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner

### endast mellanlagring och endast produktion {#staging-production-only-pipelines}

Stöd för [endast mellanlagrings- och endast produktionspipelines](/help/using/stage-prod-only.md) har introducerats, vilket gör att du kan dela upp distributionspipelines för fullständig produktion i mindre, specialiserade distributioner.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-cloudmanager_splitpipelines@adobe.com` från den e-postadress som är kopplad till din Adobe ID.
