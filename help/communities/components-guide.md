---
title: 社区组件指南
seo-title: 社区组件指南
description: 一种交互式开发工具，用于开始使用社交组件框架(SCF)
seo-description: 一种交互式开发工具，用于开始使用社交组件框架(SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---

# 社区组件指南  {#community-components-guide}

社区组件指南是[社交组件框架(SCF)](scf.md)的交互式开发工具。 它提供了可用AEM Communities组件或由多个组件构建的更复杂功能的列表。

除了每个组件的基本信息外，本指南还允许对SCF组件/功能的工作方式以及配置或自定义这些组件/功能的方式进行实验。

有关与每个组件相关的开发要点的信息，请参阅[功能和组件要点](essentials.md)。

## 入门 {#getting-started}

本指南旨在用于创作(localhost:4502)和发布(localhost:4503)实例的开发安装。

通过浏览到

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

与社区组件的交互将因以下各项而异：

* 服务器（创作或发布）。
* 网站访客是否已登录。
* 如果已登录，则分配给成员的权限。
* 是否使用默认SRP [JSRP](jsrp.md)。

在创作时，要进入编辑模式，请在服务器名称后面插入`editor.html`或`cf#`作为第一个路径段：

* 标准 UI:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 经典 UI：

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>在编辑模式下进行创作时，页面上的链接不处于活动状态。
>
>要导航到组件页面，请首先选择预览模式以激活链接。
>
>将组件页面显示在浏览器中，返回到编辑模式以打开组件的编辑对话框。
>
>有关一般创作信息，请查看[页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请查看有关[基本操作](../../help/sites-authoring/basic-handling.md)的文档。

### 主页 {#home-page}

本指南提供了SCF组件列表，这些组件可用于在页面左侧预览和制作原型。

在编辑模式下在创作实例中查看的组件指南：

![community-component1](assets/community-component1.png)

## 组件页{#component-pages}

从页面左侧的列表中选择一个组件。

![community-component-pages](assets/community-component2.png)

指南的主体显示：

1. 标题：所选组件的名称
1. [客户端库](#client-side-libraries):一个或多个必需类别的列表
1. [可包含](scf.md#add-or-include-a-communities-component):如果组件可以动态包含，则可以在创作编辑模式下切换状态：

   * 如果添加，则显示的文本为：“此组件通过其par节点包含。”
   * 如果包含，则显示的文本为：“此组件是动态包含的。”
   * 如果不包含，则不会显示任何文本

1. 示例组件或功能：组件或特征的活动实例。 如果某个组件发生了更改，则可能会对选项卡部分中提供的模板、CSS和数据进行更改。

>[!NOTE]
>
>从左侧进行选择后，当浏览器窗口过窄时，组件将显示在组件列表的下方（而不是旁边）。

### 创作交互{#author-interactions}

在创作实例中使用指南时，可以通过打开组件对话框来体验配置组件。 有关开发人员的信息，请参阅文档的[组件和功能要点](essentials.md)部分，而对话框设置则请参阅[社区组件](author-communities.md)部分，以供作者参考。

对于“社区组件”指南，某些组件对话框设置将覆盖[Includable](scf.md#add-or-include-a-communities-component)切换状态。 要在使用现有资源或动态包含的资源之间进行切换，请在编辑模式下选择组件和可包含文本，然后双击以打开编辑对话框：

![community-component3](assets/community-component3.png)

在&#x200B;**Templates**&#x200B;选项卡下：

![社区组件4](assets/community-component4.png)

* **通过 sling:include 包含子组件**

   如果未选中此选项，组件指南将使用存储库中的现有资源（作为par节点子项的jcr节点）。

   * 显示的文本为：“此组件通过其par节点包含。”

   如果选中此项，组件指南将使用sling动态包含子节点resourceType（非现有资源）的组件。

   * 显示的文本为：“此组件是动态包含的。”

   默认为未选中。

### 发布交互{#publish-interactions}

在发布实例上使用指南时，可以将组件和功能作为站点访客（未登录）以及登录时具有各种权限的成员进行体验。

>[!NOTE]
>
>请注意，如果SRP默认为[JSRP](jsrp.md)，则在发布实例上输入的UGC将仅在发布时可见，并且&#x200B;*不*&#x200B;将从创作实例上的[审核](moderate-ugc.md)控制台可见。

## 客户端库 {#client-side-libraries}

每个组件的客户端库(clientlibs)是在将组件放置到页面上时需要引用的那些&#x200B;*必需的*&#x200B;库。 clientlibs提供了一种管理和优化用于在浏览器中呈现组件的Javascript和CSS下载的方法。

有关更多信息，请访问[Clientlibs for Communities Components](clientlibs.md)。

## 模拟 {#impersonation}

在作者实例中，如果一个用户通常以管理员或开发人员身份登录，要体验以其他用户身份登录的组件，请使用&#x200B;**[!UICONTROL 模拟]**&#x200B;按钮左侧的文本框键入用户名或从下拉列表中选择，然后单击按钮。 单击还原以注销并结束模拟。

发布实例不需要模拟。 只需使用登录/注销链接来模拟各种用户，例如[演示用户](tutorials.md#demo-users)。

## 自定义 {#customization}

启用后，每个SCF组件都可通过临时修改组件的模板、CSS和数据来为可能的自定义设置制作原型。

### 启用自定义{#enabling-customization}

>[!NOTE]
>
>**此工具为只读**。对模板、CSS或数据所做的任何编辑都不会保存到存储库。

要快速体验自定义设置，必须将`scg:showIde`属性添加到组件页面的内容JCR节点并设置为true。

以注释组件为例，在创作实例或发布实例上，使用管理员权限登录：

1. 浏览到[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   例如， [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 选择组件的`jcr:content`节点

   例如，`/content/community-components/en/comments/jcr:content`

1. 添加资产

   * **名称** `scg:showIde`
   * **类型** `String`
   * **值** `true`

1. 选择&#x200B;**[!UICONTROL Save All]**
1. 在指南中重新加载注释页面

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 请注意，现在有3个用于“模板”、“CSS”和“数据”的选项卡。

![社区组件5](assets/community-component5.png)

![社区组件6](assets/community-component6.png)

### “模板”选项卡{#templates-tab}

选择模板选项卡可查看与组件关联的模板。

模板编辑器允许编译本地编辑内容并将其应用于页面顶部的示例组件实例，而不会影响存储库中的组件。

在本地编辑中运行编译时，将突出显示所有错误，方法是在边栏中放置一个圆点，并将文本标记为红色。

### CSS选项卡{#css-tab}

选择“CSS”选项卡可查看与组件关联的CSS。

如果组件是多个组件的组合，则某些CSS可能会列在其他组件之一下。

CSS编辑器允许修改CSS并将其应用于页面顶部的示例组件实例。

可通过单击装订线中规则旁边的，选择规则以使用该规则突出显示DOM的各个部分。

### 数据选项卡{#data-tab}

选择“数据”选项卡以显示.social.json端点数据。 此数据是可编辑的，并且会应用于示例组件实例。

语法错误可能会标记在边栏中，也会在编辑器中突出显示。
