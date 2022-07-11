---
title: Cloud Manager-databaser
description: Lär dig hur du får tillgång till, skapar och redigerar databaser för dina Cloud Manager-program.
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Cloud Manager-databaser {#cloud-manager-repos}

I databaserna hanterar du koden med Git. Lär dig hur du skapar databaser för dina Cloud Manager-program.

## Åtkomst till databaser {#accessing-repos}

Du kan komma åt och hantera dina Git-databaser via en självbetjäning i Cloud Manager.

Använd **Åtkomst till svarsinformation** som finns i Cloud Manager, mest framträdande på pipeline-kortet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** så ser du **Åtkomst till svarsinformation** möjlighet att komma åt och hantera din Git-databas [har konfigurerats med denna pipeline.](/help/using/production-pipelines.md)

   ![Knapp för att få åtkomst till information om svar](/help/assets/access-repo1.png)

1. Om du växlar till **Icke-produktion** pipeline-fliken, **Åtkomst till svarsinformation** finns även där som [konfigurerad för pipeline.](/help/using/non-production-pipelines.md)

   ![Icke-produktionsrörledningar](/help/assets/access-repo-nonprod.png)

1. Klicka på **Åtkomst till svarsinformation** för att öppna en dialogruta som visar:

   * URL:en till Git-databasen
   * Användarnamn
   * Lösenord
   * Git-kommando som ska köras för att klona databasen lokalt

   ![Dialogrutan Databasinformation](/help/assets/access-repo-create.png)

Använd den angivna informationen för att klona databasen lokalt så att du kan påbörja den lokala utvecklingen.

>[!NOTE]
>
>The **Åtkomst till svarsinformation** är synligt för användare i **Utvecklare** eller **Distributionshanteraren** roll.

## Lägga till databaser {#add-repos}

Så här lägger du till databaser i Cloud Manager:

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** sida, klicka på **Databaser** och navigera till **Databaser** sida.

1. Klicka på **Lägg till databas** för att starta guiden.

   >[!NOTE]
   >
   >Du måste ha **Distributionshanteraren** eller **Företagsägare** roll för att lägga till en databas.

   ![Lägg till databas](/help/assets/create-repo2.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![Uppgifter om svaret](/help/assets/repo-1.png)

1. Välj **Spara**.

Din nyskapade rapport visas.

![Ny rapport har skapats](/help/assets/create-repo3.png)

Databaser som skapas i Cloud Manager är tillgängliga att välja när du [skapa dina rörledningar.](/help/overview/ci-cd-pipelines.md)

## Visa och redigera databaser {#edit-repos}

Så här redigerar och visar du databaser i Cloud Manager:

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** sida, klicka på **Databaser** och navigera till **Databaser** sida. Här kan du visa information om dina befintliga databaser.

1. Markera databasen och klicka på ellipsknappen längst till höger i tabellen för att **Kopiera databas-URL**, **Visa och uppdatera** eller **Ta bort** din databas.

![Redigera svar](/help/assets/create-repo3.png)

## Stöd för Git-undermodul {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.

När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen klonats och den konfigurerade grenen checkas ut, om grenen innehåller en `.gitmodules` -filen i rotkatalogen körs kommandot.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Den här tekniken är ett möjligt alternativ till [arbeta med Git-databaser med flera källor](/help/managing-code/multiple-git-repos.md) för organisationer som känner sig bekväma med att använda Git-undermoduler och inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet `main`. I den&quot;primära&quot; databasen, dvs. den som är konfigurerad i pipelines, `main` grenen har en `pom.xml` fil som deklarerar projekten i de två andra databaserna:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

Sedan lägger du till undermoduler för de två andra databaserna:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Detta resulterar i en `.gitmodules` fil som ser ut så här:

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Mer information om Git-undermoduler finns i [Handbok för Git-referens](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### Begränsningar {#limitations}

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan.
* Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar.
   * När ändringar görs i undermodulens databas måste den implementerade refererade informationen därför uppdateras, till exempel med hjälp av `git submodule update --remote`.
* Om inte annat är nödvändigt rekommenderas starkt att undermoduler av typen&quot;ytlig&quot; används.
   * Om du vill göra det kör du `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.
