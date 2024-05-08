---
title: Övervakningsmiljöer
description: Lär dig övervaka dina miljöer i Cloud Manager.
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: ab527beb706ab73a14cc933a3414873dee6b7a9e
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Övervakningsmiljöer {#monitoring-environments}

Lär dig övervaka dina miljöer i Cloud Manager.

## Måtttrösklar {#thresholds}

Systemövervakning i [!UICONTROL Cloud Manager] gör du genom att observera de enskilda instanserna i en miljö och spåra en mängd olika mätvärden för varje instans. Varje mätvärde har två definierade tröskelvärden: ett tröskelvärde för varning och ett kritiskt tröskelvärde.

Om ett mätvärde överstiger dess kritiska tröskelvärde anses det vara i ett kritiskt tillstånd. Om ett mätvärde överskrider varningströskeln (men under det kritiska tröskelvärdet) anses det vara i ett varningstillstånd. Tröskelvärdena fastställs av Adobe Managed Services och kan visualiseras i [!UICONTROL Cloud Manager]. I de flesta fall är tröskelvärdena desamma för kunderna, men det finns fall där Adobe Managed Services kommer att ändra tröskelvärdena för att matcha specifika kundkrav. Frågor om tröskelvärdena ska ställas till din Customer Success Engineer (CSE).

## Åtkomst till systemövervakning {#accessing-system-monitoring}

Följ de här stegen för att få åtkomst till systemövervakning.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välja lämplig organisation och lämpligt program.

1. Tryck eller klicka på ellipsknappen för det program du vill övervaka och välj **Visa övervakning** alternativ.

   ![Inställningar](/help/assets/first-timea1.png)

The **Rapporter** öppnas för att visa information om systemövervakning.

## Systemövervakning - översikt {#system-monitoring-overview}

The **Systemövervakning** i **Rapporter** På sidan visas de övervakade miljöerna i programmet och rapporter om deras hälsa på hög nivå i fyra olika kategorier:

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

Om du vill visa information om specifika mått trycker eller klickar du på en av kategorikolumnerna för en viss instans eller kategorititeln i den vänstra navigeringen. På varje detaljsida visas en serie diagram för måtten i den kategorin. Du kan antingen visa mätvärden för alla instanser i en miljö eller för en viss instans. Du kan växla mellan miljö och instanser med listrutorna i det övre högra hörnet.

![Välj miljö](/help/assets/System_Monitoring1.png)

Navigeringen till vänster visar tillgängliga mätvärden i den valda kategorin som det finns data för den valda miljön och instanser för.

Ett enskilt diagram visar status och ett diagram över data över tiden tillsammans med tröskelvärdena. Om flera instanser visas kommer varje instans data att finnas i en separat serie.

![Mätdiagram](/help/assets/Monitoring_Graphs1.png)

Du kan dölja enskilda serier i ett diagram genom att klicka på serien i teckenförklaringen.
Om du till exempel klickar på varningströskelserien visas bara det kritiska tröskelvärdet.

![Ändra diagram](/help/assets/Monitoring_Graphs2.png)

### Måttdefinitioner {#metric-definitions}

#### Värd {#host}

* **Belastning per kärna**: Antalet processer som körs av CPU:n eller som befinner sig i vänteläge är i genomsnitt över en (load1), fem (load5) och femton (load15) minuter.
* **Antal processer**: Antal öppna processer
* **Antal användare**: Antal användare med en aktiv gränssnittssession
* **Minnesanvändning**: Procentandel av systemminnet som är allokerat
* **JVM-minne**: Storleken (i megabyte) på det allokerade Java-heap
* **Gammalt generationsutrymme**: Procentandel av JVM-gammalt genereringsminne som för närvarande allokeras

#### Nätverk {#network}

* **CQ-portkontroll**: Svarstiden i sekunder för åtkomst till AEM- eller Dispatcher-porten
   * Det finns olika mätvärden för författare, publicering och skickare.

#### Lagring {#storage}

* **Diskutrymme**: Använt diskutrymme (i megabyte) för varje monteringspunkt på värden
   * Det finns olika mätvärden för varje monteringspunkt.
   * Det finns åtminstone mått för `/` och `/mnt`, men ytterligare monteringspunktsmått kan vara tillgängliga beroende på den specifika instanskonfigurationen.
* **Mappstorlek**
* **AEM segmentlager**: Använt diskutrymme (i gigabyte) för AEM segmentarkiv

#### Program {#application}

* **Replikeringsagent**: Tiden (i sekunder) för en testreplikeringshändelse
   * Det finns olika mått för varje replikeringsagent.
* **Dispatcher Flush**: Antalet objekt som för närvarande finns i kön för rensning av dispatcher

## SLA-rapportering {#sla-reporting}

Du kan se hur väl AEM presterar i förhållande till det serviceavtal du har tecknat.

I följande diagram visas månatlig SLA-uppnående för 2019.

![SLA 2018-diagram](/help/assets/SLA-Reports-one.png)

Precis som med diagram för systemövervakning visar en rullande datapunkt de specifika värdena för den månaden.

![Datapunktens överrullning](/help/assets/SLA-Reports-two.png)

The **Händelseanalys** i det här diagrammet visar den uppsättning incidenter som har inträffat för programmet under det valda året. Varje incident har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Händelseanalys](/help/assets/sla-reporting3.png)

## SLA-mått {#sla-metrics}

* **Författarkontrakt**: Detta är det SLA som definieras i ditt avtal med Adobe Managed Services för författarnivån.
* **AMS Author SLA**: Detta är den uppmätta drifttiden för produktionsförfattarens nivåfactoringincidenter som orsakas av Adobe eller våra leverantörer.
* **Författar-SLA**: Detta är den uppmätta drifttiden för författarskiktet och ignorerar schemalagda driftavbrott, t.ex. underhållsperioder.
* **Slutanvändarkontrakt**: Detta är det SLA som definieras i ditt avtal med Adobe Managed Services för publiceringsnivån.
* **AMS-slutanvändaravtal**: Detta är den uppmätta drifttiden för produktionsnivåfaktoriseringsincidenter som orsakas av Adobe eller våra leverantörer.
* **SLA för slutanvändare**: Det här är den uppmätta drifttiden för publiceringsskiktet som ignorerar schemalagda driftavbrott, t.ex. underhållsperioder.

## Videosjälvstudie {#video-tutorial}

I den här videon får du en översikt över hur du använder diagram från Cloud Manager-rapporter för att visa dem i dina programmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
