---
title: Versionsinformation för 2023.8.0
description: Detta är versionsinformationen för Cloud Manager version 2023.8.0.
feature: Release Information
source-git-commit: 26c4c945e18f21b812f65dbabc14a4e8ab9f6b43
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager version 2023.8.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2023.8.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Utgivningsdatum för [!UICONTROL Cloud Manager] version 2023.8.0 är 10 augusti 2023. Nästa version är planerad till den 14 september 2023.

## Nyheter {#what-is-new}

* Förbättringar har gjorts för att förbättra förståelsen och visningen av felmeddelanden i användargränssnittet i Cloud Manager.

## Felkorrigeringar {#bug-fixes}

* Sällsynta fall [innehållskopia](/help/using/content-copy.md) processer som fastnar har åtgärdats.
* Ett tillfälligt testproblem har lösts för kunder som inte använder New Relic One.
* [Anpassade regler för kodkvalitet](/help/using/custom-code-quality-rules.md) `SupportedRunmode` och `ImmutableMutableMixedPackage` har tagits bort från SonarQube eftersom de endast är tillämpliga på AEM as a Cloud Service.
* Användare kommer inte längre att stöta på fasta rörledningar som verkar vara i körläge.
* The **Miljö** menyn stängs nu när **[Kopiera innehåll](/help/using/content-copy.md)** modal.
* [En omkörning av en pipeline](/help/using/code-deployment.md#reexecute-deployment) tillåts inte längre om föregående körning inte har en `commitId` anges för byggfastillståndet.
* Ett mer begripligt meddelande visas nu för sällsynta fel när en användare klickar på en pipeline i **Aktivitet** eller **Pipeline** skärmar.
