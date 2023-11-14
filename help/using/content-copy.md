---
title: Verktyget Innehållskopia
description: Med innehållskopieringsverktyget i Cloud Manager kan användare kopiera muterbart innehåll on demand från AMS-AEM 6.x-produktionsmiljöer till lägre miljöer för testningsändamål.
exl-id: 97915e58-a1d3-453f-b5ce-cad55ed73262
source-git-commit: c7803c75bcfcc967877808214704c5746015481d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---


# Verktyget Innehållskopia {#content-copy}

Med innehållskopieringsverktyget i Cloud Manager kan användare kopiera muterbart innehåll on demand från AMS-AEM 6.x-produktionsmiljöer till lägre miljöer för testningsändamål.

## Introduktion {#introduction}

Aktuella, riktiga data är värdefulla för testning, validering och för att ge användaren erkännande. Med verktyget för innehållskopiering kan du kopiera innehåll från din AMS-AEM 6.x-produktionsmiljö till en staging- eller utvecklingsmiljö för sådan testning.

Innehållet som ska kopieras definieras av en innehållsuppsättning. En innehållsuppsättning består av en lista med JCR-sökvägar som innehåller det muterbara innehåll som ska kopieras från en källmiljö till en målmiljö inom samma Cloud Manager-program. Följande sökvägar tillåts i en innehållsuppsättning.

```text
/content/**
/conf/**
/etc/**
/var/workflow/models/**
```

När du kopierar innehåll är källmiljön en källa till sanning.

* Om innehållet har ändrats i målmiljön skrivs det över av innehållet i källan, om sökvägarna är desamma.
* Om banorna inte är samma kommer innehåll från källan att sammanfogas med innehållet i målet.

## Behörigheter {#permissions}

Användaren måste tilldelas till verktyget Innehållskopia för att kunna använda verktyget **Distributionshanteraren** roll i käll- och målmiljöer.

## Skapa en innehållsuppsättning {#create-content-set}

Innan något innehåll kan kopieras måste en innehållsuppsättning definieras. När du har definierat innehållet kan du återanvända det för att kopiera innehållet. Följ de här stegen för att skapa en innehållsuppsättning.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Ökning** sida.

1. Navigera till **Innehållsuppsättningar** sidan från **Miljö** skärm.

1. Tryck eller klicka på **Lägg till innehållsuppsättning** längst upp till höger på skärmen.

   ![Innehållsuppsättningar](/help/assets/content-sets.png)

1. På **Information** Ange ett namn och en beskrivning för innehållsuppsättningen och tryck eller klicka på **Fortsätt**.

   ![Information om innehållsuppsättning](/help/assets/add-content-set-details.png)

1. På **Innehållsbanor** -fliken i guiden anger du sökvägarna till det ändringsbara innehåll som ska inkluderas i innehållsuppsättningen.

   1. Ange banan i dialogrutan **Lägg till inkluderingssökväg** fält.
   1. Tryck eller klicka på **Lägg till bana** om du vill lägga till sökvägen till innehållsuppsättningen.
   1. Tryck eller klicka på **Lägg till bana** igen om det behövs.

   ![Lägg till banor i innehållsuppsättningen](/help/assets/add-content-set-paths.png)

1. Om du behöver förfina eller begränsa din innehållsuppsättning kan undersökvägar uteslutas.

   1. I listan med inkluderade sökvägar trycker eller klickar du på **Lägg till exkludera delsökvägar** -ikonen bredvid banan som du vill begränsa.
   1. Ange den delbana som ska uteslutas under den valda banan.
   1. Tryck eller klicka **Uteslut bana**.
   1. Tryck eller klicka **Lägg till exkludera delsökvägar** igen om du vill lägga till ytterligare sökvägar som ska uteslutas efter behov.

   ![Exkludera banor](/help/assets/add-content-set-paths-excluded.png)

1. Du kan ändra de angivna sökvägarna om det behövs.

   1. Tryck eller klicka på X bredvid de uteslutna delbanorna för att ta bort dem.
   1. Tryck eller klicka på ellipsknappen bredvid banorna för att visa **Redigera** och **Ta bort** alternativ.

   ![Redigera sökvägslista](/help/assets/add-content-set-excluded-paths.png)

1. Tryck eller klicka **Skapa** för att skapa innehållsuppsättningen.

Innehållsuppsättningen kan nu användas för att kopiera innehåll mellan miljöer.

