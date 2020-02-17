---
title: 查看和了解AEM Forms分析报告
seo-title: 查看和了解AEM Forms分析报告
description: AEM Forms与Adobe Analytics集成，为您提供有关已发布自适应表单的摘要和详细分析。
seo-description: AEM Forms与Adobe Analytics集成，为您提供有关已发布自适应表单的摘要和详细分析。
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 查看和了解AEM Forms分析报告{#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms与Adobe Analytics集成，使您能够捕获和跟踪已发布表单和文档的性能指标。 分析这些指标的目的是根据使表单或文档更易用所需的更改数据做出明智决策。

## 设置分析 {#setting-up-analytics}

AEM Forms中的分析功能可作为AEM Forms加载项包的一部分使用。 有关安装加载项包的信息，请参 [阅安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

除了附加包，您还需要一个Adobe Analytics帐户。 有关该解决方案的信息，请参 [阅Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

在您拥有AEM Forms加载项包和Adobe Analytics帐户后，将Adobe Analytics帐户与AEM Forms集成，并启用对表单或文档的跟踪，如配置分析和报 [告中所述](../../forms/using/configure-analytics-forms-documents.md)。

### 如何记录用户交互信息 {#how-user-interaction-information-is-recorded}

当用户与表单交互时，将记录交互并发送到Analytics服务器。 以下列表指示服务器对各种用户活动的调用：

* 每次现场访问2次
* 1个小组访问
* 1表示保存
* 提交2份
* 2，保存
* 1寻求帮助
* 每个验证错误为1
* 对于表单再现+ 1（对于默认面板），请访问+ 1（对于默认的第1次字段访问）
* 2表单放弃

>[!NOTE]
>
>此列表并非详尽无遗。

### 查看分析报告 {#summary-report}

执行以下步骤以查看分析报告：

1. 登录AEM门户网站： `https://[hostname]:[port]`
1. 单击“ **表单”>“表单和文档”**。
1. 选择要查看其分析报告的表单。
1. 选择 **更多>分析报告**。

![分析报告](assets/analyticsreport.png)

**** 答：分析报告命令

AEM Forms显示表单的分析报告以及表单中每个面板的分析报告，如下所示。

![自适应表单的摘要报告](assets/analyticsdashboard_callout.png)

************ 答：转 **化B.表单级摘要** C.**面板级摘要** D.访客的浏览器——过 **滤器E。访客操作系统——过**&#x200B;滤器F。访客语言——过滤器

默认情况下，将显示最近七天的分析报告。 您可以查看最近15天、上个月等的报告，或指定日期范围。

>[!NOTE]
>
>过去7天和过去15天等选项不包括生成分析报告的当天的数据。 要包含当天的数据，您需要指定包括当天在内的日期范围，然后运行报告。

![date-range](assets/date-range.png)

### 自适应和HTML5表单的转换图 {#conversions-graph-for-adaptive-and-html-forms}

通过表单级转换图，您可以深入了解表单在下列关键绩效指标(KPI)上的表现：

* **再现**:表单的打开次数
* **访客**:表单的访客数
* **提交**:提交表单的次数

![转换图](assets/conversion-graph.png)

### 自适应和HTML5表单的分析报告 {#analytics-report-for-adaptive-and-html-forms}

通过表单级摘要部分，您可以深入了解表单在下列关键绩效指标(KPI)上的表现：

* **平均填充时间**:填写表单的平均时间。 当用户在表单上花费时间但不提交时，该时间不会包含在此计算中。
* **再现**:表单的呈现或打开次数
* **草稿**:表单保存为草稿的次数
* **提交**:提交表单的次数
* **中止**:用户开始填写表单然后离开而不填写表单的次数
* **唯一访客**:表单由唯一访客呈现的次数。 有关独特访客的详细信息，请参 [阅独特访客、访问和客户行为](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html)。

![扩展的表单级摘要分析报告](assets/analytics-report.png)

### Panel report {#bottom-summary-report}

面板级摘要部分提供了有关表单中每个面板的以下信息：

* **平均填充时间**:在面板上平均花费的时间，无论是否提交表单
* **遇到的错误**:用户在面板中的字段上遇到的平均错误数。 “遇到的错误”是通过将字段中的总错误除以表单的演绎版数量得出的。
* **访问的帮助**:用户访问面板中字段的上下文内帮助的平均次数。 通过将字段的帮助访问总次数除以表单的演绎版数，即可获得“访问的帮助”。

#### 详细面板报告 {#detailed-panel-report}

您还可以通过在面板报告中单击面板名称来查看每个面板的详细信息。

![详细面板报告](assets/panel-report-detailed.png)

详细报告显示面板中所有字段的值。

面板报告有三个选项卡：

* **时间报告**（默认）:显示填充面板中每个字段所花费的时间（以秒为单位）
* **错误报告**:显示填写字段时用户遇到的错误数
* **帮助报告**:访问特定字段的帮助的次数

如果多个面板可用，则可以在这些面板之间导航。

### 过滤器：浏览器、操作系统和语言 {#filters-browser-os-and-language}

“浏览器分发”、“操作系统分发”和“语言分发”表按表单用户的浏览器、操作系统和语言显示再现、访客和提交内容。 默认情况下，这些表最多显示五个条目。 单击“显示更多”可显示更多条目，单击“显示更少”可返回到五个或更少的常规条目。

要进一步筛选分析数据，您可以单击任意表中的条目。 例如，如果单击“浏览器分发”表中的Google Chrome，则报表将再次呈现，其中包含与Google Chrome浏览器相关的数据，如下所示：

![应用于Analytics报告的过滤器- Google Chrome ](assets/filter-1.png)

如果在应用过滤器后查看面板报告，则面板报告数据也会根据应用的过滤器显示。

应用过滤器后：

* 分发表变为只读，因为一次只能应用一个筛选器。
* 应用的滤镜的表消失。
* 您可以单击“关闭”按钮（在下面高亮显示）以删除已应用的过滤器。

![关闭按钮以删除已应用的滤镜](assets/close-filter.png)

### A/B测试 {#a-b-testing}

如果您启用了A/B测试并为表单进行了设置，则报表页面中会显示一个下拉框，您可以使用它显示A/B测试报表。 A/B测试报告显示您设置的两个版本的表单的比较性能。

有关A/B测试的详细信息，请参 [阅创建和管理自适应表单的A/B测试](../../forms/using/ab-testing-adaptive-forms.md)。
