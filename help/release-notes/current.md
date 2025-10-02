---
title: Versionsinformation för Cloud Manager 2025.10.0
description: Läs om Cloud Manager 2025.10.0 för Adobe Managed Services.
feature: Release Information
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 03fc811a1a617263efd0f1d5667bba6975826a0e
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.10.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.04.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.10.0 för Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.10.0 är torsdagen den 2 oktober 2025.

<!-- There are no significant new features or bug fixes in the May Cloud Manager release. -->

Nästa planerade version är torsdagen den 6 november 2025.

<!-- SAVE FOR FUTURE POSSIBLE USE There are no significant new features or bug fixes in the May Cloud Manager release. -->

## Nyheter {#what-is-new}







## Beta {#beta-program}

Delta i Cloud Manager Beta-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande möjligheter är för närvarande tillgängliga:

### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/experience-hub/experience-hub) fungerar som startpunkt för AEM och är anpassad efter organisationens behov. Berätta för Adobe om de befintliga AEM-gränssnittstilläggen så att du enkelt kan aktivera dem i Experience Hub.

![Diagram över Experience Hub arbetsflöde för utbyggbarhet och anpassning](/help/release-notes/assets/experience-hub-extensibility-customization.png)

Bädda in anpassade upplevelser i Experience Hub för att utöka och personalisera organisationens kontrollpanel. Förutom Adobe inbyggda widgetar kan du lägga till egna med hjälp av ramverket [UI Extensibility](https://developer.adobe.com/uix/docs/) . Bygg JavaScript-baserade gränssnittsappar och visa upp dem för användarna för att uppfylla företagsspecifika krav och arbetsflöden.

Intresserad av betaversionen? Mejla [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) med ditt Adobe OrgID och en kort beskrivning av den anpassning du tänker skapa.

### Bygger snabbare med modulcachning {#quick-build-cm-pipelines}

En ny byggmodell kompilerar endast ändrade moduler (i stället för hela repon) med cache-lagring på modulnivå för att korta byggtiden. Det gäller för rörledningar med kodkvalitet, fullständig stapel och enbart scener.

Intresserad av betaversionen? Mejla [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) med ditt Adobe OrgID och program-ID.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline variables](/help/getting-started/build-environment.md#pipeline-variables). -->


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

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->

## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i oktober-versionen av Cloud Manager.

<!--
Known Issues {#known-issues}

* A -->
