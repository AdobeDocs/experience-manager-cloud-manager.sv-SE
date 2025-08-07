---
title: Versionsinformation för Cloud Manager 2025.8.0
description: Läs om Cloud Manager 2025.8.0 för Adobe Managed Services.
feature: Release Information
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 73a094f47f518e2782ac96357e1adc4e923a0b63
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.8.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.04.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.8.0 i Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.8.0 är torsdagen den 7 augusti 2025.

<!-- There are no significant new features or bug fixes in the May Cloud Manager release. -->

Nästa planerade version är torsdagen den 4 september 2025.

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


## Beta {#beta-program}

Delta i Cloud Manager Beta-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande möjligheter är för närvarande tillgängliga:


### Hämta din egen Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Kunderna kan nu lägga in sina Azure DevOps Git-databaser i Cloud Manager, med stöd för både moderna Azure DevOps-databaser och äldre VSTS-databaser (Visual Studio Team Services).

* För Edge Delivery Services-användare kan den inbyggda databasen användas för att synkronisera och distribuera platskod.
* För AEM as a Cloud Service- och Adobe Managed Services-användare (AMS) kan databasen länkas till både fullständiga och frontbaserade pipelines.

Stöd för fler pipelinetyper och pull-begäran-validering via pipelines för kodkvalitet kommer snart.

Se [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/release-notes/assets/azure-repo.png)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.

#### Hantera åtkomsttoken{#manage-access-tokens}

Använd **Hantera åtkomsttoken** i Cloud Manager för att visa, byta namn på och ta bort åtkomsttoken som är kopplade till externa BYOG-databaser, som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se [Hantera åtkomsttoken](/help/managing-code/manage-access-tokens.md).

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) från den e-postadress som är kopplad till din Adobe ID.








Funktionen **Hämta din egen Git** (BYOG) har utökats med stöd för externa databaser, som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Integreringen eliminerar också behovet av konstant kodsynkronisering med Adobe-databasen och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Pipelinjer som använder externa databaser (utom GitHub-värddatabaser) och **Distributionsutlösaren** som är inställd på **Vid Git-ändringar** startar nu automatiskt.

Se [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

#### Hantera åtkomsttoken{#access-tokens}

Använd **Hantera åtkomsttoken** med BYOG för att visa, byta namn på och ta bort åtkomsttoken som är associerade med externa Bring Your Own Git-databaser, som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se [Hantera åtkomsttoken](/help/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->


## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i juliversionen av Cloud Manager.

<!--
Known Issues {#known-issues}

* A -->
