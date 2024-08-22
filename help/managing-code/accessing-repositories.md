---
title: Information om databasåtkomst
description: Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via självbetjäning från Cloud Manager.
exl-id: 1cc88c82-67c7-4553-a1b8-d2ab22be466c
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Information om databasåtkomst {#accessing-repos}

Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via självbetjäning i Cloud Manager.

## Hämta databasinformation från sidan Översikt {#overview-page}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till **pipelines**-kortet från sidan **Programöversikt**.

   ![Knappen Åtkomst till information om upprepning på miljökortet](assets/pipelines-card.png)

1. Klicka på **Åtkomst till replikinformation**. I dialogrutan **Databasinformation för..** kan du visa följande:

   * Git-användarnamn.
   * Git-lösenordet.
   * URL:en till Cloud Manager Git-databasen.
   * Färdiga Git-kommandon för att snabbt lägga till en fjärranslutning i Git-repo och push-kod.

   ![Fönstret Databasinformation](assets/access-repo-info.png)

1. Ett nytt lösenord måste skapas för att du ska kunna få åtkomst till lösenordet. Klicka på **`Generate password`**.

1. I dialogrutan **Är du säker..** bekräftar du lösenordsgenereringen genom att klicka på **Generera lösenord**.

   ![Bekräfta generering av lösenord](assets/confirm-password-generation.png)

1. I fältet **Lösenord** genereras lösenordet. Klicka på kopieringsikonen för att kopiera den till Urklipp.

   * När du genererar ett lösenord blir det tidigare lösenordet ogiltigt.
   * Cloud Manager sparar inte ditt lösenord. Spara lösenordet på ett säkert sätt.
   * Om du tappar bort lösenordet måste du skapa ett nytt.

   ![Exempel på ett genererat lösenord](assets/generated-password.png)

Med hjälp av dessa uppgifter kan du klona en lokal kopia av databasen, göra ändringar i den lokala databasen och när du är klar spara kodändringar i fjärrkoddatabasen i Cloud Manager.

>[!NOTE]
>
>* Alternativet **Åtkomst till upprepningsinformation** är synligt för användare med rollen **Utvecklare**, rollen **Distributionshanterare** eller båda.
>* Knappen **Åtkomst till replikinformation** visar bara databasåtkomstinformation för databaser som hanteras med Adobe. Åtkomstinformation om [privata databaser](private-repositories.md) är inte tillgänglig i Cloud Manager.

## Få åtkomst till databasinformation från fönstret Databaser {#repositories-window}

Knappen **Åtkomst till upprepningsinformation** är också tillgänglig i verktygsfältet i fönstret [**Databaser**](managing-repositories.md). Samma information om åtkomst till databaser som hanteras av Adobe visas.

## Återkalla ett lösenord {#revoke-password}

Du kan återkalla ett lösenord när som helst. [Skapa en supportbiljett för en sådan begäran](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support).

Biljetten behandlas med hög prioritet och återkallas vanligtvis inom en dag.
