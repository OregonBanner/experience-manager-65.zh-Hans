---
title: 使用和扩展构件（经典UI）
seo-title: 使用和扩展构件（经典UI）
description: AEM基于Web的界面使用AJAX和其他现代浏览器技术，使得作者能够直接在网页上对内容进行WYSIWYG编辑和格式化
seo-description: AEM基于Web的界面使用AJAX和其他现代浏览器技术，使得作者能够直接在网页上对内容进行WYSIWYG编辑和格式化
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '4965'
ht-degree: 0%

---


# 使用和扩展构件（经典UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>本页介绍了在经典UI中使用构件(AEM 6.4中已弃用)的情况。
>
>Adobe建议您基于[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)，利用新式的[触屏优化UI](/help/sites-developing/touch-ui-concepts.md)。

Adobe Experience Manager的基于Web的界面使用AJAX和其他现代浏览器技术，使作者能够直接在网页上对内容进行WYSIWYG编辑和格式化。

Adobe Experience Manager(AEM)使用[ExtJS](https://www.sencha.com/)构件库，它提供高度精致的用户界面元素，这些元素可以跨所有最重要的浏览器工作，并允许创建桌面级UI体验。

这些构件包含在AEM中，除了由AEM本身使用外，还可供使用AEM构建的任何网站使用。

有关AEM中所有可用构件的完整引用，请参阅[构件API文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)或现有xtypes](/help/sites-developing/xtypes.md)的[列表。 此外，[Sencha](https://www.sencha.com/products/extjs/examples/)站点上还提供了许多说明如何使用ExtJS框架的示例，该站点是框架的所有者。

本页对如何使用和扩展构件提供了一些见解。 它首先描述如何在页面[中包含客户端代码。 ](#including-the-client-sided-code-in-a-page)然后，它描述了为说明一些基本用途和扩展而创建的一些示例组件。 这些组件在&#x200B;**包共享**&#x200B;上的&#x200B;**使用ExtJS构件**&#x200B;包中可用。

该包包括以下示例：

* [使](#basic-dialogs) 用现成构件构建的基本对话框。
* [使](#dynamic-dialogs) 用现成构件和自定义的javascript逻辑构建的动态对话框。
* 基于[自定义构件](#custom-widgets)的对话框。
* [树面板](#tree-overview)在给定路径下显示JCR树。
* 以表格格式显示数据的[网格面板](#grid-overview)。

>[!NOTE]
>
>Adobe Experience Manager的经典UI基于[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/)构建。

## 在页面{#including-the-client-sided-code-in-a-page}中包含客户端代码

客户端javascript和样式表代码应放在客户端库中。

要创建客户端库，请执行以下操作：

1. 使用以下属性在`/apps/<project>`下创建一个节点：

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * 类别=&quot;[&lt;类别名称>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. 在`clientlib`下创建`css`和`js`文件夹(nt:folder)。

1. 在`clientlib`下面创建`css.txt`和`js.txt`文件(nt:files)。 这些。txt文件列表库中包含的文件。

1. 编辑`js.txt`:它需要开始“ `#base=js`”，然后列表CQ客户端库服务将聚集的文件，例如：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 编辑`css.txt`:它需要开始“ `#base=css`”，然后列表CQ客户端库服务将聚集的文件，例如：

   ```
   #base=css
    components.css
   ```

1. 在`js`文件夹下，放置属于库的javascript文件。

1. 在`css`文件夹下，放置`.css`文件和css文件使用的资源(例如，`my_icon.png`)。

>[!NOTE]
>
>之前描述的样式表的处理是可选的。

要在页面组件jsp中包含客户端库，请执行以下操作：

* 要同时包括javascript代码和样式表：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
在哪里 
`<category-nameX>` 是客户端库的名称。

* 要仅包含javascript代码，请执行以下操作：
   `<ui:includeClientLib js="<category-name>"/>`

有关详细信息，请参阅[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib)标记的说明。

在某些情况下，客户端库应仅在创作模式下可用，并应在发布模式下排除。 具体实现如下：

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 示例{#getting-started-with-the-samples}快速入门

要按照本页中的教程操作，请在本地AEM实例中安装名为&#x200B;**使用ExtJS构件**&#x200B;的包，并创建一个包含这些组件的示例页面。 为此，请执行以下操作：

1. 在AEM实例中，从“包共享”下载名为&#x200B;**使用ExtJS构件(v01)**&#x200B;的包并安装该包。 它会在存储库中的`/apps`下创建项目`extjstraining`。
1. 将包含脚本(js)和样式表(css)的客户端库包含在geometrixx页jsp的head标签中，因为您将在&#x200B;**Geometrixx**分支的新页面中包含示例组件：
在**CRXDE Lite**&#x200B;中，打开文件`/apps/geometrixx/components/page/headlibs.jsp`并将`cq.extjstraining`类别添加到现有的`<ui:includeClientLib>`标签中，如下所示：
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. 在`/content/geometrixx/en/products`下的&#x200B;**Geometrixx**&#x200B;分支中创建新页面，并将其命名为&#x200B;**使用ExtJS构件**。
1. 进入设计模式，将名为&#x200B;**使用ExtJS构件**&#x200B;的组的所有组件添加到Geometrixx设计中
1. 在编辑模式下返回：组&#x200B;**使用ExtJS构件**&#x200B;的组件可在Sidekick中使用。

>[!NOTE]
>
>本页中的示例基于Geometrixx示例内容，该内容不再随AEM一起提供，而已被We.Retail替换。 有关如何下载和安装文档，请参见Geometrixx[We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx)。

### 基本对话框{#basic-dialogs}

对话框通常用于编辑内容，但也只能显示信息。 视图完整对话框的一种简单方法是访问其json格式的表示形式。 为此，请将浏览器指向：

`https://localhost:4502/<path-to-dialog>.-1.json`

Sidekick中&#x200B;**使用ExtJS构件**&#x200B;组的第一个组件称为&#x200B;**1。 对话框基础知识**，包括四个基本对话框，这些基本对话框是使用现成构件构建的，并且没有自定义的javascript逻辑。 对话框存储在`/apps/extjstraining/components/dialogbasics`下。 基本对话框包括：

* 完整对话框（`full`节点）:它显示一个包含3个选项卡的窗口，每个选项卡都包含2个文本字段。
* 单面板对话框（`singlepanel`节点）:它显示一个窗口，其中包含1个选项卡，其中包含2个文本字段。
* 多面板对话框（`multipanel`节点）:其显示与“完整”对话框相同，但构建方式不同。
* 设计对话框（`design`节点）:它显示一个包含2个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集（4个文本字段）和一个可折叠字段集（2个文本字段）。

包括&#x200B;**1。 示例页面中的对话框基础知识**&#x200B;组件：

1. 添加&#x200B;**1。 对话框基础知识**&#x200B;组件，该组件从&#x200B;**Sidekick**&#x200B;的&#x200B;**使用ExtJS构件**&#x200B;选项卡进入示例页面。
1. 该组件显示标题、一些文本和&#x200B;**PROPERTIES**&#x200B;链接：单击链接以显示存储在存储库中的段落的属性。 再次单击链接以隐藏属性。

组件显示如下：

![chlimage_1-60](assets/chlimage_1-60.png)

#### 示例1:完整对话框{#example-full-dialog}

**Full**&#x200B;对话框显示一个窗口，其中包含三个选项卡，每个选项卡都包含两个文本字段。 它是&#x200B;**对话框基础**&#x200B;组件的默认对话框。 其特点是：

* 由节点定义：节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 显示3个选项卡（节点类型= `cq:Panel`）。
* 每个选项卡都有2个文本字段（节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/full`
* 通过请求：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

对话框显示如下：

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 示例2:单面板对话框{#example-single-panel-dialog}

**单面板**&#x200B;对话框显示一个窗口，其中有一个选项卡，其中包含两个文本字段。 其特点是：

* 显示1个选项卡（节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）
* 选项卡有2个文本字段（节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* 与&#x200B;**完整对话框**&#x200B;相比，一个优点是需要的配置更少。
* 建议使用：用于显示信息或只有几个字段的简单对话框。

要使用“单面板”对话框：

1. 将&#x200B;**对话框基础**&#x200B;组件的对话框替换为&#x200B;**单面板**&#x200B;对话框：
   1. 在&#x200B;**CRXDE Lite**&#x200B;中，删除节点：`/apps/extjstraining/components/dialogbasics/dialog`
   1. 单击&#x200B;**全部保存**&#x200B;以保存更改。
   1. 复制节点：`/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 将复制的节点粘贴到以下位置：`/apps/extjstraining/components/dialogbasics`
   1. 选择节点：`/apps/extjstraining/components/dialogbasics/Copy of singlepanel`并将其重命名为`dialog`。
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 示例3:多面板对话框{#example-multi-panel-dialog}

**多面板**&#x200B;对话框与&#x200B;**完整**&#x200B;对话框的显示方式相同，但其构建方式不同。 其特点是：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 显示3个选项卡（节点类型= `cq:Panel`）。
* 每个选项卡都有2个文本字段（节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* 与&#x200B;**完整对话框**&#x200B;相比，其优势在于其结构简化。
* 建议使用：的双曲余切值。

要使用多面板对话框：

1. 将&#x200B;**对话框基础**&#x200B;组件的对话框替换为&#x200B;**多面板**对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 示例4:富对话框{#example-rich-dialog}

**富**&#x200B;对话框显示一个包含两个选项卡的窗口。 第一个选项卡具有文本字段、下拉菜单和可折叠的文本区域。 第二个选项卡具有一个字段集，其中包含四个文本字段，以及一个可折叠字段集，其中包含两个文本字段。 其特点是：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示2个选项卡（节点类型= `cq:Panel`）。
* 第一个选项卡具有` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`构件（带有` [textfield](/help/sites-developing/xtypes.md#textfield)`）和` [selection](/help/sites-developing/xtypes.md#selection)`构件（带有3个选项），以及带有` [textarea](/help/sites-developing/xtypes.md#textarea)`构件的可折叠` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`。
* 第二个选项卡具有带4个` [textfield](/help/sites-developing/xtypes.md#textfield)`构件的` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`构件和带2个` [textfield](/help/sites-developing/xtypes.md#textfield)`构件的可折叠`dialogfieldset`。
* 由节点定义：
   `/apps/extjstraining/components/dialogbasics/rich`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

要使用&#x200B;**Rich**&#x200B;对话框：

1. 将&#x200B;**对话框基础**&#x200B;组件的对话框替换为&#x200B;**富**对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-01-31at50429](assets/screen_shot_2012-01-31at50429pm.png) ![pmscreen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 动态对话框{#dynamic-dialogs}

Sidekick中&#x200B;**使用ExtJS构件**&#x200B;组的第二个组件称为&#x200B;**2。 动态对话框**，包括三个动态对话框，它们使用现成构件构建，**使用自定义的javascript逻辑**。 对话框存储在`/apps/extjstraining/components/dynamicdialogs`下。 动态对话框包括：

* 交换机选项卡对话框（`switchtabs`节点）:它显示一个包含两个选项卡的窗口。 第一个选项卡有一个单选按钮选项，其中包含三个选项：选择某个选项时，将显示与该选项相关的选项卡。 第二个选项卡包含两个文本字段。
* 任意对话框（`arbitrary`节点）:它显示一个带有一个选项卡的窗口。 该选项卡包含一个用于拖放或上传资产的字段，以及一个用于显示有关包含页面以及资产（如果引用了页面）的某些信息的字段。
* 切换字段对话框（`togglefield`节点）:它显示一个带有一个选项卡的窗口。 该选项卡包含复选框：选中后，将显示包含两个文本字段的字段集。

包含&#x200B;**2。 示例页面上的动态对话框**&#x200B;组件：

1. 添加&#x200B;**2。 从** Sidekick **的**&#x200B;使用ExtJS构件&#x200B;**选项卡将动态对话框**&#x200B;组件添加到示例页面。
1. 该组件显示标题、一些文本和&#x200B;**PROPERTIES**&#x200B;链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。

组件显示如下：

![chlimage_1-61](assets/chlimage_1-61.png)

#### 示例1:交换机选项卡对话框{#example-switch-tabs-dialog}

**交换机选项卡**&#x200B;对话框显示一个包含两个选项卡的窗口。 第一个选项卡有一个单选按钮选项，其中包含三个选项：选择某个选项时，将显示与该选项相关的选项卡。 第二个选项卡包含两个文本字段。

其主要特点是：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示2个选项卡（节点类型= `cq:Panel`）:1选项卡，第2个选项卡取决于第1个选项卡（3个选项）中的选择。
* 有3个可选选项卡（节点类型= `cq:Panel`），每个选项卡都有2个文本字段（节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。 一次只显示一个可选选项卡。
* 由`switchtabs`节点在以下位置定义：
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* 对话框节点具有“ `beforeshow`”侦听器，它在显示对话框之前隐藏所有可选选项卡：
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 获取包含选择面板和3个可选面板的tabpanel。
* `Ejst.x2`对象在`exercises.js`文件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.manageTabs()`方法中，由于`index`的值为-1，所有可选选项卡都处于隐藏状态（i从1到3）。
* 选择选项卡具有2个监听器：一个选项卡在加载对话框时显示选定选项卡(“ `loadcontent`”事件)，另一个选项卡在更改选择时显示选定选项卡(“ `selectionchanged`”事件):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* 在`Ejst.x2.showTab()`方法中：
   `field.findParentByType('tabpanel')` 获取包含所有选项卡的表面板( `field` 表示选择构件)
   `field.getValue()` 获取选择的值，例如：tab2
   `Ejst.x2.manageTabs()` 显示所选选项卡。
* 每个可选选项卡都有一个监听器，它隐藏“ `render`”事件卡上的选项卡：
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* 在`Ejst.x2.hideTab()`方法中：
   `tabPanel` 是包含所有选项卡的tabpanel
   `index` 是可选选项卡的索引
   `tabPanel.hideTabStripItem(index)` 隐藏选项卡

它显示如下：

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 示例2:任意对话框{#example-arbitrary-dialog}

通常，对话框会显示基础组件中的内容。 此处描述的对话框称为&#x200B;**Arbitary**&#x200B;对话框，它从其他组件中提取内容。

**任意**&#x200B;对话框显示一个带有一个选项卡的窗口。 选项卡包含两个字段：一个用于拖放或上传资产，另一个用于显示有关包含页面以及资产（如果某个页面已被引用）的某些信息。

其主要特点是：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示1个Tabpanel构件（节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`），带有1个面板（节点类型= `cq:Panel`）
* 该面板有一个smartfile构件（节点类型= `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`）和一个ownerdraw构件（节点类型= `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`）
* 由`arbitrary`节点在以下位置定义：
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* ownerdraw构件有一个“ `loadcontent`”监听器，它显示加载内容时包含组件的页面和智能文件构件引用的资产的相关信息：
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` 是使用ownerdraw对象设置的
   `path` 设置为组件的内容路径(例如：/content/geometrixx/cn/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* `Ejst.x2`对象在`exercises.js`文件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.showInfo()`方法中：
   `pagePath` 是包含组件的页面的路径
   `pageInfo` 表示json格式的页面属性
   `reference` 是引用资产的路径
   `metadata` 以json格式表示资产的元数据
   `ownerdraw.getEl().update(html);` 在对话框中显示创建的html

要使用&#x200B;**任意**&#x200B;对话框：

1. 将&#x200B;**动态对话框**&#x200B;组件的对话框替换为&#x200B;**任意**对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 示例3:切换字段对话框{#example-toggle-fields-dialog}

**切换字段**&#x200B;对话框显示一个带有一个选项卡的窗口。 该选项卡包含复选框：选中后，将显示包含两个文本字段的字段集。

其主要特点是：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示1个Tabpanel构件（节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`），其中1个面板（节点类型= `cq:Panel`）。
* 该面板具有选择／复选框构件（节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`，类型= ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`）和可折叠的对话框字段集构件（节点类型= `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`），默认情况下隐藏该构件，其中包含2个文本字段构件（节点类型= `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* 由`togglefields`节点在以下位置定义：
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

该逻辑通过事件监听器和javascript代码实现，如下所示：

* 选择选项卡具有2个监听器：一个显示加载内容时的对话框字段集(&quot; `loadcontent`&quot;事件)，另一个显示更改选择时的对话框字段集(&quot; `selectionchanged`&quot;事件):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2`对象在`exercises.js`文件中定义：
   `/apps/extjstraining/clientlib/js/exercises.js`
* 在`Ejst.x2.toggleFieldSet()`方法中：
   `box` 是选择对象
   `panel` 是包含选定内容和对话框字段集构件的面板
   `fieldSet` 是dialogfieldset对象
   `show` 是基于“ ”的选择的值（true或false）, `show`显示或不显示对话框字段集

要使用&#x200B;**切换字段**&#x200B;对话框：

1. 将&#x200B;**动态对话框**&#x200B;组件的对话框替换为&#x200B;**切换字段**对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 自定义构件{#custom-widgets}

AEM附带的现成构件应涵盖大多数使用案例。 但是，有时可能需要创建自定义构件来满足特定项目的要求。 可通过扩展现有构件来创建自定义构件。 为帮助您开始进行此类自定义，**使用ExtJS构件**&#x200B;包中包含三个使用三个不同自定义构件的对话框：

* “多字段”对话框（`multifield`节点）显示一个带有一个选项卡的窗口。 该选项卡具有一个自定义的多字段构件，该构件具有两个字段：包含两个选项的下拉菜单和一个文本字段。 由于它基于现成的`multifield`构件（仅具有文本字段），因此它具有`multifield`构件的所有功能。
* 树浏览对话框（`treebrowse`节点）显示一个窗口，其中有一个选项卡包含路径浏览构件：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 项目的路径随后会添加到路径字段，并在关闭对话框时保留。
* 一个基于富文本编辑器插件的对话框（`rteplugin`节点），它向富文本编辑器中添加一个自定义按钮，将一些自定义文本插入主文本。 它由`richtext`构件(RTE)和通过RTE插件机制添加的自定义功能组成。

自定义构件和插件包含在名为&#x200B;**3的组件中。**&#x200B;使用ExtJS Widgets **包的自定义构件**。 要将此组件包含到示例页面，请执行以下操作：

1. 添加&#x200B;**3。 自定义构件**&#x200B;组件从&#x200B;**Sidekick**&#x200B;的&#x200B;**使用ExtJS构件**&#x200B;选项卡转至示例页面。
1. 该组件显示标题和一些文本，在单击&#x200B;**PROPERTIES**链接时，还会显示存储在存储库中的段落属性。 再次单击会隐藏属性。
组件显示如下：

![chlimage_1-62](assets/chlimage_1-62.png)

#### 示例1:自定义多字段构件{#example-custom-multifield-widget}

基于&#x200B;**自定义多字段**&#x200B;构件的对话框显示一个带有一个选项卡的窗口。 该选项卡具有自定义的多字段构件，该构件与具有一个字段的标准构件不同，具有两个字段：包含两个选项的下拉菜单和一个文本字段。

基于&#x200B;**自定义多字段**&#x200B;构件的对话框：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示1个表面板构件（节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`），其中包含一个面板（节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 该面板具有`multifield`构件（节点类型= `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`）。
* `multifield`构件具有基于自定义xtype &#39; `ejstcustom`&#39;的fieldconfig（节点类型= `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`）:
   * “ `fieldconfig`”是` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)`对象的配置选项。
   * “ `optionsProvider`”是`ejstcustom`构件的配置。 它使用`exercises.js`中定义的`Ejst.x3.provideOptions`方法进行设置，具体位置为：
      `/apps/extjstraining/clientlib/js/exercises.js`
并返回2个选项。
* 由`multifield`节点在以下位置定义：
   `/apps/extjstraining/components/customwidgets/multifield`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

自定义多字段构件(xtype = `ejstcustom`):

* 是名为`Ejst.CustomWidget`的javascript对象。
* 在`CustomWidget.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* 扩展` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)`构件。
* 包含3个字段：`hiddenField`（文本字段）、`allowField`(ComboBox)和`otherField`（文本字段）
* 覆盖`CQ.Ext.Component#initComponent`以添加3个字段：
   * `allowField` 是类型为 [“select”](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) 的CQ.form.Selectionobject。optionsProvider是Selection对象的配置，它使用对话框中定义的CustomWidget的optionsProvider配置进行实例化
   * `otherField` 是 [CQ.Ext.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) TextFieldobject
* 重写[CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)的`setValue`、`getValue`和`getRawValue`方法，以设置和检索格式为CustomWidget的值：
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`。
* 将自身注册为“ `ejstcustom`” xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

基于&#x200B;**自定义多字段**&#x200B;构件的对话框显示如下：

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 示例2:自定义树状浏览构件{#example-custom-treebrowse-widget}

基于自定义&#x200B;**树状浏览**&#x200B;构件的对话框显示一个窗口，其中含有一个包含自定义路径浏览构件的选项卡：单击箭头时，将打开一个窗口，您可以在其中浏览层次结构并选择项目。 项目的路径随后会添加到路径字段，并在关闭对话框时保留。

自定义树浏览对话框：

* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 显示1个表面板构件（节点类型= `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`），其中包含一个面板（节点类型= `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 该面板具有自定义构件（节点类型= `cq:Widget`, xtype = `ejstbrowse`）
* 由`treebrowse`节点在以下位置定义：
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

自定义树状浏览构件(xtype = `ejstbrowse`):

* 是名为`Ejst.CustomWidget`的javascript对象。
* 在`CustomBrowseField.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* 扩展` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`。
* 定义一个名为`browseWindow`的浏览窗口。
* 覆盖` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`，在单击箭头时显示浏览窗口。
* 定义[CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)对象：
   * 它通过调用在`/bin/wcm/siteadmin/tree.json`注册的servlet获取其数据。
   * 其根为“ `apps/extjstraining`”。
* 定义`window`对象(` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * 基于预定义面板。
   * 具有&#x200B;**OK**&#x200B;按钮，用于设置所选路径的值并隐藏面板。
* 窗口锚定在&#x200B;**路径**&#x200B;字段下。
* 所选路径将从浏览字段传递到`show`事件的窗口。
* 将自身注册为“ `ejstbrowse`” xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

要使用基于&#x200B;**自定义树状浏览**&#x200B;构件的对话框：

1. 将&#x200B;**自定义构件**&#x200B;组件的对话框替换为&#x200B;**自定义树状浏览**对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件：对话框显示如下：

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 示例3:富文本编辑器(RTE)插件{#example-rich-text-editor-rte-plug-in}

基于&#x200B;**富文本编辑器(RTE)插件**&#x200B;的对话框是基于富文本编辑器的对话框，该对话框包含一个自定义按钮，用于在方括号内插入一些自定义文本。 自定义文本可由某些服务器端逻辑分析（本例中未实现），例如添加在给定路径中定义的一些文本：

基于&#x200B;**RTE plugin**&#x200B;的对话框：

* 由retplugin节点在以下位置定义：
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins`节点具有以插件命名的子节点`inserttext`（节点类型= `nt:unstructured`）。 它有一个名为`features`的属性，它定义RTE可以使用的插件功能。

RTE插件：

* 是名为`Ejst.InsertTextPlugin`的javascript对象。
* 在`InsertTextPlugin.js` javascript文件中定义：
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* 扩展` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`对象。
* 以下方法定义` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`对象，并在实现插件中被覆盖：
   * `getFeatures()` 返回插件可用的所有功能的数组。
   * `initializeUI()` 将新按钮添加到RTE工具栏。
   * `notifyPluginConfig()` 悬停按钮时显示标题和文本。
   * `execute()` 在单击按钮时调用，并执行插件操作：它显示一个窗口，用于定义要包含的文本。
* `insertText()` 使用相应的对话框对象插入文 `Ejst.InsertTextPlugin.Dialog` 本（请参阅后面）。
* `executeInsertText()` 由对话框 `apply()` 的方法调用，单击OKbutton时 **** 将触发。
* 将自身注册为“ `inserttext`”插件：
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog`对象定义单击插件按钮时打开的对话框。 该对话框由面板、表单、文本字段和2个按钮（**OK**&#x200B;和&#x200B;**Cancel**）组成。

要使用基于&#x200B;**富文本编辑器(RTE)插件**&#x200B;的对话框：

1. 将&#x200B;**自定义构件**&#x200B;组件的对话框替换为基于&#x200B;**富文本编辑器(RTE)插件**的对话框：
按照[示例2中描述的步骤操作：单面板对话框](#example-single-panel-dialog)
1. 编辑组件。
1. 单击右侧的最后一个图标（带四个箭头的图标）。 输入路径，然后单击&#x200B;**确定**:
路径显示在括号([)中 ])。
1. 单击&#x200B;**确定**&#x200B;以关闭富文本编辑器。

基于&#x200B;**富文本编辑器(RTE)插件**&#x200B;的对话框显示如下：

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>此示例仅说明如何实现逻辑的客户端部分：占位符(*[text]*)随后必须在服务器端显式地进行分析（例如，在组件JSP中）。

### 树概述{#tree-overview}

现成的` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)`对象提供树结构化数据的树结构化UI表示。 **使用ExtJS构件**&#x200B;包中包含的树概述组件显示了如何使用`TreePanel`对象在给定路径下显示JCR树。 窗口本身可以停靠／取消停放。 在此示例中，窗口逻辑嵌入到组件jsp中的&lt;script>&lt;/script>标签之间。

要将&#x200B;**树概述**&#x200B;组件包含到示例页面中：

1. 添加&#x200B;**4。 从** Sidekick **中的**&#x200B;使用ExtJS构件&#x200B;**选项卡将概述**&#x200B;组件树添加到示例页。
1. 此时会显示以下组件：
   * 标题，带有一些文本
   * a **属性**&#x200B;链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 一个浮动窗口，具有存储库的树形表示，可以展开它。

组件显示如下：

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

树概述组件：

* 定义于：
   `/apps/extjstraining/components/treeoverview`

* 其对话框用于设置窗口的大小和停靠／取消停靠窗口（请参阅下面的详细信息）。

组件jsp:

* 从存储库中检索宽度、高度和停靠属性。
* 显示有关树概述数据格式的一些文本。
* 在javascript标签之间的组件jsp中嵌入窗口逻辑。
* 定义于：
   `apps/extjstraining/components/treeoverview/content.jsp`

组件jsp中嵌入的javascript代码：

* 通过尝试从页面检索树窗口来定义`tree`对象。
* 如果显示树的窗口不存在，则会创建`treePanel`([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` 包含用于创建窗口的数据。
   * 通过调用在以下位置注册的servlet来检索数据：
      `/bin/wcm/siteadmin/tree.json`
* `beforeload`监听器确保已加载单击的节点。
* `root`对象将路径`apps/extjstraining`设置为树根。
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)根据预定义进行设置 `treePanel`，并显示为：
   `tree.show();`
* 如果窗口已存在，则根据从存储库检索到的宽度、高度和停靠属性显示该窗口。

组件对话框：

* 显示1个选项卡，其中包含2个字段，用于设置树概述窗口的大小（宽度和高度）,1个字段用于停放／取消停放窗口
* 由节点定义（节点类型= `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* 该面板有一个大小字段构件（节点类型= `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`）和一个选择构件（节点类型= `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`），其中包含2个选项(true/false)
* 由对话框节点在以下位置定义：
   `/apps/extjstraining/components/treeoverview/dialog`
* 通过请求以json格式呈现：
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 显示如下：

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 网格概述{#grid-overview}

网格面板以行和列的表格格式表示数据。 它由以下几部分组成：

* 商店：保存数据记录（行）的模型。
* 列模型：专栏的组成。
* 视图:封装用户界面。
* 选择模型：选择行为。

**使用ExtJS构件**&#x200B;包中包含的“网格概述”组件显示了如何以表格格式显示数据：

* 示例1使用静态数据。
* 示例2使用从存储库检索的数据。

要将“网格概述”组件包含到示例页面，请执行以下操作：

1. 添加&#x200B;**5。 网格概述**&#x200B;组件从&#x200B;**Sidekick**&#x200B;中的&#x200B;**使用ExtJS构件**&#x200B;选项卡到示例页。
1. 此时会显示以下组件：
   * 带有文本的标题
   * a **属性**&#x200B;链接：单击以显示存储在存储库中的段落的属性。 再次单击可隐藏属性。
   * 包含表格格式数据的浮动窗口。

组件显示如下：

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 示例1:默认网格{#example-default-grid}

在其现成版本中，**网格概述**&#x200B;组件以表格格式显示包含静态数据的窗口。 在此示例中，逻辑以两种方式嵌入到组件jsp中：

* 通用逻辑在&lt;script>&lt;/script>标记之间定义
* 特定逻辑在单独的。js文件中可用，并在jsp中链接到。 通过注释所需的&lt;script>标签，此设置可以在两个逻辑（静态／动态）之间轻松切换。

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

组件jsp中嵌入的javascript代码：

* 通过尝试从页面检索窗口组件来定义`grid`对象：
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* 如果`grid`不存在，则通过调用`getGridPanel()`方法来定义[CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)对象(`gridPanel`)（请参见下文）。 此方法在`defaultgrid.js`中定义。
* `grid` 是基 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 于预定义的GridPanel的对象，并显示：  `grid.show();`
* 如果`grid`已存在，则根据从存储库检索到的宽度、高度和坞站属性来显示它。

组件jsp中引用的javascript文件(`defaultgrid.js`)定义了由嵌入在JSP中的脚本调用的`getGridPanel()`方法，并基于静态数据返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`对象。 逻辑如下：

* `myData` 是一组静态数据，格式为5列4行的表。
* `store` 是一个 `CQ.Ext.data.Store` 使用的对象 `myData`。
* `store` 加载到内存中：
   `store.load();`
* `gridPanel` 是消 ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 耗的对象 `store`:
   * 列宽会随时重新比例：
      `forceFit: true`
   * 一次只能选择一行：
      `singleSelect:true`

#### 示例2:引用搜索网格{#example-reference-search-grid}

安装包时，**Grid Overview**&#x200B;组件的`content.jsp`将显示一个基于静态数据的网格。 可以修改组件以显示具有以下特征的网格：

* 有三列。
* 基于通过调用Servlet从存储库检索的数据。
* 可以编辑最后一列的单元格。 该值将保留在由第一列中显示的路径定义的节点下的`test`属性中。

如前面一节所述，窗口对象通过调用`defaultgrid.js`文件`/apps/extjstraining/components/gridoverview/defaultgrid.js`中定义的`getGridPanel()`方法获取其` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`对象。 **网格概述**组件为`getGridPanel()`方法提供了不同的实现，该方法在`referencesearch.js`文件`/apps/extjstraining/components/gridoverview/referencesearch.js`中定义。 通过切换组件jsp中引用的。js文件，网格将基于从存储库检索到的数据。

切换组件jsp中引用的。js文件：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在组件的`content.jsp`文件中，注释包含`defaultgrid.js`文件的行，使其如下所示：
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. 从包含`referencesearch.js`文件的行中删除注释，使其如下所示：
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 保存更改。
1. 刷新示例页。

组件显示如下：

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

组件jsp(`referencesearch.js`)中引用的javascript代码定义从组件jsp调用的`getGridPanel()`方法，并根据从存储库动态检索的数据返回` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`对象。 `referencesearch.js`中的逻辑将一些动态数据定义为GridPanel的基础：

* `reader` 是一 ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`个对象，它以json格式读取3列的servlet响应。
* `cm` 是3 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 列的对象。可以编辑“测试”列单元格，因为它们是使用编辑器定义的：
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 列可排序：
   `cm.defaultSortable = true;`
* `store` 是对 ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 象：
   * 它通过调用注册在“ `/bin/querybuilder.json`”的servlet获取其查询，其中使用一些参数来过滤该数据
   * 它基于`reader`，预先定义
   * 表按“**jcr:path**”列的升序排序
* `gridPanel` 是可 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 以编辑的对象：
   * 它基于预定义的`store`和列模型`cm`
   * 一次只能选择一行：
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit`监听器确保在“**Test**”列中的单元格被编辑后：
      * 在存储库中设置由“**jcr:path**”列定义的路径上节点的属性“ `test`”，其值为单元格
      * 如果POST成功，则该值将添加到`store`对象，否则它将被拒绝
