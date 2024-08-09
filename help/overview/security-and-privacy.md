---
title: Säkerhet och integritet
description: Läs mer om säkerhet och sekretess för kod och artefakter i Cloud Manager.
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Säkerhet och integritet {#security-and-privacy}

Läs mer om säkerhet och sekretess för kod och artefakter i Cloud Manager.

## Roller och behörigheter {#roles}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet.

Mer information om vilka roller du kan tilldela i Admin Console och användarrollbehörigheter finns i [Rollbaserade behörigheter](/help/requirements/role-based-permissions.md).

## Resursisolering {#resource-isolation}

[!UICONTROL Cloud Manager]-kunder behöver sina IMS-autentiseringsuppgifter för att autentisera eftersom alla behörigheter som är kopplade till [!UICONTROL Cloud Manager] är kopplade till deras IMS-organisationer. Under introduktionsprocessen ser provisioneringsteamet till att resursisolering används i [!UICONTROL Cloud Manager].

## Datasäkerhet {#data-security}

Koden i [!UICONTROL Cloud Manager] krypteras under överföring. Binärfiler som Cloud Manager bygger krypteras också när de skickas och krypteras när de lagras.

Varje kund får sin egen Git-databas och koden är säker och inte delad med andra organisationer.

## Dataintegritet {#data-privacy}

[!UICONTROL Cloud Manager] följer de integritetsprinciper som definieras av Adobe. Utvecklare kan överföra kod säkert till Git-databaser via HTTPS.

Användargränssnittet för [!UICONTROL Cloud Manager] är byggt på tjänster som följer ett gemensamt kontrollramverk för Adobe som uppfyller kraven. Användargränssnittet för [!UICONTROL Cloud Manager] använder säkra tjänster från flera molnleverantörer.
