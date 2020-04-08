---
title: Versionsinformation för 2020.3.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.3.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.3.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.3.0
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# Versionsinformation för 2020.3.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.3.0 är 5 mars 2020.

## Nyheter {#whats-new}

* Loggen för byggsteget är nu tillgänglig medan byggsteget körs.
* Vissa av meddelandena på informationssidan för pipeline-körning har redigerats för tydlighet.

## Felkorrigeringar {#bug-fixes}

* Vissa distributionskonfigurationer kan göra att loggar för distributionsstegen inte är tillgängliga om distributionen misslyckas.
* Specifika fel i distributionsstegen för Managed Services-program kan göra att efterföljande körningar inte kan startas.
* Den tillfälliga SonarQube-instansen som användes i byggsteget misslyckades ibland att starta inom den konfigurerade tidsgränsen.
* I specifika projekt ska *ResourceResolver-objekten alltid stängas* vilket ger ett Null-pekarundantag. Detta påverkade dock inte genomförandet av pipeline.