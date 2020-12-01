---
title: Versionsinformation för 2019.10.0
seo-title: Versionsinformation om AEM Cloud Manager för 2019.10.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2019.10.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2019.10.0.
translation-type: tm+mt
source-git-commit: 52c54568d8ab7b5091c25b3b65b4baa126bf61f5
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Versionsinformation för 2019.10.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] Release 2019.10.0 och lägger till uppdateringar i distributionssteg och hantering av maven-projektversioner.
Mer information finns i avsnitten nedan.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2019.10.0 är 10 oktober 2019.

## Nyheter {#whats-new}

* Betydande delar av driftsättningsstegen har blivit mer prestandaförbättringar.
* När så är lämpligt kommer byggprojektet Maven att innehålla projektversionen i Git.
* Vid byggtillfället finns nya miljövariabler tillgängliga.
* Icke-produktionsförlopp kan tas bort från kortet på sidan **Översikt** samt API:t.
* Det finns ett nytt valfritt godkännandesteg direkt efter steget för att distribuera scenen, men före steget för säkerhetstestet.
* När du konfigurerar en CI/CD-pipeline kan frånkoppling och koppling av dispatcherinstanser från belastningsutjämnaren hoppas över för dev- och scenmiljöer.
Mer information finns i **[Distributionsprocess](deploying-code.md#deployment-process)**.
* CLI:n för Cloud Manager har utökats för att ge stöd åt loggar för körningssteg.
* Molnhanterarens API har nu stöd för redigering av en pipeline-konfigurerad gren.
* Begäranden som utförs under prestandatestning inkluderar nu en specifik token ***CloudManagerTest*** i användaragenten.

## Felkorrigeringar {#bug-fixes}

* Vissa av korten på sidan **Översikt** justerades inte vertikalt korrekt.
* Vissa feltillstånd medförde inte att pipeline-körningar markerades korrekt och förhindrade efterföljande körningar.
