---
title: Information om databasåtkomst
description: Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via Creative Cloud Manager.
source-git-commit: b15ef71ae24f51811798d2d25c8f75320e21c01f
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Information om databasåtkomst {#accessing-repos}

Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via Creative Cloud Manager.

## Åtkomst till databasinformation från översiktssidan {#overview-page}

Med Cloud Manager är det enkelt att hämta databasåtkomstinformation för databaser som hanteras av Adobe via **Åtkomst till svarsinformation** finns väl synligt på pipeline-kortet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** sida.

   ![Knappen Åtkomst till upprepningsinformation på miljökortet](assets/pipelines-card.png)

1. Tryck eller klicka på **Åtkomst till svarsinformation** för att öppna **Databasinformation** dialogruta och vy:

   * Git-användarnamn.
   * Git-lösenordet.
   * URL:en till Cloud Managers Git-databas.
   * Fördefinierade Git-kommandon för att snabbt lägga till en fjärranslutning i Git-repo och push-kod.

   ![Fönstret Databasinformation](assets/access-repo-info.png)

1. Ett nytt lösenord måste skapas för att du ska kunna få åtkomst till lösenordet. Om du vill göra det trycker eller klickar du på **Generera lösenord** -knappen.

1. Bekräfta generering av lösenord i dialogrutan **Är du säker...** genom att trycka på eller klicka **Generera lösenord**.

   ![Bekräfta lösenordsgenerering](assets/confirm-password-generation.png)

1. Lösenordet genereras och visas för kopiering i **Lösenord** fält.

   * Om du genererar ett lösenord blir det tidigare lösenordet ogiltigt.
   * Lösenordet sparas inte i molnhanteraren. Det är ditt ansvar att spara lösenordet på ett säkert sätt.
   * Eftersom lösenordet inte sparas i Cloud Manager måste du återskapa ett nytt lösenord om du tappar bort det.

   ![Exempel på ett genererat lösenord](assets/generated-password.png)

Med dessa autentiseringsuppgifter kan du klona en lokal kopia av databasen, göra ändringar i den lokala databasen och när du är klar spara kodändringar i fjärrkoddatabasen i Cloud Manager.

>[!NOTE]
>
>* The **Åtkomst till svarsinformation** alternativet är synligt för användare med **Utvecklare** eller **Distributionshanteraren** roller.
>* The **Åtkomst till svarsinformation** visas bara databasens åtkomstinformation för databaser som hanteras av Adobe. Åtkomstinformation om [privata databaser](private-repositories.md) är inte tillgängligt i Cloud Manager.

## Åtkomst till databasinformation från fönstret Databaser {#repositories-window}

An **Åtkomst till svarsinformation** finns även i verktygsfältet i [**Databaser** -fönstret.](managing-repositories.md) den visar samma information om åtkomst till databaser som hanteras av Adobe.

## Återkalla ett åtkomstlösenord {#revoke-password}

Du kan återkalla ett lösenord när som helst. Gör så här: [skapa en supportbiljett för den här förfrågan.](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

Biljetten kommer att behandlas med hög prioritet och bör återkallas inom en dag.