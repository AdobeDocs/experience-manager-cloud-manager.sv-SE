---
title: Viktiga begrepp
description: Precis som alla kraftfulla verktyg omfattar Cloud Manager många koncept och termer. I det här dokumentet sammanfattas några av de viktigaste för dig när du börjar använda Cloud Manager.
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Viktiga begrepp {#key-concepts}

Precis som alla kraftfulla verktyg omfattar Cloud Manager många koncept och termer. I det här dokumentet sammanfattas några av de viktigaste för dig när du börjar använda Cloud Manager.

## Program {#application}

Ett program är den uppsättning anpassningar och konfigurationer som skapas av en kund för att anpassa den underliggande [lösningen](#solution) (till exempel AEM Sites eller AEM Assets) för deras specifika användningsfall och behov. Ett program är en logisk enhet som kan bestå av flera [artefakter](#artifact).

Ett exempelprogram är det fiktiva [WKND-livsstilprogrammet](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview).

## Artefakt {#artifact}

En artefakt är en driftsättningsbar enhet och är resultatet av en byggprocess som omvandlar källkoden till en enda enhet. En ZIP-fil som innehåller källkoden.

## Artefaktarkiv {#artifact-repository}

En artefaktdatabas är en lagringsplats där kundspecifika [artefakter](#artifact) sparas och skyddas.

## Miljö {#environment}

En miljö är ett enda kluster med virtuella datorer i ett [program](#program). För AEM består den här miljön av en redigeringsinstans (eventuellt med en extra redigeringsinstans i kallt läge), noll eller flera publiceringsinstanser, en eller flera Dispatcher-instanser och en belastningsutjämnare.

## Git-databas {#git-repository}

En Git-databas är en plats där kundspecifik källkod lagras och är tillgänglig [med Git](https://git-scm.com).

## Instans {#instance}

En instans är en specifik virtuell server som kör AEM [solution](#solution). Förekomster representerar en enda logisk enhet från ett distributionsperspektiv.

## Organisation {#organization}

En organisation är en Adobe-konstruktion som representerar en företagskund. Ett företag kan ha flera organisationer beroende på hur de etablerades i Adobe Identity Management System (IMS).

## Pipeline {#pipeline}

En pipeline är en uppsättning distributionssteg som körs eller körs i följd.

## Produkt {#product}

En produkt är en specifik uppsättning funktioner i en [lösning](#solution) som licensieras av en organisation. Olika [program](#program) inom en organisation kan ha rätt till olika produktuppsättningar, till exempel AEM Sites, AEM Assets eller AEM Forms.

## Program {#program}

Ett program är en uppsättning miljöer som stöder en logisk gruppering av kundinitiativ, som vanligtvis motsvarar ett köpt servicenivåavtal (SLA). Varje program har exakt en produktionsmiljö och kan ha många icke-produktionsmiljöer.

## Lösning {#solution}

En lösning är en av Adobe [!UICONTROL Experience Cloud]-lösningarna. Exempel: Adobe Experience Manager, Adobe Target eller Adobe Analytics.

## Steg {#step}

Ett steg är en konfigurerad instruktionsuppsättning som utför en viss arbetsenhet som ett byggblock i en [pipeline](#pipeline).
