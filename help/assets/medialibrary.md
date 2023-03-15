---
title: 使用Media Library进行基本的数字资产管理
description: ”[!DNL Experience Manager Assets] 以及Media Library资产管理。”
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---


# 使用Media Library进行基本资源管理 {#manage-assets-using-media-library}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/medialibrary.html?lang=zh-Hans) |

[!DNL Adobe Experience Manager] platform提供了多种不同的功能来管理资产。 Media Library允许用户将少量资源上传到存储库、搜索并使用网页中的资源，以及完成关于资源的简单资源管理任务。

Media Library是一种轻量级数字资产管理(DAM)解决方案，免费提供 [!DNL Adobe Experience Manager Sites] 许可证。 [!DNL Sites] 是一种Web内容管理(WCM)产品。 Media Library可与Experience Manager的所有功能配合使用。

[!DNL Adobe Experience Manager Assets] 许可证可单独购买。 [!DNL Experience Manager Assets] 允许通过企业用例、元数据、架构、搜索和用户界面的自定义以及Media Library提供的功能之外的许多其他功能来稳健地处理资源。

## 许可要求 {#avail-media-library-license}

具有以下特征的客户 [!DNL Sites] 许可证有权使用Media Library。 它适用于的所有组件 [!DNL Experience Manager].

Media Library作为Sites的一部分安装。 在站点许可和安装之外，不需要其他许可证或软件包。

## [!DNL Assets] 对比Media Library {#assets-and-media-library}

Experience Manager Assets提供企业级DAM功能。 Assets功能是通过 [!DNL Experience Manager] 在一个包中。 但是，尚未购买Assets许可证的用户无权使用高级DAM功能。 没有Assets许可证，仅限 [Media Library功能](#use-media-library) 可用。

如果您想防止无意中使用 [!DNL Assets] 您尚未获得许可的功能，然后删除所有 [!DNL Assets]特定工作流、组件、分类、选项和 [!DNL Assets] 管理员来源 [!DNL Experience Manager]. 这样做可防止您的用户意外使用 [!DNL Assets] 您未授权的功能。

## 使用Media Library {#use-media-library}

Media Library为以下用例提供基本DAM功能：

* 使用创建的网页 [!DNL Adobe Experience Manager Sites].
* 使用创建的自适应表单和通信 [!DNL Adobe Experience Manager Forms].
* 使用创建的数字屏幕体验 [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 用于Headless操作的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

要使用Media Library功能，您可以使用默认的 [!DNL Experience Manager] 用户界面。 Media Library是 [!DNL Experience Manager Sites] 无需安装，也不需要单独的界面或插件。 使用现有界面，Media Library用户有权完成以下任务：

* 创建文件夹以组织资源。
* 上传资源.
* 发布资产。
* 编辑、移动和复制资产。
* 浏览、筛选和搜索（包括相似性搜索）资源。
* 向元数据字段中添加值并编辑这些值，但智能标记字段除外，这些字段在 [!UICONTROL 基本] 资产的选项卡 [!UICONTROL 属性] 默认页面。
* 添加和删除静态演绎版。
* 下载文件夹、资源和资源演绎版。
* 创建资源版本。
* 创建资产并执行审核任务。
* 为资源作批注。
* 将资源添加到 [!DNL Sites] 通过“内容查找器”进行分页。
* 用法 [!DNL Content Fragments].
* 将HTTP REST和GraphQL API用于 [!DNL Content Fragments] 和引用的媒体资产，位于Sites许可证下。
* Marketing Cloud集成。
* 自定义和扩展资源管理用户界面。
* 访问查询生成器(API)以扩展搜索功能。
* 创建静态标记。
* 创作项目和任务。
* 活动流（时间线）。
* 注释和批注。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>许多高级DAM用例由完成 [!DNL Experience Manager Assets]. 通过Media Library许可证，您可以使用Media Library仅完成列出的用例。 如果未列出用例，请勿将其与Media Library许可证一起使用。 如果您有任何疑问，请联系Adobe客户支持。

请注意，不能使用智能标记， [!DNL Asset] 链接， [!DNL Asset] 选择器、批量标记、修改资源工作流或标准 [!DNL Adobe Experience Manager] 用于访问Media Library的用户界面，而无需 [!DNL Assets] 许可证。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services产品描述](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5内部部署产品描述](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

