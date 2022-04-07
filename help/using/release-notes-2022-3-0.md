---
title: Versionsinformation för 2022.3.0
description: Detta är versionsinformationen för Cloud Manager version 2022.3.0.
feature: Release Information
source-git-commit: f1d359921a11ab8a6117a15cd5eb72362bbb8360
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager version 2022.3.0 {#release-notes}

Den här sidan dokumenterar versionsinformationen för [!UICONTROL Cloud Manager] version 2022.3.0.

>[!NOTE]
>
>Information om den senaste utgåvan av Cloud Manager på AEM as a Cloud Service finns i [Cloud Manager i AEM as a Cloud Service versionsinformation.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2022.3.0 är 10 mars 2022. Nästa version är planerad till den 7 april 2022.

## Nyheter {#what-is-new}

* Utanför HTTP-begäranden från tillgångstester kommer nu från ett fast IP-intervall.


## Felkorrigeringar {#bug-fixes}

* The **Hoppa över ändringar i belastningsutjämnaren** det gick inte att inaktivera alternativet.
* The **Hoppa över ändringar i belastningsutjämnaren** alternativet visades inte på AMS Dev Deploy **Redigera pipeline-arbetsflöde**.
* En delmängd av Git-databaser som skapats manuellt hade ett felaktigt namnvärde, vilket hindrade återanvändningsfunktionen för build-felaktigheter från att vara effektiv. Namnen på dessa databaser har ändrats och användarna ser det korrigerade namnet i Cloud Manager API/UI.
* Artefakter från rörledningar som inte är avsedda för produktion återanvänds på ett olämpligt sätt i rörledningar för hela produktionen.
* När du lägger till eller redigerar en pipeline för kodkvalitet visas inte längre alternativen för att hantera måttfel.
* En del oväntade pipelinevariabelkonfigurationer kan orsaka i byggsteget.
