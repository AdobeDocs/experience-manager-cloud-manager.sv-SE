---
title: Arbeta med flera Git-databaser
description: Lär dig hur du kan arbeta med din egen Git-databas eller flera Git-databaser i stället för att arbeta direkt med Cloud Manager Git-databas.
exl-id: 53bf78bb-489a-4a83-8459-c361f532d54a
source-git-commit: f855fa91656e4b3806a617d61ea313a51fae13b4
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# Arbeta med Git-databaser med flera källor {#working-with-multiple-source-git-repos}

Lär dig hur du kan arbeta med din egen Git-databas eller flera Git-databaser i stället för att arbeta direkt med Cloud Manager Git-databas.

## Synkronisera kundhanterade Git-databaser {#syncing-customer-managed-git-repositories}

Om du vill att Cloud Manager Git-databas ska vara uppdaterad, skapar du en automatisk synkroniseringsprocess om du använder din egen databas eller databaser.

Beroende på var din Git-databas ligger kan en GitHub-åtgärd eller en kontinuerlig integreringslösning som Jenkins användas för att konfigurera automatiseringen. Med en automatisering på plats kan varje överföring till din egen databas automatiskt vidarebefordras till Cloud Manager Git-databas.

En sådan automatisering för en enskild kundägd Git-databas är enkel, men att konfigurera den för flera databaser kräver en mer komplicerad inledande konfiguration. Innehållet från flera Git-databaser måste mappas till olika kataloger i en och samma Cloud Manager Git-databas. Cloud Manager Git-databas måste etableras med en rotmask `pom.xml`, som listar de olika delprojekten i modulavsnittet

Nedan visas ett exempel på `pom.xml` för två kundägda Git-databaser. Det första projektet placeras i katalogen `project-a` och det andra projektet placeras i katalogen `project-b`.

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

En sådan rot `pom.xml` skickas till en gren i Cloud Manager Git-databasen. Därefter måste de två projekten konfigureras så att ändringarna automatiskt vidarebefordras till Cloud Manager Git-databasen.

En överföring till en gren i projekt A kan till exempel utlösa en GitHub-åtgärd. Åtgärden checkar ut projekt A och Cloud Manager Git-databasen. Det kopierar allt innehåll från projekt A till katalogen `project-a` i Cloud Manager Git-databasen. Sedan implementeras och push-ändras ändringen.

En ändring av grenen `main` i projekt A skickas till exempel automatiskt till grenen `main` i Cloud Manager Git-databasen. Det kan förstås finnas en mappning mellan grenar, som en push-överföring till en gren med namnet `dev` i projekt A, som skickas till en gren med namnet `development` i Cloud Manager Git-databasen. Liknande steg krävs för projekt B.

Beroende på förgreningsstrategin och arbetsflödena kan synkroniseringen konfigureras för olika grenar. Om den använda Git-databasen inte tillhandahåller ett koncept som liknar GitHub-åtgärder, kan en integrering med Jenkins (eller liknande) också göras. I det här fallet utlöser en webkrok ett Jenkins-jobb som utför arbetet.

Gör följande för att lägga till en ny (tredje) källa eller databas:

1. Lägg till en ny GitHub-åtgärd i den nya databasen som överför ändringar från den databasen till Cloud Manager Git-databasen.
1. Utför den åtgärden minst en gång för att se till att projektkoden finns i Cloud Manager Git-databasen.
1. Lägg till en referens till den nya katalogen i rotkatalogen `pom.xml` i Cloud Manager Git-databasen.

## Exempel på GitHub-åtgärd {#sample-github-action}

En push-överföring till `main`-grenen utlöser den här GitHub-åtgärden som sedan skickas till en underkatalog till Cloud Manager Git-databasen. GitHub-åtgärderna måste ha två hemligheter, `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta och skicka till Cloud Manager Git-databas.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

Så som visas ovan är det flexibelt att använda en GitHub-åtgärd. Alla mappningar mellan grenar i Git-databaserna kan utföras och alla mappningar av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>
>Skriptet ovan använder `git add` för att uppdatera databasen, vilket förutsätter att borttagningar inkluderas. Beroende på standardkonfigurationen för Git kan detta krav behöva ersättas med `git add --all`.

## Exempel på Jenkins-jobb {#sample-jenkins-job}

Skriptet är ett exempel som kan användas i ett Jenkins-jobb eller liknande. En ändring i en Git-databas utlöser den. Jenkins-jobbet checkar ut det senaste läget för projektet eller grenen och utlöser sedan det här skriptet.

Skriptet checkar i sin tur ut Cloud Manager Git-databas och implementerar projektkoden i en underkatalog.

Jenkins-jobbet måste ha två hemligheter, `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta och skicka till Cloud Manager Git-databas.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

Så som visas ovan är användningen av ett Jenkins-jobb mycket flexibel. Alla mappningar mellan grenar i Git-databaserna kan utföras och alla mappningar av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>
>Skriptet ovan använder `git add` för att uppdatera databasen, vilket förutsätter att borttagningar inkluderas. Beroende på standardkonfigurationen för Git kan `git add` behöva ersättas med `git add --all`.
