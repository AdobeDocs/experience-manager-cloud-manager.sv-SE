---
title: Hantera åtkomsttoken i Cloud Manager
description: Lär dig hur du visar, redigerar och tar bort åtkomsttoken som används för Använd egen Git i Cloud Manager i Adobe Managed Services.
badge: label="Privat beta" type="Positive" url="/help/release-notes/current.md#access-tokens"
exl-id: 873aad0b-d7c6-4bc3-a70d-bbfdc1e02193
source-git-commit: 254ad0ac77e793657292e34ae4a6bf3baecea8d5
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Hantera åtkomsttoken för externa databaser {#manage-access-tokens}

Cloud Manager använder åtkomsttoken för att hantera databaser på externa Git-plattformar. Tidigare var det nödvändigt att återanvisa den associerade databasen om en token skulle upphöra att gälla för att fortsätta fungera.

Med funktionen **Hantera åtkomsttoken** kan du nu hantera tokens mer effektivt. Du kan visa, byta namn på eller ta bort tokens som är anslutna till externa Git-providers som stöds, inklusive GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se även [Lägg till externa databaser i Cloud Manager](/help/managing-code/external-repositories.md).

>[!NOTE]
>
>De funktioner som beskrivs i den här artikeln är endast tillgängliga via det privata betaprogrammet. Mer information och om du vill registrera dig för den privata betaversionen finns i [Hantera åtkomsttoken](/help/release-notes/current.md#access-tokens).

## Visa åtkomsttoken {#view-access-tokens}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/getting-started/navigation.md#my-programs-console)** väljer du det program vars Git-åtkomsttoken du vill hantera.
1. Klicka på ![Mappdispositionsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Databaser** på sidomenyn under **Program**.
1. Klicka på **Hantera åtkomsttoken** i sidans övre högra hörn.

   Knappen **Hantera åtkomsttoken** visas bara om programmet använder funktionen Hämta egen Git.

   ![Dialogrutan Hantera åtkomsttoken innehåller en aktiv token och en inaktiv token](/help/managing-code/assets/access-tokens-manage.png)

1. I dialogrutan **Hantera åtkomsttoken**:
   * Alla åtkomsttoken visas.
   * Du kan **redigera** alla token.
   * Du kan **ta bort** endast token som *inte används*. Om en token används är knappen ![Ta bort disposition](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) inaktiverad.

## Redigera en åtkomsttoken {#edit-access-tokens}

1. Klicka på ![Redigera-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) i dialogrutan **Hantera åtkomsttoken** till höger om ett tokennamn.
1. I dialogrutan **Redigera åtkomsttoken** uppdaterar du **tokennamnet**, **åtkomsttoken** eller båda.

   ![Dialogrutan Redigera åtkomsttoken](/help/managing-code/assets/access-tokens-edit.png)

1. Om **åtkomsttoken** används för närvarande visas ett varningsmeddelande om att alla associerade databaser automatiskt valideras efter uppdateringen.

1. Klicka på **Uppdatera** för att spara ändringarna.

## Ta bort en åtkomsttoken {#delete-access-token}

1. Klicka på ikonen ![Ta bort](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) i dialogrutan **Hantera åtkomsttoken** till höger om ett tokennamn.

   Ikonen är inaktiverad (![Ta bort dispositionsikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)) för tokens som används.

1. Klicka på **Ta bort** i dialogrutan **Ta bort åtkomsttoken** om du vill ta bort token permanent.
