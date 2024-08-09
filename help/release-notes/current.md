---
title: Versionsinformation för 2024.7.0
description: Läs mer om versionsinformationen för Cloud Manager 2024.7.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2024.7.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] 2024.7.0.

>[!NOTE]
>
>Den senaste versionsinformationen för Cloud Manager i AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service aktuella versionsinformation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/cloud-manager/current).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2024.7.0 är 18 juli 2024. Nästa version är planerad till den 13 augusti 2024.

## Nyheter {#what-is-new}

* Produktionspipeline ](/help/using/production-pipelines.md#adding-production-pipeline) och [icke-produktionspipeline](/help/using/non-production-pipelines.md#adding-non-production-pipeline) utlöser **Vid Git-ändringar** för att starta pipelinen vid en implementering är nu tillgängliga för [privata databaser](/help/managing-code/private-repositories.md).[
* En förproduktionspipeline kan bara aktiveras manuellt och kan inte konfigureras som **Vid Git-ändringar**.
* För rörledningar som endast är avsedda för produktion omfattar listan över befordrbara exekveringar exekveringar med en artefaktversion som är större än artefaktversionen som distribueras i produktionsmiljön.
* [AEM Project Archetype](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/overview) har uppdaterats till [version 49](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49).

## Program för tidigt antagande {#early-adoption}

Bli en del av Cloud Manager program för tidig användning och få möjlighet att testa några av de kommande funktionerna

### Rörledningar som endast är avsedda för mellanlagring och enbart för produktion {#staging-production-only-pipelines}

Nu finns stöd för [endast staging-och-production-only-pipelines](/help/using/stage-prod-only.md), vilket gör att du kan dela upp distributionspipelines för fullstacksproduktion i mindre, specialiserade distributioner.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-cloudmanager_splitpipelines@adobe.com` från den e-postadress som är kopplad till din Adobe ID.
