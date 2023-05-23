---
title: 样式系统
seo-title: Style System
description: 样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。
seo-description: The Style System allows a template author to define style classes in the content policy of a component so that a content author is able to select them when editing the component on a page. These styles can be alternative visual variations of a component, making it more flexible.
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
exl-id: 1772368a-f5c9-440c-a92a-0f1d34cc4bf8
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 62%

---

# 样式系统{#style-system}

样式系统允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。

如此一來，您就不需要為每種樣式開發自訂元件，或是自訂元件對話方塊以啟用此類樣式功能。 它帶來更多可重複使用的元件，這些元件可以快速輕鬆地適應內容作者的需求，而無需任何AEM後端開發。

## 用例 {#use-case}

範本作者不僅需要為內容作者設定元件運作方式的能力，還需要設定元件的許多替代視覺變體。

同樣地，內容作者不僅需要建構和排列其內容的能力，還需要選取其視覺呈現方式。

样式系统针对模板作者和内容作者的要求提供了统一的解决方案：

* 範本作者可以在元件的內容原則中定義樣式類別。
* 內容作者接著可在編輯頁面上的元件時，從下拉式清單中選取這些類別，以套用對應的樣式。

然後，樣式類別會插入至元件的裝飾包裝函式元素上，如此一來，元件開發人員就不需要在提供CSS規則以外的方式處理樣式。

## 概述 {#overview}

通常，可通过以下形式来使用样式系统。

1. Web 设计人员创建组件的不同可视化变量。

1. 向 HTML 开发人员提供组件的 HTML 输出以及要实施的所需可视化变量。

1. HTML 开发人员定义与每个可视化变量对应的 CSS 类，该类将插入到组件的包装元素中。

1. HTML 开发人员为每个可视化变量实施相应的 CSS 代码（和可选 JS 代码），以使它们按照定义的方式显示。

1. AEM 开发人员将提供的 CSS（和可选 JS）放置在[客户端库](/help/sites-developing/clientlibs.md)中并对其进行部署。

1. AEM 开发人员或模板作者配置页面模板并编辑每个已设置样式的组件的策略，从而添加定义的 CSS 类、为每种样式提供用户友好名称，并指示可组合的样式。

1. 之后，AEM 页面作者可以在页面编辑器中通过组件工具栏的样式菜单选择设计的样式。

請注意，在AEM中實際執行的只有最後三個步驟。 這表示所有必要的CSS和Javascript開發都可以在不使用AEM的情況下完成。

實際實作樣式只需要在AEM上部署，並在所需範本的元件中選取。

下图说明了样式系统的架构。

![aem-style-system](assets/aem-style-system.png)

## 使用 {#use}

