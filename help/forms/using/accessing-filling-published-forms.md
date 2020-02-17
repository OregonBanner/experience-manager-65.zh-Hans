---
title: 访问和填写已发布的表单
seo-title: 访问和填写已发布的表单
description: Forms Portal为Web开发人员提供了组件，可在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
seo-description: Forms Portal为Web开发人员提供了组件，可在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 访问和填写已发布的表单{#accessing-and-filling-published-forms}

在以表单为中心的门户部署设置中，表单开发和门户开发是两个不同的活动。 表单设计人员在存储库中设计和存储表单时，Web开发人员会创建一个Web应用程序来列出表单并处理提交。 然后将表单复制到Web层，因为表单存储库和Web应用程序之间没有通信。

这通常会导致设置和生产延迟的管理问题。 例如，如果存储库中有较新版本的表单，则表单设计器将替换Web层上的表单，修改Web应用程序，并在公共站点上重新部署表单。 重新部署Web应用程序可能会导致某些服务器停机。 由于服务器停机是计划中的活动，因此无法立即将更改推送到公共站点。

Forms Portal减少了管理开销和生产延迟。 它为Web开发人员提供了组件，以便在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。

有关表单门户及其功能的详细信息，请参 [阅在门户上发布表单的介绍](/help/forms/using/introduction-publishing-forms.md)。

## 表单门户快速入门 {#getting-started-with-forms-portal}

导航到已发布的表单门户页面。 有关创建表单门户页面的详细信息，请参 [阅创建表单门户页面](../../forms/using/creating-form-portal-page.md)。

Roms门户的搜索和Lister组件显示AEM服务器的Publish实例上可用的表单。 此列表包括创作表单门户页面时在过滤器中定义的所有表单或表单。 表单门户页面的外观与下图所示类似：

![示例表单门户页面 ](assets/forms-portal-page.png)

示例表单门户页面

### 搜索和制表人 {#search-and-lister}

搜索和制表人组件允许您向表单门户添加以下功能：

* 在现成可用的面板、卡或网格视图中列出表单。 它还支持自定义模板从Forms manager中的特定文件夹列出表单。
* 指定表单的呈现方式- HTML5、PDF或两者。
* 指定PDF和XFA表单的呈现方式- HTML5、PDF或两者。 非XFA表单为HTML5。
* 支持根据条件（如表单属性、元数据和标记）搜索表单。
* 将表单数据提交到servlet。
* 使用自定义样式表(CSS)自定义门户的外观。
* 创建指向表单的链接。

您可以使用以下选项在“表单门户”页面中搜索表单：

* 全文搜索
* 高级搜索

通过全文搜索，您可以根据指定的关键字查找和列出表单。

![高级搜索对话框](assets/search-panel.png)

高级搜索对话框

“高级搜索”允许您根据指定的表单属性搜索表单。 与全文搜索相比，这提供了更具体的结果。 高级搜索包括基于标记、属性（如作者、描述和标题）、修改日期和全文的搜索。

Lister根据搜索参数显示表单。 搜索结果中的每个表单都会显示一个图标，该图标以超链接方式链接到关联的表单。 您可以单击该图标以打开并使用关联的表单。

### 填写表单 {#filling-a-form}

![示例自适应表单](assets/filling_a_form.png)

示例自适应表单

表单可以从页面的“搜索”和“制表人”组件中随表单一起提供的链接进行访问。

每个表单都包含帮助信息，使用户能够填写表单。

#### 草稿和提交 {#drafts-and-submission}

用户可以通过单击“保存”按钮来保存表单的草稿。 这允许用户在提交表单之前的一段时间内处理表单。

表单中填写的数据（包括附件）将作为草稿保存在服务器上。 表单的草稿可以保存任意次数。 保存的表单显示在页面的“草稿和提交”组件的“草稿”选项卡中。

填写表单后，用户单击表单上的“提交”按钮提交表单。 提交的表单显示在页面的“草稿和提交”组件的“提交”选项卡中。

>[!NOTE]
>
>仅当自适应表单的提交操作被配置为“表单门户提交操作”时，提交的表单才会显示在“已提交的表单”选项卡中。 有关提交操作的详细信息，请参 [阅配置提交操作](../../forms/using/configuring-submit-actions.md)。

![草稿和提交组件](assets/draft-submission.png)

草稿和提交组件

## Start a new form using submitted form data {#start-a-new-form-using-submitted-form-data}

您需要经常填写和提交某些表单。 例如，每年都提交个人纳税申报表。 在这种情况下，虽然每次填写表单时都会更改某些信息，但大多数信息与个人和家庭详细信息没有更改。 但是，您仍然需要从头开始重新填写整个表单。

AEM Forms有助于优化表单填写体验并大幅缩短再次填写和提交表单的时间。 最终用户可以使用提交表单中的数据启动新表单。 此功能内置于草稿和提 [交组件中](../../forms/using/draft-submission-component.md)。 当您将草稿和提交组件添加到表单门户页面并发布它时，最终用户将在“已提交的表单”和“草稿表单”选项卡中找到一个选项，以使用已提交表单中的数据启动新表单。 以下图像突出显示了此选项。

![开始——新表单](assets/start-a-new-form.png)

单击按钮以启动新表单时，该按钮将打开一个新表单，其中包含来自相应提交表单的数据。 您现在可以根据需要查看和更新信息，并提交表单。
