---
title: Versionsinformation för Cloud Manager 2024.12.0
description: Läs om Cloud Manager 2024.12.0 på Adobe Managed Services.
feature: Release Information
exl-id: 811567af-66c9-4c1f-ae9e-60603b70ef80
source-git-commit: e266a4192e2a897f142a6c83ae5766483946320d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2024.12.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2024.12.0 i Adobe Managed Services.

>[!NOTE]
>
>Se [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

<!-- SAVE FOR FUTURE POSSIBLE USE No notable bugs or features for the September release of Cloud Manager. -->

Versionsdatumet för [!UICONTROL Cloud Manager] 2024.12.0 är 5 december 2024.

Nästa planerade version är 23 januari 2025.

<!-- ## What's new {#what-is-new} -->

<!-- * The AEM Code Quality step now uses SonarQube 9.9 Server, replacing the older 7.4 version. This upgrade brings additional security, performance, and code quality checks, offering more comprehensive analysis and coverage for your projects. --> <!-- CMGR-45683 -->

## Program för tidigt antagande {#early-adoption}

Bli en del av Cloud Manager program för tidig användning och få möjlighet att testa kommande funktioner.

### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

Funktionen **Hämta egen Git** har utökats med stöd för externa databaser, som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Den här integreringen eliminerar också behovet av konstant kodsynkronisering med databasen Adobe och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Pipelinjer som använder externa databaser (utom GitHub-värddatabaser) och **Distributionsutlösaren** som är inställd på **Vid Git-ändringar** startar nu automatiskt.

Se [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.


<!-- ## Bug fixes {#bug-fixes}

* A

Known Issues {#known-issues}

* A -->
