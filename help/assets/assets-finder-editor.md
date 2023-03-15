---
title: 创建和配置资产编辑器页面
description: 了解如何创建自定义资产编辑器页面并同时编辑多个资产。
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 1%

---

# 创建和配置资产编辑器页面 {#creating-and-configuring-asset-editor-pages}

本文档将介绍以下内容：

* 为什么要创建自定义的资产编辑器页面。
* 如何创建和自定义Asset Editor页面，这些页面是WCM页面，允许您查看和编辑元数据以及对资源执行操作。
* 如何同时编辑多个资源。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>资产共享可用作开源参考实施。 参见 [资产共享公域](https://adobe-marketing-cloud.github.io/asset-share-commons/). 官方并不支持此功能。

## 为何要创建和配置Asset Editor页面？ {#why-create-and-configure-asset-editor-pages}

数字资产管理正在越来越多的场景中使用。 从面向受过专业培训的少数用户群体（例如摄影师或分类学家）的小型解决方案，过渡到更大、更多样化的用户群体（例如商业用户、WCM作者、记者等）时，强大的 [!DNL Adobe Experience Manager Assets] 对于专业用户而言，可能会提供太多的信息，利益相关者会开始请求特定的用户界面或应用程序访问与其相关的数字资产。

这些以资产为中心的应用程序可以是内部网中的简单照片画廊，员工可以在其中从展会访问或面向公众的网站的新闻中心上传照片。 以资产为中心的应用程序还可以扩展到包括购物车、结帐和验证流程在内的完整解决方案。

创建以资产为中心的应用程序在很大程度上变成了一个无需编码、仅了解用户组及其需求以及了解正在使用的元数据的配置过程。 使用创建的以资产为中心的应用程序 [!DNL Assets] 可扩展：通过适度编码，可以创建可重复使用的组件，用于搜索、查看和修改资源。

中一个以资产为中心的应用程序 [!DNL Experience Manager] 包含一个资产编辑器页面，该页面可用于获取特定资产的详细视图。 如果访问资产的用户拥有必要的权限，则还可以通过资产编辑器页面编辑元数据。

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create a new Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create a new Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create a new asset share page via the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes a number of predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example cq:tags) and a content tree to populate the options from (for example the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, e.g. tiff:ImageLength and the user can then enter a value, e.g. 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## 创建和配置资产编辑器页面 {#creating-and-configuring-an-asset-editor-page}

您可以自定义资产编辑器，以确定用户查看和编辑数字资产的方式。 为此，您需要创建一个新的Asset Editor页面，然后自定义用户可在该页面上执行的视图和操作。

>[!NOTE]
>
>如果要将自定义字段添加到DAM资产编辑器，请新增 `cq:Widget` 节点至 `/apps/dam/content/asseteditors.`

### 创建资产编辑器页面 {#creating-the-asset-editor-page}

创建资产编辑器页面时，好的做法是直接在资产共享页面下方创建页面。

要创建资产编辑器页面，请执行以下操作：

1. 在 **[!UICONTROL 网站]** 选项卡，导航到要创建资产编辑器页面的位置，然后单击 **新**.
1. 选择 **Geometrixx资产编辑器** 并单击 **创建**. 此时将创建新页面，并且该页面将列在 **网站** 选项卡。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用Geometrixx资产编辑器模板创建的基本页面如下所示：

![assetshare5](assets/assetshare5.png)

要自定义Asset Editor页面，请使用sidekick中的元素。 可从访问的资产编辑器页面 **Geometrixx新闻中心** 是基于此模板的页面的自定义版本：

![assetshare6](assets/assetshare6.png)

#### 将资产编辑器设置为从资产共享页面打开 {#setting-which-asset-editor-opens-from-an-asset-share-page}

创建自定义资产编辑器页面后，您需要确保双击所创建的自定义资产共享在自定义编辑器页面中打开资产时。

要设置资产编辑器页面，请执行以下操作：

1. 在“资产共享”页面中，单击 **编辑** ，位于查询生成器旁边。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 单击 **常规** 选项卡（如果尚未选择）。

1. 在 **资产编辑器的路径** 字段中，输入要在资产共享页面中打开资产的资产编辑器的路径，然后单击 **确定**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 添加资产编辑器组件 {#adding-asset-editor-components}

您可以通过向页面添加组件来确定资产编辑器具有什么功能。

要添加资产编辑器组件，请执行以下操作：

1. 在要自定义的资产编辑器页面中，选择 **资产编辑器** 在副手手里。 将显示所有可用的资产编辑器组件。

>[!NOTE]
>
>可自定义的内容取决于可用的组件。 要启用组件，请转到“设计”模式并选择需要启用的组件。

1. 将组件从Sidekick拖到资产编辑器中，并在组件对话框中进行任何修改。 下表介绍了这些组件，下面的详细说明对这些组件进行了说明。

>[!NOTE]
>
>在设计资产编辑器页面时，您可以创建只读或可编辑的组件。 用户知道，如果铅笔的图像出现在组件中，则可以编辑字段。 默认情况下，大多数组件都设置为只读。

| 组件 | 描述 |
|---|---|
| **[!UICONTROL 元数据表单] 和 [!UICONTROL 元数据文本字段]** | 允许您将其他元数据添加到资源中并对该资源执行操作，例如提交。 |
| **[!UICONTROL 子资产]** | 允许您自定义子资产。 |
| **标记** | 允许用户选择标记并将其添加到资源。 |
| **[!UICONTROL 缩略图]** | 显示资源的缩略图及其文件名，并允许您添加替换文本。 您也可以在此处添加资产编辑器操作。 |
| **[!UICONTROL 标题]** | 显示可自定义的资源标题。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 元数据表单和文本字段 — 配置视图元数据组件 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

元数据表单是一个包含开始和结束操作的表单。 在两者之间，输入 **文本** 字段。 参见 [Forms](/help/sites-authoring/default-components-foundation.md#form-component) 以了解有关使用表单的更多信息。

1. 通过单击创建开始操作 **编辑** 在表单的“开始”区域中。 如果需要，可以输入Box标题。 默认情况下，框标题为 **元数据**. 如果要生成用于验证的java-script客户端代码，请选中“客户端验证”复选框。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 通过单击创建“结束”操作 **编辑** 表单的结束区域。 例如，您可能希望创建 **[!UICONTROL 提交]** 允许用户提交其元数据更改的选项。 或者，您也可以添加 **重置** 用于将元数据重置为其原始状态的选项。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 介于之间 **表单开始** 和 **表单结尾**，将元数据文本字段拖到表单中。 用户将元数据填充到这些文本字段中，他们可以在这些字段中提交或完成其他操作。

1. 双击字段名称，例如， **标题** 以打开元数据字段并进行更改。 在 **常规** 的选项卡 **编辑组件** 窗口中，您可以定义命名空间和字段标签以及类型，例如， `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

参见 [自定义和扩展资产](/help/assets/extending-assets.md) 有关修改元数据表单中可用的命名空间的信息。

1. 单击 **约束** 选项卡。 在此处，您可以选择是否需要字段，并根据需要添加任何约束。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 单击 **显示** 选项卡。 在这里，您可以为元数据字段输入新的宽度和行数。 选择 **字段为只读** 用于允许用户编辑元数据的复选框。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各种字段的元数据表单示例：

![元数据](assets/chlimage_1-390.png)

在Asset Editor页面上，用户随后可以在元数据字段中输入值（如果它们可编辑）并执行结束操作（例如，提交更改）。

#### 子资产 {#sub-assets}

在子资产组件中，您可以查看和选择子资产。 您可以确定 [主资产](/help/assets/assets.md#what-are-digital-assets) 和子资产。

双击子资产组件以打开子资产对话框，您可以在其中更改主资产和任何子资产的标题。 默认值显示在相应字段的下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是填充的子资产组件示例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您选择子资产，请注意组件如何显示相应的页面，以及“框”标题如何从“子资产”更改为“同级”。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 标记 {#tags}

标记组件是一个组件，用户可以在其中将现有标记分配给资产，这有助于以后组织和检索。 您可以将此组件设置为只读，以便用户无法添加标记，而只能查看它们。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

双击“标记”组件以打开“标记”对话框，可以在其中根据需要从“标记”中更改标题，还可以选择分配的命名空间。 要使此字段可编辑，请清除 **[!UICONTROL 隐藏编辑]** 复选框。 默认情况下，标记是可编辑的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果用户可以编辑标记，则可以通过从“标记”下拉菜单中选择标记来单击铅笔以添加标记。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是填充的标记组件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 缩略图 {#thumbnail}

缩略图组件是资产显示选定缩略图的地方（对于多种格式，缩略图都是自动提取的）。 此外，组件会显示文件名，并且 [可修改的操作](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

双击缩略图组件以打开缩略图对话框，您可以在其中更改替换文本。 默认情况下，缩略图替代文本默认为 **单击以下载** 资产。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是填充的缩略图组件示例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 标题 {#title}

标题组件显示资源的标题和描述。

默认情况下，它处于只读模式，因此用户无法编辑它。 要使其可编辑，请双击该组件并清除 **隐藏编辑按钮** 复选框。 此外，为多个资产输入标题。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以编辑标题，则可以通过单击铅笔打开 **资产属性** 窗口。 此外，您还可以通过选择日期和时间来打开和关闭资产。

编辑 [!UICONTROL 标题]，用户可以更改 **标题**， **描述**，并输入 **日期** 和 **关闭时间** 以打开和关闭资产。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是填充的标题组件示例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 添加资产编辑器操作 {#adding-asset-editor-actions}

您可以通过一系列预定义的操作来确定用户可对选定数字资源执行的操作。

要将操作添加到资产编辑器页面，请执行以下操作：

1. 在要自定义的资产编辑器页面中，单击 **资产编辑器** 在副手手里。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

以下操作可用：

| 操作 | 描述 |
|---|---|
| [!UICONTROL 下载] | 允许用户将选定的资产下载到其计算机。 |
| [!UICONTROL 编辑者] | 允许用户编辑图像（交互式编辑） |
| [!UICONTROL Lightbox] | 将资产保存到“灯箱”，您可以在其中对其执行其他操作。 当在多个页面中处理资产时，这非常有用。 |
| [!UICONTROL 锁定] | 允许用户锁定资源。 默认情况下不启用此功能，需要在组件列表中启用此功能。 |
| [!UICONTROL 引用] | 单击此项可在使用资产的页面上显示。 |
| [!UICONTROL 版本控制] | 允许您创建和恢复资源的版本。 |

1. 将相应的操作拖到 **操作** 区域。 它会创建一个选项，用于执行在页面上拖动的操作。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用“资产编辑器”页面可多次编辑资产 {#multi-editing-assets-with-the-asset-editor-page}

替换为 [!DNL Experience Manager Assets] 您可以一次更改多个资产。 选择资源后，您可以同时更改其：

* 标记
* 元数据

要使用“资产编辑器”页面多编辑资产，请执行以下操作：

1. 打开Geometrixx **新闻中心** 页面：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 选择资源：

   * 在Windows上： `Ctrl + click` 每个资产。
   * 在Mac上： `Cmd + click` 每个资产。

   要选择一系列资源，请执行以下操作：单击第一个资源，然后单击 `Shift + click` 最后一个资源。

1. 单击 **编辑元数据** 在 **操作** 字段（页面左侧）。
1. Geometrixx **新闻中心资产编辑器** 页面将在新选项卡中打开。 资源的元数据显示如下：

   * 标记不适用于所有资产，但仅适用于少数资产，以斜体显示。
   * 应用于所有资产的标记将以普通字体显示。
   * 标记以外的元数据：仅当所有选定资源都相同时，才会显示字段的值。

1. 单击 **下载** 下载包含资产原始演绎版的ZIP文件。
1. 单击旁边的“编辑标记”选项 **标记** 字段。

   * 并非适用于所有资产，但只适用于少数资产的标记具有灰色背景。
   * 应用于所有资产的标记具有白色背景。

   您可以：

   * 单击 `x` 以移除所有资产的标记。
   * 单击 `+` 以将标记添加到所有资产。
   * 单击 **箭头** 并选择标记以向所有资产添加新标记。

   单击 **确定** 将更改写入表单。 旁边的那个盒子 **标记** 字段会自动选中。

1. 编辑说明字段。 例如，将其设置为：

   `This is a common description`

   编辑字段时，其值会在提交表单时覆盖所选资产的现有值。

   注意：编辑字段时，将自动选中字段旁边的框。

1. 单击 **更新元数据** 以提交表单并保存所有资产的更改。

   注意：仅修改选中的元数据。
