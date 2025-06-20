---
title: Rollbaserade behörigheter
description: Lär dig mer om Cloud Manager förkonfigurerade rollbaserade behörigheter för att hantera åtkomst till dina molnresurser.
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 3%

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till Git-databasen. En företagsägare har olika behörigheter för att definiera nyckeltal (KPI) och godkänna distributioner.

>[!NOTE]
>
>I den här dokumentationen beskrivs rollbaserade behörigheter för Cloud Manager för Adobe Managed Services (AMS).
>
>Motsvarande dokumentation för AEM as a Cloud Service finns i dokumentet [Introduktion till Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/cloud-manager-introduction#role-based-permissions) i dokumentationen för AEM as a Cloud Service.

## Användarroller {#user-roles}

Rollhantering för [!UICONTROL Cloud Manager] har slutförts med [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html). Alla användare av [!UICONTROL Cloud Manager] måste vara medlemmar i kundens IMS-organisation och ha produktkontexten för Adobe Managed Services. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager]-produktprofil i Admin Console.

Mer information om hur du konfigurerar dina roller finns i [Konfigurera användare och roller](/help/requirements/users-and-roles.md).

I följande tabell visas de roller du kan tilldela i Admin Console.

| Rollen [!UICONTROL Cloud Manager] | Beskrivning |
|---|---|
| Business Owner | Den primära användaren som slutför den första [!UICONTROL Cloud Manager]-konfigurationen och ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov. |
| Innehållsförfattare | Användaren interagerar vanligtvis inte med Cloud Manager, men kan använda Cloud Manager programväljare (när du har navigerat från Experience Cloud) för att få åtkomst till Adobe Experience Manager (AEM). |
| Customer Success Engineer | Användaren stöder främst AMS-kundens framgång och engagerar med [!UICONTROL Cloud Manager] för att köra distributioner. Dessa driftsättningar kräver övervakning av en Adobe Customer Success Engineer (CSE). |
| Deployment Manager | Användaren hanterar distributionsåtgärderna med [!UICONTROL Cloud Manager] för att köra fas- och produktionsdistributioner, kan godkänna viktiga 3-nivåfel vid behov och har tillgång till Git-databasen. |
| Developer | Användaren utvecklar och testar anpassad programkod, använder främst [!UICONTROL Cloud Manager] för att visa distributionsstatus och har åtkomst till Git-databasen. |
| Program Manager | Användaren använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-nivåfel vid behov. |

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika, associerade förkonfigurerade behörigheter. Följande tabell visar vilka behörigheter som är tillgängliga och vilka roller som kan utföra dem.

| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer | ÄRENDE |
| --- | --- | --- | --- | --- | --- | --- |
| `Read the Application` | Läs programmets KPI:er | x | x | x | x | x |
| `Write Application` | Konfigurera eller redigera program | x | | | | |
| `Add Program` | Lägg till nytt program | x |  |  |  |  |
| `Read Environment` | Se miljöinformation | x | x | x | x | x |
| `Create Execution` | Starta pipeline | x | x | x | | |
| `Read Execution` | Se körningsstatus | x | x | x | x | x |
| `Resume Execution` | Möjlighet att återuppta körningen när den pausats | x | x | x | | x |
| `Execution Approve Deploy to Production` | Godkänn direkt | x | x | x | | |
| `Execution Schedule Deploy to Production` | Schemalägg produktionsdistribution | x | x | x | | x |
| `Execution Deploy to Production` | Distribuera program till produktion när de pausas för CSE-övervakning |  |  |  |  | x |
| `Execution Cancel` | Avbryt aktuell körning |  |  | x |  |  |
| `Execution Override Quality Gate Failures` | Godkänn viktiga fel i kvalitetsgrinden | x | x | x |  |  |
| `Pipeline Create` | Ställ in/redigera pipeline |  | x |  |  |  |
| `Pipeline Read` | Se pipeline-information | x | x | x | x | x |
| `Pipeline Write` | Ställ in/redigera pipeline |  | x |  |  |  |
| P`ipeline Modify Approval` | Tillåter redigering av alternativet Affärsägare |  | x |  |  |  |
| `Pipeline Modify Managed Deployment` | Tillåter redigering av CSE-tillsynsalternativet |  | x |  |  |  |
| `Pipeline Delete` | Tillåter att pipeline tas bort |  | x |  |  |  |
| `Step Read` | Se resultaten av mätvärdena för stegkvalitet | x | x | x | x | x |
| `Generate Personal Access Token` | Access Git |  | x |  | x |  |

<!-- CQDOC-22080 | Download log files  |  |  | x |  | x |  | -->

Mer information om hur du konfigurerar användare finns i [Konfigurera användare och roller](/help/requirements/users-and-roles.md).

>[!TIP]
>
>Anpassade behörighetsprofiler med konfigurerbara behörigheter är också tillgängliga. Mer information finns i [Anpassade behörigheter](/help/using/custom-permissions.md).
