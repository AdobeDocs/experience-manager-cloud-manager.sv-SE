---
title: Använda guiden
description: Följ den här sidan för att lära dig hur du använder guiden för att skapa ett AEM
translation-type: tm+mt
source-git-commit: 7146a41d64365c9de03d32f4fc4c33f9e366c244
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 9%

---


# Använda guiden {#using-wizard-to-create-an-aem-application-project}

När kunderna är ombord på Cloud Manager får de en tom Git-databas. Nuvarande Adobe Managed Services-kunder (eller lokala AEM-kunder som migrerar till AMS) har vanligtvis redan sin projektkod i Git (eller något annat versionskontrollsystem) och kommer att importera sitt projekt till Cloud Managers Git-databas. Nya kunder har dock inga befintliga projekt.

För att hjälpa nya kunder att komma igång kan Cloud Manager nu skapa ett minimalt AEM som utgångspunkt. Den här processen baseras på [**AEM projekttyp**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).


Följ stegen nedan för att skapa ett AEM programprojekt i Cloud Manager:

1. När du har loggat in på Cloud Manager och den grundläggande programkonfigurationen är klar, visas ett särskilt CTA-kort på skärmen **Översikt**, om databasen är tom.

   ![](assets/image2018-10-3_14-29-44.png)

1. Klicka på **Skapa för att** öppna en dialogruta där användaren kan ange de parametrar som krävs för AEM projekttyp. I standardformuläret frågar dialogrutan efter två värden:

   * **Titel** - som standard är detta inställt på *Programnamn*

   * **Nytt grennamn** - som standard är detta *överordnad*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   Dialogrutan har en låda som du kan öppna genom att klicka på handtaget längst ned i dialogrutan. I den utökade versionen av dialogrutan visas alla konfigurationsparametrar för Arketypen. Många av dessa parametrar har standardvärden som genereras baserat på **titeln**.

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >Om t.ex. **Title** är ***We.Finance*** genereras parametern Base Maven Artifact Id som ***com.weFinance***. Om du vill kan du ändra dessa värden.
   >
   >
   >Du kan till exempel ändra från det genererade ***värdet com.weFinance*** till ***net.weFinance***.

1. Klicka på **Skapa** i det föregående steget för att skapa startprojektet med hjälp av arkitypen och spara i den namngivna Git-grenen. När det är klart kan du konfigurera pipeline.