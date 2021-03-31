---
title: 将媒体库用于基本数字资产管理
description: '[!DNL Experience Manager Assets] 和媒体库，以便进行资源管理。'
contentOwner: AG
role: 架构师、领导者
feature: 资产管理
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 使用媒体库进行基本资源管理{#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] 平台提供了不同的资产管理功能。媒体库允许用户将少量资产上传到存储库、搜索和使用网页中的资产，并完成对资产的简单资产管理任务。

媒体库是一个轻量级数字资产管理(DAM)解决方案，随[!DNL Adobe Experience Manager Sites]许可证提供。 [!DNL Sites] 是Web内容管理(WCM)产品。媒体库可用于所有Experience Manager功能。

[!DNL Adobe Experience Manager Assets] 许可证可单独购买。[!DNL Experience Manager Assets] 允许通过企业用例、元数据、模式、搜索和用户界面的自定义设置以及媒体库提供之外的许多其他功能，对资产进行强大处理。

## 许可要求{#avail-media-library-license}

拥有[!DNL Sites]许可证的客户有权使用媒体库。 它适用于[!DNL Experience Manager]的所有组件。

媒体库作为站点的一部分进行安装。 除站点许可和安装之外，无需任何其他许可或包。

## [!DNL Assets] 与媒体库  {#assets-and-media-library}

Experience Manager资产提供企业级DAM功能。 资产功能通过[!DNL Experience Manager]在一个包中提供。 但是，尚未购买资产许可证的用户无权使用高级DAM功能。 没有“资源”许可证，只有[媒体库功能](#use-media-library)可用。

如果您希望防止意外使用您未获得许可的[!DNL Assets]功能，请从[!DNL Experience Manager]中删除所有特定于[!DNL Assets]的工作流、组件、分类、选项和[!DNL Assets]管理员。 这样做可防止用户意外使用您未授权的[!DNL Assets]功能。

## 使用媒体库{#use-media-library}

媒体库广泛涵盖以下用例：

* 为使用[!DNL Adobe Experience Manager Sites]创建的网页提供基本的DAM功能。
* 使用[!DNL Adobe Experience Manager Forms]创建的自适应表单和通信。
* 使用[!DNL Adobe Experience Manager Screens]创建的数字屏幕体验。
* [!DNL Assets] 用于无头操作的HTTP REST API。

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

要使用媒体库功能，可以使用默认的[!DNL Experience Manager]用户界面。 媒体库是[!DNL Experience Manager Sites]安装的一部分，不需要任何单独的接口或加载项。 使用现有界面，媒体库用户有权完成以下任务:

* 创建文件夹以组织资产。
* 上传资产。
* 发布资产。
* 编辑、移动和复制资产。
* 浏览、筛选和搜索（包括相似性搜索）资产。
* 在元数据字段中添加值并编辑这些值，但“智能标记”字段除外。默认情况下，这些值位于资产[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡中。
* 添加和删除静态演绎版。
* 下载文件夹、资产和资产演绎版。
* 创建资产版本。
* 为资产创建和执行审核任务。
* 注释资产。
* 通过内容查找器将资产添加到[!DNL Sites]页面。
* 用法 [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>许多高级DAM使用案例由[!DNL Experience Manager Assets]完成。 媒体库许可允许您使用媒体库仅履行列出的使用案例。 如果未列出用例，请勿将其与媒体库许可证一起使用。 如果您有任何查询，请与Adobe客户关怀联系。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5内部部署产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

