---
title: Versionsinformation för 2021.7.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.7.0
feature: Versionsinformation
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# Versionsinformation för 2021.7.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.7.0.

>[!NOTE]
>Se [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) för att se den senaste versionsinformationen för Cloud Manager i AEM som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.7.0 är 15 juli 2021.
Nästa version är planerad till den 12 augusti 2021.

## Nyheter {#whats-new}

* Kunderna kan nu använda Azul 8 och 11 JDK:er för sina Cloud Manager-byggprocesser och kan antingen välja att använda en av dessa JDK:er för verktygskedjor-kompatibla Maven-plugins *eller* hela Maven-processkörningen.

* IP för utgående utgång loggas nu i loggfilen för byggsteget.

* Knapparna Hantera Git har fått namnet Åtkomst till Git-information och dialogrutan har uppdaterats visuellt.

* Vissa oväntade omkonfigurationer av topologin kan leda till att detaljerade testrapporter inte längre är tillgängliga från informationssidan för pipeline-körning.

## Felkorrigeringar {#bug-fixes}

* Manuell navigering till sidan med körningsinformation för en körning som inte finns visade inte på något fel, bara en oändlig inläsningsskärm.

* I vissa fall kommer det automatiska återförsöket för misslyckade behållare som används i platsprestanda inte att börja gälla på 2 timmar, vilket resulterar i ett testfel.

## Kända fel {#known-issues}

Kunder som byter till Azul JDK bör vara medvetna om att inte alla befintliga program kompileras utan fel i Azul JDK. Vi rekommenderar att du testar lokalt innan du byter.