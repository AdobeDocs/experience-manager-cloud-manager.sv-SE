---
title: Versionsinformation för 2020.1.0
seo-title: Versionsinformation om AEM Cloud Manager för 2020.1.0
description: Följ den här sidan för att få information om Cloud Manager version 2020.1.0
seo-description: Följ den här sidan för att få information om AEM Cloud Manager version 2020.1.0
translation-type: tm+mt
source-git-commit: 854c09878a633bd46e4d7e9d604a8335c225a1c4

---

# Versionsinformation för 2020.1.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2020.1.0 och dessutom läggs uppdateringar till för åtkomst av Git-inloggningsuppgifter och inloggningsupplevelsen.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.1.0 är 16 januari 2020.

## Nyheter {#whats-new}

* Git-inloggningsuppgifter kan nu hämtas inifrån användargränssnittet i Cloud Manager. Mer information finns i [Accessing Git](/help/using/accessing-git.md) .
* Inloggningsupplevelsen och URL-strukturen har ändrats som en del av ett Adobe-omfattande initiativ. Gamla bokmärken dirigeras om till de nya URL-adresserna.


## Felkorrigeringar {#bug-fixes}

* Distributioner av topologier som bara är avsedda för författare distribuerade inte ändringar i dispatcherkonfigurationen.
* I vissa konfigurationer gick det inte att skapa endast en pipeline för kodkvalitet.
* Miljösammanfattningskortet på översiktssidan återgavs ibland inte korrekt.
* Pipeline-körningar kan timeout inträffa i stora topologier.
