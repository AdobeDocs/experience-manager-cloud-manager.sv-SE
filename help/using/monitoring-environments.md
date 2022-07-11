---
title: Övervakningsmiljöer
description: Lär dig hur du övervakar dina miljöer i Cloud Manager.
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Övervakningsmiljöer {#monitoring-environments}

Lär dig hur du övervakar dina miljöer i Cloud Manager.

## Måtttrösklar {#thresholds}

Systemövervakning i [!UICONTROL Cloud Manager] gör du genom att observera de enskilda instanserna i en miljö och spåra en mängd olika mätvärden för varje instans. Varje mätvärde har två definierade tröskelvärden: ett tröskelvärde för varning och ett kritiskt tröskelvärde.

Om ett mätvärde överstiger dess kritiska tröskelvärde anses det vara i ett kritiskt tillstånd. Om ett mätvärde överskrider varningströskeln (men under det kritiska tröskelvärdet) anses det vara i ett varningstillstånd. Tröskelvärdena fastställs av Adobes hanterade tjänster och kan visualiseras i [!UICONTROL Cloud Manager]. I de flesta fall är tröskelvärdena olika för olika kunder, men det finns fall där Adobes hanterade tjänster ändrar tröskelvärdena så att de matchar specifika kundkrav. Frågor om tröskelvärdena ska ställas till din Customer Success Engineer (CSE).

## Åtkomst till systemövervakning {#accessing-system-monitoring}

Följ de här stegen för att komma åt systemövervakning.

1. Logga in på **Managed Services - program** landningssida.

   ![Program för hanterade tjänster](/help/assets/ProgramLanding.png)

1. Klicka på den fjärde ikonen på programkortet.

   ![Inställningar](/help/assets/first-timea1.png)


Du kan även navigera till **Systemövervakning** landningssida genom **Rapporter** globalt navigeringsmenyalternativ i [!UICONTROL Cloud Manager].

## Systemövervakning - översikt {#system-monitoring-overview}

På sidan Översikt över systemövervakning visas de övervakade miljöerna i programmet och rapporter om deras hälsa på hög nivå i fyra olika kategorier:

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

Om du vill visa information om specifika mått kan du antingen klicka på en av kategorierna i den vänstra navigeringen eller klicka på en av kategoriindikatorerna för en viss instans. På varje detaljsida visas en serie diagram för måtten i den kategorin. Du kan antingen visa mätvärden för alla instanser i en miljö eller för en viss instans. Du kan växla mellan miljö och instanser med listrutorna i det övre högra hörnet.

![Välj miljö](/help/assets/System_Monitoring1.png)

Navigeringen till vänster visar tillgängliga mätvärden i den valda kategorin som det finns data för den valda miljön och instanser för.

![Övervakningsmått](/help/assets/System_Monitoring2.png)

Ett enskilt diagram visar status och ett diagram över data över tiden tillsammans med tröskelvärdena. Om flera instanser visas kommer varje instans data att finnas i en separat serie.

![Mätdiagram](/help/assets/Monitoring_Graphs1.png)

Du kan dölja enskilda serier i ett diagram genom att klicka på serien i teckenförklaringen.
Om du till exempel klickar på varningströskelserien visas bara det kritiska tröskelvärdet.

![Ändra diagram](/help/assets/Monitoring_Graphs2.png)

### Måttdefinitioner {#metric-definitions}

#### Värd {#host}

* **Belastning per kärna**: Antalet processer som körs av processorn eller som befinner sig i vänteläge är i genomsnitt över en (load1), fem (load5) och femton (load15) minutersperiod
* **Antal processer**: Antal öppna processer
* **Antal användare**: Antalet användare med en aktiv gränssnittssession
* **Minnesanvändning**: Procentandel av systemminnet som för närvarande är allokerat
* **JVM-minne**: Storleken (i megabyte) på det allokerade Java-heap
* **Gammalt generationsutrymme**: Procentandel av JVM-gammalt genereringsminne som för närvarande allokeras

#### Nätverk {#network}

* **CQ-portkontroll**: Svarstiden i sekunder för åtkomst till AEM- eller Dispatcher-porten
   * Det finns olika mätvärden för författare, publicering och skickare.

#### Lagring {#storage}

* **Diskutrymme**: Det använda diskutrymmet (i megabyte) för varje monteringspunkt på värden
   * Det finns olika mätvärden för varje monteringspunkt.
   * Det finns åtminstone mått för `/` och `/mnt`, men ytterligare monteringspunktsmått kan vara tillgängliga beroende på den specifika instanskonfigurationen.
* **Mappstorlek**
* **AEM segmentarkiv**: Använt diskutrymme (i gigabyte) för AEM segmentarkiv

#### Program {#application}

* **Replikeringsagent**: Tiden (i sekunder) för en testreplikeringshändelse
   * Det finns olika mått för varje replikeringsagent.
* **Dispatcher Flush**: Antalet objekt som för närvarande finns i kön för rensning av dispatcher

## SLA-rapportering {#sla-reporting}

Kunderna kan se hur väl deras AEM presterar jämfört med deras avtalade serviceavtal (SLA). Det här är tillgängligt via en undermeny på **Rapporter** skärm.

I följande diagram visas månatlig SLA-uppnående för 2018.

![SLA 2018-diagram](/help/assets/SLA-Reports-one.png)

Precis som med diagram för systemövervakning visar en rullande datapunkt de specifika värdena för den månaden.

![Datapunktens överrullning](/help/assets/SLA-Reports-two.png)

The **Händelseanalys** i det här diagrammet visar den uppsättning incidenter som har inträffat för programmet under det valda året. Varje incident har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Händelseanalys](/help/assets/sla-reporting3.png)

## SLA-mått {#sla-metrics}

* **Författarkontrakt**: Det här är det SLA som definieras i ditt avtal med Adobe Managed Services för författarnivån.
* **AMS Author SLA**: Detta är den uppmätta drifttiden för produktionsförfattarens nivåfactoringincidenter som orsakas av Adobe eller våra leverantörer.
* **Författar-SLA**: Det här är den uppmätta drifttiden för författarskiktet och ignorerar schemalagda driftavbrott, t.ex. underhållsperioder.
* **Slutanvändarkontrakt**: Det här är det SLA som definieras i ditt avtal med Adobes hanterade tjänster för publiceringsnivån.
* **AMS-slutanvändaravtal**: Detta är den uppmätta drifttiden för produktionsnivåfaktoriseringsincidenter som orsakas av Adobe eller våra leverantörer.
* **SLA för slutanvändare**: Detta är den uppmätta drifttiden för publiceringsskiktet som ignorerar schemalagda driftavbrott, t.ex. underhållsperioder.

## Videosjälvstudiekurs {#video-tutorial}

I den här videon får du en översikt över hur du använder diagram från Cloud Manager-rapporter för att visa dem i dina programmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
