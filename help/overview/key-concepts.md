---
title: Viktiga begrepp
description: Som med alla kraftfulla verktyg omfattar Cloud Manager många koncept och termer. I det här dokumentet sammanfattas några av de viktigaste för dig när du börjar använda Cloud Manager.
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 67621fb2dbb0c32371b2ffc16ec45f47daf04e05
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Viktiga begrepp {#key-concepts}

Som med alla kraftfulla verktyg omfattar Cloud Manager många koncept och termer. I det här dokumentet sammanfattas några av de viktigaste för dig när du börjar använda Cloud Manager.

## Program {#application}

Ett program är en uppsättning anpassningar och konfigurationer som skapas av en kund för att anpassa det underliggande [lösning](#solution) (t.ex. AEM Sites eller AEM Assets) för deras specifika användningsområden och behov. Ett program är en logisk enhet som kan bestå av flera [artefakter.](#artifact)

Ett exempelprogram är den fiktiva [WKND livsstilstillämpning.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

## Artefakt {#artifact}

En artefakt är en driftsättningsbar enhet och är resultatet av en byggprocess som omvandlar källkoden till en enda enhet. Till exempel en ZIP-fil som innehåller källkoden.

## Artefaktarkiv {#artifact-repository}

En artefaktdatabas är en lagringsplats där kundspecifika [artefakter](#artifact) sparas och skyddas.

## Miljö {#environment}

En miljö består av ett enda kluster av virtuella datorer i en [program.](#program) För AEM består detta av en redigeringsinstans (eventuellt med en extra redigeringsinstans i kallt läge), noll eller flera publiceringsinstanser, en eller flera dispatcherinstanser och en belastningsutjämnare.

## git-databas {#git-repository}

En Git-databas är en plats där kundspecifik källkod lagras och är tillgänglig [med git.](https://git-scm.com)

## Instans {#instance}

En instans är en specifik virtuell server som kör AEM [lösning.](#solution) Förekomster representerar en enda logisk enhet från ett distributionsperspektiv.

## Organisation {#organization}

En organisation är en Adobe-konstruktion som representerar en företagskund. Ett företag kan ha flera organisationer beroende på hur de etablerades i Adobe Identity Management System (IMS).

## Pipeline {#pipeline}

En pipeline är en uppsättning distributionssteg som körs i sekvens.

## Produkt {#product}

En produkt är en specifik uppsättning funktioner i en [lösning](#solution) licensieras av en organisation. Annat [program](#program) inom en organisation kan ha rätt till olika produktuppsättningar, till exempel AEM Sites, AEM Assets eller AEM Forms.

## Program {#program}

Ett program är en uppsättning miljöer som stöder en logisk gruppering av kundinitiativ, som vanligtvis motsvarar ett köpt servicenivåavtal (SLA). Varje program har exakt en produktionsmiljö och kan ha många icke-produktionsmiljöer.

## Lösning {#solution}

En lösning är en av Adobe [!UICONTROL Experience Cloud] lösningar. Exempel: Adobe Experience Manager, Adobe Target eller Adobe Analytics.

## Steg {#step}

Ett steg är en konfigurerad instruktionsuppsättning som fungerar som en byggsten i en [pipeline.](#pipeline)
