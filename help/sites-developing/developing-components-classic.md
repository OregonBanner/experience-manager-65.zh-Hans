---
title: 开发AEM组件（经典UI）
seo-title: Developing AEM Components (Classic UI)
description: 经典UI使用ExtJS创建提供组件外观的小部件。 HTL不是AEM推荐的脚本语言。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# 开发AEM组件（经典UI）{#developing-aem-components-classic-ui}

经典UI使用ExtJS创建提供组件外观的小部件。 由于这些构件的性质，组件与经典UI的交互方式与 [触屏优化UI](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>组件开发的许多方面对于经典UI和触屏UI都是通用的，因此 **您必须阅读 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md) 早于** 使用此页面，该页面介绍经典UI的详细信息。

>[!NOTE]
>
>虽然HTML模板语言(HTL)和JSP都可用于开发经典UI的组件，但此页说明了使用JSP进行开发。 这完全是因为在经典UI中使用JSP的历史记录。
>
>HTL现在是AEM推荐的脚本语言。 参见 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 和 [开发AEM组件](/help/sites-developing/developing-components.md) 以比较方法。

## 结构 {#structure}

页面上介绍了组件的基本结构 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md#structure)，适用于触屏优化UI和经典UI。 即使您不需要在新组件中使用触屏UI的设置，也可以在继承现有组件时了解这些设置。

## JSP脚本 {#jsp-scripts}

可以使用JSP脚本或Servlet渲染组件。 根据Sling的请求处理规则，默认脚本的名称是：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP脚本文件 `global.jsp` 用于提供对用于呈现组件的任何JSP脚本文件的快速访问（即访问内容）。

因此 `global.jsp` 应包含在每个组件渲染JSP脚本中，其中提供的一个或多个对象 `global.jsp` 已使用。

默认的位置 `global.jsp` 为：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>路径 `/libs/wcm/global.jsp`CQ 5.3及更早版本使用的已过时。

### global.jsp、使用的API和Taglibs的功能 {#function-of-global-jsp-used-apis-and-taglibs}

下面列出了默认环境提供的最重要的对象 `global.jsp`：

摘要:

