---
title: Verktyget Innehållskopia
description: Med Cloud Manager innehållskopia kan man kopiera muterbart innehåll on demand från AMS-AEM 6.x-produktionsmiljöer till lägre miljöer för testning.
exl-id: 97915e58-a1d3-453f-b5ce-cad55ed73262
source-git-commit: 8e2c57d2594691e7fb18d8a538caa9b54a26b6bb
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---


# Verktyget Innehållskopia {#content-copy}

Med Cloud Manager innehållskopia kan man kopiera muterbart innehåll on demand från AMS-AEM 6.x-produktionsmiljöer till lägre miljöer för testning.

## Introduktion {#introduction}

Aktuella, riktiga data är värdefulla för testning, validering och för att ge användaren erkännande. Med innehållskopieringsverktyget kan du kopiera innehåll från din AMS-AEM 6.x-produktionsmiljö till testnings- eller utvecklingsmiljöer. Det här arbetsflödet stöder olika testscenarier.

En innehållsuppsättning definierar innehållet som ska kopieras. En innehållsuppsättning innehåller en lista med JCR-sökvägar med det ändringsbara innehåll som ska kopieras. Innehållet flyttas från en källmiljö till en målmiljö. Allt görs i samma Cloud Manager-program.

Följande sökvägar tillåts i en innehållsuppsättning:

```text
/content/**
/conf/**
/etc/**
/var/workflow/models/**
/var/commerce/**
```

När du kopierar innehåll är källmiljön en källa till sanning.

* Om du redigerar innehåll i målmiljön skrivs källinnehållet över om sökvägarna matchar.
* Om banorna inte är likadana sammanfogas innehåll från källan med innehållet i målplatsen.

## Behörigheter {#permissions}

Användaren måste tilldelas rollen **Distributionshanterare** i käll- och målmiljöerna för att kunna använda verktyget för innehållskopiering.

## Skapa en innehållsuppsättning {#create-content-set}

Innan något innehåll kan kopieras måste en innehållsuppsättning definieras. När du har definierat innehållet kan du återanvända det för att kopiera innehållet. Följ de här stegen för att skapa en innehållsuppsättning.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera från sidan **Översikt** till skärmen **Miljö**.

1. Gå till sidan **Innehållsuppsättningar** på skärmen **Miljö**.

1. Klicka på **Lägg till innehållsuppsättning** i skärmens övre högra hörn.

   ![Innehållsuppsättningar](/help/assets/content-sets.png)

1. Ange ett namn och en beskrivning för innehållsuppsättningen på fliken **Detaljer** i guiden och klicka på **Fortsätt**.

   ![Information om innehållsuppsättning](/help/assets/add-content-set-details.png)

1. På fliken **Innehållssökvägar** i guiden anger du sökvägarna till det ändringsbara innehåll som ska inkluderas i innehållsuppsättningen.

   1. Ange sökvägen i fältet **Lägg till inkluderingssökväg**.
   1. Klicka på **Lägg till sökväg** för att lägga till sökvägen till innehållsuppsättningen.
   1. Klicka på **Lägg till sökväg** igen om det behövs.

   ![Lägg till sökvägar i innehållsuppsättningen](/help/assets/add-content-set-paths.png)

1. Om du behöver förfina eller begränsa din innehållsuppsättning kan undersökvägar uteslutas.

   1. I listan med inkluderade sökvägar klickar du på ikonen **Lägg till exkludera delsökvägar** intill den sökväg som du vill begränsa.
   1. Ange den undersökväg som ska uteslutas från den valda sökvägen.
   1. Klicka på **Uteslut sökväg**.
   1. Klicka igen på **Lägg till exkludera delsökvägar** om du vill lägga till ytterligare sökvägar som ska exkluderas efter behov.

   ![Exkluderar banor](/help/assets/add-content-set-paths-excluded.png)

1. Du kan ändra de angivna sökvägarna om det behövs.

   1. Klicka på `X` bredvid de uteslutna delsökvägarna för att ta bort dem.
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

1. Navigera från sidan **Översikt** till skärmen **Miljö**.

1. Gå till sidan **Innehållsuppsättningar** på skärmen **Miljö**.

1. Välj en innehållsuppsättning från konsolen och välj **Kopiera innehåll** på ellipsmenyn.

   ![Innehållskopia](/help/assets/copy-content.png)

   >[!NOTE]
   >
   >En miljö kan inte markeras om:
   >
   >* Användaren har inte rätt behörighet.
   >* Miljön har en pågående pipeline eller en åtgärd för att kopiera innehåll.

1. I dialogrutan **Kopiera innehåll** anger du käll- och målmiljöerna för kopieringsåtgärden.
   * Målmiljöns områden måste vara samma som eller en delmängd av källmiljöns regioner.

1. Du kan välja att ta bort eller behålla de uteslutna sökvägarna i målmiljön. Markera kryssrutan `Do not delete exclude paths from destination` om du vill behålla `exclude paths` som anges i innehållsuppsättningen. Om kryssrutan inte är markerad tas uteslutna sökvägar bort i målmiljön.

1. Du kan välja att kopiera versionshistoriken för sökvägar som kopieras från källan till målmiljön. Markera kryssrutan `Copy Versions` om du vill kopiera all versionshistorik.

   ![Kopierar innehåll](/help/assets/copying-content.png)

1. Klicka på **Kopiera**.

Kopieringsprocessen startar. Kopieringsprocessens status visas i konsolen för den valda innehållsuppsättningen.

## Kopiera innehåll {#copy-activity}

Du kan övervaka statusen för dina kopieringsprocesser på sidan **Kopiera innehållsaktivitet**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj sedan rätt organisation och program.

1. Navigera från sidan **Översikt** till skärmen **Miljö**.

1. Gå till sidan **Kopiera innehållsaktivitet** på skärmen **Miljö**.

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
* Innehållskopiering kan bara utföras inom samma nivå. Det vill säga författare/författare eller publicera/publicera.
* Det går inte att kopiera innehåll mellan program och regioner.
* Innehållskopia för molndatalagringsbaserad topologi kan bara utföras när käll- och målmiljön finns på samma molnleverantör och i samma region.
* Det går inte att köra samtidiga innehållskopieringsåtgärder i samma miljö.
* Innehållskopiering kan inte utföras om det finns någon aktiv åtgärd som körs i mål- eller källmiljön, t.ex. en CI/CD-pipeline.
* Upp till femtio sökvägar kan anges per innehållsuppsättning. Det finns ingen begränsning för uteslutna banor.
* Verktyget för innehållskopia bör inte användas som kloning eller spegling eftersom det inte går att spåra flyttat eller borttaget innehåll i källan.
* En innehållskopia kan inte pausas eller avbrytas när den väl har initierats.
* Verktyget för innehållskopiering kopierar resurser och Dynamic Media-metadata från den högre miljön till den valda lägre miljön. Kopierade resurser måste sedan bearbetas på nytt med arbetsflödet [DAM-processresurser](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/using/assets-workflow) i den nedre miljön om du vill använda respektive Dynamic Media-konfiguration.
* Processen för innehållskopiering är avsevärt snabbare när versionshistorik inte kopieras.
* [Dynamic Media-konfigurationer med resurser som är större än 2 GB aktiverade](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/config-dms7#optional-config-dms7-assets-larger-than-2gb) stöds inte.
* När versionshistorik inte kopieras går kopieringen betydligt snabbare.
* Målmiljöns områden måste vara samma som eller en delmängd av källmiljöns regioner.

## Kända fel {#known-issues}

{{content-copy-known-issues}}
