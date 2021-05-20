---
title: HTML5表单简介
seo-title: HTML5表单简介
description: HTML5表单是Adobe Experience Manager 6.0(AEM 6.0)软件中的一项新功能，可渲染HTML5格式的XFA表单模板。
seo-description: HTML5表单是Adobe Experience Manager 6.0(AEM 6.0)软件中的一项新功能，可渲染HTML5格式的XFA表单模板。
uuid: 63a2f000-c4c5-40e8-ab3f-c7c44c79ec09
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 672ee050-63d1-46ed-bef2-f55800208d78
docset: aem65
feature: 移动设备表单
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# HTML5表单简介{#introduction-to-html-forms}

HTML5表单是Adobe Experience Manager 6.0(AEM 6.0)软件中的一项新功能，可渲染HTML5格式的XFA表单模板。 此功能允许在不支持基于XFA的PDF的移动设备和桌面浏览器上渲染表单。 HTML5表单不仅支持XFA表单模板的现有功能，还为移动设备添加了新功能，如涂写签名。

HTML5表单基于标准HTML5结构生成文档。 您可以在支持HTML5的所有现代浏览器中查看HTML5表单。 它不需要为浏览器安装任何其他浏览器插件。 有关支持的浏览器的更多信息，请参阅[支持的客户端平台](https://adobe.com/go/learn_aemforms_supportedplatforms_63)。

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5表单{#key-capabilities-of-html-forms-br}的关键功能

* 在所有兼容的浏览器上都支持HTML5格式的现有XFA表单。
* 利用标准XFA表单设计功能，为移动设备定位表单。
* 使用HTML5格式的动态XFA功能。
* 使用高度精确的SVG文本布局(SVG 1.1)来匹配PDF文本布局。
* 提供对JavaScript和FormCalc的支持。
* 根据数据驱动事件或用户输入将片段动态组合为交互式表单。
* 支持自定义CSS以根据企业标准匹配表单外观。
* 允许自定义小组件提供丰富的数据捕获体验。
* 支持与Web应用程序集成。

### 多渠道发布{#multichannel-publishing}

表单开发人员可以使用XFA模板以PDF和HTML5格式渲染表单。 如果您拥有大量XFA表单，且需要进行少量更改才能适应HTML5表单设计实践，则此功能非常有用。 您可以将现有XFA表单渲染为HTML5，以定位尚不支持基于XFA的PDF的各种设备。

## 管理HTML5表单{#manage-html-forms}

AEM还提供了统一视图，以便使用AEM Forms UI列出和管理所有表单模板。 您可以激活、停用、发布和预览表单。 有关更多信息，请参阅[管理表单简介](../../forms/using/introduction-managing-forms.md)。

### Forms自定义{#forms-customization}

HTML5表单使用标准HTML5结构呈现表单模板。 这样，使用Web技术（主要是CSS和JavaScript），可以轻松地自定义和扩展HTML5格式的表单。 您可以轻松自定义现有小组件的外观，创建您自己的自定义小组件，或在表单中使用自定义样式。 有关创建自定义小组件和自定义现有小组件的更多信息，请参阅[使用HTML5表单插入自定义小组件](../../forms/using/custom-widgets.md)。
