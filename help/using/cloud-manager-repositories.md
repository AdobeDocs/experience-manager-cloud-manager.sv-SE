---
title: Cloud Manager-databaser
description: Cloud Manager-databaser
source-git-commit: 7bda34be143d2d7587e61c09dab642f3419dfad9
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Cloud Manager-databaser {#cloud-manager-repos}

Databaser som skapas och är tillgängliga i Cloud Manager kan visas och hanteras via sidan Databaser.

## Lägga till och hantera databaser {#add-manage-repos}

Följ stegen nedan för att visa och hantera databaser i Cloud Manager:

1. På sidan **Programöversikt** klickar du på fliken **Databaser** och går till sidan **Databaser**.

1. Klicka på **Lägg till databas** för att starta guiden.

   >[!NOTE]
   >En användare i rollen Distributionshanterare eller Affärsägare måste vara inloggad för att kunna lägga till en databas.

   ![](assets/create-repo2.png)


1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![](assets/repo-1.png)

1. Välj **Spara**. Din nyskapade rapport visas i tabellen enligt nedan.

   ![](assets/create-repo3.png)

   >[!NOTE]
   >Databaser som skapas i Cloud Manager är också tillgängliga så att du kan välja bland dem under stegen för att lägga till eller redigera pipeline.

1. Du kan markera databasen och klicka på menyalternativen längst till höger i tabellen till **Kopiera databas-URL**, **Visa och uppdatera** eller **Ta bort** databasen, vilket visas i bilden nedan.

   ![](assets/create-repo3.png)



## Stöd för Git-undermodul {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället. När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen har klonats och den konfigurerade grenen har checkats ut, körs kommandot om grenen innehåller en `.gitmodules`-fil i rotkatalogen.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Den här tekniken är ett möjligt alternativ till https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html för organisationer som är bekväma med att använda Git-undermoduler och som inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet main . I den&quot;primära&quot; databasen, d.v.s. den som konfigurerats i pipelines, har huvudgrenen en pom.xml-fil som deklarerar projekten i de två andra databaserna:

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

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Detta resulterar i en `.gitmodules`-fil som ser ut så här:

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Mer information om Git-undermoduler finns i [referenshandboken för Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan. Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar. När ändringar görs i undermodulens databas måste därför den implementering som refereras uppdateras, till exempel med `git submodule update --remote` .

