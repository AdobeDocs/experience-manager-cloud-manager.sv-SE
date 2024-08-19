---
title: Utvärderingsfas
seo-title: Evaluation Phase
description: Läs om hur utvärderingsfasen i guiden för produktuppdatering bedömer uppgraderingskomplexiteten med mönsteridentifieraren.
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: 11a6a53d8cbfb689810a9a8e7d82293a49863084
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Utvärderingsfas {#evaluation}

Den första fasen i produktuppdateringsguiden är fasen **[!UICONTROL Evaluation]**, som utvärderar uppgraderingskomplexiteten med mönsterdetektorn direkt i guiden. Efter det här steget kan du öppna utvärderingsrapporten.

Med den genererade rapporten kan du kontrollera om författarinstansen är berättigad till en uppgradering genom att identifiera följande mönster:

* Bryt vissa regler för områden som påverkas eller skrivs över av uppgraderingen.

* Använd en AEM 6.x-funktion eller ett API som inte är bakåtkompatibelt med den nya versionen av AEM och som kan brytas efter en uppgradering.

Rapporten är en bedömning av den utvecklingsinsats som ingår i uppgraderingen till Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Mer information om mönsterdetektorn finns i [Utvärdera uppgraderingskomplexiteten med mönsterdetektorn](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/upgrading/pattern-detector).

## Kör utvärderingsrapporten {#running}

Mönsterdetektorn kan köras i alla miljöer. Men för att öka avkänningsfrekvensen och undvika flaskhalsar i affärskritiska instanser kör Cloud Manager programmet i utvecklingsmiljön i författarinstansen.

**Så här kör du utvärderingsrapporten:**

1. Starta guiden enligt beskrivningen i dokumentet [Produktuppdateringsguiden](/help/product-update-wizard/overview.md).

1. Klicka på **[!UICONTROL Run Evaluation]**.

   ![Kör utvärdering](/help/assets/Run-Evaluation.png)

1. Guiden informerar dig om åtgärdens status. Obs! **Pågår** eller **har slutförts** när utvärderingsrapporten genereras.

1. När rapporten har skapats kan du klicka på **[!UICONTROL Download report]** för att spara en kopia.

   ![Rapporten skapades](/help/assets/Evaluation-1.png)

Den aktuella versionen av produktuppdateringsguiden i Cloud Manager har endast stöd för **utvärderingsfasen**. De andra fyra faserna, **Reparation**, **Körning**, **Validering** och **Slutförande**, kommer snart.
