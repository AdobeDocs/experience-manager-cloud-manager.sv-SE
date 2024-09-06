---
source-git-commit: 4ff440250b4ed0770c34a7042ec7d22c79ffe05e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---
# Fragment (#snippets)

## Kända fel i innehållskopia {#content-copy-known-issues}

Tänk på följande kända fel när du använder funktionen för att kopiera innehåll i [en.](/help/using/content-copy.md)

* Om en resurs i källmiljön byter namn kan det leda till att innehållskopieringsåtgärden misslyckas på grund av att UUID:n i målmiljön är i konflikt.
   * För att undvika det här felet bör du först ta bort resurserna och sedan återskapa dem med det nya resursnamnet, i stället för att byta namn.
