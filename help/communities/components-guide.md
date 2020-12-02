---
title: 社区组件指南
seo-title: 社区组件指南
description: 一个交互式开发工具，用于开始使用社交组件框架(SCF)
seo-description: 一个交互式开发工具，用于开始使用社交组件框架(SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---


# 社区组件指南  {#community-components-guide}

社区组件指南是[社交组件框架(SCF)](scf.md)的交互式开发工具。 它提供可用的AEM Communities组件列表或由多个组件构建的更复杂的功能。

除了每个组件的基本信息，该指南还允许对SCF组件／功能的工作方式以及配置或自定义它们的方式进行试验。

有关每个组件相关的开发必备工具的信息，请参阅[功能和组件必备工具](essentials.md)。

## 入门 {#getting-started}

本指南适用于作者(localhost:4502)和发布(localhost:4503)实例的开发安装。

通过浏览到

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

与社区组件的交互将因以下各项而异：

* 服务器（作者或发布）。
* 站点访客是否已登录。
* 如果已登录，则指定给成员的权限。
* 是否使用默认SRP [JSRP](jsrp.md)。

在创作时，要进入编辑模式，请在服务器名后插入`editor.html`或`cf#`作为第一个路径段：

* 标准 UI:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 经典 UI：

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>在“编辑”模式下进行创作时，页面上的链接不处于活动状态。
>
>要导航到组件页面，请首先选择预览模式以激活链接。
>
>在浏览器中显示组件页面时，返回编辑模式以打开组件的编辑对话框。
>
>有关一般创作信息，请视图[页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请视图有关[基本操作](../../help/sites-authoring/basic-handling.md)的文档。

### 主页 {#home-page}

本指南提供了一系列SCF组件，可用于预览和沿页面左侧进行原型设计。

组件指南，如在编辑模式下在作者实例上查看：

![community-component1](assets/community-component1.png)

## 组件页{#component-pages}

从页面左侧的列表中选择组件。

![社区组件——页面](assets/community-component2.png)

向导的主体显示：

1. 标题：所选组件的名称
1. [客户端库](#client-side-libraries):列表一个或多个必需类别
1. [包括](scf.md#add-or-include-a-communities-component):如果组件可以动态包含，则可以在作者编辑模式下切换状态：

   * 如果添加，则显示的文本为：“此组件通过其par节点提供。”
   * 如果包括，则显示的文本为：“此组件是动态包含的。”
   * 如果不包括，则不显示任何文本

1. 示例组件或功能：组件或功能的活动实例。 如果某个组件，则可能会随着对选项卡部分中提供的模板、CSS和数据所做的更改而改变它。

>[!NOTE]
>
>从左侧进行选择后，当浏览器窗口过窄时，组件将显示在组件列表的下方而不是旁边。

### 创作交互{#author-interactions}

在创作实例上使用指南时，可以通过打开组件对话框来体验配置组件的过程。 文档的[组件和功能要素](essentials.md)部分提供开发人员信息，而创作的[社区组件](author-communities.md)部分介绍了对话框设置。

对于“社区组件”指南，某些组件对话框设置会以[Includable](scf.md#add-or-include-a-communities-component)切换状态覆盖。 要在使用现有资源或动态包含的资源之间进行切换，请在编辑模式下同时选择组件和可包含文本，并单击多次以打开编辑对话框：

![社区组件3](assets/community-component3.png)

在&#x200B;**模板**&#x200B;选项卡下：

![community-component4](assets/community-component4.png)

* **通过 sling:include 包含子组件**

   如果未选中，组件指南将使用存储库（jcr节点，它是par节点的子节点）中的现有资源。

   * 显示的文本：“此组件通过其par节点提供。”

   如果选中此项，组件指南将使用sling动态包含子节点的resourceType（非现有资源）的组件。

   * 显示的文本：“此组件是动态包含的。”

   默认为未选中。

### 发布交互{#publish-interactions}

在发布实例上使用指南时，可以将组件和功能作为站点访客（未登录）以及登录时具有各种权限的成员进行体验。

>[!NOTE]
>
>请注意，如果SRP默认为[JSRP](jsrp.md)，则在发布实例上输入的UGC将仅在发布时可见，并且&#x200B;*不*&#x200B;将从创作实例上的[仲裁](moderate-ugc.md)控制台可见。

## 客户端库 {#client-side-libraries}

每个组件列出的客户端库(clientlibs)是将组件放置到页面上时需要引用的&#x200B;*必需*。 客户端库提供了管理和优化在浏览器中呈现组件时使用的Javascript和CSS下载的方法。

有关详细信息，请访问[Clientlibs for Communities Components](clientlibs.md)。

## 模拟 {#impersonation}

在作者实例中，一个用户通常以管理员或开发人员身份登录，为了体验以其他用户身份登录的组件，请使用&#x200B;**[!UICONTROL 模拟]**&#x200B;按钮左侧的文本框键入用户名或从下拉列表中进行选择，然后单击按钮。 单击“还原”以注销并结束模拟。

发布实例无需模拟。 只需使用“登录／注销”链接模拟各种用户，如[demo用户](tutorials.md#demo-users)。

## 自定义{#customization}

启用后，每个SCF组件都可通过临时修改组件的模板、CSS和数据来为可能的自定义创建原型。

### 启用自定义{#enabling-customization}

>[!NOTE]
>
>**此工具为只读**。对模板、CSS或数据所做的任何编辑都不会保存到存储库中。

要快速试验自定义，必须将`scg:showIde`属性添加到组件页的内容JCR节点并设置为true。

以注释组件为例，在作者实例或发布实例上，使用管理员权限登录：

1. 浏览至[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   例如，[http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 选择组件的`jcr:content`节点

   例如，`/content/community-components/en/comments/jcr:content`

1. 添加属性

   * **名称** `scg:showIde`
   * **类型** `String`
   * **值** `true`

1. 选择&#x200B;**[!UICONTROL 保存全部]**
1. 重新加载指南中的“注释”页

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 请注意，现在有3个用于模板、CSS和数据的选项卡。

![社区组件5](assets/community-component5.png)

![社区组件6](assets/community-component6.png)

### 模板选项卡{#templates-tab}

选择模板选项卡以查看与组件关联的模板。

模板编辑器允许编译本地编辑并将其应用于页面顶部的示例组件实例，而不会影响存储库中的组件。

在本地编辑时运行编译将突出显示所有错误，方法是在装订线中放置一个点并将文本标记为红色。

### CSS选项卡{#css-tab}

选择CSS选项卡以查看与组件关联的CSS。

如果组件是多个组件的组合，则某些CSS可能列在其中一个组件下。

CSS编辑器允许修改CSS并将其应用于页面顶部的示例组件实例。

可以选择一条规则，通过单击装订线中规则旁边，使用该规则突出显示DOM的各个部分。

### 数据选项卡{#data-tab}

选择“数据”选项卡以显示。social.json端点数据。 此数据是可编辑的，并应用于示例组件实例。

语法错误可在装订线中标记，也可在编辑器中突出显示。
