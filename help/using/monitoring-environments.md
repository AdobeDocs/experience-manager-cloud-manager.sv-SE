---
title: Övervakningsmiljöer
description: Lär dig övervaka dina miljöer i Cloud Manager.
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---


# Övervakningsmiljöer {#monitoring-environments}

Lär dig övervaka dina miljöer i Cloud Manager.

## Måtttrösklar {#thresholds}

Systemövervakning i [!UICONTROL Cloud Manager] görs genom att observera de enskilda instanserna i en miljö och spåra en mängd mätvärden för varje instans. Varje mätvärde har två definierade tröskelvärden: ett tröskelvärde för varning och ett kritiskt tröskelvärde.

Om ett mätvärde överstiger dess kritiska tröskelvärde anses det vara i ett kritiskt tillstånd. Om ett mätvärde överskrider varningströskeln (men under det kritiska tröskelvärdet) anses det vara i ett varningstillstånd. Tröskelvärdena anges av Adobe Managed Services och kan visas i [!UICONTROL Cloud Manager]. I de flesta fall är tröskelvärdena desamma för kunderna, men det finns fall där Adobe Managed Services kommer att ändra tröskelvärdena för att matcha specifika kundkrav. Frågor om tröskelvärdena ska ställas till din Customer Success Engineer (CSE).

## Åtkomst till systemövervakning {#accessing-system-monitoring}

Följ de här stegen för att få åtkomst till systemövervakning.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välj rätt organisation och program.

1. Klicka på ellipsknappen för programmet som du vill övervaka och välj alternativet **Visa övervakning**.

   ![Inställningar](/help/assets/first-timea1.png)

Sidan **Rapporter** öppnas och visar information om systemövervakning.

## Systemövervakning - översikt {#system-monitoring-overview}

Avsnittet **Systemövervakning** på sidan **Rapporter** visar de övervakade miljöerna i programmet och rapporterar om deras hälsa på hög nivå i fyra olika kategorier:

* Värd
* Lagring
* Nätverk
* Program

Statusen i varje kategori är en sammanfattning av enskilda mätvärden. Om något av mätvärdena i en kategori är i kritiskt tillstånd, är hela kategorin i ett kritiskt tillstånd för syftet med översiktssidan. Samma sammanfattning kan visas på miljönivå och instansnivå.

![Systemövervakning - översikt](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>Som standard visas instanser av produktionsmiljön när du navigerar till den här sidan, men även andra miljöer kan visas.

## Information om systemövervakning {#system-monitoring-detail}

Om du vill visa information om specifika mått klickar du på en av kategorikolumnerna för en viss instans eller på kategorititeln i den vänstra navigeringen. På varje detaljsida visas en serie diagram för måtten i den kategorin. Du kan antingen visa mätvärden för alla instanser i en miljö eller för en viss instans. Du kan växla mellan miljö och instanser med listrutorna i det övre högra hörnet.

![Välj miljö](/help/assets/System_Monitoring1.png)

Navigeringen till vänster visar tillgängliga mätvärden i den valda kategorin som det finns data för den valda miljön och instanser för.

Ett enskilt diagram visar status och ett diagram över data över tiden tillsammans med tröskelvärdena. Om flera instanser visas kommer varje instans data att finnas i en separat serie.

![Mätdiagram](/help/assets/Monitoring_Graphs1.png)

Du kan dölja enskilda serier i ett diagram genom att klicka på serien i teckenförklaringen.
Om du till exempel klickar på varningströskelserien visas bara det kritiska tröskelvärdet.

![Ändra diagram](/help/assets/Monitoring_Graphs2.png)

### Måttdefinitioner {#metric-definitions}

#### Värd {#host}

* **Inläsning per kärna**: Det genomsnittliga antalet processer som körs av processorn eller befinner sig i vänteläge under en (load1), fem (load5) och femton (load15) minutersperiod.
* **Antal processer**: Antal öppna processer
* **Antal användare**: Antalet användare med en aktiv gränssnittssession
* **Minnesanvändning**: Procentandel av systemminnet som för närvarande är allokerat
* **JVM-minne**: Storleken (i megabyte) på den allokerade Java-heap
* **Gammalt generationsutrymme**: Procentandel av JVM-gammalt genereringsminne som för närvarande allokeras

#### Nätverk {#network}

* **CQ-portkontroll**: Svarstiden i sekunder för åtkomst till AEM- eller Dispatcher-porten
   * Det finns olika mätvärden för författare, publicering och skickare.

#### Lagring {#storage}

* **Diskutrymme**: Använt diskutrymme (i MB) för varje monteringspunkt på värden
   * Det finns olika mätvärden för varje monteringspunkt.
   * Det finns åtminstone mått för `/` och `/mnt`, men det kan finnas ytterligare värden för monteringspunkter beroende på den specifika instanskonfigurationen.
* **Mappstorlek**
* **AEM Segmentarkiv**: Använt diskutrymme (i gigabyte) för AEM segmentarkiv

#### Program {#application}

* **Replikeringsagent**: Tiden (i sekunder) för en testreplikeringshändelse
   * Det finns olika mått för varje replikeringsagent.
* **Dispatcher Flush**: Antalet objekt som för närvarande finns i tömningskön för dispatcher

## SLA-rapportering {#sla-reporting}

Du kan se hur väl din AEM presterar i förhållande till ditt avtalade servicenivåavtal (SLA).

I följande diagram visas SLA månatliga resultat för 2019.

![SLA 2018-diagram](/help/assets/SLA-Reports-one.png)

Precis som med diagram för systemövervakning visar en rullande datapunkt de specifika värdena för den månaden.

![Datapunktsöverrullning](/help/assets/SLA-Reports-two.png)

Avsnittet **Händelseanalys** i det här diagrammet visar den uppsättning incidenter som har inträffat för programmet under det valda året. Varje incident har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Händelseanalys](/help/assets/sla-reporting3.png)

## SLA Metrics {#sla-metrics}

* **Författarkontrakt**: Detta är den SLA som definieras i ditt avtal med Adobe Managed Services för författarnivån.
* **AMS Author SLA**: Detta är den uppmätta drifttiden för produktionsförfattarens factoring-incidenter som orsakas av Adobe eller våra leverantörer.
* **Författare av SLA**: Detta är den uppmätta drifttiden för författarnivån som ignorerar schemalagda driftavbrott, t.ex. underhållsperioder.
* **Slutanvändaravtal**: Detta är den SLA som definieras i ditt avtal med Adobe Managed Services för publiceringsnivån.
* **AMS-slutanvändare SLA**: Detta är den uppmätta drifttiden för de factoringincidenter i produktionsskiktet som orsakas av Adobe eller våra leverantörer.
* **Slutanvändare SLA**: Det här är den uppmätta drifttiden för publiceringsskiktet som ignorerar schemalagda driftstopp, till exempel underhållsfönster.

## Videosjälvstudie {#video-tutorial}

I den här videon får du en översikt över hur du använder diagram från Cloud Manager Reports för en genomgång av dina programmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
