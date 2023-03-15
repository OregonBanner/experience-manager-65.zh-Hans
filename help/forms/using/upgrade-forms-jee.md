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
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%

---

# 升级到JEE上的AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

JEE上的AEM 6.5.12.0 Forms提供两种类型的安装程序：完整安装程序和修补程序安装程序。

**完整安装程序**：您可以使用 [JEE上的AEM 6.5.12.0完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 设置新的AEM Forms实例，或执行从JEE上的AEM 6.3 Forms、JEE上的AEM 6.4，以及从JEE上的AEM 6.5.x.x Forms到JEE上的AEM 6.5.12.0 Forms的就地升级。

**修补程序安装程序**： [JEE上的AEM 6.5.12.0修补程序安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 适用于已经在使用AEM 6.5.x.x版本的客户。 您可以使用修补程序安装程序升级到AEM Forms的最新版本。

下表描述了使用完整安装程序和修补程序安装程序的方案。

![](assets/full-and-patch-installer.png)

执行以下过程，使用完整安装程序将JEE上的现有AEM 6.3 Forms或JEE上的AEM 6.4 Forms升级到JEE上的AEM 6.5.12.0 Forms：

1. 从下载AEM 6.5 Forms on JEE安装程序 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 您需要有效的维护和支持合同才能使用安装程序。
1. 参见 [升级清单和规划](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 了解为确保成功升级而执行的检查。
1. 参见 [准备升级到AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 了解并执行相关任务，确保升级在最短服务器停机时间下正常运行。
1. 根据您的现有环境和应用程序服务器，选择以下文档之一并按照说明操作。

   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

无法从LiveCycleES2、LiveCycleES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms直接升级到AEM 6.5 Forms。 您可以对LiveCycle或AEM Forms的一个或多个版本执行中间升级，然后升级到AEM 6.5 Forms。 有关中间版本和相应升级说明的列表，请参阅 [选择升级路径](upgrade.md).
