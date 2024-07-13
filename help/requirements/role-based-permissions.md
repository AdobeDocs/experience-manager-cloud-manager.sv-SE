---
title: Rollbaserade behörigheter
description: Lär dig mer om Cloud Manager förkonfigurerade rollbaserade behörigheter för att hantera åtkomst till dina molnresurser.
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: fc1bc626dc18d25ce8c5bbae71396b234b5676db
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 2%

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till Git-databasen. En företagsägare har olika behörigheter för att definiera nyckeltal (KPI) och godkänna distributioner.

>[!NOTE]
>
>I den här dokumentationen beskrivs rollbaserade behörigheter för Cloud Manager för Adobe Managed Services (AMS).
>
>Motsvarande dokumentation för AEM as a Cloud Service finns i dokumentet [Introduktion till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/concepts/cloud-manager-introduction.html#role-based-permissions) i dokumentationen för AEM as a Cloud Service.

## Användarroller {#user-roles}

Rollhantering för [!UICONTROL Cloud Manager] har slutförts med Admin Console [.](https://helpx.adobe.com/enterprise/using/admin-console.html) Alla användare av [!UICONTROL Cloud Manager] måste vara medlemmar i kundens IMS-organisation och ha produktkontexten Adobe Managed Services. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager]-produktprofil i Admin Console.

Mer information om hur du konfigurerar dina roller finns i dokumentet [Konfigurera användare och roller.](/help/requirements/users-and-roles.md)

I den här tabellen visas de roller du kan tilldela i Admin Console.

| Roll för [!UICONTROL Cloud Manager] | Beskrivning |
|---|---|
| Business Owner | Detta är den primära användaren som slutför den inledande [!UICONTROL Cloud Manager]-konfigurationen och ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov. |
| Program Manager | Den här användaren använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-skiktsfel vid behov. |
| Deployment Manager | Den här användaren hanterar distributionsåtgärderna med [!UICONTROL Cloud Manager] för att köra fas- och produktionsdistributioner, kan godkänna viktiga 3-skiktsfel vid behov och har åtkomst till Git-databasen. |
| Developer | Den här användaren utvecklar och testar anpassad programkod, använder i första hand [!UICONTROL Cloud Manager] för att visa distributionsstatus och har åtkomst till Git-databasen. |
| Customer Success Engineer | Den här användaren stöder vanligtvis kundframgångar för AMS-kunder och interagerar med [!UICONTROL Cloud Manager] i syfte att köra distributioner som kräver CSE-övervakning (Customer Success Engineer). |
| Innehållsförfattare | Den här användaren interagerar vanligtvis inte med Cloud Manager, men kan använda Cloud Manager programväljare (som har navigerat från Experience Cloud) för att få åtkomst till Adobe Experience Manager (AEM). |

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har särskilda associerade förkonfigurerade behörigheter. Den här tabellen visar vilka behörigheter som är tillgängliga och vilka roller som kan utföra dem.


| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer | ÄRENDE |
|--- |--- |--- |--- |--- |--- |--- |
| Läsprogram | Läs programmets KPI:er | x | x | x | x | x |
| Skriv program | Programinstallation eller redigering | x |  |  |  |  |
| Lägg till program | Lägg till nytt program | x |  |  |  |  |
| Läs miljö | Se miljöinformation | x | x | x | x | x |
| Skapa körning | Starta pipeline | x | x | x |  |  |
| Läskörning | Se körningsstatus | x | x | x | x | x |
| Återuppta körning | Kan återuppta körning när den pausats | x | x | x |  | x |
| Godkänn distribution av körning till produktion | Godkänn direkt | x | x | x |  |  |
| Distribuera körningsschema till produktion | Schemalägg produktionsdistribution | x | x | x |  | x |
| Körningsdistribution till produktion | Distribuera program till produktion när de pausas för CSE-övervakning |  |  |  |  | x |
| Avbryt körning | Avbryt aktuell körning |  |  | x |  |  |
| Fel vid kvalitetshastighet för körning | Godkänn viktiga fel i kvalitetsgrinden | x | x | x |  |  |
| Skapa pipeline | Ställ in/redigera pipeline |  | x |  |  |  |
| Pipeline-läsning | Se pipeline-information | x | x | x | x | x |
| Pipeline Write | Ställ in/redigera pipeline. |  | x |  |  |  |
| Ändra godkännande av pipeline | Tillåter redigering av alternativet Affärsägare |  | x |  |  |  |
| Ändra hanterad distribution i pipeline | Tillåter redigering av CSE-tillsynsalternativet |  | x |  |  |  |
| Ta bort pipeline | Tillåter att pipeline tas bort |  | x |  |  |  |
| Läs steg | Se resultaten av mätvärdena för stegkvalitet | x | x | x | x | x |
| Generera token för personlig åtkomst | Åtkomstgit |  | x |  | x |  |

Mer information om hur du konfigurerar användarna finns i dokumentet [Konfigurera användare och roller.](/help/requirements/users-and-roles.md)

>[!TIP]
>
>Anpassade behörighetsprofiler med konfigurerbara behörigheter är också tillgängliga. Mer information finns i dokumentet [Anpassade behörigheter](/help/using/custom-permissions.md).
