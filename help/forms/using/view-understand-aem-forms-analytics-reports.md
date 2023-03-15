---
title: 查看和了解AEM Forms analytics报表
seo-title: View and understand AEM Forms analytics reports
description: AEM Forms与Adobe Analytics集成，并为您提供有关已发布自适应表单的摘要和详细分析。
seo-description: AEM Forms integrates with Adobe Analytics and provides you summary and detailed analytics about your published adaptive forms.
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 2%

---

# 查看和了解AEM Forms analytics报表 {#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms与Adobe Analytics集成，允许您捕获和跟踪已发布表单和文档的性能指标。 分析这些指标的目的在于，根据有关使表单或文档更有用所需的更改的数据做出明智的决策。

## 设置分析 {#setting-up-analytics}

AEM Forms中的Analytics功能作为AEM Forms附加组件包的一部分提供。 有关安装附加组件包的信息，请参阅 [安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

除了附加组件包之外，您还需要Adobe Analytics帐户。 有关解决方案的信息，请参见 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

拥有AEM Forms附加组件包和Adobe Analytics帐户后，请将Adobe Analytics帐户与AEM Forms集成，并对您的表单或文档启用跟踪，如中所述 [配置分析和报表](../../forms/using/configure-analytics-forms-documents.md).

### 用户交互信息的记录方式 {#how-user-interaction-information-is-recorded}

当用户与表单交互时，交互将被记录并发送到Analytics服务器。 以下列表指示各种用户活动的服务器调用：

* 每次访问每个字段2次调用
* 1表示访问面板
* 1表示保存
* 2提交
* 2表示保存
* 1获取帮助
* 每个验证错误为1
* 1表示表单演绎版+ 1表示默认面板访问+ 1表示默认第1次字段访问
* 2表示表单放弃

>[!NOTE]
>
>这份清单并非详尽无遗。

### 查看Analytics报表 {#summary-report}

执行以下步骤可查看Analytics报表：

1. 登录到AEM门户，网址为 `https://[hostname]:'port'`
1. 单击 **Forms > Forms和文档**.
1. 选择要查看其分析报表的表单。
1. 选择 **更多> Analytics报表**.

![分析报告](assets/analyticsreport.png)

**答：** Analytics报表命令

AEM Forms显示表单的analytics报表以及表单中每个面板的报表，如下所示。

![自适应表单的摘要报告](assets/analyticsdashboard_callout.png)

**答：** 转化 **B.** 表单级别摘要 **C.** 面板级别摘要 **D.** 访客浏览器 — 过滤器 **E.** 访客的操作系统 — 过滤器 **F.** 访客语言 — 过滤器

默认情况下，将显示过去七天的Analytics报表。 您可以查看过去15天、上个月等的报告，或指定日期范围。

>[!NOTE]
>
>“最近7天”和“最近15天”等选项不包含您生成分析报表的当天数据。 要包含当天的数据，您需要指定包含当天的日期范围，然后运行报表。

![date-range](assets/date-range.png)

### 自适应表单和HTML5表单的转化图 {#conversions-graph-for-adaptive-and-html-forms}

表单级转化图让您深入了解表单在下列关键绩效指标(KPI)上的执行情况：

* **演绎版**：表单被打开的次数
* **访客**：表单的访客数量
* **提交内容**：提交表单的次数

![转化图](assets/conversion-graph.png)

### 自适应和HTML5表单的Analytics报表 {#analytics-report-for-adaptive-and-html-forms}

表单级别摘要部分让您深入了解表单对以下关键绩效指标(KPI)的执行情况：

* **平均填充时间**：填写表单所用的平均时间。 当用户将时间花费在表单上但未提交时，该时间不计入此计算中。
* **演绎版**：表单已呈现或打开的次数
* **草稿**：表单另存为草稿的次数
* **提交内容**：提交表单的次数
* **中止**：用户开始填写表单然后离开而未完成表单的次数
* **独特访客**：表单由独特访客呈现的次数。 有关独特访客的更多信息，请参阅 [独特访客、访问次数和客户行为](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html).

![扩展的表单级摘要分析报告](assets/analytics-report.png)

### 面板报告 {#bottom-summary-report}

面板级别的摘要部分提供有关表单中每个面板的以下信息：

* **平均填充时间**：在面板上花费的平均时间，无论是否提交表单
* **遇到的错误**：用户在面板中的字段遇到的平均错误数。 遇到的错误通过将字段中的错误总数除以表单的演绎版数得出。
* **已访问帮助**：用户访问面板中字段的上下文帮助的平均次数。 访问帮助的次数是将某个字段访问帮助的总次数除以表单的演绎版数。

#### 详细的面板报告 {#detailed-panel-report}

您还可以通过单击面板报表中的面板名称来查看每个面板的详细信息。

![详细的面板报告](assets/panel-report-detailed.png)

详细报告显示面板中所有字段的值。

“面板报告”有三个选项卡：

* **时间报表**（默认）：显示填写面板中每个字段所花费的时间（以秒为单位）
* **错误报告**：显示用户在填写字段时遇到的错误数
* **帮助报告**：访问特定字段的帮助的次数

如果多个面板可用，则您可以在面板之间导航。

### 过滤器：浏览器、操作系统和语言 {#filters-browser-os-and-language}

“浏览器分发”、“OS分发”和“语言分发”表根据表单用户的浏览器、操作系统和语言显示演绎版、访客和提交内容。 默认情况下，这些表格最多可显示五个条目。 您可以单击显示更多以显示更多条目，然后单击显示更少以返回常规五个或更少条目。

要进一步筛选分析数据，您可以单击任何表中的条目。 例如，如果单击“浏览器分发”表中的Google Chrome，则报表将再次渲染为与Google Chrome浏览器相关的数据，如下所示：

![应用于Analytics报表的筛选器 — Google Chrome ](assets/filter-1.png)

如果在应用过滤器后查看面板报告，则也会根据应用的过滤器显示面板报告数据。

应用过滤器后：

* 分发表变为只读，因为一次只能应用一个过滤器。
* 应用的过滤器的表消失。
* 您可以单击“关闭”按钮（突出显示于下方）以删除应用的过滤器。

![“关闭”按钮可删除应用的过滤器](assets/close-filter.png)

### A/B测试 {#a-b-testing}

如果您已启用并设置了表单的A/B测试，则报表页面中有一个下拉菜单，您可以使用它来显示A/B测试报表。 A/B测试报告显示您设置的两个版本表单的比较性能。

有关A/B测试的更多信息，请参阅 [创建和管理自适应表单的A/B测试](../../forms/using/ab-testing-adaptive-forms.md).
