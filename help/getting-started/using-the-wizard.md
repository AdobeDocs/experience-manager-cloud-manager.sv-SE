---
title: Använda guiden Nytt projekt
description: Följ den här sidan för att lära dig hur du använder guiden för att skapa ett AEM
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: cb791a4f148ba394687b5e824b75fe1386d83c18
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Använda guiden Nytt projekt {#using-the-wizard}

När du är registrerad på Cloud Manager som ny kund får du en tom Git-databas. För att du ska komma igång erbjuder Cloud Manager en guide för att skapa ett minimalt AEM baserat på [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) som startpunkt.

Följ de här stegen för att skapa ett AEM projekt med guiden.

1. Logga in i Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välja lämplig organisation.

1. Om du inte redan har det [skapa ditt program.](program-setup.md) När programmet har skapats känner Cloud Manager igen att databaserna ännu inte har konfigurerats och ett särskilt åtgärdskort visas på **Översikt** skärm.

   ![Skapa projekt-CTA](/help/assets/image2018-10-3_14-29-44.png)

1. Klicka **Skapa** för att starta guiden och ange viktiga värden.

   * **Titel** - Detta är projektets namn och är som standard inställt på namnet på programmet.
   * **Nytt grennamn** - Detta är den första grenen i Git-databaserna och kommer som standard att vara `main`.

   ![Projektvärden](/help/assets/screen_shot_2018-10-08at55825am.png)

1. Dialogrutan har en låda som du kan öppna genom att klicka på handtaget längst ned. I den utökade formen visas alla konfigurationsparametrar för AEM projekttyp. Dessa parametrar har standardvärden som genereras baserat på **Titel** du redan har angett och inte behöver ändras. De förklaras här för din information.

   ![Detaljerade arkivtypsparametrar](/help/assets/screen_shot_2018-10-08at60032am.png)

1. Klicka **Skapa** för att skapa startprojektet med hjälp av arketypen och spara i den namngivna Git-grenen.

Nu har du ett basprojekt! Nu kan du ställa in dina rörledningar.

## Befintliga eller migrerande kunder {#existing-migrating}

Om du är Adobe Managed Services-kund (AMS) eller en lokal AEM som migrerar till har du troligen redan en projektkod i Git eller ett annat versionskontrollsystem.

I så fall importerar du ditt projekt till Cloud Managers Git-databas.
