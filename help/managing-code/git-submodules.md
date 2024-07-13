---
title: Stöd för Git-undermodul
description: Lär dig hur du kan använda Git-undermoduler för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.
exl-id: f946d7e7-114a-4e33-bb82-2625d37bba2f
source-git-commit: e93285f7c7495ec9d2f11d289adaf6aaba7e58ea
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Stöd för Git-undermodul för Adobe-databaser {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.

När Cloud Manager byggprocess körs, efter att databasen som konfigurerats för pipelinen har klonats och den konfigurerade grenen har checkats ut, körs kommandot om grenen innehåller en `.gitmodules`-fil i rotkatalogen.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Den här tekniken är ett möjligt alternativ till [att arbeta med flera Git-källdatabaser](/help/managing-code/multiple-git-repos.md) för organisationer som är bekväma med att använda Git-undermoduler och som inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet `main`. I den&quot;primära&quot; databasen, d.v.s. den som konfigurerats i pipelines, har grenen `main` en `pom.xml`-fil som deklarerar projekten i de andra två databaserna:

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

Detta resulterar i en `.gitmodules`-fil som ser ut så här:

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

Mer information om Git-undermoduler finns i [referenshandboken för Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

## Begränsningar {#limitations}

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan.
* Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar.
   * Detta innebär att när ändringar görs i undermodulens databas måste den implementering som refereras uppdateras, till exempel med hjälp av `git submodule update --remote`.
* Om inte annat är nödvändigt rekommenderas starkt att undermoduler av typen&quot;ytlig&quot; används.
   * Det gör du genom att köra `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.


## Stöd för Git-undermodul för privata databaser {#private-repositories}

Stöd för Git-undermoduler när [privata databaser](private-repositories.md) används är i stort sett detsamma som när du använder Adobe-databaser.

När du har konfigurerat din `pom.xml`-fil och kör `git submodule`-kommandona måste du lägga till en `.gitmodules`-fil i rotkatalogen i aggregeringsdatabasen för att Cloud Manager ska kunna identifiera inställningarna för undermodulen.

![.gitmodules-fil](assets/gitmodules.png)

![Aggregator](assets/aggregator.png)

### Begränsningar och Recommendations {#limitations-recommendations-private-repos}

Tänk på följande begränsningar när du använder Git-undermoduler med privata databaser.

* Git-URL:erna för undermodulerna kan antingen vara i HTTPS- eller SSH-format, men de måste länka till en github.com
   * Det går inte att lägga till en undermodul i en GitHub-aggregeringsdatabas eller vice versa om du lägger till en undermodul i Adobe.
* GitHub-undermodulerna måste vara tillgängliga för Adobe GitHub-appen.
* [Begränsningarna för att använda Git-undermoduler med databaser som hanteras med Adobe ](#limitations-recommendations) gäller också.
