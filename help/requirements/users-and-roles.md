---
title: Lägg till användare och roller
description: Lär dig hur du använder Admin Console för att lägga till användare och roller och skapa profiler.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 15%

---


# Lägg till användare och roller {#add-users-and-roles}

Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter att använda. Exempelvis kan bara vissa användare ange nyckeltal (KPI) för ett program. Dessa behörigheter är logiskt grupperade i roller.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!NOTE]
>
>Används [!UICONTROL Cloud Manager]måste du ha en Adobe ID och Adobe Managed Services-produktkontexten.

## Rolldefinitioner {#role-definitions}

I den här tabellen sammanfattas rollerna.

| [!UICONTROL Cloud Manager] Roll | Beskrivning |
|--- |--- |
| Företagsägare | Den här användaren ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov. |
| Programhanteraren | Den här användaren använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och godkänna viktiga 3-nivåfel vid behov. |
| Distributionshanteraren | Den här användaren hanterar distributionsåtgärder och använder [!UICONTROL Cloud Manager] för att utföra mellanlagrings-/produktionsdistributioner, redigera CI/CD-pipelines, godkänna viktiga 3-skiktsfel vid behov och få tillgång till Git-databasen. |
| Utvecklare | Den här användaren utvecklar och testar anpassad programkod och använder främst [!UICONTROL Cloud Manager] om du vill visa distributionsstatus och har åtkomst till Git-databasen för kodimplementeringar. |
| Customer Success Engineer | Den här användaren stöder i allmänhet kundframgångar för AMS-kunder och interagerar med [!UICONTROL Cloud Manager] för att genomföra driftsättningar som kräver CSE-tillsyn. |
| Innehållsförfattare | Användaren interagerar vanligtvis inte med [!UICONTROL Cloud Manager] men kan använda [!UICONTROL Cloud Manager] programväljaren för att få åtkomst till AEM. |

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

## Skapa en profil med Admin Console {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] roller hanteras från Admin Console. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager] produktprofil.

Admin Console är en central plats för hantering av Adobe i hela organisationen. Mer information om Adobe Admin Console finns i dokumentationen för [Admin Console.](https://helpx.adobe.com/enterprise/using/admin-console.html)

>[!NOTE]
>
>Gå till Admin Console och konfigurera ditt team (användare och roller) på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

För att kunna tillhandahålla lämpliga rollbaserade behörigheter till [!UICONTROL Cloud Manager] -användare måste en administratör i kundens organisation skapa nya produktprofiler under [!UICONTROL AEM Managed Services] produktsammanhang som motsvarar var och en av de fyra [!UICONTROL Cloud Manager] roller:

* Företagsägare
* Distributionshanteraren
* Utvecklare
* Programhanteraren

Du kan skapa eller lägga till användare/grupper i dessa produktprofiler med Admin Console.

1. Logga in på Admin Console och klicka **Ny profil** för att lägga till en ny profil.

   ![Ny profil](/help/assets/admin_console_roles-1.png)

1. Ange informationen för att konfigurera en ny roll för [!UICONTROL Cloud Manager].

   * **Profilnamn**
   * **Visningsnamn**
   * **Behörighetsgrupp**

1. Klicka **Klar** för att slutföra skapandet av profilen.

När du skapar produktprofiler **Visningsnamn** måste vara det tekniska värde som definieras av [!UICONTROL Cloud Manager] (se följande tabell). The **Profilnamn** kan vara vad som helst, men för att undvika förvirring bör du använda värdena i **Rekommenderat profilnamn** kolumn. När du skapar produktprofilen avmarkerar du **Samma som profilnamn** och anger motsvarande värde som **visningsnamn**.

| **Roll** | **Visningsnamn (obligatoriskt)** | **Rekommenderat profilnamn** |
|---|---|---|
| Företagsägare | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Roll för företagsägare |
| Distributionshanteraren | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Distributionshanterarroll |
| Utvecklare | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Utvecklarroll |
| Programhanteraren | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Programhanterarroll |

![Skapa en ny profil](/help/assets/screen_shot_2018-05-04at171819.png)

När du har skapat en produktprofil kan du lägga till användare (eller grupper) i dessa produktprofiler.

![Redigera användare](/help/assets/image2018-4-9_15-19-26.png)

![Användargrupper](/help/assets/image2018-4-9_15-16-47.png)
