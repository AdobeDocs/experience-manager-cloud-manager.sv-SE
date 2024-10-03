---
source-git-commit: 9d910e1b1a4aad000a8389ddc22ce380bbccd4ef
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 0%

---
# Fragment (#snippets)

## Kända fel i innehållskopia {#content-copy-known-issues}

Om en resurs i källmiljön byter namn när funktionen [innehållskopiering](/help/using/content-copy.md) används kan det leda till att innehållskopieringen misslyckas på grund av att UUID i målmiljön är i konflikt.

För att undvika det här felet bör du först ta bort resurserna och sedan återskapa dem med det nya resursnamnet, i stället för att byta namn.
