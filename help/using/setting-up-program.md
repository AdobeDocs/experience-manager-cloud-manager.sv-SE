---
title: Konfigurera ditt program
seo-title: Konfigurera ditt program
description: Efter introduktionen måste företagsägaren göra en inledande konfiguration av programmet.
seo-description: 'Efter introduktionen måste företagsägaren göra en inledande konfiguration av Adobe AEM Cloud Manager. Detta innebär att ange programbeskrivningen och definiera de nyckeltal som ska användas för prestandatestning. '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 2c05eb4610e35d5126c6c67e44f4b71f3026c887

---


# Konfigurera ditt program {#setup-your-program}

Efter introduktionen måste företagsägaren slutföra en inledande konfiguration av programmet. Detta innebär att du ställer in programbeskrivningen och definierar de KPI:er (Key Performance Indicators) som ska användas för prestandatestning. Du kan också överföra en miniatyrbild. Dessutom kan företagsägaren konfigurera miljöetablering medan programmet konfigureras.

De KPI:er som definieras fungerar som en baslinje för prestandatestning som skickas varje gång pipeline körs.

>[!NOTE]
>
>De nyckeltal som definieras mäts i tester som körs i **scenmiljön** . Vanligtvis skalas dessa KPI:er ned så att de passar scenmiljöns funktioner.
>
>En användare som t.ex. förväntar sig i genomsnitt 1 000 sidvisningar per minut i sin produktionsmiljö **** och som har fyra dispatcher-/publiceringsservrar i produktion bör skala detta till 250 sidvisningar per minut (förutsatt att scenmiljön bara består av ett enda dispatcher-/publiceringsserverpar).
>
>Dessutom har många användare ett CDN (Content Delivery Network), till exempel Akamai eller CloudFront, framför produktionsmiljön. Eftersom [!UICONTROL Cloud Manager] tester utförs direkt mot scenmiljön bör KPI endast återspegla den trafik som förväntas passera genom CDN, dvs. cacheminnet missar. Vanligtvis är detta en relativt liten del av den totala produktionstrafiken.

## Använda [!UICONTROL Cloud Manager] för att konfigurera ditt program {#using-cloud-manager-to-setup-your-program}

Följ stegen nedan för att konfigurera programmet och definiera nyckeltal:

1. Klicka på **Konfigurera program** för att starta installationsprocessen i [!UICONTROL Cloud Manager].

   ![](assets/SetUpProgram1.png)

1. Skärmen **Installationsprogram** visar Redigera programinformation.

1. Du kan se tre alternativ som **Allmänt**, **KPI** och **Etablering** .

1. På fliken **Allmänt** överför du en miniatyrbild till programmet. Du kan också lägga till en beskrivning till programmet.

   ![](assets/Setup_Program-General.png)

1. Under **KPI** kan du definiera två KPI:er (förväntningarna för varje distribution). Separata KPI:er definieras för **AEM Sites** och **AEM Assets**. Du kan ange nyckeltal för de produkter som du har licensierat.

   **AEM Sites**

   1. Hur lång är den 95:e percentilens svarstid som du kan acceptera?

      * Rekommenderat värde - 3 sekunder
   1. Hur många sidvisningar per minut under toppbelastningen?

      * Rekommenderat värde - 200 sidvisningar per minut
   **AEM Assets**

   Sedan den första versionen har Cloud Manager kunnat köra prestandatestning för AEM Sites-program. I den här versionen har funktionen även lagts till för att utföra prestandatester för AEM Assets-program. Resursprestandatestning utförs genom att resurser laddas upp upprepade gånger under en 30-minuters testperiod och att bearbetningstiden för varje tillgång samt olika mätvärden på systemnivå mäts.
Under programinstallationen anges resursspecifika nyckeltal:

   * 95:e percentilens bearbetningstid
   * Överförda resurser per minut
   ![](assets/Setup_Program-KPIs.png)

1. Under **Provisioning** kan du visa eller redigera provisioneringskonfigurationen för produktions- och icke-produktionsmiljöer i ditt program. Du ser att **Automatisk skalning är aktiverat** om autoskalning har aktiverats för programmet.

   >[!NOTE]
   >
   >* Funktionen för autoskalning kan bara användas i produktionsmiljön och kanske inte är tillgänglig för alla kundprogram.
   >* On-demand-skalning är inte tillgängligt för den här versionen av [!UICONTROL Cloud Manager].


   ![](assets/Setup_Program-Provisioning.png)

1. Klicka på **Spara** för att slutföra installationsguiden.

   >[!NOTE]
   >
   >Du kan alltid redigera programmet när det initiala programmet redan har konfigurerats. Följ stegen nedan för mer information.

## Redigera ett program

1. Navigera till lösningen på startskärmen i **Cloud Manager** .

   ![](assets/SetUpProgram5.png)

1. Välj lösningen och klicka på **Redigera** för att uppdatera eller ändra programmet, vilket visas i bilden nedan.

   ![](assets/SetUpProgram6.png)

1. Skärmen **Redigera program** visas där du kan uppdatera eller ändra programmet.

   ![](assets/Editing_Program-screen3.png)

## Nästa steg {#the-next-steps}

Om du redan har konfigurerat **pipeline** kommer de uppdaterade inställningarna att beaktas vid nästa körning. Om du inte har konfigurerat pipeline än följer du stegen för att konfigurera din pipeline först.

Se [Konfigurera CI/CD-pipeline](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) för att konfigurera pipeline.