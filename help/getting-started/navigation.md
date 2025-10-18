---
title: Navigera i användargränssnittet i Cloud Manager
description: Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.
exl-id: 9c1545ce-1c6d-417f-a6f4-fe53caef3433
source-git-commit: b98e1711f1f98f52977dd6cb4cd2bc834d81a360
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 0%

---


# Navigera i användargränssnittet i Cloud Manager {#navigation}

Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.

Cloud Manager gränssnitt består huvudsakligen av två grafiska gränssnitt:

* [På konsolen Mina program](#my-programs-console) kan du visa och hantera alla program.
* [I fönstret Programöversikt](#program-overview) kan du se information om och hantera ett enskilt program.

## My Programs console {#my-programs-console}

När du loggar in på Cloud Manager på [experience.adobe.com](https://experience.adobe.com/experiencemanager) och väljer lämplig organisation, kommer du till konsolen **Mina program**.

![Konsolen Mina program](/help/getting-started/assets/cloud-manager-my-programs-console.png)

Konsolen **Mina program** innehåller en översikt över alla program som du har åtkomst till i den valda organisationen. Den består av flera delar.

|   | Område | Beskrivning |
| --- | --- | --- |
| 1 | [Verktygsfält](#toolbars-my-programs-toolbars) | Använd för organisationsval, aviseringar och kontoinställningar. |
| 2 | Fliken för den vänstra panelen | På olika flikar kan du växla den aktuella vyn av dina program, inklusive följande:<br><ul><li>**Experience Manager** öppnar startsidan för dina olika AEM-lösningar</li><li>**Alla program** som visar alla tillgängliga program.</li><li>**Licens** öppnar kontrollpanelen för licenser. License Dashboard gäller endast *AEM as a Cloud Service-program* (AEMaaCS), inte Adobe Managed Services-program som AEM 6.5 och AEM 6.5 LTS. Information om vilken typ av tjänst ditt program har (AEMaaCS eller AMS) finns i avsnittet [Programkort](#program-cards) i den här artikeln. Flikarna stängs som standard och kan visas med menyikonen ![Visa, den nedrullningsbara meny](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) som finns till vänster om rubriken [Cloud Manager](#cloud-manager-header).</li></ol> |
| 3 | [Mina program](#my-programs-section) | Visar alla tillgängliga program som du kan välja.<br>Mer information om program finns i [Program och programtyper](/help/getting-started/program-setup.md). |
| 4 | [Anrop och statistik](#cta-statistics) | Ger en översikt över din senaste aktivitet. |
| 5 | [Snabblänkar](#quick-links) | Snabb åtkomst till relaterade resurser. |


### Verktygsfält {#my-programs-toolbars}

Det finns två verktygsfält ovanpå varandra.

#### Cloud Manager header {#cloud-manager-header}

Den första är Cloud Manager header. Sidhuvudet är beständigt när du navigerar i Cloud Manager. Det är en ankarpunkt som ger dig tillgång till inställningar och information som gäller för alla Cloud Manager-program.

![Experience Cloud-rubriken](/help/getting-started/assets/cloud-manager-header-toolbar.png)

| Område | Beskrivning |
| --- | --- |
| ![Visa menyikon, hamburger](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) | En nedrullningsbar meny som ger åtkomst till flikar för specifika delar av ett enskilt program.<br>Information om vilken typ av tjänst ditt program har (AMS eller AEMaaCS) finns i avsnittet [Programkort](#program-cards) i det här dokumentet. |
| ![Adobe röd och vit ikon](/help/getting-started/assets/AdobeLogoWhiteOnRed.svg) Cloud Manager | Klicka för att öppna konsolen **Mina program** för Cloud Manager, oavsett var du befinner dig i Cloud Manager. |
| *`Name of selected organization`* | Organisationsväljaren visar organisationen som du är inloggad på (i det här exemplet *Foundation Internal*). Klicka för att växla till en annan organisation om din Adobe ID är kopplad till flera organisationer. |
| ![Feedback-ikon](/help/getting-started/assets/AppComment.svg) Feedback | Klicka för att ge Adobe feedback om Cloud Manager. |
| ![AI Assistant-ikon](/help/getting-started/assets/AIChat.svg) | AI Assistant har ett gränssnitt för att effektivisera sökningen efter svar på dina AEM-relaterade frågor. Se [AI-assistenten](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/ai-in-aem/ai-assistant/ai-assistant-in-aem#) |
| ![Hjälpikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_HelpOutline_18_N.svg) | Klicka för att ge snabb åtkomst till utbildningsresurser och supportresurser. |
| ![Vit klockikon](/help/getting-started/assets/Bell.svg) | Klicka för att visa antalet för närvarande tilldelade ofullständiga [meddelanden](/help/using/notifications.md) |
| ![Appikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) | Klicka för att snabbt växla mellan AEM hemsida och AEM lösningar |
| *`Dynamic Account icon`* | Klicka på din användarbild för att komma åt dina **kontoinställningar** och **programinställningar**, eller för att logga ut.<br>Om du väljer att inte lägga till en användarbild tilldelas en ikon slumpmässigt (vilket visas i verktygsfältsbilden ovan). |

<!--
1. The ![Show menu icon, hamburger](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) icon on the left side of the header is  
   * The License Dashboard only applies to AEM as a Cloud Service programs, not AMS programs.
   * To determine the type of service your program has (AMS or AEMaaCS), see the [Program Cards section](#program-cards) of this document.
1. The **Adobe Cloud Manager** button takes you back to the **My Programs** console of Cloud Manager no matter where you are in Cloud Manager.
1. Click **Feedback** to provide feedback to Adobe about Cloud Manager.
1. The organization selector displays the organization that you are currently signed into (in this example, Foundation Internal). Click to switch to another organization if your Adobe ID is associated with multiple.
1. Clicking the solutions switcher lets you quickly jump to other Experience Cloud solutions.
1. The Help icon provides quick access to learning and support resources.
1. The notifications icon is badged with the number of currently assigned incomplete [notifications](/help/using/notifications.md)
1. Select the icon representing your user to access your user settings. If you do not select a user picture, an icon is randomly assigned. -->

#### Verktygsfältet Program {#program-toolbar}

Verktygsfältet Program innehåller länkar för att växla mellan Cloud Manager-program och åtgärder som passar just det sammanhanget.

![Cloud Manager-verktygsfält](/help/getting-started/assets/cloud-manager-programs-toolbar.png)

|   | Område | Beskrivning |
| --- | --- | --- |
| 1 | Mina program | Klicka för att öppna en nedrullningsbar lista där du kan välja att lägga till ett program, välja andra befintliga program eller gå tillbaka till Experience Manager hemsida. |
| 2 | ![Informationsikon](/help/getting-started/assets/Info.svg) Komma igång | Klicka för att komma åt [startdokumentationsresan](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/onboarding/journey/overview) så att du kommer igång med Cloud Manager.<br>Startresan är utformad för Cloud Manager på Adobe Experience Manager as a Cloud Service (AEMaaCS) och inte för Cloud Manager på Adobe Managed Services (AMS). Många koncept är dock desamma. |
| 3 | *`Dynamic action button`* | Åtgärdsknappen innehåller sammanhangsberoende åtgärder som du kan klicka på, till exempel **Lägg till program** (se exemplet ovan) eller lägga till en domän. |

### Samtal och statistik {#cta-statistics}

I avsnittet call-to-action och statistik finns sammanställda data för din organisation, till exempel om du har konfigurerat dina program, och statistik för dina aktiviteter under de senaste 90 dagarna kan visa följande:

* Antal [distributioner](/help/using/code-deployment.md)
* Antal [kodkvalitetsproblem](/help/using/code-quality-testing.md) som identifierats
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Mina program {#my-programs-section}

Huvudinnehållet i My Programs-konsolen är avsnittet **Mina program** som listar dina program som enskilda kort. Klicka på ett kort för att komma åt sidan **Programöversikt** för mer information om programmet.

Beroende på vilka behörigheter du har kanske du inte kan välja vissa program.

Du kan använda följande sorteringsalternativ för att snabbt hitta det program du vill ha:

![Sorteringsalternativ](/help/getting-started/assets/cloud-manager-my-programs-sorting.png)

* Sortera efter:
   * Skapad den
   * Programnamn
   * Status
* ![Sorteringsordning nedåt-ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg) / ![Sorteringsordning uppåt-ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg) Sortera program nedåt respektive uppåt.
* ![Ikon för klassisk stödrastervy](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg) / ![Ikon för punktlistor eller textlistor](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TextBulleted_18_N.svg) Visa program i stödrasterformulär eller listformat.

#### Programkort {#program-cards}

Ett kort eller en rad i en tabell representerar alla program och ger en översikt över programmet och snabblänkar för att vidta åtgärder.

![Programkort](/help/getting-started/assets/cloud-manager-program-card.png)

* Programavbildning (om den är konfigurerad)
* Programnamn (i ovanstående exempel: *WKND Magazine*)
* Tjänsttyp:
   * **Experience Manager** för AMS-program
   * **Experience Manager Cloud** för [AEM as a Cloud Service-program](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/home)
* Status (i exemplet ovan, *Ready*)
* Konfigurerade lösningar
* Skapad den

Klicka på ![informationsikonen](/help/getting-started/assets/Info.svg) för att få snabb åtkomst till ytterligare information om programmet (användbart i listvyn).

![Popup-fönstret Information i Cloud Manager AMS](/help/getting-started/assets/cloud-manager-information-view.png)

Klicka på ikonen ![Mer, ellips](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), så får du tillgång till fler åtgärder som du kan vidta i programmet.

![Ellipsknappen för program](/help/getting-started/assets/cloud-manager-program-ellipsis.png)

* Experience Manager Home
* Navigera till en viss [miljö](/help/using/managing-environments.md) i programmet
* Öppna [programöversikt](#program-overview)
* [Redigera programmet](/help/getting-started/program-setup.md)
* Visa övervakning

### Snabblänkar {#quick-links}

I avsnittet med snabblänkar får du tillgång till användbara, relaterade resurser.

## Fönstret Programöversikt {#program-overview}

Om du väljer ett program i konsolen [**Mina program**](#my-programs-console) kommer du till sidan **Programöversikt** .

![Programöversikt](/help/getting-started/assets/cloud-manager-program-overview.png)

**Programöversikt** ger dig tillgång till all information om ett Cloud Manager-program. Precis som **Mina program** består den av flera delar.

1. [Verktygsfält](#program-overview-toolbar) om du snabbt vill gå tillbaka till konsolen **Mina program** och navigera i programmet.
1. [Flikområdet](#program-tabs) om du vill växla mellan olika aspekter av programmet.
1. En [call-to-action](#cta) som baseras på de senaste åtgärderna i programmet.
1. Associerade [miljöer](#environments) i programmet.
1. Associerade [pipeline](#pipelines) för programmet.

### Verktygsfält {#program-overview-toolbar}

Verktygsfälten för programöversikten liknar verktygsfälten i [Min programkonsol](#my-programs-toolbars). Här illustreras bara skillnaderna.

#### Cloud Manager header {#cloud-manager-header-2}

Cloud Manager-rubriken har en ![Visa-menyikon, hamburger](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)-listruta som öppnas automatiskt för att visa de navigerbara flikarna i programöversikten.

Klicka på ![Visa menyikon, hamburger](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) för att dölja flikarna.

#### Verktygsfältet Program {#program-toolbar-2}

Verktygsfältet för program ger dig fortfarande möjlighet att snabbt växla till andra program, men ger dessutom tillgång till sammanhangsberoende åtgärder som att lägga till och redigera programmet.

![Verktygsfältet Program](assets/cloud-manager-program-toolbar.png)

Om du dessutom döljer flikarna med ![Visa menyikon, hamburger](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg), kan verktygsfältet fortfarande visa fliken som du för närvarande är på.

### Programflikar {#program-tabs}

Varje program har flera alternativ och data kopplade till sig. Dessa data samlas in på flikar för att underlätta navigeringen i programmet. Flikarna ger dig tillgång till:

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

Använd ![Visa menyikonen, hamburgaren](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i [Cloud Manager-huvudet](#cloud-manager-header-2) för att dölja flikarna.

### Call-to-action {#cta}

I call-to-action-avsnittet finns information som du kan använda beroende på programmets status. För ett nytt program kan du se nästa steg som erbjuds och en påminnelse om ett publiceringsdatum, [som anges när programmet skapas](/help/getting-started/program-setup.md).

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
