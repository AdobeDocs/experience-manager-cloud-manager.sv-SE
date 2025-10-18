---
title: Använda guiden Nytt projekt
description: Följ den här sidan för att lära dig hur du använder guiden för att skapa ett AEM Application Project.
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: b98e1711f1f98f52977dd6cb4cd2bc834d81a360
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Använd den nya projektguiden {#using-the-wizard}

När du är registrerad på Cloud Manager som ny kund får du en tom Git-databas. Som hjälp att komma igång erbjuder Cloud Manager en guide för att skapa ett minimalt AEM-projekt baserat på [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) som utgångspunkt.

Följ de här stegen för att skapa ett AEM-projekt med guiden.

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välj lämplig organisation.

1. Om du inte redan har det [skapar du ditt program](program-setup.md). När programmet skapas upptäcker Cloud Manager att databaserna inte har konfigurerats än. Ett särskilt call-to-action-kort visas sedan på skärmen **Översikt**.

   ![Skapa projekt-CTA](/help/assets/image2018-10-3_14-29-44.png)

1. Klicka på **Skapa** för att starta guiden och ange viktiga värden.

   * **Titel** - Projektets titel. Som standard anges namnet på programmet.
   * **Nytt grennamn** - Den första grenen i Git-databaserna. Som standard är det `main`.

   ![Projektvärden](/help/assets/screen_shot_2018-10-08at55825am.png)

1. Dialogrutan har en låda som du kan öppna genom att klicka på handtaget längst ned. I den utökade versionen av dialogrutan visas alla konfigurationsparametrar för AEM-projekttypen. De här parametrarna har standardvärden som genereras baserat på den **Title** som du redan har angett och som inte behöver ändras. De förklaras här för din information.

   ![Detaljerade parametrar för arketyp](/help/assets/screen_shot_2018-10-08at60032am.png)

1. Klicka på **Skapa** om du vill skapa startprojektet med hjälp av arketypen och spara det i den namngivna Git-grenen.

Du har nu ett basprojekt. Det är dags att lägga upp dina rörledningar.

## Befintliga eller migrerade kunder {#existing-migrating}

Om du är en Adobe Managed Services-kund (AMS) eller en AEM-kund på plats som migrerar har du troligen redan en projektkod i Git eller ett annat versionskontrollsystem.

I så fall kan du importera ditt projekt till Cloud Manager Git-databasen.
