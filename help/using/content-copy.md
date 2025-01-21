---
title: Konsekvens för innehållskopia för miljö
description: Med Content Copy i Cloud Manager kan man kopiera muterbart innehåll On-demand från Adobe Experience Manager 6.x-produktionsmiljöer som ligger på Adobe Managed Services till lägre testmiljöer.
exl-id: 97915e58-a1d3-453f-b5ce-cad55ed73262
source-git-commit: 84b3366481c2efd497583627eac67046452f6c38
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# Content Copy for environment consistent {#content-copy}

Med Content Copy i Cloud Manager kan man kopiera muterbart innehåll On-demand från Adobe Experience Manager 6.x-produktionsmiljöer som ligger på Adobe Managed Services till lägre testmiljöer.

## Om Innehållskopia {#introduction}

Aktuella, riktiga data är värdefulla för testning, validering och för att ge användaren erkännande. Med Content Copy kan du kopiera innehåll från din AMS-AEM 6.x-produktionsmiljö till testnings- eller utvecklingsmiljöer. Det här arbetsflödet stöder olika testscenarier.

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

Om du redigerar innehåll i målmiljön skrivs källinnehållet över om sökvägarna matchar.

Om banorna inte är likadana sammanfogas innehåll från källan med innehållet i målplatsen.

### Behörigheter {#permissions}

Användaren måste tilldelas rollen **Distributionshanterare** i käll- och målmiljöerna för att kunna använda funktionen för innehållskopiering.

## Skapa en innehållsuppsättning {#create-content-set}

Innan något innehåll kan kopieras måste en innehållsuppsättning definieras. När du har definierat innehållet kan du återanvända det för att kopiera innehållet. Följ de här stegen för att skapa en innehållsuppsättning.

**Så här skapar du en innehållsuppsättning:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att öppna den vänstra menyn.

1. Klicka på ikonen ![Ruta ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) **Innehållsuppsättningar** på den vänstra menyn på sidan **Tjänster**.

1. Klicka på **Lägg till innehållsuppsättning** i sidans övre högra hörn.

   ![Innehållsuppsättningar](/help/assets/content-sets.png)

1. I dialogrutan **`Add Content Set`**, på fliken **Detaljer**, i fälten **Namn** och **Beskrivning**, skriver du ett namn och en valfri beskrivning för innehållsuppsättningen och klickar sedan på **Fortsätt**.

   ![Information om innehållsuppsättning](/help/assets/add-content-set-details.png)

1. På fliken **Innehållssökvägar** anger du en sökväg till det innehåll som kan ändras och som ska inkluderas i innehållsuppsättningen i textfältet **Sökväg**.

   Endast sökvägar som börjar med `/content`, `/conf`, `/etc`, `/var/workflow/models` eller `/var/commerce` kan tas med.

1. Klicka på ikonen ![Lägg till mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderAdd_18_N.svg) **Lägg till sökväg** för att lägga till (eller ta med) sökvägen till innehållsuppsättningen.

1. (Valfritt) Om det behövs lägger du till tilläggsbanor (upp till 50) genom att upprepa de två föregående stegen. I annat fall fortsätter du till nästa steg.

   ![Lägg till sökvägar i innehållsuppsättningen](/help/assets/add-content-set-paths.png)

1. (Valfritt) Om du vill begränsa innehållsuppsättningen kan du även ange underbanor i en inkluderad innehållssökväg som ska uteslutas.

   1. Klicka på ikonen ![Ta bort mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderDelete_18_N.svg) till höger om den inkluderade innehållssökvägen som du vill begränsa.
   1. I textfältet anger du en relativ sökväg till rotsökvägen som visas i dialogrutan.
   1. Klicka på ikonen ![Ta bort mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderDelete_18_N.svg) **Uteslut sökväg**.
   1. Om det behövs upprepar du stegen i. till iii. ovan om du vill lägga till fler uteslutna banor. Det finns ingen begränsning. I annat fall fortsätter du till nästa steg.

   ![Exkluderar banor](/help/assets/add-content-set-paths-excluded.png)

1. (Valfritt) Gör något av följande:

   1. Klicka på ikonen ![Korsstorlek 500](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg) till höger om en exkluderad underbana om du vill ta bort den.
   1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/ui_18/More.svg) till höger om en inkluderad innehållssökväg och klicka sedan på **Redigera** eller **Ta bort**.

   ![Redigerar sökvägslista](/help/assets/add-content-set-excluded-paths.png)

1. Klicka på **Skapa**. Nu kan du använda innehållsuppsättningen för att kopiera innehåll mellan miljöer.

## Redigera eller ta bort en innehållsuppsättning {#edit-content-set}

När du redigerar en innehållsuppsättning kan du behöva utöka de konfigurerade sökvägarna för att visa de uteslutna delsökvägarna.

**Så här redigerar eller tar du bort en innehållsuppsättning:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att öppna den vänstra menyn.

1. Klicka på ikonen ![Ruta ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) **Innehållsuppsättningar** på den vänstra menyn under **Tjänster**.

