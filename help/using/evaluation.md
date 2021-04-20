---
title: Utvärdering
seo-title: Utvärdering
description: 'Den här sidan fungerar som en startpunkt för utbildningsfasen i produktuppdateringsguiden. '
seo-description: Den här sidan fungerar som en startpunkt för utbildningsfasen i produktuppdateringsguiden.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Utvärderingsfas {#evaluation}

Den första fasen i produktuppdateringsguiden är **[!UICONTROL Evaluation]**-fasen.
Här kan du bedöma uppgraderingens komplexitet med mönsterdetektorn som du kan nå direkt från guiden. Efter det här steget har du tillgång till utvärderingsrapporten.

I den genererade rapporten kan du kontrollera om Author-instansen har uppgraderat genom att identifiera mönster som:

* Brott mot vissa regler och görs i områden som kommer att påverkas eller skrivas över av uppgraderingen.

* Använd en AEM 6.x-funktion eller ett API som inte är bakåtkompatibelt på den nya AEM och som kan brytas efter uppgraderingen.

Detta är en bedömning av den utvecklingsinsats som ingår i uppgraderingen till Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Mer information om mönsteravkännare finns i [Utvärdera uppgraderingskomplexiteten med mönsteravkännaren](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## Köra utvärderaren {#running-evaluator}

Följ stegen nedan för att generera en utvärderingsrapport:

1. Klicka på **[!UICONTROL Run Evaluation]**.

   >[!NOTE]
   >
   >Mönsterdetektorn kan köras i alla miljöer. För att öka avkänningshastigheten och undvika flaskhalsar i affärskritiska instanser körs den i testmiljön på författarinstansen.

   ![](assets/Run-Evaluation.png)

1. Guiden informerar dig om åtgärdens status. Du kommer att lägga märke till **Pågår** eller **slutförd** som tillämpligt när utvärderingsrapporten genereras.

   När rapporten har skapats kan du klicka på **[!UICONTROL Download report]** för att spara en kopia.

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >Den aktuella versionen av produktuppdateringsguiden i Cloud Manager stöder endast fasen **Evaluation**. Övriga fyra faser, som **Reparation**, **Körning**, **Verifiering** och **Slutförande**, kommer snart.
