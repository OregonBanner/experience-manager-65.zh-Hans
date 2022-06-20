---
title: 有关资产使用和共享的报表
description: 有关中资产的报表 [!DNL Adobe Experience Manager Assets] 以帮助您了解数字资产的使用、活动和共享情况。
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

资产报表允许您评估 [!DNL Adobe Experience Manager Assets] 部署。 使用 [!DNL Assets]，则可以为数字资产生成各种报表。 这些报表提供有关您的系统使用情况、用户与资产的交互方式以及下载和共享哪些资产的有用信息。

使用报表中的信息获取关键成功量度，以衡量 [!DNL Assets] 企业内部和客户。

的 [!DNL Assets] 报告框架使用 [!DNL Sling] 以异步方式处理报表请求的作业。 它可用于大型存储库。 异步报表处理提高了生成报表的效率和速度。

报表管理界面是直观的，包括用于访问已存档报表和查看报表运行状态（成功、失败和已排队）的细粒度选项和控件。

生成报表后，系统会通过电子邮件（可选）和收件箱通知您。 您可以从报表列表页面查看、下载或删除报表，其中显示所有以前生成的报表。

## 先决条件 {#prerequisite-for-reporting}

要生成报表，请执行以下操作：

* 启用 [!UICONTROL Day CQ DAM事件记录器] 服务 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
* 选择要报告的活动或事件。 例如，要生成已下载资产的报表，请选择 [!UICONTROL 已下载资产（已下载）].

![在Web控制台中启用资产报告功能](assets/reports-config-day-cq-dam-event-recorder.png)

## 生成报表 {#generate-reports}

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

[!DNL Adobe Experience Manager] 管理员可以轻松地为您的实施生成和自定义这些报表。 管理员可以按照以下步骤生成报表：

1. 在 [!DNL Experience Manager] 界面，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.

   ![用于导航资产报表的工具页面](assets/AssetsReportNavigation.png)

1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 中。
1. 从 **[!UICONTROL 创建报表]** 页面，选择要创建的报表并单击 **[!UICONTROL 下一个]**.

   ![选择报表类型](assets/choose_report.png)

   >[!NOTE]
   >
   >默认情况下，内容片段和链接共享包含在资产中 [!UICONTROL 下载] 报表。 选择相应的选项以创建链接共享报表，或从下载报表中排除内容片段。

   >[!NOTE]
   >
   >的 [!UICONTROL 下载] 报表仅显示单独选择后下载或使用快速操作下载的资产的详细信息。 但是，它不包括已下载文件夹中资产的详细信息。

1. 在存储报表的CRX存储库中配置报表详细信息，如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为 `/content/dam`. 您可以指定其他路径。

   ![添加报表详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。

   您可以选择立即生成报表，也可以选择在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果您选择稍后计划报表，请确保在“日期”和“时间”字段中指定日期和时间。 如果您没有指定任何值，报表引擎会将其视为即时生成的报表。

   配置字段可能因您创建的报表类型而异。 例如， **[!UICONTROL 磁盘使用情况]** 报表提供了一些选项，用于在计算资产使用的磁盘空间时包含资产演绎版。 您可以选择在子文件夹中包含或排除资产，以便计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   ![“磁盘使用情况”报告的详细信息页面](assets/disk_usage_configuration.png)

   创建 **[!UICONTROL 文件]** 报表中，您可以包含/排除子文件夹。 但是，您不能为此报表包含资产演绎版。

   ![“文件”报表的“详细信息”页面](assets/files_report.png)

   的 **[!UICONTROL 链接共享]** 报表显示与内部外部用户共享的资产的URL [!DNL Assets]. 其中包括共享资产的用户的电子邮件 ID、接受共享资产的用户的电子邮件 ID、链接的共享日期和到期日期。列不可自定义。

   的 **[!UICONTROL 链接共享]** ，不包括子文件夹和演绎版的选项，因为它仅发布下面显示的共享URL `/var/dam/share`.

   ![“链接共享”报表的详细信息页面](assets/link_share.png)

1. 单击 **[!UICONTROL 下一个]** 中。

1. 在 **[!UICONTROL 配置列]** 页面，默认情况下会选择某些列以在报表中显示。 您可以选择更多列。 取消所选列以将其排除在报表中。

   ![选择或取消选择的报表列](assets/configure_columns.png)

   要显示自定义列名称或属性路径，请在 `jcr:content` 节点。 或者，通过属性路径选取器添加。

   ![选择或取消选择的报表列](assets/custom_columns.png)

1. 单击 **[!UICONTROL 创建]** 中。 系统会显示一条消息，通知已开始生成报告。
1. 在 [!UICONTROL 资产报表] 页面，则报表生成状态基于报表作业的当前状态，例如 [!UICONTROL 成功], [!UICONTROL 失败], [!UICONTROL 已排队]或 [!UICONTROL 已计划]. 通知收件箱中会显示相同的状态。要查看报表页面，请单击报表链接。 或者，选择报表，然后单击 **[!UICONTROL 查看]** 中。

   ![生成的报表](assets/report_page.png)

   单击 **[!UICONTROL 下载]** 从工具栏下载CSV格式的报表。

## 添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以显示符合您自定义要求的更多数据：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* [!DNL Brand Portal] 发布
* 文件

要向这些报表添加自定义列，请执行以下步骤：

1. 在 [!DNL Manager interface]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.
1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 中。

1. 从 **[!UICONTROL 创建报表]** 页面，选择要创建的报表并单击 **[!UICONTROL 下一个]**.
1. 根据需要配置报表详细信息，如标题、描述、缩略图、文件夹路径和日期范围。

1. 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![指定报表自定义列的名称](assets/custom_columns-1.png)

1. 在 `jcr:content` 节点。 或者，在属性路径字段中键入路径。

   ![从jcr:content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单击 **[!UICONTROL 添加]** 重复步骤5和6。

1. 单击 **[!UICONTROL 创建]** 中。 系统会显示一条消息，通知已开始生成报告。

## 配置清除服务 {#configure-purging-service}

要删除不再需要的报表，请从Web控制台中配置DAM报表清除服务，以根据现有报表的数量和年龄来清除现有报表。

1. 从访问Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL DAM报表清除服务]** 配置。
1. 在 `scheduler.expression.name` 字段。 您还可以配置报表的年龄和数量阈值。
1. 保存更改。

## 故障诊断信息、提示和限制 {#best-practices-and-limitations}

* 如果报表中的某些报表或数字不可用或无法按预期使用，请确保 [!UICONTROL Day CQ DAM事件记录器] 服务已启用。

* 删除不再需要的报表。 使用DAM报表清除服务中的配置选项来配置清除报表的标准。

* 如果未生成磁盘使用情况报表，并且您正在使用 [!DNL Dynamic Media]，请确保所有资产均正确继续。 要解析资产，请重新处理资产，然后再次生成报表。
