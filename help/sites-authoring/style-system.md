---
title: 样式系统
seo-title: 样式系统
description: 样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。
seo-description: 样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 样式系统{#style-system}

样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。

使用样式系统，您无需为每种样式开发自定义组件，也无需自定义组件对话框来启用此类样式功能。样式系统允许使用更多可重用组件，可以快速轻松地调整这些组件以满足内容作者的需求，而无需进行任何 AEM 后端开发。

## 用例 {#use-case}

模板作者不仅需要能够为内容作者配置组件的使用方式，还需要能够配置组件的多种替代可视化变量。

同样，内容作者不仅需要能够构建和布置他们的内容，还需要能够选择内容的可视呈现方式。

样式系统针对模板作者和内容作者的要求提供了统一的解决方案：

* 模板作者可以在组件的内容策略中定义样式类。
* 之后，内容作者在页面上编辑组件时，可以从下拉列表中选择这些类，以便应用相应的样式。

样式类随后会插入到组件的装饰包装器元素中，这样组件开发人员除了提供 CSS 规则之外，便无需关注样式的处理。

## 概述 {#overview}

通常，可通过以下形式来使用样式系统。

1. Web 设计人员创建组件的不同可视化变量。

1. 向 HTML 开发人员提供组件的 HTML 输出以及要实施的所需可视化变量。

1. HTML开发人员定义与每个可视变量相对应的CSS类，这些类将插入到封装组件的元素上。

1. HTML开发人员为每个可视变量实施相应的CSS代码（和可选的JS代码），以便它们看起来如所定义。

1. AEM 开发人员将提供的 CSS（和可选 JS）放置在[客户端库](/help/sites-developing/clientlibs.md)中并对其进行部署。

1. AEM开发人员或模板作者配置页面模板并编辑每个已设置样式的组件的策略，添加定义的CSS类，为每个样式提供用户友好名称，并指示可组合的样式。

1. 之后，AEM 页面作者可以在页面编辑器中通过组件工具栏的样式菜单选择设计的样式。

请注意，实际上只有最后三个步骤在 AEM 中执行。这意味着，必需的 CSS 和 Javascript 的所有开发工作都可以在没有 AEM 的情况下完成。

实际上，要实施这些样式，只需在 AEM 上部署并在所需模板的组件中进行选择即可。

下图说明了样式系统的架构。

![aem-style-system](assets/aem-style-system.png)

## 用法 {#use}

要演示该功能，需要为组件创建样式。您可以使用 [We.Retail](/help/sites-developing/we-retail.md) 的核心组件[列表组件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)的实施作为基础，安装包含样式的随附包，以便浏览该功能的运作方式。

下载样 [式系统演示包](assets/package_-_style_systemdemo.zip)

>[!NOTE]
>
>演示包旨在显示作者可以如何使用样式系统，而不是作为如何更好地实施该系统的参考。
>
>只有当 We.Retail 提供了内置示例和最佳实践实施时，才需要该包。

下面的[作为内容作者](/help/sites-authoring/style-system.md#as-a-content-author)和[作为模板作者](/help/sites-authoring/style-system.md#as-a-template-author)部分介绍了如何基于 We.Retail 使用样式系统演示包来测试样式系统的功能。

如果您希望为自己的组件使用样式系统，请执行以下操作：

1. 按照[概述](/help/sites-authoring/style-system.md#overview)部分中的所述，将 CSS 作为客户端库进行安装。
1. 按照[作为模板作者](/help/sites-authoring/style-system.md#as-a-template-author)部分中的所述，配置您要向内容作者提供的 CSS 类。
1. 然后，内容作者可以按照[作为内容作者](/help/sites-authoring/style-system.md#as-a-content-author)部分中的所述使用样式。

### 作为内容作者 {#as-a-content-author}

1. After installing the style system demo package, navigate to We.Retail&#39;s English language master home page at `http://localhost:4502/sites.html/content/we-retail/language-masters/en` and edit the page.
1. 在 parsys 的底部或顶部选择&#x200B;**列表**&#x200B;组件。Do not confuse it with the **Articles List** component.

   ![screen_shot_2017-11-15at162032](assets/screen_shot_2017-11-15at162032.png)

1. 点按或单击&#x200B;**列表**&#x200B;组件工具栏上的&#x200B;**样式**&#x200B;按钮以打开样式菜单，然后更改该组件的外观。

   ![screen_shot_2017-11-15at162358](assets/screen_shot_2017-11-15at162358.png)

   >[!NOTE]
   >
   >In this example, the **Layout** styles (**Block** and **Grid**) are mutually exclusive, while the **Display** options (**Image** or **Date**) can be combined. 这可以[在模板中由模板作者进行配置](/help/sites-authoring/style-system.md#as-a-template-author)。

### 作为模板作者 {#as-a-template-author}

1. While editing We.Retail&#39;s English language master home page at `http://localhost:4502/sites.html/content/we-retail/language-masters/en`, edit the template of the page via **Page Information -> Edit Template**.

   ![screen_shot_2017-11-15at162922](assets/screen_shot_2017-11-15at162922.png)

1. 点按或单击&#x200B;**列表**&#x200B;组件的&#x200B;**策略**&#x200B;按钮，以编辑该组件的策略。请勿将其与&#x200B;**文章列表**&#x200B;组件混淆。

   ![screen_shot_2017-11-15at163133](assets/screen_shot_2017-11-15at163133.png)

1. 在属性的“样式”选项卡中，您可以看到样式的配置方式。

   ![screen_shot_2017-12-15at101404](assets/screen_shot_2017-12-15at101404.png)

   * **组名称：**&#x200B;样式可以在样式菜单中分组到一起，内容作者在配置组件样式时将看到该样式菜单。
   * **样式可以合并：**&#x200B;允许一次选择该组中的多个样式。
   * **样式名称：**&#x200B;在配置组件样式时将向内容作者显示的样式描述。
   * **CSS 类：**&#x200B;与样式关联的 CSS 类的实际名称。
   使用拖动手柄可调整组以及组中样式的顺序。使用添加或删除图标可添加或者删除组或组中的样式。

>[!CAUTION]
>
>The CSS classes (as well as any necessary Javascript) configured as style properties of a component&#39;s policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.

## 设置 {#setup}

>[!NOTE]
>
>已完全启用核心组件版本 2 来充分利用样式系统，无需其他配置。
>
>请按照以下步骤来为您自己的自定义组件启用样式系统，或者扩展核心组件版本 1 来使用该功能。

为了使组件能够与 AEM 的样式系统结合使用并在其设计对话框中显示样式选项卡，组件开发人员必须在产品中通过对组件进行以下设置来包含该选项卡：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

配置组件后，由页面作者配置的样式将由 AEM 自动插入到装饰元素，AEM 会自动在每个可编辑的组件周围包裹该装饰元素。组件本身不需要执行任何操作即可实现这一点。

### 具有元素名称的样式 {#styles-with-element-names}

开发人员还可以使用 `cq:styleElements` 字符串数组属性为组件上的样式配置允许的元素名称列表。然后，在设计对话框内策略的“样式”选项卡中，模板作者也可以为每个样式选择一个要设置的元素名称。这将设置包装器元素的元素名称。

This property is set on the `cq:Component` node. 例如：

* `/apps/weretail/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>避免为可以合并的样式定义元素名称。当定义多个元素名称时，其优先级顺序为：
>
>1. HTL优先于所有内容： `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然后，在多个活动样式中，会采用组件策略中配置的样式列表中的第一个样式。
>1. Finally, the component&#39;s `cq:htmlTag`/ `cq:tagName` will be considered as a fallback value.
>



这种定义样式名称的功能对于极其通用的组件（如布局容器或内容片段组件）非常有用，可为它们提供更多含义。

For instance it allows a Layout Container to be given semantics like `<main>`, `<aside>`, `<nav>`, etc.
