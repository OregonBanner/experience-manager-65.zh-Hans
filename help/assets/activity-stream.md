---
title: 时间轴视图中数字资产的活动流
description: 本文介绍了如何在时间轴上显示资产的活动日志。
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 21%

---

# 时间轴中的活动流 {#activity-stream-in-timeline}

此功能在时间轴上显示资源的活动日志。 如果您在中执行以下任何与资产相关的操作 [!DNL Adobe Experience Manager Assets]，活动流功能会更新时间线以反映该活动。

活动流中记录了以下操作：

* 创建
* 删除
* 下载（包括演绎版）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

时间轴中显示的活动日志是从 CRX 中的 `/var/audit/com.day.cq.dam/content/dam` 位置获取的，日志文件就存储在该位置。此外，上传新资产或修改现有资产并签入时，会记录时间轴活动 [!DNL Experience Manager] via [Adobe资源链接](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 或 [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>临时工作流不会显示在时间轴中，因为不会保存这些工作流的历史记录信息。

要查看活动流，请在资产上执行一个或多个操作，选择资产，然后选择 **[!UICONTROL 时间线]** 从GlobalNav列表中。

![时间轴–2](assets/timeline-2.png)

时间轴显示您对资产执行的操作的活动流。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>**[!UICONTROL 发布]**&#x200B;和&#x200B;**[!UICONTROL 取消发布]**&#x200B;任务的默认日志存储位置为 `/var/audit/com.day.cq.replication/content`。对于&#x200B;**[!UICONTROL 移动]**&#x200B;任务，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。
