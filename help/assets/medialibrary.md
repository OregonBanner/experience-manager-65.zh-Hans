---
title: 将Media Library用于基本数字资产管理
description: '"[!DNL Experience Manager Assets] 和Media Library进行资产管理。”'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# 将Media Library用于基本资产管理 {#manage-assets-using-media-library}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager] platform提供了不同的资产管理功能。 Media Library允许用户将少量资产上传到存储库、搜索和使用网页中的资产，并完成资产上的简单资产管理任务。

Media Library是一款轻量级的数字资产管理(DAM)解决方案，与 [!DNL Adobe Experience Manager Sites] 许可证。 [!DNL Sites] 是Web内容管理(WCM)产品。 Media Library可与所有Experience Manager功能配合使用。

[!DNL Adobe Experience Manager Assets] 许可证可单独购买。 [!DNL Experience Manager Assets] 允许通过企业用例、元数据、架构、搜索和用户界面的自定义，以及Media Library提供的其他许多功能，对资产进行可靠处理。

## 许可要求 {#avail-media-library-license}

具有 [!DNL Sites] 许可证有权使用Media Library。 它适用于 [!DNL Experience Manager].

Media Library将作为Sites的一部分进行安装。 除Sites许可证和安装之外，无需其他许可证或包。

## [!DNL Assets] 与Media Library {#assets-and-media-library}

Experience Manager Assets提供企业级DAM功能。 资产功能通过 [!DNL Experience Manager] 在一个包中。 但是，未购买资产许可证的用户无权使用高级DAM功能。 在没有资产许可证的情况下，仅 [Media Library功能](#use-media-library) 中。

如果要防止意外使用 [!DNL Assets] 您尚未获得许可的功能，然后删除所有 [!DNL Assets]特定的工作流、组件、分类、选项和 [!DNL Assets] 管理员 [!DNL Experience Manager]. 这样可防止用户意外使用 [!DNL Assets] 您未获得许可的功能。

## 使用Media Library {#use-media-library}

Media Library为以下用例提供了基本的DAM功能：

* 使用创建的网页 [!DNL Adobe Experience Manager Sites].
* 使用创建的自适应表单和通信 [!DNL Adobe Experience Manager Forms].
* 使用创建的数字屏幕体验 [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 用于无头操作的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

要使用Media Library功能，您可以使用默认 [!DNL Experience Manager] 用户界面。 Media Library是 [!DNL Experience Manager Sites] 无需安装单独的界面或附加组件。 使用现有界面，Media Library用户有权完成以下任务：

* 创建文件夹以组织资产。
* 上传资源.
* 发布资产。
* 编辑、移动和复制资产。
* 浏览、过滤和搜索（包括相似性搜索）资产。
* 向中添加值并编辑元数据字段（智能标记字段除外）中的值，这些值在 [!UICONTROL 基本] 选项卡 [!UICONTROL 属性] 页面。
* 添加和删除静态演绎版。
* 下载文件夹、资产和资产演绎版。
* 创建资产版本。
* 创建并执行资产审核任务。
* 在资产中添加批注。
* 将资产添加到 [!DNL Sites] 页面。
* 用法 [!DNL Content Fragments].
* 使用HTTP REST和GraphQL API [!DNL Content Fragments] 和引用的媒体资产（根据“站点”许可证）。
* Marketing Cloud集成。
* 自定义和扩展资产管理用户界面。
* 访问查询生成器(API)以扩展搜索功能。
* 创建静态标记。
* 创作项目和任务。
* 活动流（时间轴）。
* 注释和批注。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>许多高级DAM用例由 [!DNL Experience Manager Assets]. Media Library许可证授权您使用Media Library仅执行列出的用例。 如果未列出用例，请勿将其与Media Library许可证结合使用。 如果您有任何疑问，请联系Adobe客户支持。

请注意，您不能使用智能标记， [!DNL Asset] 链接， [!DNL Asset] 选择器、批量标记、修改资产工作流或标准 [!DNL Adobe Experience Manager] 用户界面访问Media Library，而 [!DNL Assets] 许可证。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5Managed Services产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5内部部署产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

