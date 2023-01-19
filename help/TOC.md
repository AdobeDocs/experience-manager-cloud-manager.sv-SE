---
product: Adobe Experience Manager
sub-product: Cloud Manager
user-guide-title: Dokumentation om Cloud Manager
breadcrumb-title: Cloud Manager-dokumentation för AEM 6.x
user-guide-description: Lär dig hur du använder Cloud Manager för att självhantera Adobe Experience Manager för AMS i molnet.
feature-set: Experience Manager Cloud Manager, Experience Manager
role: Admin
source-git-commit: b42a849e9e9e776be1b5055971b68fd0c19871e2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 9%

---


# Dokumentation om Cloud Manager {#content}

+ [Cloud Manager för AMS](introduction.md)
+ Översikt {#overview}
   + [Viktiga begrepp](overview/key-concepts.md)
   + [Användarresa](overview/user-journey.md)
   + [CI/CD-rör](overview/ci-cd-pipelines.md)
   + [Säkerhet och integritet](overview/security-and-privacy.md)
   + [Hjälpresurser](overview/help-resources.md)
   + [Vanliga frågor om Cloud Manager](overview/faqs.md)
+ Detta behövs {#requirements}
   + [Åtkomsträttigheter](requirements/access-rights.md)
   + [Databas för källkod](requirements/source-code-repository.md)
   + [Rollbaserade behörigheter](requirements/role-based-permissions.md)
   + [Konfigurera användare och roller](requirements/users-and-roles.md)
   + [Miljöprovisionering](requirements/environment-provisioning.md)
+ Komma igång {#getting-started}
   + [Inloggning för första gången](getting-started/first-time-login.md)
   + [Programinställningar](getting-started/program-setup.md)
   + Skapa AEM projekt {#project-creation}
      + [Använda guiden](getting-started/using-the-wizard.md)
      + [Projektinställningar](getting-started/project-setup.md)
      + [Byggmiljön](getting-started/build-environment.md)
   + [Konfigurera grenar](getting-started/configuring-branches.md)
   + [Dispatcher Configurations](getting-started/dispatcher-configurations.md)
+ Använda {#using}
   + CI/CD-rör {#pipelines}
      + [Konfigurera produktionsförlopp](using/production-pipelines.md)
      + [Konfigurera icke-produktionsförlopp](using/non-production-pipelines.md)
      + [Hantera pipeline](using/managing-pipelines.md)
   + [Koddistribution](using/code-deployment.md)
   + [Testning av kodkvalitet](using/code-quality-testing.md)
   + [Hantera miljöer](using/managing-environments.md)
   + [Övervakningsmiljöer](using/monitoring-environments.md)
   + [API för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)
   + [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager/blob/main/README.md)
   + [Meddelanden](using/notifications.md)
   + [Anpassade regler för kodkvalitet](using/custom-code-quality-rules.md)
   + [Innehållskopia](using/content-copy.md)
+ Hantera kod {#managing-code}
   + [Versionshantering för Maven Project](managing-code/maven-project-version.md)
   + [Databaser](managing-code/repositories.md)
   + [Integrera med Git](managing-code/git-integration.md)
   + [Arbeta med flera Git-databaser](managing-code/multiple-git-repos.md)
+ Produktuppdateringsguide {#product-update-wizard}
   + [Översikt](product-update-wizard/overview.md)
   + [Utvärdering](product-update-wizard/evaluation.md)
+ Versionsinformation {#release-notes}
   + [Aktuell versionsinformation](release-notes/current.md)
   + 2022 {#2022}
      + [Versionsinformation för 2022.12.0](release-notes/2022/2022-12-0.md)
      + [Versionsinformation för 2022.11.0](release-notes/2022/2022-11-0.md)
      + [Versionsinformation för 2022.10.0](release-notes/2022/2022-10-0.md)
      + [Versionsinformation för 2022.9.0](release-notes/2022/2022-9-0.md)
      + [Versionsinformation för 2022.8.0](release-notes/2022/2022-8-0.md)
      + [Versionsinformation för 2022.7.0](release-notes/2022/2022-7-0.md)
      + [Versionsinformation för 2022.6.0](release-notes/2022/2022-6-0.md)
      + [Versionsinformation för 2022.5.0](release-notes/2022/2022-5-0.md)
      + [Versionsinformation för 2022.4.0](release-notes/2022/2022-4-0.md)
      + [Versionsinformation för 2022.3.0](release-notes/2022/2022-3-0.md)
      + [Versionsinformation för 2022.2.0](release-notes/2022/2022-2-0.md)
      + [Versionsinformation för 2022.1.0](release-notes/2022/2022-1-0.md)
   + 2021 {#2021}
      + [Versionsinformation för 2021.12.0](release-notes/2021/2021-12-0.md)
      + [Versionsinformation för 2021.11.0](release-notes/2021/2021-11-0.md)
      + [Versionsinformation för 2021.10.0](release-notes/2021/2021-10-0.md)
      + [Versionsinformation för 2021.9.0](release-notes/2021/2021-9-0.md)
      + [Versionsinformation för 2021.8.0](release-notes/2021/2021-8-0.md)
      + [Versionsinformation för 2021.7.0](release-notes/2021/2021-7-0.md)
      + [Versionsinformation för 2021.6.0](release-notes/2021/2021-6-0.md)
      + [Versionsinformation för 2021.5.0](release-notes/2021/2021-5-0.md)
      + [Versionsinformation för 2021.4.0](release-notes/2021/2021-4-0.md)
      + [Versionsinformation för 2021.3.0](release-notes/2021/2021-3-0.md)
      + [Versionsinformation för 2021.2.0](release-notes/2021/2021-2-0.md)
   + 2020 {#2020}
      + [Versionsinformation för 2020.12.0](release-notes/2020/2020-12-0.md)
      + [Versionsinformation för 2020.11.0](release-notes/2020/2020-11-0.md)
      + [Versionsinformation för 2020.10.0](release-notes/2020/2020-10-0.md)
      + [Versionsinformation för 2020.9.0](release-notes/2020/2020-9-0.md)
      + [Versionsinformation för 2020.8.0](release-notes/2020/2020-8-0.md)
      + [Versionsinformation för 2020.7.0](release-notes/2020/2020-7-0.md)
      + [Versionsinformation för 2020.6.0](release-notes/2020/2020-6-0.md)
      + [Versionsinformation för 2020.5.0](release-notes/2020/2020-5-0.md)
      + [Versionsinformation för 2020.4.0](release-notes/2020/2020-4-0.md)
      + [Versionsinformation för 2020.3.0](release-notes/2020/2020-3-0.md)
      + [Versionsinformation för 2020.2.0](release-notes/2020/2020-2-0.md)
      + [Versionsinformation för 2020.1.0](release-notes/2020/2020-1-0.md)
   + 2019 {#2019}
      + [Versionsinformation för 2019.12.0](release-notes/2019/2019-12-0.md)
      + [Versionsinformation för 2019.11.0](release-notes/2019/2019-11-0.md)
      + [Versionsinformation för 2019.10.0](release-notes/2019/2019-10-0.md)
      + [Versionsinformation för 2019.9.0](release-notes/2019/2019-9-0.md)
      + [Versionsinformation för 2019.8.0](release-notes/2019/2019-8-0.md)
      + [Versionsinformation för 2019.7.0](release-notes/2019/2019-7-0.md)
      + [Versionsinformation för 2019.6.0](release-notes/2019/2019-6-0.md)
      + [Versionsinformation för 2019.5.0](release-notes/2019/2019-5-0.md)
      + [Versionsinformation för 2019.4.0](release-notes/2019/2019-4-0.md)
      + [Versionsinformation för 2019.3.0](release-notes/2019/2019-3-0.md)
      + [Versionsinformation för 2019.2.0](release-notes/2019/2019-2-0.md)
      + [Versionsinformation för 2019.1.0](release-notes/2019/2019-1-0.md)
   + 2018 {#2018}
      + [Versionsinformation för 2018.9.0](release-notes/2018/2018-9-0.md)
      + [Versionsinformation för 2018.8.0](release-notes/2018/2018-8-0.md)
      + [Versionsinformation för 2018.7.0](release-notes/2018/2018-7-0.md)
      + [Versionsinformation för 2018.6.0](release-notes/2018/2018-6-0.md)
      + [Versionsinformation för 2018.5.0](release-notes/2018/2018-5-0.md)
