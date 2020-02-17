---
title: 使用和扩展构件（经典UI）
seo-title: 使用和扩展构件（经典UI）
description: AEM的基于Web的界面使用AJAX和其他现代浏览器技术，使创作者能够直接在网页上对内容进行WYSIWYG编辑和格式化
seo-description: AEM的基于Web的界面使用AJAX和其他现代浏览器技术，使创作者能够直接在网页上对内容进行WYSIWYG编辑和格式化
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 使用和扩展构件（经典UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本页介绍了在经典UI中使用构件（在AEM 6.4中已弃用）的情况。
>
>Adobe建议您基于 [Coral UI和Granite UI利用新](/help/sites-developing/touch-ui-concepts.md) 式触屏优 [化UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)[](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)。

Adobe Experience Manager的基于Web的界面使用AJAX和其他现代浏览器技术，使创作者能够直接在网页上对内容进行WYSIWYG编辑和格式化。

Adobe Experience Manager(AEM)使用 [ExtJS](https://www.sencha.com/) 构件库，该构件库提供高度流畅的用户界面元素，这些元素可跨所有最重要的浏览器工作，并允许创建桌面级UI体验。

这些构件包含在AEM中，除了供AEM本身使用外，还可供使用AEM构建的任何网站使用。

有关AEM中所有可用构件的完整引用，您可以参阅构件 [API文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) ，或查看现 [有xtypes列表](/help/sites-developing/xtypes.md)。 此外，Sencha站点（框架的所有者）上提供了许多说明如何使用ExtJS框架的示 [例](https://www.sencha.com/products/extjs/examples/) 。

本页提供了一些有关如何使用和扩展构件的洞察。 它首先介绍如 [何在页面中包含客户端代码](#including-the-client-sided-code-in-a-page)。 然后，它描述了为说明一些基本用途和扩展而创建的一些示例组件。 这些组件位于包共享 **上的使用ExtJS构件** 包 **中**。

该包包括以下示例：

* [使用现成构件](#basic-dialogs) (Widget)构建的基本对话框。
* [使用现成构件](#dynamic-dialogs) 、自定义的javascript逻辑构建的动态对话框。
* 基于自定义构件 [的对话框](#custom-widgets)。
* 树 [面板](#tree-overview) ，在给定路径下显示JCR树。
* 以表 [格格式显示数据](#grid-overview) 的网格面板。

>[!NOTE]
>
>Adobe Experience manager的经典UI基于 [ExtJS 3.4.0构建](https://extjs.cachefly.net/ext-3.4.0/docs/)。

## 在页面中包括客户端代码 {#including-the-client-sided-code-in-a-page}

客户端javascript和样式表代码应放在客户端库中。

创建客户端库：

1. 使用以下属 `/apps/<project>` 性创建节点：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * 类别=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;
   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 在下 `clientlib` 面创建 `css` 和文 `js` 件夹(nt:folder)。

1. 在下 `clientlib` 面创建 `css.txt` 和 `js.txt` 文件(nt:files)。 这些。txt文件会列出库中包含的文件。

1. 编辑 `js.txt`:它需要以“ `#base=js`”开头，后跟将由CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 编辑 `css.txt`:它需要以“ `#base=css`”开头，后跟将由CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=css
    components.css
   ```

1. 在文件 `js` 夹下，放置属于库的javascript文件。

1. 在文 `css` 件夹下，放置文 `.css` 件和css文件使用的资源(例如， `my_icon.png`)。

>[!NOTE]
>
>前面所述的样式表处理是可选的。

要在页面组件jsp中包含客户端库，请执行以下操作：

* 要同时包括javascript代码和样式表，请执行以下操作：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
其中 `<category-nameX>` 是客户端库的名称。

* 要仅包含javascript代码，请执行以下操作：
   `<ui:includeClientLib js="<category-name>"/>`

有关详细信息，请参阅 [&lt;ui:includeClientLib>标签的说明](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 。

在某些情况下，客户端库应仅在创作模式下可用，并应在发布模式下排除。 具体实现如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 范例入门 {#getting-started-with-the-samples}

要按照本页中的教程操作，请将名为 **** Using ExtJS Widgets的包安装到本地AEM实例中，并创建一个包含这些组件的示例页面。 为此，请执行以下操作：

1. 在AEM实例中，从“包共享” **中下载名为“使用ExtJS构件(v01)** ”的包并安装该包。 它将在存储库 `extjstraining` 中创 `/apps` 建下面的项目。
1. 将包含脚本(js)和样式表(css)的客户端库包含在geometrixx页面jsp的head标签中，因为您将在 **** Geometrixx分支的新页面中包含示例组件：在 **CRXDE中** ，打开文件 `/apps/geometrixx/components/page/headlibs.jsp` 并将类别添加 `cq.extjstraining` 到现有标签中，如 `<ui:includeClientLib>` 下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在下面的 **Geometrixx** 分支中创建新页 `/content/geometrixx/en/products` 面，并将其命 **名为使用ExtJS Widget**。
1. 进入设计模式，将名为“使用ExtJS构件”的组 **的所有组件添加到Geometrixx的设计中** 。
1. 返回编辑模式：使用ExtJS构件 **的组的组件** ，可在Sidekick中找到。

>[!NOTE]
>
>本页上的示例基于Geometrixx示例内容，该示例内容不再随AEM一起提供，但已被We.Retail替换。 有关如何下载 [和安装Geometrixx的信息，请参阅文档We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx) 。

### 基本对话框 {#basic-dialogs}

对话框通常用于编辑内容，但也只能显示信息。 查看完整对话框的一种简单方法是访问其json格式的表示形式。 为此，请将您的浏览器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

在Sidekick中使用ExtJS **构件组的第一个组件** ，称为 **1。 对话框基础** ，包括四个基本对话框，这些对话框是使用现成构件构建的，并且没有自定义的javascript逻辑。 对话框存储在下面 `/apps/extjstraining/components/dialogbasics`。 基本对话框包括：

* 完整对话框( `full` 节点):它显示一个包含3个选项卡的窗口，每个选项卡都包含2个文本字段。
* 单个面板对话框( `singlepanel` 节点):它显示一个窗口，其中包含1个选项卡，其中包含2个文本字段。
* 多面板对话框(节 `multipanel` 点):其显示与“完整”对话框相同，但构建方式不同。
* 设计对话框(节 `design` 点):它显示一个包含2个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集（4个文本字段）和一个可折叠的字段集（2个文本字段）。

包括 **1。 示例页面中的对话框基础** (Dialog Basics)组件：

1. 添加 **1。 对话框基础** ”组件，该组件位于Sidekick中“使 **用ExtJS构件** ”选项卡的示 **例页面**。
1. 该组件显示标题、一些文本和 **PROPERTIES** 链接：单击该链接可显示存储在存储库中的段落的属性。 再次单击链接以隐藏属性。

组件显示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 示例1:完整对话框 {#example-full-dialog}

“完 **整** ”对话框显示一个窗口，其中包含三个选项卡，每个选项卡具有两个文本字段。 它是对话框基础组件的默 **认对话框** 。 其特点是：

* 由节点定义：节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 显示3个选项卡(节点类型= `cq:Panel`)。
* 每个选项卡都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/full`
* 通过请求以JSON格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

对话框显示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 示例2:单个面板对话框 {#example-single-panel-dialog}

“单 **个面板** ”对话框显示一个窗口，其中一个选项卡具有两个文本字段。 其特点是：

* 显示1个选项卡(节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* 选项卡有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 与完整对话框相 **比** ，一个优势是需要的配置更少。
* 建议使用：用于显示信息或只有几个字段的简单对话框。

要使用“单个面板”对话框，请执行以下操作：

1. 将对话框基础 **组件的对话框** ，替换为 **单个面板对话框** :
   1. 在 **CRXDE Lite中**，删除节点： `/apps/extjstraining/components/dialogbasics/dialog`
   1. Click **Save All** to save the changes.
   1. 复制节点： `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 将复制的节点粘贴到以下位置： `/apps/extjstraining/components/dialogbasics`
   1. 选择节点：并 `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`重命名它 `dialog`。
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 示例3:多面板对话框 {#example-multi-panel-dialog}

“多 **面板** ”对话框与“完整”对话框的显示屏 **相同** ，但构建方式不同。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)。
* 显示3个选项卡(节点类型= `cq:Panel`)。
* 每个选项卡都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 与“完整对话 **框”相比** ,“完整对话框”的一个优势是结构简化。
* 建议使用：中。

要使用“多面板”对话框，请执行以下操作：

1. 将对话框基础 **组件的对话框** ，替换为 **多面板对话框** :按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 示例4:富对话框 {#example-rich-dialog}

“ **富** ”对话框显示一个包含两个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集（包含四个文本字段）和一个可折叠字段集（包含两个文本字段）。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示2个选项卡(节点类型= `cq:Panel`)。
* 第一个选项卡具有带 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 有一个构件和一个 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 带有3个选项 ` [selection](/help/sites-developing/xtypes.md#selection)` 的构件以及一个带有构件 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 的可折叠 ` [textarea](/help/sites-developing/xtypes.md#textarea)` 构件。
* 第二个选项卡具有一个 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 带有4个构件的构件 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 和一个带有2个构件 `dialogfieldset` 的可折叠 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 构件。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/rich`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

要使用“富 **”对话框** :

1. 用“丰富”对话框替 **换对话框** “对话框基 **础** ”组件：按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 动态对话框 {#dynamic-dialogs}

在Sidekick中使用ExtJS **构件组的第** 2个组件称为 **2。 动态对话框** ，包括三个动态对话框，它们是使用现成的构件和自定义的javascript逻辑 **构建的**。 对话框存储在下面 `/apps/extjstraining/components/dynamicdialogs`。 动态对话框包括：

* 切换选项卡对话框(节 `switchtabs` 点):它显示一个包含两个选项卡的窗口。 第一个选项卡有一个单选按钮选项，其中包含三个选项：选中某个选项时，将显示与该选项相关的选项卡。 第二个选项卡包含两个文本字段。
* 任意对话框( `arbitrary` 节点):它显示一个带有一个选项卡的窗口。 该选项卡包含一个用于拖放或上传资产的字段，以及一个字段，该字段显示有关包含页面以及资产（如果引用了该页面）的一些信息。
* 切换字段对话框(节 `togglefield` 点):它显示一个带有一个选项卡的窗口。 该选项卡中有一个复选框：选中后，将显示一个包含两个文本字段的字段集。

包含 **2。 示例页面上的** “动态对话框”组件：

1. 添加 **2。 动态对话框** ”组件，该组件位于Sidekick中“使 **用ExtJS构件** ”选项卡的示 **例页面**。
1. 该组件显示标题、一些文本和 **PROPERTIES** 链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。

组件显示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 示例1:切换选项卡对话框 {#example-switch-tabs-dialog}

“切 **换选项卡** ”对话框显示一个包含两个选项卡的窗口。 第一个选项卡有一个单选按钮选项，其中包含三个选项：选中某个选项时，将显示与该选项相关的选项卡。 第二个选项卡包含两个文本字段。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示2个选项卡(节点类型= `cq:Panel`):1选项卡，第2个选项卡取决于第1个选项卡（3个选项）中的选择。
* 有3个可选选项卡(节点类型= `cq:Panel`)，每个选项卡都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。 一次只显示一个可选选项卡。
* 由位于以下位置 `switchtabs` 的节点定义：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* 对话框节点有一个“ `beforeshow`”监听器，它在显示对话框之前隐藏所有可选选项卡：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
   `dialog.items.get(0)` 获取包含选择面板和3个可选面板的表面板。
* 该对 `Ejst.x2` 象在以下位置的文 `exercises.js` 件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在该方 `Ejst.x2.manageTabs()``index` 法中，当值为-1时，所有可选选项卡都将被隐藏（i从1到3）。
* 选择选项卡具有2个监听器：一个选项卡在加载对话框时显示选定选项卡(“ `loadcontent`”事件)，另一个选项卡在更改选择时显示选定选项卡(“ `selectionchanged`”事件):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在方 `Ejst.x2.showTab()` 法中：
   `field.findParentByType('tabpanel')` 获取包含所有选项卡的表面板( `field` 表示选择构件)
   `field.getValue()` 获取选择的值，例如：tab2
   `Ejst.x2.manageTabs()` 显示选定的选项卡。
* 每个可选选项卡都有一个监听器，用于隐藏“ `render`”事件上的选项卡：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在方 `Ejst.x2.hideTab()` 法中：
   `tabPanel` 是包含所有选项卡的表面板
   `index` 是可选选项卡的索引
   `tabPanel.hideTabStripItem(index)` 隐藏选项卡

它显示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 示例2:任意对话框 {#example-arbitrary-dialog}

通常情况下，对话框会显示基础组件中的内容。 此处描述的对话框称为“任 **意** ”对话框，它从其他组件中提取内容。

“任 **意** ”对话框显示一个带有一个选项卡的窗口。 该选项卡包含两个字段：一个用于拖放或上传资产，另一个用于显示有关包含页面以及资产（如果某个页面已被引用）的某些信息。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个Tabpanel构件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)和1个面板(节点类型= `cq:Panel`)
* 该面板有一个智能文件构件(节点类型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)和一个所有权绘制构件(节点类型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* 由位于以下位置 `arbitrary` 的节点定义：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* ownerdraw构件有一个“ `loadcontent`”监听器，它显示有关加载内容时包含组件的页面和智能文件构件引用的资产的信息：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
   `field` 使用ownerdraw对象设置
   `path` 设置为组件的内容路径(例如：/content/geometrixx/cn/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* 该对 `Ejst.x2` 象在以下位置的文 `exercises.js` 件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在方 `Ejst.x2.showInfo()` 法中：
   `pagePath` 是包含组件的页面的路径
   `pageInfo` 表示json格式的页面属性
   `reference` 是引用资产的路径
   `metadata` 以json格式表示资产的元数据
   `ownerdraw.getEl().update(html);` 在对话框中显示创建的html

要使用“任意 **”对话框** :

1. 用“任意”对话 **框替换** “动态对 **话框** ”组件：按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 示例3:切换字段对话框 {#example-toggle-fields-dialog}

“切 **换字段** ”对话框显示一个带有一个选项卡的窗口。 该选项卡中有一个复选框：选中后，将显示一个包含两个文本字段的字段集。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个Tabpanel构件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`)和1个面板(节点类型= `cq:Panel`)。
* 该面板有一个选择／复选框构件(节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`)和一个可折叠的对话框域集构件(节点类型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`)，默认情况下隐藏该构件，其中包含2个文本域构件(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由位于以下位置 `togglefields` 的节点定义：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* 选择选项卡具有2个监听器：其中一个显示加载内容时的对话框字段集(“ `loadcontent`”事件)，另一个显示更改选择时的对话框字段集(“ `selectionchanged`”事件):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* 该对 `Ejst.x2` 象在以下位置的文 `exercises.js` 件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在方 `Ejst.x2.toggleFieldSet()` 法中：
   `box` 是选择对象
   `panel` 是包含选择和对话框字段集构件的面板
   `fieldSet` 是对话框字段集对象
   `show` 是根据对话框字段集显示或不显示的“ ” `show`选择的值（true或false）

要使用“切换字 **段”对话框** :

1. 将“动态对话框”组 **件的对话框** 替换为“切 **换字段”对话框** :按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自定义构件 {#custom-widgets}

AEM附带的现成构件应涵盖大多数使用案例。 但是，有时可能需要创建自定义构件来满足特定于项目的要求。 可通过扩展现有构件来创建自定义构件。 为帮助您开始进行此类自定义，“使 **** 用ExtJS构件”包中包括三个使用三个不同自定义构件的对话框：

* 多字段对话框(节 `multifield` 点)显示一个包含一个选项卡的窗口。 该选项卡具有一个自定义的多字段构件，该构件具有两个字段：一个包含两个选项的下拉菜单和一个文本字段。 由于它基于现成构件(只有一个文 `multifield` 本字段)，因此它具有构件的所有功 `multifield` 能。
* 树浏览对话框(节 `treebrowse` 点)显示一个窗口，其中有一个选项卡包含路径浏览构件：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 然后，项目的路径将添加到路径字段，并在关闭对话框时保留。
* 基于富文本编辑器插件的对话框（节点），可向富文本编辑器中添加一个自定义按钮，以将一些自定义文本插入主文本。 `rteplugin` 它由构件( `richtext` RTE)和通过RTE插件机制添加的自定义功能组成。

自定义构件和插件包含在名为 **3的组件中。 使用** ExtJS构件包 **的自定义构件** 。 要将此组件包含到示例页面，请执行以下操作：

1. 添加 **3。 自定义构件** (Custom Widgets **)组件，从Sidekick中的“使用ExtJS构** 件”选项卡 **，指向示例**&#x200B;页面。
1. 该组件显示标题、一些文本，并在单击 **PROPERTIES** 链接时，显示存储在存储库中的段落属性。 再次单击会隐藏属性。
组件显示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 示例1:自定义多字段构件 {#example-custom-multifield-widget}

基于 **自定义多字段** (Custom Multifield)构件的对话框显示一个带有一个选项卡的窗口。 该选项卡具有自定义的多字段构件，该构件与标准构件（具有一个字段）不同，具有两个字段：一个包含两个选项的下拉菜单和一个文本字段。

基于 **自定义多字段** 构件的对话框：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个包含面板(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)的表面板构件(节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 该面板有一个 `multifield` 构件(节点类型= `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`)。
* 构 `multifield` 件有一个基于自定义xtype &#39; `nt:unstructured`&#39;的字段配置(节点类型= 、 xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions``ejstcustom`):
   * “ `fieldconfig`”是对象的配置选 ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` 项。
   * “ `optionsProvider`”是构件的配 `ejstcustom` 置。 它使用在以下位置 `Ejst.x3.provideOptions` 定义的方法进 `exercises.js` 行设置：
      `/apps/extjstraining/clientlib/js/exercises.js`
并返回2个选项。
* 由位于以下位置 `multifield` 的节点定义：
   `/apps/extjstraining/components/customwidgets/multifield`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自定义多字段构件(xtype = `ejstcustom`):

* 是名为javascript对象 `Ejst.CustomWidget`。
* 在以下位置的 `CustomWidget.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 扩展构 ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` 件。
* 包含3个字段：( `hiddenField` 文本字段)、 `allowField` (ComboBox) `otherField` 和（文本字段）
* 覆盖 `CQ.Ext.Component#initComponent` 以添加3个字段：
   * `allowField` 是 [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) object，类型为“select”。 optionsProvider是Selection对象的配置，该对象使用对话框中定义的CustomWidget的optionsProvider配置进行实例化
   * `otherField` 是 [CQ.Ext.form.TextField对象](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)
* 重写 `setValue`CQ.form.CompositeField的方 `getValue``getRawValue`[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) 法和方法，以设置和检索格式为CustomWidget的值：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`.
* 将自身注册为“ `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

基于 **自定义多字段** (Custom Multifield)构件的对话框显示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 示例2:自定义树状浏览构件 {#example-custom-treebrowse-widget}

基于树状 **浏览构件的自定义** “树状浏览构件”对话框显示一个窗口，其中有一个选项卡包含一个自定义路径浏览构件：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 然后，项目的路径将添加到路径字段，并在关闭对话框时保留。

自定义树浏览对话框：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个包含面板(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)的表面板构件(节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 该面板有一个自定义构件(节点类型= `cq:Widget`, xtype = `ejstbrowse`)
* 由位于以下位置 `treebrowse` 的节点定义：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自定义树状浏览构件(xtype = `ejstbrowse`):

* 是名为javascript对象 `Ejst.CustomWidget`。
* 在以下位置的 `CustomBrowseField.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 扩展 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`。
* 定义一个名为的浏览窗口 `browseWindow`。
* 覆盖 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` 在单击箭头时显示浏览窗口。
* 定义 [CQ.Ext.tree.TreePanel对象](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) :
   * 它通过调用在注册的servlet获取其数据 `/bin/wcm/siteadmin/tree.json`。
   * 其根为“ `apps/extjstraining`”。
* 定义 `window` 对象( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 基于预定义面板。
   * 有一个 **确定** (OK)按钮，用于设置所选路径的值并隐藏面板。
* 窗口锚定在“路径” **字段下** 。
* 选定的路径将从浏览字段传递到事件窗口 `show` 中。
* 将自身注册为“ `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

要使用基于自定 **义树状浏览构件** 的对话框，请执行以下操作：

1. 将“自定义构件”组 **件的对话框替换** “自定 **义树浏览”对话框** :按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件：该对话框如下所示：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 示例3:富文本编辑器(RTE)插件 {#example-rich-text-editor-rte-plug-in}

基 **于富文本编辑器(RTE)插件的对话框是基于富文本编辑器的对话框** ，该对话框包含一个自定义按钮，用于在方括号内插入一些自定义文本。 自定义文本可由某些服务器端逻辑（本例中未实现）分析，例如添加在给定路径中定义的一些文本：

基于 **RTE插件的对话框** :

* 由位于以下位置的retplugin节点定义：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* 该节 `rtePlugins` 点有一个以插件 `inserttext` 命名的子节点(节点类型= `nt:unstructured`)。 它有一个名为的 `features`属性，该属性定义RTE可使用的插件功能。

RTE插件：

* 是名为javascript对象 `Ejst.InsertTextPlugin`。
* 在以下位置的 `InsertTextPlugin.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 扩展对 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 象。
* 以下方法定义了对 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 象，并在实施插件中被覆盖：
   * `getFeatures()` 返回插件可用的所有功能的数组。
   * `initializeUI()` 将新按钮添加到RTE工具栏。
   * `notifyPluginConfig()` 在悬停按钮时显示标题和文本。
   * `execute()` 在单击按钮并执行插件操作时调用：它显示一个窗口，用于定义要包含的文本。
* `insertText()` 使用相应的对话框对象插入文 `Ejst.InsertTextPlugin.Dialog` 本（请参阅后面）。
* `executeInsertText()` 由对话框的 `apply()` 方法调用，单击“确定”按钮时 **将触发** 。
* 将自身注册为“ `inserttext`”插件：
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* 对 `Ejst.InsertTextPlugin.Dialog` 象定义单击插件按钮时打开的对话框。 该对话框由面板、表单、文本字段和2个按钮(确&#x200B;**定** 和 **取消**)组成。

要使用基 **于富文本编辑器(RTE)插件的对话框** ，请执行以下操作：

1. 将“自定义构件 **”组件的对** 话框替换为基于 **富文本编辑器(RTE)插件的对话框** :按照示例2中描述的 [步骤操作：单个面板对话框](#example-single-panel-dialog)
1. 编辑组件。
1. 单击右侧的最后一个图标（带四个箭头的图标）。 输入路径，然后单击“确 **定”**:路径显示在括号([ ]).
1. 单击 **确定** ，关闭富文本编辑器。

基 **于富文本编辑器(RTE)插件的对话框** ，如下所示：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此示例仅说明如何实现逻辑的客户端部分：然后，必须&#x200B;*[在服务器端显式地分析占位符(文本]*)（例如，在组件JSP中）。

### 树概述 {#tree-overview}

现成对象提供树结构 ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` 化数据的树结构化UI表示。 “使用ExtJS构件”包中包 **含的“树概述”组件显示如**`TreePanel` 何使用对象在给定路径下显示JCR树。 窗口本身可以停靠／取消停放。 在此示例中，窗口逻辑嵌入在&lt;script>&lt;/script>标签之间的组件jsp中。

要将树概 **述组件包含到示例页面** ，请执行以下操作：

1. 添加 **4。 将“概述** ”组件树结构化为 **Sidekick中“使用ExtJS构** 件”选项卡中的示例 **页面**。
1. 此时将显示组件：
   * 标题，带有一些文本
   * 属性 **链接** :单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 一个浮动窗口，其中包含存储库的树形表示，可展开。

组件显示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

树概述组件：

* 定义于：
   `/apps/extjstraining/components/treeoverview`

* 其对话框用于设置窗口的大小和停放／取消停放窗口（请参阅下面的详细信息）。

组件jsp:

* 从存储库中检索宽度、高度和停靠属性。
* 显示有关树概述数据格式的一些文本。
* 在javascript标记之间的组件jsp中嵌入窗口逻辑。
* 定义于：
   `apps/extjstraining/components/treeoverview/content.jsp`

嵌入到组件jsp中的javascript代码：

* 通过尝 `tree` 试从页面检索树窗口来定义对象。
* 如果显示树的窗口不存在， `treePanel` 则会[创建(CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` 包含用于创建窗口的数据。
   * 通过调用在以下位置注册的servlet检索数据：
      `/bin/wcm/siteadmin/tree.json`
* 监听 `beforeload` 器确保已加载单击的节点。
* 对 `root` 象将路径设 `apps/extjstraining` 置为树根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)根据预定义进行设置 `treePanel`，并显示如下：
   `tree.show();`
* 如果窗口已存在，则根据从存储库检索到的宽度、高度和停靠的属性显示该窗口。

组件对话框：

* 显示1个选项卡，其中2个字段用于设置树概述窗口的大小（宽度和高度）,1个字段用于停放／取消停放窗口
* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 该面板有一个大小字段构件(节点类型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)和一个选择构件(节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`)，带有2个选项(true/false)
* 由位于以下位置的对话框节点定义：
   `/apps/extjstraining/components/treeoverview/dialog`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 显示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 网格概述 {#grid-overview}

网格面板以行和列的表格格式表示数据。 它由以下几部分组成：

* 商店：保存数据记录的模型（行）。
* 列模型：专栏的组成。
* 查看：封装用户界面。
* 选择模型：选择行为。

“使用ExtJS构件”包中包 **含的“网格概述”组件** ，显示了如何以表格格式显示数据：

* 示例1使用静态数据。
* 示例2使用从存储库检索到的数据。

要将“网格概述”组件包含到示例页面，请执行以下操作：

1. 添加 **5。 网格概述** 、Sidekick中“使用ExtJS构件” **选项卡中示例页面的网** 格概述 ****。
1. 此时将显示组件：
   * 带有文本的标题
   * 属性 **链接** :单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 包含表格格式数据的浮动窗口。

组件显示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 示例1:默认网格 {#example-default-grid}

在开箱即用版本中，网格概述组件 **** 以表格格式显示一个包含静态数据的窗口。 在此示例中，该逻辑通过两种方式嵌入到组件jsp中：

* 通用逻辑在&lt;script>&lt;/script>标记之间定义
* 特定逻辑在单独的。js文件中可用，并在jsp中链接到。 通过对所需的&lt;script>标签进行注释，该设置可以在两个逻辑（静态／动态）之间轻松切换。

网格概述组件：

* 定义于：
   `/apps/extjstraining/components/gridoverview`
* 其对话框用于设置窗口的大小和停放／取消停放窗口。

组件jsp:

* 从存储库中检索宽度、高度和停靠属性。
* 显示一些文本作为网格概述数据格式的介绍。
* 引用定义GridPanel对象的javascript代码：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
   `defaultgrid.js` 将一些静态数据定义为GridPanel对象的基础。
* 在javascript标签之间嵌入javascript代码，该标签定义使用GridPanel对象的Window对象。
* 定义于：
   `apps/extjstraining/components/gridoverview/content.jsp`

嵌入到组件jsp中的javascript代码：

* 通过尝 `grid` 试从页面检索窗口组件来定义对象：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果 `grid` 不存在，则通过调用方 [法来定义CQ.Ext.grid.GridPanel对象(](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) )(请参阅 `gridPanel``getGridPanel()` 下文)。 此方法在中定义 `defaultgrid.js`。
* `grid` 是基于 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 预定义的GridPanel的对象，并且显示： `grid.show();`
* 如果 `grid` 已存在，则根据从存储库检索到的宽度、高度和停靠的属性显示该属性。

组件jsp中引用的javascript文件( `defaultgrid.js`)定义了由嵌入在JSP中的脚本调用的方法，并基于静态数据返回 `getGridPanel()`` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 一个对象。 逻辑如下：

* `myData` 是一组静态数据，格式为5列4行的表。
* `store` 是一个 `CQ.Ext.data.Store` 被消耗的对象 `myData`。
* `store` 加载到内存中：
   `store.load();`
* `gridPanel` 是一个 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，它使用 `store`:
   * 列宽随时会重新比例调整：
      `forceFit: true`
   * 一次只能选择一行：
      `singleSelect:true`

#### 示例2:引用搜索网格 {#example-reference-search-grid}

安装包时，网格概 `content.jsp` 述组 **** 件会显示基于静态数据的网格。 可以修改组件以显示具有以下特征的网格：

* 有三列。
* 基于通过调用servlet从存储库检索的数据。
* 可以编辑最后一列的单元格。 该值将保留在由第一列 `test` 中显示的路径定义的节点下的属性中。

如前面部分所述，窗口对象通过调 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 用文件中定义的方 `getGridPanel()` 法获取其 `defaultgrid.js` 对象，位 `/apps/extjstraining/components/gridoverview/defaultgrid.js`置 **网格概述**组件为方法提供了不同的实现， `getGridPanel()` 在文件中的 `referencesearch.js` 位置定义 `/apps/extjstraining/components/gridoverview/referencesearch.js`。 通过切换组件jsp中引用的。js文件，网格将基于从存储库检索的数据。

切换组件jsp中引用的。js文件：

1. 在 **CRXDE Lite中**，在组件的 `content.jsp` 文件中，注释包含该文件的 `defaultgrid.js` 行，使其如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 从包含文件的行中删除注 `referencesearch.js` 释，使其如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 保存更改。
1. 刷新示例页面。

组件显示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

组件jsp( `referencesearch.js`)中引用的javascript代码定义从组件jsp调用的方法，并根据从存储库动态检索到的数据返回 `getGridPanel()`` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 一个对象。 中的逻辑 `referencesearch.js` 将某些动态数据定义为GridPanel的基础：

* `reader` 是一个 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`对象，它为3列读取json格式的servlet响应。
* `cm` 是3 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 列的对象。
“测试”列单元格可以编辑，因为它们是使用编辑器定义的：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 列可以排序：
   `cm.defaultSortable = true;`
* `store` 是对 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 象：
   * 它通过调用注册在“ ”的servlet获取其数据， `/bin/querybuilder.json`并使用一些用于过滤查询的参数
   * 它基于， `reader`事先定义
   * 表按“**jcr:path**”列的升序排序
* `gridPanel` 是可 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 以编辑的对象：
   * 它基于预定义的列模 `store` 型和列模型 `cm`
   * 一次只能选择一行：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * 监 `afteredit` 听器确保在“**Test**”列中的单元格编辑后：
      * 在存储库中， `test`使用单元格的值设置“**jcr:path**”列所定义路径处节点的属性“”
      * 如果POST成功，则该值将添加到对象，否 `store` 则它将被拒绝
