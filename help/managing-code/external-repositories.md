---
title: Lägg till externa databaser i Cloud Manager - tidig Adobe
description: Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub-, GitLab- och Bitbucket-databaser.
exl-id: 4500cacc-5e27-4bbb-b8f6-5144dac7e6da
source-git-commit: 58cdebf819f2737be5d8e129ff5b9783888f3c21
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Lägga till externa databaser i Cloud Manager {#external-repositories}

Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub-, GitLab- och Bitbucket-databaser.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet](/help/release-notes/current.md#early-adoption).

## Konfigurera en extern databas

Konfigurationen av en extern lagringsplats i Cloud Manager består av tre steg:

1. [Lägg till en extern databas](#add-external-repo) till ett valt program.
1. Ange en åtkomsttoken för den externa databasen.
1. Validera ägarskap för den externa databasen.


## Lägga till en extern databas {#add-ext-repo}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/getting-started/navigation.md#my-programs-console) väljer du det program som du vill länka till en extern databas.


1. Välj ![Mappikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Databaser** på sidomenyn under **Tjänster**.

   ![Sidan Databaser](/help/managing-code/assets/repositories-tab.png)

1. Klicka på **Lägg till databas** i det övre högra hörnet på sidan **Databaser**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** för att länka en extern Git-databas till ditt program.

   ![Lägg till egen databas](/help/managing-code/assets/repositories-private-repo-type.png)

1. Ange följande information om din databas i varje fält:

   | Fält | Beskrivning |
   | --- | --- |
   | **Databasnamn** | Obligatoriskt. Ett uttrycksfullt namn för din nya databas. |
   | **Databas-URL** | Obligatoriskt. Databasens URL.<br><br> Om du använder en GitHub-värdbaserad databas måste sökvägen sluta i `.git`.<br>Till exempel *`https://github.com/org-name/repo-name.git`* (URL-sökvägen är endast avsedd som illustration).<br><br>Om du använder en extern databas måste den använda följande URL-sökvägsformat:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> eller<br>`https://self-hosted-domain/org-name/repo-name.git`<br>Och matcha Git-leverantören. |
   | **Välj databastyp** | Obligatoriskt. Välj den databastyp som du använder: **GitHub**, **GitLab** eller **BitBucket**. Om databasens URL-sökväg ovan innehåller Git-leverantörens namn, till exempel GitLab eller Bitbucket, är databastypen redan förvald. |
   | **Beskrivning** | Valfritt. En detaljerad beskrivning av databasen. |

1. Välj **Spara** för att lägga till databasen.

1. I dialogrutan **Validering av privat databasägande** anger du en åtkomsttoken för att validera ägarskapet för den externa databasen så att du kan komma åt den.

   ![Välja en befintlig åtkomsttoken för en databas](/help/managing-code/assets/repositories-exisiting-access-token.png)
   *Väljer en befintlig åtkomsttoken för en BitBucket-databas.*

   | Tokentyp | Beskrivning |
   | --- | --- |
   | **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
   | **Lägg till ny åtkomsttoken** | **Databastyp: GitHub**<br> ・ Ange ett namn för åtkomsttoken som du skapar i textfältet **Token Name**.<br> ・ Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitHub-dokumentationen](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<br> ・ behörigheter krävs:<br>  ・ `Read access to metadata`<br>  ・ `Read and write access to code and pull requests`.<br> ・ Klistra in den token du just skapade i fältet **Åtkomsttoken**. |
   |  | **Databastyp: GitLab**<br> ・ Ange ett namn för åtkomsttoken som du skapar i textfältet **Token Name**.<br> ・ Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitLab-dokumentationen](https://docs.gitlab.com/user/profile/personal_access_tokens/).<br> ・ behörigheter krävs:<br>  ・ `api`<br>  ・ `read_api`<br>  ・ `read_repository`<br>  ・ `write_repository`<br> ・ Klistra in den token du just skapade i fältet **Åtkomsttoken** . |
   |  | **Databastyp: Bitbucket**<br> ・ I textfältet **Token Name** anger du ett namn för åtkomsttoken som du skapar.<br> ・ Skapa en databasåtkomsttoken med hjälp av [Bitbucket-dokumentationen](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<br> ・ behörigheter krävs:<br>  ・ `Read and write access to code and pull requests` |

   >[!NOTE]
   >
   >Funktionen **Lägg till ny åtkomsttoken** är för närvarande i fasen Tidiga Adobe-program. Ytterligare funktioner planeras. Därför kan de behörigheter som krävs för åtkomsttoken ändras. Dessutom kan användargränssnittet för hantering av tokens uppdateras, inklusive funktioner som utgångsdatum för token. Och automatiska kontroller för att säkerställa att tokens som är länkade till databaser förblir giltiga.

1. Klicka på **Validera**.

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

## Länka en validerad extern databas till en pipeline {#validate-ext-repo}

1. Lägga till eller redigera en pipeline:
   * [Lägg till en produktionspipeline](/help/using/production-pipelines.md)
   * [Lägga till icke-produktionsrörledningar](/help/using/non-production-pipelines.md)
   * [Redigera en pipeline](/help/using/managing-pipelines.md#editing-pipelines)

   ![Källkodskatalogen för pipeline och Git-grenen](/help/managing-code/assets/pipeline-repo-gitbranch.png)
   *Lägg till icke-produktionsförlopp, dialogruta med vald databas och Git-förgrening,*

1. När du lägger till eller redigerar en pipeline och vill ange platsen **Source-kod** för den nya eller befintliga pipelinen, väljer du den externa databas du vill använda i listrutan **Databas** .

1. I listrutan **Git Branch** väljer du grenen som källa för pipelinen.

1. Klicka på **Spara**.


>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/managing-code/managing-repositories.md).


## Begränsningar

Externa databaser kan inte länkas till konfigurationspipelines.

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY

* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->

