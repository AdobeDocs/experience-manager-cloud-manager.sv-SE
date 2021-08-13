---
title: Åtkomst till databaser
seo-title: Åtkomst till databaser
description: På den här sidan beskrivs hur du kan komma åt och hantera Git-databasen.
seo-description: Följ den här sidan för att lära dig hur du får åtkomst till och hanterar din Git-databas.
feature: Git-databaser
exl-id: 403fc93d-60fc-4439-8c9d-0a512ca34458
source-git-commit: 5bbe76a46b7a15ccbab85c4487d2a20aaf59a4e7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Åtkomst till databaser {#accessing-repos}

Du kan komma åt och hantera din Git-databas med hjälp av Git-kontohantering för självbetjäning från användargränssnittet i Cloud Manager.

## Använda självbetjäning för Git-kontohantering {#self-service-git}

Använd knappen **Åtkomst till repo-information** som är tillgänglig från användargränssnittet i Cloud Manager, som är mest framträdande på pipeline-kortet.

1. Gå till **Pipelines**-kortet från sidan **Programöversikt**.

1. Du kommer att visa alternativet **Åtkomst till repo-information** för att komma åt och hantera din Git-databas.

   ![](assets/access-repo1.png)

   Om du dessutom väljer pipelinefliken **Icke-produktion** visas även alternativet **Åtkomst till repo-information**.

   ![](assets/access-repo-nonprod.png)


   >[!NOTE]
   >Alternativet **Åtkomst till repo-information** är synligt för användare i rollen Utvecklare eller Distributionshanterare. Om du klickar på den här knappen öppnas en dialogruta där användaren kan hitta URL:en till sin Git-databas för Cloud Manager tillsammans med användarnamn och lösenord.

   ![](assets/access-repo-create.png)

   Viktigt att tänka på när du hanterar ditt Git i Cloud Manager är:

   * **URL**: Databas-URL
   * **Användarnamn**: Användarnamnet
   * **Lösenord**: Värdet som visas när användaren klickar på knappen **Generera lösenord**.


      >[!NOTE]
      >En användare kan checka ut en kopia av sin kod och göra ändringar i den lokala koddatabasen. När det är klart kan användaren spara sina kodändringar i fjärrkoddatabasen i Cloud Manager.
