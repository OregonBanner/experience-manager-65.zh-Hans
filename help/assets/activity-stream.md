---
title: 活动时间轴视图中数字资产流
description: 本文介绍如何在时间轴上显示资产的活动日志。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 30%

---


# 时间轴中的活动流 {#activity-stream-in-timeline}

这项功能可将资产的活动日志显示在时间轴上。如果您在[!DNL Adobe Experience Manager Assets]中执行下列任何与资产相关的操作，活动流功能会更新时间轴以反映活动。

以下操作记录在活动流中：

* 创建
* 删除
* 下载（包括再现）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

时间轴中显示的活动日志是从 CRX 中的 `/var/audit/com.day.cq.dam/content/dam` 位置获取的，日志文件就存储在该位置。此外，当上传新资产或通过[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)或[Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)修改现有资产并签入[!DNL Experience Manager]时，将记录时间轴活动。

>[!NOTE]
>
>临时工作流不会显示在时间轴中，因为没有为这些工作流保存历史记录信息。

要视图活动流，请对资产执行一个或多个操作，选择资产，然后从GlobalNav列表中选择&#x200B;**[!UICONTROL 时间轴]**。

![时间线-2](assets/timeline-2.png)

时间轴显示您对资产执行的操作的活动流。

![活动流](assets/activity_stream.png)

>[!NOTE]
>
>**[!UICONTROL 发布]**&#x200B;和&#x200B;**[!UICONTROL 取消发布]**&#x200B;任务的默认日志存储位置为 `/var/audit/com.day.cq.replication/content`。对于&#x200B;**[!UICONTROL 移动]**&#x200B;任务，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。
