---
title: Versionsinformation för 2019.8.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.8.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.8.0.
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2019.8.0.
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---

# Versionsinformation för 2019.8.0 {#release-notes-for}

I version [!UICONTROL Cloud Manager] 2019.8.0 finns stöd för selektiva, inbyggda innehållspaket, bättre byggprestanda och en mängd mindre fel har åtgärdats.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.8.0 är 19 augusti 2019.

## Nyheter {#whats-new}

* Nytt kommandoradsgränssnitt till Cloud Manager API, som drivs av [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager).
* Specifika innehållspaket som skapas av bygget kan deklareras som överhoppningsbara och kommer inte att distribueras. Mer information finns i avsnittet ***Hoppa över innehållspaket*** i [Skapa ett AEM-programprojekt](create-an-application-project.md) .
* Uppsättningen med förinlästa beroenden i byggbehållaren har omarbetats för att undvika onödiga nätverksbegäranden.
* Meddelandet på översiktssidan för vissa felaktigt konfigurerade program har förbättrats.

## Felkorrigeringar {#bug-fixes}

* Vid åtkomst till SLA-rapporter var standardåret 2018, inte 2019.
* För långa miljönamn ökade inte systemväljaren på rapportskärmen korrekt.
* Regeln ***ConfigAndInstallShouldOnlyContainOsgiNodes*** -kodkvalitet genererade falska positiva utfall när Sling Rewriter-komponenten användes.
* Regeln ***ConfigAndInstallShouldOnlyContainOsgiNodes*** -kodkvalitet genererade felaktiga positiva värden för vissa ovanliga sökvägsstrukturer.
* Kunder som bara har tillgång till resurser har kanske inte konsekvent kunnat navigera till sina AEM-miljöer.
* Dialogrutan [!UICONTROL Create a Branch and Project] återges på olika sätt i olika webbläsare.
