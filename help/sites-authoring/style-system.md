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
source-git-commit: 0985ba24f7430381fccc40faf3a316d3abd85a30
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 69%

---


# 样式系统{#style-system}

样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以是组件的替代可视变体，使组件更灵活。

使用样式系统，您无需为每种样式开发自定义组件，也无需自定义组件对话框来启用此类样式功能。样式系统允许使用更多可重用组件，可以快速轻松地调整这些组件以满足内容作者的需求，而无需进行任何 AEM 后端开发。

## 用例 {#use-case}

模板作者不仅需要能够为内容作者配置组件的使用方式，还需要能够配置组件的多种替代可视化变量。

同样，内容作者不仅需要能够构建和布置他们的内容，还需要能够选择内容的可视呈现方式。

样式系统为模板作者和内容作者的要求提供了统一的解决方案：

* 模板作者可以在组件的内容策略中定义样式类。
* 之后，内容作者在页面上编辑组件时，可以从下拉列表中选择这些类，以便应用相应的样式。

样式类随后会插入到组件的装饰包装器元素中，这样组件开发人员除了提供 CSS 规则之外，便无需关注样式的处理。

## 概述 {#overview}

使用样式系统通常采用以下形式。

1. Web 设计人员创建组件的不同可视化变量。

1. 向 HTML 开发人员提供组件的 HTML 输出以及要实施的所需可视化变量。

1. HTML 开发人员定义与每个可视化变量对应的 CSS 类，该类将插入到组件的包装元素中。

1. HTML 开发人员为每个可视化变量实施相应的 CSS 代码（和可选 JS 代码），以使它们按照定义的方式显示。

1. AEM 开发人员将提供的 CSS（和可选 JS）放置在[客户端库](/help/sites-developing/clientlibs.md)中并对其进行部署。

1. AEM 开发人员或模板作者配置页面模板并编辑每个已设置样式的组件的策略，从而添加定义的 CSS 类、为每种样式提供用户友好名称，并指示可组合的样式。

1. 之后，AEM 页面作者可以在页面编辑器中通过组件工具栏的样式菜单选择设计的样式。

请注意，实际上只有最后三个步骤在 AEM 中执行。这意味着，必需的 CSS 和 Javascript 的所有开发工作都可以在没有 AEM 的情况下完成。

实际上，要实施这些样式，只需在 AEM 上部署并在所需模板的组件中进行选择即可。

下图说明了样式系统的架构。

![aem-style-system](assets/aem-style-system.png)

## 用法 {#use}

为了演示该功能，我们 [将以](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)WKND对核心组件的 [标题组件](https://www.adobe.com/go/aem_cmp_title_v2) 的实现为例。

The following sections [As a Content Author](#as-a-content-author) and [As a Template Author](#as-a-template-author) describe how to test the functionality of the Style System using the Style System of WKND.

如果您希望将样式系统用于您自己的组件，请执行以下操作：

1. 按照[概述](#overview)部分中的所述，将 CSS 作为客户端库进行安装。
1. 按照[作为模板作者](#as-a-template-author)部分中的所述，配置您要向内容作者提供的 CSS 类。
1. 然后，内容作者可以按照[作为内容作者](#as-a-content-author)部分中的所述使用样式。

### 作为内容作者 {#as-a-content-author}

1. 安装WKND项目后，在上导航至WKND的英语母版主页并 `http://<host>:<port>/sites.html/content/wknd/language-masters/en` 编辑页面。
1. 在页面的 **下方** ，选择一个标题组件

   ![作者的样式系统](assets/style-system-author.png)

1. 点按或单击&#x200B;**列表**&#x200B;组件工具栏上的&#x200B;**样式**&#x200B;按钮以打开样式菜单，然后更改该组件的外观。

   ![选择样式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此示例中，Colors **样式** (Black **、Gray** Styles **和GrayStyle**********************)是专用的，而Adobe StyleOptions(、RightJight、、和()可以合并为白色。 这可以[在模板中由模板作者进行配置](#as-a-template-author)。

### 作为模板作者 {#as-a-template-author}

1. While editing WKND&#39;s English language master home page at `http://<host>:<port>/sites.html/content/wknd/language-masters/en`, edit the template of the page via **Page Information -> Edit Template**.

   ![编辑模板](assets/style-system-edit-template.png)

1. Edit the policy of the **Title** component by tapping or clicking the **Policy** button of the component.

   ![编辑策略](assets/style-system-edit-policy.png)

1. 在属性的“样式”选项卡中，您可以看到样式的配置方式。

   ![编辑属性](assets/style-system-properties.png)

   * **组名称：**&#x200B;样式可以在样式菜单中分组到一起，内容作者在配置组件样式时将看到该样式菜单。
   * **样式可以合并：**&#x200B;允许一次选择该组中的多个样式。
   * **样式名称：**&#x200B;在配置组件样式时将向内容作者显示的样式描述。
   * **CSS 类：**&#x200B;与样式关联的 CSS 类的实际名称。
   使用拖动手柄可调整组以及组中样式的顺序。使用添加或删除图标可添加或者删除组或组中的样式。

>[!CAUTION]
>
>The CSS classes (as well as any necessary Javascript) configured as style properties of a component&#39;s policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.

## 设置 {#setup}

核心组件版本2及更高版本已完全启用，可充分利用样式系统，无需额外配置。

只需执行以下步骤，即为您自己的自定义组件启用样式系统，或在“编 [辑”对话框中启用可选的样式选项卡。](#enable-styles-tab-edit)

### 在“设计”对话框中启用“样式”选项卡 {#enable-styles-tab-design}

要使组件能够与AEM的样式系统一起使用并在其设计对话框中显示样式选项卡，组件开发人员必须在组件中包含具有以下设置的样式选项卡：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

配置组件后，由页面作者配置的样式将由 AEM 自动插入到装饰元素，AEM 会自动在每个可编辑的组件周围包裹该装饰元素。组件本身不需要执行任何操作即可实现这一点。

### 在“编辑”对话框中启用“样式”选项卡 {#enable-styles-tab-edit}

自AEM 6.5.3.0版起，“编辑”对话框中的可选样式选项卡现已可用。 与“设计对话框”选项卡不同，“编辑对话框”中的选项卡对于样式系统的功能而言并非必不可少，但对于内容作者来说，它是设置样式的可选替代界面。

编辑对话框选项卡可以采用与设计对话框选项卡类似的方式：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>默认情况下，“编辑”对话框上的“样式”选项卡未启用。

### 具有元素名称的样式 {#styles-with-element-names}

开发人员还可以使用 `cq:styleElements` 字符串数组属性为组件上的样式配置允许的元素名称列表。然后，在设计对话框内策略的“样式”选项卡中，模板作者也可以为每个样式选择一个要设置的元素名称。这将设置包装器元素的元素名称。

此属性在 `cq:Component` 节点上设置。例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>避免为可以合并的样式定义元素名称。当定义多个元素名称时，其优先级顺序为：
>
>1. HTL 优先于所有内容：`data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然后，在多个活动样式中，会采用组件策略中配置的样式列表中的第一个样式。
>1. 最后，组件的 `cq:htmlTag`/`cq:tagName` 将被视为回退值。
>



这种定义样式名称的功能对于极其通用的组件（如布局容器或内容片段组件）非常有用，可为它们提供更多含义。

例如，使用该功能可以为布局容器提供 `<main>`、`<aside>`、`<nav>` 等语义。
