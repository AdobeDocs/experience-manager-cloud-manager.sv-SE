---
title: Source Code Repository
description: Lär dig mer om Git-databasen som är avsedd för alla program du har i Cloud Manager.
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Source Code Repository {#source-code-repository}

Lär dig mer om Git-databasen som är avsedd för alla program du har i Cloud Manager.

## Cloud Manager Repository {#cloud-manager-repository}

Din [!UICONTROL AEM Managed Services]-prenumeration innehåller en källkodsdatabas som har etablerats och hanteras av Adobe. Varje program tilldelas en enda unik Git-databas där den tillhörande koden lagras och skyddas.

Som en god praxis bör du alltid använda Cloud Manager Git-databas, som är tom utan några förgreningar som konfigurerats eller exempelprojekt. Om du vill använda Cloud Manager Git-databas får du en privat åtkomsttoken som gör att du kan använda vilken Git-klient som helst för att skapa grenar, lagra och hämta koden, lista implementeringshistoriken osv.

Mer information om hur du konfigurerar grenar i Git finns i [Konfigurera grenar ](/help/getting-started/configuring-branches.md).

Mer information om hur du använder Cloud Manager Git-databasen med CI/CD-pipeline finns i [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

## Lokal databas {#on-premise-repository}

Du kan ha en befintlig Git-databas och vill fortsätta använda den. I så fall kan du använda Git-funktionen för flera fjärrdatabaser. Den dagliga utvecklingen kommer att fortsätta i din Git-databas. När en utgivningsgren är klar för distribution till produktion kan du skicka den senaste koden till Cloud Manager Git-databasen och utlösa Cloud Manager CI/CD-pipeline.

Om du vill visa vanliga Git-kommandon läser du [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) på GitHub-webbplatsen.
