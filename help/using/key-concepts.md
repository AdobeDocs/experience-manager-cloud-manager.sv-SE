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
translation-type: tm+mt
source-git-commit: aa4ff4eb2f3292fe4cb0baf8087b4d0213443cf4

---


# Viktiga begrepp {#key-concepts}

Den här sidan beskriver en del grundläggande terminologi som används i Cloud Manager. Vi rekommenderar att du läser den här sidan innan du granskar resten av Cloud Manager-dokumentationen.

**Tillämpning** Den uppsättning anpassningar och konfigurationer som skapas av en kund (eller deras anpassare) för att anpassa den underliggande lösningen efter deras specifika användningsfall och behov. Ett program är en logisk enhet som kan bestå av flera artefakter.

Till exempel *We.Retail*.

**Artefakt** En driftsättningsbar enhet. Resultatet av någon byggprocess som omvandlar källkoden till en enda enhet. En ZIP-fil som innehåller källkoden.

**Artefaktdatabas** En lagringsplats där kundspecifika artefakter sparas och skyddas.

**Miljö** Ett enda kluster med virtuella datorer i ett program. För AEM består detta av en författarinstans (eventuellt med en extra instans av en författare i kallt läge), noll eller flera publiceringsinstanser, en eller flera dispatcherinstanser och en belastningsutjämnare.

**Git-databas** En plats där kundspecifik källkod lagras, tillgänglig via Git-protokollet.

**Instans** En specifik virtuell server som kör AEM-lösningen. Förekomster representerar en enda logisk enhet från ett distributionsperspektiv.

**Organisationens** Adobe-konstruktion som representerar en Enterprise-kund. Ett företag kan ha flera organisationer beroende på hur de ursprungligen etablerades i Adobes system för identitetshantering.

**Pipeline** En uppsättning distributionssteg som körs i sekvens.

**Produkt** En specifik uppsättning funktioner i en lösning som licensierats av en organisation. Olika program i en organisation kan vara berättigade till olika produktuppsättningar. Exempel: Sites, Assets of Forms.

**Program** En uppsättning miljöer som stöder en logisk gruppering av kundinitiativ, som vanligtvis motsvarar ett inköpt serviceavtal (SLA). Varje program har exakt en produktionsmiljö och kan ha många icke-produktionsmiljöer.

**Lösning** En av Adobes [!UICONTROL Experience Cloud] lösningar. Exempel: Adobe Experience Manager, Adobe Target eller Adobe Analytics.

**Steg** En konfigurerad instruktionsuppsättning som utför en viss arbetsenhet, byggstenar för en pipeline.
