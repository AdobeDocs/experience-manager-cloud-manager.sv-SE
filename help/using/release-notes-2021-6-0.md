---
title: Versionsinformation för 2021.6.0
description: Följ den här sidan för att få information om Cloud Manager version 2021.6.0
feature: Versionsinformation
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Versionsinformation för 2021.6.0 {#release-notes-for}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!UICONTROL Cloud Manager] version 2021.6.0.

>[!NOTE]
>Se [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) för att se den senaste versionsinformationen för Cloud Manager i AEM som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2021.6.0 är 10 juni 2021.
Nästa version är planerad till 15 juli 2021.

## Nyheter {#whats-new}

* Resurs- och platstesterna kommer nu att köras parallellt (när det är tillämpligt), vilket minskar den totala körningstiden för pipeline. Den här funktionen kommer att aktiveras för kunderna under de kommande veckorna.

* Maven Dependencies som laddas ned under byggfasen cachelagras nu mellan pipeline-körningar. Den här funktionen kommer att aktiveras för kunderna under de kommande veckorna.

* Det standardförgreningsnamn som används både när projektet skapas och i det förvalda push-kommandot via Hantera Git-arbetsflöden har ändrats till `main`.

* Redigera programupplevelser i användargränssnittet har uppdaterats. Mer information finns i [Redigera ett program](/help/using/setting-up-program.md#editing-program).

* Kvalitetsregeln `ImmutableMutableMixCheck` har uppdaterats för att klassificera `/oak:index`-noder som oföränderliga.

* Kvalitetsreglerna `CQBP-84` och `CQBP-84--dependencies` har konsoliderats till en enda regel. Som en del av den här konsolideringen identifierar genomsökningen av beroenden mer korrekt problem i tredjepartsberoenden som distribueras till AEM.

* I vissa situationer kan en misslyckad beräkning av mätvärdet för överhoppade tester leda till att pipeline-körningar misslyckas.

## Felkorrigeringar {#bug-fixes}

* JCR-noddefinitioner som innehåller en ny rad efter att rotelementnamnet inte tolkades korrekt.

* API för listdatabaser filtrerar inte borttagna databaser.

* Ett felaktigt felmeddelande visades när ett ogiltigt värde angavs för schemasteget.

* I vissa fall när pipelinekörningen nådde steget Distribuera till produktionssteg och användaren stoppar körningen, visade statusmeddelandet för distributionen i användargränssnittet inte vad som faktiskt hände.