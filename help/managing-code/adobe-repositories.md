---
title: Lägga till Adobe-databaser i Cloud Manager
description: Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.
source-git-commit: 85c1e22609dc5646d3de0ccc71e9423d4243e13a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Lägga till Adobe-databaser i Cloud Manager {#adobe-repositories}

Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.

## Lägga till en Adobe-hanterad databas {#add-adobe-repository}

The **Databaser** gör det enkelt att lägga till fler Adobe-hanterade databaser för programmet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** väljer du **Databaser** för att växla till **Databaser** sida.

1. Klicka **Lägg till databas** i verktygsfältet.

   ![Knappen Lägg till databas](assets/repositories.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![Dialogrutan Lägg till databas](assets/add-repository-wizard.png)

När guiden stängs visas den nya databasen i tabellen i **Databaser** -fönstret. Nu kan du associera en [Rörledning för CI/CD](/help/overview/ci-cd-pipelines.md) med det eller hantera det i [**Databaser** -fönstret.](managing-repositories.md)

>[!TIP]
>
>Du kan också lägga till GitHub-databaser som du hanterar själv som [privata databaser.](private-repositories.md)
