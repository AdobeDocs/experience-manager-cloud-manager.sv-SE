---
title: Hantera databaser i Cloud Manager
description: Lär dig hur du skapar, visar och redigerar Git-databaser i Cloud Manager.
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 73add7bee892769d1b3864e3238aff26bf96162d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Cloud Manager-databaser {#cloud-manager-repos}

Lär dig hur du skapar, visar och redigerar Git-databaser i Cloud Manager.

## Ökning {#overview}

Databaser används för att lagra och hantera projektkoden med Git. Alla program som du skapar i Cloud Manager har en databas som hanteras av Adobe.

Du kan välja att skapa ytterligare databaser som hanterar Adobe och även lägga till egna privata databaser. Alla databaser som är kopplade till ditt program kan visas i **Databaser** -fönstret.

Databaser som skapas i Cloud Manager kan du också välja när du lägger till eller redigerar pipelines. Se [CI-CD-rör](/help/overview/ci-cd-pipelines.md) om du vill veta mer.

Det finns en enda primär databas eller en gren för en given pipeline. Med [stöd för Git-undermodul,](git-submodules.md) många sekundära grenar kan inkluderas vid byggtillfället.

## Fönstret Databaser {#repositories-window}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** väljer du **Databaser** för att växla till **Databaser** sida.

1. The **Databaser** visas alla databaser som är associerade med ditt program.

   ![Databasfönster](assets/repositories.png)

The **Databaser** -fönstret innehåller information om databaserna:

* Typ av databas
   * **Adobe** anger databaser som hanteras av Adobe
   * **GitHub** anger privata GitHub-databaser som du hanterar
* När den skapades
* Pipelines som är associerade med databasen

Du kan markera databasen i fönstret och klicka på ellipsknappen för att vidta åtgärder för den valda databasen.

* **[Kontrollera grenar/skapa projekt](#check-branches)** (endast tillgängligt för Adobe-databaser)
* **[Kopiera databas-URL](#copy-url)**
* **[Visa och uppdatera](#view-update)**
* **[Ta bort](#delete)**

![Databasåtgärder](assets/repository-actions.png)

## Lägga till databaser {#adding-repositories}

Tryck eller klicka på **Lägg till databas** knappen i **Databaser** fönster för att starta **Lägg till databas** guide.

![Guiden Lägg till databas](assets/add-repository-wizard.png)

Cloud Manager har stöd för båda databaser som hanteras av Adobe (**Adobe Repository**) och dina egna självhanterade databaser (**Privat databas**). De obligatoriska fälten varierar beroende på vilken typ av databas du väljer att lägga till. Mer information finns i följande dokument.

* [Lägga till Adobe-databaser i Cloud Manager](adobe-repositories.md)
* [Lägga till privata databaser i Cloud Manager](private-repositories.md)

>[!NOTE]
>
>* En användare måste ha rollen **Distributionshanteraren** eller **Företagsägare** för att kunna lägga till en databas.
>* Det finns en gräns på 300 databaser i alla program i ett visst företag eller i en IMS-organisation.

## Åtkomst till svarsinformation {#repo-info}

När du visar dina databaser i **Databaser** kan du visa information om hur du kommer åt databaser som hanteras med Adobe programmatiskt genom att trycka på eller klicka på **Åtkomst till svarsinformation** i verktygsfältet.

![Databasinformation](assets/access-repo-info.png)

The **Databasinformation** öppnas med information. Mer information om åtkomst till databasinformation finns i dokumentet [Åtkomst till databasinformation.](accessing-repositories.md)

## Kontrollera grenar {#check-branches}

The **Kontrollera grenar/skapa projekt** -åtgärden utför två funktioner beroende på databasens tillstånd.

* Om databasen är nyskapad skapar åtgärden ett exempelprojekt baserat på [AEM projekttyp.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/overview)
* Om exempelprojektet redan har skapats i databasen kontrolleras statusen för databasen och dess grenar, och sedan rapporteras om exempelprojektet redan finns.

![Kontrollera grenar](assets/check-branches.png)

## Kopiera databas-URL {#copy-url}

The **Kopiera databas-URL** åtgärden kopierar URL:en för databasen som valts i **Databaser** till Urklipp som ska användas någon annanstans.

## Visa och uppdatera {#view-update}

The **Visa och uppdatera** funktionsmakrot öppnar **Uppdatera databas** -dialogrutan. Med den kan du visa **Namn** och **Förhandsgranskning av databas-URL** samt uppdatera **Beskrivning** i databasen.

![Visa och uppdatera databasinformation](assets/update-repository.png)

## Ta bort {#delete}

The **Ta bort** -åtgärden tar bort databasen från ditt projekt. En databas kan inte tas bort om den är associerad med en pipeline.

![Ta bort](assets/delete.png)

Observera att när en databas tas bort i Cloud Manager markeras den som borttagen och är inte längre tillgänglig för användaren, men den bevaras i systemet i återställningssyfte.

Om du försöker skapa en ny databas efter att ha tagit bort en databas med samma namn får du felmeddelandet `An error has occurred while trying to create repository. Please contact your CSE or Adobe Support.`

Om du får det här felmeddelandet kontaktar du Adobe Support så att de kan hjälpa dig att byta namn på den borttagna databasen eller välja ett annat namn för den nya databasen.
