---
title: Konfigurera grenar
description: Lär dig hur du konfigurerar din första gren i Git och hur den används av CI/CD-flödet för att distribuera programkoden.
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: 4c051cd1696f8a00d0278131c9521ad4dcb956a3
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Konfigurera grenar {#configuring-branches}

Lär dig hur du konfigurerar din första gren i Git och hur den används av CI/CD-flödet för att distribuera programkoden.

## Konfigurera din första gren i Git {#setting-up-your-first-branch-in-git}

En enda, inledningsvis tom, Git-databas [har etablerats](/help/requirements/environment-provisioning.md) för varje program som ingår i Cloud Manager. Den här databasen kan innehålla så många grenar som utvecklingsprocessen kräver, men det måste finnas minst en gren som används av CI/CD-pipeline för att distribuera programkod till scenen och produktionen. Det bästa sättet är att använda `main` som namnet på den här grenen. Detta är bekvämt standardbeteendet för Git-klienter när nya projekt konfigureras.

När du skapar ett nytt projekt kommer du att köra en uppsättning kommandon som liknar följande.

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
>Det är inte ett krav att använda kommandoradsklienten. Det finns en mängd olika grafiska Git-klienter som kan användas antingen som fristående program eller som en del av en integrerad utvecklingsmiljö, som Eclipse eller IntelliJ. Så länge klientprogrammet stöder Git med HTTPS bör det vara kompatibelt med [!UICONTROL Cloud Manager].

## Knuffa din första gren {#pushing-your-first-branch}

När du har implementerat minst en revision kan du lägga till [!UICONTROL Cloud Manager] -databasen som en fjärrdatabas och skicka dina implementeringar till den.

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
>Den specifika URL:en, tillsammans med dina inloggningsuppgifter, tillhandahålls av din Customer Success Engineering under [!UICONTROL Cloud Manager] onboarding.

## Ytterligare grenar {#additional-branches}

En enstaka `main` kan räcka för mycket enkla projekt, men i de flesta fall krävs en mer komplex förgreningsstrategi. Många kunder följer en process där den dagliga utvecklingsaktiviteten utförs på en gren som kallas `develop` och utvecklargrenen är kopplad till `main` när det är dags för en distribution.

>[!TIP]
>
>Om du vill visa gemensamma Git-kommandon går du till [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet).
