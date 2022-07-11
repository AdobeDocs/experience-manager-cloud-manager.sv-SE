---
title: Säkerhet och integritet
description: Läs mer om säkerhet och sekretess för din kod och dina artefakter i Cloud Manager.
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: d7751757c1d3bda3d60406a1d39cb41c61f5c863
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Säkerhet och integritet {#security-and-privacy}

Läs mer om säkerhet och sekretess för din kod och dina artefakter i Cloud Manager.

## Roller och behörigheter {#roles}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet.

Läs dokumentet om du vill veta mer om vilka roller du kan tilldela i Admin Console och behörigheter för användarroller [Rollbaserade behörigheter.](/help/requirements/role-based-permissions.md)

## Resursisolering {#resource-isolation}

[!UICONTROL Cloud Manager] kunderna behöver sina IMS-autentiseringsuppgifter för att autentisera som alla behörigheter som är kopplade till [!UICONTROL Cloud Manager] är knutna till sina IMS-organisationer. Under introduktionsprocessen ser provisioneringsteamet till att resursisolering används i [!UICONTROL Cloud Manager].

## Datasäkerhet {#data-security}

Kod i [!UICONTROL Cloud Manager] är krypterad i transit. Binärfiler som skapas i Cloud Manager krypteras också när de skickas och krypteras när de lagras.

Varje kund får sin egen Git-databas och koden är säker och inte delad med andra organisationer.

## Dataintegritet {#data-privacy}

[!UICONTROL Cloud Manager] följer de integritetsprinciper som definieras av Adobe. Utvecklare kan överföra kod säkert till Git-databaser via HTTPS.

[!UICONTROL Cloud Manager]Användargränssnittet byggs ovanpå tjänster som följer ett gemensamt styrramverk för Adobe som uppfyller kraven. [!UICONTROL Cloud Manager]Användargränssnittet använder säkra tjänster från flera molnleverantörer.
