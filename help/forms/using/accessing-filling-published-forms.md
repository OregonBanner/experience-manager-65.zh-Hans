---
title: 访问和填写已发布的表单
seo-title: 访问和填写已发布的表单
description: Forms门户为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
seo-description: Forms门户为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# 访问和填写已发布的表单{#accessing-and-filling-published-forms}

在以表单为中心的门户部署设置中，表单开发和门户开发是两个不同的活动。 在表单设计人员在存储库中设计和存储表单时， Web开发人员会创建一个Web应用程序，以列出表单并处理提交。 然后，Forms将复制到Web层，因为表单存储库与Web应用程序之间没有通信。

这通常会导致管理设置和生产延迟时出现问题。 例如，如果存储库中提供了较新版本的表单，则表单设计器将替换Web层上的表单，修改Web应用程序，并在公共网站上重新部署该表单。 重新部署Web应用程序可能会导致服务器停机。 由于服务器停机是计划活动，因此无法立即将更改推送到公共站点。

Forms Portal减少了管理开销和生产延迟。 它为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。

有关表单门户及其功能的更多信息，请参阅[在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)。

## Forms Portal入门{#getting-started-with-forms-portal}

导航到已发布的表单门户页面。 有关创建Forms门户页面的更多信息，请参阅[创建Forms门户页面](../../forms/using/creating-form-portal-page.md)。

Roms Portal的Search和Lister组件显示AEM Server的Publish实例上可用的表单。 此列表包含创作表单门户页面时过滤器中定义的所有表单或表单。 表单门户页面与类似，如下图所示：

![表单门户页面示例  ](assets/forms-portal-page.png)

表单门户页面示例

### 搜索和制表人{#search-and-lister}

搜索和制表人组件允许您向表单门户添加以下功能：

* 在面板、卡片或网格视图中列出现成可用的表单。 它还支持Forms Manager中特定文件夹中的自定义模板列表表单。
* 指定表单的呈现方式 — HTML5、PDF或两者。
* 指定PDF和XFA表单的呈现方式 — HTML5、PDF或两者。 非XFA表单为HTML5。
* 允许根据条件（如表单属性、元数据和标记）搜索表单。
* 将表单数据提交到Servlet。
* 使用自定义样式表(CSS)自定义门户的外观。
* 创建指向表单的链接。

您可以使用以下选项在Forms Portal页面中搜索表单：

* 全文搜索
* 高级搜索

通过全文搜索，您可以查找并列出基于指定关键词的表单。

![高级搜索对话框](assets/search-panel.png)

高级搜索对话框

“高级搜索”允许您根据指定的表单属性搜索表单。 与全文搜索相比，这提供了更具体的结果。 高级搜索包括基于标记、属性（如“作者”、“描述”和“标题”）、修改日期和全文的搜索。

Lister根据搜索参数显示表单。 搜索结果中的每个表单都会显示一个图标，该图标已添加到关联表单的超链接。 您可以单击图标以打开并使用关联的表单。

### 填写表单{#filling-a-form}

![自适应表单示例](assets/filling_a_form.png)

自适应表单示例

可以从页面搜索和Lister组件中随表单一起提供的链接访问表单。

每个表单都包含帮助信息，使用户能够填写表单。

#### 草稿和提交{#drafts-and-submission}

用户可以通过单击保存按钮来保存表单草稿。 这允许用户在提交表单之前的一段时间内处理表单。

在表单（包括附件）中填写的数据将作为草稿保存在服务器上。 表单草稿可保存任意次数。 保存的表单会显示在页面草稿和提交组件的草稿选项卡中。

填写完表单后，用户单击表单上的“提交”按钮提交表单。 提交的表单显示在页面草稿和提交组件的提交选项卡中。

>[!NOTE]
>
>仅当将自适应表单的提交操作配置为Forms Portal提交操作时，提交的表单才会显示在已提交的Forms选项卡中。 有关提交操作的更多信息，请参阅[配置提交操作](../../forms/using/configuring-submit-actions.md)。

![草稿和提交组件](assets/draft-submission.png)

草稿和提交组件

## 使用提交的表单数据{#start-a-new-form-using-submitted-form-data}启动新表单

您需要经常填写和提交某些表单。 例如，每年提交个人纳税申报表。 在这种情况下，虽然每次填写表格时，某些信息都会发生变化，但大多数信息与个人和家庭的详细信息没有变化。 但是，您仍需要从头开始再次填写整个表单。

AEM Forms可帮助优化表单填写体验，并显着减少填写和再次提交表单的时间。 最终用户可以使用已提交表单中的数据启动新表单。 此功能内置于[草稿和提交组件](../../forms/using/draft-submission-component.md)中。 在将草稿和提交组件添加到表单门户页面并发布该组件后，最终用户将在已提交的Forms和草稿Forms选项卡中找到一个选项，以使用已提交表单中的数据开始新表单。 下图突出显示了该选项。

![start-a-new-form](assets/start-a-new-form.png)

单击按钮以启动新表单时，将打开一个新表单，其中包含来自相应已提交表单的数据。 您现在可以根据需要查看和更新信息，并提交表单。
