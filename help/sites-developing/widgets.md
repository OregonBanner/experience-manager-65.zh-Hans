---
title: 使用和扩展小组件（经典UI）
seo-title: Using and Extending Widgets (Classic UI)
description: AEM基于Web的界面使用AJAX和其他现代浏览器技术，使作者能够直接在网页上编辑和格式化内容。
seo-description: AEM's web-based interface uses AJAX and other modern browser technologies to enable WYSIWYG editing and formatting of content by authors right on the web page
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4934'
ht-degree: 0%

---

# 使用和扩展小组件（经典UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本页介绍经典UI中小组件的用法，该小组件在AEM 6.4中已弃用。
>
>Adobe建议您利用现代 [触屏优化UI](/help/sites-developing/touch-ui-concepts.md) 基于 [Coral用户界面](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite用户界面](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

Adobe Experience Manager的基于web的界面使用AJAX和其他现代浏览器技术，使作者能够直接在网页上对内容进行WYSIWYG编辑和格式化。

Adobe Experience Manager(AEM)使用 [ExtJS](https://www.sencha.com/) 小组件库，它提供了经过高度优化的用户界面元素，这些元素可在所有最重要的浏览器中使用，并允许创建桌面级UI体验。

这些小组件包含在AEM中，除了供AEM本身使用外，还可供使用AEM构建的任何网站使用。

有关AEM中所有可用小组件的完整引用，您可以参阅 [小组件API文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) 或 [现有xtype列表](/help/sites-developing/xtypes.md). 此外，还提供了许多显示如何使用ExtJS框架的示例，这些示例位于 [森查](https://www.sencha.com/products/extjs/examples/) 站点，框架的所有者。

本页对如何使用和扩展小组件提供了一些分析。 它首先描述了如何 [在页面中包含客户端代码](#including-the-client-sided-code-in-a-page). 然后，该文档描述了为说明一些基本用法和扩展而创建的一些示例组件。 这些组件在 **使用ExtJS小组件** 软件包 **包共享**.

该包包含以下示例：

* [基本对话框](#basic-dialogs) 内置的开箱即用小组件。
* [动态对话框](#dynamic-dialogs) 内置开箱即用的小组件和自定义的javascript逻辑。
* 基于的对话 [自定义小组件](#custom-widgets).
* A [树面板](#tree-overview) 在给定路径下显示JCR树。
* A [网格面板](#grid-overview) 以表格格式显示数据。

>[!NOTE]
>
>Adobe Experience Manager的经典UI基于 [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## 在页面中包含客户端代码 {#including-the-client-sided-code-in-a-page}

客户端javascript和样式表代码应放置在客户端库中。

要创建客户端库，请执行以下操作：

1. 在下面创建节点 `/apps/<project>` 具有以下属性：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[混合：可锁定]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * 类别=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 下面 `clientlib` 创建 `css` 和 `js` 文件夹(nt:folder)。

1. 下面 `clientlib` 创建 `css.txt` 和 `js.txt` 文件(nt:files)。 这些.txt文件会列出库中包含的文件。

1. 编辑 `js.txt`:它需要以&#39;开头 `#base=js`“ ”后跟将由CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 编辑 `css.txt`:它需要以&#39;开头 `#base=css`“ ”后跟将由CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=css
    components.css
   ```

1. 在 `js` 文件夹中，放置属于库的javascript文件。

1. 在 `css` 文件夹，放置 `.css` 文件和css文件使用的资源(例如 `my_icon.png`)。

>[!NOTE]
>
>对之前描述的样式表的处理是可选的。

要在页面组件jsp中包含客户端库，请执行以下操作：

* 要同时包含javascript代码和样式表，请执行以下操作：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
where 
`<category-nameX>` 是客户端库的名称。

* 要仅包含javascript代码，请执行以下操作：
   `<ui:includeClientLib js="<category-name>"/>`

有关更多详细信息，请参阅 [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 标记。

在某些情况下，客户端库应仅在创作模式下可用，而应在发布模式下排除。 具体实现如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 示例入门 {#getting-started-with-the-samples}

要按照本页上的教程操作，请安装名为 **使用ExtJS小组件** 在本地AEM实例中，并创建一个将包含组件的示例页面。 为此，请执行以下操作：

1. 在AEM实例中，下载名为 **使用ExtJS小组件(v01)** 从包共享中，安装包。 它会创建项目 `extjstraining` 下面 `/apps` 中。
1. 将包含脚本(js)和样式表(css)的客户端库包含到geometrixx页jsp的head标记中，因为您将示例组件包含在 **Geometrixx** 分支：in **CRXDE Lite** 打开文件 `/apps/geometrixx/components/page/headlibs.jsp` 并添加 `cq.extjstraining` 类别 `<ui:includeClientLib>` 标记如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在 **Geometrixx** 下方 `/content/geometrixx/en/products` 并称之为 **使用ExtJS小组件**.
1. 进入设计模式，并添加组中名为 **使用ExtJS小组件** Geometrixx设计
1. 在编辑模式下返回：组的组件 **使用ExtJS小组件** 可在Sidekick中使用。

>[!NOTE]
>
>本页面上的示例基于Geometrixx示例内容，该内容不再随AEM一起提供，而已被We.Retail替换。 查看文档 [We.Retail参考实施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 以了解如何下载和安装Geometrixx。

### 基本对话框 {#basic-dialogs}

对话框通常用于编辑内容，但也只能显示信息。 查看完整对话框的一种简单方法是访问其json格式的表示形式。 为此，请将您的浏览器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

的 **使用ExtJS小组件** 在Sidekick中的组被调用 **1. 对话框基础知识** 以及包含四个基本对话框，这些对话框是使用现成的小组件构建的，并且不使用自定义的javascript逻辑。 对话框存储在下面 `/apps/extjstraining/components/dialogbasics`. 基本对话框包括：

* 完整对话框( `full` 节点):它显示一个窗口，其中包含3个选项卡，每个选项卡都包含2个文本字段。
* 单个面板对话框( `singlepanel` 节点):它显示一个窗口，其中带有1个选项卡，其中具有2个文本字段。
* 多面板对话框( `multipanel` 节点):其显示方式与“完整”对话框相同，只是构建方式不同。
* 设计对话框( `design` 节点):此时将显示一个带有2个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集，其中包含4个文本字段，以及一个可折叠的字段集，其中包含2个文本字段。

包括 **1. 对话框基础知识** 组件：

1. 添加 **1. 对话框基础知识** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 该组件显示标题、部分文本和 **属性** 链接：单击链接以显示存储库中所存储段落的属性。 再次单击链接以隐藏属性。

组件显示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 示例1:完整对话框 {#example-full-dialog}

的 **完整** 对话框显示一个窗口，其中包含三个选项卡，每个选项卡都包含两个文本字段。 它是 **对话框基础知识** 组件。 其特点是：

* 由节点定义：节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* 显示3个选项卡(节点类型= `cq:Panel`)。
* 每个选项卡都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/full`
* 通过请求以下项以JSON格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

该对话框显示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 示例2:单面板对话框 {#example-single-panel-dialog}

的 **单个面板** 对话框显示一个窗口，其中有一个选项卡具有两个文本字段。 其特点是：

* 显示1个选项卡(节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* 选项卡具有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 比 **完整对话框** 需要的配置较少。
* 建议使用：用于显示信息或仅具有几个字段的简单对话框。

要使用单个面板对话框，请执行以下操作：

1. 替换 **对话框基础知识** 组件 **单个面板** 对话框：
   1. 在 **CRXDE Lite**，删除节点： `/apps/extjstraining/components/dialogbasics/dialog`
   1. 单击 **全部保存** 以保存更改。
   1. 复制节点： `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 将复制的节点粘贴到下面： `/apps/extjstraining/components/dialogbasics`
   1. 选择节点： `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`并重命名 `dialog`.
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 示例3:多面板对话框 {#example-multi-panel-dialog}

的 **多面板** 对话框的显示与 **完整** 对话，但是它是以不同的方式构建的。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)。
* 显示3个选项卡(节点类型= `cq:Panel`)。
* 每个选项卡都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 比 **完整对话框** 就是它的结构简化了。
* 建议使用：的子菜单。

要使用多面板对话框，请执行以下操作：

1. 替换 **对话框基础知识** 组件 **多面板** 对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 示例4:富对话框 {#example-rich-dialog}

的 **富** 对话框显示一个带有两个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集，其中包含四个文本字段，而一个可折叠的字段集中包含两个文本字段。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示2个选项卡(节点类型= `cq:Panel`)。
* 第一个选项卡具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 小组件 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 和 ` [selection](/help/sites-developing/xtypes.md#selection)` 具有3个选项的小组件，以及可折叠的 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 带有 ` [textarea](/help/sites-developing/xtypes.md#textarea)` 小组件。
* 第二个选项卡具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 带4的小组件 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 小部件和可折叠的 `dialogfieldset` 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 小组件。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/rich`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

使用 **富** 对话框：

1. 替换 **对话框基础知识** 组件 **富** 对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 动态对话框 {#dynamic-dialogs}

的第二个组件 **使用ExtJS小组件** 在Sidekick中的组被调用 **2. 动态对话框** 和包含三个使用现成小组件构建的动态对话框，以及 **使用自定义javascript逻辑**. 对话框存储在下面 `/apps/extjstraining/components/dynamicdialogs`. 动态对话框包括：

* 切换选项卡对话框( `switchtabs` 节点):此时将显示一个带有两个选项卡的窗口。 第一个选项卡具有一个单选按钮选项，其中包含三个选项：选择某个选项后，会显示与该选项相关的选项卡。 第二个选项卡有两个文本字段。
* 任意对话框( `arbitrary` 节点):此时会显示一个带有一个选项卡的窗口。 选项卡中有一个用于放置或上传资产的字段，以及一个字段，用于显示有关容器页面以及资产（如果引用了）的一些信息。
* 切换字段对话框( `togglefield` 节点):此时会显示一个带有一个选项卡的窗口。 选项卡中有一个复选框：选中此选项后，将显示一个字段集，其中包含两个文本字段。

要包含 **2. 动态对话框** 组件：

1. 添加 **2. 动态对话框** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 该组件显示标题、部分文本和 **属性** 链接：单击以显示存储库中所存储段落的属性。 再次单击可隐藏属性。

组件显示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 示例1:“切换选项卡”对话框 {#example-switch-tabs-dialog}

的 **切换选项卡** 对话框显示一个带有两个选项卡的窗口。 第一个选项卡具有一个单选按钮选项，其中包含三个选项：选择某个选项后，会显示与该选项相关的选项卡。 第二个选项卡有两个文本字段。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示2个选项卡(节点类型= `cq:Panel`):1选项卡，则第2个选项卡取决于第1个选项卡（3个选项）中的选择。
* 具有3个可选选项卡(节点类型= `cq:Panel`)，则每个文本字段都有2个文本字段(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。 一次只显示一个可选选项卡。
* 由 `switchtabs` 节点：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

该逻辑通过事件侦听器和Javascript代码实现，如下所示：

* 对话框节点具有“ `beforeshow`“监听程序，在显示对话框之前隐藏所有可选选项卡：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 获取包含选择面板和3个可选面板的表面板。
* 的 `Ejst.x2` 对象在 `exercises.js` 文件：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.manageTabs()` 方法，作为的值 `index` 为–1时，隐藏所有可选选项卡（从1到3）。
* “选择”选项卡具有2个侦听器：一个用于在加载对话框时显示所选选项卡(&quot; `loadcontent`“事件”)，以及在更改选择时显示选定选项卡(“ `selectionchanged`“事件):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在 `Ejst.x2.showTab()` 方法：
   `field.findParentByType('tabpanel')` 获取包含所有选项卡( `field` 表示选择小组件)
   `field.getValue()` 获取选择的值，例如：tab2
   `Ejst.x2.manageTabs()` 显示选定的选项卡。
* 每个可选选项卡都有一个侦听器，用于隐藏“ `render`&quot;事件：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在 `Ejst.x2.hideTab()` 方法：
   `tabPanel` 是包含所有选项卡的选项卡面板
   `index` 是可选选项卡的索引
   `tabPanel.hideTabStripItem(index)` 隐藏选项卡

其显示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 示例2:任意对话 {#example-arbitrary-dialog}

通常，对话框会显示基础组件中的内容。 此处描述的对话框名为 **任意** 对话框中，从其他组件中提取内容。

的 **任意** 对话框显示一个带有一个选项卡的窗口。 选项卡包含两个字段：一个用于放置或上传资产，另一个用于显示有关容器页面以及资产（如果已引用）的一些信息。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个表格面板小组件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)，带有1个面板(节点类型= `cq:Panel`)
* 面板具有智能文件小组件(节点类型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)和ownerdraw小组件(节点类型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* 由 `arbitrary` 节点：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

该逻辑通过事件侦听器和Javascript代码实现，如下所示：

* ownerdraw小组件具有“ `loadcontent`&quot;侦听器，用于显示加载内容时包含组件的页面和智能文件小组件引用的资产的相关信息：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` 使用ownerdraw对象进行设置
   `path` 使用组件的内容路径进行设置(例如：/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* 的 `Ejst.x2` 对象在 `exercises.js` 文件：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.showInfo()` 方法：
   `pagePath` 是包含组件的页面路径
   `pageInfo` 表示json格式的页面属性
   `reference` 是引用资产的路径
   `metadata` 以json格式表示资产的元数据
   `ownerdraw.getEl().update(html);` 在对话框中显示已创建的html

使用 **任意** 对话框：

1. 替换 **动态对话框** 组件 **任意** 对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 示例3:切换字段对话框 {#example-toggle-fields-dialog}

的 **切换字段** 对话框显示一个带有一个选项卡的窗口。 选项卡中有一个复选框：选中此选项后，将显示一个字段集，其中包含两个文本字段。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个表格面板小组件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`)，带有1个面板(节点类型= `cq:Panel`)。
* 该面板具有一个选择/复选框小组件(节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，类型= ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`)和可折叠的对话框字段集小组件(节点类型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`)，默认隐藏2个文本字段小组件(节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由 `togglefields` 节点：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

该逻辑通过事件侦听器和Javascript代码实现，如下所示：

* “选择”选项卡有2个侦听器：其中一个用于显示加载内容时对话框字段集(&quot; `loadcontent`“ event”和一个用于在更改选择时显示对话框字段集(“ `selectionchanged`“事件):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* 的 `Ejst.x2` 对象在 `exercises.js` 文件：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.toggleFieldSet()` 方法：
   `box` 是选择对象
   `panel` 是包含所选内容和对话框字段集小组件的面板
   `fieldSet` 是dialogfieldset对象
   `show` 是基于“ `show`“对话框字段集是否显示

使用 **切换字段** 对话框：

1. 替换 **动态对话框** 组件 **切换字段** 对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自定义小组件 {#custom-widgets}

AEM附带的现成小组件应涵盖大多数用例。 但是，有时可能需要创建自定义小组件以满足特定于项目的要求。 可通过扩展现有小组件来创建自定义小组件。 为帮助您开始进行此类自定义， **使用ExtJS小组件** 包包含三个使用三个不同自定义小组件的对话框：

* 多字段对话框( `multifield` 节点)显示一个带有一个选项卡的窗口。 选项卡具有一个自定义的多字段小组件，该小组件具有两个字段：包含两个选项和一个文本字段的下拉菜单。 因为它基于现成的 `multifield` 小组件（仅具有文本字段），具有 `multifield` 小组件。
* 树浏览对话框( `treebrowse` 节点)显示一个窗口，其中包含一个包含路径浏览小组件的选项卡：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 项目的路径随后会添加到路径字段，并在对话框关闭时持久保留该路径。
* 基于富文本编辑器插件的对话框( `rteplugin` 节点)来向富文本编辑器添加自定义按钮，以向主文本插入一些自定义文本。 它由 `richtext` 构件(RTE)和自定义功能（通过RTE插件机制添加）的集成。

自定义小组件和插件将包含在名为 **3. 自定义小组件** 的 **使用ExtJS小组件** 包。 要将此组件包含到示例页面，请执行以下操作：

1. 添加 **3. 自定义小组件** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 该组件会显示标题和一些文本，在单击 **属性** 链接，存储库中所存储段落的属性。 再次单击会隐藏属性。
组件显示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 示例1:自定义多字段小组件 {#example-custom-multifield-widget}

的 **自定义多字段** 基于小组件的对话框显示一个带有一个选项卡的窗口。 选项卡具有一个自定义的多字段小组件，该小组件与具有一个字段的标准小组件不同，具有两个字段：包含两个选项和一个文本字段的下拉菜单。

的 **自定义多字段** 基于小组件的对话框：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个表格面板小组件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 该面板具有 `multifield` 小组件（节点类型） `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`)。
* 的 `multifield` 小组件具有字段配置(节点类型= `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`)，基于自定义xtype ` `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39;是 ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` 对象。
   * &#39; `optionsProvider`&#39;是 `ejstcustom` 小组件。 它通过 `Ejst.x3.provideOptions` 方法（在中定义） `exercises.js` at:
      `/apps/extjstraining/clientlib/js/exercises.js`
和返回2个选项。
* 由 `multifield` 节点：
   `/apps/extjstraining/components/customwidgets/multifield`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自定义多字段小组件(xtype = `ejstcustom`):

* 是名为的Javascript对象 `Ejst.CustomWidget`.
* 在 `CustomWidget.js` javascript文件：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 扩展 ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` 小组件。
* 具有3个字段： `hiddenField` （文本字段）、 `allowField` （组合框）和 `otherField` （文本字段）
* 覆盖 `CQ.Ext.Component#initComponent` 要添加3个字段，请执行以下操作：
   * `allowField` 是 [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) “select”类型的对象。 optionsProvider是Selection对象的配置，该对象是使用对话框中定义的CustomWidget的optionsProvider配置进行实例化的
   * `otherField` 是 [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 对象
* 覆盖方法 `setValue`, `getValue` 和 `getRawValue` of [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) 要使用以下格式设置和检索CustomWidget的值，请执行以下操作：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`。
* 将自身注册为“ `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

的 **自定义多字段** 基于小组件的对话框如下所示：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 示例2:自定义树状浏览小组件 {#example-custom-treebrowse-widget}

自定义 **树状浏览** 基于小组件的对话框显示一个窗口，其中包含一个包含自定义路径浏览小组件的选项卡：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 项目的路径随后会添加到路径字段，并在对话框关闭时持久保留该路径。

自定义树状浏览对话框：

* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示1个表格面板小组件(节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有自定义小组件(节点类型= `cq:Widget`, xtype = `ejstbrowse`)
* 由 `treebrowse` 节点：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自定义树状浏览小组件(xtype = `ejstbrowse`):

* 是名为的Javascript对象 `Ejst.CustomWidget`.
* 在 `CustomBrowseField.js` javascript文件：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 扩展 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* 定义一个名为 `browseWindow`.
* 覆盖 ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` 以在单击箭头时显示浏览窗口。
* 定义 [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) 对象：
   * 它通过调用在注册的Servlet来获取其数据 `/bin/wcm/siteadmin/tree.json`.
   * 其根为“ `apps/extjstraining`&quot;
* 定义 `window` 对象( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 基于预定义的面板。
   * 具有 **确定** 按钮来隐藏选定路径的值。
* 窗口在 **路径** 字段。
* 所选路径将从浏览字段传递到 `show` 事件。
* 将自身注册为“ `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

使用 **自定义树状浏览** 基于小组件的对话框：

1. 替换 **自定义小组件** 组件 **自定义树状浏览** 对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 示例3:富文本编辑器(RTE)插件 {#example-rich-text-editor-rte-plug-in}

的 **富文本编辑器(RTE)插件** “基于”对话框是基于富文本编辑器的对话框，具有一个自定义按钮，用于在方括号内插入一些自定义文本。 自定义文本可以由某些服务器端逻辑解析（本示例中未实现），例如，添加在给定路径中定义的一些文本：

的 **RTE插件** 基于对话框：

* 由rtplugin节点在以下位置定义：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* 的 `rtePlugins` 节点具有子节点 `inserttext` (节点类型= `nt:unstructured`)以插件命名。 它有一个名为 `features`，用于定义RTE可用的插件功能。

RTE插件：

* 是名为的Javascript对象 `Ejst.InsertTextPlugin`.
* 在 `InsertTextPlugin.js` javascript文件：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 扩展 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 对象。
* 以下方法定义 ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 对象，并在实施插件中被覆盖：
   * `getFeatures()` 返回该插件可用的所有功能的数组。
   * `initializeUI()` 将新按钮添加到RTE工具栏。
   * `notifyPluginConfig()` 在按钮悬停时显示标题和文本。
   * `execute()` 单击按钮并执行插件操作时，将调用：它会显示一个窗口，用于定义要包含的文本。
* `insertText()` 使用相应的对话框对象插入文本 `Ejst.InsertTextPlugin.Dialog` （请参阅之后）。
* `executeInsertText()` 由 `apply()` 对话框的方法，在 **确定** 按钮。
* 将自身注册为“ `inserttext`&#39;插件：
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* the `Ejst.InsertTextPlugin.Dialog` 对象定义在单击插件按钮时打开的对话框。 该对话框由面板、表单、文本字段和2个按钮(**确定** 和 **取消**)。

使用 **富文本编辑器(RTE)插件** 基于对话框：

1. 替换 **自定义小组件** 组件 **富文本编辑器(RTE)插件** 基于对话框：按照 [示例2:单面板对话框](#example-single-panel-dialog)
1. 编辑组件。
1. 单击右侧的最后一个图标（带四个箭头的图标）。 输入路径并单击 **确定**:路径显示在方括号内([ ]）。
1. 单击 **确定** 以关闭富文本编辑器。

的 **富文本编辑器(RTE)插件** 基于对话框显示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此示例仅显示如何实施逻辑的客户端部分：占位符(*[文本]*)，则必须在服务器端进行显式解析（例如，在组件JSP中）。

### 树概述 {#tree-overview}

开箱即用 ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` 对象提供树结构化数据的树结构化用户界面表示。 包含在 **使用ExtJS小组件** 包中显示了如何使用 `TreePanel` 对象，以在给定路径下显示JCR树。 窗口本身可以停靠/取消停靠。 在本例中，窗口逻辑嵌入到组件jsp中， &lt;script>&lt;/script> 标记。

要包含 **树概述** 组件添加到示例页面：

1. 添加 **4. 树概述** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 组件会显示：
   * 带有文本的标题
   * a **属性** 链接：单击以显示存储库中所存储段落的属性。 再次单击可隐藏属性。
   * 可展开的具有存储库树表示的浮动窗口。

组件显示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

树概述组件：

* 定义于：
   `/apps/extjstraining/components/treeoverview`

* 其对话框允许设置窗口大小和停靠/取消停靠窗口（请参阅下面的详细信息）。

组件jsp:

* 从存储库中检索宽度、高度和停靠属性。
* 显示有关树概述数据格式的一些文本。
* 在javascript标记之间的组件jsp中嵌入窗口逻辑。
* 定义于：
   `apps/extjstraining/components/treeoverview/content.jsp`

组件jsp中嵌入的Javascript代码：

* 定义 `tree` 对象。
* 如果显示树的窗口不存在， `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` 包含用于创建窗口的数据。
   * 通过调用在以下位置注册的Servlet来检索数据：
      `/bin/wcm/siteadmin/tree.json`
* 的 `beforeload` 侦听器确保加载了点击的节点。
* 的 `root` 对象设置路径 `apps/extjstraining` 作为树根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)，则会根据预定义的 `treePanel`，且显示为：
   `tree.show();`
* 如果窗口已存在，则会根据从存储库检索的宽度、高度和停靠属性来显示该窗口。

组件对话框：

* 显示1个选项卡，其中包含2个字段用于设置树概述窗口的大小（宽度和高度），1个字段用于停放/取消停放窗口
* 由节点定义(节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 该面板具有一个大小字段小组件(节点类型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)和选择小组件(节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，类型= `radio`)，其中包含2个选项(true/false)
* 由对话框节点在以下位置定义：
   `/apps/extjstraining/components/treeoverview/dialog`
* 通过请求以下项以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 显示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 网格概述 {#grid-overview}

网格面板以行和列的表格格式表示数据。 它由以下内容组成：

* 存储：保存数据记录（行）的模型。
* 列模型：专栏的构成。
* 查看：封装用户界面。
* 选择模型：选择行为。

中包含的网格概述组件 **使用ExtJS小组件** 包显示了如何以表格格式显示数据：

* 示例1使用静态数据。
* 示例2使用从存储库检索到的数据。

要将网格概述组件包含到示例页面，请执行以下操作：

1. 添加 **5. 网格概述** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 组件会显示：
   * 带有文本的标题
   * a **属性** 链接：单击以显示存储库中所存储段落的属性。 再次单击可隐藏属性。
   * 包含表格格式的数据的浮动窗口。

组件显示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 示例1:默认网格 {#example-default-grid}

在其现成版本中， **网格概述** 组件以表格格式显示一个包含静态数据的窗口。 在本例中，逻辑以两种方式嵌入到组件jsp中：

* 在 &lt;script>&lt;/script> 标记
* 特定逻辑在单独的.js文件中可用，并在jsp中链接到。 This setup enables to easily switch between the two logic (static/dynamic) by commenting the desired &lt;script> tags.

网格概述组件：

* 定义于：
   `/apps/extjstraining/components/gridoverview`
* 其对话框用于设置窗口的大小和停靠/取消停靠窗口。

组件jsp:

* 从存储库中检索宽度、高度和停靠属性。
* 显示一些文本作为网格概述数据格式的简介。
* 引用定义GridPanel对象的Javascript代码：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` 将一些静态数据定义为GridPanel对象的基。
* 在可定义使用GridPanel对象的Window对象的Javascript标记之间嵌入Javascript代码。
* 定义于：
   `apps/extjstraining/components/gridoverview/content.jsp`

组件jsp中嵌入的Javascript代码：

* 定义 `grid` 对象，方法是尝试从页面中检索窗口组件：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果 `grid` 不存在， [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 对象( `gridPanel`) `getGridPanel()` 方法（请参阅下文）。 此方法在 `defaultgrid.js`.
* `grid` 是 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 对象，基于预定义的GridPanel并显示： `grid.show();`
* 如果 `grid` 已存在，则会根据从存储库检索的宽度、高度和停靠属性来显示该属性。

Javascript文件( `defaultgrid.js`)在组件jsp中引用定义 `getGridPanel()` 方法，该方法由嵌入在JSP中的脚本调用并返回 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，基于静态数据。 逻辑如下：

* `myData` 是静态数据数组，格式为包含5列和4行的表。
* `store` 是 `CQ.Ext.data.Store` 使用的对象 `myData`.
* `store` 在内存中加载：
   `store.load();`
* `gridPanel` 是 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 使用的对象 `store`:
   * 列宽随时会进行重新比例：
      `forceFit: true`
   * 一次只能选择一行：
      `singleSelect:true`

#### 示例2:引用搜索网格 {#example-reference-search-grid}

安装包时， `content.jsp` 的 **网格概述** 组件显示基于静态数据的网格。 可以修改组件以显示具有以下特征的网格：

* 有三列。
* 基于通过调用Servlet从存储库检索到的数据。
* 可以编辑最后一列的单元格。 该值将保留在 `test` 属性。

如前面部分所述，窗口对象将获取其 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象 `getGridPanel()` 方法 `defaultgrid.js` 文件位置 `/apps/extjstraining/components/gridoverview/defaultgrid.js`. **网格概述**组件为 `getGridPanel()` 方法，在中定义 `referencesearch.js` 文件位置 `/apps/extjstraining/components/gridoverview/referencesearch.js`. 通过切换组件jsp中引用的.js文件，网格将基于从存储库检索到的数据。

切换组件jsp中引用的.js文件：

1. 在 **CRXDE Lite**，在 `content.jsp` 文件中，注释包含 `defaultgrid.js` 文件，因此其外观如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 从包含 `referencesearch.js` 文件，因此其外观如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 保存更改。
1. 刷新示例页面。

组件显示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

组件jsp中引用的Javascript代码( `referencesearch.js`)定义 `getGridPanel()` 从组件jsp调用的方法并返回 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，基于从存储库动态检索的数据。 中的逻辑 `referencesearch.js` 将一些动态数据定义为GridPanel的基础：

* `reader` 是 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`用于为3列读取json格式的servlet响应的对象。
* `cm` 是 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 对象。
可以编辑“测试”列单元格，因为这些单元格是通过编辑器定义的：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 可对列进行排序：
   `cm.defaultSortable = true;`
* `store` 是 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 对象：
   * 它通过调用在“ ”注册的servlet来获取其数据 `/bin/querybuilder.json`”，其中包含一些用于筛选查询的参数
   * 基于 `reader`，事先定义
   * 表按照&#x200B;**jcr:path**“ ”列的升序
* `gridPanel` 是 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 可编辑的对象：
   * 它基于预定义的 `store` 和列模型 `cm`
   * 一次只能选择一行：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * the `afteredit` 侦听器确保在“**测试**“ ”列已编辑：
      * 属性&#39; `test`“”所定义路径上节点的“ ”**jcr:path**“ ”列在存储库中设置，其值为单元格
      * 如果POST成功，则会将值添加到 `store` 对象，否则将被拒绝
