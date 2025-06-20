---
title: Utvärderingsfas
seo-title: Evaluation Phase
description: Läs om hur utvärderingsfasen i guiden för produktuppdatering bedömer uppgraderingskomplexiteten med mönsteridentifieraren.
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Utvärderingsfas {#evaluation}

Den första fasen i produktuppdateringsguiden är fasen **[!UICONTROL Evaluation]**. Mönsterdetektorn körs i guiden för att bedöma uppgraderingens komplexitet. I slutet av det här steget kan du visa utvärderingsrapporten.

Rapporten kontrollerar om författarinstansen är redo att uppgradera genom att identifiera mönster för följande:

* Regelfel i områden som påverkas eller skrivs över av uppgraderingen.
* Den använder AEM 6.x-funktioner eller API:er som inte är bakåtkompatibla och som kan brytas efter uppgraderingen.

Den här rapporten är en uppskattning av den utvecklingsinsats som krävs för att uppgradera till Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Mer information om mönsterdetektorn finns i [Utvärdera uppgraderingskomplexiteten med mönsterdetektorn](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/implementing/deploying/upgrading/pattern-detector).

## Kör utvärderingsrapporten {#running}

Mönsterdetektorn kan köras i alla miljöer. Men för att öka avkänningsfrekvensen och undvika flaskhalsar i affärskritiska instanser kör Cloud Manager programmet i utvecklingsmiljön i författarinstansen.

**Så här kör du utvärderingsrapporten:**

1. Starta guiden enligt beskrivningen i dokumentet [Produktuppdateringsguiden](/help/product-update-wizard/overview.md).

1. Klicka på **[!UICONTROL Run Evaluation]**.

   ![Kör utvärdering](/help/assets/Run-Evaluation.png)

1. Guiden informerar dig om åtgärdens status. Obs! **Pågår** eller **har slutförts** när utvärderingsrapporten genereras.

1. När rapporten har skapats kan du klicka på **[!UICONTROL Download report]** för att spara en kopia.

   ![Rapporten skapades](/help/assets/Evaluation-1.png)

Den aktuella produktuppdateringsguiden i Cloud Manager har endast stöd för **utvärderingsfasen**. De andra fyra faserna, **Reparation**, **Körning**, **Validering** och **Slutförande**, kommer snart.
