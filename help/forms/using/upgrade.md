---
title: 升级到AEM 6.5 Forms
seo-title: 升级到AEM 6.5 Forms
description: 您可以从AEM 6.3 Forms和AEM 6.4 Forms直接升级到AEM 6.5 Forms。
seo-description: 您可以从AEM 6.3 Forms和AEM 6.4 Forms直接升级到AEM 6.5 Forms。
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# 升级到AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM 6.5 Forms包括若干新增功能和增强功能，可简化表单和通信的创建、管理和用户体验。 要了解AEM 6.5 Forms的所有新增功能和增强功能，请参阅新增 [功能摘要文档](../../forms/using/whats-new.md)。

您可以升级现有LiveCycle或AEM Forms安装，以获得AEM 6.5 Forms中提供的新功能和增强功能，同时保持现有数据、流程和资产不变。 升级时，还会保留元数据和进程的状态。 您可以选择升级途径开始升级。

下图显示了OSGi上AEM Forms的可用升级路径：

![](do-not-localize/osgi-upgrade-path.png)

您可以从以下位置执行直接升级：

* OSGi上的AEM 6.3表单
* OSGi上的AEM 6.4表单

您还可以从

* OSGi上的AEM 6.0 Forms
* OSGi上的AEM 6.1表单
* OSGi上的AEM 6.2 Forms

下图显示了JEE上AEM Forms的可用升级路径：

![](do-not-localize/jee-upgrade-6-5.png)

您可以从以下位置执行直接升级：

* JEE上的AEM 6.3表单
* JEE上的AEM 6.4表单

您还可以从

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* JEE上的AEM 6.0表单
* JEE上的AEM 6.1表单
* JEE上的AEM 6.2表单

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
