---
title: Navigera i användargränssnittet för Cloud Manager
description: Lär dig hur användargränssnittet i Cloud Manager är organiserat och hur du navigerar för att hantera program och miljöer.
exl-id: 9c1545ce-1c6d-417f-a6f4-fe53caef3433
source-git-commit: 9d0f4dd29e2d05ab3f6900ee23c536b91c849e65
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 0%

---

# Navigera i gränssnittet för molnhanteraren {#navigation}

Lär dig hur användargränssnittet i Cloud Manager är organiserat och hur du navigerar för att hantera program och miljöer.

Användargränssnittet för molnhantering består huvudsakligen av två grafiska gränssnitt:

* [The My Programs console](#my-programs) där du kan visa och hantera alla program.
* [Fönstret Programöversikt](#program-overview) där du kan se detaljerna i och hantera ett enskilt program.

## My Programs Console {#my-programs}

När du loggar in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och väljer lämplig organisation kommer du till **Mina program** konsol.

![My Programs console](assets/my-programs-console.png)

Konsolen Mina program ger en översikt över alla program som du har tillgång till i den valda organisationen. Den består av flera delar.

1. [Verktygsfält](#toolbars-my-programs-toolbars) för organisationsval, aviseringar och kontoinställningar
1. [Statistik och uppmaning](#statistics) för en översikt över din senaste aktivitet
1. [Program och licenser](#programs-license) för att förstå din nuvarande licensstatus och hantera dina program
1. [Snabblänkar](#quick-links) för enkel åtkomst till relaterade resurser

>[!TIP]
>
>Se dokumentet [Program och programtyper](/help/getting-started/program-setup.md) om du vill ha mer information om programmen.

### Verktygsfält {#my-programs-toolbars}

Det finns två verktygsfält ovanpå varandra.

#### Cloud Manager Header {#cloud-manager-header}

Det första är Cloud Manager-huvudet, som är beständigt när du navigerar i Cloud Manager. Det är en ankarpunkt som ger dig tillgång till inställningar och information som gäller för alla program i Cloud Manager.

![Rubriken Experience Cloud](assets/experience-cloud-header.png)

1. Knappen Cloud Manager tar dig tillbaka till konsolen Mina program i Cloud Manager oavsett var du befinner dig i Cloud Manager.
1. Tryck eller klicka på knappen Feedback för att ge Adobe feedback om Cloud Manager.
1. Organisationsväljaren visar den organisation du är inloggad på (i det här exemplet Foundation Internal). Tryck eller klicka för att växla till en annan organisation om din Adobe ID är kopplad till flera.
1. Om du trycker eller klickar på lösningens väljare kan du snabbt gå över till andra Experience Cloud-lösningar.
1. Hjälpikonen ger snabb åtkomst till utbildningsresurser och supportresurser.
1. Aviseringsikonen är märkt med antalet tilldelade ofullständiga [meddelanden.](/help/using/notifications.md)
1. Välj den ikon som representerar användaren för att få åtkomst till dina användarinställningar. Om du inte har konfigurerat någon användarbild tilldelas ikonen slumpmässigt.

#### Verktygsfältet Program {#program-toolbar}

Verktygsfältet Program innehåller länkar för att växla mellan Cloud Manager-program och åtgärder som passar sammanhanget.

![Verktygsfältet Program](assets/program-toolbar.png)

1. Programväljaren öppnas i en listruta där du snabbt kan välja andra program eller vidta sammanhangsberoende åtgärder som att skapa ett nytt program
1. Länken Komma igång ger dig tillgång till [Dokumentationsresa för introduktion](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/overview) så att du kommer igång med Cloud Manager.
   * Observera att introduktionsresan är utformad för AEM as a Cloud Service och inte för Cloud Service för AMS, men många koncept är desamma.
1. Åtgärdsknappen innehåller sammanhangsberoende åtgärder som att skapa ett nytt program.

### Statistik {#statistics}

Statistikavsnittet innehåller sammanställda data för din organisation, t.ex. om du har konfigurerat dina program kan statistik över dina aktiviteter under de senaste 90 dagarna visa, inklusive:

* Antal [distributioner](/help/using/code-deployment.md)
* Antal [problem med kodkvalitet](/help/using/code-quality-testing.md) identifierad
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Program och licenser {#programs-license}

Huvudinnehållet i My Programs-konsolen är listan över program och licensens status.

#### Fliken Program {#programs}

The **Program** I visas kort som representerar de program du har åtkomst till. Tryck eller klicka på ett kort för att komma åt **Programöversikt** sidan med programmet för att få information om programmet.

Använd sorteringsalternativen för att bättre hitta det program du behöver.

![Sorteringsalternativ](assets/my-programs-sorting.png)

* Sortera efter
   * Skapad den (standard)
   * Programnamn
   * Status
* Stigande (standard) / Fallande
* Stödrastervisning (standard)
* Listvy

Varje program representeras av ett kort (eller en rad i en tabell) som ger en översikt över programmet och snabblänkar för att vidta åtgärder.

![Programkort](assets/program-card.png)

* Programavbildning (om den är konfigurerad)
* Programnamn
* Tjänsttyp: **Experience Manager Cloud** for [AEM as a Cloud Service program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/home) eller **Experience Manager** för AMS-program
* Status
* Konfigurerade lösningar
* Skapad den

Informationsikonen ger dig även snabb åtkomst till ytterligare information om programmet (användbart i listvyn).

![Information](assets/information-view.png)

Ellipsikonen ger dig tillgång till ytterligare åtgärder som du kan vidta i programmet.

![Ellipsknapp för program](assets/program-ellipsis.png)

* Navigera till en viss [miljö](/help/using/managing-environments.md) av programmet
* Öppna [programöversikt](#program-overview)
* [Redigera programmet](/help/getting-started/program-setup.md)
* Visa övervakning

#### Fliken Licens {#license-tab}

The **Licens** ger snabb åtkomst till kontrollpanelen för licenser.

### Snabblänkar {#quick-links}

I avsnittet med snabblänkar får du tillgång till resurser som du använder ofta.

## Programöversiktsfönster {#program-overview}

När du har valt ett program i konsolen Mina program visas programöversikten.

![Programöversikt](assets/program-overview.png)

Programöversikten ger dig tillgång till all information om ett Cloud Manager-program. Precis som My Programs-konsolen består den av flera delar.

1. [Verktygsfält](#program-overview-toolbar) för att snabbt gå tillbaka till My Programs-konsolen och navigera i programmet
1. [Tabbar](#program-tabs) växla mellan olika aspekter av programmet
1. A [uppmaning](#cta) på grundval av programmets senaste åtgärder
1. An [miljööversikt](#environments) av programmet
1. An [Översikt över rörledningarna](#pipelines) av programmet
1. Länkar till [användbara resurser](#useful-resources)

### Verktygsfält {#program-overview-toolbar}

Verktygsfälten i programöversikten liknar de i [Min programkonsol.](#my-programs-toolbars) Här illustreras bara skillnaderna.

#### Cloud Manager Header {#cloud-manager-header-2}

Cloud Manager-huvudet har en hamburgermeny som öppnas automatiskt för att visa de navigerbara flikarna i programöversikten.

![Molnhanterarens hamburgmeny](assets/cloud-manager-hamburger.png)

Tryck eller klicka på menyikonen för hamburgaren för att dölja flikarna.

#### Verktygsfältet Program {#program-toolbar-2}

Verktygsfältet för program ger dig fortfarande möjlighet att snabbt växla till andra program, men ger även tillgång till sammanhangsberoende åtgärder som att lägga till och redigera programmet.

![Verktygsfältet Program](assets/cloud-manager-program-toolbar.png)

Verktygsfältet innehåller dessutom alltid den flik som du är på om du har valt att dölja flikarna med hjälp av hamburgmenyn.

### Programflikar {#program-tabs}

Varje program har många alternativ och data kopplade till sig. Dessa data samlas in på flikar för att underlätta navigeringen i programmet. Flikarna ger dig tillgång till:

* Översikt - Programöversikt enligt beskrivningen i det aktuella dokumentet
* [Aktivitet](/help/using/managing-pipelines.md#activity) - Historiken över programmets rörliga körningar
* [Pipelines](/help/using/managing-pipelines.md#pipelines) - Alla rörledningar som konfigurerats för programmet
* [Databaser](/help/managing-code/repositories.md) - Alla databaser har konfigurerats för programmet
* [Rapporter](/help/using/monitoring-environments.md#system-monitoring-overview) - Mätvärden, t.ex. SLA-data
* [Miljö](/help/using/managing-environments.md) - Alla miljöer som konfigurerats för programmet
* [Innehållsuppsättningar](/help/using/content-copy.md) - Innehållsuppsättningar som skapats för kopieringsändamål
* [Kopiera innehållsaktivitet](/help/using/content-copy.md) - kopieringsaktiviteter
* Utbildningsvägar - ytterligare utbildningsresurser om Cloud Manager

Som standard visas **Ökning** -fliken. Den aktuella fliken markeras. Välj en annan flik om du vill visa information om den.

Använda hamburgermenyn i [Cloud Manager-rubrik](#cloud-manager-header-2) om du vill dölja flikarna.

### Call-to-Action {#cta}

I avsnittet om uppmaning att ringa in får du användbar information beroende på programmets status. För ett nytt program kan du se nästa steg som erbjuds samt en påminnelse om ett publiceringsdatum, [anges när programmet skapas.](/help/getting-started/program-setup.md)

För ett live-program, status för den senaste distributionen med länkar för information och start av en ny distribution.

![Call-to-action](assets/info-banner.png)

### Miljökort {#environments}

The **Miljö** kort ger dig en översikt över dina miljöer samt länkar för snabba åtgärder.

The **Miljö** endast tre miljöer. Klicka **Visa alla** för att se alla miljöer i programmet.

Se dokumentet [Hantera miljöer](/help/using/managing-environments.md) för mer information om hur du hanterar dina miljöer.

### Förloppskort {#pipelines}

The **Pipelines** kort ger dig en översikt över dina rörledningar och länkar för snabba åtgärder.

The **Pipelines** På kortet finns endast tre rörledningar. Klicka **Visa alla** för att se alla rörledningar i programmet.

Se dokumentet [Hantera pipelines](/help/using/managing-pipelines.md) om du vill ha mer information om hur du hanterar dina rörledningar.

### Användbara resurser {#useful-resources}

The **Användbara resurser** finns länkar till ytterligare utbildningsresurser för Cloud Manager.
