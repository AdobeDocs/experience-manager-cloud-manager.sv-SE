---
title: Programinställningar
description: Efter introduktionen måste företagsägaren göra en inledande konfiguration av programmet.
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# Programinställningar {#program-setup}

Efter introduktionen slutför företagsägaren den första konfigurationen av programmet, inklusive inställning av programbeskrivningen och definition av nyckeltal (KPI) som används för prestandatestning.

## Programinställningar med [!UICONTROL Cloud Manager] {#program-setup-cloud-manager}

Följ de här stegen för att konfigurera programmet och definiera KPI:er.

1. Logga in i Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välja lämplig organisation.

1. Klicka **Installationsprogram** för att starta installationsprocessen.

   ![Konfigurera program](/help/assets/set-up-program/setup1.png)

1. I **Installationsprogram** kan du ange programinformation på tre flikar:

   * **Allmänt**
   * **KPI**
   * **Provisionering**

1. På **Allmänt** lägger du till en beskrivning av programmet och överför en miniatyrbild genom att klicka på **Ändra foto**.

   ![Fliken Allmänt](/help/assets/Setup_Program-General.png)

1. På **KPI** kan du definiera dina KPI:er. I det här exemplet definieras separata KPI:er för **AEM Sites** och **AEM Assets**. Du kan ange nyckeltal för de produkter som du har licensierat.

   * Se avsnittet [KPI:er](#kpis) om du vill ha mer information om hur KPI:er mäts i Cloud Manager.

   ![Definiera KPI:er](/help/assets/Setup_Program-KPIs.png)

1. På **Provisionering** kan du definiera skalningsalternativen på begäran för dina miljöer om autoskalning är aktiverat för programmet.

   * Automatisk skalning gäller endast för produktionsmiljön och kanske inte är tillgängligt för alla kundprogram.

   ![Etableringsalternativ](/help/assets/Setup_Program-Provisioning.png)

1. Klicka **Spara** för att slutföra installationsguiden.

Ditt program kommer att skapas. Det kan ta flera minuter innan resurser etableras innan programmet är klart att användas.

## Redigera ett program {#editing-program}

Du kan redigera program när de har konfigurerats. Följ de här stegen för att redigera ett program.

1. Logga in i Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välja lämplig organisation.

1. Navigera till programmet från startskärmen i Cloud Manager.

1. Klicka på **Redigera program** för att uppdatera eller ändra programmet från **Översikt** sida.

   ![Redigera programalternativ](/help/assets/set-up-program/edit-program1.png)

1. The **Redigera program** visas så att du kan uppdatera programmet. Se avsnittet [Programinstallation med Cloud Manager](#program-setup-cloud-manager) för information om tillgängliga fält.

   ![Redigera programdialogruta](/help/assets/set-up-program/edit-program-general.png)

1. Klicka på **Uppdatera** för att spara ändringarna.

Observera att ändringarna sparas direkt i Cloud Manager, men kommer inte att återspeglas i dina miljöer förrän nästa pipeline-körning.

Om du ännu inte har skapat en pipeline kan du läsa dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurerar icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

## Växla mellan program {#swithing-programs}

När du arbetar med ett program kan du snabbt växla till ett annat program utan att gå tillbaka till översiktssidan för Cloud Manager.

Använd åtgärdsfältet för att växla till ett annat program, redigera det aktuella programmet eller lägga till ett nytt program.

![Programväljare](/help/assets/set-up-program/setup2.png)

## KPI:er {#kpis}

Platsens KPI:er mäts i tester som körs i mellanlagringsmiljön. Vanligtvis skalas dessa KPI:er ned för att passa funktionerna i mellanlagringsmiljön.

En användare som till exempel förväntar sig ett genomsnitt på 1 000 sidvisningar per minut i sin produktionsmiljö och har fyra dispatcher-/publiceringsservrar i produktion bör skala detta till 250 sidvisningar per minut. Detta förutsätter att deras mellanlagringsmiljö endast består av ett enda dispatcher-/publiceringsserverpar.

Resursprestandatestning utförs genom att resurser laddas upp upprepade gånger under en 30-minuters testperiod och att bearbetningstiden för varje tillgång samt olika mätvärden på systemnivå mäts.

Du kan ha ett leveransnätverk (CDN) som Akamai eller CloudFront framför produktionsmiljön. Sedan [!UICONTROL Cloud Manager] testerna direkt mot testmiljön bör KPI endast återspegla den trafik som förväntas passera genom CDN, det vill säga cacheminnet missar. Vanligtvis är detta en relativt liten del av den totala produktionstrafiken.

## Videoöversikt {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
