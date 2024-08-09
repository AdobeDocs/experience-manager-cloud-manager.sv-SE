---
title: Navigera i användargränssnittet i Cloud Manager
description: Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.
exl-id: 9c1545ce-1c6d-417f-a6f4-fe53caef3433
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---


# Navigera i gränssnittet för molnhanteraren {#navigation}

Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.

Användargränssnittet för molnhantering består huvudsakligen av två grafiska gränssnitt:

* [Konsolen Mina program](#my-programs-console) där du kan visa och hantera alla program.
* [Fönstret Programöversikt](#program-overview) där du kan se information om och hantera ett enskilt program.

## My Programs Console {#my-programs-console}

När du loggar in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och väljer lämplig organisation, kommer du till konsolen **Mina program**.

![Konsolen Mina program](assets/my-programs-console.png)

Konsolen Mina program ger en översikt över alla program som du har tillgång till i den valda organisationen. Den består av flera delar.

1. [Verktygsfält](#toolbars-my-programs-toolbars) för organisationsval, aviseringar och kontoinställningar
1. Flikar som gör att du kan växla den aktuella vyn av dina program.
   * Vyn **Hem** (standard) som väljer vyn **Mina program** med en översikt över alla program
   * **Licens** som har åtkomst till License Dashboard. Kontrollpanelen för licenser gäller endast AEM as a Cloud Service-program, inte AMS-program.
      * Information om vilken typ av tjänst ditt program har (AMS eller AEMaaCS) finns i avsnittet [Programkort](#program-cards) i det här dokumentet.
   * Observera att flikarna som standard är stängda och att de kan visas med hjälp av hamburgermenyn i [Cloud Manager-huvudet](#cloud-manager-header).
1. [Call-to-Actions och Statistics](#cta-statistics) för en översikt över din senaste aktivitet
1. [**Mina program** avsnitt](#my-programs-section) med en översikt över alla dina program
1. [Snabblänkar](#quick-links) för enkel åtkomst till relaterade resurser

>[!TIP]
>
>Mer information om program finns i [Program och programtyper](/help/getting-started/program-setup.md).

### Verktygsfält {#my-programs-toolbars}

Det finns två verktygsfält ovanpå varandra.

#### Cloud Manager Header {#cloud-manager-header}

Det första är Cloud Manager-rubriken som är beständig när du navigerar i Cloud Manager. Det är en ankarpunkt som ger dig tillgång till inställningar och information som gäller för alla Cloud Manager-program.

![Experience Cloud-huvudet](assets/experience-cloud-header.png)

1. Hamburger-menyn som ger åtkomst till flikar som kan ta dig till specifika delar av ett enskilt program eller växla mellan License Dashboard och **[My Programs](#my-programs-console)** -konsolen beroende på sammanhanget.
   * Kontrollpanelen för licenser gäller endast AEM as a Cloud Service-program, inte AMS-program.
   * Information om vilken typ av tjänst ditt program har (AMS eller AEMaaCS) finns i avsnittet [Programkort](#program-cards) i det här dokumentet.
1. Med Cloud Manager-knappen kommer du tillbaka till My Programs-konsolen i Cloud Manager oavsett var du befinner dig i Cloud Manager.
1. Klicka på knappen Feedback för att ge Adobe feedback om Cloud Manager.
1. Organisationsväljaren visar den organisation du är inloggad på (i det här exemplet Foundation Internal). Klicka för att växla till en annan organisation om din Adobe ID är kopplad till flera.
1. Genom att klicka på lösningens väljare kan du snabbt gå över till andra Experience Cloud-lösningar.
1. Hjälpikonen ger snabb åtkomst till utbildningsresurser och supportresurser.
1. Aviseringsikonen är märkt med antalet för närvarande tilldelade ofullständiga [meddelanden](/help/using/notifications.md)
1. Välj den ikon som representerar användaren för att få åtkomst till dina användarinställningar. Om du inte har konfigurerat någon användarbild tilldelas ikonen slumpmässigt.

#### Verktygsfältet Program {#program-toolbar}

Verktygsfältet Program innehåller länkar för att växla mellan Cloud Manager-program och åtgärder som passar just det sammanhanget.

![Verktygsfältet Program](assets/program-toolbar.png)

1. Programväljaren öppnas i en listruta där du snabbt kan välja andra program eller vidta sammanhangsberoende åtgärder som att skapa ett nytt program
1. Länken Komma igång ger dig tillgång till [dokumentationsresan för introduktion](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/overview) så att du kan komma igång med Cloud Manager.
   * Observera att introduktionsresan är utformad för AEM as a Cloud Service och inte för Cloud Service för AMS, men många koncept är desamma.
1. Åtgärdsknappen innehåller sammanhangsberoende åtgärder som att skapa ett nytt program.

### Samtal-till-åtgärder och statistik {#cta-statistics}

Avsnittet om uppmaning till handling och statistik innehåller aggregerade data för din organisation, t.ex. om du har konfigurerat dina program, kan statistik över dina aktiviteter under de senaste 90 dagarna visa, inklusive:

* Antal [distributioner](/help/using/code-deployment.md)
* Antal [kodkvalitetsproblem](/help/using/code-quality-testing.md) som identifierats
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Avsnittet Mina program {#my-programs-section}

Huvudinnehållet i My Programs-konsolen är avsnittet **Mina program** som listar dina program som enskilda kort. Klicka på ett kort för att komma åt sidan **Programöversikt** för mer information om programmet.

>[!NOTE]
>
>Beroende på vilka behörigheter du har kanske du inte kan välja vissa program.

Använd sorteringsalternativen för att bättre hitta det program du behöver.

![Sorteringsalternativ](assets/my-programs-sorting.png)

* Sortera efter
   * Skapad den (standard)
   * Programnamn
   * Status
* Stigande (standard) / Fallande
* Stödrastervisning (standard)
* Listvy

#### Programkort {#program-cards}

Varje program representeras av ett kort (eller en rad i en tabell) som ger en översikt över programmet och snabblänkar för att vidta åtgärder.

![Programkort](assets/program-card.png)

* Programavbildning (om den är konfigurerad)
* Programnamn
* Tjänsttyp:
   * **Experience Manager** för AMS-program
   * **Experience Manager Cloud** för [AEM as a Cloud Service-program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/home)
* Status
* Konfigurerade lösningar
* Skapad den

Informationsikonen ger dig även snabb åtkomst till ytterligare information om programmet (användbart i listvyn).

![Information](assets/information-view.png)

Ellipsikonen ger dig tillgång till ytterligare åtgärder som du kan vidta i programmet.

![Ellipsknappen för program](assets/program-ellipsis.png)

* Navigera till en viss [miljö](/help/using/managing-environments.md) i programmet
* Öppna [programöversikt](#program-overview)
* [Redigera programmet](/help/getting-started/program-setup.md)
* Visa övervakning

### Snabblänkar {#quick-links}

I avsnittet med snabblänkar får du tillgång till resurser som du använder ofta.

## Programöversiktsfönster {#program-overview}

När du har valt ett program i konsolen [**Mina program**](#my-programs-console) visas programöversikten.

![Programöversikt](assets/program-overview.png)

Programöversikten ger dig tillgång till alla detaljer i ett Cloud Manager-program. Precis som My Programs-konsolen består den av flera delar.

1. [Verktygsfält](#program-overview-toolbar) om du snabbt vill gå tillbaka till konsolen Mina program och navigera i programmet
1. [Tabbar](#program-tabs) för att växla mellan olika aspekter av programmet
1. En [uppmaning till åtgärd](#cta) baserad på de senaste åtgärderna i programmet
1. En [översikt över programmets miljöer](#environments)
1. En [översikt över programmets pipelines](#pipelines)
1. Länkar till [användbara resurser](#useful-resources)

### Verktygsfält {#program-overview-toolbar}

Verktygsfälten för programöversikten liknar de i [Min programkonsol](#my-programs-toolbars). Här illustreras bara skillnaderna.

#### Cloud Manager Header {#cloud-manager-header-2}

Cloud Manager header har en hamburger-meny som automatiskt öppnas och visar de navigerbara flikarna i programöversikten.

![Cloud Manager hamburger-meny](assets/cloud-manager-hamburger.png)

Klicka på menyikonen för hamburgaren för att dölja flikarna.

#### Verktygsfältet Program {#program-toolbar-2}

Verktygsfältet för program ger dig fortfarande möjlighet att snabbt växla till andra program, men ger även tillgång till sammanhangsberoende åtgärder som att lägga till och redigera programmet.

![Verktygsfältet Program](assets/cloud-manager-program-toolbar.png)

Verktygsfältet innehåller dessutom alltid den flik som du är på om du har valt att dölja flikarna med hjälp av hamburgmenyn.

### Programflikar {#program-tabs}

Varje program har många alternativ och data kopplade till sig. Dessa data samlas in på flikar för att underlätta navigeringen i programmet. Flikarna ger dig tillgång till:

* Översikt - Programöversikt enligt beskrivningen i det aktuella dokumentet
* [Aktivitet](/help/using/managing-pipelines.md#activity) - Historiken för programmets pipeline-körningar
* [Pipelines](/help/using/managing-pipelines.md#pipelines) - Alla pipelines har konfigurerats för programmet
* [Databaser](/help/managing-code/managing-repositories.md) - Alla databaser har konfigurerats för programmet
* [Rapporter](/help/using/monitoring-environments.md#system-monitoring-overview) - Mätvärden som SLA-data
* [Miljö](/help/using/managing-environments.md) - Alla miljöer konfigurerade för programmet
* [Innehållsuppsättningar](/help/using/content-copy.md) - Innehållsuppsättningar som skapats för kopieringsändamål
* [Kopiera innehållsaktivitet](/help/using/content-copy.md) - aktiviteter för innehållskopiering
* Utbildningsvägar - ytterligare utbildningsresurser om Cloud Manager

Som standard visas fliken **Översikt** när du öppnar ett program. Den aktuella fliken markeras. Välj en annan flik om du vill visa information om den.

Använd hamburger-menyn i [Cloud Manager-huvudet](#cloud-manager-header-2) för att dölja flikarna.

### Call-to-Action {#cta}

I avsnittet om uppmaning att ringa in får du användbar information beroende på programmets status. För ett nytt program kan du se nästa steg som erbjuds och en påminnelse om ett publiceringsdatum, [som anges när programmet skapas](/help/getting-started/program-setup.md).

För ett live-program, status för den senaste distributionen med länkar för information och start av en ny distribution.

![Call-to-action](assets/info-banner.png)

### Miljökort {#environments}

Kortet **Environment** ger dig en översikt över dina miljöer och länkar för snabba åtgärder.

Kortet **Environment** innehåller endast tre miljöer. Klicka på **Visa alla** om du vill visa alla miljöer i programmet.

Mer information om hur du hanterar miljöer finns i [Hantera miljöer](/help/using/managing-environments.md).

### Förloppskort {#pipelines}

Kortet **Pipelines** ger dig en översikt över dina pipelines och länkar för snabba åtgärder.

Kortet **Pipelines** innehåller endast tre pipelines. Klicka på **Visa alla** om du vill visa alla rörledningar för programmet.

Mer information om hur du hanterar dina pipelines finns i [Hantera pipelines](/help/using/managing-pipelines.md).

### Användbara resurser {#useful-resources}

Avsnittet **Användbara resurser** innehåller länkar till ytterligare utbildningsresurser för Cloud Manager.
