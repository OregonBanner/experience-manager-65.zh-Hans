---
title: 与 [!DNL Assets] 活动流集成
description: 介绍其录制功 [!DNL Experience Manager] 能以及如何配置它以记录特定事件。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 与 [!DNL Assets] 活动流集成 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] 用户可执行许多操作，如创建、上传和删除资产。 可以记录这些操作，以便提供用户操作的历史记录。 本节介绍的录制功能 [!DNL Experience Manager] 以及如何配置 [!DNL Experience Manager] 以记录特定事件。

## 性能注意事项和默认行为 {#performance-considerations-and-default-behavior}

例如，进行批量导入时，此集成可能会占用CPU和磁盘空间。 由于这些原因， [!DNL Assets] 默认情况下会禁用与活动流的集成。

## 支持的操作事件 {#supported-action-events}

可以将以下事件配置为记录：

* 已接受许可（已接受）
* 已创建资产(ASSET_CREATED)
* 已移动资产(ASSET_MOVED)
* 资产已删除(ASSET_REMOVED)
* 已拒绝许可(被拒绝)
* 已下载资产（已下载）
* 资产版本控制（版本控制）
* 资产版本已恢复（已恢复）
* 资产元数据已更新(METADATA_UPDATED)
* 已发布到外部系统的资产(PUBLISHED_EXTERNAL)
* 资产的原始已更新(ORIGINAL_UPDATED)
* 资产演绎版已更新(RENDITION_UPDATED)
* 删除资产演绎版(RENDITION_REMOVED)
* 子资产已更新(SUBASSET_UPDATED)
* 已删除子资产(SUBASSET_REMOVED)

## 配置 [!DNL Assets] 事件录制 {#configuring-aem-assets-events-recording}

Web控 [制台提供](/help/sites-deploying/configuring-osgi.md) “资产事件记录器”调整的访问权限。 要配置资产事件记录器，请按如下步骤继续：

1. 导航到 **[!UICONTROL Web控制台]**

1. 单击 **[!UICONTROL 配置]**。

1. 多次单 **[!UICONTROL 击“Day CQ DAM事件记录器”]**。

1. 选中 **[!UICONTROL 启用此服务]**。

1. 检查 **[!UICONTROL 要]** 在用户事件类型流中记录哪些活动。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 阅读录制的事件 {#reading-recorded-events}

记录的事件作为活动存储。 您可以使用ActivityManager API以编程 [方式读取它们](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)。