为了演示该功能，我们将使用核心组件的[标题组件](https://www.adobe.com/go/aem_cmp_title_v2_cn)的 [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans) 实施作为示例。

下面的[作为内容作者](#as-a-content-author)和[作为模板作者](#as-a-template-author)部分介绍了如何使用 WKND 样式系统来测试样式系统的功能。

如果您希望为自己的组件使用样式系统，请执行以下操作：

1. 將CSS安裝為使用者端程式庫，如區段所述 [概觀](#overview).
1. 依照一節中的說明，設定您想要可供內容作者使用的CSS類別 [作為範本作者](#as-a-template-author).
1. 然後，內容作者就可以使用區段中所述的樣式 [作為內容作者](#as-a-content-author).

### 作為內容作者 {#as-a-content-author}

1. 安装 WKND 项目后，导航到 WKND 的英语母版主页 `http://<host>:<port>/sites.html/content/wknd/language-masters/en`，然后编辑该页面。
1. 选择该页面下方的&#x200B;**标题**&#x200B;组件

   ![作者的样式系统](assets/style-system-author.png)

1. 点按或单击&#x200B;**列表**&#x200B;组件工具栏上的&#x200B;**样式**&#x200B;按钮以打开样式菜单，然后更改该组件的外观。

   ![选择样式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此示例中，**颜色**&#x200B;样式（**黑色**、**白色**&#x200B;和&#x200B;**灰色**）是互斥的，而&#x200B;**样式**&#x200B;选项（**下划线**、**右对齐**&#x200B;和&#x200B;**最小间距**）则可以组合使用。这可以在[模板中配置为模板作者](#as-a-template-author)。

### 作為範本作者 {#as-a-template-author}

1. 编辑 WKND 的英语母版主页 `http://<host>:<port>/sites.html/content/wknd/language-masters/en` 时，通过&#x200B;**页面信息 > 编辑模板**&#x200B;来编辑该页面的模板。

   ![编辑模板](assets/style-system-edit-template.png)

1. 通过点按或单击&#x200B;**标题**&#x200B;组件的&#x200B;**策略**&#x200B;按钮，编辑该组件的策略。

   ![编辑策略](assets/style-system-edit-policy.png)

1. 在属性的“样式”选项卡中，您可以看到样式的配置方式。

   ![编辑属性](assets/style-system-properties.png)

   * **群組名稱：** 樣式可在樣式選單中分組，內容作者在設定元件樣式時會看到該選單。
   * **樣式可以合併：** 允許同時選取該群組中的多個樣式。
   * **樣式名稱：** 設定元件樣式時，內容作者會看到的樣式說明。
   * **CSS類別：** 與樣式關聯的CSS類別的實際名稱。

   使用拖曳操作框來排列群組的順序以及群組內的樣式。 使用新增或刪除圖示來新增或移除群組內的群組或樣式。

>[!CAUTION]
>
>配置为组件策略的样式属性的 CSS 类（以及任何必需的 Javascript）必须部署为[客户端库](/help/sites-developing/clientlibs.md)才能正常工作。

## 设置 {#setup}

核心组件版本 2 及更高版本完全支持使用样式系统，并且无需进行额外配置。

只有为您自己的自定义组件启用样式系统，或者[在“编辑”对话框中启用可选的“样式”选项卡](#enable-styles-tab-edit)时，才需执行以下步骤。

### 在“设计”对话框中启用“样式”选项卡 {#enable-styles-tab-design}

为了使组件能够与 AEM 的样式系统结合使用并在其“设计”对话框中显示“样式”选项卡，组件开发人员必须通过对组件进行以下设置来包含“样式”选项卡：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

設定好元件後，AEM會自動將頁面作者設定的樣式插入裝飾元素上，AEM會自動將該裝飾元素包裝在每個可編輯的元件周圍。 元件本身不需執行任何其他動作，即可讓此情況發生。

### 在“编辑”对话框中启用“样式”选项卡 {#enable-styles-tab-edit}

自AEM 6.5.3.0版開始，現在提供「編輯」對話方塊中的可選「樣式」索引標籤。 与“设计”对话框选项卡不同，“编辑”对话框中的选项卡对于样式系统的正常运行来说并不是必需的，但它是内容作者设置样式的可选替代界面。

可以采用与“设计”对话框选项卡类似的方式包括“编辑”对话框选项卡：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>默认情况下，“编辑”对话框中的“样式”选项卡处于未启用状态。

### 具有元素名称的样式 {#styles-with-element-names}

开发人员还可以使用 `cq:styleElements` 字符串数组属性为组件上的样式配置允许的元素名称列表。然後在「設計」對話方塊中原則的「樣式」標籤中，範本作者也可以選擇要為每個樣式設定的元素名稱。 這會設定包裝函式元素的元素名稱。

此属性在 `cq:Component` 节点上设置。例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>請避免為可組合的樣式定義元素名稱。 定義多個元素名稱時，優先順序為：
>
>1. HTL 优先于所有内容：`data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然后，在多个活动样式中，会采用组件策略中配置的样式列表中的第一个样式。
>1. 最后，组件的 `cq:htmlTag`/`cq:tagName` 将被视为回退值。

>


这种定义样式名称的功能对于极其通用的组件（如布局容器或内容片段组件）非常有用，可为它们提供更多含义。

例如，使用该功能可以为布局容器提供 `<main>`、`<aside>`、`<nav>` 等语义。
