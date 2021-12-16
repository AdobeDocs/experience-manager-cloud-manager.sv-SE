---
title: Versionsinformation för 2021.10.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.10.0
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Versionsinformation för 2021.10.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] Version 2021.10.0.

>[!NOTE]
>Se [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) om du vill visa den senaste versionsinformationen för Cloud Manager på AEM as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] Version 2021.10.0 är 14 oktober 2021.

## Nyheter {#whats-new}

* Produktionspipelinjer kan nu köras i&quot;nödläge&quot;, vilket innebär att man slipper utföra säkerhets- och prestandatestningssteg vid driftsättning i nödsituationer.

* För enhetlighet med Cloud Service kommer befintliga distributionsledningar nu att refereras till och märkas i användargränssnittet som&quot;fullständigt stackade&quot;-pipelines.

* Pipelinekortet har uppdaterats så att det nu visas ett enda, integrerat ansikte som visar både pipelines för produktion och icke-produktion, och användaren kan välja Kör/Pausa/Fortsätt direkt på den åtgärdsmeny som är kopplad till varje pipeline.

* En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via gränssnittet.

* Lägg till och redigera rörliga upplevelser har uppdaterats för att nu använda välbekanta, moderna moduler.

* Användare av Cloud Manager kan nu skicka feedback direkt från användargränssnittet via **Feedback** överst till höger på landningssidan.

* Årliga SLA-diagram kan nu hämtas från användargränssnittet i Cloud Manager.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* API-dokumentationen för Cloud Manager innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Se [API-spelning för Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) för mer information.

* Verktygstipset på programkortet blir mer beskrivande om ett markeringsalternativ under Navigera till är inaktiverat. Nu står det&quot;En produktionsmiljö existerar inte&quot;.


## Felkorrigeringar {#bug-fixes}

* När data som lästs in från interna system inte matats in korrekt kan det leda till att orelaterade data från CSE inte återspeglas korrekt i Cloud Manager.

* I specifika kundsituationer ignorerades ogiltiga artefakter som hämtades under byggsteget och som skulle ha orsakat ett byggfel.
