---
title: Arbeta med Git-databaser med flera källor
description: Arbeta med Git-databaser med flera källor - Cloud Manager
feature: Git Repositories
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# Arbeta med Git-databaser med flera källor {#working-with-multiple-source-git-repos}


## Synkroniserar kundhanterade Git-databaser {#syncing-customer-managed-git-repositories}

I stället för att arbeta direkt med Cloud Managers Git-databas kan kunderna arbeta med sina egna Git-databaser eller med flera egna Git-databaser. I dessa fall bör en automatisk synkroniseringsprocess konfigureras för att säkerställa att Cloud Managers Git-databas alltid är uppdaterad. Beroende på var kundens Git-databas finns kan en GitHub-åtgärd eller en kontinuerlig integreringslösning som Jenkins användas för att konfigurera automatiseringen. Med en automatisering på plats kan varje överföring till en kundägd Git-databas automatiskt vidarebefordras till Cloud Managers Git-databas.

En sådan automatisering för en enskild kundägd Git-databas är enkel, men om du konfigurerar den för flera databaser krävs en inledande konfiguration. Innehållet från flera Git-databaser måste mappas till olika kataloger i den enskilda Cloud Managers Git-databas.  Cloud Managers Git-databas måste etableras med en rotmappsruta som listar de olika delprojekten i modulavsnittet

Nedan visas ett exempel på ett badrum för två kundägda Git-databaser: det första projektet placeras i katalogen `project-a`, det andra projektet placeras i katalogen `project-b`.

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

Ett sådant rotrum överförs till en gren i Cloud Managers Git-databas. Därefter måste de två projekten konfigureras för att automatiskt vidarebefordra ändringar till Cloud Managers Git-databas.

En GitHub-åtgärd kan till exempel utlösas av en push-åtgärd till en gren i projekt A. Åtgärden checkar ut projekt A och Cloud Manager Git-databasen och kopierar allt innehåll från projekt A till katalogen `project-a` i Cloud Managers Git-databas och utför sedan ändringen. En ändring av huvudgrenen i projekt A skickas till exempel automatiskt till huvudgrenen i Cloud Managers Git-databas. Det kan förstås finnas en mappning mellan grenar, som en push-funktion till en gren med namnet&quot;dev&quot; i projekt A skickas till en gren med namnet&quot;development&quot; i Cloud Managers Git-databas. Liknande steg krävs för projekt B.

Beroende på förgreningsstrategin och arbetsflödena kan synkroniseringen konfigureras för olika grenar. Om den använda Git-databasen inte innehåller något liknande koncept som GitHub-åtgärder, kan du även integrera via Jenkins (eller liknande). I det här fallet utlöser en webkrok ett Jenkins-jobb som utför arbetet.

Följ stegen nedan för att lägga till en ny (tredje) källa eller databas:

1. Lägg till en ny GitHub-åtgärd i den nya databasen som överför ändringar från den databasen till Cloud Managers Git-databas.
1. Utför den åtgärden minst en gång för att se till att projektkoden finns i Git-databasen i Cloud Manager.
1. Lägg till en referens till den nya katalogen i rotmappen Maven i Cloud Manager Git-databasen.


## Exempel på GitHub-åtgärd {#sample-github-action}

Detta är ett exempel på GitHub-åtgärd som utlöses av en push-åtgärd till huvudgrenen och sedan övergår till en underkatalog till Cloud Managers Git-databas. GitHub-åtgärderna måste innehålla två hemligheter, `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta och överföra till Cloud Managers Git-databas.

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

Så som visas ovan är det mycket flexibelt att använda en GitHub-åtgärd. Alla mappningar mellan grenar i Git-databaserna kan utföras liksom all mappning av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>Skriptet ovan använder `git add` för att uppdatera databasen, vilket förutsätter att borttagningar inkluderas - beroende på standardkonfigurationen för Git måste detta ersättas med `git add --all`.

## Exempel på Jenkins-jobb {#sample-jenkins-job}

Det här är ett exempelskript som kan användas i ett Jenkins-jobb eller liknande. Den aktiveras av en ändring i en Git-databas. Jenkins-jobbet checkar ut det senaste läget för projektet eller grenen och utlöser sedan det här skriptet.

Det här skriptet checkar i sin tur ut Cloud Managers Git-databas och implementerar projektkoden i en underkatalog.

Jenkins-jobbet måste förses med två hemligheter, `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta till och överföra till Cloud Managers Git-databas.

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

Så som visas ovan är användningen av ett Jenkins-jobb mycket flexibel. Alla mappningar mellan grenar i Git-databaserna kan utföras liksom all mappning av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>Skriptet ovan använder `git add` för att uppdatera databasen, vilket förutsätter att borttagningar inkluderas - beroende på standardkonfigurationen för Git måste detta ersättas med `git add --all`.