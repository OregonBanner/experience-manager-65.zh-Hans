---
title: 使用客户端库
seo-title: 使用客户端库
description: AEM提供客户端库文件夹，利用该文件夹可将客户端代码存储在存储库中，将其整理为各个类别，并定义何时以及如何将每个类别的代码提供给客户端
seo-description: AEM提供客户端库文件夹，利用该文件夹可将客户端代码存储在存储库中，将其整理为各个类别，并定义何时以及如何将每个类别的代码提供给客户端
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---

# 使用客户端库{#using-client-side-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了&#x200B;**客户端库文件夹**，这允许您将客户端代码存储在存储库中，将其组织成各个类别，并定义何时以及如何将每个类别的代码提供给客户端。 然后，客户端库系统会负责在最终网页中生成正确的链接，以加载正确的代码。

## 客户端库在AEM中的工作原理{#how-client-side-libraries-work-in-aem}

在页面的HTML中包含客户端库（即JS或CSS文件）的标准方法是，在该页面的JSP中包含`<script>`或`<link>`标记，其中包含相关文件的路径。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

虽然此方法在AEM中有效，但在页面及其组成组件变得复杂时，可能会导致问题。 在这种情况下，最终HTML输出中可能会包含同一JS库的多个副本。 要避免这种情况并允许对客户端库进行逻辑组织，AEM会使用&#x200B;**客户端库文件夹**。

