---
title: Versionsinformation för Cloud Manager 2025.4.0
description: Läs om Cloud Manager 2025.4.0 för Adobe Managed Services.
feature: Release Information
exl-id: cc1dc94b-129d-4de7-8e57-8fc5dcba7d9f
source-git-commit: 54c03955e66f4b893829d4e8186babc30d4dbdb3
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.4.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.04.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.4.0 på Adobe Managed Services.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.4.0 är torsdagen den 10 april 2025.

Nästa planerade version är torsdagen den 8 maj 2025.

<!--
## What's new {#what-is-new}

* 
-->


## Program för tidigt antagande {#early-adoption}

Delta i Cloud Manager tidiga Adobe-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande tidiga introduktionsmöjligheter finns för närvarande:

### Använd din egen Git - nu med stöd för GitLab och Bitbucket {#gitlab-bitbucket}

Funktionen **Hämta egen Git** har utökats med stöd för externa databaser, som GitLab och Bitbucket. Det nya stödet är utöver det stöd som redan finns för privata och företags GitHub-databaser. När du lägger till dessa nya rapporter kan du även länka dem direkt till dina rörledningar. Du kan lagra dessa databaser på publika molnplattformar eller i ditt privata moln eller din privata infrastruktur. Integreringen eliminerar också behovet av konstant kodsynkronisering med Adobe-databasen och ger möjlighet att validera pull-begäranden innan de slås samman till en huvudgren.

Pipelinjer som använder externa databaser (utom GitHub-värddatabaser) och **Distributionsutlösaren** som är inställd på **Vid Git-ändringar** startar nu automatiskt.

Se [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>För närvarande gäller kvalitetskontrollerna av koden för pull-begäran som är klar endast för GitHub-värdbaserade databaser, men en uppdatering som utökar den här funktionen till andra Git-leverantörer finns i arbetsflödet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.

### Rörledningar som endast är avsedda för mellanlagring och enbart för produktion {#staging-production-only-pipelines}

Adobe presenterar stöd för [endast mellanlagrings- och endast produktionspipelines](/help/using/stage-prod-only.md). Med den här nya funktionen kan du dela upp rörledningar för driftsättning i högklassig produktion i mindre, mer specialiserade driftsättningar.

Om du vill testa den här funktionen och lämna feedback skickar du ett e-postmeddelande till [Grp-cloudmanager_splitpipelines@adobe.com](mailto:Grp-cloudmanager_splitpipelines@adobe.com) från den e-postadress som är kopplad till din Adobe ID.



<!--
### Self-service Service Pack updates for AMS Cloud Manager customers 

As part of the early adopters program, Adobe Managed Services Cloud Manager customers can now perform self-service service pack updates through the **Cloud Manager** user interface. This feature is currently available *only for development environments* and includes limited error reporting for failures.  

Customers can check for service pack updates on the **Program Overview** page under the **Environments** section (**three-dot menu**).

![Check for updates menu option](/help/release-notes/assets/check-for-updates-1.png)

![Update Service Pack dialog box](/help/release-notes/assets/check-for-updates-2.png)

The installation and upgrade process can be tracked on the **Activity** page. 

Once the process is complete, customers must **approve the execution** for the service pack upgrade to finalize successfully.

![Approve service page update](/help/release-notes/assets/check-for-updates-3.png)

If you are interested in testing this new feature and sharing your feedback, contact your Adobe Customer Success Engineer.

See also [Service Pack Updates for Development Environments - Early Adopter](/help/using/service-packs-environments.md).
-->


<!--
## Bug fixes {#bug-fixes}

* A

Known Issues {#known-issues}

* A -->