>[!NOTE]
>
>Du kan lägga till upp till 50 banor i en innehållsuppsättning.
>Det finns ingen begränsning för uteslutna banor.

## Redigera en innehållsuppsättning {#edit-content-set}

Följ liknande steg som när du skapar ett innehållssteg. Istället för att trycka eller klicka **Lägg till innehållsuppsättning** väljer du en befintlig uppsättning från konsolen och väljer **Redigera** på ellipsmenyn.

![Redigera innehållsuppsättning](/help/assets/edit-content-set.png)

När du redigerar din innehållsuppsättning kan du behöva utöka de konfigurerade sökvägarna för att visa de uteslutna delsökvägarna.

## Kopierar innehåll {#copy-content}

När en innehållsuppsättning har skapats kan du använda den för att kopiera innehåll. Följ de här stegen för att kopiera innehåll.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Ökning** sida.

1. Navigera till **Innehållsuppsättningar** sidan från **Miljö** skärm.

1. Välj en innehållsuppsättning från konsolen och välj **Kopiera innehåll** på ellipsmenyn.

   ![Innehållskopia](/help/assets/copy-content.png)

   >[!NOTE]
   >
   >En miljö kan inte markeras om:
   >
   >* Användaren har inte rätt behörighet.
   >* Miljön har en pågående pipeline eller en åtgärd för att kopiera innehåll.

1. I **Kopiera innehåll** anger du källa och mål för kopieringsåtgärden.

1. Du kan välja att ta bort eller behålla de uteslutna sökvägarna i målmiljön. Markera kryssruta `Do not delete exclude paths from destination` om du vill behålla de uteslutna sökvägar som anges i innehållsuppsättningen. Om kryssrutan inte är markerad tas uteslutna sökvägar bort i målmiljön.

1. Du kan välja att kopiera versionshistorik för sökvägarna som kopieras från käll- till målmiljön. Markera kryssruta `Copy Versions` om du vill kopiera all versionshistorik.

   ![Kopierar innehåll](/help/assets/copying-content.png)

1. Tryck eller klicka **Kopiera**.

Kopieringsprocessen startar. Kopieringsprocessens status visas i konsolen för den valda innehållsuppsättningen.

## Innehållskopia aktivitet {#copy-activity}

Du kan övervaka statusen för dina kopieringsprocesser i **Kopiera innehållsaktivitet** sida.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Ökning** sida.

1. Navigera till **Kopiera innehållsaktivitet** sidan från **Miljö** skärm.

![Innehållskopia aktivitet](/help/assets/copy-content-activity.png)

### Status för innehållskopia {#statuses}

När du börjar kopiera innehåll kan processen ha någon av följande statusar.

| Status | Beskrivning |
|---|---|
| Pågår | Innehållskopieringen pågår |
| Misslyckades | Åtgärden Kopiera innehåll misslyckades |
| Slutförd | Innehållskopieringen har slutförts |

## Begränsningar {#limitations}

Verktyget för innehållskopiering har följande begränsningar.

* En innehållskopia kan inte utföras från en lägre miljö till en högre miljö.
* Innehållskopia kan bara utföras inom samma nivå (dvs. författare eller publicera).
* Det går inte att kopiera innehåll mellan program och regioner.
* Innehållskopia för molndatalagringsbaserad topologi kan bara utföras när käll- och målmiljön finns på samma molnleverantör och samma region.
* Det går inte att köra samtidiga kopieringsåtgärder för innehåll i samma miljö.
* Innehållskopiering kan inte utföras om det finns någon aktiv åtgärd som körs på mål- eller källmiljön, t.ex. en CI/CD-pipeline.
* Upp till femtio sökvägar kan anges per innehållsuppsättning. Det finns ingen begränsning för uteslutna banor.
* Verktyget för innehållskopia bör inte användas som kloning eller spegling eftersom det inte kan spåra flyttat eller borttaget innehåll i källan.
* En innehållskopia kan inte pausas eller avbrytas när den väl har initierats.
* Verktyget för innehållskopiering kopierar resurser tillsammans med dynamiska medierelaterade metadata från den högre miljön till den valda nedre miljön.
   * Kopierade resurser måste sedan bearbetas på nytt med [Arbetsflöde för resurser i DAM-process](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html) i den nedre miljön för att kunna använda respektive dynamiska mediekonfiguration.
* Processen för innehållskopiering går mycket snabbare när versionshistoriken inte kopieras.
