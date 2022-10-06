---
title: 开发AEM组件（经典UI）
seo-title: Developing AEM Components (Classic UI)
description: 经典UI使用ExtJS创建小组件，以提供组件的外观。 HTL不是推荐的AEM脚本语言。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2394'
ht-degree: 1%

---

# 开发AEM组件（经典UI）{#developing-aem-components-classic-ui}

经典UI使用ExtJS创建小组件，以提供组件的外观。 由于这些小组件的性质，组件与经典UI和 [触屏优化UI](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>组件开发的许多方面在经典UI和触屏UI中都是通用的，因此 **你必须读 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md) 之前** 使用此页面，该页面介绍经典UI的特定内容。

>[!NOTE]
>
>虽然HTML模板语言(HTL)和JSP都可用于开发经典UI的组件，但本页说明了如何使用JSP进行开发。 这完全是由于在经典UI中使用JSP的历史记录所致。
>
>HTL现在是推荐的AEM脚本语言。 请参阅 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 和 [开发AEM组件](/help/sites-developing/developing-components.md) 来比较方法。

## 结构 {#structure}

页面上介绍了组件的基本结构 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md#structure)，它同时应用触屏界面和经典用户界面。 即使您不需要在新组件中使用触屏优化UI的设置，在继承现有组件时，也需要了解这些设置。

## JSP脚本 {#jsp-scripts}

JSP脚本或Servlet可用于渲染组件。 根据Sling的请求处理规则，默认脚本的名称为：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP脚本文件 `global.jsp` 用于提供对特定对象（即访问内容）的快速访问，以访问用于呈现组件的任何JSP脚本文件。

因此 `global.jsp` 应包含在每个组件中，其中呈现JSP脚本中提供的一个或多个对象 `global.jsp` 中，将使用。

默认位置 `global.jsp` 为：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>路径 `/libs/wcm/global.jsp`而且，CQ 5.3及更早版本使用的版本现在已过时。

### global.jsp、已用API和Taglibs的函数 {#function-of-global-jsp-used-apis-and-taglibs}

下面列出了默认提供的最重要的对象 `global.jsp`:

摘要:

