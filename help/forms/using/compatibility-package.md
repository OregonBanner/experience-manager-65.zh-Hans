---
title: 兼容性包
seo-title: 兼容性包
description: 在AEM Forms 6.5上安装兼容性包可让您使用AEM Forms 6.4及早期版本中的Correspondence Management资源以及已弃用的自适应表单模板和页面
seo-description: 在AEM Forms 6.4上安装兼容性包可让您使用AEM Forms 6.4中的Correspondence Management资源和已弃用的自适应表单模板和页面
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 6%

---


# 兼容性包{#compatibility-package}

## 概述 {#overview}

在AEM Forms 6.5中，交互通信是创建客户通信的默认和推荐的方法。要继续在AEM Forms 6.5中使用字母，您需要安装最新的[AEMFD兼容性包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。

AEMFD兼容性包还允许您[在AEM Forms 6.5上使用AEM Forms 6.4、6.3和6.2中的以下资源：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 文档片段
* 书信
* 数据字典
* 自适应表单已弃用的模板和页面

有关详细信息，请参阅[通过安装兼容性包](../../forms/using/compatibility-package.md#assetsmadecompatible)使资产与AEM Forms 6.5兼容。

## 在AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}中添加对AEM Forms 6.4、6.3和6.2资源的支持

执行升级后，请执行以下操作来安装AEMFD兼容性包并使您的资源与6.5兼容：

确保您预装了[AEM Compatibility包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

1. 安装最新的6.5 [兼容性软件包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   有关上载和安装包的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。

1. 日志稳定后，重新启动服务器。
1. 使用迁移实用程序使您的资源与6.5兼容。

   有关详细信息，请参阅[迁移实用程序](../../forms/using/migration-utility.md)。

## 通过安装兼容性包{#assetsmadecompatible}使资源与AEM Forms 6.5兼容

通过安装兼容性包，您可以使以下资源和模板与AEM Forms 6.5兼容：

* 来自AEM 6.4及更早版本的通信管理资产：

   * [书信](../../forms/using/create-letter.md)
   * [数据字典](/help/forms/using/data-dictionary.md)
   * 文档片段

* 自适应表单已弃用模板：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnmortmentTemplate
   * /libs/fd/af/templates/simpleEnmortmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnmortmentTemplate
   * /libs/fd/af/templates/tabbedEnmortmentTemplate2
   * /libs/fd/afaddon/templates/advancedEngromentTemplate
   * /libs/fd/afaddon/templates/advancedEnmortmentTemplate2

* 自适应表单已弃用的页面：

   * /libs/fd/af/components/page/调查
   * /libs/fd/af/components/page/tabberollment
   * /libs/fd/afaddon/components/page/advancedenrollment

