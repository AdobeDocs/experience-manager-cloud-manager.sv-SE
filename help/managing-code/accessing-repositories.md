---
title: Information om databasåtkomst
description: Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering från Cloud Manager.
exl-id: 1cc88c82-67c7-4553-a1b8-d2ab22be466c
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Information om databasåtkomst {#accessing-repos}

Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering från Cloud Manager.

## Åtkomst till databasinformation från översiktssidan {#overview-page}

Med Cloud Manager är det enkelt att hämta databasåtkomstinformation för databaser som hanteras med Adobe genom att använda knappen **Åtkomst till repo** som finns på pipeline-kortet.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

   ![Knappen Åtkomst till information om upprepning på miljökortet](assets/pipelines-card.png)

1. Klicka på knappen **Åtkomst till replikinformation** för att öppna dialogrutan **Databasinformation** och visa:

   * Git-användarnamn.
   * Git-lösenordet.
   * URL:en till Cloud Manager Git-databasen.
   * Fördefinierade Git-kommandon för att snabbt lägga till en fjärranslutning i Git-repo och push-kod.

   ![Fönstret Databasinformation](assets/access-repo-info.png)

1. Ett nytt lösenord måste skapas för att du ska kunna få åtkomst till lösenordet. Klicka på knappen **Skapa lösenord** om du vill göra det.

1. Bekräfta generering av lösenord i dialogrutan **Är du säker..** genom att klicka på **Generera lösenord**.

   ![Bekräfta generering av lösenord](assets/confirm-password-generation.png)

1. Lösenordet genereras och visas för kopiering i fältet **Lösenord**.

   * Om du genererar ett lösenord blir det tidigare lösenordet ogiltigt.
   * Cloud Manager kommer inte att spara lösenordet. Det är ditt ansvar att spara lösenordet på ett säkert sätt.
   * Eftersom Cloud Manager inte sparar lösenordet måste du återskapa ett nytt om du tappar bort det.

   ![Exempel på ett genererat lösenord](assets/generated-password.png)

Med hjälp av dessa uppgifter kan du klona en lokal kopia av databasen, göra ändringar i den lokala databasen och när du är klar spara kodändringar i fjärrkoddatabasen i Cloud Manager.

>[!NOTE]
>
>* Alternativet **Åtkomst till replikinformation** är synligt för användare med rollerna **Utvecklare** eller **Distributionshanteraren**.
>* Knappen **Åtkomst till replikinformation** visar bara databasåtkomstinformation för databaser som hanteras med Adobe. Åtkomstinformation om [privata databaser](private-repositories.md) är inte tillgänglig i Cloud Manager.

## Åtkomst till databasinformation från fönstret Databaser {#repositories-window}

En **Access Repo Info** -knapp är också tillgänglig i verktygsfältet i [**databasfönstret**](managing-repositories.md). Den visar samma information om åtkomst till databaser som hanteras av Adobe.

## Återkalla ett åtkomstlösenord {#revoke-password}

Du kan återkalla ett lösenord när som helst. Om du vill göra det [skapar du en supportbiljett för den här begäran](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support).

Biljetten kommer att behandlas med hög prioritet och bör återkallas inom en dag.