* `<cq:defineObjects />`

   * `slingRequest`  — 封装的请求对象( `SlingHttpServletRequest`)。
   * `slingResponse`  — 封装的响应对象( `SlingHttpServletResponse`)。
   * `resource` - Sling资源对象( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling资源解析程序对象( `slingRequest.getResoucreResolver();`)。
   * `currentNode`  — 请求的已解析JCR节点。
   * `log`  — 默认日志记录器()。
   * `sling` - Sling脚本助手。
   * `properties`  — 已寻址资源的属性( `resource.adaptTo(ValueMap.class);`)。
   * `pageProperties`  — 已寻址资源页面的属性。
   * `pageManager`  — 用于访问AEM内容页面的页面管理器( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component`  — 当前AEM组件的组件对象。
   * `designer`  — 用于检索设计信息的设计器对象( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign`  — 编址资源的设计。
   * `currentStyle`  — 已寻址资源的样式。

### 访问内容 {#accessing-content}

在AEM WCM中，有三种方法可访问内容：

* 通过 `global.jsp`:

   属性对象是ValueMap的实例(请参阅 [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html))并包含当前资源的所有属性。

   示例： `String pageTitle = properties.get("jcr:title", "no title");` 在页面组件的渲染脚本中使用。

   示例： `String paragraphTitle = properties.get("jcr:title", "no title");` 在标准段落组件的渲染脚本中使用。

* 通过 `currentPage` 引入的对象 `global.jsp`:

   的 `currentPage` 对象是页面的实例(请参阅 [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml))。 页面类提供了一些访问内容的方法。

   示例: `String pageTitle = currentPage.getTitle();`

* 通过 `currentNode` 引入的对象 `global.jsp`:

   的 `currentNode` 对象是节点的实例(请参阅 [JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html))。 节点的属性可通过 `getProperty()` 方法。

   示例: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP标记库 {#jsp-tag-libraries}

通过CQ和Sling标记库，您可以访问特定函数，以在模板和组件的JSP脚本中使用。

有关详细信息，请参阅文档 [标记库](/help/sites-developing/taglib.md).

## 使用客户端HTML库 {#using-client-side-html-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为帮助处理此问题，AEM提供 **客户端库文件夹**，用于在存储库中存储客户端代码，将其整理为不同的类别，并定义何时以及如何将每类代码提供给客户端。 然后，客户端库系统会负责在最终网页中生成正确的链接，以加载正确的代码。

查看文档 [使用客户端HTML库](/help/sites-developing/clientlibs.md) 以了解更多信息。

## 对话框 {#dialog}

您的组件需要一个供作者使用的对话框才能添加和配置内容。

请参阅 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md#dialogs) 以了解更多详细信息。

## 配置编辑行为 {#configuring-the-edit-behavior}

您可以配置组件的编辑行为。 这包括一些属性，例如组件可用的操作、就地编辑器的特性以及与组件上的事件相关的侦听器。 配置对于触屏UI和经典UI都是通用的，尽管存在某些特定差异。

的 [配置了组件的编辑行为](/help/sites-developing/components-basics.md#edit-behavior) 通过添加 `cq:editConfig` 类型节点 `cq:EditConfig` 组件节点下(类型 `cq:Component`)和添加特定属性和子节点。

## 使用和扩展ExtJS小组件 {#using-and-extending-extjs-widgets}

请参阅 [使用和扩展ExtJS小组件](/help/sites-developing/widgets.md) 以了解更多详细信息。

## 对ExtJS小组件使用xtypes {#using-xtypes-for-extjs-widgets}

请参阅 [使用xtype](/help/sites-developing/xtypes.md) 以了解更多详细信息。

## 开发新组件 {#developing-new-components}

本节将介绍如何创建您自己的组件并将其添加到段落系统中。

快速入门的方法是复制现有组件，然后进行所需的更改。

有关如何开发组件的示例，请参见 [扩展文本和图像组件 — 示例。](#extending-the-text-and-image-component-an-example)

### 开发新组件（调整现有组件） {#develop-a-new-component-adapt-existing-component}

要根据现有组件为AEM开发新组件，您可以复制组件，请为新组件创建javascript文件并将其存储在AEM可访问的位置(另请参阅 [自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. 使用CRXDE Lite，在中创建新组件文件夹：

   / `apps/<myProject>/components/<myComponent>`

   像在库中一样重新创建节点结构，然后复制现有组件（如文本组件）的定义。 例如，要自定义文本组件副本，请执行以下操作：

   * 从 `/libs/foundation/components/text`
   * 到 `/apps/myProject/components/text`

1. 修改 `jcr:title` 以反映其新名称。
1. 打开新组件文件夹，然后进行所需的更改。 此外，请删除文件夹中任何无关的信息。

   您可以进行以下更改：

   * 在对话框中添加新字段

      * `cq:dialog`  — 触屏UI对话框
      * `dialog`  — 经典UI对话框
   * 替换 `.jsp` 文件（在新组件之后命名）
   * 或完全重新工作整个组件（如果需要）

   例如，如果您获取标准文本组件的副本，则可以向对话框中添加额外的字段，然后更新 `.jsp` 来处理输入。

   >[!NOTE]
   >
   >以下组件：
   >
   >* 触屏优化UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 组件
   >* 经典UI使用 [ExtJS小组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >为经典UI定义的对话框将在触屏UI中运行。
   >
   >为触屏UI定义的对话框将无法在经典UI中运行。
   >
   >根据您的实例和创作环境，您可能希望为组件定义这两种类型的对话框。

1. 以下节点之一应存在并正确初始化，以便显示新组件：

   * `cq:dialog`  — 触屏UI对话框
   * `dialog`  — 经典UI对话框
   * `cq:editConfig`  — 组件在编辑环境中的行为方式（例如拖放）
   * `design_dialog`  — 用于设计模式的对话框（仅限经典UI）

1. 通过以下任一方式在段落系统中激活新组件：

   * 使用CRXDE Lite添加值 `<path-to-component>` (例如， `/apps/geometrixx/components/myComponent`)到节点的属性组件 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 按照 [向段落系统添加新组件](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. 在AEM WCM中，打开您网站的页面，并插入刚刚创建的类型的新段落，以确保组件正常工作。

>[!NOTE]
>
>要查看页面加载的时间统计信息，可以使用Ctrl-Shift-U - `?debugClientLibs=true` 在URL中设置。

### 向段落系统添加新组件（设计模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

开发组件后，可将其添加到段落系统，使作者能够在编辑页面时选择和使用组件。

1. 例如，在使用段落系统的创作环境中访问页面 `<contentPath>/Test.html`.
1. 通过以下任一方式切换到设计模式：

   * 添加 `?wcmmode=design` 返回到URL的结尾并再次访问，例如：

      `<contextPath>/ Test.html?wcmmode=design`

   * 在Sidekick中单击设计

   您现在处于设计模式，可以编辑段落系统。

1. 单击编辑。

   将显示属于段落系统的组件列表。 此外，还将列出新组件。

   可以激活（或停用）这些组件，以确定在编辑页面时向作者提供的组件。

1. 激活组件，然后返回到正常的编辑模式，以确认该组件可供使用。

### 扩展文本和图像组件 — 示例 {#extending-the-text-and-image-component-an-example}

本节提供了有关如何使用可配置的图像放置功能来扩展广泛使用的文本和图像标准组件的示例。

文本和图像组件的扩展允许编辑器使用组件的所有现有功能以及一个额外的选项来指定图像的位置：

* 在文本的左侧（当前行为和新的默认行为）
* 在右侧

扩展此组件后，可通过组件的对话框配置图像放置。

本练习中介绍了以下技术：

* 复制现有组件节点并修改其元数据
* 修改组件的对话框，包括父对话框中小组件的继承
* 修改组件的脚本以实施新功能

>[!NOTE]
>
>此示例针对经典UI。

>[!NOTE]
>
>此示例基于Geometrixx示例内容，该内容不再随AEM一起提供，而已被We.Retail替换。 查看文档 [We.Retail参考实施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 以了解如何下载和安装Geometrixx。

#### 扩展现有文本时间组件 {#extending-the-existing-textimage-component}

要创建新组件，我们将使用标准文本时间组件作为基础并对其进行修改。 我们将新组件存储在GeometrixxAEM WCM示例应用程序中。

1. 从以下位置复制标准文本时间组件 `/libs/foundation/components/textimage` 到Geometrixx组件文件夹中， `/apps/geometrixx/components`，使用textimage作为目标节点名称。 （通过导航到组件，右键单击并选择复制并浏览到目标目录，可复制组件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 要简化此示例，请导航到您复制的组件，并删除新文本时间节点的所有子节点，以下子节点除外：

   * 对话框定义： `textimage/dialog`
   * 组件脚本： `textimage/textimage.jsp`
   * 编辑配置节点（允许拖放资产）： `textimage/cq:editConfig`

   >[!NOTE]
   >
   >对话框定义取决于UI:
   >
   >* 触屏UI: `textimage/cq:dialog`
   >* 经典 UI: `textimage/dialog`


1. 编辑组件元数据：

   * 组件名称

      * 已设置 `jcr:description` to `Text Image Component (Extended)`
      * 已设置 `jcr:title` to `Text Image (Extended)`
   * 组，其中组件列在Sidekick中（保持原样）

      * 离开 `componentGroup` 设置为 `General`
   * 新组件的父组件（标准文本时间组件）

      * 已设置 `sling:resourceSuperType` to `foundation/components/textimage`

   在此步骤之后，组件节点如下所示：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 更改 `sling:resourceType` 图像编辑配置节点的属性(属性： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) `geometrixx/components/textimage.`

   这样，当图像被放置到页面上的组件时， `sling:resourceType` 扩展textimage组件的属性设置为： `geometrixx/components/textimage.`

1. 修改组件的对话框以包含新选项。 新组件会继承与原始组件相同的对话框部分。 我们唯一的补充就是 **高级** 选项卡，添加 **图像位置** 下拉列表，带选项 **左** 和 **Right**:

   * 离开 `textimage/dialog`属性未更改。

   注意方式 `textimage/dialog/items` 有四个子节点，从tab1到tab4，表示textimage对话框的四个选项卡。

   * 对于前两个选项卡（tab1和tab2）：

      * 将xtype更改为cqinclude（从标准组件继承）。
      * 添加具有值的路径属性 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`和 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`，分别为。
      * 删除所有其他属性或子节点。
   * 对于选项卡3:

      * 保留属性和子节点，不进行更改
      * 将新字段定义添加到 `tab3/items`，类型的节点位置 `cq:Widget`
      * 为新 `tab3/items/position`节点：

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * 添加子节点 `position/options` 类型 `cq:WidgetCollection` 用于表示图像放置的两种选项，并在其下创建两个节点，即o1和o2类型 `nt:unstructured`.
      * 对于节点 `position/options/o1` 设置属性： `text` to `Left` 和 `value` to `left.`
      * 对于节点 `position/options/o2` 设置属性： `text` to `Right` 和 `value` to `right`.
   * 删除选项卡4。

   图像位置会在内容中保留，因为 `imagePosition`表示 `textimage` 段落。 完成这些步骤后，组件对话框如下所示：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 扩展组件脚本， `textimage.jsp`，并额外处理新参数：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   我们将替换强调代码片段 *%>&lt;div class=&quot;image&quot;>&lt;%* 包含为此标记生成自定义样式的新代码。

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

开发组件后，您可以将其添加到段落系统中，这允许作者在编辑页面时选择和使用组件。 这些步骤允许您测试组件。

1. 以Geometrixx（如英语/公司）打开页面。
1. 单击Sidekick中的“设计”以切换到设计模式。
1. 通过单击页面中间段落系统上的编辑，编辑段落系统设计。 此时会显示可放置在段落系统中的组件列表，其中应包含您新开发的组件文本图像（扩展）。 通过选择段落系统并单击确定，将其激活。
1. 切换回编辑模式。
1. 将文本图像（扩展）段落添加到段落系统，使用示例内容初始化文本和图像。 保存更改。
1. 打开文本和图像段落的对话框，将“高级”选项卡上的“图像位置”更改为“右侧” ，然后单击“确定”以保存更改。
1. 段落在右侧显示图像。
1. 组件现已准备就绪，可供使用。

组件将其内容存储在公司页面的段落中。

### 禁用图像组件的上传功能 {#disable-upload-capability-of-the-image-component}

要禁用此功能，我们将使用标准图像组件作为基础并对其进行修改。 我们将新组件存储在Geometrixx示例应用程序中。

1. 从以下位置复制标准图像组件 `/libs/foundation/components/image` 到Geometrixx组件文件夹中， `/apps/geometrixx/components`，使用图像作为目标节点名称。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 编辑组件元数据：

   * 已设置 **jcr:title** to `Image (Extended)`

1. 导航到 `/apps/geometrixx/components/image/dialog/items/image`。
1. 添加新属性:

   * **名称**: `allowUpload`
   * **类型**: `String`
   * **值**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 单击 **全部保存**. 组件已准备好进行测试。
1. 以Geometrixx（如英语/公司）打开页面。
1. 切换到设计模式并激活“图像（扩展）”。
1. 切换回编辑模式，并将其添加到段落系统。 在下一张图片中，您可以看到原始图像组件与刚刚创建的图像组件之间的差异。

   原始图像组件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新图像组件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 组件现已准备就绪，可供使用。
