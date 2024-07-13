---
title: Programinställningar
description: Efter introduktionen måste företagsägaren göra en inledande konfiguration av programmet.
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Programinställningar {#program-setup}

Efter introduktionen slutför företagsägaren den första konfigurationen av programmet, inklusive inställning av programbeskrivningen och definition av nyckeltal (KPI) som används för prestandatestning.

## Programinställningar med [!UICONTROL Cloud Manager] {#program-setup-cloud-manager}

Följ de här stegen för att konfigurera programmet och definiera KPI:er.

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välj lämplig organisation.

1. Klicka på **Konfigurera program** för att starta installationsprocessen.

   ![Konfigurera program](/help/assets/set-up-program/setup1.png)

1. I dialogrutan **Setup Program** kan du ange programinformation på tre flikar:

   * **Allmänt**
   * **KPI**
   * **Etablerar**

1. Lägg till en beskrivning av programmet på fliken **Allmänt** och överför en miniatyrbild genom att klicka på **Ändra foto** om du vill.

   ![Fliken Allmänt](/help/assets/Setup_Program-General.png)

1. Definiera dina KPI:er på fliken **KPI**. I det här exemplet definieras separata KPI:er för **AEM Sites** och **AEM Assets**. Du kan ange nyckeltal för de produkter som du har licensierat.

   * Mer information om hur KPI:er mäts i Cloud Manager finns i avsnittet [KPI:er](#kpis).

   ![Definierar KPI:er](/help/assets/Setup_Program-KPIs.png)

1. På fliken **Provisioning** kan du definiera skalningsalternativ på begäran för dina miljöer om autoskalning är aktiverat för ditt program.

   * Automatisk skalning gäller endast för produktionsmiljön och kanske inte är tillgängligt för alla kundprogram.

   ![Etableringsalternativ](/help/assets/Setup_Program-Provisioning.png)

1. Klicka på **Spara** för att slutföra installationsguiden.

Ditt program kommer att skapas. Det kan ta flera minuter innan resurser etableras innan programmet är klart att användas.

## Redigera ett program {#editing-program}

Du kan redigera program när de har konfigurerats. Följ de här stegen för att redigera ett program.

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) och välj lämplig organisation.

1. Gå till programmet från Cloud Manager hemskärm.

1. Klicka på **Redigera program** för att uppdatera eller ändra programmet från sidan **Översikt**.

   ![Redigera programalternativ](/help/assets/set-up-program/edit-program1.png)

1. Dialogrutan **Redigera program** visas så att du kan uppdatera programmet. Mer information om tillgängliga fält finns i avsnittet [Programinställningar med Cloud Manager](#program-setup-cloud-manager).

   ![Dialogrutan Redigera program](/help/assets/set-up-program/edit-program-general.png)

1. Klicka på **Uppdatera** för att spara ändringarna.

Observera att ändringarna sparas direkt i Cloud Manager, men att de inte kommer att återspeglas i dina miljöer förrän nästa pipeline körs.

Om du ännu inte har skapat en pipeline läser du dokumenten [Konfigurera produktionsförlopp](/help/using/production-pipelines.md) och [Konfigurera icke-produktionsförlopp.](/help/using/non-production-pipelines.md)

## Växla mellan program {#swithing-programs}

När du arbetar med ett program kan du snabbt växla till ett annat program utan att gå tillbaka till Cloud Manager översiktssida.

Använd åtgärdsfältet för att växla till ett annat program, redigera det aktuella programmet eller lägga till ett nytt program.

![Programväljare](/help/assets/set-up-program/setup2.png)

## KPI:er {#kpis}

Platsens KPI:er mäts i tester som körs i mellanlagringsmiljön. Vanligtvis skalas dessa KPI:er ned för att passa funktionerna i mellanlagringsmiljön.

En användare som till exempel förväntar sig ett genomsnitt på 1 000 sidvisningar per minut i sin produktionsmiljö och har fyra dispatcher-/publiceringsservrar i produktion bör skala detta till 250 sidvisningar per minut. Detta förutsätter att deras mellanlagringsmiljö endast består av ett enda dispatcher-/publiceringsserverpar.

Assets prestandatestning görs genom att överföra resurser upprepade gånger under en 30-minuters testperiod och mäta bearbetningstiden för varje resurs samt olika mätvärden på systemnivå.

Du kan ha ett leveransnätverk (CDN) som Akamai eller CloudFront framför produktionsmiljön. Eftersom [!UICONTROL Cloud Manager] testar mot mellanlagringsmiljön direkt bör KPI endast återspegla den trafik som förväntas passera genom CDN, det vill säga, cacheminnet missar. Vanligtvis är detta en relativt liten del av den totala produktionstrafiken.

## Videoöversikt {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
