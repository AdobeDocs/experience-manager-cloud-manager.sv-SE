---
title: Source Code Repository
description: Läs mer om Git-databasen som är avsedd för alla program du har i Cloud Manager.
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Source kodarkiv {#source-code-repository}

Läs mer om Git-databasen som är avsedd för alla program du har i Cloud Manager.

## Cloud Manager-databas {#cloud-manager-repository}

Din [!UICONTROL AEM Managed Services]-prenumeration innehåller en källkodsdatabas som har etablerats och hanteras av Adobe. Varje program tilldelas en enda unik Git-databas där den tillhörande koden lagras och skyddas.

Som en god praxis bör du alltid använda Cloud Manager Git-databas, som är tom utan några förgreningar som konfigurerats eller provprojekt. Cloud Manager tillhandahåller en privat åtkomsttoken för sin Git-databas, så att du kan använda alla Git-klienter för att skapa grenar, hantera kod, hämta implementeringshistorik och mycket mer.

Mer information om hur du konfigurerar grenar i Git finns i [Konfigurera grenar](/help/getting-started/configuring-branches.md).

Mer information om hur du använder Cloud Manager Git-databasen med CI/CD-pipeline finns i [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp](/help/using/non-production-pipelines.md).

## Lokal databas {#on-premise-repository}

Du kan ha en befintlig Git-databas och vill fortsätta använda den, och då kan du använda Git-funktionen för flera fjärrdatabaser. Den dagliga utvecklingen kommer att fortsätta i din Git-databas. När en utgivningsgren är klar för distribution till produktion kan du skicka den senaste koden till Cloud Manager Git-databasen och utlösa Cloud Manager CI/CD-pipeline.

Mer information om vanliga Git-kommandon finns i [Git-värmebladet](https://education.github.com/git-cheat-sheet-education.pdf).
