---
title: 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信
description: 在AEM Sites页面中嵌入自适应表单或交互式通信。 用户无需离开站点页面即可填写和提交表单。
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 4%

---

# 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

AEM Forms允许表单开发人员将自适应表单和交互式通信无缝嵌入到AEM Sites单页应用程序(SPA)中。 嵌入式自适应表单和交互式通信功能完善，用户无需离开页面即可填写并提交表单。 它有助于用户停留在网页上其他元素的上下文中，同时与自适应表单或交互式通信交互。

在AEM Sites单页应用程序中，您可以使用添加自适应表单或交互式通信 [AEM Forms SPA容器组件](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites SPA的AEM Forms组件，您可以将其添加到站点页面。

有关在非SPA AEM Sites中嵌入自适应表单的信息，请参阅 [在AEM Sites页面中嵌入自适应表单或交互式通信](/help/forms/using/embed-adaptive-form-aem-sites.md).

## 前提条件 {#prerequisites}

要使用AEM Forms SPA Container组件在AEM Sites SPA中嵌入自适应表单或交互式通信，请确保您已安装：

* Java SE Development Kit 8或更高版本
* Apache Maven 3.3.1或更高版本
* AEM创作实例
* [AEM Forms 6.4.2附加组件包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 在创作实例上

## 安装AEM Forms SPA容器组件 {#install-aem-forms-spa-container-component}

执行以下步骤安装AEM Forms SPA Container组件：

1. [克隆或下载适用于SPA的AEM Forms组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. 安装适用于SPA的AEM Forms组件。 有关安装组件的说明，请参见 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 文件。

   该组件包括 [示例React组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) ，可用于将SPA容器组件与基于React的SPA项目集成。

1. [克隆或下载基于React的SPA项目](https://github.com/adobe/aem-sample-we-retail-journal).
1. SPA SPA使用 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 文件。

   安装AEM Forms SPA Container组件并将该组件与基于React的SPA项目集成后，您可以在AEM Sites页面中嵌入自适应表单和交互式通信。

## 嵌入自适应表单或交互式通信 {#af-component}

要使用AEM Forms for SPA容器组件嵌入自适应表单或交互式通信，请执行以下操作：

1. 在编辑模式下打开AEM sites页面，您要在该页面中嵌入自适应表单或交互式通信。
1. 插入 **SPA的AEM表单** 组件时，使用以下任一选项：

   * 在站点页面上选择布局容器，然后选择 **+** 并选择 **SPA的AEM表单** 组件。

   * 在组件浏览器面板中，拖放 **SPA的AEM表单** 组件。
   * 在Assets浏览器中搜索自适应表单或交互式通信，并将其拖放到站点页面上。 它将表单嵌入到AEM Forms for SPA组件容器中。

   >[!NOTE]
   >
   >不支持在页面上呈现多个AEM Forms SPA Container组件。 您可以在一个页面上有多个AEM Forms SPA Container，但一次只能呈现一个组件。 确保页面上只显示一个组件，以避免出现差异。

1. 在站点页面中选择嵌入的AEM Forms SPA容器组件，然后选择 ![settings_icon](assets/settings_icon.png) 在操作栏上。 此 **编辑AEM Forms SPA容器** 对话框打开。
1. 在 **编辑AEM Forms容器** 对话框，请指定以下内容：

   * **资源类型：** 选择要嵌入的资源类型。 选项包括 **自适应表单** 和 **交互式通信**

   * **资产路径**：浏览并选择要嵌入的自适应表单或交互式通信。 如果使用Assets浏览器插入自适应表单或交互式通信，则会自动填充字段。
   * **渠道** （仅限交互式通信）：选择要嵌入的交互式渠道类型。 选项包括 **Web渠道** 和 **打印渠道**.

   * **主题**：选择用于定义自适应表单或交互式通信组件样式的主题。 样式设置包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。

1. 选择 ![完成图标](assets/done_icon.png) 以保存设置。 自适应表单或交互式通信现在嵌入到页面中。

## 发布嵌入式自适应表单和交互式通信 {#publish-embedded-adaptive-form-and-interactive-communication}

考虑以下在AEM Sites页面上发布嵌入资产（自适应表单或交互式通信）的情景：

* 如果您是首次发布AEM Sites页面，并且该页面包含嵌入的自适应表单或交互式通信，请发布Sites页面和嵌入的资源。
* 如果在已发布的Sites页面中仅修改了嵌入的自适应表单或交互式通信，请发布原始资产，所做的更改会反映在已发布的Sites页面中。 已发布的站点页面包含对资产的引用，因此无需重新发布页面。
* 如果修改了Sites页面和嵌入的自适应表单或交互式通信，请重新发布Sites页面和嵌入的资产。

## 修改嵌入式自适应表单和交互式通信 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM sites页在AEM Forms容器中维护对自适应表单和交互式通信的引用。 因此，在原始自适应表单和交互式通信中配置的所有配置和属性（如主题、样式和提交操作）均保留在嵌入式自适应表单和交互式通信中。

要修改嵌入式自适应表单和交互式通信的任何配置或属性，请执行以下操作之一。

* 在相应编辑器中打开自适应表单或交互式通信中的原始表单，然后对其进行修改。
* 在编辑模式下，从站点页面中选择自适应表单或交互式通信，然后选择 **在新窗口中编辑**. 原始表单将在编辑模式下打开。

## 注意事项和最佳实践 {#considerations-and-best-practices}

在AEM Sites页面中嵌入自适应表单时，请牢记以下几点：

* 原始表单中的页眉和页脚未包含在嵌入表单中。
* 支持用户草稿和提交嵌入式表单，并且这些草稿和已提交的Forms选项卡位于Forms Portal上。
* 在原始表单上配置的提交操作将保留在嵌入表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入表单中不起作用。 但是，您可以使用站点页面上的体验定位，根据用户配置文件显示不同的表单。
* 如果您已为原始表单配置了Adobe Analytics，则会在Adobe Analytics中捕获嵌入表单的分析数据。 但是，它在Forms Analytics报表中不可用。
