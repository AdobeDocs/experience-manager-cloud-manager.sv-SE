---
title: Versionsinformation för 2019.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.8.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.8.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.8.0.
translation-type: tm+mt
source-git-commit: 2ada697ca21acd0c73dbce2bce3e9481ac50272c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Versionsinformation för 2019.8.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0-versionen har stöd för selektiva, inbyggda innehållspaket, förbättrad byggprestanda och en mängd mindre fel har åtgärdats.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.8.0 är 19 augusti 2019.

## Nyheter {#whats-new}

* Nytt kommandoradsgränssnitt till Cloud Manager-API:t som drivs av [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager).
* Specifika innehållspaket som skapas av bygget kan deklareras som överhoppade och kommer inte att distribueras. Mer information finns i [Hoppar över innehållspaket](/help/using/setting-up-project.md#skipping-content-packages).
* Uppsättningen med förinlästa beroenden i byggbehållaren har omarbetats för att undvika onödiga nätverksbegäranden.
* Meddelandet på översiktssidan för vissa felaktigt konfigurerade program har förbättrats.

## Felkorrigeringar {#bug-fixes}

* Vid åtkomst till SLA-rapporter var standardåret 2018, inte 2019.
* För långa miljönamn ökade inte miljöväljaren på rapportskärmen korrekt.
* Kodkvalitetsregeln ***ConfigAndInstallShouldOnlyContainOsgiNodes*** genererade falskt positiva utfall när komponenten Sling Rewriter användes.
* Kodkvalitetsregeln ***ConfigAndInstallShouldOnlyContainOsgiNodes*** genererade felaktiga positiva värden för vissa ovanliga sökvägsstrukturer.
* Kunder som bara har tillgång till resurser har kanske inte konsekvent kunnat navigera till sina AEM miljöer.
* Dialogrutan Skapa en gren och projekt renderades olika i olika webbläsare.
