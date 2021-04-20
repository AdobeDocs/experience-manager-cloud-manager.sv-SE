---
title: Viktiga begrepp
seo-title: Viktiga begrepp
description: På den här sidan visas de nyckeltermer som är associerade med Cloud Manager.
seo-description: Följ den här sidan för att förstå de nyckeltermer som är associerade med Cloud Manager.
uuid: 2a37810b-98f8-4f01-90de-1e52c754ad16
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: b702dfc0-3534-4d90-af19-8559d8baf6a6
feature: Getting Started
level: Beginner
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Nyckelbegrepp {#key-concepts}

Den här sidan beskriver en del grundläggande terminologi som används i Cloud Manager. Vi rekommenderar att du läser den här sidan innan du granskar resten av Cloud Manager-dokumentationen.

**** ProgramDen uppsättning anpassningar och konfigurationer som skapas av en kund för att anpassa den underliggande lösningen efter deras specifika användningsfall och behov. Ett program är en logisk enhet som kan bestå av flera artefakter.

Till exempel *We.Retail*.

**Artefakt** En driftsättningsbar enhet. Resultatet av någon byggprocess som omvandlar källkoden till en enda enhet. En ZIP-fil som innehåller källkoden.

**Artefaktarkiv** En lagringsplats där kundspecifika artefakter sparas och skyddas.

**Miljö** Ett kluster med virtuella datorer i ett program. För AEM består detta av en författarinstans (eventuellt med ytterligare en författarinstans i kallt läge), noll eller flera publiceringsinstanser, en eller flera dispatcherinstanser och en belastningsutjämnare.

**Git** RepositoryEn plats där kundspecifik källkod lagras, tillgänglig via Git-protokollet.

**** InstanceEn specifik virtuell server som kör AEM. Förekomster representerar en enda logisk enhet från ett distributionsperspektiv.

**** OrganisationAdobe-konstruktioner som representerar en Enterprise-kund. Ett företag kan ha flera organisationer beroende på hur de ursprungligen etablerades i Adobe Identity Management System.

**PipelineEn** uppsättning distributionssteg som körs i följd.

**** ProduktEn specifik uppsättning funktioner i en lösning som licensierats av en organisation. Olika program inom en organisation kan ha rätt till olika produktuppsättningar. Exempel: Sites, Assets of Forms.

**Program** En uppsättning miljöer som stöder en logisk gruppering av kundinitiativ, som vanligtvis motsvarar ett köpt serviceavtal (SLA). Varje program har exakt en produktionsmiljö och kan ha många icke-produktionsmiljöer.

**** SolutionEn av Adobe:s  [!UICONTROL Experience Cloud] lösningar. Exempel: Adobe Experience Manager, Adobe Target eller Adobe Analytics.

**** StegEn konfigurerad instruktionsuppsättning som utför en viss arbetsenhet, byggstenar för en pipeline.
