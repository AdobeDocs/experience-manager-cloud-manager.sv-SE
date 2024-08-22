---
title: Versionshantering för Maven Project
description: Läs om hur Maven hanterar projektversioner i Cloud Manager.
exl-id: a1d676e0-27cc-4b0d-8799-527c0520946a
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Hantering av maven-projektversioner {#project-version}

Läs om hur Maven hanterar projektversioner i Cloud Manager.

## Hur Maven hanterar projektversioner {#how-maven}

För driftsättnings- och produktionsinstallationer genererar Cloud Manager en unik, stegvis version.

Den här versionen visas på sidan med information om pipeline-körning och aktivitetssidan. När en bygge körs uppdateras projektet Maven så att den här versionen används. En tagg skapas i Git-databasen med den versionen som namn.

Om den ursprungliga projektversionen uppfyller vissa kriterier sammanfogas både den ursprungliga projektversionen och den version av Cloud Manager som genererats av den uppdaterade projektversionen av Maven. Men taggen använder alltid den genererade versionen. För att den här sammanfogningen ska ske måste den ursprungliga projektversionen ha exakt tre versionssegment, till exempel `1.0.0` eller `1.2.3`, men inte `1.0` eller `1`, och den ursprungliga versionen får inte sluta med `-SNAPSHOT`.

>[!NOTE]
>
>Det här ursprungliga projektversionsvärdet måste anges statiskt i elementet `<version>` i filen på den översta nivån `pom.xml` i Git-databasgrenen.

Om den ursprungliga versionen uppfyller dessa villkor läggs den genererade versionen till i den ursprungliga versionen som ett nytt versionssegment. Den genererade versionen ändras också något, vilket inkluderar korrekt sortering och versionshantering. Anta till exempel att en genererad version av `2019.926.121356.0000020490` antas:

| Version | Version i `pom.xml` | Kommentar |
| --- | --- | --- |
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Rätt formaterad originalversion |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | ögonblicksbildsversion, överskriven |
| `1` | `2019.926.121356.0000020490` | Ofullständig version, överskriven |

>[!NOTE]
>
>Oavsett om originalversionen integrerades i den Cloud Manager-initierade versionen eller inte går den fortfarande att komma åt som en Maven-egenskap med namnet `cloudManagerOriginalVersion`.
