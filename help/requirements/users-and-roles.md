---
title: Lägg till användare och roller
description: Lär dig hur du använder Admin Console för att lägga till användare och roller och skapa profiler.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: dd96d773ea3e6b9c45886fe41b28d3dd70cb8a61
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 7%

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

För att kunna tillhandahålla lämpliga rollbaserade behörigheter till [!UICONTROL Cloud Manager] -användare måste en administratör i kundens organisation skapa nya produktprofiler under [!UICONTROL AEM Managed Services] produktsammanhang som motsvarar var och en av de fyra [!UICONTROL Cloud Manager] roller:

* Företagsägare
* Distributionshanteraren
* Utvecklare
* Programhanteraren

Du kan skapa eller lägga till användare/grupper i dessa produktprofiler med Admin Console.

1. Logga in på Admin Console vid [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Klicka på **Översikt** klickar du på den produkt du vill ändra på **Produkter och tjänster** kort. Om det inte finns med i listan använder du **Produkter** för att hitta produkten och klicka på den.

   ![Översiktsflik i Admin Console](/help/assets/admin-console-overview.png)

1. På **Produkter** klickar du på den miljö där du vill lägga till användare/grupper i produktprofiler.

   ![Fliken Produkter i Admin Console](/help/assets/admin-console-product.png)

1. På **Produktprofil** -fliken för produkten klickar du på **Ny profil** för att lägga till en ny profil.

   ![Ny profil](/help/assets/admin-console-product-profiles.png)

1. Ange informationen för att konfigurera en ny roll för [!UICONTROL Cloud Manager].

   * **Profilnamn** - **Profilnamn** kan vara vad som helst, men för att undvika förvirring bör du använda värdena i **Rekommenderat profilnamn** kolumn.
   * **Visningsnamn** - **Visningsnamn** måste vara det tekniska värde som definieras av [!UICONTROL Cloud Manager] (se följande tabell).
   * **Behörighetsgrupp** - Du kan välja en behörighetsgrupp för profilen (inte alltid tillgänglig).

   ![Skapa en ny profil](/help/assets/screen_shot_2018-05-04at171819.png)

   | Roll | Visningsnamn (obligatoriskt) | Rekommenderat profilnamn |
   |---|---|---|
   | Företagsägare | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Roll för företagsägare |
   | Distributionshanteraren | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Distributionshanterarroll |
   | Utvecklare | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Utvecklarroll |
   | Programhanteraren | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Programhanterarroll |


1. Klicka **Klar** för att spara den nya profilen.

## Tilldela profiler till användare eller användargrupper {#assign-profiles}

När du har skapat produktprofiler kan du tilldela användare eller användargrupper till dem.

1. Logga in på Admin Console vid [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. I Admin Console väljer du **Användare** -fliken.

   ![Fliken Användare](/help/assets/admin-console-users.png)

1. Klicka på **Användare** i den vänstra navigeringspanelen och klicka sedan på en användare för att ändra den.

1. Klicka på ellipsknappen i dialogrutan **Produkter** avsnitt och markera **Redigera**.

   ![Redigera användare](/help/assets/admin-console-edit-user.png)

1. I **Redigera produkter och användargrupper** klickar du på plusknappen och väljer de profiler som ska tilldelas användaren.

   * Om användaren redan är tilldelad rollerna är plusknappen en redigeringsknapp (en penna), men fungerar på samma sätt.

   ![Redigera produkter och användargrupper](/help/assets/admin-console-edit-products-and-user-groups.png)

1. Klicka **Spara** för att spara profilerna för användaren.

Upprepa samma steg för att tilldela profiler till användargrupper, men välj **Användargrupper** från den vänstra navigeringspanelen på **Användare** -fliken. Klicka på en användargrupp och välj **Tilldelade produktprofiler** och klicka **Tilldela produktprofil** för att tilldela profiler.

![Tilldela profiler till grupp](/help/assets/admin-console-edit-user-groups.png)
