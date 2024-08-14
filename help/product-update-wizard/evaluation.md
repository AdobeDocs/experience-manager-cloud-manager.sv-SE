---
title: Utvärderingsfas
seo-title: Evaluation Phase
description: Läs om hur utvärderingsfasen i Product Update Wizard bedömer uppgraderingskomplexiteten med mönsterdetektorn.
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Utvärderingsfas {#evaluation}

Den första fasen i produktuppdateringsguiden är **[!UICONTROL Evaluation]**-fasen, som utvärderar uppgraderingskomplexiteten med mönsterdetektorn direkt i guiden. Efter det här steget har du tillgång till en utvärderingsrapport.

I den genererade rapporten kan du kontrollera om författarinstansen är berättigad till en uppgradering genom att identifiera mönster som:

* Brott mot vissa regler om områden som kommer att påverkas eller skrivas över av uppgraderingen.

* Använd en AEM 6.x-funktion eller ett API som inte är bakåtkompatibelt med den nya versionen av AEM och som kan brytas efter uppgraderingen.

Rapporten är en bedömning av den utvecklingsinsats som ingår i uppgraderingen till Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Mer information om mönsteridentifierare finns i [Utvärdera uppgraderingskomplexiteten med mönsterdetektorn](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=en).

## Kör utvärderingsrapporten {#running}

Mönsterdetektorn kan köras i alla miljöer. För att öka avkänningsfrekvensen och undvika flaskhalsar i affärskritiska instanser kommer Cloud Manager att köra programmet i utvecklingsmiljön för den som skapat instansen.

**Så här kör du utvärderingsrapporten:**

1. Starta guiden enligt beskrivningen i dokumentet [Produktuppdateringsguiden](/help/product-update-wizard/overview.md).

1. Klicka på **[!UICONTROL Run Evaluation]**.

   ![Kör utvärdering](/help/assets/Run-Evaluation.png)

1. Guiden informerar dig om åtgärdens status. Obs! **Pågår** eller **har slutförts** när utvärderingsrapporten genereras.

1. När rapporten har skapats kan du klicka på **[!UICONTROL Download report]** för att spara en kopia.

   ![Rapporten skapades](/help/assets/Evaluation-1.png)

Den aktuella versionen av produktuppdateringsguiden i Cloud Manager har endast stöd för **utvärderingsfasen**. De andra fyra faserna, **Reparation**, **Körning**, **Validering** och **Slutförande**, kommer snart.
