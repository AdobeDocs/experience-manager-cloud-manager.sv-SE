---
title: Versionsinformation för Cloud Manager 2025.1.0
description: Läs om Cloud Manager 2025.1.0 på Adobe Managed Services.
feature: Release Information
source-git-commit: c25508b24f00b8f8cfa7bae3cc4b0d6ecf684db3
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.1.0 i Adobe Managed Services {#release-notes}

<!-- RELEASE WIKI  https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release -->

Läs mer om [!UICONTROL Cloud Manager] 2025.1.0 i Adobe Managed Services.

>[!NOTE]
>
>Se [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/home).

## Releasedatum {#release-date}

<!-- SAVE FOR FUTURE POSSIBLE USE No notable bugs or features for the September release of Cloud Manager. -->

Lanseringsdatumet för [!UICONTROL Cloud Manager] 2025.1.0 är onsdagen den 22 januari 2024.

Nästa planerade version är torsdagen den 13 februari 2025.

## Nyheter {#what-is-new}

**Regler för kodkvalitet:** Cloud Manager Code Quality step kommer att börja använda SonarQube Server 9.9 med Cloud Manager version 2025.2.0, som är planerad till torsdagen den 13 februari 2025.

Uppdaterade SonarQube-regler finns nu tillgängliga på [Kodkvalitetsregler](/help/using/code-quality-testing.md#code-quality-testing-step) för att förbereda.

Du kan&quot;kontrollera&quot; de nya reglerna tidigt genom att ange följande textvariabel för pipeline (se skärmbild nedan):

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

Ange dessutom följande variabel för att säkerställa att kodkvalitetssteget körs för samma implementering (som normalt hoppas över för samma `commitId`):

`CM_DISABLE_BUILD_REUSE` = `true`

![Konfigurationssida för variabler](/help/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe rekommenderar att du skapar en ny CI/CD Code Quality-pipeline som är konfigurerad till samma gren som huvudproduktionsflödet. Ställ in lämpliga variabler *före* den 13 februari 2025 för att verifiera att de nya tvingande reglerna inte inför blockerare.

<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


<!-- ## Bug fixes {#bug-fixes}

* A

Known Issues {#known-issues}

* A -->
