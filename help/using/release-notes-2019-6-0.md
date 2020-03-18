---
title: Versionsinformation för 2019.6.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.8.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.6.0.
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2019.6.0.
translation-type: tm+mt
source-git-commit: 7cfa0cf66efd5891263bfcc83a5149daec5c8b67

---

# Versionsinformation för 2019.6.0 {#release-notes-for}

I version [!UICONTROL Cloud Manager] 2019.6.0 har nya regler för kodkvalitet och en ny produktuppdateringsguide lagts till. Mer information finns i avsnitten nedan.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.6.0 är 20 juni 2019.

## Nyheter {#whats-new}

* Guiden Ny produktuppdatering hjälper kunderna att köra en AEM-uppdatering. Läs mer i [produktuppdateringsguiden](overview-productupdate-wizard.md) .
* Kodkvalitetsregler som undersöker innehållsstrukturer. Mer information finns i [Anpassade regler](custom-code-quality-rules.md) för kodkvalitet.
* Den största tillåtna storleken för Git-överföring har ökats till 1 GB.

## Felkorrigeringar {#bug-fixes}

* I vissa fall kunde rörledningar inte startas på grund av ett tidigare fel.

## Kända fel {#known-issues}

* CSV-hämtningen av kodkvalitet sorteras inte alltid efter allvarlighetsgrad.
* Felaktiga positiva värden kan rapporteras av regeln *ConfigAndInstallShouldOnlyContainOsgiNodes* om OSGi-konfigurationer placeras i en kapslad mapp under en *konfigurationsmapp* .