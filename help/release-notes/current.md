---
title: Versionsinformation om Cloud Manager 2026.3.0
description: Läs om Cloud Manager 2026.3.0 för Adobe Managed Services.
feature: Release Information
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 9ce8a2ca2117992421052b76b0f5c7c9c5a6195b
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2026.3.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.04.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2026.3.0 för Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2026.3.0 är torsdagen den 5 mars 2026.
<!-- There are no significant new features or bug fixes in the May Cloud Manager release. -->

Nästa planerade version är torsdagen den 2 april 2026.

<!-- SAVE FOR FUTURE POSSIBLE USE There are no significant new features or bug fixes in the May Cloud Manager release. -->

## Nyheter {#what-is-new}

* **Stöd för UI-utbyggbarhet i AEM Experience Hub**
Stöd för gränssnittstillägg i [&#x200B; AEM Experience Hub &#x200B;](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/experience-hub/experience-hub) är nu aktiverat, vilket gör att utvecklare kan utöka gränssnittet med anpassade funktioner och widgetar som skapats med Adobe App Builder.

  Mer information finns i [AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/).

* **Konfigurationspipelines stöder nu hanterade hemligheter**

  Användare kan nu lägga till och hantera hemligheter direkt i Cloud Manager konfigurationspipelines. Dessa hemligheter åsidosätter på ett säkert sätt värden i pipeline-konfigurationsspecifikationen och stöder flexibla, miljöspecifika distributioner.

  ![Alternativet Visa/redigera variabler på den nedrullningsbara menyn för en vald pipeline](/help/release-notes/assets/view-edit-variables-option.png)
  *Visa/redigera variabelalternativ i listrutan för en vald pipeline.*

  ![Dialogrutan Variabelkonfiguration &#x200B;](/help/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*Dialogrutan Variabelkonfiguration.*

* **Förbättrad stabilitet, prestanda och tillförlitlighet**

  Den här versionen innehåller optimerings- och underhållsuppdateringar som förbättrar stabiliteten, prestandan och tillförlitligheten i Cloud Manager.


## Beta {#beta-program}

Delta i Cloud Manager Beta-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande möjligheter är för närvarande tillgängliga:

<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/experience-hub/experience-hub) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### Bygger snabbare med modulcachning {#quick-build-cm-pipelines}

En ny byggmodell kompilerar endast ändrade moduler (i stället för hela repon) med cache-lagring på modulnivå för att korta byggtiden. Det gäller för rörledningar med kodkvalitet, fullständig stapel och enbart scener.

![Dialogrutan Redigera icke-produktionspipeline som visar två alternativ för byggstrategi som är Fullständigt bygge och Smart bygge](/help/release-notes/assets/non-production-pipeline-edit.png)
*Dialogrutan Redigera icke-produktionsförlopp visar två alternativ för Build Strategy som är Full Build och Smart Build.*

I dialogrutan **Lägg till/redigera pipeline**, under fliken **Source-kod**, finns ett nytt avsnitt i avsnittet **Skapa strategi** där du kan välja något av följande byggalternativ:

* **Fullständigt bygge** - Skapar alla moduler i databasen vid varje körning.
* **Smart Build** - Skapar bara moduler som ändrats sedan den senaste implementeringen, vilket förkortar den totala byggtiden.

Du styr vilka pipelines som använder **Smart build**. Under betaversionen visas det här alternativet endast för **kodkvalitet**- och **dev-distribution**-pipelines.

Intresserad? Mejla [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) med ditt Adobe OrgID och program-ID.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline variables](/help/getting-started/build-environment.md#pipeline-variables). -->

## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i mars 2026-versionen av Cloud Manager om AMS.

<!--
Known Issues {#known-issues}

* A -->
