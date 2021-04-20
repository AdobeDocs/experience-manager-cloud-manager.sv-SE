---
title: Konfigurera dina Release-grenar
seo-title: Konfigurera dina Release-grenar
description: Konfigurera frisläppningsgrenar i Git för AEM Cloud Manager
seo-description: Följ den här sidan om du vill veta mer om hur du konfigurerar dina utgivningsgrenar i Git.
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
feature: Git Repositories
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Konfigurera dina Release-grenar {#configure-your-release-branches}

## Konfigurera din första gren i Git {#setting-up-your-first-branch-in-git}

En enskild, inledningsvis tom, **Git-databas** har etablerats för varje program som introduceras i Cloud Manager. Den här databasen kan innehålla så många (eller så få) grenar som utvecklingsprocessen följer, men det måste finnas minst en gren som används av CI/CD-pipeline för att distribuera programkod till scenen och produktionen. Det bästa sättet är att använda `master` som namn på den här grenen. Detta är bekvämt standardbeteendet för Git-klienter när nya projekt konfigureras.

När du skapar ett nytt projekt kommer du att köra en uppsättning kommandon som följande:

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
>Det är inte ett krav att använda kommandoradsklienten. Det finns en mängd grafiska Git-klienter tillgängliga antingen som fristående program eller som en del av en integrerad utvecklingsmiljö (IDE), till exempel Eclipse eller IntelliJ. Så länge klientprogrammet stöder Git med HTTPS bör det vara kompatibelt med [!UICONTROL Cloud Manager].

## Tryck på din första gren {#pushing-your-first-branch}

När du har implementerat minst en revision kan du lägga till databasen [!UICONTROL Cloud Manager] som en **fjärr** och sedan överföra dina implementeringar till den:

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      master -> master
```

>[!NOTE]
>
>Den specifika URL:en, tillsammans med dina inloggningsuppgifter, tillhandahålls av din Customer Success Engineering under [!UICONTROL Cloud Manager]-introduktionen.

## Ytterligare grenar {#additional-branches}

En enskild `master`-gren kan räcka för mycket enkla projekt, men i de flesta fall krävs en mer komplex förgreningsstrategi. Många kunder följer en process där dagliga utvecklingsaktiviteter utförs på en gren som heter `develop` och där framkallningsgrenen slås samman i `master`-grenen när det är dags för en distribution.

>[!NOTE]
>
>Mer information om vanliga Git-kommandon finns i [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet).
