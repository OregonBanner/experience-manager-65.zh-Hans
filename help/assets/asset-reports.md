---
title: 有关资产使用和共享的报告
description: 有关您在中资源的报表 [!DNL Adobe Experience Manager Assets] 以帮助您了解数字资产的使用情况、活动和共享。
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 8%

---

# 资源报表 {#asset-reports}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/asset-reports.html?lang=en) |

通过资产报告，您可以评估 [!DNL Adobe Experience Manager Assets] 部署。 替换为 [!DNL Assets]，您可以为数字资产生成各种报表。 这些报表提供有关系统使用情况、用户如何与资源交互以及下载和共享哪些资源的有用信息。

使用报告中的信息获得关键成功指标以衡量采用情况 [!DNL Assets] 企业内部和客户。

此 [!DNL Assets] 报告框架使用 [!DNL Sling] 作业以按顺序异步处理报表请求。 它对于大型存储库是可伸缩的。 异步报表处理提高了生成报表的效率和速度。

报告管理界面直观易用，包括访问存档报告和查看报告运行状态（成功、失败和排队）的细粒度选项和控件。

生成报告后，系统会通过电子邮件（可选）和收件箱通知来通知您。 您可以从报告列表页面中查看、下载或删除报告，所有之前生成的报告都将显示在该页面中。

## 先决条件 {#prerequisite-for-reporting}

要生成报表，请执行以下操作：

* 启用 [!UICONTROL Day CQ DAM事件记录器] 服务来源 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
* 选择要报告的活动或事件。 例如，要生成有关已下载资产的报告，请选择 [!UICONTROL 已下载资产（已下载）].

![在Web控制台中启用资产报告](assets/reports-config-day-cq-dam-event-recorder.png)

## 生成报告 {#generate-reports}

[!DNL Experience Manager Assets] 会为您生成以下标准报表：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* [!DNL Brand Portal] 发布
* 磁盘使用情况
* 文件
* 链接共享

[!DNL Adobe Experience Manager] 管理员可以轻松地为您的实施生成和自定义这些报表。 管理员可以按照以下步骤生成报告：

1. In [!DNL Experience Manager] 界面，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报告]**.

   ![用于导航资产报表的“工具”页面](assets/AssetsReportNavigation.png)

1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 工具栏中。
1. 从 **[!UICONTROL 创建报告]** 页面上，选择要创建的报告并单击 **[!UICONTROL 下一个]**.

   ![选择报表类型](assets/choose_report.png)

   >[!NOTE]
   >
   >默认情况下，资产中包含内容片段和链接共享 [!UICONTROL 下载] 报告。 选择相应的选项以创建链接共享报表或从下载报表中排除内容片段。

   >[!NOTE]
   >
   >此 [!UICONTROL 下载] 报表仅显示单独选择后下载的资产或使用快速操作下载的资产的详细信息。 但是，它不包括已下载文件夹内资源的详细信息。

1. 在存储报告的CRX存储库中配置报告详细信息，例如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为 `/content/dam`. 您可以指定其他路径。

   ![用于添加报告详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。

   您可以选择现在生成报告，也可以选择在未来的日期和时间生成报告。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在“日期”和“时间”字段中指定日期和时间。 如果您未指定任何值，则报告引擎会将其视为将立即生成的报告。

   根据您创建的报告类型，配置字段可能有所不同。 例如， **[!UICONTROL 磁盘使用情况]** 报表提供了一些选项，用于在计算资产使用的磁盘空间时包含资产演绎版。 您可以选择在子文件夹中包括或排除资产以计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   ![“磁盘使用情况”报告的“详细信息”页面](assets/disk_usage_configuration.png)

   当您创建 **[!UICONTROL 文件]** 报表中，您可以包含/排除子文件夹。 但是，您不能包含此报表的资产演绎版。

   ![“文件”报告的“详细信息”页面](assets/files_report.png)

   此 **[!UICONTROL 链接共享]** 报表显示从内与外部用户共享的资产的URL [!DNL Assets]. 其中包括共享资产的用户的电子邮件 ID、接受共享资产的用户的电子邮件 ID、链接的共享日期和到期日期。列不可自定义。

   此 **[!UICONTROL 链接共享]** 报表，不包括子文件夹和呈现形式的选项，因为它仅发布显示在下的共享URL `/var/dam/share`.

   ![链接共享报告的详细信息页面](assets/link_share.png)

1. 单击 **[!UICONTROL 下一个]** 工具栏中。

1. 在 **[!UICONTROL 配置列]** 页面中，某些列会默认显示在报表中。 您可以选择更多列。 取消选择列以在报告中将其排除。

   ![选择或取消选择报表列](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在 `jcr:content` CRX中的节点。 或者，通过属性路径选取器添加它。

   ![选择或取消选择报表列](assets/custom_columns.png)

1. 单击 **[!UICONTROL 创建]** 工具栏中。 此时将显示一条消息，通知已开始生成报告。
1. 在 [!UICONTROL 资产报表] 页面时，报表生成状态基于报表作业的当前状态，例如 [!UICONTROL 成功]， [!UICONTROL 失败]， [!UICONTROL 已排队]，或 [!UICONTROL 已计划]. 通知收件箱中将显示相同的状态。要查看报告页面，请单击报告链接。 或者，选择报告，然后单击 **[!UICONTROL 视图]** 工具栏中。

   ![生成的报告](assets/report_page.png)

   单击 **[!UICONTROL 下载]** ，以CSV格式下载报表。

## 添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以显示符合自定义要求的更多数据：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* [!DNL Brand Portal] 发布
* 文件

要向这些报表中添加自定义列，请执行以下步骤：

1. 在 [!DNL Manager interface]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报告]**.
1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 工具栏中。

1. 从 **[!UICONTROL 创建报告]** 页面上，选择要创建的报告并单击 **[!UICONTROL 下一个]**.
1. 配置报表详细信息，如标题、描述、缩略图、文件夹路径和日期范围（如果适用）。

1. 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![指定报表自定义列的名称](assets/custom_columns-1.png)

1. 将属性路径添加到 `jcr:content` 使用属性路径选取器的CRXDE中的节点。 或者，在属性路径字段中键入路径。

   ![从jcr：content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单击 **[!UICONTROL 添加]** 并重复步骤5和6。

1. 单击 **[!UICONTROL 创建]** 工具栏中。 此时将显示一条消息，通知已开始生成报告。

## 配置清除服务 {#configure-purging-service}

要删除您不再需要的报表，请从Web控制台配置DAM报表清除服务，以根据现有报表的数量和期限清除现有报表。

1. 从访问Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL DAM报表清除服务]** 配置。
1. 在中指定清除服务的频率（时间间隔） `scheduler.expression.name` 字段。 您还可以配置报表的年龄和数量阈值。
1. 保存更改。

## 疑难解答信息、提示和限制 {#best-practices-and-limitations}

* 如果报表中的一些报表或数字不可用或按预期显示，请确保 [!UICONTROL Day CQ DAM事件记录器] 服务已启用。

* 删除不再需要的报表。 使用DAM报告清除服务中的配置选项来配置清除报告的标准。

* 如果“Disk Usage Report（磁盘使用情况报表）”未生成，并且您正在使用 [!DNL Dynamic Media]，请确保所有资产均可正确继续。 要解决此问题，请重新处理资产，然后再次生成报表。
