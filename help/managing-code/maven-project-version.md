---
title: Versionshantering för Maven Project
description: Läs om hur Maven hanterar projektversioner i Cloud Manager.
exl-id: a1d676e0-27cc-4b0d-8799-527c0520946a
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Versionshantering för Maven Project {#project-version}

Läs om hur Maven hanterar projektversioner i Cloud Manager.

## Hur Maven hanterar projektversioner {#how-maven}

För driftsättnings- och produktionsinstallationer genererar Cloud Manager en unik, stegvis version.

Den här versionen visas på sidan med information om pipeline-körning och aktivitetssidan. När ett bygge körs uppdateras Maven-projektet till att använda den här versionen och en tagg skapas i Git-databasen med den versionen som namn.

Om den ursprungliga projektversionen uppfyller vissa kriterier kommer den uppdaterade projektversionen från Maven att sammanfoga både den ursprungliga projektversionen och den version av Cloud Manager som genererats. Men taggen använder alltid den genererade versionen. För att den här sammanfogningen ska ske måste den ursprungliga projektversionen ha exakt tre versionssegment, till exempel `1.0.0` eller `1.2.3`, men inte `1.0` eller `1`, och den ursprungliga versionen får inte sluta med `-SNAPSHOT`.

>[!NOTE]
>
>Det här ursprungliga projektversionsvärdet måste anges statiskt i elementet `<version>` i den översta `pom.xml`-filen i Git-databasgrenen.

Om den ursprungliga versionen uppfyller dessa villkor läggs den genererade versionen till i den ursprungliga versionen som ett nytt versionssegment. Den genererade versionen kommer också att ändras något för att inkludera korrekt sortering och versionshantering. Anta till exempel att en genererad version av `2019.926.121356.0000020490` antas:

| Version | Version i `pom.xml` | Kommentar |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Rätt formaterad originalversion |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | ögonblicksbildsversion, överskriven |
| `1` | `2019.926.121356.0000020490` | Ofullständig version, överskriven |

>[!NOTE]
>
>Oavsett om originalversionen införlivades i den Cloud Manager-initierade versionen eller inte är originalversionen tillgänglig som en Maven-egenskap med namnet `cloudManagerOriginalVersion`.
