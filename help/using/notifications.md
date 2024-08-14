---
title: Meddelanden
description: Läs om hur Cloud Manager meddelar dig om viktiga händelser.
exl-id: cfd5655f-2d2c-4304-b25c-6cdffe7ff64c
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Meddelanden {#notifications}

Läs om hur Cloud Manager meddelar dig om viktiga händelser.

## Meddelanden i Cloud Manager {#cloud-manager-notifications}

[!UICONTROL Cloud Manager] skickar meddelanden till dig när en produktionspipeline startar och slutförs (utan fel eller slutförs), i början av en produktionsdistribution och när stegen **Go-Live Approval** och **Scheduled** nås. Dessa meddelanden skickas via meddelandesystemet [!UICONTROL Experience Cloud].

>[!NOTE]
>
>Godkännandemeddelanden och schemalagda meddelanden skickas endast till användare i rollerna **Business Owner**, **Program Manager** och **Deployment Manager**.

Meddelandena visas i ett sidofält inom [!UICONTROL Cloud Manager] och i hela Adobe [!UICONTROL Experience Cloud].

Klockikonen i sidhuvudet visas när du har nya meddelanden.

![Aviseringsikon](/help/assets/notifications-bell-badged.png)

Klicka på klockikonen för att öppna sidofältet och visa meddelandena. Fliken **Meddelanden** i sidlisten innehåller de senaste meddelandena, till exempel distributionsbekräftelser. Meddelanden gäller dina miljöer.

![Sidofältet Meddelanden](/help/assets/notifications-activities.png)

Fliken **Meddelanden** innehåller produktmeddelanden från Adobe. Meddelanden gäller produkten.

![Sidofältet Meddelanden](/help/assets/notificaitons-announcements.png)

Klicka på ett meddelande eller meddelande för att visa information om det. Meddelanden som är kopplade till aktiviteter som pipeline-distributioner tar dig till detaljerna för den aktiviteten, som till exempel körningsfönstret för pipeline.

Klicka på alternativet **Visa alla** längst ned på panelen om du vill visa alla meddelanden i inkorgen.

Klicka på alternativet **Markera alla som lästa** längst ned på panelen om du vill markera alla olästa meddelanden som lästa och rensa klockikonens emblem.

## Meddelandekonfiguration {#configuration}

Du kan anpassa hur du tar emot meddelanden och vilka meddelanden du får.

Klicka på kugghjulsikonen högst upp i sidofältet för meddelanden.

![Ikon för meddelandeinställningar](/help/assets/notifications-configuration.png)

Detta öppnar fönstret **Experience Cloud-inställningar** där du kan definiera dina meddelandeprenumerationer och hur du får dina meddelanden.

### Prenumerationer {#subscriptions}

Prenumerationer definierar för vilka produkter du får meddelanden och vilka meddelanden.

![Meddelandeprenumerationer](/help/assets/notifications-subscriptions.png)

Som standard får du alla meddelanden för alla produkter. Klicka på **Anpassa** bredvid en produkt för att definiera de typer av meddelanden du får för den produkten.

![Anpassa prenumerationer](/help/assets/notifications-subscriptions-customize.png)

### Prioritet {#priority}

Prioritetsvarningar markeras med en **HIGH** -tagg och kan konfigureras så att de endast tas emot som aviseringar. I avsnittet **Prioritet** kan du definiera vilka kategorier som kvalificerar som prioritetsmeddelanden.

![Aviseringsprioritet](/help/assets/notifications-priority.png)

Använd listrutan för att lägga till i listan över kategorier som kvalificerar sig som prioritet. Klicka på X bredvid kategorinamnen för att ta bort dem.

### Varningar {#alerts}

Varningar visas i fönstrets övre högra hörn under några sekunder. Använd avsnittet **Varningar** för att definiera för vilka aviseringar du får.

![Aviseringar](/help/assets/notifications-alerts.png)

Du kan definiera hur varningarna ska fungera.

* **Visa aviseringar för** - Definierar de typer av meddelanden som utlöser aviseringar
* **Varningar ska finnas kvar på skärmen tills jag stänger av dem** - Anger om varningarna ska finnas kvar om du inte aktivt inaktiverar dem
* **Varaktighet** - Definierar hur länge varningen ska finnas kvar på skärmen om du inte har valt att de ska vara kvar på skärmen.

### E-post {#emails}

Meddelanden finns tillgängliga i webbanvändargränssnittet för alla [!UICONTROL Experience Cloud]-lösningar i Adobe. Du kan också välja att de här meddelandena ska skickas via e-post i avsnittet **E-post**.

![Meddelandemeddelanden](/help/assets/notifications-emails.png)

Inga e-postmeddelanden skickas som standard. Du kan välja att få e-post som:

* Direkt
* Dagligen
* Vecka

När **snabbmeddelanden** har valts skickas e-postmeddelanden omedelbart för varje meddelande. För **Daglig sammandrag** och **Veckosammandrag** kan du välja när din dagliga sammandrag ska skickas och på vilken dag och när veckosammandraget ska skickas.