客户端库文件夹是`cq:ClientLibraryFolder`类型的存储库节点。 [CND符号](https://jackrabbit.apache.org/node-type-notation.html)中的定义是

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

默认情况下，`cq:ClientLibraryFolder`节点可以置于存储库的`/apps`、`/libs`和`/etc`子树中的任意位置(这些默认值和其他设置可通过[系统控制台](https://localhost:4502/system/console/configMgr)的&#x200B;**AdobeGranite HTML库管理器**&#x200B;面板进行控制)。

每个`cq:ClientLibraryFolder`都会填充一组JS和/或CSS文件，以及一些支持文件（请参阅下文）。 `cq:ClientLibraryFolder`的属性配置如下：

* `categories`:标识今秋JS和/或CSS文件集所属的类 `cq:ClientLibraryFolder` 别。`categories`属性具有多值，允许库文件夹属于多个类别的一部分（请参阅下文，了解这种属性的用途）。

* `dependencies`:这是此库文件夹所依赖的其他客户端库类别的列表。例如，给定两个`cq:ClientLibraryFolder`节点`F`和`G`时，如果`F`中的文件需要`G`中的另一个文件才能正常运行，则`G`的`categories`中至少有一个应位于`F`的`dependencies`中。

* `embed`:用于嵌入来自其他库的代码。如果节点F嵌入节点G和H，则生成的HTML将包含来自节点G和H的内容。
* `allowProxy`:如果客户端库位于下 `/apps`，则此属性允许通过代理Servlet访问它。请参阅下面的[查找客户端库文件夹和使用代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 。

## 引用客户端库{#referencing-client-side-libraries}

由于HTL是开发AEM站点的首选技术，因此应使用HTL在AEM中包含客户端库。 但是，也可以使用JSP来执行此操作。

### 使用HTL {#using-htl}

在HTL中，客户端库通过AEM提供的帮助程序模板加载，该模板可通过[ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)访问。 此文件中提供了三个模板，可通过[ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)调用：

* **css**  — 仅加载引用的客户端库的CSS文件。
* **js**  — 仅加载引用客户端库的JavaScript文件。
* **all**  — 加载引用的客户端库的所有文件（CSS和JavaScript）。

每个帮助程序模板都需要一个`categories`选项来引用所需的客户端库。 该选项可以是字符串值数组，也可以是包含逗号分隔值列表的字符串。

有关更多详细信息和使用示例，请参阅文档[HTML模板语言快速入门](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

向JSP代码中添加`ui:includeClientLib`标记，以在生成的HTML页面中添加指向客户端库的链接。 要引用库，请使用`ui:includeClientLib`节点的`categories`属性的值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，`/etc/clientlibs/foundation/jquery`节点为`cq:ClientLibraryFolder`类型，其类别属性为值`cq.jquery`。 JSP文件中的以下代码引用了库：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML页面包含以下代码：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有关完整信息（包括用于筛选JS、CSS或主题库的属性），请参阅[ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`，过去常用于包含客户端库，但自AEM 5.6起已弃用它。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 应改用，如上所述。

## 创建客户端库文件夹{#creating-client-library-folders}

创建`cq:ClientLibraryFolder`节点以定义JavaScript和层叠样式表库，并使它们可用于HTML页面。 使用节点的`categories`属性标识它所属的库类别。

节点包含一个或多个在运行时合并到单个JS和/或CSS文件中的源文件。 生成的文件的名称是扩展名为`.js`或`.css`的节点名称。 例如，名为`cq.jquery`的库节点会生成名为`cq.jquery.js`或`cq.jquery.css`的生成文件。

客户端库文件夹包含以下项目：

* 要合并的JS和/或CSS源文件。
* 支持CSS样式的资源，如图像文件。

   **注意：** 您可以使用子文件夹来组织源文件。
* 一个`js.txt`文件和/或一个`css.txt`文件，用于标识要合并到生成的JS和/或CSS文件中的源文件。

![clientlibarch](assets/clientlibarch.png)

有关特定于客户端库的小组件的要求的信息，请参阅[使用和扩展小组件](/help/sites-developing/widgets.md)。

Web客户端必须具有访问`cq:ClientLibraryFolder`节点的权限。 您还可以从存储库的安全区域中显示库（请参阅下面的“从其他库嵌入代码”）。

### 在/lib {#overriding-libraries-in-lib}中覆盖库

位于`/apps`下的客户端库文件夹优先于位于`/libs`中的相似名称文件夹。 例如，`/apps/cq/ui/widgets`优先于`/libs/cq/ui/widgets`。 当这些库属于同一类别时，将使用`/apps`下的库。

### 查找客户端库文件夹并使用代理客户端库Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客户端库文件夹位于存储库的`/etc/clientlibs`下方。 此功能仍受支持，但建议客户端库现在位于`/apps`下。 这是为了在其他脚本附近找到客户端库，这些脚本通常位于`/apps`和`/libs`下。

>[!NOTE]
>
>客户端库文件夹下的静态资源必须位于名为&#x200B;*resources*&#x200B;的文件夹中。 如果文件夹&#x200B;*resources*&#x200B;下没有静态资源（如图像），则无法在发布实例上引用该资源。 示例如下：https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>为了更好地将代码与内容和配置隔离，建议在`/apps`下找到客户端库，并利用`allowProxy`属性通过`/etc.clientlibs`公开它们。

为了访问`/apps`下的客户端库，请使用代理服务器。 ACL仍对客户端库文件夹强制执行，但如果将`allowProxy`属性设置为`true`，则Servlet允许通过`/etc.clientlibs/`读取内容。

如果静态资源位于客户端库文件夹下的资源下，则只能通过代理访问该静态资源。

例如：

* `/apps/myproject/clientlibs/foo`中有clientlib
* `/apps/myprojects/clientlibs/foo/resources/icon.png`中有一个静态图像

然后，将`foo`上的`allowProxy`属性设置为true。

* 然后，您可以请求`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然后，可以通过`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`引用该图像

>[!CAUTION]
>
>使用代理客户端库时，AEM Dispatcher配置可能需要更新，以确保允许具有扩展clientlibs的URI。

>[!CAUTION]
>
>Adobe建议在`/apps`下查找客户端库，并使用代理Servlet使其可用。 但请记住，最佳做法仍要求公共站点不得包含任何直接通过`/apps`或`/libs`路径提供的内容。

### 创建客户端库文件夹{#create-a-client-library-folder}

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 选择要在其中找到客户端库文件夹的文件夹，然后单击&#x200B;**创建>创建节点**。
1. 输入库文件的名称，然后在类型列表中选择`cq:ClientLibraryFolder`。 单击&#x200B;**确定**，然后单击&#x200B;**保存全部**。
1. 要指定库所属的类别或类别，请选择`cq:ClientLibraryFolder`节点，添加以下属性，然后单击&#x200B;**Save All**:

   * 名称：类别
   * 类型：字符串
   * 值：类别名称
   * 多：选择

1. 通过任何方式将源文件添加到库文件夹。 例如，使用WebDav客户端复制文件，或创建文件并手动创作内容。

   **注意：** 您可以根据需要将源文件组织在子文件夹中。

1. 选择客户端库文件夹，然后单击&#x200B;**创建>创建文件**。
1. 在文件名框中，键入以下文件名之一，然后单击“确定”：

   * **`js.txt`:** 使用此文件名生成JavaScript文件。
   * **`css.txt`:** 使用此文件名生成层叠样式表。

1. 打开文件并键入以下文本以标识源文件路径的根：

   `#base=*[root]*`

   将* `[root]`*替换为包含源文件的文件夹路径（相对于TXT文件）。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：

   `#base=.`

   以下代码会将根目录设置为`cq:ClientLibraryFolder`节点下名为mobile的文件夹：

   `#base=mobile`

1. 在`#base=[root]`下面的行中，键入源文件相对于根的路径。 将每个文件名放在单独的行上。
1. 单击&#x200B;**Save All**。

### 链接到依赖项{#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，请将其他库标识为依赖项。 在JSP中，引用客户端库文件夹的`ui:includeClientLib`标记导致HTML代码包含到生成的库文件的链接以及依赖关系。

依赖项必须是另一个`cq:ClientLibraryFolder`。 要识别依赖关系，请使用以下属性将属性添加到`cq:ClientLibraryFolder`节点：

* **名称：** 依赖项
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq:ClientLibraryFolder节点的类别属性的值。

例如， / `etc/clientlibs/myclientlibs/publicmain`对`cq.jquery`库具有依赖关系。 引用主客户端库的JSP会生成包含以下代码的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 嵌入来自其他库的代码{#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到其他客户端库中。 在运行时，嵌入库生成的JS和CSS文件包含嵌入库的代码。

嵌入代码对于提供对存储在存储库安全区域中的库的访问权限非常有用。

#### 特定于应用程序的客户端库文件夹{#app-specific-client-library-folders}

最佳做法是将所有与应用程序相关的文件保留在其`/app`下的应用程序文件夹中。 拒绝网站访客访问`/app`文件夹也是最佳做法。 要满足这两个最佳实践，请在`/etc`文件夹下创建一个客户端库文件夹，该文件夹嵌入位于`/app`以下的客户端库。

使用类别属性标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性属性将属性添加到嵌入`cq:ClientLibraryFolder`节点：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 要嵌入的节点的类别属 `cq:ClientLibraryFolder` 性的值。

#### 使用嵌入最小化请求{#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现，发布实例为典型页面生成的最终HTML包含相对大量的`<script>`元素，特别是当您的网站正在使用客户端上下文信息进行分析或定位时。 例如，在非优化项目中，您可能会在页面的HTML中找到以下系列的`<script>`元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在这种情况下，将所有必需的客户端库代码合并到单个文件中，以减少页面加载时来回请求的数量，这非常有用。 要实现此目的，您可以使用`cq:ClientLibraryFolder`节点的embed属性，将所需的库`embed`放入特定于应用程序的客户端库中。

AEM中包含以下客户端库类别。 您应仅嵌入特定网站运行所需的内容。 但是，**您应维护此处列出的顺序**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS文件{#paths-in-css-files}中的路径

嵌入CSS文件时，生成的CSS代码会使用相对于嵌入库的资源的路径。 例如，可公开访问的库`/etc/client/libraries/myclientlibs/publicmain`嵌入了`/apps/myapp/clientlib`客户端库：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

`main.css`文件包含以下样式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain`节点生成的CSS文件包含以下样式（使用原始图像的URL）：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 为特定移动组使用库{#using-a-library-for-specific-mobile-groups}

使用客户端库文件夹的`channels`属性来标识使用该库的移动组。 当针对不同设备功能设计了同一类别的库时， `channels`属性非常有用。

要将客户端库文件夹与设备组关联，请使用以下属性将属性添加到`cq:ClientLibraryFolder`节点：

* **名称：** 渠道
* **类型：** 字符串[]
* **值：** 移动设备组的名称。要从组中排除库文件夹，请在名称前添加感叹号(“！”)。

例如，下表列出了`cq.widgets`类别中每个客户端库文件夹的`channels`属性值：

| 客户端库文件夹 | 渠道属性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[无值]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## 使用预处理器{#using-preprocessors}

AEM支持可插拔的预处理器，并支持[YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) for CSS和JavaScript和[Google Closure Compiler(GCC)](https://developers.google.com/closure/compiler/) for JavaScript，将YUI设置为AEM默认预处理器。

可插拔预处理器允许灵活使用，包括：

* 定义可处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩小，但也可用于未缩小的情况
* clientlib可定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 有关已知问题的列表，请参阅[YUI Compressor GitHub文档](https://github.com/yui/yuicompressor/issues)。 在使用YUI时，切换到特定客户端的GCC压缩程序可能会解决一些观察到的问题。

>[!CAUTION]
>
>请勿在客户端库中放置缩小的库。 请改为提供原始库，如果需要缩小，请使用预处理器的选项。

### 使用 {#usage}

您可以选择为每个客户端库或系统范围配置预处理器配置。

* 在clientlibrary节点上添加多值属性`cssProcessor`和`jsProcessor`

* 或通过&#x200B;**HTML库管理器** OSGi配置定义系统默认配置

clientlib节点上的预处理器配置优先于OSGI配置。

### 格式和示例{#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### 用于CSS缩小的YUI压缩程序和用于JS的GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 键入前处理，然后GCC缩小和模糊处理{#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC选项{#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有关GCC选项的更多详细信息，请参阅[GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 设置系统默认缩小器{#set-system-default-minifier}

在AEM中，YUI设置为默认的缩小符。 要将此代码更改为GCC，请执行以下步骤。

1. 转到位于[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的Apache Felix配置管理器
1. 查找并编辑&#x200B;**AdobeGranite HTML库管理器**。
1. 启用&#x200B;**Minify**&#x200B;选项（如果尚未启用）。
1. 将值&#x200B;**JS处理器默认配置**&#x200B;设置为`min:gcc`。

   如果使用分号(例如，`min:gcc;obfuscate=true`。

1. 单击&#x200B;**Save**&#x200B;以保存更改。

## 调试工具{#debugging-tools}

AEM提供了多种工具来调试和测试客户端库文件夹。

### 请参阅嵌入的文件{#see-embedded-files}

要跟踪嵌入代码的源，或确保嵌入的客户端库生成预期结果，您可以在运行时查看正在嵌入的文件的名称。 要查看文件名，请将`debugClientLibs=true`参数附加到网页的URL后面。 生成的库包含`@import`语句，而不是嵌入的代码。

在上一个[从其他库嵌入代码](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)部分的示例中， `/etc/client/libraries/myclientlibs/publicmain`客户端库文件夹嵌入了`/apps/myapp/clientlib`客户端库文件夹。 将参数附加到网页后，会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开`publicmain.css`文件会显示以下代码：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL:

   `?debugClientLibs=true`
1. 页面加载时，查看页面源。
1. 单击作为链接元素的href提供的链接以打开文件并查看源代码。

### 发现客户端库{#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`组件会生成有关系统上所有客户端库文件夹的信息页面。 `/libs/granite/ui/content/dumplibs`节点将组件作为资源类型。 要打开页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

该信息包括库路径和类型（CSS或JS），以及库属性的值，如类别和依赖关系。 页面上的后续表显示了每个类别和渠道中的库。

### 请参阅生成的输出{#see-generated-output}

`dumplibs`组件包含测试选择器，该测试选择器显示为`ui:includeClientLib`标记生成的源代码。 页面包含js、css和主题属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：

   * 在`dumplibs.html`页面中，单击&#x200B;**单击此处以进行输出测试**&#x200B;文本中的链接。

   * 在Web浏览器中打开以下URL（根据需要使用其他主机和端口）：

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   默认页面显示类别属性没有值的标记的输出。

1. 要查看类别的输出，请键入客户端库`categories`属性的值，然后单击&#x200B;**Submit Query**。

## 为开发和生产配置库处理{#configuring-library-handling-for-development-and-production}

HTML库管理器服务会处理`cq:ClientLibraryFolder`标记，并在运行时生成库。 环境类型、开发或生产类型决定了应如何配置服务：

* 提高安全性：禁用调试
* 提高性能：删除空格并压缩库。
* 提高可读性：包括空格和不压缩。

有关配置服务的信息，请参阅[AEM HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
