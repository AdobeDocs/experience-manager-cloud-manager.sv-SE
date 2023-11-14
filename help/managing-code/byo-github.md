---
title: Arbeta med dina egna GitHub-databaser i Cloud Manager
description: Lär dig hur du konfigurerar Cloud Manager så att det fungerar med dina egna GitHub-databaser.
feature: Release Information
source-git-commit: 76a3dc6df41032488a3cfe11d0c72769562b96df
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Arbeta med dina egna GitHub-databaser i Cloud Manager {#byo-github}

Genom att konfigurera Cloud Manager så att det fungerar med dina egna GitHub-databaser kan du validera koden direkt i GitHub-databasen via Cloud Manager, så att du slipper synkronisera koden konsekvent med Adobe-databasen.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopteringsprogrammet.](/help/release-notes/current.md#early-adoption)

## Konfiguration {#configuration}

Konfigurationen består av två huvudsteg:

1. [Lägg till databas](#add-repo)
1. [Validering av ägarskap för privat databas](#validate-ownership)

### Lägg till databas {#add-repo}

1. I Cloud Manager kan du gå till **Programöversikt** sida, tryck eller klicka på **Databaser** för att växla till **Databaser** sida och klicka på **Lägg till databas**.

1. I **Lägg till databas** dialogruta, välja **Privat databas** som databastyp.

1. Ange information om din databas

   * **Databasnamn** - Ett uttrycksfullt namn
   * **Databas-URL** - Databasens URL, som måste sluta med `.git`
   * **Beskrivning** (valfritt) - En längre beskrivning av databasen efter behov

   ![Lägg till egen databas](/help/assets/repositories/add-own-github.png)

1. Tryck eller klicka **Spara**.

>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i dokumentet [Databaser för Cloud Manager.](/help/managing-code/repositories.md)

### Validering av privat databasägande {#validate-ownership}

Cloud Manager känner nu till din GitHub-databas, men den behöver fortfarande åtkomst till den. Om du vill bevilja åtkomst måste du installera appen Adobe GitHub och verifiera att du äger den angivna databasen.

1. När du har lagt till en egen databas **Validering av privat databasägande** öppnas.

   ![Validering av privat databasägande](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager använder en GitHub-app för att interagera säkert med din databas.
   * En ägare till din GitHub-organisation måste installera appen som finns på `https://github.com/apps/cloud-manager-for-aem-stage` och ge åtkomst till databasen.
   * Mer information om hur du gör detta finns i dokumentationen för GitHub.

1. För att förbättra säkerheten måste du skapa en hemlig fil i databasens standardgren. Tryck eller klicka **Generera**.

1. Bekräfta genereringen av den hemliga filen genom att trycka eller klicka **Bekräfta**.

   ![Bekräfta hemlig generering](/help/assets/repositories/confirm-generation.png)

1. Tillbaka i **Validering av privat databasägande** har Cloud Manager genererat innehållet i den privata filen i **Hemligt filinnehåll** fält. Kopiera innehållet från det fältet.

   * Innehållet i den hemliga filen visas bara en gång. Om du inte kopierar innehållet innan du stänger det här fönstret måste du generera om hemligheten.

   ![Kopiera hemligt filinnehåll](/help/assets/repositories/new-secret.png)

1. Skapa en ny fil i standardgrenen för GitHub-repon som anropades `.well-known/adobe/cloud-manager-challenge` och klistra in det hemliga filinnehållet i filen och spara.

1. När appen är installerad och den hemliga filen finns i databasen kan du trycka eller klicka på **Validera** i **Validering av privat databasägande** -dialogrutan.

Programmet kan installeras och en hemlig fil kan skapas i vilken ordning som helst. Båda stegen måste dock slutföras innan du kan validera.

Till valideringen visas databasen med en röd ikon, som anger att den ännu inte har validerats och inte kan användas.

![Ovaliderat svar](/help/assets/repositories/unvalidated-repo.png)

Observera att **Typ** kolumnen identifierar enkelt databaser som tillhandahålls av Adobe (**Adobe**) och dina egna GitHub-databaser (**GitHub**).

Om du behöver gå tillbaka till databasen vid ett senare datum för att slutföra valideringen kan du gå till **Databaser** trycker eller klickar du på ellipsknappen på raden som representerar GitHub-databasen som du just lade till och väljer **Ägarverifiering** i listrutan.

## Använda dina egna GitHub-databaser med Cloud Manager {#using}

När GitHub-databasen har validerats i Cloud Manager är integreringen klar och du kan använda databasen med Cloud Manager.

1. När du skapar en pull-begäran startas en GitHub-kontroll automatiskt.

   ![GitHub-kontroller](/help/assets/repositories/github-checks.png)

1. För varje pull-begäran: [pipeline med hög kvalitet för stackkod](/help/using/managing-pipelines.md) skapas automatiskt. Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

1. GitHub-kontrollen fortsätter att vara i ett körningsläge tills kodkvalitetskontrollerna har slutförts. Kodkvalitetsresultaten sprids sedan till GitHub-kontrollen.

   ![Kvalitetskontroller för GitHub-kod](/help/assets/repositories/github-code-quality.png)

När pull-begäran stängs eller sammanfogas, tas hela stackkodens kvalitetsflöde som skapas automatiskt bort.

## Begränsningar {#limitations}

Tänk på följande begränsningar när du använder egna GitHub-databaser med Cloud Manager.

* Du kan inte använda GitHub-databaser som direkt datakälla för de pipelines som du hanterar.
   * Den här funktionen är planerad.
* Du kan inte pausa pull-begärandevalideringen med GitHub-kontrollen från molnhanteraren.
   * Om GitHub-databasen valideras i Cloud Manager försöker Cloud Manager alltid att validera de pull-begäranden som skapas för den databasen.
Om appen Adobe GitHub tas bort från din GitHb-organisation tas valideringsfunktionen för pull-begäranden bort för alla databaser.
