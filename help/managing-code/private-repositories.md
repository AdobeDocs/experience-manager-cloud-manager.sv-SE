---
title: Lägg till privata databaser i Cloud Manager
description: Lär dig hur du konfigurerar Cloud Manager så att det fungerar med dina egna privata GitHub-databaser.
feature: Release Information
exl-id: e0d103c9-c147-4040-bf53-835e93d78a0b
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Lägga till privata databaser i Cloud Manager {#private-repositories}

Lär dig hur du konfigurerar Cloud Manager så att det fungerar med dina egna privata GitHub-databaser.

## Ökning {#overview}

När du konfigurerar Cloud Manager med dina privata GitHub-databaser kan du validera koden direkt i GitHub, vilket eliminerar behovet av att synkronisera med Adobe-databasen ofta.

>[!NOTE]
>
>Den här funktionen är exklusiv för public GitHub. Det finns inget stöd för GitHub som är självvärd.

## Konfiguration {#configuration}

Konfigurationen består av två huvudsteg:

1. [Lägg till databas](#add-repo)
1. [Validering av ägarskap för privat databas](#validate-ownership)



### Lägga till en databas {#add-repo}

1. Gå till sidan **Programöversikt** i Cloud Manager och klicka på fliken **Databaser** för att växla till sidan **Databaser** och sedan på **Lägg till databas**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** som databastyp.

1. Ange information om din databas

   * **Databasnamn** - ett uttrycksfullt namn
   * **Databas-URL** - Databasens URL, som måste sluta med `.git`
   * **Beskrivning** (valfritt) - En längre beskrivning av databasen efter behov

   ![Lägg till egen databas](/help/assets/repositories/add-own-github.png)

1. Klicka på **Spara**.

>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/managing-code/managing-repositories.md).



### Validera ägarskap för en privat databas {#validate-ownership}

Cloud Manager känner nu till din GitHub-databas, men den behöver fortfarande åtkomst till den. Om du vill bevilja åtkomst måste du installera Adobe GitHub-appen och verifiera att du äger den angivna databasen.

1. När du har lagt till din egen databas visas dialogrutan **Validering av privat databasägande**.

   ![Verifiering av privat databasägande](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager använder en GitHub-app för att interagera med din databas på ett säkert sätt.

   En ägare till din GitHub-organisation måste installera appen som finns på `https://github.com/apps/cloud-manager-for-aem` och bevilja åtkomst till databasen. Mer information finns i dokumentationen för GitHub.

1. Om du vill förbättra säkerheten skapar du en hemlig fil i databasens standardgren. Klicka på **Generera**.

1. Bekräfta genereringen av den hemliga filen genom att klicka på **Bekräfta**.

   ![Bekräfta hemlig generering](/help/assets/repositories/confirm-generation.png)

1. I dialogrutan **Validering av privat databasägande** har Cloud Manager genererat innehållet i fältet **Hemligt filinnehåll**. Kopiera innehållet från det fältet.

   Innehållet i den hemliga filen visas bara en gång. Om du inte kopierar innehållet innan du stänger det här fönstret måste du återskapa hemligheten.

   ![Kopiera hemligt filinnehåll](/help/assets/repositories/new-secret.png)

1. Skapa en ny fil i standardgrenen för GitHub-repon med namnet `.well-known/adobe/cloud-manager-challenge` och klistra in det hemliga filinnehållet i den filen och spara.

1. När appen har installerats och den hemliga filen finns i databasen kan du klicka på **Validera** i dialogrutan **Validering av privat databasägande**.

Programmet kan installeras och du kan generera en hemlig fil i vilken ordning som helst. Båda stegen måste dock slutföras innan du kan validera.

Till valideringen visas databasen med en röd ikon, som anger att den ännu inte har validerats och inte kan användas.

![Ovaliderat svar](/help/assets/repositories/unvalidated-repo.png)

Observera att kolumnen **Type** enkelt identifierar databaser som tillhandahålls av Adobe (**Adobe**) och dina egna GitHub-databaser (**GitHub**).

Gå till sidan **Databaser** om du vill gå tillbaka till databasen senare och slutföra valideringen. Klicka på ikonen ![Mer, ellipsen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid GitHub-databasen som du lade till och klicka sedan på **Verifiering av ägarskap**.


## Använda privata databaser med Cloud Manager {#using}

När GitHub-databasen har validerats i Cloud Manager slutförs integreringen och du kan använda databasen med Cloud Manager.

**Så här använder du privata databaser med Cloud Manager:**

1. När du skapar en pull-begäran startas en GitHub-kontroll automatiskt.

   ![GitHub-kontroller](/help/assets/repositories/github-checks.png)

1. För varje pull-begäran skapas automatiskt en [fullständig kvalitetspipeline för stackkod](/help/using/managing-pipelines.md). Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

1. GitHub-kontrollen fortsätter att vara i ett körningsläge tills kodkvalitetskontrollerna har slutförts. Kodkvalitetsresultaten sprids sedan till GitHub-kontrollen.

   ![Kvalitetskontroller för GitHub-kod](/help/assets/repositories/github-code-quality.png)

När pull-begäran stängs eller sammanfogas, tas hela stackkodens kvalitetsflöde som skapas automatiskt bort.

>[!TIP]
>
>I dokumentet [GitHub Check Annotations](github-annotations.md) finns mer information om den information som ges via GitHub när pull-begärandekontroller körs.

>[!TIP]
>
>Du kan styra de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas. Mer information finns i [GitHub-kontrollkonfigurationen för privata databaser](github-check-config.md).



## Associera privata databaser med rörledningar {#pipelines}

Validerade privata databaser kan associeras med [rörledningar i full hög och i framtend](/help/overview/ci-cd-pipelines.md).



## Begränsningar {#limitations}

Vissa begränsningar gäller när du använder privata databaser med Cloud Manager.

* Rörledningar för webbnivå och konfiguration stöds inte i privata databaser.
* Ingen Git-tagg skapas och skickas när privata databaser används i produktion av rörledningar i en hel hög.
* Om Adobe GitHub-appen tas bort från din GitHb-organisation tar den här åtgärden bort pull-begärandevalideringsfunktionen för alla databaser.
* Pipeliner som använder privata databaser och utlösaren för bygge som inte har implementerats startas inte automatiskt när en ny implementering överförs till den valda grenen.
* [Återanvändning av felaktigheter](/help/getting-started/project-setup.md#build-artifact-reuse) gäller inte för privata databaser.
* Du kan inte pausa pull-begärandevalideringen med GitHub-kontrollen från Cloud Manager. Om GitHub-databasen valideras i Cloud Manager försöker Cloud Manager validera pull-begäranden som skapas för den databasen.
