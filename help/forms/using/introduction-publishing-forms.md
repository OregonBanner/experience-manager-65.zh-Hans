---
title: 在门户上发布表单的简介
description: Adobe Experience Manager Forms提供了可用于构建Forms Portal的组件。 向您介绍可用的Forms Portal组件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 1%

---

# 在门户上发布表单的简介{#introduction-to-publishing-forms-on-a-portal}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | 本文 |


## AEM Forms portal组件概述 {#aem-forms-portal-components-overview}

在以表单为中心的典型门户部署方案中，表单开发和门户开发是两个相互分离的活动。 当表单设计人员将表单设计和存储在存储库中时，Web开发人员会创建一个Web应用程序来列出表单并处理表单提交。 Forms将会复制到Web层，因为Forms存储库和Web应用程序之间没有通信。

这种情形往往导致管理问题和生产延迟。 例如，如果存储库中有较新版本的表单，则必须在Web层上替换表单、修改Web应用程序并在公共站点上重新部署表单。 重新部署Web应用程序可能会导致某些服务器停机。 通常，服务器停机是计划内活动，因此更改无法即时推送到公共站点。

AEM Forms提供门户组件，可减少管理开销和生产延迟。 这些组件让Web开发人员能够在使用Forms (AEM)创作的网站上创建和自定义Adobe Experience Manager门户。

![AEM Forms门户](assets/aem-forms-portal.png)

利用表单门户组件，可添加以下功能：

* 以自定义布局列出表单。 现成提供列表视图、卡片视图和面板视图布局。 您可以创建自己的自定义布局。
* 允许您在列出自定义元数据和自定义操作时显示它们。
* 列出使用AEM Forms Portal组件的发布实例上由Forms UI发布的表单。
* 允许最终用户以HTML和PDF格式呈现表单。
* 使用自定义HTML配置文件渲染表单。
* 启用基于各种条件（如表单属性、元数据和标记）的表单搜索。
* 将表单数据提交到Servlet。
* 使用自定义CSS可自定义门户的外观。
* 创建表单链接。
* 列出与最终用户创建的自适应表单相关的草稿和提交。

## 可用的AEM Forms Portal组件 {#available-aem-forms-portal-components}

AEM Forms现成提供以下门户组件，这些组件分组在 **文档服务** 和 **文档服务谓词** 组件组：

### 搜索和列表程序 {#search-amp-lister}

通过搜索和列表程序组件，您可以将表单存储库中的表单列出到门户页面上，并提供配置选项来根据指定条件列出表单。 它还允许您指定搜索条件，以使门户用户能够在表单列表中搜索。

### 草稿和提交 {#drafts-amp-submissions}

虽然搜索和列表组件显示由Forms作者公开的表单，但草稿和提交组件显示另存为草稿的表单，以供以后填写和提交的表单。 此组件可为任何登录用户提供个性化体验。

### 链接 {#link}

使用链接组件，可在页面上的任意位置创建指向表单的链接。 考虑这样一种情景：您提供培训方案，希望用户提交表单以注册参加培训。 您已在您的网站上发布了该计划的详细信息。 在详细信息下方，您要提供注册表单的链接。 链接组件可以帮助您创建该链接。

## Forms Portal工作流 {#forms-portal-workflow}

Forms门户允许您将表单从表单存储库列出到门户页面上。 它还允许您指定搜索条件，以使门户用户能够在表单列表中搜索。 您还可以使用草稿和提交组件显示另存为草稿的表单，以供稍后完成和提交表单。 在这些功能在Sites页面上可用之前，您需要执行一组特定操作。 按照列出的顺序执行步骤，使组件和相应的功能在站点页面上可用：

1. **启用Forms Portal组件**：现成的Forms Portal组件不可使用。 [从AEM Sidekick启用组件](/help/forms/using/enabling-forms-portal-components.md) 用于AEM Sites页面。
1. **在页面上列出表单(创建Forms Portal页面)：** 您可以在AEM Sites和非AEM站点页面上列出表单。 该列表包含发布实例上可用的表单。 用户可以打开表单并开始填写这些表单。 每当用户打开表单时，都会创建一个表单的新实例：

   1. **在AEM Sites页面上列出表单**：添加 **[搜索和列表程序](../../forms/using/creating-form-portal-page.md)** 组件到页面并配置 **[列表窗格](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 在中，在页面上列出表单。 添加并配置 **搜索窗格** 组件到 **搜索和列表程序** 组件向页面中添加搜索功能。 将包含Forms Portal组件的页面称为 [Forms Portal页面](../../forms/using/creating-form-portal-page.md).

   1. **在非AEM Sites页面上列出表单：** 使用 [Forms Portal搜索API](/help/forms/using/listing-forms-webpage-using-apis.md) 在非AEM Sites页面上查询、检索和列出表单。

1. **在Forms门户页面上列出草稿和已提交的表单**：将草稿和提交组件添加并配置到Forms Portal页面。 组件列出了处于草稿状态的所有表单以及已提交的表单。

   要使提交的自适应表单显示在提交选项卡中，请设置 **提交操作** 到 **[Forms Portal提交操作](configuring-submit-actions.md).** 或者，启用Forms Portal提交选项。 每当用户提交表单时，该表单都会添加到提交选项卡。

1. **为草稿和已提交的表单数据配置存储：** 默认情况下，草稿和提交数据存储在AEM存储库中。 在生产环境中，建议不要将草稿或已提交的表单数据存储在AEM存储库中。 [配置Forms Portal组件以将数据保存到安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **（可选）自定义Forms Portal组件：** [自定义Forms Portal页面模板](../../forms/using/customizing-templates-forms-portal-components.md) 为组件提供独特的外观。
1. **（可选）将自定义元数据添加到表单：** [将自定义元数据添加到表单](../../forms/using/customizing-templates-forms-portal-components.md) 以改善列表和搜索体验。
1. **发布Forms Portal页面：** 您的Forms门户页面现已准备就绪。 发布页面。

## 相关文章 {#related-articles}

* [启用Forms Portal组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建Forms门户页面](../../forms/using/creating-form-portal-page.md)
* [使用API列出网页上的表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](../../forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [将草稿和提交组件与数据库集成的示例](integrate-draft-submission-database.md)
* [自定义Forms Portal组件的模板](../../forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](../../forms/using/introduction-publishing-forms.md)