1. I tabellen på sidan **Innehållsuppsättningar** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/ui_18/More.svg) till höger om en inkluderad innehållssökväg och sedan på **Redigera** eller **Ta bort** .

![Redigera innehållsuppsättning](/help/assets/edit-content-set.png)

## Kopiera innehåll {#copy-content}

När en innehållsuppsättning har skapats kan du använda den för att kopiera innehåll.

En miljö kan vara otillgänglig för markering om något av följande villkor gäller:

* Användaren saknar de behörigheter som krävs.
* En pipeline- eller innehållskopieringsåtgärd körs för närvarande i miljön.

**Så här kopierar du innehåll:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att öppna den vänstra menyn.

1. Klicka på ikonen ![Ruta ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) **Innehållsuppsättningar** på den vänstra menyn under **Tjänster**.

1. I tabellen på sidan **Innehållsuppsättningar**, till höger om den innehållssökväg som du vill kopiera, klickar du på ![Mer ikon](https://spectrum.adobe.com/static/icons/ui_18/More.svg) och sedan på **Kopiera innehåll**.

   ![Innehållskopia](/help/assets/copy-content.png)

1. I dialogrutan **Kopiera innehåll** väljer du **Source** -miljön och **målmiljön** för innehållskopieringsåtgärden.

   * Områden i en målmiljö måste vara en delmängd av regioner i en källmiljö.
   * Kompatibilitetsproblem kontrolleras innan en innehållskopia körs. När du väljer miljön **Mål** valideras käll- och målmiljöerna automatiskt. Om valideringen misslyckas avbryts processen och ett felmeddelande visas i dialogrutan som förklarar orsaken till felet.

     ![Kopierar innehåll](/help/assets/copying-content.png)

1. (Valfritt) Gör något av följande:

   1. Markera **`Do not delete exclude paths from destination`** om du vill *behålla* de uteslutna sökvägarna i målmiljön. Den här inställningen bevarar de uteslutna sökvägarna som anges i innehållsuppsättningen intakta.
   1. Om du vill *ta bort* de uteslutna sökvägarna i målmiljön avmarkerar du **`Do not delete exclude paths from destination`**. Den här inställningen tar bort de uteslutna sökvägarna som anges i innehållsuppsättningen.
   1. Om du vill kopiera versionshistoriken för sökvägar från källmiljön till målmiljön ska du kontrollera **Kopiera versioner**. Processen för innehållskopiering är avsevärt snabbare när versionshistoriken *inte* kopieras.

1. Klicka på **Kopiera**. Kopieringsprocessens status visas i konsolen för den valda innehållsuppsättningen.

## Kontrollera status för en innehållskopia {#copy-activity}

Du kan övervaka statusen för dina kopieringsprocesser på sidan **Kopiera innehållsaktivitet**.

**Så här kontrollerar du statusen för en innehållskopia:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att öppna den vänstra menyn.

1. Klicka på ikonen ![Historik ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) **Kopiera innehållsaktivitet** på den vänstra menyn under **Tjänster**.

   ![Aktivitet för innehållskopia](/help/assets/copy-content-activity.png)

   En innehållskopia kan ha någon av följande statusar:

   | Status | Beskrivning |
   | --- | --- |
   | Pågår | Processen för innehållskopia pågår. |
   | Slutförd | Innehållskopieringsprocessen har slutförts. |
   | Misslyckades | Det gick inte att kopiera innehåll. |

## Begränsningar för innehållskopia {#limitations}

* En innehållskopia kan inte utföras från en lägre miljö till en högre miljö.
* Innehållskopiering kan bara utföras inom samma nivå. Det vill säga författare/författare eller publicera/publicera.
* Det går inte att kopiera innehåll mellan program och regioner.
* Innehållskopia för molndatalagringsbaserad topologi kan bara utföras när käll- och målmiljön finns på samma molnleverantör och i samma region.
* Det går inte att köra samtidiga innehållskopieringsåtgärder i samma miljö.
* Innehållskopiering kan inte utföras om det finns någon aktiv åtgärd som körs i mål- eller källmiljön, t.ex. en CI/CD-pipeline.
* Innehållskopia ska inte användas som kloning eller speglingsverktyg eftersom det inte går att spåra flyttat eller borttaget innehåll i källan.
* En innehållskopia kan inte pausas eller avbrytas när den väl har initierats.
* Innehållskopia duplicerar resurser och Dynamic Media-metadata från den högre miljön till den valda lägre miljön. Kopierade resurser måste sedan bearbetas på nytt med arbetsflödet [DAM-processresurser](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/using/assets-workflow) i den nedre miljön om du vill använda respektive Dynamic Media-konfiguration.
* [Dynamic Media-konfigurationer med resurser som är större än 2 GB aktiverade](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/config-dms7#optional-config-dms7-assets-larger-than-2gb) stöds inte.
* Målmiljöns områden måste vara samma som eller en delmängd av källmiljöns regioner.

## Kända fel i Content Copy {#known-issues}

{{content-copy-known-issues}}
