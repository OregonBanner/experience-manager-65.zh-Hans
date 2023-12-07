---
title: 使用和扩展小组件（经典UI）
description: Adobe Experience Manager基于Web的界面使用AJAX和其他现代浏览器技术，让作者能够在网页上对WYSIWYG内容进行编辑和格式化
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# 使用和扩展小组件（经典UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本页介绍经典UI中构件的使用，AEM 6.4已弃用该构件。
>
>Adobe建议您使用 [触屏优化UI](/help/sites-developing/touch-ui-concepts.md) 基于 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

Adobe Experience Manager (AEM)基于Web的界面使用AJAX和其他现代浏览器技术，支持作者在网页上通过WYSIWYG编辑和格式化内容。

AEM使用 [ExtJS](https://www.sencha.com/) widgets库提供了经过高度完善的用户界面元素，这些元素可在所有最重要的浏览器中使用，并允许创建桌面级的UI体验。

这些构件包含在AEM中，除了AEM本身的使用之外，还可以由使用AEM构建的任何网站使用。

有关AEM中所有可用小组件的完整参考，请参见 [构件API文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 或 [现有xtype的列表](/help/sites-developing/xtypes.md). 此外，上提供了许多说明如何使用ExtJS框架的示例 [森查](https://examples.sencha.com/extjs/7.6.0/) 站点的所有者。

本页提供了有关如何使用和扩展构件的某些见解。 它首先介绍如何 [在页面中包含客户端代码](#including-the-client-sided-code-in-a-page). 然后，它描述了一些已创建的示例组件，以说明一些基本用法和扩展。 这些组件在以下位置提供： **使用ExtJS小组件** 打包 **包共享**.

此包中包含以下示例：

* [基本对话框](#basic-dialogs) 使用开箱即用的小组件构建。
* [动态对话框](#dynamic-dialogs) 使用开箱即用的小部件和自定义的JavaScript逻辑构建。
* 对话框基于 [自定义构件](#custom-widgets).
* A [树面板](#tree-overview) 在给定路径下显示JCR树。
* A [网格面板](#grid-overview) 以表格格式显示数据。

>[!NOTE]
>
>Adobe Experience Manager的经典用户界面构建于 [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## 在页面中包含客户端代码 {#including-the-client-sided-code-in-a-page}

客户端的JavaScript和样式表代码应放置在客户端库中。

要创建客户端库，请执行以下操作：

1. 在下创建节点 `/apps/<project>` 具有以下属性：

   * name=&quot;clientlib&quot;
   * jcr：mixinTypes=&quot;[mix：lockable]&quot;
   * jcr：primaryType=&quot;cq：ClientLibraryFolder&quot;
   * sling：resourceType=&quot;widgets/clientlib&quot;
   * 类别=&quot;[&lt;category-name>]&quot;
   * 依赖项=&quot;[cq.widget]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. 以下 `clientlib` 创建 `css` 和 `js` 文件夹(nt：folder)。

1. 以下 `clientlib` 创建 `css.txt` 和 `js.txt` 文件(nt：files)。 这些.txt文件列出库中包含的文件。

1. 编辑 `js.txt`：必须以&#39;开头 `#base=js`&#39;后跟CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 编辑 `css.txt`：必须以&#39;开头 `#base=css`&#39;后跟CQ客户端库服务聚合的文件列表，例如：

   ```
   #base=css
    components.css
   ```

1. 在 `js` 文件夹中，放置属于库的JavaScript文件。

1. 在 `css` 文件夹，放置 `.css` css文件使用的文件和资源(例如， `my_icon.png`)。

>[!NOTE]
>
>之前描述的样式表的处理是可选的。

要在页面组件jsp中包含客户端库，请执行以下操作：

* 要同时包含JavaScript代码和样式表，请执行以下操作：
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
位置 `<category-nameX>` 是客户端库的名称。

* 要仅包含JavaScript代码，请执行以下操作：
  `<ui:includeClientLib js="<category-name>"/>`

有关详细信息，请参阅标记的描述 [ &lt;ui:includeClientLib> ](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 。&lt;/ui:includeClientLib>

有时，客户 Libraries 应当仅在作者模式下可用，且应在发布模式下排除。 可以按如下方式实现：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 快速入门示例 {#getting-started-with-the-samples}

要遵循此页面上的教程，请安装包 **使用ExtJS小组件** 在本地AEM实例中创建，并创建一个包含组件的示例页面。 为此，请执行以下操作：

1. 在AEM实例中，下载名为的包 **使用ExtJS小组件(v01)** 从包共享中，安装包。 它会创建项目 `extjstraining` 以下 `/apps` 在存储库中。
1. 将包含脚本(js)和样式表(css)的客户端库包含在Geometrixx页jsp的head标记中。 您要将示例组件包含在 **Geometrixx** 分支：在 **CRXDE Lite** 打开文件 `/apps/geometrixx/components/page/headlibs.jsp` 并添加 `cq.extjstraining` 类别到现有 `<ui:includeClientLib>` 标记如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在中创建页面 **Geometrixx** 分支如下 `/content/geometrixx/en/products` 并称其为 **使用ExtJS小组件**.
1. 进入设计模式，添加名为的组的所有组件 **使用ExtJS小组件** 到Geometrixx的设计
1. 返回编辑模式：组的组件 **使用ExtJS小组件** 在Sidekick中可用。

>[!NOTE]
>
>此页面上的示例基于Geometrixx示例内容，该内容不再随AEM一起提供，已被We.Retail取代。 请参阅 [We.Retail参考实施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 了解如何下载和安装Geometrixx。

### 基本对话框 {#basic-dialogs}

对话框通常用于编辑内容，但也可以显示信息。 查看完整对话框的一个简单方法是以json格式访问其表示形式。 为此，请将浏览器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

第一个组件 **使用ExtJS小组件** Sidekick中的组名为 **1. Dialogue基础** 并且包含四个使用现成小组件构建的基本对话框，这些对话框无需自定义JavaScript逻辑。 对话框存储在下方 `/apps/extjstraining/components/dialogbasics`. 基本对话框包括：

* 完整对话框( `full` 节点)：显示一个窗口，其中包含三个选项卡，每个选项卡都有两个文本字段。
* 单面板对话框( `singlepanel` 节点)：显示一个带有两个文本字段的选项卡的窗口。
* 多面板对话框( `multipanel` 节点)：其显示与“完整”对话框相同，但构建方式不同。
* “设计”对话框( `design` 节点)：显示一个带有两个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠文本区域。 第二个选项卡有一个包含四个文本字段的字段集和一个包含两个文本字段的可折叠字段集。

包括 **1. Dialogue基础** 示例页面中的组件：

1. 添加 **1. Dialogue基础** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 组件显示标题、某些文本和 **属性** 链接。 选择该链接将显示存储在存储库中的段落的属性。 再次选择链接可隐藏属性。

该组件显示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 示例1：完整对话框 {#example-full-dialog}

此 **完整** 对话框显示一个窗口，其中带有三个制表符，每个制表符都有两个文本字段。 这是 **Dialogue基础** 组件。 其特点是：

* 由节点定义：节点类型= `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* 显示三个选项卡(节点类型= `cq:Panel`)。
* 每个选项卡都有两个文本字段(节点类型= `cq:Widget`， xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。
* 由节点定义：
  `/apps/extjstraining/components/dialogbasics/full`
* 通过请求以JSON格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

该对话框显示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 示例2：单面板对话框 {#example-single-panel-dialog}

此 **单个面板** 对话框显示一个窗口，其中有一个选项卡具有两个文本字段。 其特点是：

* 显示一个选项卡(节点类型= `cq:Dialog`， xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* 选项卡有两个文本字段(节点类型= `cq:Widget`， xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* 由节点定义：
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 比以下产品具有一项优势 **完整对话框** 就是只需要较少的配置。
* 建议使用：用于显示信息或只有几个字段的简单对话框。

要使用单面板对话框，请执行以下操作：

1. 替换对话框 **Dialogue基础** 包含的组件 **单个面板** 对话框：
   1. 在 **CRXDE Lite**，删除节点： `/apps/extjstraining/components/dialogbasics/dialog`
   1. 单击 **全部保存** 以保存更改。
   1. 复制节点： `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 将复制的节点粘贴到下方： `/apps/extjstraining/components/dialogbasics`
   1. 选择节点： `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`并为其重命名 `dialog`.
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 示例3：多面板对话框 {#example-multi-panel-dialog}

此 **多面板** 对话框的显示方式与 **完整** 对话框，但构建方式有所不同。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)。
* 显示三个选项卡（节点 type = `cq:Panel` ）。
* 每个选项卡有两个 textfields （节点 type = `cq:Widget` ，xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)` ）。
* 由节点定义：
  `/apps/extjstraining/components/dialogbasics/multipanel`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 比以下产品具有一项优势 **完整对话框** 就是它有一个简化的结构。
* 建议使用：用于多选项卡对话框。

要使用“多面板”对话框，请执行以下操作：

1. 替换对话框 **Dialogue基础** 包含的组件 **多面板** 对话框：请按照中所述的步骤进行操作。 [示例2：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 示例4：富对话框 {#example-rich-dialog}

此 **富有** 对话框显示一个带有两个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠文本区域。 第二个选项卡有一个包含四个文本字段的字段集和一个包含两个文本字段的可折叠字段集。 其特点是：

* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示两个选项卡(节点类型= `cq:Panel`)。
* 第一个选项卡具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 带有构件 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 和 ` [selection](/help/sites-developing/xtypes.md#selection)` 包含三个选项和一个可折叠的构件 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 带有 ` [textarea](/help/sites-developing/xtypes.md#textarea)` 构件。
* 第二个标签具有 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 包含四个构件 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 构件和可折叠 `dialogfieldset` 具有两个 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 构件。
* 由节点定义：
  `/apps/extjstraining/components/dialogbasics/rich`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

要使用 **富有** 对话框：

1. 替换对话框 **Dialogue基础** 包含的组件 **富有** 对话框：请按照中所述的步骤进行操作。 [示例2：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 动态对话框 {#dynamic-dialogs}

的第二个组件 **使用ExtJS小组件** Sidekick中的组名为 **2. 动态对话框** 并包含三个使用现成构件和构建的动态对话框 **使用自定义的JavaScript逻辑**. 对话框存储在下方 `/apps/extjstraining/components/dynamicdialogs`. 动态对话框包括：

* “切换选项卡”对话框( `switchtabs` 节点)：显示一个带有两个选项卡的窗口。 第一个选项卡具有一个带有三个选项的单选选项：当选中某个选项时，将显示与该选项相关的选项卡。 第二个选项卡有两个文本字段。
* “任意”对话框( `arbitrary` 节点)：显示带有一个选项卡的窗口。 选项卡中有一个字段用于放置或上传资产，还有一个字段用于显示有关容器页面以及资产（如果引用）的一些信息。
* 切换字段对话框( `togglefield` 节点)：显示带有一个选项卡的窗口。 该选项卡具有一个复选框：选中时，将显示一个字段集，其中包含两个文本字段。

要包含 **2. 动态对话框** 示例页面上的组件：

1. 添加 **2. 动态对话框** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 组件显示标题、某些文本和 **属性** 链接。 选择该链接将显示存储在存储库中的段落的属性。 再次选择链接可隐藏属性。

该组件显示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 示例1：切换选项卡对话框 {#example-switch-tabs-dialog}

此 **切换选项卡** 对话框显示一个带有两个选项卡的窗口。 第一个选项卡具有一个带有三个选项的单选选项：当选中某个选项时，将显示与该选项相关的选项卡。 第二个选项卡有两个文本字段。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示两个选项卡(节点类型= `cq:Panel`)：一个选择选项卡，第二个选项卡取决于第一个选项卡中的选择（三个选项）。
* 有三个可选选项卡(节点类型= `cq:Panel`)，每个字段都有两个文本字段(节点类型= `cq:Widget`， xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。 一次只显示一个可选选项卡。
* 由定义 `switchtabs` 节点位于：
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

该逻辑通过事件侦听器和JavaScript代码实现，如下所示：

* 对话框节点具有“ `beforeshow`”侦听器，在对话框显示之前隐藏所有可选选项卡：
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` 获取 `tabpanel` 包含选择面板和三个可选面板。
* 此 `Ejst.x2` 对象定义于 `exercises.js` 文件位于：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 在 `Ejst.x2.manageTabs()` 方法，作为的值 `index` 为–1，所有可选选项卡都隐藏（i从1到3）。
* 选择选项卡有两个监听器：其中一个在加载对话框时显示所选选项卡(&quot; `loadcontent`”事件)，在选择更改时显示选定选项卡的事件(“ `selectionchanged`“ event)：
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 对于 `Ejst.x2.showTab()` 方法，
  `field.findParentByType('tabpanel')` 获取 `tabpanel` 包含所有选项卡( `field` 表示选择小组件)
  `field.getValue()` 获取所选内容的值，例如tab2
  `Ejst.x2.manageTabs()` 显示选定的选项卡。
* 每个可选选项卡都有一个侦听器，用于隐藏“ `render`”事件：
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 对于 `Ejst.x2.hideTab()` 方法，
  `tabPanel``tabpanel`是包含所有选项卡的
  `index` 是可选选项卡的索引
  `tabPanel.hideTabStripItem(index)` 隐藏选项卡

它显示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 示例2：任意对话框 {#example-arbitrary-dialog}

通常，对话框会显示底层组件的内容。 此处介绍的对话框名为 **任意** 对话框，从其他组件中提取内容。

此 **任意** 对话框显示一个带有一个选项卡的窗口。 选项卡包含两个字段：一个用于放置或上传资源，另一个用于显示有关容器页面的一些信息，另一个用于显示有关资源的信息（如果已引用）。

其主要特点是：

* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示一个 `tabpanel` 构件(节点类型= `cq:Widget`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)具有一个面板(节点类型= `cq:Panel`)
* 面板具有smartfile小组件(节点类型= `cq:Widget`， xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)和ownerdraw小组件(节点类型= `cq:Widget`， xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* 由定义 `arbitrary` 节点位于：
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

该逻辑通过事件侦听器和JavaScript代码实现，如下所示：

* 此 `ownerdraw` 构件具有&quot; `loadcontent`”侦听器，显示有关包含该组件的页面的信息。 即，在加载内容时smartfile小组件所引用的资产：
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` 设置 `ownerdraw` 对象
  `path` 使用组件的内容路径设置(例如， `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* 此 `Ejst.x2` 对象定义于 `exercises.js` 文件位于：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 对于 `Ejst.x2.showInfo()` 方法，
  `pagePath` 是包含该组件的页面的路径；
  `pageInfo` 以json格式表示页面属性；
  `reference` 是引用资产的路径；
  `metadata` 以json格式表示资源的元数据；
  `ownerdraw.getEl().update(html);` 在对话框中显示创建的html

要使用 **任意** 对话框：

1. 使用任意对话框替换动态对话框 **组件的对话框** ： ****
关注示例2：单个面板对话框中描述的 [ 步骤](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 示例3：切换字段对话框 {#example-toggle-fields-dialog}

此 **切换字段** 对话框显示一个带有一个选项卡的窗口。 选项卡有复选框：如果选中，则会显示包含两个文本字段的字段集。

其主要特征包括：

* 由节点（节点 type = `cq:Dialog` ，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)` ）定义。
* 用一个面板（节点 type = `cq:Panel` ）显示一个 `tabpanel` 小组件（节点 type = `cq:Widget` ，xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)` ）。
* 该面板包含一个选择/复选框小组件（节点 type = `cq:Widget` 、xtype = ` [selection](/help/sites-developing/xtypes.md#selection)` 、type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)` ）和一个隐藏可折叠的 dialogfieldset 小组件（节点 type = `cq:Widget` ，xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` ），其中包含两个文本字段小组件（节点 type = `cq:Widget` ，xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)` ）。
* 由定义 `togglefields` 节点位于：
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

该逻辑通过事件侦听器和JavaScript代码实现，如下所示：

* “选择”选项卡有两个侦听器：其中一个在加载内容时显示dialogfieldset (&quot; `loadcontent`“ event”)，选择更改时显示对话框字段集的活动(“ `selectionchanged`“ event)：
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* 此 `Ejst.x2` 对象定义于 `exercises.js` 文件位于：
  `/apps/extjstraining/clientlib/js/exercises.js`
* 对于 `Ejst.x2.toggleFieldSet()` 方法，
  `box` 是选取对象；
  `panel` 是包含选定内容和dialogfieldset小组件的面板；
  `fieldSet` 是dialogfieldset对象；
  `show` 是所选内容的值（true或false）；基于&#39; `show`&#39;是否显示dialogfieldset

要使用 **切换字段** 对话框，请执行以下操作：

1. 替换对话框 **动态对话框** 包含的组件 **切换字段** 对话框：请按照中所述的步骤进行操作。 [示例2：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自定义构件 {#custom-widgets}

AEM附带的现成小组件应该涵盖大多数使用案例。 但是，有时可能有必要创建自定义构件以满足项目特定要求。 可通过扩展现有构件来创建自定义构件。 为了帮助您开始进行此类自定义，请使用 **`Using ExtJS Widgets`** 包中包含三个使用三个不同自定义小组件的对话框：

* 多字段对话框( `multifield` 节点)显示带有一个选项卡的窗口。 选项卡具有一个自定义的多字段构件，该构件包含两个字段：一个是包含两个选项的下拉菜单，另一个是文本字段。 因为它基于开箱即用型 `multifield` 构件（仅具有文本字段），它具有 `multifield` 构件。
* 树浏览对话框( `treebrowse` 节点)显示一个窗口，其中包含一个包含路径浏览小部件的选项卡：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 项目的路径随后将添加到路径字段，并在对话框关闭时保留。
* 基于富文本编辑器插件的对话框( `rteplugin` 节点)来将自定义按钮添加到富文本编辑器，以将某些自定义文本插入到主文本。 它包含 `richtext` 以及通过RTE插件机制添加的自定义功能的构件(RTE)。

自定义小部件和插件包含在名为的组件中 **3. 使用 ExtJS 小组件** 包的 **自定义小组件** 。要在示例页面中包含此组件：

1. **添加3。**&#x200B;在 Sidekick **中** 使用 ExtJS 选项卡小 **组件的示例页面** 的自定义 widget 部分。
1. 该组件显示标题、一些文本，并在单击 **属性** 关联时，存储在存储库中的段落属性。 再次单击将隐藏属性。
该组件显示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 示例1：自定义多字段构件 {#example-custom-multifield-widget}

此 **自定义多字段** 基于构件的对话框会显示一个带有一个选项卡的窗口。 选项卡具有自定义的多字段构件，与具有一个字段的标准构件不同，该构件具有两个字段：一个包含两个选项的下拉菜单和一个文本字段。

此 **自定义多字段** 基于构件的对话框：

* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)。
* 显示一个 `tabpanel` 构件(节点类型= `cq:Widget`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(节点类型= `cq:Widget`， xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有 `multifield` 构件(节点类型= `cq:Widget`， xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`)。
* 此 `multifield` 构件具有fieldconfig(节点类型= `nt:unstructured`， xtype = `ejstcustom`，选项提供程序= `Ejst.x3.provideOptions`)，它基于自定义xtype ` `ejstcustom`&#39;：
   * ’ `fieldconfig`&#39;是 ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)` 对象。
   * ’ `optionsProvider`&#39;是 `ejstcustom` 构件。 它通过 `Ejst.x3.provideOptions` 在中定义的方法 `exercises.js` 在：
     `/apps/extjstraining/clientlib/js/exercises.js`
并返回两个选项。
* 由定义 `multifield` 节点位于：
  `/apps/extjstraining/components/customwidgets/multifield`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自定义 `multifield` 构件(xtype = `ejstcustom`)：

* 是一个名为的JavaScript对象 `Ejst.CustomWidget`
* 在中定义 `CustomWidget.js` JavaScript文件位于：
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 扩展 ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` 构件。
* 有三个字段： `hiddenField` （文本字段）， `allowField` (ComboBox)，和 `otherField` （文本字段）
* 覆盖 `CQ.Ext.Component#initComponent` 添加三个字段：
   * `allowField` 是 [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) 类型为“select”的对象。 optionsProvider是Selection对象的配置，通过对话框中定义的CustomWidget的optionsProvider配置实例化
   * `otherField` 是 [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField) 对象
* 覆盖 CQ 的方法 `setValue` [ `getValue` `getRawValue` 和 CompositeField ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) ，以使用格式设置和检索 CustomWidget 的值：
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`。
* 将其自身注册为&#39; `ejstcustom`&#39; xtype：
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

此 **自定义多字段** 基于构件的对话框如下所示：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 示例2：自定义 `Treebrowse` 构件 {#example-custom-treebrowse-widget}

基于自定义 **`Treebrowse`** 小组件的对话框显示一个窗口，其中包含一个含有自定义路径浏览小组件的选项卡。 选择箭头时，将打开一个窗口，您可以在其中浏览层级并选择一个项目。 然后，将项目的路径添加到路径字段，并在关闭对话框时保持。

自定义 `treebrowse` 对话框：

* 由节点（节点 type = `cq:Dialog` ，xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)` ）定义。
* 显示一个 `tabpanel` 构件(节点类型= `cq:Widget`， xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)包含面板(节点类型= `cq:Widget`， xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有自定义构件(节点类型= `cq:Widget`， xtype = `ejstbrowse`)
* 由定义 `treebrowse` 节点位于：
  `/apps/extjstraining/components/customwidgets/treebrowse`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自定义树状浏览构件(xtype = `ejstbrowse`)：

* 是一个名为的JavaScript对象 `Ejst.CustomWidget`
* 在中定义 `CustomBrowseField.js` JavaScript文件位于：
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 扩展 ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* 定义一个名为的浏览窗口 `browseWindow`.
* 覆盖 ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` 在单击箭头时显示浏览窗口。
* 定义 [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) 对象：
   * 它通过调用注册于以下位置的servlet获取数据： `/bin/wcm/siteadmin/tree.json`.
   * 其根为&quot; `apps/extjstraining`“。
* 定义 `window` 对象( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)：
   * 基于预定义面板。
   * 有一个 **确定** 按钮，用于设置所选路径的值并隐藏面板。
* 窗户固定于下方 **路径** 字段。
* 所选路径将从浏览字段传递到上的窗口。 `show` 事件。
* 将其自身注册为&#39; `ejstbrowse`&#39; xtype：
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

要使用 **自定义树浏览** 基于构件的对话框：

1. 替换对话框 **自定义构件** 包含的组件 **自定义树浏览** 对话框：请按照中所述的步骤进行操作。 [示例2：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 示例3：富文本编辑器（RTE）插件 {#example-rich-text-editor-rte-plug-in}

**富文本编辑器（RTE）基于插件** 的对话框是一个基于文本编辑器的 rtf 对话框，其中包含一个自定义按钮，用于在方括号中插入一些自定义文本。自定义文本可由某些服务器端逻辑解析（在此示例中未实施），例如，添加一些在给定路径中定义的文本：

基于 RTE 插件 **的** 对话框：

* 由以下位置的rteplugin节点定义：
  `/apps/extjstraining/components/customwidgets/rteplugin`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* 此 `rtePlugins` 节点具有子节点 `inserttext` (节点类型= `nt:unstructured`)的插件名称。 它有一个属性，名为 `features` 该插件可定义RTE可用的插件功能。

RTE插件：

* 是一个名为的JavaScript对象 `Ejst.InsertTextPlugin`
* 在中定义 `InsertTextPlugin.js` JavaScript文件位于：
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 扩展 ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 对象。
* 以下方法定义 ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 和实现插件中覆盖的对象和：
   * `getFeatures()` 返回插件使其可用的所有功能的数组。
   * `initializeUI()` 向RTE工具栏中添加新按钮。
   * `notifyPluginConfig()` 将按钮悬停时显示标题和文本。
   * `execute()` 单击按钮并执行插件操作时，将调用：它会显示一个窗口，用于定义要包含的文本。
* `insertText()` 使用相应的对话框对象插入文本 `Ejst.InsertTextPlugin.Dialog` （请参阅之后）。
* `executeInsertText()` 由调用 `apply()` 对话框的方法，此对话框在 **确定** 已单击按钮。
* 将其自身注册为&#39; `inserttext`&#39;插件：
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* 该 `Ejst.InsertTextPlugin.Dialog` 对象定义在单击插件按钮时打开的对话框。 该对话框包含一个面板、一个表单、一个文本字段和两个按钮(**确定** 和 **取消**)。

要使用 **富文本编辑器(RTE)插件** 基于的对话框：

1. 替换对话框 **自定义构件** 包含的组件 **富文本编辑器(RTE)插件** 基于的对话框：请按照中所述的步骤进行操作。 [示例2：单面板对话框](#example-single-panel-dialog)
1. 编辑组件。
1. 单击右侧的最后一个图标（带有四个箭头的图标）。 输入路径并单击 **确定**：路径显示在方括号中([ ]）。
1. 单击 **确定** 因此请关闭富文本编辑器。

富文本编辑器（RTE）基于插件 **的** 对话框显示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此示例仅说明如何实施逻辑的客户端部分：占位符(*[文本]*)然后必须在服务器端显式解析（例如，在组件JSP中）。

### 树概述 {#tree-overview}

开箱即用 ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` 对象提供树形结构数据的用户界面表示。 使用 ExtJS **widget 包中** 包含的树概述组件显示如何使用该 `TreePanel` 对象在给定路径下显示 JCR 树。窗口本身可以停靠/断开连接。 在此示例中，窗口逻辑嵌入在标记之间 &lt;script> 的组件 jsp 中。

要在 **示例页面中包含树概述** 组件：

1. **添加4。在 Sidekick** 中 **使用 ExtJS 选项卡小** 组件的示例页面 **的树概述** 部分。
1. 组件显示：
   * 标题，带一些文本
   * a **属性** 链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 带有可展开的存储库树表示的浮动窗口。

该组件显示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

树概述组件：

* 定义于：
  `/apps/extjstraining/components/treeoverview`

* 该对话框允许您设置窗口的大小并停靠或取消停靠窗口（请参阅下面的详细信息）。

组件jsp：

* 从存储库中检索宽度、高度和停靠属性。
* 显示有关树概述数据格式的一些文本。
* 在JavaScript标记之间将窗口逻辑嵌入到组件jsp中。
* 定义于：
  `apps/extjstraining/components/treeoverview/content.jsp`

嵌入到组件jsp中的JavaScript代码：

* 定义 `tree` 对象，方法是尝试从页面检索树窗口。
* 如果显示树的窗口不存在， `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel))已创建：
   * `treePanel` 包含用于创建窗口的数据。
   * 通过调用在以下位置注册的servlet来检索数据：
     `/bin/wcm/siteadmin/tree.json`
* 此 `beforeload` 侦听器确保加载了选定的节点。
* 此 `root` 对象设置路径 `apps/extjstraining` 作为树的根目录。
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)的设置基于预定义的 `treePanel`、和的显示方式：
  `tree.show();`
* 如果存在该窗口，则会根据从存储库中检索到的宽度、高度和停靠属性显示该窗口。

组件对话框：

* 显示一个选项卡，其中有两个字段用于设置树概览窗口的大小（宽度和高度），另一个字段用于固定/取消固定窗口
* 由节点定义(节点类型= `cq:Dialog`， xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)。
* 面板具有大小字段小组件(节点类型= `cq:Widget`， xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)和选择小组件(节点类型= `cq:Widget`， xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，类型= `radio`)，具有两个选项(true/false)
* 由对话框节点在以下位置定义：
  `/apps/extjstraining/components/treeoverview/dialog`
* 通过请求以json格式呈现：
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 显示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 网格概述 {#grid-overview}

网格面板以行和列的表格格式表示数据。 它由以下部分组成：

* 存储：保存数据记录（行）的模型。
* 列模型：列的组成。
* 视图：封装用户界面。
* 选择模型：选择行为。

网格概述组件包含在 **使用ExtJS小组件** 包显示如何以表格格式显示数据：

* 示例1使用静态数据。
* 示例2使用从存储库中检索的数据。

要在示例页面中包含网格概述组件，请执行以下操作：

1. 添加 **5. 网格概述** 组件到示例页面 **使用ExtJS小组件** 选项卡 **Sidekick**.
1. 此时将显示组件：
   * 带有一些文本的标题
   * a **属性** 链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 包含表格格式数据的浮动窗口。

该组件显示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 示例1：默认网格 {#example-default-grid}

在其现成版本中， **网格概述** 组件以表格格式显示包含静态数据的窗口。 在此示例中，逻辑以两种方式嵌入到组件 jsp 中：

* 在标记之间 &lt;script> 定义通用逻辑
* 特定逻辑可在单独的.js文件中使用，并在jsp中链接到。 通过此设置，您可以通过注释所需的逻辑在两个逻辑（静态/动态）之间切换 &lt;script> 标记之间。

网格概述组件：

* 定义位置：
  `/apps/extjstraining/components/gridoverview`
* 此对话框可让您设置窗口的大小以及停靠或取消停靠窗口。

组件 jsp：

* 从存储库中检索宽度、高度和停靠属性。
* 在网格概述数据格式的简介中显示一些文本。
* 引用定义GridPanel对象的JavaScript代码：
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` 将某些静态数据定义为GridPanel对象的基础。
* 在JavaScript标记之间嵌入JavaScript代码，该标记定义了使用GridPanel对象的Window对象。
* 定义于：
  `apps/extjstraining/components/gridoverview/content.jsp`

嵌入到组件jsp中的JavaScript代码：

* 定义 `grid` 对象，方法是尝试从页面检索窗口组件：
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果 `grid` 不存在， [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 对象( `gridPanel`)通过调用 `getGridPanel()` 方法（见下文）。 此方法的定义位置为 `defaultgrid.js`.
* `grid` 是 ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` 对象，它基于预定义的GridPanel并显示： `grid.show();`
* 如果 `grid` 存在，根据从存储库检索到的宽度、高度和停靠属性显示它。

JavaScript文件( `defaultgrid.js`)组件jsp中引用的 `getGridPanel()` 方法，该方法由嵌入到JSP中的脚本调用，并返回 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，基于静态数据。 其逻辑如下：

* `myData` 是一个静态数据数组，格式为包含五列和四行的表。
* `store` 是 `CQ.Ext.data.Store` 使用对象 `myData`.
* `store` 已加载到内存中：
  `store.load();`
* `gridPanel` 是 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 使用对象 `store`：
   * 列宽始终按比例分配：
     `forceFit: true`
   * 一次只能选择一行：
     `singleSelect:true`

#### 示例2：引用搜索网格 {#example-reference-search-grid}

安装包时， `content.jsp` 的 **网格概述** 组件显示基于静态数据的网格。 可以修改该组件以显示具有以下特征的网格：

* 具有三列。
* 基于通过调用servlet从存储库检索的数据。
* 可以编辑最后一列的单元格。 该值会保留在 `test` 属性，该属性位于由第一列中显示的路径定义的节点下。

如上一节中所述，窗口对象将获取其 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，方法是 `getGridPanel()` 在中定义的方法 `defaultgrid.js` 文件位于 `/apps/extjstraining/components/gridoverview/defaultgrid.js`. **网格概述**组件为提供了不同的实施 `getGridPanel()` 方法，在中定义 `referencesearch.js` 文件位于 `/apps/extjstraining/components/gridoverview/referencesearch.js`. 通过切换组件jsp中引用的.js文件，网格将基于从存储库检索的数据。

切换在组件jsp中引用的.js文件：

1. 在 **CRXDE Lite**，在 `content.jsp` 文件，注释包含 `defaultgrid.js` 文件，因此它如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 从包含 `referencesearch.js` 文件，因此它如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 保存更改。
1. 刷新示例页面。

该组件显示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

组件jsp引用的JavaScript代码( `referencesearch.js`)定义 `getGridPanel()` 从组件jsp调用方法并返回 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 对象，基于从存储库动态检索的数据。 中的逻辑 `referencesearch.js` 将某些动态数据定义为GridPanel的基础：

* `reader` 是 ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`以json格式读取三列servlet响应的对象。
* `cm` 是 ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 三列的对象。
可以编辑“测试”列单元格，因为它们是使用编辑器定义的：
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 这些列可排序：
  `cm.defaultSortable = true;`
* `store` 是 ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 对象：
   * 它通过调用在“ ”注册的servlet获取数据 `/bin/querybuilder.json`&quot;，并使用一些参数筛选查询
   * 它基于 `reader`，预先定义
   * 该表将根据‘**jcr：path**&#39;列升序
* `gridPanel` 是 ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 可以编辑的对象：
   * 它基于预定义的 `store` 在列模型上 `cm`
   * 一次只能选择一行：
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * 该 `afteredit` 侦听器确保在&#39;&#39;中的单元格之后&#x200B;**测试**&#x200B;已编辑“ ”列：
      * 属性&#39; `test`“”定义的路径上的节点的“**jcr：path**“”列在存储库中设置单元格值
      * 如果POST成功，则会将该值添加到 `store` 对象，否则拒绝它
