---
title: Rollbaserade behörigheter
description: Lär dig mer om Cloud Managers förkonfigurerade rollbaserade behörigheter för att hantera åtkomst till dina molnresurser.
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 522e5fbc650a8159602eb1aeaf42d64f4e23e8b4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 14%

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till Git-databasen. En företagsägare har olika behörigheter för att definiera nyckeltal (KPI) och godkänna distributioner.

## Användarroller {#user-roles}

Rollhantering för [!UICONTROL Cloud Manager] är klar med [Admin Console.](https://helpx.adobe.com/enterprise/using/admin-console.html) Alla användare av [!UICONTROL Cloud Manager] måste vara medlem i kundens IMS-organisation och ha Adobe Managed Services Product Context. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager] produktprofil i Admin Console.

Mer information om hur du konfigurerar dina roller finns i dokumentet [Konfigurera användare och roller.](/help/requirements/users-and-roles.md)

I den här tabellen visas de roller du kan tilldela i Admin Console.

| [!UICONTROL Cloud Manager] Roll | Beskrivning |
|---|---|
| Business Owner | Detta är den primära användaren som slutför den inledande [!UICONTROL Cloud Manager] installation och ansvarar för att definiera nyckeltal, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel vid behov. |
| Program Manager | Den här användaren använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och godkänna viktiga 3-nivåfel vid behov. |
| Deployment Manager | Den här användaren hanterar distributionsåtgärderna med [!UICONTROL Cloud Manager] för att utföra fas- och produktionsdistributioner, kan godkänna viktiga 3-nivåfel vid behov och har tillgång till Git-databasen. |
| Developer | Den här användaren utvecklar och testar anpassad programkod, som huvudsakligen använder [!UICONTROL Cloud Manager] för att visa distributionsstatus och har åtkomst till Git-databasen. |
| Customer Success Engineer | Den här användaren stöder i allmänhet kundframgångar för AMS-kunder och interagerar med [!UICONTROL Cloud Manager] för att kunna genomföra distributioner som kräver tillsyn av kundframgångsingenjör (CSE). |
| Innehållsförfattare | Användaren interagerar vanligtvis inte med [!UICONTROL Cloud Manager], men kan använda [!UICONTROL Cloud Manager] programväxlare (efter att ha navigerat från [!UICONTROL Experience Cloud]) för att få tillgång till Adobe Experience Manager (AEM). |

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har särskilda associerade förkonfigurerade behörigheter. Den här tabellen visar vilka behörigheter som är tillgängliga och vilka roller som kan utföra dem.


| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare | ÄRENDE |
|--- |--- |--- |--- |--- |--- |--- |
| Läsprogram | Läs programmets KPI:er | x | x | x | x | x |
| Skriv program | Programinstallation eller redigering | x |  |  |  |  |
| Lägg till program | Lägg till nytt program | x |  |  |  |  |
| Läs miljö | Se miljöinformation | x | x | x | x | x |
| Skapa körning | Starta pipeline | x | x | x |  |  |
| Läskörning | Se körningsstatus | x | x | x | x | x |
| Återuppta körning | Kan återuppta körning när den pausats | x | x | x |  | x |
| Kör Godkänn distribution till produktion | Godkänn direkt | x | x | x |  |  |
| Distribuera körningsschema till produktion | Schemalägg produktionsdistribution | x | x | x |  | x |
| Körningsdistribution till produktion | Distribuera program till produktion när de pausas för CSE-övervakning |  |  |  |  | x |
| Avbryt körning | Avbryt aktuell körning |  |  | x |  |  |
| Fel vid kvalitetshastighet för körning | Godkänn viktiga fel i kvalitetsgaten | x | x | x |  |  |
| Skapa pipeline | Ställ in/redigera pipeline |  | x |  |  |  |
| Pipeline-läsning | Se pipeline-information | x | x | x | x | x |
| Pipeline Write | Ställ in/redigera pipeline. |  | x |  |  |  |
| Ändra godkännande av pipeline | Tillåter redigering av alternativet Affärsägare |  | x |  |  |  |
| Ändra hanterad distribution i pipeline | Tillåter redigering av CSE-tillsynsalternativet |  | x |  |  |  |
| Ta bort pipeline | Tillåter att pipeline tas bort |  | x |  |  |  |
| Läs steg | Se resultaten av mätvärdena för stegkvalitet | x | x | x | x | x |
| Generera token för personlig åtkomst | Åtkomstgit |  | x |  | x |  |

Mer information om hur du konfigurerar användarna finns i dokumentet [Konfigurera användare och roller.](/help/requirements/users-and-roles.md)