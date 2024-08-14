---
source-git-commit: c772b3c576cac3a76433b67dc8a5233802996813
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---
# Fragment (#snippets)

## Kända fel i innehållskopia {#content-copy-known-issues}

Du bör vara medveten om följande kända fel när du använder funktionen för att kopiera innehåll i [en.](/help/using/content-copy.md)

* Om en resurs i källmiljön byter namn kan det leda till att innehållskopieringsåtgärden misslyckas på grund av att UUID:n i målmiljön är i konflikt.
   * För att undvika det här felet bör du först ta bort resurserna och sedan återskapa dem med det nya resursnamnet, i stället för att byta namn.
