---
title: Lägga till Adobe-databaser i Cloud Manager
description: Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.
exl-id: 24c6ca97-ea70-41b8-b4c7-b8b0f406a57d
source-git-commit: e93285f7c7495ec9d2f11d289adaf6aaba7e58ea
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Lägga till Adobe-databaser i Cloud Manager {#adobe-repositories}

Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.

## Lägga till en Adobe-hanterad databas {#add-adobe-repository}

Fönstret **Databaser** gör det enkelt att lägga till fler Adobe-hanterade databaser för ditt program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** väljer du fliken **Databaser** för att växla till sidan **Databaser**.

1. Klicka på **Lägg till databas** i verktygsfältet.

   ![Knappen Lägg till databas](assets/repositories.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![Dialogrutan Lägg till databas](assets/add-repository-wizard.png)

När guiden stängs visas din nya databas i tabellen i fönstret **Databaser**. Nu kan du associera en [CI/CD-pipeline](/help/overview/ci-cd-pipelines.md) med den eller hantera den i fönstret [**Databaser**.](managing-repositories.md)

>[!TIP]
>
>Du kan också lägga till GitHub-databaser som du hanterar själv som [privata databaser.](private-repositories.md)
