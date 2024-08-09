---
title: Lägg till användare och roller
description: Lär dig hur du använder Admin Console för att lägga till användare och roller och skapa profiler.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 6%

---


# Lägg till användare och roller {#add-users-and-roles}

Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att kunna använda. Exempelvis kan bara vissa användare ange nyckeltal (KPI) för ett program. Dessa behörigheter är logiskt grupperade i roller.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!NOTE]
>
>Om du vill använda [!UICONTROL Cloud Manager] måste du ha en Adobe ID och produktkontexten för Adobe Managed Services.

## Rolldefinitioner {#role-definitions}

I tabellen sammanfattas rollerna.

| Roll för [!UICONTROL Cloud Manager] | Beskrivning |
|--- |--- |
| Business Owner | Den här användaren ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov. |
| Program Manager | Den här användaren använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-nivåfel vid behov. |
| Deployment Manager | Den här användaren hanterar distributionsåtgärder och använder [!UICONTROL Cloud Manager] för att utföra mellanlagrings-/produktionsdistributioner, redigera CI/CD-pipelines, godkänna viktiga 3-skiktsfel vid behov och har åtkomst till Git-databasen. |
| Developer | Den här användaren utvecklar och testar anpassad programkod och använder främst [!UICONTROL Cloud Manager] för att visa distributionsstatus och få åtkomst till Git-databasen för kodimplementeringar. |
| Customer Success Engineer | Den här användaren stöder vanligtvis kundframgångar för AMS-kunder och interagerar med [!UICONTROL Cloud Manager] i syfte att köra distributioner som kräver CSE-övervakning. |
| Innehållsförfattare | Den här användaren interagerar vanligtvis inte med [!UICONTROL Cloud Manager], men kan använda programväljaren [!UICONTROL Cloud Manager] för att komma åt AEM. |

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

## Skapa en profil med Admin Console {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] roller hanteras från Admin Console. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager]-produktprofil.

Admin Console är en central plats för hantering av Adobe i hela organisationen. Mer information om Adobe Admin Console finns i dokumentationen för [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

För att kunna ge rätt rollbaserade behörigheter till [!UICONTROL Cloud Manager] användare måste en administratör i kundens organisation skapa nya produktprofiler under produktkontexten för [!UICONTROL AEM Managed Services] som motsvarar var och en av de fyra [!UICONTROL Cloud Manager] rollerna:

* Business Owner
* Deployment Manager
* Developer
* Program Manager

Du kan skapa eller lägga till användare/grupper i dessa produktprofiler med Admin Console.

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

1. Klicka på fliken **Översikt** och klicka på den produkt du vill ändra på kortet **Produkter och tjänster**. Om den inte finns med i listan använder du fliken **Produkter** för att leta reda på produkten och klicka på den.

   ![Översikt över Admin Console ](/help/assets/admin-console-overview.png)

1. På fliken **Produkter** klickar du på den miljö som du vill lägga till användare/grupper för i produktprofiler.

   ![Fliken Produkter i Admin Console](/help/assets/admin-console-product.png)

1. Klicka på **Ny profil** på fliken **Produktprofil** för att lägga till en ny profil.

   ![Ny profil](/help/assets/admin-console-product-profiles.png)

1. Ange informationen för att konfigurera en ny roll för [!UICONTROL Cloud Manager].

   * **Profilnamn** - **Profilnamn** kan vara vad som helst, men för att undvika missförstånd bör du använda värdena i kolumnen **Rekommenderat profilnamn**.
   * **Visningsnamn** - **Visningsnamn** måste vara det tekniska värde som definieras av [!UICONTROL Cloud Manager] (se följande tabell).
   * **Behörighetsgrupp** - Du kan välja en behörighetsgrupp för profilen (inte alltid tillgänglig).

   ![Skapar en ny profil](/help/assets/screen_shot_2018-05-04at171819.png)

   | Roll | Visningsnamn (obligatoriskt) | Rekommenderat profilnamn |
   |---|---|---|
   | Business Owner | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Roll för företagsägare |
   | Deployment Manager | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Distributionshanterarroll |
   | Developer | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Utvecklarroll |
   | Program Manager | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - rollen programhanterare |


1. Klicka på **Klar** för att spara den nya profilen.

## Tilldela profiler till användare eller användargrupper {#assign-profiles}

När du har skapat produktprofiler kan du tilldela användare eller användargrupper till dem.

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

1. Gå till Admin Console och välj fliken **Användare**.

   ![Fliken Användare](/help/assets/admin-console-users.png)

1. Klicka på **Användare** i den vänstra navigeringspanelen och klicka sedan på en användare för att ändra den.

1. Klicka på ellipsknappen i avsnittet **Produkter** och välj **Redigera**.

   ![Redigera användare](/help/assets/admin-console-edit-user.png)

1. Klicka på plusknappen i dialogrutan **Redigera produkter och användargrupper** och välj de profiler som ska tilldelas till användaren.

   * Om användaren redan är tilldelad rollerna är plusknappen en redigeringsknapp (en penna), men fungerar på samma sätt.

   ![Redigera produkter och användargrupper](/help/assets/admin-console-edit-products-and-user-groups.png)

1. Klicka på **Spara** för att spara profilerna för användaren.

Upprepa samma steg om du vill tilldela profiler till användargrupper, men välj **Användargrupper** i den vänstra navigeringspanelen på fliken **Användare**. Klicka på en användargrupp och välj fliken **Tilldelade produktprofiler** och klicka på **Tilldela produktprofil** för att tilldela profiler.

![Tilldela profiler till gruppen](/help/assets/admin-console-edit-user-groups.png)
