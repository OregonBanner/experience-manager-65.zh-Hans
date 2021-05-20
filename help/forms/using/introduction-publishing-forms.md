---
title: 在门户上发布表单简介
seo-title: 在门户上发布表单简介
description: AEM Forms提供了可用于构建表单门户的组件。 本文将介绍可用的Forms门户组件。
seo-description: AEM Forms提供了可用于构建表单门户的组件。 本文将介绍可用的Forms门户组件。
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# 在门户上发布表单简介{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms Portal组件概述{#aem-forms-portal-components-overview}

在典型的以表单为中心的门户部署场景中，表单开发和门户开发是两个不相干的活动。 表单设计人员在存储库中设计和存储表单时， Web开发人员会创建一个Web应用程序来列出表单和处理表单提交。 Forms将复制到Web层，因为表单存储库与Web应用程序之间没有通信。

这种情况往往导致管理问题和生产延迟。 例如，如果存储库中有较新版本的表单可用，则需要替换Web层上的表单，修改Web应用程序，并在公共网站上重新部署该表单。 重新部署Web应用程序可能会导致服务器停机。 通常，服务器停机是计划的活动，因此更改不能即时推送到公共站点。

AEM Forms提供门户组件，可减少管理开销和生产延迟。 这些组件使Web开发人员能够在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。

![AEM Forms门户](assets/aem-forms-portal.png)

利用表单门户组件，可添加以下功能：

* 以自定义布局列出表单。 提供了开箱即用的列表视图、卡片视图和面板视图布局。 您可以创建自己的自定义布局。
* 允许您在列出自定义元数据和自定义操作时显示这些元数据。
* 在使用AEM Forms Portal组件的发布实例上列出由Forms UI发布的表单。
* 允许最终用户以HTML和PDF格式呈现表单。
* 使用自定义HTML配置文件渲染表单。
* 允许根据各种条件（如表单属性、元数据和标记）搜索表单。
* 将表单数据提交到Servlet。
* 使用自定义CSS自定义门户的外观。
* 创建指向表单的链接。
* 列出与最终用户创建的自适应表单相关的草稿和提交。

## 可用的AEM Forms门户组件{#available-aem-forms-portal-components}

AEM Forms提供了以下开箱即用的门户组件，这些组件分组在&#x200B;**Document Services**&#x200B;和&#x200B;**Document Services谓词**&#x200B;组件组下：

### 搜索和制表人 {#search-amp-lister}

搜索和制表人组件允许您从表单存储库将表单列到您的门户页面上，并提供根据指定条件列出表单的配置选项。 它还允许您指定搜索标准，以便门户用户能够在表单列表中进行搜索。

### 草稿和提交 {#drafts-amp-submissions}

搜索和制表人组件显示由Forms作者公开的表单，而草稿和提交组件则显示另存为草稿的表单，以供日后完成和提交的表单。 此组件可为任何已登录的用户提供个性化体验。

### 链接 {#link}

链接组件允许您创建指向页面上任意位置表单的链接。 假设您提供了培训计划，并且希望用户提交表格以注册培训。 你已经在你的网站上公布了节目细节。 在详细信息下方，您希望提供指向注册表单的链接。 链接组件可帮助您创建该链接。

## Forms门户工作流{#forms-portal-workflow}

Forms Portal允许您将表单从表单存储库列到门户页面上。 它还允许您指定搜索标准，以便门户用户能够在表单列表中进行搜索。 您还可以使用“草稿和提交”组件显示另存为草稿的表单，以供日后完成提交的表单。 在站点页面上提供这些功能之前，您必须执行一组特定操作。 按照所列顺序执行步骤，在站点页面上提供组件和各自的功能：

1. **启用Forms Portal组件**:开箱即用的表单门户组件不可用。[从AEM Sidekick为AEM Sites页](/help/forms/using/enabling-forms-portal-components.md) 面启用组件。
1. **在页面上列出表单（创建表单门户页面）：** 您可以在AEM Sites和非AEM网站页面上列出表单。列表包含发布实例上可用的表单。 用户可以打开表单并开始填写这些表单。 每当用户打开表单时，都会创建表单的新实例：

   1. **在AEM Sites页面上列出表单**:将搜索 **[和列](../../forms/using/creating-form-portal-page.md)** 表组件添加到页面并配置 **[列表](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 面板，以在页面上列出表单。将&#x200B;**搜索窗格**&#x200B;组件添加到&#x200B;**搜索和制表人**&#x200B;组件，并将其配置为向页面添加搜索功能。 具有Forms Portal组件的页面称为[Forms Portal页面](../../forms/using/creating-form-portal-page.md)。

   1. **在非AEM Sites页面上列出表单：** 使用 [Forms Portal搜索](/help/forms/using/listing-forms-webpage-using-apis.md) API，查询、检索和列出非AEM Sites页面上的表单。

1. **在表单门户页面上列出草稿和提交的表单**:将“草稿和提交”组件添加并配置到表单门户页面。组件列出了处于草稿状态的所有表单以及已提交的表单。

   要使提交的自适应表单显示在提交选项卡中，请将&#x200B;**Submit action**&#x200B;设置为&#x200B;**[Forms Portal Submit Action](configuring-submit-actions.md)。** 或者，启用Forms Portal提交选项。每当用户提交表单时，表单都会添加到提交选项卡。

1. **为草稿和已提交的表单数据配置存储：** 默认情况下，草稿和已提交的数据存储在AEM存储库中。在生产环境中，建议不要将草稿或提交的表单数据存储在AEM存储库中。 [配置Forms Portal组件以将数据保存到安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage)。
1. **（可选）自定义表单门户组件：** [自定义您的表单门户](../../forms/using/customizing-templates-forms-portal-components.md) 页面模板，以为组件提供独特的外观。
1. **（可选）将自定义元数据添加到表单：** [将自定义元数据添加](../../forms/using/customizing-templates-forms-portal-components.md) 到表单，以改善列表和搜索体验。
1. **发布Forms门户页面：** 您的Forms门户页面现已准备就绪。发布页面。

## 相关文章{#related-articles}

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](../../forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](../../forms/using/draft-submission-component.md)
* [自定义草稿和提交表单的存储](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [将草稿和提交组件与数据库集成的示例](integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](../../forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](../../forms/using/introduction-publishing-forms.md)
