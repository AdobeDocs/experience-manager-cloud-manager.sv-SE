---
title: Säkerhet och integritet
seo-title: Säkerhet och integritet för AEM Cloud Manager
description: Följ den här sidan om du vill veta mer om säkerhet och sekretess för dina resurser (kod/artefakter).
seo-description: Följ den här sidan om du vill veta mer om säkerhet och sekretess för dina resurser (kod/artefakter) med AEM Cloud Manager.
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: Komma igång
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Säkerhet och sekretess {#security-and-privacy}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. I det här avsnittet beskrivs säkerheten och sekretessen för dina resurser (kod/artefakter) med AEM Cloud Manager. Dessutom har [!UICONTROL Cloud Manager] förkonfigurerade roller med lämplig behörighet.

Mer information om vilka roller du kan tilldela i Admin Console och användarrollbehörigheter finns i [Rollbaserade behörigheter](/help/using/role-based-permissions.md).


## Resursisolering {#resource-isolation}

Kunder som använder [!UICONTROL Cloud Manager] behöver sina IMS-autentiseringsuppgifter för att autentisera eftersom alla behörigheter som är kopplade till [!UICONTROL Cloud Manager] kommer att konfigureras och kopplas till deras IMS-organisation. Under introduktionsprocessen ser provisioneringsteamet till att resursisolering används i [!UICONTROL Cloud Manager].

## Datasäkerhet {#data-security}

Kod i [!UICONTROL Cloud Manager] krypteras under överföring. Binärfiler som skapas i Cloud Manager krypteras också när de skickas och krypteras när de lagras.

Varje kund får sin egen **Git-databas** och koden är säker och inte delad med andra **organisationer**.

## Dataintegritet {#data-privacy}

[!UICONTROL Cloud Manager] följer de integritetsprinciper som definieras av Adobe. Utvecklare skickar kod säkert till **Git-databasen** via HTTPS.

Användargränssnittet (UI) för [!UICONTROL Cloud Manager] är baserat på tjänster som uppfyller ett gemensamt kontrollramverk som definieras av Adobe. Användargränssnittet för [!UICONTROL Cloud Manager] använder säkra tjänster från flera molnleverantörer.
