---
title: Konfigurera grenar
description: Lär dig hur du konfigurerar din första gren i Git och hur den används av CI/CD-flödet för att distribuera programkoden.
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Konfigurera grenar {#configuring-branches}

Lär dig hur du konfigurerar din första gren i Git och hur den används av CI/CD-flödet för att distribuera programkoden.

## Konfigurera din första gren i Git {#setting-up-your-first-branch-in-git}

En enskild, till att börja med tom, Git-databas [etableras](/help/requirements/environment-provisioning.md) för varje program som introduceras i Cloud Manager. Den här databasen kan innehålla så många grenar som utvecklingsprocessen kräver, men det måste finnas minst en gren som används av CI/CD-pipeline för att distribuera programkod till scenen och produktionen. Det bästa sättet är att använda `main` som namn på den här grenen. Detta är bekvämt standardbeteendet för Git-klienter när nya projekt skapas.

När du till exempel skapar ett nytt projekt kör du en uppsättning kommandon som liknar följande.

```shell
$ git init
Initialized empty Git repository in /Users/myname/workspace/new-project/.git/
... steps which add Maven build files and source code ...
$ git add pom.xml core/pom.xml core/src ui.apps/pom.xml ui.apps/src
$ git commit -m "initial commit"
 19 files changed, 777 insertions(+)
 create mode 100644 core/pom.xml
 create mode 100644 pom.xml
 create mode 100644 ui.apps/pom.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/config.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/definition/.content.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/filter.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/nodetypes.cnd
 create mode 100644 ui.apps/src/main/content/META-INF/vault/properties.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/apps/my-aem-project/install/.vltignore
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/_rep_policy.xml
```

>[!NOTE]
>
>Det är inte ett krav att använda kommandoradsklienten. Det finns en mängd grafiska Git-klienter som kan användas antingen som fristående program eller som en del av en integrerad utvecklingsmiljö, till exempel Eclipse eller IntelliJ. Så länge klientprogrammet stöder Git med HTTPS bör det vara kompatibelt med [!UICONTROL Cloud Manager].

## Tryck din första gren {#pushing-your-first-branch}

När du har implementerat minst en revision kan du lägga till databasen [!UICONTROL Cloud Manager] som en fjärrdatabas och sedan skicka dina implementeringar till den.

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      main -> main
```

>[!NOTE]
>
>Den specifika URL:en, tillsammans med dina autentiseringsuppgifter, tillhandahålls av din Adobe CSE (Customer Success Engineer) under [!UICONTROL Cloud Manager]-introduktionen.

## Ytterligare grenar {#additional-branches}

En enskild `main`-gren kan räcka för mycket enkla projekt, men i de flesta fall krävs en mer komplex förgreningsstrategi. Många kunder följer en process där dagliga utvecklingsaktiviteter utförs på en gren som kallas `develop`. `develop`-grenen sammanfogas sedan i `main`-grenen när det är dags för en distribution.

>[!TIP]
>
>Mer information om vanliga Git-kommandon finns i [Git-värmebladet](https://training.github.com/downloads/github-git-cheat-sheet).
