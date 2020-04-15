---
title: 有关数字资产的报告
description: 了解AEM资产中有关资产的报告，帮助您了解数字资产的使用、活动和共享情况。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 资产报表 {#asset-reports}

资产报告是评估Adobe Experience Manager(AEM)资产部署的实用程序的关键工具。 通过AEM资产，您可以为数字资产生成各种报告。 这些报告提供有关系统使用情况、用户与资产交互方式以及下载和共享哪些资产的有用信息。

使用报告中的信息得出关键成功指标，以衡量企业内部和客户对AEM资产的采用情况。

AEM资产报告框架使用Sling作业以有序方式异步处理报表请求。 它可针对大型存储库进行扩展。 异步报表处理提高了生成报表的效率和速度。

报表管理界面直观，包括用于访问存档报表和视图报表运行状态（成功、失败和已排队）的细粒度选项和控件。

生成报告后，您会通过电子邮件（可选）和收件箱通知收到通知。 您可以从报告列表页面视图、下载或删除报告，其中显示所有以前生成的报告。

## 生成报告 {#generate-reports}

AEM资产会为您生成以下标准报表：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* 品牌门户发布
* 磁盘使用情况
* 文件
* 链接共享

AEM管理员可以轻松生成和自定义这些报告以用于您的实施。 管理员可以按照以下步骤生成报告：

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]** > **[!UICONTROL 报表]**。

![“工具”页面以导航资产报表](assets/AssetsReportNavigation.png)

1. 在资产报 [!UICONTROL 表页面] ，单击工 **[!UICONTROL 具栏中的]** 创建。
1. 从创 **[!UICONTROL 建报表页面]** ，选择要创建的报表，然后单击下 **[!UICONTROL 一步]**。

   ![选择报告类型](assets/choose_report.png)

   >[!NOTE]
   >
   >在生成&#x200B;**[!UICONTROL 已下载资产]**&#x200B;报表之前，请确保已启用“资产下载”服务。从 Web 控制台 (`https://[aem_server]:[port]/system/console/configMgr`) 中打开 **[!UICONTROL Day CQ DAM 事件记录器]**&#x200B;配置，并在“事件类型”中选择&#x200B;**[!UICONTROL 已下载资产]**&#x200B;选项（如果尚未选择）。

   >[!NOTE]
   >
   >默认情况下，内容片段和链接共享包含在“已下载资产”报表中。 选择相应的选项以创建链接共享的报告或从下载报告中排除内容片段。

1. 在存储报告的CRX存储库中配置报告详细信息，如标题、说明、缩略图和文件夹路径。 默认情况下，文件夹路径为 `/content/dam`。 您可以指定其他路径。

   ![要添加报告详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。

   您可以选择立即生成报表或在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在“日期”和“时间”字段中指定日期和时间。 如果未指定任何值，报表引擎会将其视为即时生成的报表。

   配置字段可能因您创建的报告类型而异。 例如，“磁盘使 **[!UICONTROL 用情况]** ”报告提供了在计算资产使用的磁盘空间时包含资产演绎版的选项。 您可以选择在子文件夹中包含或排除资产，以便计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   ![“ Disk Usage”报告的“Details”（详细信息）页](assets/disk_usage_configuration.png)

   在创建“文 **[!UICONTROL 件]** ”报告时，可以包含／排除子文件夹。 但是，您不能为此报表包含资产演绎版。

   ![“文件”报告的“详细信息”页](assets/files_report.png)

   **[!UICONTROL 链接共享]**&#x200B;报表显示 AEM Assets 中与外部用户共享的资产的 URL。其中包括共享资产的用户的电子邮件 ID、接受共享资产的用户的电子邮件 ID、链接的共享日期和到期日期。列不可自定义。

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![“链接共享”报告的详细信息页面](assets/link_share.png)

1. 单击 **[!UICONTROL 工具栏]** 中的下一步。

1. 在“配 **[!UICONTROL 置列]** ”页中，某些列在默认情况下处于选中状态以显示在报告中。 您可以选择更多列。 取消选择选定的列，以在报告中将其排除。

   ![选择或取消选择报告列](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在CRX的jcr:content节点下配置资产二进制的属性。 或者，通过属性路径选取器添加它。

   ![选择或取消选择报告列](assets/custom_columns.png)

1. 单击 **[!UICONTROL 工具栏]** 中的创建。 系统会显示一条消息，通知已开始生成报告。
1. 在“资产报表”页面中，报表生成状态基于报表作业的当前状态，例如成功、失败、已排队或已计划。 通知收件箱中显示相同的状态。要视图报告页面，请单击报告链接。 或者，选择报告，然后单击工 **[!UICONTROL 具栏中的视图]** 。

   ![生成的报告](assets/report_page.png)

   单击 **[!UICONTROL 工具栏中]** “下载”以下载CSV格式的报告。

## 添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以显示更多符合自定义要求的数据：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* 品牌门户发布
* 文件

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]** > **[!UICONTROL 报表]**。
1. 在资产报 [!UICONTROL 表页面] ，单击工 **[!UICONTROL 具栏中的]** 创建。

1. 从创 **[!UICONTROL 建报表页面]** ，选择要创建的报表，然后单击下 **[!UICONTROL 一步]**。
1. 根据需要配置报告详细信息，如标题、说明、缩略图、文件夹路径和日期范围。

1. 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![指定报告的自定义列的名称](assets/custom_columns-1.png)

1. 使用属性路径选取器在CRXDE `jcr:content` 中的节点下添加属性路径。 或者，在属性路径字段中键入路径。

   ![从jcr:content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单 **[!UICONTROL 击]** “添加”，然后重复步骤5和6。

1. 单击 **[!UICONTROL 工具栏]** 中的创建。 系统会显示一条消息，通知已开始生成报告。

## 配置清除服务 {#configure-purging-service}

要删除不再需要的报表，请从Web控制台中配置DAM报表清除服务，以根据现有报表的数量和年龄清除这些报表。

1. 从访问Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开 **[!UICONTROL DAM报表清除服务配置]** 。
1. 在字段中指定清除服务的频率(时间间 `scheduler.expression.name` 隔)。 您还可以为报告配置年龄和数量阈值。
1. 保存更改。
