---
title: 升级到 AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: 您可以从AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升级到AEM 6.3 Forms。
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 2e6d688818e9cc337444bcda2a49485e9167a113
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%

---

# 在JEE上升级到AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms on JEE提供了两种类型的安装程序：完整安装程序和修补程序安装程序。

**完整安装程序**:您可以使用 [AEM 6.5.12.0 on JEE full installer](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 要设置新的AEM Forms实例，或从JEE上的AEM 6.3 Forms、JEE上的AEM 6.4执行升级，以及从JEE上的AEM 6.5.x.x Forms到JEE上的AEM 6.5.12.0 Forms的就地升级。

**修补程序安装程序**: [AEM 6.5.12.0 on JEE补丁安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 适用于已使用AEM 6.5.x.x版本的客户。 您可以使用修补程序安装程序升级到最新版本的AEM Forms。

下表描述了使用完整和修补程序安装程序的传感器。

![](assets/full-and-patch-installer.png)

请执行以下步骤以使用完整安装程序将JEE上的现有AEM 6.3 Forms或JEE上的AEM 6.4 Forms升级到JEE上的AEM 6.5.12.0 Forms:

1. 从JEE安装程序下载AEM 6.5 Forms [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 要使用安装程序，您需要签订有效的维护和支持合同。
1. 请参阅 [升级核对清单和规划](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 了解要执行的检查以确保成功升级。
1. 请参阅 [准备升级到AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 学习和执行任务，以确保升级在服务器停机时间最短的情况下正常运行。
1. 根据您现有的环境和应用程序服务器，选择以下文档之一并按照说明操作。

   * [从AEM 6.3或AEM 6.4 Forms升级到适用于JBoss的AEM 6.5 Forms](http://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for WebSphere](http://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for JBoss Turnkey](http://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

无法直接从LiveCycleES2、LiveCycleES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms升级到AEM 6.5 Forms。 您可以执行到一个或多个版本的LiveCycle或AEM Forms的中间升级，然后升级到AEM 6.5 Forms。 有关中间版本的列表和相应的升级说明，请参阅 [选择升级路径](upgrade.md).
