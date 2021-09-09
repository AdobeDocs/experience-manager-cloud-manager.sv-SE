---
title: Versionsinformation för 2021.8.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.8.0
feature: Release Information
source-git-commit: 3fccb0b577662ebc12b65777cbf9624e06d4259d
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# Versionsinformation för 2021.8.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.8.0.

>[!NOTE]
>Se [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) för att se den senaste versionsinformationen för Cloud Manager i AEM som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.8.0 är 12 augusti 2021.


## Nyheter {#whats-new}

* Självbetjäning som gör att användare kan skapa och hantera flera databaser via användargränssnittet i Cloud Manager.

* SonarQube läste git-historikdata i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 29.

## Felkorrigeringar {#bug-fixes}

* När en pipeline aktiveras två gånger av någon anledning resulterar det i att en av körningarna misslyckas med *det går inte att uppdatera pipelinekörningsstatus*-fel.
