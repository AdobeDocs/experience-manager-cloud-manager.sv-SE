---
title: Verktyget Innehållskopia
description: Med Cloud Manager Content Copy Tool kan man kopiera muterbart innehåll on demand från AMS-AEM 6.x till lägre miljöer för testning.
exl-id: 97915e58-a1d3-453f-b5ce-cad55ed73262
source-git-commit: 200366e5db92b7ffc79b7a47ce8e7825b29b7969
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# Verktyget Innehållskopia {#content-copy}

Med Cloud Manager Content Copy Tool kan man kopiera muterbart innehåll on demand från AMS-AEM 6.x till lägre miljöer för testning.

## Introduktion {#introduction}

Aktuella, riktiga data är värdefulla för testning, validering och för att ge användaren erkännande. Med verktyget för innehållskopiering kan du kopiera innehåll från din AMS-AEM 6.x-produktionsmiljö till en staging- eller utvecklingsmiljö för sådan testning.

Innehållet som ska kopieras definieras av en innehållsuppsättning. En innehållsuppsättning består av en lista med JCR-sökvägar som innehåller det muterbara innehåll som ska kopieras från en källmiljö till en målmiljö inom samma Cloud Manager-program. Följande sökvägar tillåts i en innehållsuppsättning.

```text
/content/**
/conf/**
/etc/**
/var/workflow/models/**
/var/commerce/**
```

När du kopierar innehåll är källmiljön en källa till sanning.

* Om innehållet har ändrats i målmiljön skrivs det över av innehållet i källan, om sökvägarna är desamma.
* Om banorna inte är samma kommer innehåll från källan att sammanfogas med innehållet i målet.

## Behörigheter {#permissions}

Användaren måste tilldelas rollen **Distributionshanterare** i käll- och målmiljöerna för att kunna använda verktyget för innehållskopiering.

## Skapa en innehållsuppsättning {#create-content-set}

Innan något innehåll kan kopieras måste en innehållsuppsättning definieras. När du har definierat innehållet kan du återanvända det för att kopiera innehållet. Följ de här stegen för att skapa en innehållsuppsättning.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Navigera till sidan **Innehållsuppsättningar** från skärmen **Miljö**.

1. Klicka på knappen **Lägg till innehållsuppsättning** längst upp till höger på skärmen.

   ![Innehållsuppsättningar](/help/assets/content-sets.png)

1. Ange ett namn och en beskrivning för innehållsuppsättningen på fliken **Detaljer** i guiden och klicka på **Fortsätt**.

   ![Information om innehållsuppsättning](/help/assets/add-content-set-details.png)

1. På fliken **Innehållssökvägar** i guiden anger du sökvägarna till det ändringsbara innehåll som ska inkluderas i innehållsuppsättningen.

   1. Ange sökvägen i fältet **Lägg till inkluderingssökväg**.
   1. Klicka på knappen **Lägg till bana** för att lägga till sökvägen till innehållsuppsättningen.
   1. Klicka på knappen **Lägg till bana** igen om det behövs.

   ![Lägg till sökvägar i innehållsuppsättningen](/help/assets/add-content-set-paths.png)

1. Om du behöver förfina eller begränsa din innehållsuppsättning kan undersökvägar uteslutas.

   1. I listan med inkluderade sökvägar klickar du på ikonen **Lägg till exkludera delsökvägar** intill den sökväg som du vill begränsa.
   1. Ange den delbana som ska uteslutas under den valda banan.
   1. Klicka på **Uteslut sökväg**.
   1. Klicka på **Lägg till exkludera delsökvägar** igen om du vill lägga till ytterligare sökvägar som ska exkluderas efter behov.

   ![Exkluderar banor](/help/assets/add-content-set-paths-excluded.png)

1. Du kan ändra de angivna sökvägarna om det behövs.

   1. Klicka på X bredvid de uteslutna delbanorna för att ta bort dem.
   1. Klicka på ellipsknappen bredvid sökvägarna för att visa alternativen **Redigera** och **Ta bort**.

   ![Redigerar sökvägslista](/help/assets/add-content-set-excluded-paths.png)

1. Klicka på **Skapa** för att skapa innehållsuppsättningen.

Innehållsuppsättningen kan nu användas för att kopiera innehåll mellan miljöer.

>[!NOTE]
>
>Du kan lägga till upp till 50 banor i en innehållsuppsättning.
>Det finns ingen begränsning för uteslutna banor.

## Redigera en innehållsuppsättning {#edit-content-set}

Följ liknande steg som när du skapar ett innehållssteg. I stället för att klicka på **Lägg till innehållsuppsättning** markerar du en befintlig uppsättning i konsolen och väljer **Redigera** på ellipsmenyn.

![Redigera innehållsuppsättning](/help/assets/edit-content-set.png)

När du redigerar din innehållsuppsättning kan du behöva utöka de konfigurerade sökvägarna för att visa de uteslutna delsökvägarna.

## Kopierar innehåll {#copy-content}

När en innehållsuppsättning har skapats kan du använda den för att kopiera innehåll. Följ de här stegen för att kopiera innehåll.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Navigera till sidan **Innehållsuppsättningar** från skärmen **Miljö**.

1. Välj en innehållsuppsättning från konsolen och välj **Kopiera innehåll** på ellipsmenyn.

   ![Innehållskopia](/help/assets/copy-content.png)

   >[!NOTE]
   >
   >En miljö kan inte markeras om:
   >
   >* Användaren har inte rätt behörighet.
   >* Miljön har en pågående pipeline eller en åtgärd för att kopiera innehåll.

1. I dialogrutan **Kopiera innehåll** anger du källan och målet för kopieringsåtgärden.

1. Du kan välja att ta bort eller behålla de uteslutna sökvägarna i målmiljön. Markera kryssrutan `Do not delete exclude paths from destination` om du vill behålla de uteslutna sökvägar som anges i innehållsuppsättningen. Om kryssrutan inte är markerad tas uteslutna sökvägar bort i målmiljön.

1. Du kan välja att kopiera versionshistorik för sökvägarna som kopieras från käll- till målmiljön. Markera kryssrutan `Copy Versions` om du vill kopiera all versionshistorik.

   ![Kopierar innehåll](/help/assets/copying-content.png)

1. Klicka på **Kopiera**.

Kopieringsprocessen startar. Kopieringsprocessens status visas i konsolen för den valda innehållsuppsättningen.

## Innehållskopia aktivitet {#copy-activity}

Du kan övervaka statusen för dina kopieringsprocesser på sidan **Kopiera innehållsaktivitet**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Navigera till sidan **Kopiera innehållsaktivitet** från skärmen **Miljö**.

![Aktivitet för innehållskopia](/help/assets/copy-content-activity.png)

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
   * Kopierade resurser måste sedan bearbetas på nytt med arbetsflödet [DAM-processresurser](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html) i den nedre miljön för att kunna använda respektive dynamiska mediekonfiguration.
* Processen för innehållskopiering går mycket snabbare när versionshistoriken inte kopieras.
