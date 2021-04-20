---
title: Rollbaserade behörigheter
description: Följ den här sidan om du vill veta mer om rollbaserade behörigheter.
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: User Roles
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 15%

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.

## Användarroller {#user-roles}

Rollhantering för [!UICONTROL Cloud Manager] görs i [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html). Alla användare av [!UICONTROL Cloud Manager] måste vara medlemmar i kundens IMS-organisation och ha Adobe Managed Services Product Context. Specifika rollmedlemskap erbjuds genom att användaren läggs till i en [!UICONTROL Cloud Manager]-produktprofil i Admin Console.

Mer information om hur du konfigurerar dina roller finns i [Konfigurera användare och roller](setting-up-users-and-roles.md).

I följande tabelllista definieras vilka roller du kan tilldela i Admin Console.

| **[!UICONTROL Cloud Manager]Roll** | **Beskrivning** |
|---|---|
| Business Owner | Primär användare som slutför den inledande [!UICONTROL Cloud Manager]-installationen. Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Program Manager | Använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status och visa KPI:er. Kan godkänna viktiga 3-nivåfel. |
| Deployment Manager | Hanterar distributionsåtgärderna. Använder [!UICONTROL Cloud Manager] för att köra scen- och produktionsdistributioner. Kan godkänna viktiga 3-nivåfel. Har åtkomst till Git-databasen. |
| Developer | Utvecklar och testar anpassad programkod. I används främst [!UICONTROL Cloud Manager] för att visa status. Har implementerat åtkomst till Git-databasen. |
| Customer Success Engineer | Stöder vanligtvis kundframgångar för AMS-kunder. Interagerar med [!UICONTROL Cloud Manager] för att köra distributioner som kräver CSE-övervakning (Customer Success Engineer). |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Den här användaren kan använda [!UICONTROL Cloud Manager]-programväxlaren (efter att ha navigerat från [!UICONTROL Experience Cloud]) för att få åtkomst till Adobe Experience Manager (AEM). |

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll. Den här tabellen visar vilka funktioner som är tillgängliga och vilka roller som kan utföra funktionen.

Mer information om hur du konfigurerar användare finns i [Konfigurera användare och roller](setting-up-users-and-roles.md).

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare | ÄRENDE |
|--- |--- |--- |--- |--- |--- |--- |
| Läsprogram | Läs Program-KPI:er. | x | x | x | x | x |
| Skriv program | Programinstallation eller redigering. | x |  |  |  |  |
| Lägg till program | Lägg till nytt program. | x |  |  |  |  |
| Läs miljö | Se Miljöinformation. | x | x | x | x | x |
| Skapa körning | Starta pipeline. | x | x | x |  |  |
| Läskörning | Se körningsstatus. | x | x | x | x | x |
| Återuppta körning | Kan återuppta körning när den är pausad. | x | x | x |  | x |
| Kör Godkänn distribution till produktion | Godkänn GoLive. | x | x | x |  |  |
| Distribuera körningsschema till produktion | Schemalägg produktionsdistribution. | x | x | x |  | x |
| Körningsdistribution till produktion | Distribuera programmet till produktionen när det pausas för CSE Oversight. |  |  |  |  | x |
| Avbryt körning | Avbryt aktuell körning. |  |  | x |  |  |
| Fel vid kvalitetshastighet för körning | Godkänn viktiga fel i Quality Gate. | x | x | x |  |  |
| Skapa pipeline | Konfigurera/redigera pipeline. |  | x |  |  |  |
| Pipeline-läsning | Se Information om pipeline. | x | x | x | x | x |
| Pipeline Write | Konfigurera/redigera pipeline. |  | x |  |  |  |
| Ändra godkännande av pipeline | Tillåter redigering av alternativet Affärsägare. |  | x |  |  |  |
| Ändra hanterad distribution i pipeline | Tillåter redigering av alternativet CSE Oversight. |  | x |  |  |  |
| Ta bort pipeline | Tillåter borttagning av en pipeline. |  | x |  |  |  |
| Läs steg | Se resultaten av mätvärdena för stegkvalitet. | x | x | x | x | x |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |  |

