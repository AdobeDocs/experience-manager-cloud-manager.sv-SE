---
title: Versionsinformation för 2018.9.0
seo-title: Versionsinformation om AEM Cloud Manager för 2018.9.0
description: Följ den här sidan om du vill ha information om Cloud Manager version 2018.9.0.
seo-description: Följ den här sidan om du vill ha information om AEM Cloud Manager version 2018.9.0.
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---


# Versionsinformation för 2018.9.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0-versionen har stöd för ett Adobe I/O-baserat API, inklusive händelser, för integrering av CI/CD-pipeline för [!UICONTROL Cloud Manager] med andra system. Det börjar också skriva om UI-lagret i React.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2018.9.0 är 1 november 2018.

## Nyheter {#whats-new}

* **CI/CD Pipeline**  - Nytt API och Event-system för integrering av  [!UICONTROL Cloud Manager]CI/CD-pipeline med andra system. Mer information finns i [!UICONTROL Cloud Manager] API-dokumentation (https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html).

* **Användargränssnitt**  - Introduktion till ett nytt användargränssnittslager som är mer responsivt.

## Felkorrigeringar {#bug-fixes}

* I [!UICONTROL Cloud Manager] 2018.8.0 listades varaktigheterna för aktivitetssidan i minuter och timmar, men den informationen visades inte i tabellhuvudet.
* I enstaka fall kunde man inte starta den nya programprojektguiden.
* Knappetiketten i den nya programprojektguiden var vilseledande.
* I vissa fall kan du klicka på knappen Detaljer på sidan Aktivitet för att dirigera om sidan Översikt.
* Vissa sällsynta och oväntade omständigheter har lett till att ett kort saknas på sidan Översikt.
* Ikonen Resurser visades på sidan Programlista för alla kunder.
* När fel uppstod i bakomliggande led verkar ibland en pipeline-körning finnas kvar i *steget Validera*.
* Under vissa omständigheter var längden på programbeskrivningen felaktig.

## Kända fel {#known-issues}

* Förgreningar som har skapats med programprojektguiden får inte innehålla streck.
* Meddelandesidlisten i Adobe [!UICONTROL Experience Cloud] kanske inte läser in meddelanden på ett konsekvent sätt. Meddelanden visas emellertid i Adobe [!UICONTROL Experience Cloud] och, om de är konfigurerade, skickas de fortfarande via e-post.

