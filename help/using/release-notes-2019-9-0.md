---
title: Versionsinformation för 2019.9.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.9.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.9.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.9.0.
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---

# Versionsinformation för 2019.9.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0-utgåvan uppdaterar säkerhetstestkriterierna, lägger till hämtningsbara övervakningsdiagram och åtgärdar vissa kundrapporterade användbarhetsproblem.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.9.0 är 12 september 2019.

## Nyheter {#whats-new}

* Kategoriseringen av hälsokontrollen för Sling Referrer-filtret har ändrats från Kritisk till Viktigt.
* Kategoriseringen av HTML Library Manager Config-hälsokontrollen har ändrats från Kritisk till Viktigt.
* Det går nu att hämta övervakningsdiagram. Mer information finns i [Övervaka dina miljöer](monitor-your-environments.md).
* Om ett program inte har någon AEM för produktion kommer du att navigera till översiktssidan för Cloud Manager genom att klicka på programkortet från landningssidan, utan att skapa någon feldialogruta.
* Kortet **Pipeline Settings** på sidan **Översikt** har fått namnet **Production Pipeline Settings**.
* Alternativknapparna för det viktiga felbeteendet har tagits bort från enbart pipelines för kodkvalitet.
* Sidan **Aktivitet** visar nu namnet på pipeline för varje körning.
* Körningssidan visar nu namnet på pipeline.
* I dialogrutan Sammanfattning av kodkvalitet visas nu en beskrivning av varje klassificering.

## Felkorrigeringar {#bug-fixes}

* Vissa användare kunde inte visa körningsinformation när de väntade på godkännande.
* Högermarginalen var inte konsekvent på sidan **Översikt**.
* Byggbehållaren kan få slut på minne i stora projekt.
* Under vissa omständigheter kunde regeln BannedPaths OakPAL inte identifiera installerat innehåll under /libs.
* När en kvalitetsport avvisades, visade fortfarande dialogrubriken *Delvis passerad*.

## Kända fel {#known-issues}

* Det går inte att hämta övervakningsdiagram i Safari.
