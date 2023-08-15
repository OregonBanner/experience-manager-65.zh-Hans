---
title: 访问和填写已发布的表单
description: Forms Portal为Web开发人员提供了组件，以便在使用Adobe Experience Manager (AEM)创作的网站上创建和自定义表单门户。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# 访问和填写已发布的表单{#accessing-and-filling-published-forms}

在以表单为中心的门户部署设置中，表单开发和门户开发是两个不同的活动。 当表单设计人员将表单设计和存储在存储库中时，Web开发人员会创建一个Web应用程序来列出表单并处理提交。 Forms随后将复制到Web层，因为Forms存储库和Web应用程序之间没有通信。

这通常会导致在管理设置和生产延迟时出现问题。 例如，如果存储库中有较新版本的表单可用，则表单设计器会替换Web层上的表单、修改Web应用程序并重新部署公共站点上的表单。 重新部署Web应用程序可能会导致某些服务器停机。 由于服务器停机是计划的活动，因此不能将更改立即推送到公共站点。

Forms Portal可减少管理开销和生产延迟。 它为Web开发人员配备了组件，以便在使用Adobe Experience Manager (AEM)创作的网站上创建和自定义表单门户。

有关Forms Portal及其功能的详细信息，请参阅 [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md).

## Forms Portal入门 {#getting-started-with-forms-portal}

导航到已发布的表单门户页面。 有关创建表单门户页面的详细信息，请参阅 [创建表单门户页面](../../forms/using/creating-form-portal-page.md).

roms portal的Search and Lister组件显示AEM服务器的Publish实例上可用的表单。 此列表包含在创作Forms Portal页面时在筛选器中定义的所有表单或表单。 如下图所示，Forms Portal页面看起来类似：

![一个示例表单门户页面 ](assets/forms-portal-page.png)

一个示例表单门户页面

### 搜索和侦听器 {#search-and-lister}

通过搜索和列表程序组件，可将以下功能添加到表单门户：

* 在面板、卡片或网格视图中列出现成可用的表单。 它还支持Forms Manager中特定文件夹的自定义templatesList表单。
* 指定表单的呈现方式 — HTML5、PDF或两者。
* 指定PDF和XFA表单的呈现方式 — HTML5、PDF或两者。 非XFA表单作为HTML5。
* 启用基于条件（如表单属性、元数据和标记）的表单搜索。
* 将表单数据提交到Servlet。
* 使用自定义样式表(CSS)自定义门户的外观。
* 创建表单链接。

您可以使用以下选项在Forms Portal页面中搜索表单：

* 全文搜索
* 高级搜索

全文搜索允许您根据指定的关键词查找和列出表单。

![高级搜索对话框](assets/search-panel.png)

高级搜索对话框

高级搜索允许您根据指定的表单属性搜索表单。 这比全文搜索提供更具体的结果。 高级搜索包括基于标记、属性（如“作者”、“描述”和“标题”）、修改日期和全文的搜索。

列表程序根据搜索参数显示表单。 搜索结果中的每个表单都显示有一个图标，该图标超链接到关联的表单。 您可以单击图标以打开并处理关联的表单。

### 填写表单 {#filling-a-form}

![自适应表单示例](assets/filling_a_form.png)

自适应表单示例

可以通过与页面的“搜索和列表程序”组件中的表单一起提供的链接来访问表单。

每个表单都包含帮助信息，可让用户填写表单。

#### 草稿和提交 {#drafts-and-submission}

用户可以选择通过单击保存表单草稿 **保存**. 这样，用户就可以在提交表单之前处理一段时间内的表单。

在表单中填写的数据（包括附件）将作为草稿保存在服务器上。 表单的草稿可以保存任意次数。 保存的表单将显示在页面的“草稿和提交”组件的“草稿”选项卡中。

填写完表单后，用户通过单击表单上的提交按钮提交表单。 提交的表单会显示在页面草稿和提交组件的提交选项卡中。

>[!NOTE]
>
>仅当自适应表单的提交操作配置为Forms Portal提交操作时，已提交的表单才会显示在已提交的Forms选项卡中。 有关提交操作的详细信息，请参阅 [配置提交操作](../../forms/using/configuring-submit-actions.md).

![草稿和提交组件](assets/draft-submission.png)

草稿和提交组件

## 使用提交的表单数据开始新表单 {#start-a-new-form-using-submitted-form-data}

有些表格您必须经常填写和提交。 例如，个人纳税申报单每年都会提交。 在这种情况下，尽管每次填写表单时某些信息都会更改，但大多数信息（如个人和家庭详细信息）不会更改。 但是，您仍需要从头开始再次填写整个表单。

AEM Forms可帮助优化表单填写体验，并显着减少再次填写和提交表单的时间。 最终用户可使用已提交表单中的数据启动新表单。 此功能内置于 [草稿和提交组件](../../forms/using/draft-submission-component.md). 在将草稿和提交组件添加到Forms Portal页面并进行发布时，最终用户会在已提交的Forms和草稿Forms选项卡中看到一个选项，该选项可使用已提交表单中的数据创建新表单。 下图突出显示了该选项。

![开始 — 新建 — 表单](assets/start-a-new-form.png)

当您单击按钮以创建新表单时，它会打开一个新表单，其中包含来自相应已提交表单的数据。 您现在可以根据需要查看和更新信息，并提交表单。
