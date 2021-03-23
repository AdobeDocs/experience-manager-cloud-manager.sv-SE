---
title: Versionsinformation för 2020.1.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.1.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.1.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.1.0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# Versionsinformation för 2020.1.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.1.0 och innehåller uppdateringar för åtkomst av Git-autentiseringsuppgifter och inloggningsupplevelsen.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.1.0 är 16 januari 2020.

## Nyheter {#whats-new}

* Git-inloggningsuppgifter kan nu hämtas inifrån användargränssnittet i Cloud Manager. Mer information finns i [Accessing Git](/help/using/accessing-git.md).
* Inloggningsupplevelsen och URL-strukturen har ändrats som en del av ett initiativ som omfattar hela Adobe. Gamla bokmärken dirigeras om till de nya URL-adresserna.


## Felkorrigeringar {#bug-fixes}

* Distributioner av topologier som bara är avsedda för författare distribuerade inte ändringar i dispatcherkonfigurationen.
* I vissa konfigurationer gick det inte att skapa endast en pipeline för kodkvalitet.
* Miljösammanfattningskortet på översiktssidan återgavs ibland inte korrekt.
* Pipeline-exekveringar kan göra timeout för stora topologier.
