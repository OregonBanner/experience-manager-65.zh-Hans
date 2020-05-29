---
title: 基础组件
seo-title: 基础组件
description: 'null'
seo-description: 'null'
uuid: 3caf9123-ae58-4590-af2f-57ef076daf7f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: ea2a523e-8d26-4be4-822f-35f153e40308
docset: aem65
legacypath: /content/docs/en/aem/6-2/author/page-authoring/default-components/editmode
pagetitle: Foundation Components
translation-type: tm+mt
source-git-commit: 071f4a292343f0ad52ca3700c95bf60f03c307cc
workflow-type: tm+mt
source-wordcount: '7287'
ht-degree: 88%

---


# 基础组件 {#foundation-components}

>[!CAUTION]
>
>Most Foundation Components are now deprecated with AEM 6.5. See the [release notes](/help/release-notes/deprecated-removed-features.md) for further information.
>
>Adobe 建议在 AEM 项目中利用更现代且可扩展的[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。These are part of the [We.Retail sample content](/help/sites-developing/we-retail.md) and can also be [installed separately and used for development](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html) by your administrator.
>
>您可以使用AEM [现代化工具套件](https://opensource.adobe.com/aem-modernize-tools/) ，重新构建基于基础组件的站点以使用核心组件。

基础组件专门为在创作标准网页内容时使用而设计。这些组件构成了适用于标准 AEM 安装的现成组件的子集。

Some are immediately available through component browser, various others are also available by using [design mode](/help/sites-authoring/default-components-designmode.md) (if the page is based on a static template) or by [editing the template](/help/sites-authoring/templates.md) (if the page is based on an editable template).

支持使用基础组件，但它们大部分已被弃用并被核心组件取代，核心组件提供了更大的可扩展性和灵活性。

>[!NOTE]
>
>此部分仅讨论在标准 AEM 安装中现成可用的组件。
>
>根据您的实例，您可能已经拥有明确按照您的要求开发的自定义组件。这些组件甚至会与此处讨论的某些组件同名。

[编辑页面](/help/sites-authoring/editing-content.md)时，可以在页面编辑器侧面板的&#x200B;**组件**&#x200B;选项卡中使用组件。

您可以选择一个组件并将其拖动到页面上的所需位置。然后，可以使用以下方法编辑该组件：

* [配置属性](/help/sites-authoring/editing-page-properties.md)
* [编辑内容](/help/sites-authoring/editing-content.md)

* [编辑内容 - 全屏模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

组件会根据称为组件组的各种类别进行分类，具体包括：

* [常规](#general)：包括基本组件，例如文本、图像、表、图表等。
* [列](#columns)：包括组织内容布局所需的组件。
* [表单](#formgroup)：包括创建表单所需的所有组件。

## 常规 {#general}

常规组件是指用于创建内容的基本组件。

### 帐户项 {#account-item}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

您可以为链接定义标题和描述。

![chlimage_1-88](assets/chlimage_1-88.png)

### 自适应图像 {#adaptive-image}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[图像核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html)。

“自适应图像”基础组件生成的图像的大小会被调整至适应打开网页的窗口。要使用该组件，可以从文件系统或 DAM 提供图像资源。打开网页后，Web 浏览器将下载该图像的一个副本，且大小已调整至适合当前窗口。

以下特性可决定窗口的大小：

* 设备屏幕：移动设备在显示网页时通常会延伸至整个屏幕。
* Web 浏览器窗口大小：笔记本电脑和台式机的用户可以调整 Web 浏览器窗口的大小。

例如，当在手机上打开网页时，该组件会生成一个小图像，而在平板电脑上打开时则会生成一个中等大小的图像。在笔记本电脑上，当页面在最大化的 Web 浏览器中打开时，组件将创建并提供一个大图像。当 Web 浏览器的大小调整至适应部分屏幕时，该组件会适应性地提供较小图像并刷新视图。

#### 支持的图像格式 {#supported-image-formats}

您可以将包含以下文件扩展名的图像文件用于自适应图像组件：

* .jpg
* .jpeg
* .png
* .gif **

>[!CAUTION]
>
>GIF 动图文件在 AEM 中不可进行自适应呈现。

#### 图像大小和质量 {#images-sizes-and-quality}

下表列出了针对给定视图端口宽度生成的图像的宽度：系统将计算生成的图像的高度，保持宽高比不变，且图像边缘内部没有空白。可使用裁剪避免空白的出现。

当图像为 JPEG 图像时，视图端口大小也可能影响 JPEG 质量。JPEG 有如下几种质量：

* 低 (0.42)
* 中 (0.82)
* 高 (1.00)

| **视图端口宽度范围（像素）** | **图像宽度（像素）** | **JPEG 质量** | **目标设备类型** |
|---|---|---|---|
| 宽度 &lt;= 319 | 320 | 低 |  |
| 宽度 = 320 | 320 | 中 | 移动手机（纵向） |
| 320 &lt; 宽度 &lt; 481 | 480 | 中 | 移动手机（横向） |
| 480 &lt; 宽度 &lt; 769 | 476 | 高 | 平板电脑（纵向） |
| 768 &lt; 宽度 &lt; 1025 | 620 | 高 | 平板电脑（横向） |
| 宽度 &lt;= 1025 | 全屏幕（原始大小） | 高 | 桌面设备 |

#### 属性 {#properties}

该对话框允许您为自适应图像组件的实例编辑属性，其中很多属性都与其基于的图像组件的属性相同。这些属性位于两个选项卡中：

* **图像**

   * **图像**
从内容查找器中拖动图像，或单击打开浏览窗口以从中加载图像。图像加载后，您可以裁剪、旋转或删除该图像。要放大和缩小图像，请使用图像下方的滚动条（在“确定”和“取消”按钮上方）。

   * **裁剪**
裁剪图像。拖动边框可裁剪图像。

   * **旋转**
连续单击“旋转”，直到图像旋转至所需外观为止。

   * **清除**&#x200B;删除当前图像。

* **高级**

   * **标题**
自适应图像组件不使用此属性。

   * **替换文本**
用于图像的替换文本。

   * **链接到**
自适应图像组件不使用此属性。

   * **说明**
自适应图像组件不使用此属性。

#### 扩展自适应图像组件 {#extending-the-adaptive-image-component}

有关自定义自适应图像组件的信息，请参阅[了解自适应图像组件](/help/sites-developing/responsive.md#using-adaptive-images)。

### 轮播 {#carousel}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[轮播核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)。

传送组件允许您通过以下方式显示与单个页面关联的图像：

* 每次显示一幅图像
* 短时间显示
* 按指定的顺序显示
* 在指定的延迟时间后显示

可单击控件还允许用户按需实时地循环查看显示的页面。单击当前可见的页面图像即可跳转到该页面。换言之，“传送”可充当导航控件。

#### 属性 {#properties-1}

这些属性位于两个选项卡中：

* **传送**
在此处，可以指定传送的操作方式：

   * 播放速度
显示下一张幻灯片之前停留的时间（以毫秒为单位）。
   * 过渡时间
两张幻灯片之间的过渡时间（以毫秒为单位）。
   * 控件样式
下拉菜单中提供了多种选项；例如，上一个/下一个按钮、右上切换。

* **列表**

   在此，您可以指定页面在传送中的包含方式：

   * **生成列表对象**
生成页面列表的方式有若干种：使用“子页面”、“固定列表”、“搜索”或“高级搜索”（所有方式如下所述）。
请注意，无论选择哪种方式，包含在列表中的页面均应具有与此页面关联的图像，传送中将显示该图像。如果给定页面的“页面属性”下没有该页面的图像，则应在开始操作之前将图像与页面相关联，否则传送将显示空白（或大部分为空白）的页面。请参阅[编辑页面属性](/help/sites-authoring/editing-page-properties.md)。
根据您选择的项目，将显示一个新面板：

      * **子页面选项**

         * **父页面**
手动或使用选择器指定一个路径。如果将此选项留空，则使用当前页面作为父页面。
      * **固定列表选项**

         * **页面**&#x200B;选择页面列表。 使 `+` 用添加更多条目和上／下按钮来调整顺序。
      * **搜索选项**

         * **开始**
手动或使用选择器输入一个开始路径。

         * **搜索查询**
可以输入纯文本搜索查询。
      * **高级搜索选项**

         * **QueryBuilder 谓词记号**
可以使用“QueryBuilder 谓词记号”输入搜索查询。例如，您可以输入“fulltext=Marketing”，以使内容带有“Marketing”的所有页面都显示在传送中。
有关查询表达式的完整说明和更多示例，请参阅 [QueryBuilder API](/help/sites-developing/querybuilder-api.md)。
   * **排序依**&#x200B;据 `jcr:title`从下 `jcr:created`拉菜 `cq:lastModified`单中选 `cq:template` 择、、或。

   * **限制**
您希望在传送中使用的最多项目数；这是可选项。





>[!NOTE]
>
>您可以为 Adobe Experience Manager 创建一个自定义传送组件，使其显示位于 AEM DAM 中的数字资产。有关信息，请参阅[为 Adobe Experience Manager 创建自定义传送组件](https://helpx.adobe.com/experience-manager/using/custom-carousel-components.html)。

### 图表 {#chart}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

图表组件允许您添加条形图、折线图或饼图。AEM 可根据您提供的数据创建图表。您可通过在“数据”选项卡中直接键入或通过复制并粘贴电子表格来提供数据。

* **数据**

   * **图表数据**
使用 CSV 格式输入您的图表数据；逗号分隔值格式使用逗号（“,”）作为字段分隔符。

* **高级**

   * **图表类型**
从饼图、折线图和条形图中进行选择。

   * **替换文本**
显示的用于替代图表的替换文本。

   * **宽度**
图表的宽度（以像素为单位）。

   * **高度**
图表的高度（以像素为单位）。

下面显示了一个图表数据示例，其后是生成的条形图：

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
>
>您可以创建一个自定义 AEM 图表控件来显示位于 AEM JCR 中的数据。有关信息，请参阅[在图表中显示 Adobe Experience Manager 数据](https://helpx.adobe.com/experience-manager/using/displaying-experience-manager-data-chart.html)。

### 内容片段 {#content-fragment}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[内容片段核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)。

[内容片段](/help/sites-authoring/content-fragments.md)将作为独立于页面的资产来创建和管理。您随后可以在创作内容页面时使用这些片段及其变量。

### 设计导入程序 {#design-importer}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此组件允许您上传含有设计包的 zip 文件。

### 下载 {#download}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

下载组件可在所选网页上创建下载指定文件的链接。您可以从内容查找器中拖动资产或上传文件。

* **下载**

   * **说明**
随下载链接一起显示的简短说明。

   * **文件**
在生成的网页上可供下载的文件。从内容查找器中拖动资产或单击相应区域以上传可供下载的文件。

以下示例显示 Geometrixx 中的下载组件：

![dc_download_use](assets/dc_download_use.png)

### 外部 {#external}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

外部应用程序集成组件（**外部**）允许您使用 iFrame 将外部应用程序嵌入到您的 AEM 页面。

* **外部**

   * **目标应**&#x200B;用程序指定要集成的Web应用程序的URL; 例如：

      ```
      https://en.wikipedia.org/wiki/Main_Page
      ```

   * **传递参数**
根据需要选中要传递到应用程序的参数所对应的框。

   * **宽度和高度**定义iframe的大小

外部应用程序会集成到 AEM 页面的段落系统；例如，在使用目标应用程序 `https://en.wikipedia.org/wiki/Main_Page` 时：

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>根据您的用例，还有其他选项可用于外部应用程序的集成，例如，[Portlet 的集成](/help/sites-administering/aem-as-portal.md)。

### Flash {#flash}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

Flash 组件允许您加载 Flash 影片。您可以从内容查找器中将 Flash 资产拖动到组件上，也可以使用对话框：

* **Flash**

   * **Flash 影片**

      Flash 影片文件。从内容查找器中拖动资产，或者单击以打开浏览窗口。

   * **大小**

      支持影片的显示区域的尺寸（以像素为单位）。

* **备用图像**

   要显示的备用图像

* **高级**

   * **上下文菜单**

      指示是否应显示或隐藏上下文菜单。

   * **窗口模式**

      窗口的显示方式，例如不透明、透明或显示为独立（实底）窗口。

   * **背景颜色**

      从提供的颜色图表中选择的背景颜色。

   * **最低版本**

      运行影片所需的 Adobe Flash Player 的最低版本。默认数量为 9.0.0。

   * **属性**

      任何其他所需的属性。

### 图像 {#image}

>[!CAUTION]
>
>此基础组件已被弃用。Adobe 建议改用[图像核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html)。

图像组件可根据指定的参数显示图像和相应文本。

您可以上传图像，然后编辑和处理该图像（例如裁剪、旋转、添加链接/标题/文本）。

您可以从[资产浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)中将图像直接拖放到组件上或其[“配置”对话框](/help/sites-authoring/editing-content.md#component-edit-dialog)中。此外，也可以从“配置”对话框中上传图像；此对话框还控制着图像的所有定义和操作：

![chlimage_1-91](assets/chlimage_1-91.png)

上传图像之后（不是之前），您可以根据需要使用[就地编辑](/help/sites-authoring/editing-content.md#edit-content)功能裁剪/旋转图像：

![](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>就地编辑器在编辑时使用图像的原始大小和长宽比。 您还可以指定高度和宽度属性。 在保存编辑更改时，将应用属性中定义的所有大小和长宽比限制。

>根据您的实例，[页面设计](/help/sites-developing/designer.md)还可能会强制应用最小和最大限制；这些限制在项目实施过程中开发。
>
还有其他几个选项在全屏编辑模式下可用；例如，地图和缩放：

![](do-not-localize/chlimage_1-16.png)

>[!NOTE]
无法使用 Internet Explorer 监控上传过程。
Internet Explorer 用户需要上传图像，单击&#x200B;**确定**，然后重新打开图像，以预览方式查看已上传的文件，并进行修改（即裁剪）。

>See the [Certified Platforms](/help/release-notes/release-notes.md#certifiedplatforms) section for more information about HTML5 features used by AEM.

加载图像后，您可以配置下列各项：

* **地图**

   要映射图像，请选择“映射”。 您可以指定创建图像映射的方式（矩形、多边形等）以及该区域应指向的位置。

* **裁剪**

   选择裁剪以裁剪图像。 可使用鼠标裁剪图像。

* **旋转**

   要旋转图像，请选择“旋转”。 连续使用“旋转”，直到图像旋转成您需要的外观。

* **清除**

   删除当前图像。

* **标题**

   图像的标题。

* **替换文本**

   用于创建辅助内容的替代文本。

* **链接到**

   创建指向资产或网站中其他页面的链接。

* **描述**

   对图像的说明。

* **大小**

   设置图像的高度和宽度。

>[!NOTE]
有些选项仅在全屏编辑器中可用。

最终图像（带有&#x200B;**标题**&#x200B;和&#x200B;**说明**）可能如下所示：

![chlimage_1-92](assets/chlimage_1-92.png)

### 布局容器 {#layout-container}

此组件提供了一种网格段落系统，让您可以在[响应式网格](/help/sites-authoring/responsive-layout.md)内添加和放置组件。这样，您就可以根据目标设备（包括一系列手机、平板电脑和台式机）的宽度来定义不同的内容布局。

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
此组件已通过 [HTML 模板语言 (HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) 进行了实施。

### 列表 {#list}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[列表核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)。

列表组件允许您配置用于显示列表的搜索条件：

* **列表**

   * **生成列表对象**

      您可在此指定列表将检索其内容的位置。有下列几种方法：

   * 根据您选择的项目，将显示一个新面板：

      * **子页面选项**

         * **子项** （父页面）

            手动或使用选择器指定一个路径。 如果将此选项留空，则使用当前页面作为父页面。
      * **固定列表选项**

         * **页面**

            选择页面列表。 使用 + 添加更多条目，然后使用向上/向下按钮调整顺序。
      * **搜索选项**

         * 开始

            手动或使用选择器输入起始路径。

         * 搜索查询

            您可以输入纯文本搜索查询。
      * **高级搜索选项**

         * **QueryBuilder 谓词记号**

            您可以使用QueryBuilder谓词记号输入搜索查询。 例如，您可以输入“fulltext=Marketing”，以使内容带有“Marketing”的所有页面都显示在传送中。


            有关查询表达式的完整说明和更多示例，请参阅 [QueryBuilder API](/help/sites-developing/querybuilder-api.md)。
      * **标记**

         Specify the **Parent page**, **Tags/Keywords** and your required match criteria.
   * **显示方式**

      希望列出项目的方式；包括链接、Teaser 和新闻。

   * **排序依据**

      是否要对列表进行排序，如需要，可将该条件用于排序。您可以输入条件或从提供的下拉列表中选择一个。

   * **限制**

      指定您希望在列表中显示的最大项目数。

   * **启用信息源**

      指示是否应为列表激活 RSS 源。

   * **每页显示条目数**

      您可立即在此指定要显示的列表项目数。所含项目多于指定数量的列表将使用分页以多个部分显示列表。






以下示例以显示子页面列表的方式展示了&#x200B;**列表**&#x200B;组件（设计由站点设计的自定义 CSS 定义来控制）。

![dc_列表_use](assets/dc_list_use.png)

### 登录 {#login}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此组件提供了“用户名”和“密码”字段。

![chlimage_1-94](assets/chlimage_1-94.png)

您可以配置：

* 登录

   * 区域标签

      输入字段的导入文本。

   * 用户名标签

      用于标记用户名字段的文本。

   * 密码标签

      用于标记密码字段的文本。

   * “登录”按钮标签

      登录按钮的文本。

   * 重定向到

      您可以指定用户登录后应打开的网站页面。

* 已登录

   * “继续”按钮标签

      用于指示用户已登录的文本。

### 订单状态 {#order-status}

* **标题**

   * **标题**

      指定要显示的标题文本。

   * **链接**

      指定应显示订单状态的页面（产品）。

   * **类型/大小**

      从提供的选择中进行选择。

![chlimage_1-95](assets/chlimage_1-95.png)

### 针对开发人员的 Adobe AIR API 参考 {#reference}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[内容片段核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)。

使用&#x200B;**引用**&#x200B;组件可以从 AEM 网站的其他页面引用文本（在当前实例中）。引用的段落内容会像在当前页面上一样进行显示。当源段落发生更改时，此内容也将随之更新（可能需要刷新页面）。

* **段落引用**

   * **针对开发人员的 Adobe AIR API 参考**

      指定要引用的页面和段落的路径（包括内容）。

要指定段落的路径，您需要在（页面的）路径后面附加以下后缀：

`.../jcr:content/par/<paragraph-ID>`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

除了引用特定段落以外，还可以通过修改路径来指定整个段落系统。要指定整个段落系统，您需要在路径后面附加以下后缀：

`/jcr:content/par`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

完成配置后，该内容将像在源页面上一样进行显示。只有在打开组件进行编辑时，才能看出它是引用内容：

![chlimage_1-96](assets/chlimage_1-96.png)

### 搜索 {#searching}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[快速搜索核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/quick-search.html)。

搜索组件会向您的页面添加搜索功能。

您可以配置：

* 搜索

   * **节点类型**

      If the search is to be restricted to specific node type list them here; for example, `cq:Page`.

   * **搜索路径**

      指定要搜索的分支的根页面。

   * **搜索按钮文本**

      名称显示在实际的搜索按钮上。

   * **统计数据文本**

      文本显示在搜索结果上方。

   * **无结果文本**

      如果没有任何结果，将显示在此输入的文本。

   * **拼写检查文本**

      如果某人输入类似术语，则此文本将显示在该术语前面。例如，如果您键入 geometrixxe，则系统会显示“是否要：geometrixx”。

   * **类似的页面文本**

      类似页面的结果旁显示的文本。单击此链接可查看具有类似内容的页面。

   * **相关的搜索文本**

      相关术语和主题的搜索旁显示的文本。

   * **搜索趋势文本**

      用户输入的搜索词上方的标题。

   * **结果页面标签**

      在此列表底部显示的文本，带有指向其他结果页的链接。

   * **上一标签**

      指向先前的搜索页的链接上显示的名称。

   * **下一标签**

      指向随后的搜索页的链接上显示的名称。

以下示例显示了从标准安装的根目录中搜索单词 *geometrixx* 后的“搜索”组件。该示例还说明了结果分页情况：

![dc_search_use](assets/dc_search_use.png)

以下示例演示了一个拼写错误且无效的搜索词：

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Sitemap {#sitemap}

>[!CAUTION]
此基础组件已被弃用。Adobe recommends leveraging the [Navigation](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/navigation.html), [Language Navigation](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/language-navigation.html), and [Breadcrumb Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/breadcrumb.html) instead.

自动 Sitemap 列表，该列表（具有默认设置）列出了当前网站中的所有页面（作为活动链接）。例如，提取结果如下所示：

![dc_sitemap_use](assets/dc_sitemap_use.png)

如果需要，您可以配置：

* **Sitemap**

   * **根路径**

      列表从中开始的路径。

### Slideshow {#slideshow}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[轮播核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)。

此组件允许您加载一系列将在您的页面上显示为幻灯片放映的图像。您可以添加或删除图像以及为每个图像指定标题。在“高级”下，您还可以指定显示区域的大小。

您可以配置：

* **幻灯片**

   * **新幻灯片**

      You can specify a selection of slides using the **Add** (and **Remove**) buttons.

   * **标题**

      根据需要指定标题。 此标题会覆盖在相应的幻灯片上。

* **高级**

   * **大小**

      以像素为单位指定宽度和高度。

幻灯片放映组件随后会在较短的时间内按顺序重复显示每个图像，然后淡入到下一张幻灯片：

![dc_slideshow_use](assets/dc_slideshow_use.png)

### 表 {#table}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html)。

>[!NOTE]
与&#x200B;**[文本](#text)**基础组件一样，**表**基础组件也基于[富文本编辑器](/help/sites-authoring/rich-text-editor.md)。

**表**&#x200B;组件经过预配置，让您可以构建和填写表，以及设置表的格式。使用对话框，您可以配置表，并通过以下任一方式创建内容：

* 从头开始创建
* 从外部编辑器（例如 Excel、OpenOffice、Notepad 等）复制并粘贴电子表格或表。

您可以使用内嵌编辑器对内容进行基本更改：

![dc_table](assets/dc_table.png)

在全屏模式下，您可以配置表格布局：

![chlimage_1-97](assets/chlimage_1-97.png)

以下屏幕快照显示了表组件的示例；其设计取决于特定于站点的 CSS：

![dc_table_use](assets/dc_table_use.png)

### 标记云 {#tag-cloud}

标记云以图表形式呈现应用于网站内容的所选标记：

![dc_tagclouduse](assets/dc_tagclouduse.png)

配置“标记云”组件时，您可以指定：

* **要显示的标记**

   要显示的标记从中收集的位置。从含有所有子项或所有标记的页面进行选择。

* **页面**

   选择要引用的页面。

* **标记上无链接**

   显示的标记是否应作为链接。

有关应用标记的更多信息，请访问[使用标记](/help/sites-authoring/tags.md)。

### 文本 {#text}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html)。

>[!NOTE]
与&#x200B;**表**&#x200B;基础组件一样，**文本**&#x200B;基础组件也基于[富文本编辑器](/help/sites-authoring/rich-text-editor.md)。

通过文本组件可以使用所见即所得 （WYSIWYG) 编辑器输入文本块，相应编辑器功能由[富文本编辑器](/help/sites-authoring/rich-text-editor.md)提供。通过精选的图标可以设置文本格式，包括字体特性、对齐方式、链接、列表和缩进。

![chlimage_1-98](assets/chlimage_1-98.png)

When you open the **Configure** dialog, you can also set:

* **分隔条**
* **文本样式**

已设置格式的文本随后将显示在页面上；实际设计将取决于站点 CSS：

![dc_text_use](assets/dc_text_use.png)

有关文本组件和富文本编辑器所提供功能的更多详细信息，请参阅[富文本编辑器](/help/sites-authoring/rich-text-editor.md)页面。

#### 就地编辑 {#inplace-editing}

除了基于对话框的富文本编辑模式以外，AEM 还提供了[就地编辑](/help/sites-authoring/editing-content.md)模式，当文本在页面布局中显示时，可以通过该模式直接编辑文本。

### 文本和图像 {#text-image}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[图像](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html)和[文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html)。

文本和图像组件可添加文本块和图像。您也可以将文本和图像分开添加和编辑。有关详细信息，请参阅[文本](#text)组件和[图像](#image)组件。

![chlimage_1-99](assets/chlimage_1-99.png)

您可以配置：

* **组件样式** (**样式**)

   您可在此左对齐或右对齐图像。默认为&#x200B;**左**&#x200B;对齐，图像位于左侧。

* **图像属性** (**高级图像属性**)

   允许您指定以下内容：

   * **图像资产**

      上传所需的图像。

   * **标题**

      块标题；鼠标悬停时将显示。

   * **替换文本**

      无法显示图像时将显示的替换文本。如果留空，则将使用该标题。

   * **链接到**

      指定目标路径。

   * **描述**

      对图像的说明。

   * **大小**

      设置图像的高度和宽度。

以下示例显示了图像左对齐的文本图像组件：

![dc_textimage_use](assets/dc_textimage_use.png)

### 标题 {#title}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[标题核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)。

标题组件可以：

* 显示当前页的名称；可通过将标题字段留空来实现这一点
* 显示您在标题字段中指定的文本。

您可以配置：

* **标题**

   如果您要使用页面标题之外的名称，请在此输入该名称。

* **链接**

   如果标题将作为链接运行，则输入 URI。

* **类型/大小**

   从下拉列表中选择“小”或“大”。“小”生成为图像。“大”生成为文本。

以下示例演示将要显示的&#x200B;**标题**&#x200B;组件；设计取决于站点特定的 CSS。

![dc_title_use](assets/dc_title_use.png)

### 视频 {#video}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

**视频**&#x200B;组件允许您在页面上放置一个预定义的现成视频元素。

另请参阅[配置视频配置文件](/help/sites-administering/config-video.md#configuringvideoprofiles)以便与 HTML5 元素结合使用。

在将组件的实例放置到页面上后，您可以配置：

* 视频

   * **视频资产**

      上传或删除视频资产。

   * **大小**

      视频固有的大小（宽 x 高，以像素为单位）将出现在“大小”（参阅上文）旁边的框中。如果要覆盖视频固有的尺寸，请在此处手动输入宽度和高度尺寸。单击&#x200B;**确定**&#x200B;关闭对话框。

>[!NOTE]
支持的格式包括：
* `.mp4`
* `Ogg`
* `FLV` （Flash视频）


## 列 {#columns}

列是控制 AEM 中内容布局的机制。标准安装中提供了用于创建 2 列和/或 3 列的组件。

以下示例显示了使用的 2 列组件。您可以将占位符用于新组件：

![dc_columncontroluse](assets/dc_columncontroluse.png)

### 2 列 {#columns-1}

默认为 2 个相等列的列控件组件。

### 3 列 {#columns-2}

默认为 3 个相等列的列控件组件。

### 列控件 {#column-control}

列控件组件允许用户选择如何将网页主面板中的内容拆分为多个列。用户可以选择所需的列数（从预定义的列表中），然后创建、删除或移动每个列中的内容。

* **列控件**

   * **列布局**

      选择您要呈现的列数。创建后，每列都有自己的链接，用于在添加内容时拖动组件或资产。

## 表单 {#form}

>[!CAUTION]
组件中的基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

表单组件用于为访客创建表单以提交输入。表单和表单组件可用于收集用户反馈（例如，客户满意度调查问卷）和用户信息（例如，用户注册）等信息。

>[!NOTE]
请参阅 [AEM 表单帮助](/help/forms/home.md)，以获取有关 AEM 表单的信息。

表单是从多个不同组件中构建的：

* **表单**

   表单组件定义页面上新表单的开始和结尾。其他组件稍后可放置在这些元素之间，例如表格、下载等。

* **表单字段和元素**

   表单字段和元素可以包括文本框、单选按钮、图像等。用户通常在表单字段中完成操作，例如键入文本。有关详细信息，请参阅单个表单元素。

* **个人资料组件**

   与访客个人资料相关的个人资料组件用于社交协作以及需要访客个人信息的其他区域。

下面显示了一个表单示例。它由&#x200B;**表单**&#x200B;组件（开始和结尾）组成，其中包含两个用于输入内容的&#x200B;**表单****文本**&#x200B;字段、一个用于引导文本的&#x200B;**常规****文本**&#x200B;字段以及一个&#x200B;**提交**&#x200B;按钮。

![dc_form](assets/dc_form.png)

>[!NOTE]
有关开发和进一步自定义表单的信息，请参阅[开发表单](/help/sites-developing/developing-forms.md)页面。相关信息包括添加操作和约束，预载字段以及通过使用脚本调用服务的方式执行操作，等等。

### （许多）表单组件的常规设置 {#settings-common-to-many-form-components}

尽管每个表单组件都具有不同的用途，但许多表单组件都由相似的选项和参数构成。

配置任意表单组件时，对话框中都提供有下列选项卡：

* **标题与文本**

   您需要在此指定基本信息，例如表单的标题以及任何附带的文本。在适当情况下，该选项卡还允许您定义其他重要信息，例如字段是否可多选以及可供选择的项目。

* **初始值**

   允许您指定默认值。

* **约束**

   您可以在此指定字段是否为必填字段以及对该字段进行约束（例如，必须为数字等）。

* **样式**

   指示字段的大小和样式。

>[!NOTE]
您看到的字段差别很大，具体取决于各个组件。

这些选项卡为您提供必需的参数；具体的选项卡依各个组件类型而定，但可能包括：

* **标题与文本**

   * **元素名称**

      表单元素的名称。该选项卡指示数据在存储库中的存储位置。这是必填字段，只能包含下列字符：

      * 字母数字字符
      * `_ . / : -`
   * **标题**

      显示的字段标题。如果保留为空，则将显示默认标题。

   * **描述**

      允许您根据需要提供用户的其他信息。说明在表单上的字段下方显示，其字体比标题字体小。

   * **显示/隐藏**

      确定字段何时可见。


* **初始值**

   * **默认值**

      打开表单时字段中显示的值；即在用户输入任何内容前显示的值。

* **约束**

   * **必填**

      这取决于表单组件类型，但提供一个或多个单击框以指示该字段或该字段的某些部分是必需的。

   * **必需的消息**

      通知用户此字段为必填字段的消息； 必填字段还将标有星号和星号。

   * **约束**

      可供选择的约束取决于表单组件类型。

   * **约束消息**

      用于通知用户所需内容的消息。

* **样式**

   * **大小**

      在行和列中。

   * **宽度**

      按像素。

   * **CSS**

### 表单（组件） {#form-component}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单容器核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-container.html)。

表单组件使用&#x200B;**表单开始**&#x200B;和&#x200B;**表单结尾**&#x200B;元素定义表单的开始和结尾。它们始终是成对的，以确保正确定义表单。

![dc_form-1](assets/dc_form-1.png)

在表单开始和表单结尾之间，您可以添加表单组件，用于定义用户实际输入的字段。

>[!NOTE]
基础组件表单组件仅支持使用其他基础组件表单组件（按钮、文本、隐藏等）。不支持在基础组件表单中使用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)表单组件（反之亦然）。

#### 表单开始 {#start-of-form}

定义页面上新表单的开始时需要此组件。您可以配置：

* **表单**

   * **感谢页面**

      为感谢访客提供其意见而引用的页面。如果留空，表单将在提交后重新显示。

   * **启动工作流**

      决定提交表单后将触发哪个工作流。

* **高级**

   * **操作类型**

      一个表单需要一项操作。此操作定义执行用户提交数据时触发的操作（与 HTML 中的 action= 类似）。有些操作需要相应的&#x200B;**操作配置**。
标准 AEM 安装中包含以下操作类型选项：

      * **帐户请求**
      * **创建内容**
      * **创建潜在客户**
      * **创建和更新帐户**
      * **电子邮件服务: 创建订阅者并添加到列表**
      * **电子邮件服务: 发送自动回复的电子邮件**
      * **电子邮件服务: 使用户从列表中取消订阅**
      * **编辑社区**
      * **编辑资源**
      * **编辑工作流控制的资源**
      * **邮件**
      * **所下的订单明细**
      * **个人资料更新**
      * **重置密码**
      * **设置密码**
      * **存储内容**

         这是默认操作类型。

      * **通过上传存储内容**
      * **提交订单**
      * **取消订阅者的订阅**
      * **更新订单**
   * **表单标识符**

      表单标识符可唯一标识表单。单个页面上具有多个表单时，应使用表单标识符；请确保它们具有不同的标识符。

   * **加载路径**

      用于将预定义值加载到表单字段中的节点属性的路径。

      这是指定库中节点的路径的可选字段。如果此节点具有与字段名称相匹配的属性，则表单上的相应字段将随这些属性的值预加载。如果不存在任何匹配，则字段将包含默认值。

      使用&#x200B;**加载路径**，您可以预载必填字段中包含值的表单。请参阅[预载表单值](/help/sites-developing/developing-forms.md#preloading-form-values)。

   * **客户端验证**

      指示此表单是否需要客户端验证（*始终*&#x200B;进行服务器验证）。结合&#x200B;**表单 Captcha** 组件可以实现这一点。

   * **验证资源类型**

      如果您要验证整个表单（而非单个字段），则定义表单验证资源类型。如果您要验证完整表单，还应包含以下任一内容：

      * 客户端验证的脚本：

         `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * 服务器端验证的脚本：

         `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`
   * **操作配置**

      The options available in **Action Configuration** are dependent on the **Action Type** selected:

      * **帐户请求**

         * **创建帐户页**

            创建新帐户时使用的页面。
      * **创建内容**

         * 内容路径

            表单转储的任何内容的内容路径。Enter a path that ends with a slash `/`. 斜杠表示对于每个表单端口而言，新节点是在给定位置创建的；例如：

            `/forms/feedback/`

         * **类型**

            选择所需的类型。

         * **表单**

            指定表单。

         * **呈现工具**

            从列表中选择所需的选项。

         * **资源类型**

            如果设置此项，则此项将作为 `sling:resourceType`

         * **视图选择器**
      * **创建潜在客户**

         * **潜在客户会添加到此列表中**

            指定所需的潜在客户列表。
      * **创建和更新帐户**

         * **初始的组**

            要将新用户分配到的组。

         * **主页**

            成功登录后显示的页面。

         * **路径**

            创建和存储新帐户的路径（相对）。

         * **查看数据...**

            单击此按钮可访问有关批量编辑器中表单结果的信息。From here, you can export the information to a `.tsv` (tab-separated) file (for use, for example, in an Excel spreadsheet).
      * **邮件**

         * **从**

            输入电子邮件应来自的电子邮件地址。

         * **发送到**

            输入表单被发送到的电子邮件地址。

         * **抄送**

            输入抄送电子邮件地址。

         * **密送**

            输入密送电子邮件地址。

         * **主题**

            输入电子邮件的主题。
      * **重置密码**

         * **更改密码页**

            更改密码时使用的页面。
      * **存储内容**

         * **内容路径**

            表单转储的任何内容的内容路径。Enter a path that ends with a slash `/`. 斜杠表示对于每个表单端口而言，新节点是在给定位置创建的；例如：
            `/forms/feedback/`

         * **查看数据...**

            单击此按钮可访问有关批量编辑器中表单结果的信息。从此处，您可以将信息导出到。tsv（制表符分隔）文件（例如，在Excel电子表格中使用）。
      * **通过上传存储内容**

         此选项与“存储内容” **选项相同**。

      * **取消订阅者的订阅**

         * **潜在客户将从此列表中删除**

            指定所需的潜在客户列表。










#### 表单结尾 {#end-of-form}

此组件标记表单的结尾。您可以配置：

* **表单结尾**

   * **显示提交按钮**

      指示是否应显示“提交”按钮。

   * **提交名**

      如果您要在一个表单中使用多个提交按钮，则应使用标识符。

   * **提交标题**

      按钮上显示的名称，例如“提交”或“发送”。

   * **显示重置按钮**

      选中复选框可使重置按钮可见。

   * **重置标题**

      重置按钮上显示的名称。

   * **描述**

      按钮下方显示的信息。

### 帐户名称 {#account-name}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-text.html)。

此组件允许用户输入帐户名称：

![dc_form_accountname](assets/dc_form_accountname.png)

### 地址 {#address}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-text.html)。

此组件允许您采用以下格式添加国际地址字段：

![dc_form_addresfield](assets/dc_form_addressfield.png)

组件配置为立即使用，但您可以根据需要更改配置。例如，可以为地址的单个元素添加约束。将字段留空将使用默认设置。

### Captcha {#captcha}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

Captcha 组件需要用户键入屏幕上所示的字母数字字符串。该字符串会随每次刷新而变。

![dc_form_captcha](assets/dc_form_captcha.png)

您可为此组件配置不同参数，包括当 captcha 字符串无效时将显示的消息。

### 复选框组 {#checkbox-group}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单选项核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-options.html)。

通过复选框可以生成一个或多个复选框的列表，其中某些复选框可以同时选中。

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

您可以指定各种参数，包括标题、说明和元素名称。您可以使用 + 和 - 按钮添加或删除项目，然后使用向上和向下箭头定位这些项目。

>[!NOTE]
使用&#x200B;**项目加载路径**，您可以预加载值的复选框组列表。
请参阅[预载包含多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 信用卡详细信息 {#credit-card-details}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此组件允许您提供输入信用卡详细信息所需的字段。您可以对其进行配置，以指定接受的卡类型和所需的信息（例如，安全码）。

![chlimage_1-100](assets/chlimage_1-100.png)

### 下拉列表 {#dropdown-list}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单选项核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-options.html)。

可以配置下拉列表，为您提供一系列值供您选择：

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

您可以指定标题以及要在列表中显示的项目。使用 + 和 - 按钮，可以添加或删除列表项目，然后使用向上和向下按钮定位这些项目。您可以指定是否允许用户从列表中选择多个项目，还可以指定用户首次打开列表时应自动选择的项目（初始值）。

>[!NOTE]
使用&#x200B;**项目加载路径**，您可以预载包含值的下拉列表。
请参阅[预载包含多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 文件上传 {#file-upload}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

文件上传组件为用户提供了选择和上传文件的途径。

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
您可以创建一个自定义上传组件来将文件上传至 Sling Servlet。有关信息，请参阅[将文件上传至 Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/uploading-files-aem1.html)。

### 隐藏字段 {#hidden-field}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单隐藏核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-hidden.html)。

此组件允许您创建隐藏字段。隐藏字段可用于多种目的；例如，当您需要在提交表单后执行操作，或者在帖子处理期间需要使用隐藏数据时。

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
还可以自定义您的表单，以根据表单中其他字段的值显示或隐藏特定表单组件。当仅在特定条件下才需要表单字段时，更改表单字段的可见性很有用。
请参阅[显示和隐藏表单组件](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components)。

### 图像按钮 {#image-button}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单按钮核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-button.html)。

图像按钮允许您使用自己的图像和文本创建按钮：

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### 图像上传 {#image-upload}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

图像上传组件为用户提供了选择和上传图像文件的途径。

![dc_form_imageupload](assets/dc_form_imageupload.png)

### 链接字段 {#link-field}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

链接字段允许用户指定 URL：

![dc_form_link](assets/dc_form_link.png)

最常用于日历事件表单，它在该表单中用于事件的 URL/链接字段。

### 密码字段 {#password-field}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此组件用于允许用户输入密码：

![dc_form_password](assets/dc_form_password.png)

### 密码重置 {#password-reset}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此组件为用户提供了两个字段，分别用于：

* 输入密码
* 重复输入密码以确认输入正确。

使用默认设置时组件将显示为：

![dc_password_reset](assets/dc_password_reset.png)

### 单选按钮组 {#radio-group}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单选项核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-options.html)。

单选按钮组为您提供了一个或多个单选复选框列表，在任何特定时间都只能选择其中一个。

您可以指定元素名称、标题和说明。使用 + 和 - 按钮可以添加或删除项目，然后使用向上和向下箭头定位这些项目，以及根据需要指定默认值：

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
使用&#x200B;**项目加载路径**，您可以预载包含值的单选按钮组。
请参阅[预载包含多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 提交按钮 {#submit-button}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单按钮核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-button.html)。

此组件允许您使用以下默认文本创建提交按钮：

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

或者使用您自己的文本：

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### 标记字段 {#tags-field}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

此字段允许您选择标记：

![dc_form_tags_use](assets/dc_form_tags_use.png)

您可以指定各种参数，包括可通过特殊选项卡使用的命名空间：

* **标记字段**

   * **允许的命名空间**

      * **Geometrixx Outdoors**
      * **工作流**
      * **论坛**
      * **Stock Photography**
      * **Geometrixx Media**
      * **标准标记**
      * **营销**
      * **资产属性**
      * **宽度（以像素为单位）**
      * **弹出窗口大小**

### 文本字段 {#text-field}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单文本核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-text.html)。

可以将标准文本字段配置为您需要的大小且消息中包含您自己的潜在客户：

![dc_form_text](assets/dc_form_text.png)

### Workflow Submit Button(s) {#workflow-submit-button-s}

>[!CAUTION]
此基础组件已被弃用。Adobe 建议改用[表单按钮核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/forms/form-button.html)。

此组件允许您创建可在工作流中使用的提交按钮。

![chlimage_1-101](assets/chlimage_1-101.png)

