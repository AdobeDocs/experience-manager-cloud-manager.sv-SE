---
title: Lägg till användare och roller
description: Lär dig hur du använder Admin Console för att lägga till användare och roller och skapa profiler.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: 9ad9af206fafea45f8bbf61b02950de0776b5a9f
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 4%

---


# Lägga till användare och roller {#add-users-and-roles}

Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att kunna använda. Exempelvis kan bara vissa användare ange nyckeltal (KPI) för ett program. Dessa behörigheter är logiskt grupperade i roller.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare, som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!NOTE]
>
>Om du vill använda [!UICONTROL Cloud Manager] måste du ha en Adobe ID och Adobe Managed Services produktkontext.

## Rolldefinitioner {#role-definitions}

I följande tabell sammanfattas rollerna i Cloud Manager.

| Rollen [!UICONTROL Cloud Manager] | Beskrivning |
| --- | --- |
| Business Owner | Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov. |
| Program Manager | De använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-nivåfel vid behov. |
| Deployment Manager | Hanterar distributionsåtgärder och använder [!UICONTROL Cloud Manager] för att utföra mellanlagrings- och produktionsdistributioner, redigera CI/CD-pipelines och godkänna kritiska 3-nivåfel vid behov. De har även tillgång till Git-databasen. |
| Developer | Utvecklar och testar anpassad programkod och använder främst [!UICONTROL Cloud Manager] för att visa distributionsstatus och få åtkomst till Git-databasen för kodimplementeringar. |
| Customer Success Engineer | CSE stöder vanligtvis kundframgångar för AMS-kunder. De interagerar med [!UICONTROL Cloud Manager] i syfte att köra distributioner som kräver CSE-övervakning. |
| Innehållsförfattare | De interagerar vanligtvis inte med [!UICONTROL Cloud Manager], men de kan använda programväljaren [!UICONTROL Cloud Manager] för att få åtkomst till AEM. |

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

## Skapa en produktprofil med Admin Console {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] roller hanteras från Admin Console. Specifika rollmedlemskap tillhandahålls genom att användaren läggs till i en [!UICONTROL Cloud Manager]-produktprofil.

Admin Console är en central plats för hantering av Adobe-berättiganden i hela organisationen. Mer information om Adobe Admin Console finns i [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

En administratör måste skapa nya produktprofiler under produktkontexten [!UICONTROL AEM Managed Services] för att tilldela rollbaserade behörigheter för [!UICONTROL Cloud Manager] -användare, som motsvarar var och en av de fyra [!UICONTROL Cloud Manager] rollerna.

* Business Owner
* Deployment Manager
* Developer
* Program Manager

Skapa eller lägg till användare eller grupper i dessa produktprofiler med Admin Console.

<!-- CQDOC-22790
>[!IMPORTANT]
>
>Due to a current limitation in the Admin Console and Cloud Manager, profiles cannot be saved with **No permissions** selected. Attempting to do so results in a backend error. This behavior affects the creation of Deployment Manager profiles. As a workaround, select at least one permission when creating a new profile. -->

**Så här skapar du en produktprofil med Admin Console:**

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

1. Klicka på fliken **Översikt** och klicka sedan på den produkt du vill redigera på kortet **Produkter och tjänster**. Om den inte finns med i listan använder du fliken **Produkter** för att leta reda på produkten och klicka på den.

   ![Översikt över Admin Console ](/help/assets/admin-console-overview.png)

1. På fliken **Produkter** klickar du på den miljö som du vill lägga till användare/grupper för i produktprofiler.

   ![Fliken Produkter i Admin Console](/help/assets/admin-console-product.png)

1. Klicka på **Ny profil** på fliken **Produktprofil** för att lägga till en ny profil.

   ![Ny profil](/help/assets/admin-console-product-profiles.png)

1. Ange informationen för att konfigurera en ny roll för [!UICONTROL Cloud Manager].

   * **Profilnamn** - **Profilnamn** kan vara vad som helst, men för att undvika missförstånd bör du använda värdena i kolumnen **Rekommenderat profilnamn**.
   * **Visningsnamn** - **Visningsnamn** måste vara det tekniska värde som definieras av [!UICONTROL Cloud Manager] (se följande tabell).
   * **Behörighetsgrupp** - Du kan välja en behörighetsgrupp för profilen (inte alltid tillgänglig).

<!-- CQDOC-22790
      >[!IMPORTANT]
      >
      >Due to a current limitation in the Admin Console and Cloud Manager, profiles cannot be saved with **No permissions** selected. Attempting to do so results in a backend error. This behavior affects the creation of Deployment Manager profiles. As a workaround, select at least one permission when creating a new profile. -->

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

1. I Admin Console väljer du fliken **Användare**.

   ![Fliken Användare](/help/assets/admin-console-users.png)

1. Klicka på **Användare** i den vänstra navigeringspanelen och klicka sedan på en användare för att ändra den.

1. Klicka på ikonen ![Mer, ellips](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i avsnittet **Produkter** och klicka på **Redigera**.

   ![Redigera användare](/help/assets/admin-console-edit-user.png)

1. I dialogrutan **Redigera produkter och användargrupper** klickar du på ikonen ![Lägg till, plustecken](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) och väljer de profiler som ska tilldelas till användaren.

   * Om användaren redan är tilldelad rollerna är knappen ![Lägg till plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) en redigeringsknapp (en penna), men fungerar på samma sätt.

   ![Redigera produkter och användargrupper](/help/assets/admin-console-edit-products-and-user-groups.png)

1. Klicka på **Spara** för att spara profilerna för användaren.

Upprepa samma steg om du vill tilldela profiler till användargrupper, men välj **Användargrupper** i den vänstra navigeringspanelen på fliken **Användare**. Klicka på en användargrupp och välj **Tilldelade produktprofiler** och klicka på **Tilldela produktprofil** för att tilldela profiler.

![Tilldela profiler till gruppen](/help/assets/admin-console-edit-user-groups.png)
