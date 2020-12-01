---
title: Databas för källkod
seo-title: Källkodslagringsplats för Adobe AEM Cloud Manager
description: Följ den här sidan för att lära dig mer om Git-databasen som är avsedd för varje program som du har i Cloud Manager.
seo-description: Följ den här sidan för att lära dig mer om Git-databasen som är avsedd för alla program du har i Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
translation-type: tm+mt
source-git-commit: 697311cd00ef96568f6befd2fe76febafc27961e
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---


# Databas för källkod {#source-code-repository}

## Cloud Manager-databas {#cloud-manager-repository}

Din [!UICONTROL AEM Managed Services]-prenumeration innehåller en källkodsdatabas som tillhandahålls och hanteras av Adobe. Varje kunds program tilldelas en enda och unik **Git-databas**, där den tillhörande koden lagras och skyddas.

Som en god praxis bör du alltid använda Cloud Managers Git-databas, som är tom utan några förgreningar som konfigurerats eller exempelprojekt. Om du vill använda Cloud Managers Git-databas får du en **privat åtkomsttoken** som gör att du kan använda vilken Git-kompatibel klient som helst för att skapa grenar, lagra och hämta din kod, visa implementeringshistorik osv.

Mer information om hur du konfigurerar grenar i Git finns i [Konfigurera dina Release-grenar](configure-your-release-branches.md).

Mer information om hur du använder Cloud Managers **Git-databas** med CI/CD-pipeline finns i [Konfigurera CI/CD-pipeline](configuring-pipeline.md).

## Lokal databas {#on-premise-repository}

I vissa fall har du en befintlig Git-databas och vill fortsätta använda den. I dessa fall kan du använda Git-funktionen som stöds för flera fjärrdatabaser. Den dagliga utvecklingen kommer att fortsätta i din Git-databas. När en utgivningsgren är klar för en distribution till produktion skickar du den senaste koden till Cloud Managers Git-databas och utlöser Cloud Managers CI/CD-pipeline.

>[!NOTE]
>
>Mer information om vanliga Git-kommandon finns i [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf).

