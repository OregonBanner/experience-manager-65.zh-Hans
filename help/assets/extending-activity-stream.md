---
title: 将资产与活动流集成
description: 介绍AEM的录制功能以及如何配置AEM以录制特定事件。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 将资产与活动流集成 {#integrating-assets-with-activity-stream}

Adobe Experience Manager(AEM)资产用户可执行许多操作，如创建、上传和删除资产。 可以记录这些操作，以便提供用户操作的历史记录。 本节介绍AEM的录制功能以及如何配置AEM以记录特定事件。

## 性能注意事项和默认行为 {#performance-considerations-and-default-behavior}

此集成可能会占用CPU和磁盘空间，例如，执行批量导入时。 由于这些原因，默认情况下会禁用AEM资产与活动流的集成。

## 支持的操作事件 {#supported-action-events}

可以将以下事件配置为记录：

* 已接受许可（已接受）
* 已创建资产(ASSET_CREATED)
* 已移动资产(ASSET_MOVED)
* 资产已删除(ASSET_REMOVED)
* 许可被拒绝（已拒绝）
* 已下载资产（已下载）
* 资产版本控制（版本控制）
* 资产版本已恢复（已恢复）
* 资产元数据已更新(METADATA_UPDATED)
* 已发布到外部系统的资产(PUBLISHED_EXTERNAL)
* 资产的原始更新(ORIGINAL_UPDATED)
* 资产演绎版已更新(RENDITION_UPDATED)
* 删除了资产演绎版(RENDITION_REMOVED)
* 子资产已更新(SUBASSET_UPDATED)
* 已删除子资产(SUBASSET_REMOVED)

## 配置AEM资产事件录制 {#configuring-aem-assets-events-recording}

通过 [Web控制台](/help/sites-deploying/configuring-osgi.md) ，可以访问AEM资产事件记录器调整。 要配置AEM资产事件记录器，请按如下步骤继续：

1. 导航到 **[!UICONTROL Web控制台]**

1. 单击 **[!UICONTROL 配置]**。

1. 双击 **[!UICONTROL Day CQ DAM事件记录器]**。

1. 选中 **[!UICONTROL 启用此服务]**。

1. 检查 **[!UICONTROL 要在用户活动流中记录的]** “事件类型”。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 阅读录制的活动 {#reading-recorded-events}

记录的事件作为活动存储。 您可以使用 [ActivityManager API以编程方式读取它们](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)。
