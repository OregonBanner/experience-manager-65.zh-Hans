---
title: 将 [!DNL Assets] 与活动流集成
description: 描述 [!DNL Experience Manager] 的录制功能，以及如何将其配置为录制特定事件。
contentOwner: AG
role: Developer
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# 将[!DNL Assets]与活动流{#integrating-assets-with-activity-stream}集成

[!DNL Adobe Experience Manager Assets] 用户可执行许多操作，如创建、上传和删除资产。可以记录这些操作，以便提供用户操作的历史记录。 本节介绍[!DNL Experience Manager]的录制功能，以及如何配置[!DNL Experience Manager]以记录特定事件。

## 性能注意事项和默认行为{#performance-considerations-and-default-behavior}

例如，进行批量导入时，此集成可能会占用CPU和磁盘空间。 由于这些原因，默认情况下禁用与活动流的[!DNL Assets]集成。

## 支持的操作事件{#supported-action-events}

可以将以下事件配置为录制：

* 已接受（已接受）许可
* 已创建资产(ASSET_CREATED)
* 已移动资产(ASSET_MOVED)
* 资产已删除(ASSET_REMOVED)
* 已拒绝许可(被拒绝)
* 已下载（已下载）资产
* 资产版本化（版本化）
* 资产版本已恢复（已恢复）
* 资产元数据已更新(METADATA_UPDATED)
* 已发布到外部系统的资产(PUBLISHED_EXTERNAL)
* 资产的原始已更新(ORIGINAL_UPDATED)
* 资产演绎版已更新(RENDITION_UPDATED)
* 资产演绎版已删除(RENDITION_REMOVED)
* 已更新子资产(SUBASSET_UPDATED)
* 已删除子资产(SUBASSET_REMOVED)

## 配置[!DNL Assets]事件录制{#configuring-aem-assets-events-recording}

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供对资产事件录制器调整的访问。 要配置资产事件记录器，请按如下步骤继续：

1. 导航到&#x200B;**[!UICONTROL Web控制台]**

1. 单击&#x200B;**[!UICONTROL 配置]**。

1. 多次单击&#x200B;**[!UICONTROL Day CQ DAM事件记录器]**。

1. 选中&#x200B;**[!UICONTROL 启用此服务]**。

1. 检查要在用户事件类型流中录制的&#x200B;**[!UICONTROL 活动]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 读取录制的事件{#reading-recorded-events}

记录的事件作为活动存储。 可以使用[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以编程方式读取它们。
