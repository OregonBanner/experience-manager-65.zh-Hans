---
title: 组件概述
seo-title: 组件
description: 组件是模块化单元，可实现在网站上展示内容的特定功能
seo-description: 组件是模块化单元，可实现在网站上展示内容的特定功能
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# 组件概述{#components-overview}

本页概述了Adobe Experience Manager(AEM)组件，如用于页面 [创作的组件](/help/sites-authoring/default-components-foundation.md)。

## 什么是组件？ {#what-exactly-is-a-component}

* 模块化单元，可实现在网站上展示您的内容的特定功能。
* 可重用。
* 在存储库的一个文件夹中开发为独立单元。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系统内的任意位置运行。 它们也可以限制在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用基于Granite UI组件的子元素构建的对话框
* 使用 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) （推荐）或JSP进行开发。
* 可以开发用于创建扩展默认功能的自定义组件。

由于组件是模块化的，您可以：

* 在本地实例上开发新组件。
* 将其部署到测试环境。
* 将其部署到实时创作环境中，供作者和／或管理员添加和配置内容。
* 将其部署到实时发布环境中，在该环境中，它们用于为网站的访客呈现内容。 某些组件（例如，Communities）也接受用户的输入。

每个AEM组件：

* 是资源类型。
* 是完全实现特定功能的脚本集合。
* 可以独立运 *行*，即在AEM或门户中运行。

## AEM中的现成组件 {#out-of-the-box-components-within-aem}

AEM comes with a variety of [out-of-the-box components](/help/sites-authoring/default-components.md) that provide comprehensive functionality including:

* 段落系统 ( `parsys`)
* 页面( `responsivegrid` 仅限触屏优化UI)
* 文本
* 图像，带有随附的文本
* 工具栏

提供的组件及其在示例We.Retail网 [站中的使用说明](/help/sites-developing/we-retail.md) ，如何实施和使用组件。 这些组件提供了所有源代码，并可以按原样使用，或作为修改的或扩展组件的起始点。

### 核心组件和基础组件 {#core-components-and-foundation-components}

有两组Adobe提供的AEM组件可用：

* [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [基础组件](/help/sites-authoring/default-components-foundation.md)

**核心组件** （随AEM 6.3一起推出）提供了灵活且功能丰富的创作功能。 We. [Retail参考站点说明了如何使用核心组件](/help/sites-developing/we-retail.md) ，并代表了组件开发的当前最佳做法。

**基础组件** （AEM中提供了许多版本），标准AEM安装中提供了现成功能。 尽管仍受支持，但大多数已弃用，不再进行增强，并且基于旧技术。

>[!NOTE]
>
>[核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) ，代表组件设计和开发的当前最佳做法，并用作参考实施。
>
>[AEM Medranceization Tools](modernization-tools.md) （AEM现代化工具）可以帮助迁移到核心组件。

### 查看可用组件 {#viewing-available-components}

有关AEM实例中所有可用组件的概述，请使用组 [件控制台](/help/sites-authoring/default-components-console.md)。

或者，您也可以使用CRXDE Lite获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite中]**，从工具栏中选择工具，然后选择 **[!UICONTROL Query]** , **[!UICONTROL Query]**, **[!UICONTROL Query将打开]** Query选项卡。

1. 在“查 **[!UICONTROL 询]** ”选项卡中，选 `XPath` 择“ **[!UICONTROL 类型”]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击 **[!UICONTROL 执行]** ，此时将列出组件。

## 其他资源 {#further-reading}

以下页面提供了有关开发这些组件和其他组件的更多详细信息：

* [AEM组件——基础知识](/help/sites-developing/components-basics.md)
* [开发AEM组件](/help/sites-developing/developing-components.md)
* [开发AEM组件——代码示例](/help/sites-developing/developing-components-samples.md)
* [配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md)
* [开发人员模式](/help/sites-developing/developer-mode.md)
* [测试UI](/help/sites-developing/hobbes.md)
* [内容片段的组件](/help/sites-developing/components-content-fragments.md)
* [以JSON格式获取页面信息](/help/sites-developing/pageinfo.md)
* [国际化组件](/help/sites-developing/i18n.md)
* [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [使用隐藏条件](/help/sites-developing/hide-conditions.md)
* 经典 UI

   * [AEM组件（经典UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和扩展构件（经典UI）](/help/sites-developing/widgets.md)
   * [使用xtypes（经典UI）](/help/sites-developing/xtypes.md)
   * [开发表单（经典UI）](/help/sites-developing/developing-forms.md)

