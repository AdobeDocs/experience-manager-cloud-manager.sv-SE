---
title: Anpassade behörigheter
description: Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.
exl-id: a81eda9f-aa89-40ea-8e4c-52367a0a6aba
source-git-commit: 4a784f1594be4831be1c1c4aecb41b4f1b3b8be2
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Anpassade behörigheter {#custom-permissions}

Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.

## Introduktion {#introduction}

Cloud Manager har en uppsättning fördefinierade roller som styr åtkomsten till olika funktioner i molnhanteraren:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Med anpassade behörigheter kan användare skapa nya anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst för molnhanterare till program, rörledningar och miljöer.

>[!TIP]
>
>Mer information om fördefinierade roller finns i dokumentet [Rollbaserade behörigheter.](/help/requirements/role-based-permissions.md)

## Använda anpassade behörigheter {#using}

För att skapa och använda egna behörigheter krävs tre steg:

1. [Skapa en ny produktprofil.](#create)
1. [Tilldela anpassade behörigheter till den nya produktprofilen.](#assign-permissions)
1. [Tilldela användare till den nya produktprofilen.](#assign-users)

I det här avsnittet beskrivs de här stegen. Det kan vara praktiskt att referera till avsnitten [Villkor](#terms) och [Konfigurerbara behörigheter](#configurable-permissions) när du skapar egna anpassade behörigheter.

>[!NOTE]
>
>Du måste ha produktadministratörsbehörighet i Admin Console för att kunna skapa nya profiler och hantera behörigheter för Cloud Manager.

### Skapa en ny produktprofil {#create}

Du måste först skapa en ny produktprofil innan du kan tilldela anpassade behörigheter.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. Välj produkten **AEM Managed Services**.

1. Sök efter en instans med ett namn som matchar mönstret `*-cloud-manager` och tryck eller klicka för att hantera användare och behörigheter.

1. Du omdirigeras till fliken **Produkter** på Admin Console, där du kan hantera användare och behörigheter för molnhanteraren. Tryck eller klicka på knappen **Ny profil** på Admin Console.

![Knappen Ny profil](/help/assets/admin-console-new-profile.png)

1. Ange allmän information om profilen.

   * **Produktprofilnamn** - Ett beskrivande namn för profilen
   * **Visningsnamn** - Ett förkortat namn som visas i gränssnittet (alternativ)
   * **Beskrivning** - En informativ beskrivning av profilen som förklarar dess syfte (valfritt)
   * **Meddela användare via e-post** - När du väljer det här alternativet meddelas användarna via e-post när de läggs till eller tas bort från profilen.

1. Tryck eller klicka på **Spara** när du är klar.

Den nya produktprofilen sparas och visas i listan över produktprofiler på Admin Console.

### Tilldela anpassade behörigheter till profil {#assign-permissions}

Nu när du har en ny produktprofil kan du tilldela den anpassade behörigheter.

1. I Admin Console trycker eller klickar du på namnet på den [nya produktprofilen som du nyss skapade.](#create)

1. I det fönster som öppnas väljer du fliken **Behörigheter** för att visa en lista med redigerbara behörigheter.

   ![Redigerbara behörigheter](/help/assets/permissions-tab.png)

1. Tryck eller klicka på länken **Redigera** för en behörighet för att redigera den.

1. Fönstret **Redigera behörigheter** öppnas.
   * Den behörighet du valde i föregående steg är markerad i den vänstra kolumnen.
   * Behörighetsobjekten som är tillgängliga för tilldelning för behörigheten finns i den mellersta kolumnen med namnet **Tillgänglig behörighet**.
   * De tilldelade behörighetsobjekten finns i den högra kolumnen med etiketten **Inkluderade behörighetsobjekt**.

   ![Redigera behörighetsobjekt](/help/assets/edit-permission-items.png)

1. Tryck eller klicka på plusikonen (`+`) bredvid behörighetsobjektet för att lägga till det i kolumnen **Inkluderade behörighetsobjekt**.

   * Tryck eller klicka på ikonen `i` bredvid ett behörighetsobjekt om du vill veta mer om det.

1. Tryck eller klicka på knappen **Lägg till alla** längst upp i kolumnen **Tillgängliga behörigheter** för att lägga till alla behörigheter. Tryck eller klicka på **Ta bort alla** om du vill ta bort alla behörigheter som du tidigare valt.

1. Tryck eller klicka på **Spara** när du är klar med att definiera behörighetsobjekten för den nya produktprofilen.

Din nya produktprofil sparas nu med anpassade behörigheter.

### Tilldela användare till anpassade behörigheter {#assign-users}

Nu kan du tilldela användare till den nya produktprofilen som du skapade med anpassade behörigheter.

1. Tryck eller klicka på namnet på den [nya produktprofilen som du just har tilldelat anpassade behörigheter till i Admin Console.](#assign-permissions)

1. I det fönster som öppnas väljer du fliken **Användare**.

1. Tryck eller klicka på knappen **Lägg till användare** och tilldela användare till den nya produktprofilen med anpassade behörigheter.

Mer information om hur du använder Admin Console finns i avsnittet **Lägg till användare och användargrupper i en produktprofil** i dokumentet [Hantera produktprofiler för företagsanvändare](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## Konfigurerbara behörigheter {#configurable-permissions}

Följande behörigheter är tillgängliga för att skapa anpassade profiler.

| Behörighet | Beskrivning |
|---|---|
| Programåtkomst | Ge användarna åtkomst till program |
| Programredigering | Tillåt användare att redigera program |
| Skapa pipeline | Tillåt användare att skapa nya rörledningar |
| Ta bort pipeline | Tillåt användare att ta bort rörledningar |
| Redigera pipeline | Tillåt användare att redigera rörledningar |
| Godkänn/avvisa produktionsdistributioner | Tillåt användare att godkänna eller avvisa ett produktionsdistributionssteg |
| Avbryt körning av pipeline | Tillåt användare att avbryta pipeline-körningar |
| Körningsstart för pipeline | Tillåt användare att starta nya pipeline-körningar |
| Åsidosätt/avvisa viktiga måttfel | Tillåt användare att åsidosätta/ignorera viktiga mätfel |
| Produktionsdistributionsschema | Tillåt användare att schemalägga ett produktionsdistributionssteg |
| Datainformationsåtkomst | Tillåt användare att komma åt databasinformation och generera lösenord för åtkomst |
| Skapa databas | Tillåt användare att skapa nya Git-databaser |
| Radera databas | Tillåt användare att ta bort Git-databaser |
| Databasredigering | Tillåt användare att redigera Git-databaser |
| Generera databaskod | Tillåt användare att generera projekt från arkityp |
| Hantera innehållskopia | Tillåt användare att hantera kopieringsåtgärder för innehåll |

### Behörigheter på organisationsnivå {#organization-level}

Behörigheter på organisationsnivå avser behörigheter som alltid ges i alla program i en organisation.

Följande behörigheter är behörigheter på organisationsnivå:

* **Åtkomst till databasinformation** Med den här innehavar-/organisationsnivån kan användare generera användarnamn, lösenord och databas-URL för åtkomst och bidra till kundprojekt.
   * Användarnamn och lösenord för databasåtkomst är gemensamma för alla rapporter i organisationen, men databasens URL är unik för varje program.
   * Mer information finns i dokumentet [Source Code Repository](/help/requirements/source-code-repository.md).

## Villkor {#terms}

Följande termer används för att skapa och hantera anpassade behörigheter och fördefinierade roller.

| Term | Beskrivning |
|---|---|
| Fördefinierade behörigheter | Fördefinierade roller som **Business Owner**, **Deployment Manager** osv. för att styra olika funktioner i Cloud Manager. Mer information om fördefinierade roller finns i dokumentet [Rollbaserade behörigheter.](/help/requirements/role-based-permissions.md) |
| Anpassade behörigheter | Cloud Manager-funktioner som gör att användare kan skapa behörighetsprofiler för att definiera roller som styr funktioner som stöds i Cloud Manager |
| Behörighetsprofil | Skapat i Admin Console för att hantera konfigurerbara behörigheter som gäller för användare som ingår i behörighetsprofilen |
| Konfigurerbar behörighet | Cloud Manager-behörigheter som kan konfigureras i behörighetsprofilen |
| Behörighetsobjekt | Ett program, en miljö eller en pipeline-resurs som en behörighet kan tillämpas på |

Behörighetsobjekt avser det område där behörigheten ska tillämpas. Vanligtvis är det något av följande.

| Typ av behörighetsobjekt | Exempel | Beskrivning |
|---|---|---|
| Organisation | organisation:företagA | Alla tillämpliga resurser i en organisation. En resurs kan vara ett program, en miljö eller en pipeline. Om användaren lägger till en organisation för någon behörighet får även alla nya resurser i den organisationen den behörigheten. |
| Program | Program A | Alla tillämpliga resurser i ett program |
| Miljö | Program A: miljö | Tillämpligt på en viss miljö |
| Pipeline | Program A: Pipeline | Gäller för en viss rörledning |

## Begränsningar {#limitations}

Tänk på följande begränsningar när du använder anpassade behörigheter.

* En [begränsad uppsättning behörigheter är tillgängliga](#configurable-permissions) för att skapa anpassade profiler.
* Resurser som program, miljö, pipeline osv. som skapats i Cloud Manager kan ta upp till två minuter att visa i Admin Console för behörighetskonfiguration.
* I sällsynta fall där anpassade behörighetstjänster inte svarar är fördefinierade profiler fortfarande tillgängliga och användare i fördefinierade profiler fortfarande har lämplig åtkomst.

## Vanliga frågor {#faq}

### Vilka behörighetsprofiler är fördefinierade behörighetsprofiler?

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Mer information om fördefinierade roller finns i dokumentet [Rollbaserade behörigheter.](/help/requirements/role-based-permissions.md)

### Vad händer med fördefinierade behörighetsprofiler med introduktion till anpassade profiler?

Standardproduktprofiler och molnhanterarroller fungerar fortfarande på samma sätt som tidigare.

### Kan jag redigera fördefinierade behörighetsprofiler?

Nej, standardprofiler kan inte redigeras. Du kan inte lägga till eller ta bort behörigheter i standardbehörighetsprofilen. Du kan bara lägga till eller ta bort användare från fördefinierade profiler.

### Ska jag ta bort fördefinierade behörighetsprofiler eftersom anpassade profiler nu är tillgängliga?

Fördefinierade behörighetsprofiler får inte tas bort från Admin Console.

### Kan jag lägga till användare i flera behörighetsprofiler?

Ja, en användare kan ingå i flera profiler, inklusive fördefinierade och anpassade behörighetsprofiler. När en användare tilldelas till flera profiler blir de kombinerade behörigheterna från alla tilldelade behörighetsprofiler tillgängliga för den användaren.

### Vad händer om en användare har behörighet att redigera en miljö/pipeline men inte har åtkomst till ett program som innehåller miljön/pipeline?

I det här fallet kan användaren inte komma åt miljön eller pipelinen om de inte har behörighet för **programåtkomst** som innehåller miljön eller pipelinen.

### Vad händer om jag har både AEM as a Cloud Service- och AMS-program i samma IMS-organisation? Kan jag hantera behörigheter från en profil? {#ams-and-aemaacs}

Du bör skapa separata profiler för varje produkttyp (t.ex. en för AEM som Cloud Service och en för Adobe Managed Services eller AMS).
