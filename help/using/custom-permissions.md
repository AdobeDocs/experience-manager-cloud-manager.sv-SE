---
title: Anpassade behörigheter
description: Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.
exl-id: a81eda9f-aa89-40ea-8e4c-52367a0a6aba
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# Anpassade behörigheter {#custom-permissions}

Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.

## Introduktion {#introduction}

Cloud Manager har en uppsättning fördefinierade roller som styr åtkomsten till olika funktioner i Cloud Manager:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Med anpassade behörigheter kan användare skapa nya anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst för molnhanterare till program, rörledningar och miljöer.

>[!TIP]
>
>Mer information om fördefinierade roller finns i [Rollbaserade behörigheter](/help/requirements/role-based-permissions.md).

## Använd anpassade behörigheter {#using}

Om du vill skapa och använda dina egna anpassade behörigheter krävs följande tre steg:

1. [Skapa en ny produktprofil](#create).
1. [Tilldela anpassade behörigheter till den nya produktprofilen](#assign-permissions).
1. [Tilldela användare till den nya produktprofilen](#assign-users).

I det här avsnittet beskrivs dessa steg. Det kan vara praktiskt att se avsnitten [Villkor](#terms) och [Konfigurerbara behörigheter](#configurable-permissions) när du skapar egna anpassade behörigheter.

>[!NOTE]
>
>Du måste ha produktadministratörsbehörighet i Admin Console för att kunna skapa nya profiler och hantera behörigheter för Cloud Manager.

### Skapa en ny produktprofil {#create}

Skapa först en ny produktprofil som du kan tilldela anpassade behörigheter till.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. Välj produkten **AEM Managed Services**.

1. Sök efter en instans med ett namn som matchar mönstret `*-cloud-manager` och klicka för att hantera användare och behörigheter.

1. Du omdirigeras till fliken **Produkter** på Admin Console, där du kan hantera användare och behörigheter för Cloud Manager. Klicka på **Ny profil** i Admin Console.

![Knappen Ny profil](/help/assets/admin-console-new-profile.png)

1. Ange allmän information om profilen.

   * **Produktprofilnamn** - Ett beskrivande namn för profilen
   * **Visningsnamn** - Ett förkortat namn som visas i användargränssnittet (alternativ)
   * **Beskrivning** - En informativ beskrivning av profilen som förklarar dess syfte (valfritt)
   * **Meddela användare via e-post** - När det här alternativet har valts meddelas användarna via e-post när de läggs till eller tas bort från profilen.

1. Klicka på **Spara**.

Den nya produktprofilen sparas och visas i listan över produktprofiler på Admin Console.

### Tilldela anpassade behörigheter till den nya produktprofilen {#assign-permissions}

Nu när du har en ny produktprofil kan du tilldela den anpassade behörigheter.

1. Klicka på namnet på den [nya produktprofilen som du nyss skapade](#create) i Admin Console.

1. I det fönster som öppnas väljer du fliken **Behörigheter** för att visa en lista med redigerbara behörigheter.

   ![Redigerbara behörigheter](/help/assets/permissions-tab.png)

1. Klicka på länken **Redigera** om du vill redigera den.

1. Fönstret **Redigera behörigheter** öppnas.
   * Den behörighet du valde i föregående steg är markerad i den vänstra kolumnen.
   * Behörighetsobjekten som är tillgängliga för tilldelning för behörigheten finns i den mellersta kolumnen med namnet **Tillgänglig behörighet**.
   * De tilldelade behörighetsobjekten finns i den högra kolumnen med etiketten **Inkluderade behörighetsobjekt**.

   ![Redigera behörighetsobjekt](/help/assets/edit-permission-items.png)

1. Klicka på plusikonen (`+`) bredvid behörighetsobjektet för att lägga till det i kolumnen **Inkluderade behörighetsobjekt**. Om det behövs klickar du på ikonen `i` bredvid ett behörighetsobjekt för att lära dig mer om det.

1. Högst upp i kolumnen **Tillgängliga behörigheter** klickar du på **Lägg till alla** för att lägga till alla behörigheter. Klicka på **Ta bort alla** om du vill ta bort alla tidigare markerade behörigheter.

1. När du har definierat behörighetsobjekten för den nya produktprofilen klickar du på **Spara**.

Din nya produktprofil sparas nu med anpassade behörigheter.

### Tilldela användare till den nya produktprofilen {#assign-users}

Nu kan du tilldela användare till den nya produktprofilen som du skapade med anpassade behörigheter.

1. Klicka på namnet på den [nya produktprofilen som du just har tilldelat anpassade behörigheter till i Admin Console ](#assign-permissions).

1. I det fönster som öppnas väljer du fliken **Användare**.

1. Klicka på **Lägg till användare** och tilldela användare till din nya produktprofil med anpassade behörigheter.

Mer information om hur du använder Admin Console finns i **Lägga till användare och användargrupper i en produktprofil** i dokumentet [Hantera produktprofiler för företagsanvändare](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

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
| Datainformationsåtkomst | Ge användarna åtkomst till databasinformation och generera ett lösenord för åtkomst |
| Skapa databas | Tillåt användare att skapa nya Git-databaser |
| Radera databas | Tillåt användare att ta bort Git-databaser |
| Databasredigering | Tillåt användare att redigera Git-databaser |
| Generera databaskod | Tillåt användare att generera projekt från arkityp |
| Hantera innehållskopia | Tillåt användare att hantera kopieringsåtgärder för innehåll |

### Behörigheter på organisationsnivå {#organization-level}

Behörigheter på organisationsnivå används alltid i alla program i en organisation.

Ett exempel på en behörighet på organisationsnivå i Cloud Manager är **Åtkomst till databasinformation**. Med den här behörigheten kan användare generera ett användarnamn, ett lösenord och en databasadress för att komma åt och bidra till kundprojekt. Även om användarnamn och lösenord är konsekventa i alla databaser i organisationen har varje program en unik databas-URL.

Mer information finns i [Source-koddatabasen](/help/requirements/source-code-repository.md).

## Villkor {#terms}

Följande termer används för att skapa och hantera anpassade behörigheter och fördefinierade roller.

| Term | Beskrivning |
|---|---|
| Fördefinierade behörigheter | Fördefinierade roller som **Business Owner**, **Deployment Manager** och så vidare. för att styra olika funktioner i Cloud Manager. Mer information om fördefinierade roller finns i [Rollbaserade behörigheter](/help/requirements/role-based-permissions.md). |
| Anpassade behörigheter | Cloud Manager-funktioner som gör att användare kan skapa behörighetsprofiler för att definiera roller som styr funktioner som stöds i Cloud Manager |
| Behörighetsprofil | Skapat i Admin Console för att hantera konfigurerbara behörigheter som är tillämpliga för användare som är en del av behörighetsprofilen |
| Konfigurerbar behörighet | Cloud Manager-behörigheter kan konfigureras i behörighetsprofilen |
| Behörighetsobjekt | Ett program, en miljö eller en pipeline-resurs som en behörighet kan tillämpas på |

Behörighetsobjekt avser det område där behörigheter tillämpas. Vanligtvis är det något av följande.

| Typ av behörighetsobjekt | Exempel | Beskrivning |
|---|---|---|
| Organisation | organisation:företagA | Alla tillämpliga resurser i en organisation. En resurs kan vara ett program, en miljö eller en pipeline. Om användaren lägger till en organisation för någon behörighet har alla nya resurser i den organisationen också den behörigheten. |
| Program | Program A | Alla tillämpliga resurser i ett program |
| Miljö | Program A: miljö | Gäller i en viss miljö |
| Pipeline | Program A: Pipeline | Gäller för en viss rörledning |

## Begränsningar {#limitations}

Tänk på följande begränsningar när du använder anpassade behörigheter:

* En [begränsad uppsättning behörigheter är tillgängliga](#configurable-permissions) för att skapa anpassade profiler.
* Resurser som program, miljö, pipeline osv. som skapats i Cloud Manager kan ta upp till två minuter att visa i Admin Console för behörighetskonfiguration.
* I sällsynta fall där en anpassad behörighetstjänst inte svarar är fördefinierade profiler fortfarande tillgängliga och användare i fördefinierade profiler fortfarande har lämplig åtkomst.

## Frågor och svar {#faq}

### Vilka behörighetsprofiler är fördefinierade behörighetsprofiler?

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Mer information om fördefinierade roller finns i [Rollbaserade behörigheter](/help/requirements/role-based-permissions.md).

### Vad händer med fördefinierade behörighetsprofiler med introduktion till anpassade profiler?

Standardproduktprofiler och Cloud Manager-roller fungerar fortfarande på samma sätt som tidigare.

### Kan jag redigera fördefinierade behörighetsprofiler?

Nej, standardprofiler kan inte redigeras. Du kan inte lägga till eller ta bort behörigheter i standardbehörighetsprofilen. Du kan bara lägga till eller ta bort användare från fördefinierade profiler.

### Ska jag ta bort fördefinierade behörighetsprofiler eftersom anpassade profiler nu är tillgängliga?

Fördefinierade behörighetsprofiler får inte tas bort från Admin Console.

### Kan jag lägga till användare i flera behörighetsprofiler?

Ja, en användare kan ingå i flera profiler, inklusive fördefinierade och anpassade behörighetsprofiler. När en användare tilldelas till flera profiler är de kombinerade behörigheterna från alla tilldelade behörighetsprofiler tillgängliga för den användaren.

### Vad händer om en användare har behörighet att redigera en miljö/pipeline men inte har åtkomst till ett program som innehåller miljön/pipelinen?

I det här scenariot kan användaren inte komma åt miljön eller pipelinen om de inte har behörighet för **programåtkomst** som innehåller miljön eller pipelinen.

### Vad händer om jag har både AEM as a Cloud Service- och AMS-program i samma IMS-organisation? Kan jag hantera behörigheter från en profil? {#ams-and-aemaacs}

Skapa en separat profil för varje produkttyp. Det vill säga en för AEM som Cloud Service och en för Adobe Managed Services eller AMS.
