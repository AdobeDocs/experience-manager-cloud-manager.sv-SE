---
title: Versionsinformation för Cloud Manager 2025.2.0
description: Läs om Cloud Manager 2025.2.0 för Adobe Managed Services.
feature: Release Information
exlid: 669b1f2d8fc68526eb091e0f93f70ab93033d193
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 51dd060ec9b922ace9ce537cac669c61154284e8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.2.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.02.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.2.0 för Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.2.0 är torsdagen den 13 februari 2025.

Nästa planerade version är torsdagen den 13 mars 2025.

## Nyheter {#what-is-new}

<!-- * The AEM Code Quality step now uses SonarQube 9.9 Server, replacing the older 7.4 version. This upgrade brings additional security, performance, and code quality checks, offering more comprehensive analysis and coverage for your projects. --> <!-- CMGR-45683 -->

* **Uppgraderade SonarQube**

  Från och med torsdagen den 13 februari 2025 använder Cloud Manager kodkvalitetssteg nu SonarQube 9.9.5.90363.

  De uppdaterade reglerna, som är tillgängliga för AMS på [den här länken](/help/using/code-quality-testing.md#code-quality-testing-step), avgör säkerhetspoängen och kodkvaliteten för Cloud Manager-pipelines.

* SonarQube 9.9 är nu standardmotor för kodkvalitetskontroll för alla kunder.

* **Stöd för Java 17 och Java 21-byggmiljö**

  Kunderna kan nu bygga med Java 17 eller Java 21 som tillval, och dra nytta av prestandaförbättringar och nya språkfunktioner. Se [Byggmiljö](/help/getting-started/build-environment.md) för konfigurationssteg, inklusive uppdatering av projektbeskrivningen för Maven och vissa biblioteksversioner.

  >[!NOTE]
  >I Cloud Service-miljöer, när byggversionen är inställd på Java 17 eller Java 21, är standardvärdet Java 21.

* **Valideringar av innehållskopiering har utökats**

  Verifieringsreglerna för innehållskopiering har uppdaterats. I den här versionen kan användare inte längre utlösa en innehållskopia om det finns aktiva pipeline-körningar i käll- eller målmiljön. Användarna måste vänta tills alla pågående pipeline-körningar är klara innan de startar en innehållskopia.

<!-- 
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features.

### Bring Your Own Git - now with support for GitLab and Bitbucket {#gitlab-bitbucket}

The **Bring Your Own Git** feature has been expanded to include support for external repositories, such as GitLab and Bitbucket. This new support is in addition to the already existing support for private and enterprise GitHub repositories. When you add these new repos, you can also link them directly to your pipelines. You can host these repositories on public cloud platforms or within your private cloud or infrastructure. This integration also removes the need for constant code synchronization with the Adobe repository and provides the ability to validate pull requests before merging them into a main branch.

Pipelines using external repositories (excluding GitHub-hosted ones) and the **Deployment Trigger** set to **On Git Changes** now start automatically.

See [Add external repositories in Cloud Manager](/help/managing-code/external-repositories.md).

![Add Repository dialog box](/help/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Currently, the out-of-the-box pull request code quality checks are exclusive to GitHub-hosted repositories, but an update to extend this functionality to other Git vendors is in the works.

If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->


<!-- ## Bug fixes {#bug-fixes}

* A

Known Issues {#known-issues}

* A -->
