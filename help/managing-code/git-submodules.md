---
title: Stöd för Git-undermodul
description: Lär dig hur du kan använda Git-undermoduler för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.
source-git-commit: aa30c0024e422c96f0dfbaa2804e75143faf14dc
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---


# Stöd för Git-undermodul för Adobe-databaser {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.

När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen klonats och den konfigurerade grenen checkas ut, om grenen innehåller en `.gitmodules` -filen i rotkatalogen körs kommandot.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Detta är ett möjligt alternativ till [arbeta med Git-databaser med flera källor](/help/managing-code/multiple-git-repos.md) för organisationer som känner sig bekväma med att använda Git-undermoduler och inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet `main`. I den&quot;primära&quot; databasen, dvs. den som konfigurerats i pipelines, `main` grenen har en `pom.xml` fil som deklarerar projekten i de två andra databaserna:

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

## Begränsningar {#limitations}

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan.
* Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar.
   * När ändringar görs i undermodulens databas måste den implementerade refererade informationen därför uppdateras, till exempel med hjälp av `git submodule update --remote`.
* Om inte annat är nödvändigt rekommenderas starkt att undermoduler av typen&quot;ytlig&quot; används.
   * Om du vill göra det kör du `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.


## Stöd för Git-undermodul för privata databaser {#private-repositories}

Stöd för Git-undermoduler vid användning [privata databaser](private-repositories.md) är i stort sett detsamma som när du använder Adobe-databaser.

När du har konfigurerat `pom.xml` filen och kör `git submodule` -kommandon måste du lägga till `.gitmodules` till rotkatalogen för aggregeringsdatabasen för Cloud Manager för att identifiera inställningarna för undermodulen.

![.gitmodules-fil](assets/gitmodules.png)

![Aggregator](assets/aggregator.png)

### Begränsningar och Recommendations {#limitations-recommendations-private-repos}

Tänk på följande begränsningar när du använder Git-undermoduler med privata databaser.

* Git-URL:erna för undermodulerna kan antingen vara i HTTPS- eller SSH-format, men de måste länka till en github.com
   * Det går inte att lägga till en undermodul i en GitHub-aggregeringsdatabas eller vice versa om du lägger till en undermodul i Adobe.
* GitHub-undermodulerna måste vara tillgängliga för Adobe GitHub-appen.
* [Begränsningarna med att använda Git-undermoduler med databaser som hanteras av Adobe](#limitations-recommendations) gäller också.