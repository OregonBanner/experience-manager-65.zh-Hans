---
title: 创建和配置资产编辑器页面
description: 了解如何创建自定义资产编辑器页面和同时编辑多个资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 1%

---


# 创建和配置资产编辑器页面 {#creating-and-configuring-asset-editor-pages}

本文档将介绍以下内容：

* 创建自定义资产编辑器页面的原因。
* 如何创建和自定义资产编辑器页面，这些页面是WCM页面，您可以通过它们视图和编辑元数据，以及对资产执行操作。
* 如何同时编辑多个资产。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>资产共享可用作开放源代码引用实施。 请参 [阅资产共享共享](https://adobe-marketing-cloud.github.io/asset-share-commons/)。 官方不支持。

## 为何要创建和配置资产编辑器页面？ {#why-create-and-configure-asset-editor-pages}

数字资产管理正在越来越多的场景中使用。 当从面向专业培训用户的小型解决方案（例如摄影师或分类学者）转变为面向业务用户、WCM作者、记者等更多元化用户群时，面向专业用户的Adobe Experience Manager资产的强大用户界面会提供太多信息和利益相关方开始，要求特定用户界面或应用程序访问与其相关的数字资产。

这些以资产为中心的应用程序可以是企业内部网中的简单照片库，员工可以从贸易展访问或面向公众的网站的新闻中心上传照片。 以资产为中心的应用程序还可以扩展到包括购物车、结帐和验证流程在内的完整解决方案。

创建以资产为中心的应用程序在很大程度上成为一个无需编码的配置过程，只需了解用户组及其需求以及所使用元数据的知识。 使用Assets创建的以资源为中心的应用程序具有可扩展性： 借助适当的编码工作量，可以创建用于搜索、查看和修改资产的可重用组件。

Experience Manager中以资产为中心的应用程序由资产编辑器页面组成，该页面可用于获取特定资产的详细视图。 资产编辑器页面还允许编辑元数据，前提是访问资产的用户具有必要的权限。

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

![assetshare4](assets/assetshare4.bmp)

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

您可以自定义资产编辑器，以确定用户如何视图和编辑数字资产。 为此，您需要创建一个新的“资产编辑器”页面，然后自定义视图以及用户可以对该页面执行的操作。

>[!NOTE]
>
>如果要向DAM资产编辑器添加自定义字段，请向 `cq:Widget` `/apps/dam/content/asseteditors.`

### 创建资产编辑器页面 {#creating-the-asset-editor-page}

创建资产编辑器页面时，最好在资源共享页面的正下方创建该页面。

要创建资产编辑器页面，请执行以下操作：

1. 在“网 **站** ”选项卡中，导航到要创建资产编辑器页面的位置，然后单击“新 **建”**。
1. 选择 **Geometrixx资产编辑器** ，然后单 **击创建**。 将创建新页面，并且该页面会列在“网 **站** ”选项卡。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用Geometrixx资产编辑器模板创建的基本页面如下所示：

![assetshare5](assets/assetshare5.bmp)

要自定义资产编辑器页面，请使用Sidekick中的元素。 从Geometrixx新闻中心访问的“资 **产编辑器** ”页面是基于此模板的自定义页面版本：

![assetshare6](assets/assetshare6.bmp)

#### 设置要从资产共享页面打开的资产编辑器 {#setting-which-asset-editor-opens-from-an-asset-share-page}

在创建自定义资产编辑器页面后，您需要确保在多次单击您创建的自定义资产共享的资产时，会在自定义编辑器页面中打开资产。

要设置“资产编辑器”页面，请执行以下操作：

1. 在“资产共享”页面中，单 **击查询** 构建器旁边的“编辑”。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 如果尚 **未选** 定，请单击“常规”选项卡。

1. 在资产 **编辑器的路径** ，输入您希望资产共享页面在中打开资产的资产编辑器的路径，然后单击确 **定**。

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 添加资产编辑器组件 {#adding-asset-editor-components}

您可以通过向页面添加组件来确定资产编辑器具有哪些功能。

要添加资产编辑器组件，请执行以下操作：

1. 在要自定义的“资产编辑器”页面中，选择 **Sidekick中的** “资产编辑器”。 将显示所有可用的资产编辑器组件。

>[!NOTE]
>
>您可以自定义的内容取决于可用的组件。 要启用组件，请转至“设计”模式，然后选择需要启用的组件。

1. 将组件从Sidekick拖动到资产编辑器，并在组件对话框中进行任何修改。 下表对这些组件进行了说明，并在随后的详细说明中进行了说明。

>[!NOTE]
>
>在设计资产编辑器页面时，您可以创建只读或可编辑的组件。 用户知道，如果铅笔的图像出现在该组件中，则可以编辑该字段。 默认情况下，大多数组件都设置为只读。

| 组件 | 描述 |
|---|---|
| **[!UICONTROL 元数据表单]和元[!UICONTROL 数据文本字段]** | 允许您向资产添加其他元数据，并对该资产执行操作（如提交）。 |
| **[!UICONTROL 子资产]** | 允许您自定义子资产。 |
| **标记** | 允许用户选择标记并将其添加到资产。 |
| **[!UICONTROL 缩略图]** | 显示资产的缩略图及其文件名，并允许您添加替代文本。 您还可以在此处添加资产编辑器操作。 |
| **[!UICONTROL 标题]** | 显示可自定义的资产标题。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 元数据表单和文本字段——配置视图元数据组件 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

元数据表单是包含开始和结束操作的表单。 在中间输入文 **本** 字段。 有关 [使用表](/help/sites-authoring/default-components-foundation.md#form-component) 单的更多信息，请参阅表单。

1. 通过单击表单的开始区 **域** 中的编辑，创建开始操作。 如果需要，可以输入Box标题。 默认情况下，“框”标题为 **元数据**。 如果希望生成验证的java脚本客户端代码，请选中“客户端验证”复选框。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 通过单击表单的“结束 **”区** 域中的“编辑”创建“结束”操作。 例如，您可能希望创建“提 **交** ”按钮，以允许用户提交其元数据更改。 或者，您可以添加将元 **数据** 重置为其原始状态的“重置”按钮。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 在表单 **开始** 和表 **单结尾之**&#x200B;间，将元数据文本字段拖动到表单中。 用户将元数据填充到这些文本字段中，他们可以提交或完成其他操作。

1. 多次单击字段名称，例如 **标题** ，打开元数据字段并进行更改。 在“编 **辑组** 件 **”窗口的“常规** ”选项卡中，定义命名空间、字段标签以及类型，例如 `dc:title`。

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

有关 [修改元数据表单中可用命名空间](/help/assets/extending-assets.md) ，请参阅自定义和扩展资产。

1. Click the **Constraints** tab. 您可以在此选择字段是否为必填字段，并根据需要添加任何约束。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Click the **Display** tab. 在此，您可以为元数据字段输入新的宽度和行数。 选中字 **段为只读复选框** ，允许用户编辑元数据。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各种字段的元数据表单的示例：

![chlimage_1-162](assets/chlimage_1-390.png)

在“资产编辑器”页面上，用户随后可以在元数据字段中输入值（如果可编辑）并执行结束操作（例如，提交更改）。

#### 子资产 {#sub-assets}

子资产组件是您可以视图和选择子资产的位置。 您可以确定主资产和子资 [产下](/help/assets/assets.md#what-are-digital-assets) 显示的名称。

![screen_shot_2012-04-23at24025pm](assets/screen_shot_2012-04-23at24025pm.png)

多次-单击子资产组件以打开子资产对话框，您可以在该对话框中更改主资产和任何子资产的标题。 默认值显示在相应字段的下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是已填充子资产组件的示例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您选择了子资产，请注意组件如何显示相应的页面以及框标题从子资产更改为同级。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 标记 {#tags}

标记组件是一个组件，用户可以在该组件中为资产分配现有标记，这有助于以后的组织和检索。 您可以使此组件为只读，因此用户无法添加标记，而只能视图标记。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

多次-单击标记组件以打开标记对话框，您可以根据需要从标记中更改标题，也可以选择已分配的命名空间。 要使此字段可编辑，请清除“隐 **[!UICONTROL 藏编辑]** ”复选框。 默认情况下，标记是可编辑的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果用户可以编辑标记，则可以单击铅笔，通过从“标记”下拉菜单中选择标记来添加标记。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是已填充的标记组件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 缩略图 {#thumbnail}

缩略图组件是资产显示选定缩略图的位置（对于许多格式，缩略图会自动提取）。 此外，该组件还显示文件名以 [及您可以修改的操作](/help/assets/assets-finder-editor.md#adding-asset-editor-actions)。

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

多次-单击缩略图组件以打开缩略图对话框，在该对话框中可以更改替代文本。 默认情况下，缩略图替代文本默认为 **单击以下载资** 产。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是已填充的缩略图组件的示例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 标题 {#title}

标题组件显示资产的标题和说明。

![chlimage_1-163](assets/chlimage_1-391.png)

默认情况下，它处于只读模式，因此用户无法编辑它。 要使其可编辑，请多次单击组件并清除“隐 **藏编辑”按钮** 。 此外，为多个资产输入标题。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以编辑标题，则可以通过单击铅笔打开资产属性窗口来添加标题 **和说明** 。 此外，您还可以通过选择日期和时间来打开和关闭资产。

当用户通过单击铅笔图标编辑标题时，他们可以更 **改标题**、 **说明**，并输 **入On** 和 **** Off Times以打开和关闭资产。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是已填充标题组件的示例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 添加资产编辑器操作 {#adding-asset-editor-actions}

您可以通过一系列预定义操作来确定用户可以对选定数字资产执行的操作。

要向“资产编辑器”页面添加操作，请执行以下操作：

1. 在要自定义的“资产编辑器”页面中，单击 **Sidekick中的** “资产编辑器”。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

可以执行以下操作：

| 操作 | 描述 |
|---|---|
| [!UICONTROL 下载] | 允许用户将选定资产下载到其计算机。 |
| [!UICONTROL 编辑者] | 允许用户编辑图像（交互式编辑） |
| [!UICONTROL Lightbox] | 将资产保存到“Lightbox”中，您可以在其中对其执行其他操作。 在跨多个页面处理资产时，此功能非常便于使用。 |
| [!UICONTROL 锁定] | 允许用户锁定资产。 默认情况下，此功能未启用，需要在组件列表中启用。 |
| [!UICONTROL 引用] | 单击此图标可显示资产正在使用的页面。 |
| [!UICONTROL 版本控制] | 允许您创建和恢复资产的版本。 |

1. 将相应的操作拖至页 **面上** 的“操作”区域。 这样做会创建用于执行该操作的按钮。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用“资产编辑器”页面对资产进行多次编辑 {#multi-editing-assets-with-the-asset-editor-page}

通过Experience Manager Assets，您可以一次更改多个资产。 在选定资产后，您可以同时更改其：

* 标记
* 元数据

要使用“资产编辑器”页面对资产进行多次编辑，请执行以下操作：

1. 打开Geometrixx **新闻中心** 页：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 选择资产：

   * 在Windows上： `Ctrl + click` 每个资产。
   * 在Mac上： `Cmd + click` 每个资产。
   要选择资产范围，请执行以下操作： 单击第一个资产，然后 `Shift + click` 单击最后一个资产。

1. 在“ **操作** ”字段( **页面左侧部分** )中单击“编辑元数据”。
1. Geometrixx Press **Center资产编辑器页** 面在新选项卡中打开。 资产的元数据会按如下方式显示：

   * 标记不适用于所有资产，但仅适用于少数几个资产，以斜体显示。
   * 应用于所有资产的标记会以普通字体显示。
   * 除标记之外的元数据： 仅当所有选定资产的值相同时，才会显示字段的值。

1. 单击 **下载** ，以下载包含资产原始演绎版的zip文件。
1. 单击“标记”字段旁 **边的** “铅笔”图标以编辑标记：

   * 并不适用于所有资产，但只适用于少数资产的标记具有灰色背景。
   * 应用于所有资源的标记具有白色背景。
   您可以：

   * 单击 **x** 图标以删除所有资产的标记。
   * 单击 **+图标** ，将标记添加到所有资产。
   * 单击箭 **头** ，然后选择一个标记以向所有资产添加新标记。
   单 **击** “确定”将更改写入表单。 将自动选中 **“标记** ”字段旁边的框。

1. 编辑“说明”字段。 例如，将其设置为：

   `This is a common description`

   编辑字段时，其值会在提交表单时覆盖选定资产的现有值。

   注意： 编辑字段时，将自动选中该字段旁边的框。

1. 单击 **更新元数据** ，以提交表单并保存所有资产的更改。

   注意： 只修改选中的元数据。
