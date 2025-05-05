---
title: Information om databasåtkomst
description: Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via självbetjäning från Cloud Manager.
exl-id: 1cc88c82-67c7-4553-a1b8-d2ab22be466c
source-git-commit: 04fbc4a3fdba8b108055d66a4fdb1a31994cb18e
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Information om databasåtkomst {#accessing-repos}

Lär dig hur du får åtkomst till och hanterar dina Adobe-hanterade Git-databaser med hjälp av Git-kontohantering via självbetjäning i Cloud Manager.

## Hämta databasinformation från sidan Översikt {#overview-page}

Med Cloud Manager är det enkelt att hämta databasåtkomstinformation för databaser som hanteras med Adobe med hjälp av **Åtkomst till repo** från **pipelines**-kortet.

I dialogrutan **Databasinformation** kan du visa följande åtkomstinformation för databaser som hanteras med Adobe:

* Git-användarnamn.
* Git-lösenordet.
* URL:en till Cloud Manager Git-databasen.
* Färdiga Git-kommandon för att snabbt lägga till en fjärranslutning i Git-repo och push-kod.

  ![Fönstret Databasinformation](assets/repository-info.png)

Åtkomstinformation om [privata databaser](/help/managing-code/private-repositories.md) är inte tillgänglig i Cloud Manager.

Funktionen **Åtkomst till replikinformation** är synlig för användare med rollerna **Utvecklare** eller **Distributionshanteraren**.

**Så här kommer du åt databasinformation från översiktssidan:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** klickar du på **Åtkomst till replikinformation** under kortet **Pipelines**.

   ![Åtkomst till replikinformation på Pipelilinnes-kort](/help/managing-code/assets/pipelines-card2.png)

1. Ett nytt lösenord måste skapas för att du ska kunna få åtkomst till lösenordet. Välj **Generera lösenord** i dialogrutan **Databasinformation**.

1. Välj **Generera lösenord** i bekräftelsedialogrutan.

1. Klicka på ikonen ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) till höger om fältet **Lösenord** för att kopiera lösenordet till Urklipp.

   * När du genererar ett lösenord blir det tidigare lösenordet ogiltigt.
   * Cloud Manager sparar inte lösenordet. Det är ditt ansvar att spara lösenordet på ett säkert sätt.
   * Eftersom Cloud Manager inte sparar lösenordet måste du återskapa ett nytt om du förlorar det.

   ![Kopiera lösenord i dialogrutan Databasinformation](/help/managing-code/assets/repository-copy-password.png)

Med hjälp av dessa uppgifter kan du klona en lokal kopia av databasen, göra ändringar i den lokala databasen och när du är klar spara kodändringar i fjärrkoddatabasen i Cloud Manager.

## Få åtkomst till databasinformation från fönstret Databaser {#repositories-window}

Funktionen **Åtkomstrepo** är också tillgänglig från sidan [**Databaser**](/help/managing-code/managing-repositories.md). Samma information om åtkomst till databaser som hanteras av Adobe visas.

## Återkalla ett lösenord {#revoke-password}

Du kan återkalla ett lösenord när som helst.

Om du vill göra det [skapar du en supportbiljett för den här begäran](https://experienceleague.adobe.com/sv?support-solution=Experience+Manager&amp;support-tab=home#support). Biljetten behandlas med hög prioritet och återkallas vanligen inom en dag.
