---
title: Uppdateringar av Service Pack för utvecklingsmiljöer - tidig Adobe
description: Läs om hur du nu kan initiera uppdateringspaket för utvecklingsmiljöer via Cloud Manager användargränssnitt.
hide: true
hidefromtoc: true
exl-id: 996a8eee-843f-45a6-8f7a-31ea405c2b32
source-git-commit: 55b33db1bf80f066b1a66bc87c0abeefa4771871
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Uppdateringar av Service Pack för utvecklingsmiljöer (tidig Adobe) {#stage-prod-only}

Lär dig hur du kan initiera Service Pack-uppdateringar för utvecklingsmiljöer via Cloud Manager användargränssnitt.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet](/help/release-notes/current.md#early-adoption).

## Ökning {#service-pack-updates-overview}

Du kan initiera Service Pack-uppdateringar för utvecklingsmiljöer via Cloud Manager användargränssnitt. Med den här funktionen kan du söka efter tillgängliga Service Pack-uppdateringar och hantera installationsprocessen separat.

**Viktiga fördelar**

* Ger bättre kontroll över uppdateringarna av Cloud Manager Service Pack.
* Minskar beroendet av Adobe Customer Success Engineers (CSE) för att initiera uppdateringar.
* Spårar hela uppdateringsprocessen via Cloud Manager.

**Aktuella begränsningar**

* Alternativet för självbetjäningsuppdatering är bara tillgängligt för utvecklingsmiljöer.
* Begränsad felrapportering finns tillgänglig för misslyckade uppdateringar.
* Om det uppstår problem måste du kontakta Adobe CSE för ytterligare utredning.

## Initiera en Service Pack-uppdatering

1. Logga in på Cloud Manager med behörighet för Distributionshanteraren.
1. Gå till sidan Programöversikt.
1. Klicka på ikonen ![Mer, ellips](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), under avsnittet Miljöer.

   ![Sök efter Service Pack-uppdatering i listruta](/help/using/assets/service-pack-check-for-updates.png)

1. I listrutan klickar du på ![Öppna i ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_OpenInLight_18_N.svg) **Sök efter uppdateringar** för att söka efter tillgängliga uppdateringspaket.

   ![En lista över tillgängliga uppdateringar visas](/help/using/assets/service-pack-versions.png)

1. Klicka på önskad Service Pack-version i listan.
1. Klicka på **Uppdatera Service Pack** för att starta uppdateringsprocessen.
1. Granska informationen i bekräftelsedialogrutan och bekräfta uppdateringen.

   När installationsprocessen har bekräftats startar den och förloppet kan spåras i Cloud Manager.

## Spåra uppdateringen av Service Pack

När du har initierat uppdateringen kan du övervaka förloppet på Cloud Manager aktivitetssida.

**Så här spårar du uppdateringen av Service Pack:**

1. Navigera till aktivitetssidan från Cloud Manager-kontrollpanelen.
1. Leta efter installationsposten för Service Pack.

   ![Service Pack-installationer](/help/using/assets/service-pack-installation.png)

1. Klicka på posten för att visa detaljerade förlopps- och statusuppdateringar som liknar följande:

   ![Förlopp för installation av Service Pack](/help/using/assets/service-pack-progression.png)

### Felsöka installationsfel

* Om installationen misslyckas utlöser Cloud Manager automatiskt en återställning till föregående läge.
* Om problemet kvarstår klickar du på **Hämta logg** för att samla in felloggar och kontaktar sedan Adobe support för felsökning.

## Godkänn eller avvisa Service Pack-körningen

När installationen är klar måste du godkänna (eller avvisa) för att slutföra uppdateringen.

**Så här godkänner eller avvisar du körningen av Service Pack:**

1. Öppna aktivitetssidan i Cloud Manager.
1. Leta reda på den väntande godkännandebegäran för uppdateringen av Service Pack.

   ![Avvisa eller godkänn uppdateringen av Service Pack](/help/using/assets/service-pack-reject-approve.png)

1. Gör något av följande:

   * Slutför uppdateringen genom att klicka på **Godkänn**.

   ![Godkännande av Service Pack](/help/using/assets/service-pack-approve.png)

   * Om du vill avbryta uppdateringen klickar du på **Avvisa**.
Service Pack-installationen avbryts och inga ändringar görs.

   ![Avvisning av Service Pack](/help/using/assets/service-pack-reject.png)
