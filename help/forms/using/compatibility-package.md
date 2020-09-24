---
title: 兼容性包
seo-title: 兼容性包
description: 在AEM Forms6.5上安装兼容性软件包可让您使用AEM Forms6.4及更早版本的通信管理资产以及已弃用的自适应表单模板和页面
seo-description: 在AEM Forms6.4上安装兼容性软件包可让您使用AEM Forms6.4和已弃用的自适应表单模板和页面的通信管理资产
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 6%

---


# 兼容性包{#compatibility-package}

## 概述 {#overview}

交互通信是在AEM Forms6.5中创建客户通信的默认和推荐方法。若要在AEM Forms6.5中继续使用字母，您需要安装最新的AEMFD [兼容性包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。

AEMFD兼容性软件包还允许 [您在AEM Forms6.5上使用AEM Forms6.4、6.3和6.2的以下资源：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 文档片段
* 书信
* 数据字典
* 自适应表单已弃用的模板和页面

有关详细信息，请 [参阅通过安装兼容性包使资产与AEM Forms6.5兼容](../../forms/using/compatibility-package.md#assetsmadecompatible)。

## 在AEM Forms6.5中增加对AEM Forms6.4、6.3和6.2资产的支持 {#add-support-for-aem-forms-and-assets-in-aem-forms}

执行升级后，请执行以下操作以安装AEMFD兼容性包并使您的资源与6.5兼容：

确保已预 [装AEM](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) Compatibility包。

1. 安装最新的6.5 [兼容性包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。

   有关上传和安装包的详细信息，请参 [阅如何使用包](/help/sites-administering/package-manager.md)。

1. 日志稳定后，重新启动服务器。
1. 使用迁移实用程序使您的资源与6.5兼容。

   有关详细信息，请参阅 [迁移实用程序](../../forms/using/migration-utility.md)。

## 通过安装兼容性包与AEM Forms6.5兼容的资源 {#assetsmadecompatible}

通过安装兼容性包，您可以使以下资源和模板与AEM Forms6.5兼容：

* AEM 6.4及更早版本的通信管理资产：

   * [书信](../../forms/using/create-letter.md)
   * [数据字典](/help/forms/using/data-dictionary.md)
   * 文档片段

* 自适应表单已弃用模板：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrommentTemplate
   * /libs/fd/af/templates/simpleEngrommentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrommentTemplate
   * /libs/fd/af/templates/tabbedEnmortmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrommentTemplate
   * /libs/fd/afaddon/templates/advancedEnmortmentTemplate2

* 自适应表单已弃用的页面：

   * /libs/fd/af/components/page/调查
   * /libs/fd/af/components/page/tabbedrent
   * /libs/fd/afaddon/components/page/advancedenrollment

