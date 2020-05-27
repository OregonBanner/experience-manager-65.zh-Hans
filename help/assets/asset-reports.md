---
title: 有关数字资产的报告
description: 了解Adobe Experience Manager资产中有关资产的报告，帮助您了解数字资产的使用、活动和共享情况。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 15%

---


# 资产报表 {#asset-reports}

资产报告是评估Adobe Experience Manager资产部署的效用的重要工具。 通过资产，您可以为数字资产生成各种报表。 这些报告提供有关系统使用情况、用户如何与资产交互以及下载和共享哪些资产的有用信息。

使用报告中的信息得出关键成功指标，以衡量企业内部和客户对资产的采用情况。

资产报告框架使用Sling作业以有序方式异步处理报表请求。 它可用于大型存储库。 异步报表处理提高了报表生成的效率和速度。

报表管理界面直观，包括用于访问归档报表和视图报表运行状态（成功、失败和排队）的细粒度选项和控件。

生成报告后，系统会通过电子邮件（可选）和收件箱通知通知您。 您可以从报告列表页面视图、下载或删除报告，其中显示所有以前生成的报告。

## 生成报告 {#generate-reports}

Experience Manager资产会为您生成以下标准报表：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* 品牌门户发布
* 磁盘使用情况
* 文件
* 链接共享

Experience Manager管理员可以轻松生成和自定义这些报告，以用于您的实施。 管理员可以按照以下步骤生成报告：

1. 在Experience Manager界面中，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报]**告。
   ![](assets/AssetsReportNavigation.png)

1. 在资产 [!UICONTROL 报表页] ，单击工 **[!UICONTROL 具栏]** 中的创建。
1. 从创 **[!UICONTROL 建报表]** ，选择要创建的报表，然后单击下 **[!UICONTROL 一步]**。

   ![](assets/choose_report.png)

   >[!NOTE]
   >
   >在生成&#x200B;**[!UICONTROL 已下载资产]**&#x200B;报表之前，请确保已启用“资产下载”服务。从 Web 控制台 (`https://[aem_server]:[port]/system/console/configMgr`) 中打开 **[!UICONTROL Day CQ DAM 事件记录器]**&#x200B;配置，并在“事件类型”中选择&#x200B;**[!UICONTROL 已下载资产]**&#x200B;选项（如果尚未选择）。

   >[!NOTE]
   >
   >默认情况下，内容片段和链接共享包含在已下载的资产报告中。 选择相应的选项以创建链接共享报告或从下载报告中排除内容片段。

1. 在存储报告的CRX存储库中配置报告详细信息，如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为 `/content/dam`。 可以指定其他路径。

   ![](assets/report_configuration.png)

   选择报表的日期范围。

   您可以选择立即或在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在“日期”和“时间”字段中指定日期和时间。 如果不指定任何值，报表引擎会将其视为即时生成的报表。

   配置字段可能因您创建的报告类型而异。 例如，“磁盘使 **[!UICONTROL 用情况]** ”报告提供在计算资产使用的磁盘空间时包括资产演绎版的选项。 您可以选择在子文件夹中包含或排除资产，以便计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   ![](assets/disk_usage_configuration.png)

   创建“文件 **[!UICONTROL ”报]** 告时，可以包含／排除子文件夹。 但是，您不能为此报表包含资产演绎版。

   ![](assets/files_report.png)

   **[!UICONTROL 链接共享]**&#x200B;报表显示 Assets 中与外部用户共享的资产的 URL。其中包括共享资产的用户的电子邮件 ID、接受共享资产的用户的电子邮件 ID、链接的共享日期和到期日期。列不可自定义。

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![](assets/link_share.png)

1. 单击工 **[!UICONTROL 具栏]** 中的“下一步”。

1. 在“配 **[!UICONTROL 置列]** ”页中，默认情况下会选择某些列以显示在报告中。 您可以选择更多列。 取消选择选定列，以在报告中将其排除。

   ![](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在CRX的jcr:content节点下配置资产二进制的属性。 或者，通过属性路径选取器添加它。

   ![](assets/custom_columns.png)

1. 单击 **[!UICONTROL 工具栏]** 中的创建。 系统会显示一条消息，通知已开始生成报告。
1. 在资产报表页面中，报表生成状态基于报表作业的当前状态，例如成功、失败、已排队或已计划。 通知收件箱中显示相同的状态。要视图报告页面，请单击报告链接。 或者，选择报表，然后单击工 **[!UICONTROL 具栏]** 中的视图。

   ![](assets/report_page.png)

   单击 **[!UICONTROL 工具栏]** 中的“下载”以下载CSV格式的报告。

## 添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以根据自定义要求显示更多数据：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* 品牌门户发布
* 文件

要向这些报表添加自定义列，请执行以下步骤：

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]** > **[!UICONTROL 报]**&#x200B;告。
1. 在资产 [!UICONTROL 报表页] ，单击工 **[!UICONTROL 具栏]** 中的创建。

1. 从创 **[!UICONTROL 建报表]** ，选择要创建的报表，然后单击下 **[!UICONTROL 一步]**。
1. 根据需要配置报告详细信息，如标题、说明、缩略图、文件夹路径和日期范围。

1. 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![](assets/custom_columns-1.png)

1. 使用属性路径选 `jcr:content` 取器在CRXDE的节点下添加属性路径。 或者，在属性路径字段中键入路径。

   ![](assets/property_picker.png)

   要添加更多自定义列，请单 **[!UICONTROL 击]** “添加”，并重复步骤5和6。

1. 单击 **[!UICONTROL 工具栏]** 中的创建。 系统会显示一条消息，通知已开始生成报告。

## 配置清除服务 {#configure-purging-service}

要删除不再需要的报表，请从Web控制台中配置DAM报表清除服务，以根据现有报表的数量和年龄来清除现有报表。

1. 从访问Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开DAM **[!UICONTROL 报表清除服务配置]** 。
1. 在字段中指定清除服务的频率(时间间隔 `scheduler.expression.name` )。 您还可以配置报告的年龄和数量阈值。
1. 保存更改。
