---
title: 开发AEM组件（经典UI）
seo-title: 开发AEM组件（经典UI）
description: 经典UI使用ExtJS创建构件，提供组件的外观。 HTL不是AEM的推荐脚本语言。
seo-description: 经典UI使用ExtJS创建构件，提供组件的外观。 HTL不是AEM的推荐脚本语言。
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 开发AEM组件（经典UI）{#developing-aem-components-classic-ui}

经典UI使用ExtJS创建构件，提供组件的外观。 由于这些构件的性质，组件与经典UI和触屏优化UI的交互方式 [之间存在一些差异](/help/sites-developing/developing-components.md)。

>[!NOTE]
>
>组件开发的许多方面对于经典UI和触屏优化UI都很常见，因此 **您必须阅读[AEM组件——使用此页面之前的基础知识](/help/sites-developing/components-basics.md)** ，该页面涉及经典UI的特定信息。

>[!NOTE]
>
>尽管HTML模板语言(HTL)和JSP都可用于为经典UI开发组件，但本页说明了如何使用JSP进行开发。 这完全是由于在经典UI中使用JSP的历史记录。
>
>HTL现在是AEM的推荐脚本语言。 请参 [阅HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)[和开发AEM组件](/help/sites-developing/developing-components.md) ，以比较方法。

## 结构 {#structure}

AEM组件——基础知识页面中介绍了组件的基本结构 [](/help/sites-developing/components-basics.md#structure)，该页面同时应用触屏和经典UI。 即使您不需要在新组件中使用触屏优化UI的设置，也可以在继承现有组件时了解这些设置。

## JSP脚本 {#jsp-scripts}

JSP脚本或Servlet可用于呈现组件。 根据Sling的请求处理规则，默认脚本的名称为：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP脚本文 `global.jsp` 件用于提供对特定对象（即访问内容）的快速访问，以访问用于呈现组件的任何JSP脚本文件。

因此， `global.jsp` 应将每个组件包含在呈现JSP脚本中，其中使用了中提供的一个或多个对 `global.jsp` 象。

默认位置 `global.jsp` 为：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>CQ 5. `/libs/wcm/global.jsp`3及更早版本使用的路径现已过时。

### global.jsp、已使用的API和Taglibs的函数 {#function-of-global-jsp-used-apis-and-taglibs}

下面列出了从默认位置提供的最重要的对象 `global.jsp`:

摘要:

* `<cq:defineObjects />`

   * `slingRequest` -封装的请求对象( `SlingHttpServletRequest`)。
   * `slingResponse` -封装的响应对象( `SlingHttpServletResponse`)。
   * `resource` - Sling资源对象( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling资源解析器对象( `slingRequest.getResoucreResolver();`)。
   * `currentNode` -请求的已解析JCR节点。
   * `log` -默认记录器()。
   * `sling` - Sling脚本助手。
   * `properties` -已寻址资源的属性( `resource.adaptTo(ValueMap.class);`)。
   * `pageProperties` -已寻址资源页面的属性。
   * `pageManager` -用于访问AEM内容页面的页面管理器( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component` -当前AEM组件的组件对象。
   * `designer` -用于检索设计信息的设计器对象( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign` -已寻址资源的设计。
   * `currentStyle` -已寻址资源的样式。

### 访问内容 {#accessing-content}

在AEM WCM中，有三种访问内容的方法：

* 通过在以下位置引入的属性对象 `global.jsp`:

   属性对象是ValueMap的一个实例(请参 [阅Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html))，并包含当前资源的所有属性。

   示例：在页 `String pageTitle = properties.get("jcr:title", "no title");` 面组件的渲染脚本中使用。

   示例：在标 `String paragraphTitle = properties.get("jcr:title", "no title");` 准段落组件的渲染脚本中使用。

* 通过以 `currentPage` 下项中引入的对象 `global.jsp`:

   对 `currentPage` 象是页面的实例(请参阅 [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml))。 页面类提供了一些访问内容的方法。

   示例: `String pageTitle = currentPage.getTitle();`

* 通过 `currentNode` 在以下位置引入的对 `global.jsp`象：

   对 `currentNode` 象是节点的实例(请参 [阅JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html))。 可以通过该方法访问节点的属 `getProperty()` 性。

   示例: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP标签库 {#jsp-tag-libraries}

CQ和Sling标签库允许您访问特定函数，以用于模板和组件的JSP脚本。

有关详细信息，请参阅文档标 [记库](/help/sites-developing/taglib.md)。

## 使用客户端HTML库 {#using-client-side-html-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了客户端库文件夹 ****，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每类代码。 然后，客户端库系统负责在最终网页中生成正确的链接以加载正确的代码。

有关详细 [信息，请参阅文档使用客户端HTML库](/help/sites-developing/clientlibs.md) 。

## 对话框 {#dialog}

您的组件需要一个对话框供作者添加和配置内容。

有关更 [多详细信息，请参阅AEM组件](/help/sites-developing/components-basics.md#dialogs) -基础知识。

## 配置编辑行为 {#configuring-the-edit-behavior}

您可以配置组件的编辑行为。 这包括可用于组件的操作、就地编辑器的特性以及与组件上的事件相关的监听器等属性。 该配置对于触屏优化UI和经典UI都是通用的，尽管具有某些特定差异。

通过 [在组件节点（类型）下添加类型的节点](/help/sites-developing/components-basics.md#edit-behavior) ，并通过添加特定属性和子节点来配置 `cq:editConfig``cq:EditConfig``cq:Component`组件的编辑行为。

## 使用和扩展ExtJS构件 {#using-and-extending-extjs-widgets}

有关更 [多详细信息，请参阅使用和扩展ExtJS构件](/help/sites-developing/widgets.md) 。

## 为ExtJS构件使用xtypes {#using-xtypes-for-extjs-widgets}

有关更 [多详细信息](/help/sites-developing/xtypes.md) ，请参阅使用xtypes。

## 开发新组件 {#developing-new-components}

本节介绍如何创建您自己的组件并将其添加到段落系统中。

快速入门的方法是复制现有组件，然后进行所需的更改。

有关如何开发组件的示例在扩展文本和图像组 [件——一个示例中详细介绍。](#extending-the-text-and-image-component-an-example)

### 开发新组件（调整现有组件） {#develop-a-new-component-adapt-existing-component}

要基于现有组件为AEM开发新组件，您可以复制该组件，为新组件创建一个javascript文件，并将其存储在AEM可访问的位置(另请参阅自定义组件和 [其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. 使用CRXDE Lite，在以下位置创建一个新组件文件夹：

   / `apps/<myProject>/components/<myComponent>`

   像在库中一样重新创建节点结构，然后复制现有组件的定义，如文本组件。 例如，要自定义文本组件副本，请执行以下操作：

   * 起始日期: `/libs/foundation/components/text`
   * 到 `/apps/myProject/components/text`

1. 修改 `jcr:title` 以反映其新名称。
1. 打开新组件文件夹并进行所需的更改。 同时，删除文件夹中的任何无关信息。

   您可以进行以下更改：

   * 在对话框中添加新字段

      * `cq:dialog` -触屏优化UI的对话框
      * `dialog` -经典UI的对话框
   * 替换文 `.jsp` 件（在新组件后命名它）
   * 或完全重新处理整个组件（如果您希望）
   例如，如果您复制了标准文本组件，则可以向对话框中添加其他字段，然后更新该字段以处 `.jsp` 理在该处输入的内容。

   >[!NOTE]
   >
   >用于以下项目的组件：
   >
   >* 触屏优化UI使用 [Granite组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
   >* 经典UI使用 [ExtJS构件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >为经典UI定义的对话框将在触屏优化UI中运行。
   >
   >为触屏优化UI定义的对话框将不在经典UI中运行。
   >
   >根据您的实例和创作环境，您可能要为组件定义这两种类型的对话框。

1. 应当存在以下节点之一并正确初始化，以便显示新组件：

   * `cq:dialog` -触屏优化UI的对话框
   * `dialog` -经典UI的对话框
   * `cq:editConfig` -组件在编辑环境中的行为方式（例如拖放）
   * `design_dialog` -设计模式的对话框（仅限经典UI）

1. 通过以下任一方式在段落系统中激活新组件：

   * 使用CRXDE lite将值 `<path-to-component>` (例如， `/apps/geometrixx/components/myComponent`)添加到节点的属性组件 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 按照向段落系统添 [加新组件中的说明操作](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. 在AEM WCM中，打开网站中的页面，然后插入刚刚创建的类型的新段落，以确保组件正常工作。

>[!NOTE]
>
>要查看页面加载的计时统计信息，可使用Ctrl-Shift-U —— 在URL中 `?debugClientLibs=true` 设置该属性。

### 向段落系统添加新组件（设计模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

在开发组件后，可将其添加到段落系统中，这样作者就可以在编辑页面时选择并使用组件。

1. 例如，在您的创作环境中访问使用段落系统的页面 `<contentPath>/Test.html`。
1. 通过以下任一方式切换到“设计”模式：

   * 添 `?wcmmode=design` 加到URL末尾并再次访问，例如：

      `<contextPath>/ Test.html?wcmmode=design`

   * 单击Sidekick中的设计
   您现在处于设计模式，可以编辑段落系统。

1. 单击编辑。

   此时将显示属于段落系统的组件列表。 您的新组件也会列出。

   可以激活（或取消激活）组件，以确定在编辑页面时向作者提供的组件。

1. 激活您的组件，然后返回正常编辑模式以确认该组件可供使用。

### 扩展文本和图像组件——示例 {#extending-the-text-and-image-component-an-example}

本节提供了一个示例，说明如何使用可配置的图像放置功能扩展广泛使用的文本和图像标准组件。

文本和图像组件的扩展允许编辑使用组件的所有现有功能加上一个额外的选项来指定图像的位置：

* 在文本的左侧（当前行为和新的默认值）
* 在右侧

扩展此组件后，可以通过组件的对话框配置图像放置。

本练习介绍了以下技术：

* 复制现有组件节点并修改其元数据
* 修改组件的对话框，包括父对话框中构件的继承
* 修改组件的脚本以实现新功能

>[!NOTE]
>
>此示例针对经典UI。

>[!NOTE]
>
>此示例基于Geometrixx示例内容，该内容不再随AEM一起提供，但已被We.Retail替换。 有关如何下载 [和安装Geometrixx的信息，请参阅文档We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx) 。

#### 扩展现有文本时间组件 {#extending-the-existing-textimage-component}

要创建新组件，我们将使用标准文本时间组件作为基础并对其进行修改。 我们将新组件存储在Geometrixx AEM WCM示例应用程序中。

1. 将标准textimage组件从复制到Geometrixx `/libs/foundation/components/textimage` 组件文件夹中， `/apps/geometrixx/components`并使用textimage作为目标节点名称。 （通过导航到组件，右键单击并选择复制并浏览到目标目录，即可复制组件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 要使此示例简单明了，请导航到您复制的组件，并删除新文本时间节点的所有子节点，以下子节点除外：

   * 对话框定义： `textimage/dialog`
   * 组件脚本： `textimage/textimage.jsp`
   * 编辑配置节点（允许拖放资产）: `textimage/cq:editConfig`
   >[!NOTE]
   >
   >对话框定义取决于UI:
   >
   >* Touch-enabled UI: `textimage/cq:dialog`
   >* 经典 UI: `textimage/dialog`


1. 编辑组件元数据：

   * 组件名称

      * 设置为 `jcr:description``Text Image Component (Extended)`
      * 设置为 `jcr:title``Text Image (Extended)`
   * 组，其中组件列在Sidekick中（保持原样）

      * 保 `componentGroup` 持为 `General`
   * 新组件的父组件（标准文本时间组件）

      * 设置为 `sling:resourceSuperType``foundation/components/textimage`
   执行此步骤后，组件节点如下所示：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 更改图 `sling:resourceType` 像的编辑配置节点的属性(属性：) `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType``geometrixx/components/textimage.`

   这样，当将图像拖放到页面上的组件时，扩展文本 `sling:resourceType` 时间组件的属性将设置为： `geometrixx/components/textimage.`

1. 修改组件的对话框以包含新选项。 新组件会继承对话框中与原始组件相同的部分。 我们添加的唯一功能是扩展“高级 **** ”选项卡，添加“图像位置 **”下拉列表，其中包含“左”和“右** ”选项 ********:

   * 保留属 `textimage/dialog`性不变。
   请注意， `textimage/dialog/items` 如何有四个子节点（tab1到tab4），它们表示文本时间对话框的四个选项卡。

   * 对于前两个选项卡（tab1和tab2）:

      * 将xtype更改为cqinclude（从标准组件继承）。
      * 分别添加具有值和 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`值 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`的路径属性。
      * 删除所有其他属性或子节点。
   * 对于tab3:

      * 保留属性和子节点而不更改
      * 将新字段定义添加到类 `tab3/items`型的节点位置 `cq:Widget`
      * 为新节点设置以下属性（String类型）: `tab3/items/position`

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * 添加类 `position/options` 型的子节 `cq:WidgetCollection` 点以表示图像放置的两种选择，并在它下面创建两个类型的节点o1和o2 `nt:unstructured`。
      * 对于节 `position/options/o1` 点，请设置属性： `text` 到 `Left` 和 `value` 到 `left.`
      * 对于节 `position/options/o2` 点，请设置属性： `text` 到 `Right` 和 `value` 到 `right`。
   * 删除选项卡4。
   图像位置将作为表示段落的节 `imagePosition`点的属性保留在内容 `textimage` 中。 完成这些步骤后，组件对话框的外观如下：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 扩展组件脚本， `textimage.jsp`并额外处理新参数：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   我们将用为此标记生成自定义样式的新代码来替换强调的代码片段 *%>&lt;div class=&quot;image&quot;>&lt;%* 。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 将组件保存到存储库。 该组件已准备好进行测试。

#### 检查新组件 {#checking-the-new-component}

开发组件后，您可以将其添加到段落系统，这样作者就可以在编辑页面时选择并使用组件。 这些步骤允许您测试组件。

1. 在Geometrixx中打开页面，如“英语／公司”。
1. 单击Sidekick中的“设计”，切换到设计模式。
1. 通过单击页面中间的段落系统上的编辑，编辑段落系统设计。 将显示可放置在段落系统中的组件列表，其中应包括新开发的组件文本图像（扩展）。 通过选择段落系统并单击确定，将其激活。
1. 切换回编辑模式。
1. 将文本图像（扩展）段落添加到段落系统，使用示例内容初始化文本和图像。 保存更改。
1. 打开文本和图像段落的对话框，将“高级”选项卡上的“图像位置”更改为“右侧”，然后单击“确定”以保存更改。
1. 该段落将呈现，并且图像位于右侧。
1. 该组件现已准备好使用。

组件将其内容存储在公司页面的段落中。

### 禁用图像组件的上传功能 {#disable-upload-capability-of-the-image-component}

要禁用此功能，我们将使用标准图像组件作为基础并对其进行修改。 我们将新组件存储在Geometrixx示例应用程序中。

1. 将标准图像组件从复制 `/libs/foundation/components/image` 到Geometrixx组件文件夹中， `/apps/geometrixx/components`使用图像作为目标节点名称。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 编辑组件元数据：

   * 将 **jcr:title设置为**`Image (Extended)`

1. 导航至 `/apps/geometrixx/components/image/dialog/items/image`.
1. 添加新属性:

   * **名称**: `allowUpload`
   * **类型**: `String`
   * **值**: `false`
   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 单击“ **全部保存**”。 该组件已准备好进行测试。
1. 在Geometrixx中打开页面，如“英语／公司”。
1. 切换到设计模式并激活“图像（扩展）”。
1. 切换回编辑模式，并将其添加到段落系统。 在下一张图片上，您可以看到原始图像组件与您刚刚创建的图像组件之间的差异。

   原始图像组件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新图像组件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 该组件现已准备好使用。

