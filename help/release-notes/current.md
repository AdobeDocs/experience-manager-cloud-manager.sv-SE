---
title: Versionsinformation för Cloud Manager 2025.7.0
description: Läs om Cloud Manager 2025.7.0 för Adobe Managed Services.
feature: Release Information
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 106caded8056a8a667b6c702b573566f9358f401
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.7.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.04.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.7.0 i Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.7.0 är torsdagen den 10 juli 2025.

<!-- There are no significant new features or bug fixes in the May Cloud Manager release. -->

Nästa planerade version är torsdagen den 7 augusti 2025.

<!-- SAVE FOR FUTURE POSSIBLE USE There are no significant new features or bug fixes in the May Cloud Manager release. -->


## Nyheter {#what-is-new}

* **Rörledningar som endast är avsedda för mellanlagring och enbart för produktion**

  Cloud Manager har nu stöd för rörledningar som endast är avsedda för staging och produktion. Med den här funktionen kan du dela upp produktionsdistributioner i högar i mindre, avsedda rörledningar. <!-- This feature went into GA from Private beta in the June 5, 2025 CM release -->

  ![Lägg till en icke-produktionsförloppsdialogruta med alternativknappen Full Stack Code markerad och scenmiljön markerad](/help/release-notes/assets/add-non-production-pipeline.png)

  Se [Endast scenen och Endast produkter](/help/using/stage-prod-only.md).

* **Pipeline-favoriter**

  I den här versionen av Cloud Manager introducerar du möjligheten att fästa favoritledningar, så att du kan markera specifika pipelines som favoriter så att de visas högst upp i listan på sidan **Pipelines**. Den här förbättringen gör det enklare att hitta och köra rörledningar som du ofta använder. <!-- CMGR-68293 -->

  ![Rörledningar markerade som favoriter](/help/release-notes/assets/pipeline-favorites.png) *Två rörledningar markerade som favoriter.*

  Se [Markera pipeline-favoriter](/help/using/managing-pipelines.md#pipeline-favorites).


## Program för tidig användning {#beta-program}

Delta i Cloud Manager alfa- och betaprogram för att få exklusiv tillgång till kommande funktioner innan de släpps.

Följande möjligheter är för närvarande tillgängliga:


### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

Funktionen **Hämta din egen Git** (BYOG) har utökats med stöd för externa databaser, som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Integreringen eliminerar också behovet av konstant kodsynkronisering med Adobe-databasen och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Pipelinjer som använder externa databaser (utom GitHub-värddatabaser) och **Distributionsutlösaren** som är inställd på **Vid Git-ändringar** startar nu automatiskt.

Se [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.

#### Hantera åtkomsttoken{#access-tokens}

Använd **Hantera åtkomsttoken** med BYOG för att visa, byta namn på och ta bort åtkomsttoken som är associerade med externa Bring Your Own Git-databaser, som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se [Hantera åtkomsttoken](/help/managing-code/manage-access-tokens.md).

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.


## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i juliversionen av Cloud Manager.

<!--
Known Issues {#known-issues}

* A -->
