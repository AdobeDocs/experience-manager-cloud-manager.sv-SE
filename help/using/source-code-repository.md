---
title: Databas för källkod
seo-title: Source Code Repository for Adobe AEM Cloud Manager
description: Följ den här sidan för att lära dig mer om Git-databasen som är avsedd för varje program som du har i Cloud Manager.
seo-description: Follow this page to learn about the git repository that is provisioned for each program you have in Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: Provisioning
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# Databas för källkod {#source-code-repository}

## Cloud Manager-databas {#cloud-manager-repository}

Dina [!UICONTROL AEM Managed Services] prenumerationen kommer att innehålla en källkodsdatabas som tillhandahålls och hanteras av Adobe. Varje kunds program tilldelas en enda unik **Git-databas**, där den tillhörande koden lagras och skyddas.

Som en god praxis bör du alltid använda Cloud Managers Git-databas, som är tom utan några förgreningar som konfigurerats eller exempelprojekt. Om du vill använda Cloud Managers Git-databas får du ett **token för privat åtkomst** som gör att du kan använda en Git-kompatibel klient för att skapa grenar, lagra och hämta din kod, lista implementeringshistoriken osv.

Mer information om hur du ställer in grenar i Git finns i [Konfigurera dina Release-grenar](configure-your-release-branches.md).

Mer information om hur du använder Cloud Managers **Git-databas** med CI/CD Pipeline, se dokumenten [Konfigurera produktionsförlopp](configuring-production-pipelines.md) och [Konfigurera icke-produktionsförlopp](configuring-non-production-pipelines.md) om du vill veta mer.

## Lokal databas {#on-premise-repository}

I vissa fall har du en befintlig Git-databas och vill fortsätta använda den. I dessa fall kan du använda Git-funktionen som stöds för flera fjärrdatabaser. Den dagliga utvecklingen kommer att fortsätta i din Git-databas. När en utgivningsgren är klar för en distribution till produktion skickar du den senaste koden till Cloud Managers Git-databas och utlöser Cloud Managers CI/CD-pipeline.

>[!NOTE]
>
>Om du vill visa de gemensamma Git-kommandona går du till [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf).