* `<cq:defineObjects />`

   * `slingRequest`  — 包装的请求对象( `SlingHttpServletRequest`)。
   * `slingResponse`  — 包装的响应对象( `SlingHttpServletResponse`)。
   * `resource` - Sling资源对象( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling资源解析程序对象( `slingRequest.getResoucreResolver();`)。
   * `currentNode`  — 请求的已解析JCR节点。
   * `log`  — 默认记录器()。
   * `sling` - Sling脚本助手。
   * `properties`  — 已寻址资源的属性( `resource.adaptTo(ValueMap.class);`)。
   * `pageProperties`  — 已寻址资源的页面的属性。
   * `pageManager`  — 用于访问AEM内容页面的页面管理器( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component`  — 当前AEM组件的组件对象。
   * `designer`  — 用于检索设计信息的设计器对象( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign`  — 寻址资源的设计。
   * `currentStyle`  — 已寻址资源的样式。

### 访问内容 {#accessing-content}

有三种方法可访问AEM WCM中的内容：

* 通过中引入的属性对象 `global.jsp`：

  properties对象是ValueMap的实例(请参阅 [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html))并包含当前资源的所有属性。

  示例： `String pageTitle = properties.get("jcr:title", "no title");` 在页面组件的渲染脚本中使用。

  示例： `String paragraphTitle = properties.get("jcr:title", "no title");` 在标准段落组件的渲染脚本中使用。

* 通过 `currentPage` 引入的对象 `global.jsp`：

  此 `currentPage` 对象是页面的实例(请参阅 [AEM API](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html))。 Page类提供了一些访问内容的方法。

  示例: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` 引入的对象 `global.jsp`：

  此 `currentNode` 对象是节点的实例(请参阅 [JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html))。 可以通过以下方式访问节点的属性 `getProperty()` 方法。

  示例: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP标记库 {#jsp-tag-libraries}

通过CQ和Sling标记库，可访问在模板和组件的JSP脚本中使用的特定函数。

有关详细信息，请参阅文档 [标记库](/help/sites-developing/taglib.md).

## 使用客户端HTML库 {#using-client-side-html-libraries}

现代网站在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为帮助处理此问题，AEM提供了 **客户端库文件夹**，用于将客户端代码存储在存储库中，将其组织成不同类别，并定义何时以及如何向客户端提供每种类别的代码。 然后，客户端库系统负责在最终网页中产生正确的链接，以加载正确的代码。

查看文档 [使用客户端HTML库](/help/sites-developing/clientlibs.md) 了解更多信息。

## 对话框 {#dialog}

您的组件需要一个对话框供作者添加和配置内容。

参见 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md#dialogs) 了解更多详细信息。

## 配置编辑行为 {#configuring-the-edit-behavior}

您可以配置组件的编辑行为。 这包括各种属性，例如组件可用的操作、就地编辑器的特征以及与组件上的事件相关的侦听器。 尽管存在某些特定差异，但配置对于触屏优化UI和经典UI都是通用的。

此 [组件的编辑行为已配置](/help/sites-developing/components-basics.md#edit-behavior) 通过添加 `cq:editConfig` 类型节点 `cq:EditConfig` 在组件节点下(类型为 `cq:Component`)，并添加特定属性和子节点。

## 使用和扩展ExtJS小组件 {#using-and-extending-extjs-widgets}

参见 [使用和扩展ExtJS小组件](/help/sites-developing/widgets.md) 了解更多详细信息。

## 为ExtJS构件使用xtype {#using-xtypes-for-extjs-widgets}

参见 [使用xtype](/help/sites-developing/xtypes.md) 了解更多详细信息。

## 开发新组件 {#developing-new-components}

本节介绍如何创建自己的组件并将它们添加到段落系统中。

快速入门方法是复制现有组件，然后进行所需的更改。

中详细描述了如何开发组件的示例 [扩展文本和图像组件 — 示例。](#extending-the-text-and-image-component-an-example)

### 开发新组件（调整现有组件） {#develop-a-new-component-adapt-existing-component}

要基于现有组件为AEM开发新组件，您可以复制组件，为新组件创建一个javascript文件，并将其存储在AEM可访问的位置(另请参阅 [自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))：

1. 使用CRXDE Lite在下列位置创建新组件文件夹：

   / `apps/<myProject>/components/<myComponent>`

   按照库中的方式重新创建节点结构，然后复制现有组件（如文本组件）的定义。 例如，要自定义文本组件副本，请执行以下操作：

   * 从 `/libs/foundation/components/text`
   * 到 `/apps/myProject/components/text`

1. 修改 `jcr:title` 以反映其新名称。
1. 打开新的组件文件夹，并进行所需的更改。 另外，删除文件夹中的任何无关信息。

   您可以进行如下更改：

   * 在对话框中添加新字段

      * `cq:dialog`  — 触屏UI的对话框
      * `dialog`  — 经典UI的对话框

   * 替换 `.jsp` 文件（将其命名为新组件的后缀）
   * 或者完全重新工作整个组件（如果需要）

   例如，如果您复制了标准文本组件，则可以在对话框中添加一个附加字段，然后更新 `.jsp` 以处理在那里输入的内容。

   >[!NOTE]
   >
   >的组件：
   >
   >* 触屏优化UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 组件
   >* 经典UI [ExtJS构件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)

   >[!NOTE]
   >
   >为经典UI定义的对话框将在触屏UI中运行。
   >
   >为触屏UI定义的对话框不会在经典UI中运行。
   >
   >根据您的实例和创作环境，您可能需要为组件定义这两种类型的对话框。

1. 应存在以下节点之一并正确初始化，以便新组件显示：

   * `cq:dialog`  — 触屏UI的对话框
   * `dialog`  — 经典UI的对话框
   * `cq:editConfig`  — 组件在编辑环境中的行为（例如拖放）
   * `design_dialog`  — 用于设计模式的对话框（仅限经典UI）

1. 通过以下任一方式激活段落系统中的新组件：

   * 使用CRXDE Lite添加值 `<path-to-component>` (例如， `/apps/geometrixx/components/myComponent`)到节点的属性组件 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 按照中的说明操作 [向段落系统添加新组件](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. 在AEM WCM中，打开网站中的页面，并插入您刚刚创建的类型的新段落，以确保组件正常工作。

>[!NOTE]
>
>要查看页面加载的时间统计信息，您可以使用Ctrl-Shift-U — 和 `?debugClientLibs=true` 在URL中设置。

### 向段落系统添加新组件（设计模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

开发组件后，您可以将其添加到段落系统，这样作者就可以在编辑页面时选择和使用组件。

1. 访问创作环境中使用段落系统的页面，例如 `<contentPath>/Test.html`.
1. 通过以下任一方式切换到设计模式：

   * 添加 `?wcmmode=design` 前往URL的末尾，然后再次访问，例如：

     `<contextPath>/ Test.html?wcmmode=design`

   * 在Sidekick中单击设计

   您现在处于设计模式，可以编辑段落系统。

1. 单击“编辑”。

   此时将显示属于段落系统的组件列表。 新组件也会列出。

   可以激活（或停用）组件以确定在编辑页面时向作者提供哪些组件。

1. 激活组件，然后返回到正常编辑模式以确认该组件可供使用。

### 扩展文本和图像组件 — 示例 {#extending-the-text-and-image-component-an-example}

本节提供了一个示例，说明如何使用可配置的图像放置功能扩展广泛使用的文本和图像标准组件。

文本和图像组件的扩展允许编辑器使用组件的所有现有功能，并有一个额外的选项来指定图像的放置：

* 在文本的左侧（当前行为和新的默认值）
* 还有右手边

扩展此元件后，可通过元件的对话框配置图像放置。

本练习将介绍以下技术：

* 复制现有组件节点并修改其元数据
* 修改组件的对话框，包括从父对话框继承构件
* 修改组件的脚本以实施新功能

>[!NOTE]
>
>此示例针对经典UI。

>[!NOTE]
>
>此示例基于Geometrixx示例内容，该内容不再随AEM提供，已被We.Retail取代。 查看文档 [We.Retail参考实施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 了解如何下载和安装Geometrixx。

#### 扩展现有文本时间组件 {#extending-the-existing-textimage-component}

要创建新组件，我们使用标准文本组件作为基础并对其进行修改。 我们将新组件存储在GeometrixxAEM WCM示例应用程序中。

1. 从以下位置复制标准文本页面组件 `/libs/foundation/components/textimage` 到Geometrixx组件文件夹中， `/apps/geometrixx/components`，使用textimage作为目标节点名称。 （导航到组件，右键单击并选择复制，然后浏览到目标目录来复制组件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 要使此示例保持简单，请导航到您复制的组件，并删除新文本时间节点的所有子节点，以下子节点除外：

   * 对话框定义： `textimage/dialog`
   * 组件脚本： `textimage/textimage.jsp`
   * 编辑配置节点（允许拖放资产）： `textimage/cq:editConfig`

   >[!NOTE]
   >
   >对话框定义依赖于UI：
   >
   >* 触屏优化UI： `textimage/cq:dialog`
   >* 经典 UI: `textimage/dialog`

1. 编辑组件元数据：

   * 组件名称

      * 设置 `jcr:description` 到 `Text Image Component (Extended)`
      * 设置 `jcr:title` 到 `Text Image (Extended)`

   * 组，其中组件在sidekick中列出（保持原样）

      * 离开 `componentGroup` 设置为 `General`

   * 新组件的父组件（标准文本时间组件）

      * 设置 `sling:resourceSuperType` 到 `foundation/components/textimage`

   在此步骤之后，组件节点如下所示：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 更改 `sling:resourceType` 图像的edit configuration节点的属性(属性： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`)至 `geometrixx/components/textimage.`

   这样，当图像放到页面上的组件时， `sling:resourceType` extended textimage组件的属性设置为： `geometrixx/components/textimage.`

1. 修改组件的对话框以包含新选项。 新元件继承对话框中与原始元件相同的部分。 我们所做的唯一补充是扩展 **高级** 选项卡，添加 **图像位置** 下拉列表，带选项 **左侧** 和 **右**：

   * 保留 `textimage/dialog`属性未更改。

   请注意操作方法 `textimage/dialog/items` 具有四个子节点，即tab1到tab4，表示“文本时间”对话框的四个选项卡。

   * 对于前两个选项卡（tab1和tab2）：

      * 将xtype更改为cqinclude（继承自标准组件）。
      * 添加带有值的路径属性 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`和 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`，则不会显示任何内容。
      * 删除所有其他属性或子节点。

   * 对于选项卡3：

      * 不更改属性和子节点
      * 将新的字段定义添加到 `tab3/items`，类型的节点位置 `cq:Widget`
      * 为新的设置以下属性（字符串类型） `tab3/items/position`节点：

         * `name`： `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`

      * 添加子节点 `position/options` 类型 `cq:WidgetCollection` 表示两个图像放置选项，并在其下创建两个类型节点o1和o2 `nt:unstructured`.
      * 用于节点 `position/options/o1` 设置属性： `text` 到 `Left` 和 `value` 到 `left.`
      * 用于节点 `position/options/o2` 设置属性： `text` 到 `Right` 和 `value` 到 `right`.

   * 删除选项卡4。

   图像位置作为保留在内容中 `imagePosition`表示节点的属性 `textimage` 段落。 执行这些步骤后，“组件”对话框将如下所示：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 扩展组件脚本， `textimage.jsp`，并对新参数进行额外处理：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   我们将替换强调的代码片段 *%>&lt;div class=&quot;image&quot;>&lt;%* 新代码生成此标记的自定义样式。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 将组件保存到存储库。 组件已准备好进行测试。

#### 检查新组件 {#checking-the-new-component}

开发组件后，您可以将其添加到段落系统，这样作者就可以在编辑页面时选择和使用组件。 这些步骤允许您测试组件。

1. 以Geometrixx（如英语/公司）打开页面。
1. 通过单击Sidekick中的“设计”切换到设计模式。
1. 通过单击页面中间段落系统上的编辑，编辑段落系统设计。 此时将显示可放置在段落系统中的组件列表，该列表应包含新开发的组件文本图像（扩展） 。 选择段落系统并单击确定，以将其激活。
1. 切换回编辑模式。
1. 将文本图像（扩展）段落添加到段落系统中，用示例内容初始化文本和图像。 保存更改。
1. 打开文本和图像段落的对话框，将“高级”选项卡上的“图像位置”更改为“右” ，然后单击“确定”以保存更改。
1. 段落在渲染时将使用右侧的图像。
1. 该组件现已准备就绪，可使用。

组件将其内容存储在公司页面上的一个段落中。

### 禁用图像组件的上传功能 {#disable-upload-capability-of-the-image-component}

要禁用此功能，我们使用标准图像组件作为基础并对其进行修改。 我们将新组件存储在Geometrixx示例应用程序中。

1. 从以下位置复制标准图像组件 `/libs/foundation/components/image` 到Geometrixx组件文件夹中， `/apps/geometrixx/components`，使用图像作为目标节点名称。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 编辑组件元数据：

   * 设置 **jcr：title** 到 `Image (Extended)`

1. 导航到 `/apps/geometrixx/components/image/dialog/items/image`。
1. 添加新属性:

   * **名称**: `allowUpload`
   * **类型**： `String`
   * **值**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 单击 **全部保存**. 组件已准备好进行测试。
1. 以Geometrixx（如英语/公司）打开页面。
1. 切换到设计模式并激活图像（扩展）。
1. 切换回编辑模式并将其添加到段落系统。 在下一张图片中，您可以看到原始图像组件与您刚刚创建的组件之间的差异。

   原始图像组件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新图像组件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 该组件现已准备就绪，可使用。
