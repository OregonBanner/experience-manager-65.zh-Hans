---
title: 报告
seo-title: 报告
description: 了解如何在AEM中使用报告。
seo-description: 了解如何在AEM中使用报告。
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
translation-type: tm+mt
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2815'
ht-degree: 4%

---

# 报告 {#reporting}

为了帮助您监视和分析实例的状态，AEM提供了一系列默认报表，这些报表可以根据您的具体要求进行配置：

* [组件报告](#component-report)
* [磁盘使用情况](#disk-usage)
* [运行状况检查](#health-check)
* [页面活动报告](#page-activity-report)
* [用户生成的内容报告](#user-generated-content-report)
* [用户报告](#user-report)
* [工作流实例报告](#workflow-instance-report)
* [工作流报表](#workflow-report)

>[!NOTE]
>
>这些报表仅在经典UI中可用。 有关现代UI中的系统监视和报告，请参阅[操作仪表板。](/help/sites-administering/operations-dashboard.md)

所有报告都可以从&#x200B;**工具**&#x200B;控制台访问。 在左侧窗格中选择&#x200B;**报表**，然后多次单击右侧窗格中所需的报表以将其打开进行查看和/或配置。

也可以从&#x200B;**工具**&#x200B;控制台创建报表的新实例。 在左侧窗格中选择&#x200B;**报告**，然后选择&#x200B;**新建……**。 定义&#x200B;**标题**&#x200B;和&#x200B;**名称**，选择所需的报告类型，然后单击&#x200B;**创建**。 您的新报表实例将显示在列表中。 多次单击此图标可打开，然后从Sidekick中拖动组件以创建第一列并开始报表定义。

>[!NOTE]
>
>除了开箱即用的标准AEM报表外，您还可以[开发您自己的（全新）报表](/help/sites-developing/dev-reports.md)。

## 报表自定义的基础知识{#the-basics-of-report-customization}

可用的报表格式多种多样。 以下报告可自定义的所有使用列，详见以下各节：

* [组件报告](#component-report)
* [页面活动报告](#page-activity-report)
* [用户生成的内容报告](#user-generated-content-report)
* [用户报告](#user-report)
* [工作流实例报告](#workflow-instance-report)

>[!NOTE]
>
>以下各个报告都有各自的格式和自定义：
>
>
>* [运行状况](#health-check) 检查使用选择字段指定要报告的数据。
>* [磁盘](#disk-usage) 使用链接可深入浏览存储库结构。
>* [工作](/help/sites-administering/reporting.md#workflow-report) 流报表概述了在实例上运行的工作流。

>
>
因此，列配置的以下过程不合适。 有关各个报表的详细信息，请参阅其说明。

### 选择并定位数据列{#selecting-and-positioning-the-data-columns}

可以向任何报表添加列、在其上重新定位列或从其中删除列，无论是标准报表还是自定义报表。

Sidekick的&#x200B;**组件**&#x200B;选项卡（在报告页面上提供）列表了可选为列的所有类别数据。

要更改数据选择：

* 要添加新列，请将所需组件从sidekick拖放到所需位置

   * 绿色勾号将指示位置何时有效，一对箭头将指示放置位置的确切位置
   * 位置无效时将显示一个红色的不转动符号

* 要移动列，请单击标题，按住并拖动到新位置
* 要删除列，请单击列标题，按住并向上拖动到报表标题区域（红色减号将指示该位置无效）；释放鼠标按钮，“删除组件”对话框将请求确认您确实要删除该列。

### 列下拉菜单{#column-drop-down-menu}

报表中的每列都有一个下拉菜单。 当鼠标光标移动到列标题单元格上时，此图标会变为可见。

标题单元格的最右侧将显示一个箭头（请勿与标题文本右侧的箭头混淆，该箭头指示[当前排序机制](#sorting-the-data)）。

![reportcolumnsort](assets/reportcolumnsort.png)

菜单上的可用选项取决于列的配置（如在项目开发过程中所做的），任何无效选项都将灰显。

### 对数据{#sorting-the-data}排序

数据可以通过以下任一方式根据特定列进行排序：

* 单击相应的列标题；排序将在升序和降序之间切换，在标题文本旁边用箭头指示
* 使用[列的下拉菜单](#column-drop-down-menu)专门选择&#x200B;**升序排序**&#x200B;或&#x200B;**降序排序**;同样，标题文本旁边的箭头也将指示此问题

### 组和当前数据图表{#groups-and-the-current-data-chart}

在相应的列上，您可以从[列的下拉菜单](#column-drop-down-menu)中选择&#x200B;**按此列**&#x200B;分组。 这将根据该列中的每个不同值对数据进行分组。 您可以选择多个要分组的列。 当列中的数据不适当时，此选项将灰显；例如，每个条目都是独特的和唯一的，因此无法形成任何组，例如，用户报表的“用户ID”列。

在至少对一列进行分组后，将基于此分组生成&#x200B;**当前数据**&#x200B;的饼图。 如果对多个列进行分组，则图表中也将指示此情况。

![reportuser](assets/reportuser.png)

将光标移到饼图上将显示相应区段的聚合值。 它使用当前为列定义的聚合;例如，计数、最小、平均等。

### 过滤器和聚合{#filters-and-aggregates}

在相应的列上，您还可以从[列的下拉菜单](#column-drop-down-menu)配置&#x200B;**过滤器设置**&#x200B;和/或&#x200B;**聚合**。

#### 筛选器 {#filters}

“过滤器设置”允许您指定要显示的条目的条件。 可用的运算符有：

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

要设置过滤器：

1. 从下拉式列表中选择所需的运算符。
1. 输入要筛选的文本。
1. 单击&#x200B;**应用**。

要取消激活筛选器，请执行以下操作：

1. 删除滤镜文本。
1. 单击&#x200B;**应用**。

#### 聚合{#aggregates}

您还可以选择聚合方法（这些方法可能因所选列而异）：

![reportagregate](assets/reportaggregate.png)

### 列属性 {#column-properties}

仅当[用户报告](#user-report)中使用了[Generic column](#generic-column)时，此选项才可用。

### 历史数据 {#historic-data}

在&#x200B;**历史数据**&#x200B;下可以看到数据随时间变化的图表。 这源于定期拍摄的快照。

数据是：

* 收集者（如果可用）是第一个已排序列，否则是第一个（非分组）列
* 按相应的列分组

可以生成报表：

1. 在所需列上设置&#x200B;**分组**。
1. **编** 辑配置以定义快照的创建频率；每小时或每天。
1. **完成……** 开始快照集合的定义。

   左上角的红色/绿色滑块按钮指示何时收集快照。

结果图表显示在右下方：

![reporttrends](assets/reporttrends.png)

数据收集启动后，您可以选择：

* **时间段**

   您可以为要显示的报表数据选择起始日期和终止日期。

* **间隔**

   可以为报表的缩放和汇总选择月、周、日、小时。

   例如，如果2011年2月提供每日快照：

   * 如果间隔设置为`Day`，则图表中每个快照都显示为一个值。
   * 如果间隔设置为`Month`，则2月份的所有快照都会聚集到单个值中（在图表中显示为单个“点”）。

选择您的要求，然后单击&#x200B;**开始**&#x200B;将其应用到报表。 要在创建更多快照后更新显示，请再次单击&#x200B;**开始**。

![chlimage_1-43](assets/chlimage_1-43.png)

收集快照时，您可以：

* 使用&#x200B;**完成……再次**&#x200B;以重新初始化集合。

   **完成** “冻结”报表的结构（即分配给报表的列，这些列被分组、排序、筛选等）和开始拍摄快照。

* 打开&#x200B;**编辑**&#x200B;对话框，选择&#x200B;**无数据快照**&#x200B;以在需要前终止收集。

   **“仅** 编辑”可切换快照的拍摄。如果再次打开快照，则使用上次完成时报表的状态进行进一步快照。

>[!NOTE]
>
>快照存储在`/var/reports/...`下，其余路径将镜像报告的路径和报告完成时创建的ID。
>
>
>如果您完全确定不再需要这些实例，则可以手动清除旧快照。

>[!NOTE]
>
>预配置的报表不会占用大量的性能，但仍建议在生产环境上使用每日快照。 如果可能，在网站上活动不多时运行这些每日快照；可以使用&#x200B;**Day CQ报告配置**&#x200B;的`Daily snapshots (repconf.hourofday)`参数定义；有关如何配置此配置的详细信息，请参阅[ OSGI配置](/help/sites-deploying/configuring-osgi.md)。

#### 显示限制{#display-limits}

历史数据报表也可能因可设置的限制而在外观上略有变化，这取决于所选时段的结果数。

每条水平线都称为系列（与图表图例中的条目相对应），每条垂直圆点列表示聚合快照。

![chlimage_1-44](assets/chlimage_1-44.png)

要在较长的时间段内保持图表干净，可以设置一些限制。 对于标准报表，这些报表包括：

* 水平系列 — 默认和系统最大值均为`9`

* 垂直聚合快照 — 默认值为`35`（每个水平系列）

因此，当超出（适当）限制时：

* 点不会显示
* 历史数据图表的图例可能显示与当前数据图表不同的条目数

![chlimage_1-45](assets/chlimage_1-45.png)

自定义报告还可以显示所有系列的&#x200B;**Total**&#x200B;值。 它显示为一个系列（水平线和图例中的条目）。

>[!NOTE]
>
>对于自定义报告，可以以不同方式设置限制。

### 编辑（报告）{#edit-report}

**编辑**&#x200B;按钮可打开&#x200B;**编辑报告**&#x200B;对话框。

这是定义用于收集[历史数据](#historic-data)快照的时间段的位置，但也可以定义各种其他设置：

![reportedit](assets/reportedit.png)

* **标题**

   您可以定义自己的标题。

* **描述**

   您可以定义自己的描述。

* **根路径** (*仅对某些报表处于活动状态*)

   使用此选项可将报表限制在存储库的（子）部分。

* **报表处理**

   * **自动刷新数据**

      每次更新报表定义时，都将刷新报表数据。

   * **手动刷新数据**

      此选项可用于防止存在大量数据时自动刷新操作导致的延迟。

      选择此选项表示当报表配置的任何方面发生更改时，必须手动刷新报表数据。 这也意味着，一旦更改了配置的任何方面，报表表就会被遮蔽。

      选择此选项后，将显示&#x200B;**[加载数据](#load-data)**&#x200B;按钮（在报表上的&#x200B;**编辑**&#x200B;旁边）。 **加** 载数据将加载数据并刷新显示的报告数据。

* **快**
照您可以定义快照的制作频率；每天、每小时或根本不是。

### 加载数据 {#load-data}

仅当从&#x200B;**[Edit](#edit-report)**&#x200B;中选择了&#x200B;**手动刷新数据**&#x200B;时，**加载数据**&#x200B;按钮才可见。

![chlimage_1-46](assets/chlimage_1-46.png)

单击&#x200B;**加载数据**&#x200B;将重新加载数据并更新显示的报告。

选择手动刷新数据意味着：

1. 更改报表配置后，报表数据表将被遮蔽。

   例如，如果更改列的排序机制，则不会显示数据。

1. 如果希望再次显示报表数据，则需要单击&#x200B;**加载数据**&#x200B;以重新加载数据。

### 完成（报告）{#finish-report}

当您&#x200B;**完成**&#x200B;报告时：

* 截至该时间点的报表定义&#x200B;*将用于拍摄快照（之后，您可以继续处理报表定义，因为它与快照相分离）。*
* 将删除任何现有快照。
* 将为[历史数据](#historic-data)收集新快照。

通过此对话框，您可以定义或更新生成报表的标题和说明。

![reportfish](assets/reportfinish.png)

## 报告类型{#report-types}

### 组件报告 {#component-report}

组件报告提供有关您的网站如何使用这些组件的信息。

[有关以](#selecting-and-positioning-the-data-columns) 下信息列：

* 作者
* 组件路径
* 组件类型
* 上次修改时间
* 页面

意指您可以看到，例如：

* 在何处使用哪些组件。

   有用，例如，测试时。

* 特定组件实例的分发方式。

   如果特定页面(即“繁页”)遇到性能问题。

* 确定更改频繁/较少的站点部分。
* 了解页面内容随时间推移的发展情况。

所有组件均包含在内，产品标准和项目特定。 使用&#x200B;**编辑**&#x200B;对话框，用户还可以设置定义报表起始点的&#x200B;**根路径** — 该根下的所有组件都将考虑报表。

![](assets/reportcomponent.png) ![reportcomponenterportcompletall](assets/reportcompentall.png)

### 磁盘使用情况 {#disk-usage}

磁盘使用情况报告显示有关存储在存储库中的数据的信息。

存储库的根(/)中的报表开始;通过单击特定分支，您可以在存储库内向下钻取（当前路径将反映在报表标题中）。

![reportdiskus](assets/reportdiskusage.png)

### 运行状况检查{#health-check}

此报表分析当前请求日志：

`<cq-installation-dir>/crx-quickstart/logs/request.log`
以帮助您确定给定时间段内最昂贵的请求。

要生成报表，您可以指定：

* **期间（小时）**

   要分析的小时数（过去）。

   默认: `24`

* **最大. 结果**

   最大输出行数。

   默认: `50`

* **最大. 请求**

   要分析的最大请求数。

   默认：`-1`（全部）

* **电子邮件地址**

   将结果发送到电子邮件地址。

   可选；默认：空白

* **每日运行时：(hh:mm)**

   指定报表每天自动运行的时间。

   可选；默认：空白

![报告](assets/reporthealth.png)

### 页面活动报告 {#page-activity-report}

页面活动报表会列表页面及对页面执行的操作。

[有关以](#selecting-and-positioning-the-data-columns) 下信息列：

* 页面
* 时间
* 类型
* 用户

意指您可以监控：

* 最新修改。
* 处理特定页面的作者。
* 最近未修改的页面，因此可能需要执行操作。
* 更改次数最多/最少的页面。
* 最多/最不活跃的用户。

页面活动报告从审计日志中获取其所有信息。 默认情况下，根路径配置为位于`/var/audit/com.day.cq.wcm.core.page`的审核日志。

![reportpageactivity](assets/reportpageactivity.png)

### 用户生成的内容报告 {#user-generated-content-report}

此报告提供有关用户生成内容的信息；无论是评论、评级还是论坛。

[有关的](#selecting-and-positioning-the-data-columns) 信息列：

* 日期
* IP 地址
* 页面
* 引用
* 类型
* 用户标识符

允许您：

* 查看哪些页面接收的注释最多。
* 获取特定网站访客离开的所有评论的概述，可能问题相关。
* 在页面上添加评论时，通过监控来判断新内容是否引发评论。

![reportusercontent](assets/reportusercontent.png)

### 用户报告 {#user-report}

本报告提供有关已注册帐户和/或用户档案的所有用户的信息；这可以包括组织内的作者和外部访客。

[有关以下信息](#selecting-and-positioning-the-data-columns) （如果可用）的列：

* 年龄
* 国家/地区
* 域
* 电子邮件
* 姓氏
* 性别
* [通用](#generic-column)
* 名字
* 信息
* 关注
* 语言
* NTLM 哈希码
* 用户 ID

允许您：

* 查看用户的人口统计分布。
* 报告您添加到用户档案的自定义字段。

![reportuseranced](assets/reportusercanned.png)

#### 常规列{#generic-column}

“用户报告”中提供了&#x200B;**Generic**&#x200B;列，以便您能够访问自定义信息，通常来自[用户用户档案](/help/sites-administering/identity-management.md#profiles-and-user-accounts);例如，[收藏颜色，详见“向用户档案定义添加字段”](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition)。

在以下任一情况下，将打开“常规”列对话框：

* 将通用组件从Sidekick拖动到报表。
* 为现有“通用”列选择“列属性”。

![reportusgeneralcorm](assets/reportusrgenericcolm.png)

在&#x200B;**定义**&#x200B;选项卡中，您可以定义：

* **标题**

   您自己的通用列标题。

* **属性**

   存储库中存储的属性名称，通常在用户的用户档案内。

* **路径**

   通常，属性取自`profile`。

* **类型**

   从`String`、`Number`、`Integer`、`Date`中选择字段类型。

* **默认聚合**

   这定义默认情况下使用的聚合，如果列在至少一个分组列的报表中取消分组。 从`Count`、`Minimum`、`Average`、`Maximum`、`Sum`中选择所需的聚合。

   例如，`String`字段的&#x200B;*计数*&#x200B;表示在聚集状态中显示列的不同值数。`String`

在&#x200B;**扩展**&#x200B;选项卡中，您还可以定义可用的聚合和过滤器:

![缩略图](assets/reportusrgenericcolmextented.png)

### 工作流实例报告 {#workflow-instance-report}

这为您提供了简洁的概述，提供了有关运行和完成的工作流的各个实例的信息。

[有关以](#selecting-and-positioning-the-data-columns) 下信息列：

* 已完成
* 持续时间
* 发起者
* 模型
* 有效负荷
* 启动时间
* 状态

这意味着您可以：

* 监测工作流的平均持续时间；如果经常发生这种情况，它会突出显示工作流的问题。

![报表流量](assets/reportworkflowintance.png)

### 工作流报告{#workflow-report}

这提供了有关实例上运行的工作流的关键统计信息。

![reportworkflow](assets/reportworkflow.png)

## 在发布环境{#using-reports-in-a-publish-environment}中使用报告

根据特定要求配置报表后，您可以激活报表以将配置转移到发布环境。

>[!CAUTION]
>
>如果希望发布环境具有&#x200B;**历史数据**，则在激活页面之前，在创作环境上完成&#x200B;****&#x200B;报告。

随后，可在

`/etc/reports`

例如，“用户生成的内容”报告可在以下位置找到：

`http://localhost:4503/etc/reports/ugcreport.html`

现在，将报告从发布环境收集的数据。

由于发布环境中不允许任何报告配置，因此&#x200B;**编辑**&#x200B;和&#x200B;**完成**&#x200B;按钮不可用。 但是，如果正在收集快照，可以为&#x200B;**历史数据**&#x200B;报表选择&#x200B;**期间**&#x200B;和&#x200B;**间隔**。

![reportsuckpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>访问这些报告可能是一个安全问题；因此，我们建议您配置调度程序，以便`/etc/reports`不适用于外部访客。 有关详细信息，请参阅[安全清单](security-checklist.md)。

## 运行报表{#permissions-needed-for-running-reports}所需的权限

所需的权限取决于操作：

* 报表数据基本上是使用当前用户的权限收集的。
* 历史数据是使用完成报告的用户的权限收集的。

在标准AEM安装中，为报表预设了以下权限：

* **用户报告**

   `user administrators`  — 读写

* **页面活动报告**

   `contributors`  — 读写

* **组件报告**

   `contributors`  — 读写

* **用户生成的内容报告**

   `contributors`  — 读写

* **工作流实例报告**

   `workflow-users`  — 读写

`administrators`组的所有成员都具有创建新报告的必要权限。
