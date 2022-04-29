---
title: Cloud Manager-databaser
description: Cloud Manager-databaser
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 280d760766cf445e609b865f827c01b4ab1db69c
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Cloud Manager-databaser {#cloud-manager-repos}

Databaser som skapas och är tillgängliga i Cloud Manager kan visas och hanteras via sidan Databaser.

## Lägga till och hantera databaser {#add-manage-repos}

Följ stegen nedan för att visa och hantera databaser i Cloud Manager:

1. Från **Programöversikt** sida, klicka på **Databaser** och navigera till **Databaser** sida.

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

1. Du kan markera databasen och klicka på menyalternativen längst till höger i tabellen för att **Kopiera databas-URL**, **Visa och uppdatera** eller **Ta bort** din databas, enligt bilden nedan.

   ![](assets/create-repo3.png)



## Stöd för Git-undermodul {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället. När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen klonats och den konfigurerade grenen checkas ut, om grenen innehåller en `.gitmodules` -filen i rotkatalogen körs kommandot.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Den här tekniken är ett möjligt alternativ till [arbeta med Git-databaser med flera källor](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html) för organisationer som känner sig bekväma med att använda Git-undermoduler och inte vill hantera en extern sammanfogningsprocess.

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

Detta resulterar i en `.gitmodules` fil som ser ut så här:

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

Mer information om Git-undermoduler finns i [Handbok för Git-referens](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan. Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar. När ändringar görs i undermodulens databas måste den implementerade refererade informationen därför uppdateras, till exempel med hjälp av `git submodule update --remote`.
* Om inte annat är nödvändigt rekommenderas starkt att undermoduler av typen&quot;ytlig&quot; används. Om du vill göra det kör du `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.
