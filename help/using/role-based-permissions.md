---
title: Rollbaserade behörigheter
description: Följ den här sidan om du vill veta mer om rollbaserade behörigheter.
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
translation-type: tm+mt
source-git-commit: 157370b193c104915be063d1a4375f81839b88a2

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.

## Användarroller {#user-roles}

Rollhantering för [!UICONTROL Cloud Manager] görs i [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html). Alla användare av [!UICONTROL Cloud Manager] måste vara medlemmar i kundens IMS-organisation och ha Adobe Managed Services Product Context. Specifika rollmedlemskap erbjuds genom att användaren läggs till i en [!UICONTROL Cloud Manager] produktprofil på Admin Console.

Mer information om hur du konfigurerar dina roller finns i [Konfigurera användare och roller](setting-up-users-and-roles.md).

I följande tabelllista definieras de roller du kan tilldela i Admin Console.

| **[!UICONTROL Cloud Manager]Roll ** | **Beskrivning** |
|---|---|
| Företagsägare | Primär användare som slutför den första [!UICONTROL Cloud Manager] konfigurationen. Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Programhanteraren | Används [!UICONTROL Cloud Manager] för att konfigurera team, granska status och visa KPI:er. Kan godkänna viktiga 3-nivåfel. |
| Distributionshanteraren | Hanterar distributionsåtgärderna. Används [!UICONTROL Cloud Manager] för att köra scen- och produktionsdistributioner. Kan godkänna viktiga 3-nivåfel. Har åtkomst till Git-databasen. |
| Utvecklare | Utvecklar och testar anpassad programkod. Används främst [!UICONTROL Cloud Manager] för att visa status. Har implementerat åtkomst till Git-databasen. |
| Customer Success Engineer | Stöder vanligtvis kundframgångar för AMS-kunder. Interagerar med [!UICONTROL Cloud Manager] för att genomföra distributioner som kräver övervakning av Customer Success Engineer (CSE). |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Den här användaren kan använda [!UICONTROL Cloud Manager] Programväljaren (efter att ha navigerat från [!UICONTROL Experience Cloud]) för att få åtkomst till Adobe Experience Manager (AEM). |

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll. Den här tabellen visar vilka funktioner som är tillgängliga och vilka roller som kan utföra funktionen.

Mer information om hur du konfigurerar dina användare finns i [Konfigurera användare och roller](setting-up-users-and-roles.md).

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare | ÄRENDE |
|--- |--- |--- |--- |--- |--- |--- |
| Läsprogram | Läs Program-KPI:er. | x | x | x | x | x |
| Skriv program | Programinstallation eller redigering. | x |  |  |  |  |
| Lägg till program | Lägg till nytt program. | x |  |  |  |  |
| Läs miljö | Se Miljöinformation. | x | x | x | x | x |
| Skapa körning | Starta pipeline. | x | x | x |  |  |
| Läskörning | Se körningsstatus. | x | x | x | x | x |
| Återuppta körning | Kan återuppta körning när den är pausad. | x | x | x |  | x |
| Kör Godkänn distribution till produktion | Godkänn Adobe GoLive. | x | x | x |  |  |
| Distribuera körningsschema till produktion | Schemalägg produktionsdistribution. | x | x | x |  | x |
| Körningsdistribution till produktion | Distribuera programmet till produktionen när det pausas för CSE Oversight. |  |  |  |  | x |
| Avbryt körning | Avbryt aktuell körning. | x | x | x |  |  |
| Fel vid kvalitetshastighet för körning | Godkänn viktiga fel i Quality Gate. | x | x | x |  |  |
| Skapa pipeline | Konfigurera/redigera pipeline. |  | x |  |  |  |
| Pipeline-läsning | Se Information om pipeline. | x | x | x | x | x |
| Pipeline Write | Konfigurera/redigera pipeline. |  | x |  |  |  |
| Ändra godkännande av pipeline | Tillåter redigering av alternativet Affärsägare. |  | x |  |  |  |
| Ändra hanterad distribution i pipeline | Tillåter redigering av alternativet CSE Oversight. |  | x |  |  |  |
| Läs steg | Se resultaten av mätvärdena för stegkvalitet. | x | x | x | x | x |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |  |
