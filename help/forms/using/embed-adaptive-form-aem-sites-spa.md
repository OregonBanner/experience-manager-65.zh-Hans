---
title: 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信
seo-title: 在AEM Sites页面中嵌入自适应表单或交互式通信
description: 在AEM Sites页面中嵌入自适应表单或交互式通信。 用户无需离开站点页面即可填写和提交表单。
seo-description: 您可以在AEM Sites页面中嵌入自适应表单或交互式通信。 用户无需离开站点页面即可填写和提交表单。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: 自适应表单
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概述 {#overview}

AEM Forms允许表单开发人员将自适应表单和交互式通信无缝嵌入AEM Sites单页应用程序(SPA)中。 嵌入式自适应表单和交互式通信功能完全，用户无需离开页面即可填写和提交表单。 它有助于用户停留在网页上其他元素的上下文中，并同时与自适应表单或交互式通信进行交互。

在AEM Sites单页应用程序中，您可以使用[AEM Forms SPA容器组件](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[添加自适应表单或交互式通信。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是适用于AEM Sites SPA的AEM Forms组件，您可以将其添加到站点页面。

有关在非SPA AEM Sites中嵌入自适应表单的信息，请参阅[在AEM Sites页面中嵌入自适应表单或交互式通信](/help/forms/using/embed-adaptive-form-aem-sites.md)。

## 前提条件 {#prerequisites}

要使用AEM Forms SPA容器组件在AEM站点SPA中嵌入自适应表单或交互式通信，请确保已安装：

* Java SE Development Kit 8或更高版本
* Apache Maven 3.3.1或更高版本
* AEM创作实例
* [AEM Forms 6.4.2附加组件包创](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 作实例

## 安装AEM Forms SPA容器组件{#install-aem-forms-spa-container-component}

执行以下步骤安装AEM Forms SPA容器组件：

1. [克隆或下载适用于SPA的AEM Forms组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. 安装适用于SPA的AEM Forms组件。 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component)文件中提供了安装组件的说明。

   该组件包含[示例React组件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)，可用于将SPA容器组件与基于React的SPA项目集成。

1. [克隆或下载基于React的SPA项目](https://github.com/adobe/aem-sample-we-retail-journal)。
1. 使用[README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor)文件中提供的说明，将SPA容器组件与基于React的SPA项目集成。

   安装AEM Forms SPA容器组件并将该组件与基于React的SPA项目集成后，您可以在AEM Sites页面中嵌入自适应表单和交互式通信。

## 嵌入自适应表单或交互式通信{#af-component}

要使用AEM Forms for SPA容器组件嵌入自适应表单或交互式通信，请执行以下操作：

1. 在编辑模式下打开AEM站点页面，您要在其中嵌入自适应表单或交互式通信。
1. 使用以下任意选项在页面上插入&#x200B;**AEM For SPA**&#x200B;组件：

   * 点按“站点”页面上的布局容器，点按&#x200B;**+**，然后选择&#x200B;**AEM For SPA**&#x200B;组件。

   * 从组件浏览器面板中，将&#x200B;**AEM For SPA**&#x200B;组件拖放到页面上。
   * 在资产浏览器中搜索自适应表单或交互式通信，并将其拖放到站点页面。 它将表单嵌入到AEM Forms for SPA组件容器中。

   >[!NOTE]
   >
   >不支持在页面上渲染多个AEM Forms SPA容器组件。 您可以在一个页面上包含多个AEM Forms SPA容器，但一次只渲染一个组件。 确保页面上只显示一个组件，以避免出现差异。

1. 点按站点页面中嵌入的AEM Forms SPA容器组件，然后点按操作栏上的![settings_icon](assets/settings_icon.png)。 将打开&#x200B;**编辑AEM Forms SPA容器**&#x200B;对话框。
1. 在&#x200B;**编辑AEM Forms容器**&#x200B;对话框中，指定以下内容：

   * **资产类型：** 选择要嵌入的资产类型。选项包括&#x200B;**自适应表单**&#x200B;和&#x200B;**交互式通信**

   * **资产路径**:浏览并选择要嵌入的自适应表单或交互式通信。如果使用资产浏览器插入自适应表单或交互式通信，则会自动填充该字段。
   * **渠道** （仅限交互式通信）：选择要嵌入的交互式渠道类型。选项包括&#x200B;**Web渠道**&#x200B;和&#x200B;**打印渠道**。

   * **主题**:选择一个主题，该主题定义自适应表单或交互式通信组件的样式。样式包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。

1. 点按![done_icon](assets/done_icon.png)以保存设置。 自适应表单或交互式通信现在嵌入到页面中。

## 发布嵌入式自适应表单和交互式通信{#publish-embedded-adaptive-form-and-interactive-communication}

请考虑以下方案，以在AEM Sites页面上发布嵌入的资产（自适应表单或交互式通信）：

* 如果您是首次发布AEM Sites页面，并且该页面包含嵌入式自适应表单或交互式通信，请发布站点页面和嵌入的资产。
* 如果您在已发布的站点页面中仅修改了嵌入的自适应表单或交互式通信，则应发布原始资产，并且所做的更改会反映在已发布的站点页面中。 发布的站点页面包含对资产的引用，无需重新发布页面。
* 如果您修改了站点页面和嵌入的自适应表单或交互式通信，请重新发布站点页面和嵌入的资产。

## 修改嵌入式自适应表单和交互式通信{#modify-embedded-adaptive-form-and-interactive-communication}

AEM站点页面在AEM Forms容器中维护对自适应表单和交互式通信的引用。 因此，在原始自适应表单和交互式通信中配置的所有配置和属性（如主题、样式和提交操作）都将保留在嵌入的自适应表单和交互式通信中。

要修改嵌入式自适应表单和交互式通信的任何配置或属性，请执行以下操作之一。

* 在自适应表单中打开原始表单，或在相应编辑器中使用交互式通信打开并修改它们。
* 在编辑模式下，从站点页面中点按自适应表单或交互式通信，然后点按&#x200B;**在新窗口中编辑**。 在编辑模式下，将打开原始表单。

## 注意事项和最佳实践{#considerations-and-best-practices}

在AEM站点页面中嵌入自适应表单时，请牢记以下几点：

* 原始表单中的页眉和页脚未包含在嵌入的表单中。
* 支持用户草稿和提交嵌入的表单，这些草稿和提交内容显示在表单门户的“草稿”和“已提交”Forms选项卡中。
* 在原始表单上配置的提交操作将保留在嵌入表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入的表单中不起作用。 但是，您可以使用“站点”页面上的体验定位来根据用户配置文件显示不同的表单。
* 如果您为原始表单配置了Adobe Analytics，则会在Adobe Analytics中捕获嵌入表单的分析数据。 但是，它在表单分析报表中不可用。
