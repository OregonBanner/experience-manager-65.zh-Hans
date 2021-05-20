---
title: 将 [!DNL Assets] 与活动流集成
description: 描述 [!DNL Experience Manager] 的记录功能以及如何将其配置为记录特定事件。
contentOwner: AG
role: Developer
feature: 资产管理
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 将[!DNL Assets]与活动流{#integrating-assets-with-activity-stream}集成

[!DNL Adobe Experience Manager Assets] 用户可执行多项操作，例如创建、上传和删除资产。可以记录这些操作，以便提供用户所执行操作的历史记录。 本节介绍[!DNL Experience Manager]的记录功能以及如何配置[!DNL Experience Manager]以记录特定事件。

## 性能注意事项和默认行为{#performance-considerations-and-default-behavior}

例如，此集成可能占用CPU和磁盘空间，而执行批量导入时则会占用这些空间。 由于这些原因，默认情况下会禁用[!DNL Assets]与活动流的集成。

## 支持的操作事件{#supported-action-events}

可以将以下事件配置为记录：

* 已接受许可证（已接受）
* 已创建资产(ASSET_CREATED)
* 已移动资产(ASSET_MOVED)
* 已删除资产(ASSET_REMOVED)
* 许可证被拒绝（拒绝）
* 已下载资产（已下载）
* 资产版本控制（版本控制）
* 已恢复资产版本（已恢复）
* 更新了资产元数据(METADATA_UPDATED)
* 已发布到外部系统的资产(PUBLISHED_EXTERNAL)
* 资产的原始更新(ORIGINAL_UPDATED)
* 更新了资产演绎版(RENDITION_UPDATED)
* 已删除资产演绎版(RENDITION_REMOVED)
* 更新了子资产(SUBASSET_UPDATED)
* 已删除子资产(SUBASSET_REMOVED)

## 配置记录{#configuring-aem-assets-events-recording}的[!DNL Assets]事件

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供对资产事件记录器调整的访问权限。 要配置资产事件记录器，请按照以下步骤继续操作：

1. 导航到&#x200B;**[!UICONTROL Web控制台]**

1. 单击&#x200B;**[!UICONTROL Configuration]**。

1. 双击&#x200B;**[!UICONTROL Day CQ DAM事件记录器]**。

1. 选中&#x200B;**[!UICONTROL 启用此服务]**。

1. 检查要在用户活动流中记录的&#x200B;**[!UICONTROL 事件类型]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 读取记录的事件{#reading-recorded-events}

记录的事件将存储为活动。 您可以使用[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以编程方式读取它们。
