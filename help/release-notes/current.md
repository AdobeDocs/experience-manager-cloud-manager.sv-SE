---
title: Versionsinformation för 2024.6.0
description: Detta är versionsinformationen för Cloud Manager version 2024.6.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 851b556c0917d9f6d97d958a0c8e8aeff4141079
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager version 2024.6.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2024.6.0.

>[!NOTE]
>
>Den senaste versionsinformationen för Cloud Manager i AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2024.6.0 är 6 juni 2024. Nästa version planeras till den 18 juli 2024.

## Nyheter {#what-is-new}

* Du kan nu [använda dina egna GitHub-databaser](/help/managing-code/private-repositories.md) som källor för rörledningar i full hög.
   * Dessutom kan du dra nytta av GitHub-databaser med [git-undermoduler](/help/managing-code/git-submodules.md) som ger dig bättre kontroll över de automatiskt genererade pipelines som används för pull-begärandevalidering och som gör att du kan definiera beteenden för viktiga mått under kodsökningsfasen.
   * [Du kan också välja ](/help/managing-code/github-check-config.md) om du vill bevara rapporthistoriken på GitHub, namnge pipelinen och ange pipeline-variabler som passar dina behov.
* Nya OakPal-regler har lagts till i [Cloud Manager Code Quality scan.](/help/using/custom-code-quality-rules.md#oakpal-ui-content-package)
   * Alla nya regler som läggs till från och med juni 2024 är en oföränderlig förändring.
   * Du uppmanas att åtgärda detta så snart som möjligt eftersom dessa nya regler kommer att få rörledningar att misslyckas från och med Cloud Manager augusti 2024.

## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner

### endast mellanlagring och endast produktion {#staging-production-only-pipelines}

Stöd för [endast mellanlagrings- och endast produktionspipelines](/help/using/stage-prod-only.md) har introducerats, vilket gör att du kan dela upp distributionspipelines för fullständig produktion i mindre, specialiserade distributioner.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-cloudmanager_splitpipelines@adobe.com` från den e-postadress som är kopplad till din Adobe ID.
