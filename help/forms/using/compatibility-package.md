---
title: 兼容包
description: 通过在AEM Forms 6.5上安装兼容包，您可以使用AEM Forms 6.4及更早版本中的通信管理资源以及已弃用的自适应表单模板和页面
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 2%

---

# 兼容包{#compatibility-package}

## 概述 {#overview}

在AEM Forms 6.5中创建客户通信的默认和推荐方法是交互式通信。要继续使用AEM Forms 6.5中的字母，您需要安装最新的 [AEMFD兼容包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

AEMFD兼容包还允许您 [在AEM Forms 6.5上使用AEM Forms 6.4、6.3和6.2中的以下资源：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 文档片段
* 书信
* 数据字典
* 自适应表单弃用的模板和页面

有关更多信息，请参阅 [通过安装兼容包，使资源与AEM Forms 6.5兼容](../../forms/using/compatibility-package.md#assetsmadecompatible).

## 在AEM Forms 6.5中添加对AEM Forms 6.4、6.3和6.2资源的支持 {#add-support-for-aem-forms-and-assets-in-aem-forms}

执行升级后，请执行以下操作以安装AEMFD兼容包，并使您的资产与6.5兼容：

确保您拥有 [AEM兼容包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 已预安装。

1. 安装最新的6.5 [兼容包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   有关上载和安装软件包的更多信息，请参阅 [如何使用包](/help/sites-administering/package-manager.md).

1. 在日志稳定后，重新启动服务器。
1. 使用迁移实用程序使您的资产与6.5兼容。

   有关更多信息，请参阅 [迁移实用程序](../../forms/using/migration-utility.md).

## 通过安装兼容包，使资源与AEM Forms 6.5兼容 {#assetsmadecompatible}

通过安装兼容包，您可以使以下资源和模板与AEM Forms 6.5兼容：

* AEM 6.4及更早版本中的通信管理资源：

   * [书信](../../forms/using/create-letter.md)
   * [数据字典](/help/forms/using/data-dictionary.md)
   * 文档片段

* 自适应表单已弃用的模板：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 自适应表单已弃用页面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
