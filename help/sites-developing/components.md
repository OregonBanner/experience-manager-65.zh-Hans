---
title: 组件 概述
seo-title: 组件
description: 组件是模块化单元，可以实现在网站上显示内容的特定功能
seo-description: 组件是模块化单元，可以实现在网站上显示内容的特定功能
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 9%

---

# 组件概述{#components-overview}

本页概述了Adobe Experience Manager(AEM)组件，例如用于页面创作的[组件](/help/sites-authoring/default-components-foundation.md)。

## 什么是组件？{#what-exactly-is-a-component}

* 模块化单元，可实现在网站上呈现内容的特定功能。
* 可重复使用。
* 开发为存储库一个文件夹内的自含单元。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系统内的任何位置运行。 这些组件也可限制在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用基于Granite UI组件使用子元素构建的对话框
* 使用[HTL](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)（推荐）或JSP进行开发。
* 可以开发以创建可扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将其部署到测试环境。
* 将其部署到实时创作环境，在该环境中，作者和/或管理员可以添加和配置内容。
* 将其部署到实时发布环境，在该环境中，访客可使用这些环境向网站的访客呈现内容。 某些组件（例如，社区组件）也接受用户的输入。

每个AEM组件：

* 是资源类型。
* 是完全实现特定功能的脚本集合。
* 可以在&#x200B;*isolation*&#x200B;中运行，即在AEM或门户中运行。

## AEM {#out-of-the-box-components-within-aem}内的现成组件

AEM附带多种[现成组件](/help/sites-authoring/default-components.md)，这些组件提供了以下综合功能：

* 段落系统 ( `parsys`)
* 页面（`responsivegrid` — 仅限触屏优化UI）
* 文本
* 图像，并附加文本
* 工具栏

[示例We.Retail网站](/help/sites-developing/we-retail.md)中提供的组件及其用法说明了如何实施和使用组件。 这些组件提供了所有源代码，可以按原样使用，也可以用作修改或扩展组件的起点。

### 核心组件和基础组件{#core-components-and-foundation-components}

提供了两组Adobe提供的AEM组件：

* [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)
* [基础组件](/help/sites-authoring/default-components-foundation.md)

**核心** 组件已在AEM 6.3中引入，并提供了灵活且功能丰富的创作功能。[We.Retail参考站点](/help/sites-developing/we-retail.md)说明了核心组件的使用方式，并说明了组件开发的当前最佳实践。

**基础** 组件已在AEM中提供了许多版本，并且在标准AEM安装中现成可用。尽管仍受支持，但大多数已弃用，不再进行增强，并且基于旧版技术。

>[!NOTE]
>
>[核心](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 组件代表了组件设计和开发的当前最佳实践，可用作参考实施。
>
>[AEM现代化工](modernization-tools.md) 具扫描可帮助迁移到核心组件。

### 查看可用组件{#viewing-available-components}

有关AEM实例中所有可用组件的概述，请使用[组件控制台](/help/sites-authoring/default-components-console.md)。

或者，您还可以使用CRXDE Lite获取存储库中所有可用组件的列表。

1. 在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，以打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;选项卡中，选择`XPath`作为&#x200B;**[!UICONTROL Type]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**&#x200B;并列出组件。

## 其他资源{#further-reading}

以下页面提供了有关开发这些组件和其他组件的更多详细信息：

* [AEM组件 — 基础知识](/help/sites-developing/components-basics.md)
* [开发AEM组件](/help/sites-developing/developing-components.md)
* [开发AEM组件 — 代码示例](/help/sites-developing/developing-components-samples.md)
* [配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md)
* [开发人员模式](/help/sites-developing/developer-mode.md)
* [测试您的UI](/help/sites-developing/hobbes.md)
* [内容片段的组件](/help/sites-developing/components-content-fragments.md)
* [以JSON格式获取页面信息](/help/sites-developing/pageinfo.md)
* [组件国际化](/help/sites-developing/i18n.md)
* [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [使用隐藏条件](/help/sites-developing/hide-conditions.md)
* 经典 UI

   * [AEM组件（经典UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和扩展小组件（经典UI）](/help/sites-developing/widgets.md)
   * [使用xtype（经典UI）](/help/sites-developing/xtypes.md)
   * [开发Forms（经典UI）](/help/sites-developing/developing-forms.md)
