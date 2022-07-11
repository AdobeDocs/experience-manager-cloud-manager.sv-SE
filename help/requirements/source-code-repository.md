---
title: Databas för källkod
description: Lär dig mer om Git-databasen som har etablerats för varje program du har i Cloud Manager.
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# Databas för källkod {#source-code-repository}

Lär dig mer om Git-databasen som har etablerats för varje program du har i Cloud Manager.

## Cloud Manager-databas {#cloud-manager-repository}

Dina [!UICONTROL AEM Managed Services] prenumerationen innehåller en källkodsdatabas som tillhandahålls och hanteras av Adobe. Varje program tilldelas en enda unik Git-databas där den tillhörande koden lagras och skyddas.

Som en god praxis bör du alltid använda Cloud Managers Git-databas, som är tom utan några förgreningar som konfigurerats eller exempelprojekt. Om du vill använda Cloud Managers Git-databas får du en privat åtkomsttoken som gör att du kan använda vilken Git-klient som helst för att skapa grenar, lagra och hämta koden, lista implementeringshistoriken osv.

Mer information om hur du ställer in grenar i Git finns i [Konfigurerar versionsgrenar.](/help/getting-started/configuring-branches.md)

Mer information om hur du använder Cloud Managers Git-databas med CI/CD-pipeline finns i dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md) om du vill veta mer.

## Lokal databas {#on-premise-repository}

Du kan ha en befintlig Git-databas och vill fortsätta använda den. I så fall kan du använda Git-funktionen för flera fjärrdatabaser. Den dagliga utvecklingen kommer att fortsätta i din Git-databas. När en utgivningsgren är klar för distribution till produktion kan du överföra den senaste koden till Cloud Managers Git-databas och utlösa Cloud Managers CI/CD-pipeline.

Om du vill visa gemensamma Git-kommandon går du till [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) på GitHub-webbplatsen.
