---
title: 时间轴中的活动流
description: 本文介绍如何在时间轴上显示资产的活动日志。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 时间轴中的活动流 {#activity-stream-in-timeline}

这项功能可将资产的活动日志显示在时间轴上。如果您在Adobe Experience Manager(AEM)资产中执行下列任何与资产相关的操作，活动流功能会更新时间轴以反映活动。

以下操作记录在活动流中：

* 创建
* 删除
* 下载（包括再现）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

将从存储日志文件的CRX位置获取要显示在时间轴 `/var/audit/com.day.cq.dam/content/dam` 中的活动日志。  此外，当新资产上传或现有资产通过 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [AEM桌面应用程序修改并签入AEM时，将记录时间轴活动](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)。

>[!NOTE]
>
>临时工作流不会显示在时间轴中，因为不会保存这些工作流的历史记录信息。

要查看活动流，请对资产执行一个或多个操作，选择资产，然后从GlobalNav列表中选 **[!UICONTROL 择Timeline]** 。

![时间线-2](assets/timeline-2.png)

时间轴显示您对资产执行的操作的活动流。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>“发布”和“取消发布”任 **[!UICONTROL 务的默认]****[!UICONTROL 日志存储位置为]** “ `/var/audit/com.day.cq.replication/content`”。 对于 **[!UICONTROL 移动任务]** ，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。
