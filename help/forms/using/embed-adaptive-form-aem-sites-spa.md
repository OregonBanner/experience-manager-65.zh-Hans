---
title: 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信
seo-title: 在AEM站点页面中嵌入自适应表单或交互式通信
description: 在AEM站点页面中嵌入自适应表单或交互式通信。 用户无需离开“站点”页面即可填写和提交表单。
seo-description: 您可以在AEM站点页面中嵌入自适应表单或交互式通信。 用户无需离开“站点”页面即可填写和提交表单。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概述 {#overview}

AEM Forms允许表单开发人员将自适应表单和交互式通信无缝嵌入到AEM Sites单页应用程序(SPA)中。 嵌入式自适应表单和交互式通信功能完全可用，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中，并同时与自适应表单或交互式通信交互。

在AEM Sites单页应用程序中，您可以使用 [AEM Forms SPA容器组件添加自适应表单或交互式通信](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites SPA的AEM Forms组件，您可以将其添加到站点页面。

有关在非SPA AEM站点中嵌入自适应表单的信息，请参阅在AEM [站点中嵌入自适应表单或交互式通信](/help/forms/using/embed-adaptive-form-aem-sites.md)。

## 前提条件 {#prerequisites}

要使用AEM Forms SPA容器组件将自适应表单或交互式通信嵌入AEM站点SPA中，请确保您已安装：

* Java SE Development Kit 8或更高版本
* Apache Maven 3.3.1或更高版本
* AEM作者实例
* [创作实例上的AEM Forms 6.4.2加载项包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)

## 安装AEM Forms SPA容器组件 {#install-aem-forms-spa-container-component}

执行以下步骤安装AEM Forms SPA Container组件：

1. [克隆或下载SPA的AEM Forms组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. 安装AEM Forms组件，用于SPA。 README.md文件中提供了有关安装该组 [件的说明](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 。

   该组件包括一 [个范例React组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) ，该组件可用于将SPA容器组件与基于React的SPA项目集成。

1. [克隆或下载基于React的SPA项目](https://github.com/adobe/aem-sample-we-retail-journal)。
1. 使用 [README.md文件中的说明将SPA容器组件与基于React的SPA项目集成](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 。

   在安装AEM Forms SPA Container组件并将该组件与基于React的SPA项目集成之后，您可以在AEM Sites页面中嵌入自适应表单和交互式通信。

## 嵌入自适应表单或交互式通信 {#af-component}

要使用AEM Forms for SPA容器组件嵌入自适应表单或交互式通信，请执行以下操作：

1. 在编辑模式下打开AEM站点页面，您要在其中嵌入自适应表单或交互式通信。
1. 使用以 **下任意选项在页面上插入AEM For SPA** 组件：

   * 点按站点页面上的布局容器，点 **按+** 并选择 **AEM Form for SPA组件** 。

   * 从组件浏览器面板中，将 **AEM Form for SPA组件拖放到页面上** 。
   * 在资产浏览器中搜索自适应表单或交互式通信，然后将其拖放到站点页面。 它将表单嵌入到AEM Forms for SPA组件容器中。
   >[!NOTE]
   >
   >不支持在页面上渲染多个AEM Forms SPA Container组件。 您可以在一个页面上包含多个AEM Forms SPA Container，但一次只渲染一个组件。 确保页面上仅显示一个组件，以避免出现差异。

1. 点按站点页面中嵌入的AEM Forms SPA Container组件，然后点按操 ![作栏上的settings_icon](assets/settings_icon.png) 。 此时 **将打开编辑AEM Forms SPA容器** 。
1. 在“编 **辑AEM Forms容器** ”对话框中，指定以下内容：

   * **** 资产类型：选择要嵌入的资产类型。 选项包括自适 **应表单** 和交 **互式通信**

   * **资产路径**:浏览并选择要嵌入的自适应表单或交互式通信。 如果使用资产浏览器插入了自适应表单或交互式通信，则该字段将自动填充。
   * **渠道** （仅限交互式通信）:选择要嵌入的交互式渠道类型。 选项为 **Web渠道** 和 **打印渠道**。

   * **主题**:选择一个主题，它为自适应表单或交互式通信的组件定义样式。 样式包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。

1. 点 ![](assets/done_icon.png) 按以保存设置。 自适应表单或交互式通信现在嵌入到页面中。

## 发布嵌入式自适应表单和交互式通信 {#publish-embedded-adaptive-form-and-interactive-communication}

请考虑以下情况，以在AEM站点页面上发布嵌入式资产（自适应表单或交互式通信）:

* 如果您是第一次发布AEM站点页面，并且该页面包含嵌入的自适应表单或交互式通信，请发布站点页面和嵌入的资产。
* 如果您仅在已发布的站点页面中修改了嵌入的自适应表单或交互式通信，请发布原始资产，而更改将反映在已发布的站点页面中。 已发布的站点页面包含对资产的引用，并且不需要重新发布页面。
* 如果您修改了“站点”页面和嵌入的自适应表单或交互式通信，请重新发布“站点”页面和嵌入的资产。

## 修改嵌入式自适应表单和交互式通信 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM站点页面在AEM Forms容器中保留对自适应表单和交互式通信的引用。 因此，在原始自适应表单和交互式通信中配置的所有配置和属性（如主题、样式和提交操作）都保留在嵌入式自适应表单和交互式通信中。

要修改嵌入式自适应表单和交互式通信的任何配置或属性，请执行下列操作之一。

* 在自适应表单中打开原始表单，或在相应的编辑器中打开交互式通信，并修改它们。
* 在“站点”页面中以编辑模式点按自适应表单或交互式通信，然后在新 **窗口中点按编辑**。 原始表单在编辑模式下打开。

## 注意事项和最佳实践 {#considerations-and-best-practices}

在AEM站点页面中嵌入自适应表单时，请牢记以下几点：

* 原始表单中的页眉和页脚不包括在嵌入的表单中。
* 支持嵌入式表单的用户草稿和提交内容，并可在表单门户的“草稿”和“已提交表单”选项卡中看到这些内容。
* 在原始表单上配置的提交操作将保留在嵌入式表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入式表单中不起作用。 但是，您可以在“站点”页面上使用体验定位来根据用户配置文件显示不同的表单。
* 如果您为原始表单配置了Adobe Analytics，则嵌入式表单的分析数据会在Adobe Analytics中捕获。 但是，表单分析报告中不提供该功能。

