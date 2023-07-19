---
title: 使用客户端库
seo-title: Using Client-Side Libraries
description: AEM提供了客户端库文件夹，您可以使用这些文件夹将客户端代码存储在存储库中，将其组织为不同类别，并定义每个类别代码何时以及如何提供给客户端
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 1%

---

# 使用客户端库{#using-client-side-libraries}

现代网站在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为帮助处理此问题，AEM提供了 **客户端库文件夹**，可将客户端代码存储在存储库中，将其组织成不同类别，并定义何时以及如何向客户端提供每种类别的代码。 然后，客户端库系统负责在最终网页中产生正确的链接，以加载正确的代码。

## 客户端库在AEM中的工作原理 {#how-client-side-libraries-work-in-aem}

在页面的HTML中包含客户端库（即JS或CSS文件）的标准方法只是包含 `<script>` 或 `<link>` 标签，其中包含相关文件的路径。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

虽然这种方法在AEM中有效，但当页面及其组成组件变得复杂时，它可能会导致问题。 在这种情况下，最终HTML输出中可能会包含同一JS库的多个副本，这是一种危险。 为了避免这种情况并允许对AEM使用的客户端库进行逻辑组织 **客户端库文件夹**.

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`. 它的定义在 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html) 是

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

默认情况下， `cq:ClientLibraryFolder` 节点可以放置在 `/apps`， `/libs` 和 `/etc` 存储库的子树(这些默认设置和其他设置可通过 **AdobeGraniteHTML库管理器** 面板 [系统控制台](https://localhost:4502/system/console/configMgr))。

每个 `cq:ClientLibraryFolder` 使用一组JS和/或CSS文件以及几个支持文件（见下文）填充。 的属性 `cq:ClientLibraryFolder` 配置如下：

* `categories`：标识此JS和/或CSS文件集所属的类别 `cq:ClientLibraryFolder` 摔倒。 此 `categories` 属性是多值属性，允许库文件夹属于多个类别（请参阅下方了解其用处）。

* `dependencies`：这是此库文件夹所依赖的其他客户端库类别的列表。 例如，给定两个 `cq:ClientLibraryFolder` 节点 `F` 和 `G`，如果文件位于 `F` 需要另一个文件 `G` 为了正常运行，则至少一个 `categories` 之 `G` 应该属于 `dependencies` 之 `F`.

* `embed`：用于嵌入其他库中的代码。 如果节点F嵌入节点G和H，则生成的HTML将是来自节点G和H的内容集。
* `allowProxy`：如果客户端库位于 `/apps`，此属性允许通过代理servlet访问它。 参见 [查找客户端库文件夹并使用代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下面的。

## 引用客户端库 {#referencing-client-side-libraries}

由于HTL是开发AEM站点的首选技术，因此应使用HTL在AEM中包含客户端库。 但是，也可以使用JSP执行此操作。

### 使用HTL {#using-htl}

在HTL中，通过AEM提供的帮助程序模板来加载客户端库，可通过访问模板 [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). 此文件中提供了三个模板，可通过来调用它们 [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)：

* **css**  — 仅加载引用的客户端库的CSS文件。
* **js**  — 仅加载引用的客户端库的JavaScript文件。
* **所有**  — 加载引用的客户端库的所有文件（CSS和JavaScript）。

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

有关详细信息和使用示例，请参阅文档 [HTML模板语言快速入门](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### 使用JSP {#using-jsp}

添加 `ui:includeClientLib` 标记到JSP代码，以便在生成的HTML页面中添加指向客户端库的链接。 要引用库，请使用 `categories` 的属性 `ui:includeClientLib` 节点。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如， `/etc/clientlibs/foundation/jquery` 节点属于类型 `cq:ClientLibraryFolder` 具有categories值属性 `cq.jquery`. JSP文件中的以下代码引用了库：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML页包含以下代码：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有关完整信息，包括用于筛选JS、CSS或主题库的属性，请参阅 [ui：includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`过去通常用于包含客户端库，但自AEM 5.6起已弃用。 [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 应改用，如上所述。

## 创建客户端库文件夹 {#creating-client-library-folders}

创建 `cq:ClientLibraryFolder` 节点，用于定义JavaScript和层叠样式表库并使其可用于HTML页。 使用 `categories` 节点的属性，用于标识其所属的库类别。

该节点包含一个或多个在运行时合并到单个JS和/或CSS文件中的源文件。 生成的文件的名称是节点名称，带有 `.js` 或 `.css` 文件扩展名。 例如，库节点命名为 `cq.jquery` 生成的文件中的结果，名为 `cq.jquery.js` 或 `cq.jquery.css`.

客户端库文件夹包含以下项目：

* 要合并的JS和/或CSS源文件。
* 支持CSS样式的资源，例如图像文件。

  **注意：** 您可以使用子文件夹来组织源文件。
* 一个 `js.txt` 文件和/或一个 `css.txt` 标识要合并到生成的JS和/或CSS文件中的源文件的文件。

![clientlibarch](assets/clientlibarch.png)

有关特定于构件客户端库的要求的信息，请参阅 [使用和扩展小组件](/help/sites-developing/widgets.md).

Web客户端必须具有访问 `cq:ClientLibraryFolder` 节点。 您还可以从存储库的安全区域公开库（请参阅下面的嵌入其他库的代码）。

### 覆盖/lib中的库 {#overriding-libraries-in-lib}

位于下面的客户端库文件夹 `/apps` 优先于位置相似的同名文件夹 `/libs`. 例如， `/apps/cq/ui/widgets` 优先于 `/libs/cq/ui/widgets`. 如果这些库属于同一类别，则使用下面的库 `/apps` 已使用。

### 查找客户端库文件夹并使用代理客户端库Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客户端库文件夹位于下方 `/etc/clientlibs` 在存储库中。 这仍受支持，但建议现在将客户端库位于 `/apps`. 这是为了将客户端库定位到其他脚本附近，这些脚本通常位于下方 `/apps` 和 `/libs`.

>[!NOTE]
>
>客户端库文件夹下的静态资源必须位于名为的文件夹中 *资源*. 如果文件夹下没有静态资源（例如图像） *资源*，无法在发布实例上引用它。 下面是一个示例： https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>为了更好地将代码与内容和配置分离，建议在以下位置找到客户端库： `/apps` 并通过以下方式公开它们 `/etc.clientlibs` 利用 `allowProxy` 属性。

对于下的客户端库 `/apps` 要访问，将使用代理servelt。 仍会在客户端库文件夹上强制执行ACL，但servlet允许通过读取内容 `/etc.clientlibs/` 如果 `allowProxy` 属性设置为 `true`.

如果静态资源位于客户端库文件夹下的资源下，则只能通过代理访问。

例如：

* 您在中有一个clientlib `/apps/myproject/clientlibs/foo`
* 您有一个静态图像 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然后设置 `allowProxy` 属性 `foo` 为真。

* 然后，您可以请求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然后，您可以通过以下方式引用图像 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>在使用代理的客户端库时，AEM Dispatcher配置可能需要更新，以确保允许使用扩展的clientlibs的URI。

>[!CAUTION]
>
>Adobe建议将客户端库定位在 `/apps` 并使用代理servlet使它们可用。 但请记住，最佳做法仍然要求公共站点绝不包含任何直接通过 `/apps` 或 `/libs` 路径。

### 创建客户端库文件夹 {#create-a-client-library-folder}

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 选择要在其中找到客户端库文件夹的文件夹，然后单击 **创建>创建节点**.
1. 输入库文件的名称，然后在“类型”列表中选择 `cq:ClientLibraryFolder`. 单击 **确定** 然后单击 **全部保存**.
1. 要指定库所属的类别，请选择 `cq:ClientLibraryFolder` 节点，添加以下属性，然后单击 **全部保存**：

   * 名称：类别
   * 类型：字符串
   * 值：类别名称
   * 多：选择

1. 通过任何方式将源文件添加到库文件夹中。 例如，使用WebDav客户端复制文件，或创建文件并手动创作内容。

   **注意：** 如果需要，可以在子文件夹中组织源文件。

1. 选择客户端库文件夹并单击 **“创建”>“创建文件”**.
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”：

   * **`js.txt`：** 使用此文件名可生成JavaScript文件。
   * **`css.txt`：** 使用此文件名可生成层叠样式表。

1. 打开文件并键入以下文本以标识源文件路径的根：

   `#base=*[root]*`

   替换* `[root]`*包含源文件的文件夹的路径（相对于TXT文件）。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：

   `#base=.`

   以下代码将根设置为名为mobile的文件夹，该文件夹位于 `cq:ClientLibraryFolder` 节点：

   `#base=mobile`

1. 在以下行上 `#base=[root]`，键入源文件相对于根的路径。 将每个文件名放在单独的一行上。
1. 单击 **全部保存**.

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，请将其他库标识为依赖项。 在JSP中， `ui:includeClientLib` 引用了您的客户端库文件夹的标记会导致HTML代码包含指向生成的库文件以及依赖项的链接。

依赖项必须是另一个 `cq:ClientLibraryFolder`. 要识别依赖关系，请将资产添加到 `cq:ClientLibraryFolder` 节点具有以下属性：

* **名称：** 依赖关系
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq：ClientLibraryFolder节点的categories属性的值。

例如，/ `etc/clientlibs/myclientlibs/publicmain` 依赖于 `cq.jquery` 库。 引用主客户端库的JSP会生成包含以下代码的HTML：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 嵌入其他库中的代码 {#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到另一个客户端库中。 在运行时，嵌入库生成的JS和CSS文件包含嵌入库的代码。

嵌入代码可用于提供对存储在存储库安全区域中的库的访问权限。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最佳实践是将所有与应用程序相关的文件保存在其应用程序文件夹的下方 `/apps`. 拒绝网站访客访问 `/apps` 文件夹。 为满足这两个最佳实践的要求，请在下面创建一个客户端库文件夹 `/apps`，并使其可通过代理servlet访问，如下所述 [查找客户端库文件夹并使用代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

使用categories属性可标识要嵌入的客户端库文件夹。 要嵌入库，请向嵌入中添加属性 `cq:ClientLibraryFolder` 节点，使用以下属性属性：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 的类别属性的值 `cq:ClientLibraryFolder` 要嵌入的节点。

#### 使用嵌入功能将请求数降至最低 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现发布实例为典型页面生成的最终HTML包含相对大量的 `<script>` 元素，尤其是当站点正在使用客户端上下文信息进行分析或定位时。 例如，在非优化项目中，您可能会找到以下系列 `<script>` 页面HTML中的元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在这种情况下，将所有所需的客户端库代码合并到一个文件中会很有用，从而减少页面加载上的来回请求数。 要执行此操作，您可以 `embed` 所需的库将放入特定于应用程序的客户端库中，使用的嵌入属性 `cq:ClientLibraryFolder` 节点。

以下客户端库类别包含在AEM中。 您应仅嵌入特定网站正常工作所需的那些项目。 但是， **您应保留此处列出的顺序**：

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

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源的路径。 例如，可公开访问的库 `/etc/client/libraries/myclientlibs/publicmain` 嵌入 `/apps/myapp/clientlib` 客户端库：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

此 `main.css` 文件包含以下样式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS文件， `publicmain` 节点使用原始图像的URL生成包含以下样式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 将库用于特定移动组 {#using-a-library-for-specific-mobile-groups}

使用 `channels` 客户端库文件夹的属性，用于标识使用该库的移动组。 此 `channels` 当针对不同的设备功能设计同一类别的库时，属性很有用。

要将客户端库文件夹与设备组关联，请将资产添加到 `cq:ClientLibraryFolder` 节点具有以下属性：

* **名称：** 渠道
* **类型：** 字符串[]
* **值：** 移动组的名称。 要从组中排除库文件夹，请在名称前面加一个感叹号(“！”)。

例如，下表列出了 `channels` 属性的每个客户端库文件夹 `cq.widgets` 类别：

| 客户端库文件夹 | 渠道属性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 使用预处理器 {#using-preprocessors}

AEM允许使用可插拔的预处理器，并且附带支持 [YUI压缩程序](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 适用于CSS和JavaScript和 [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) YUI设置为AEM默认预处理器的JavaScript。

可插拔预处理器允许灵活使用，包括：

* 定义可以处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩小，也可用于非缩小情况
* clientlib可以定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 请参阅 [YUI压缩程序GitHub文档](https://github.com/yui/yuicompressor/issues) 以获取已知问题的列表。 为特定clientlibs切换到GCC压缩器可以解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>请勿将缩小的库放置在客户端库中。 而是提供原始库，如果需要缩小，请使用预处理器的选项。

### 用途 {#usage}

您可以选择按clientlibrary或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 和 `jsProcessor` 在客户端库节点上

* 或通过定义系统默认配置 **HTML库管理器** OSGi配置

clientlib节点上的预处理器配置优先于OSGI配置。

### 格式和示例 {#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### 适用于CSS缩小和GCC for JS的YUI压缩程序 {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 用于预处理的Typescript，然后用于缩小和模糊处理的GCC {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC选项 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有关GCC选项的更多详细信息，请参见 [GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels).

### 设置系统默认缩小器 {#set-system-default-minifier}

在AEM中，YUI被设置为默认小型化器。 要将其更改为GCC，请执行以下步骤。

1. 转到Apache Felix配置管理器，网址为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 查找并编辑 **AdobeGraniteHTML库管理器**.
1. 启用 **Minify** 选项（如果尚未启用）。
1. 设置值 **JS处理器默认配置** 到 `min:gcc`.

   如果用分号分隔，则可以传递选项，例如， `min:gcc;obfuscate=true`.

1. 单击 **保存** 以保存更改。

## 调试工具 {#debugging-tools}

AEM提供了多种用于调试和测试客户端库文件夹的工具。

### 请参阅嵌入的文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库产生预期结果，您可以在运行时查看嵌入文件的名称。 要查看文件名，请附加 `debugClientLibs=true` 参数到网页URL。 生成的库包含 `@import` 语句而不是嵌入代码。

在上一个示例中 [嵌入其他库中的代码](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) 部分， `/etc/client/libraries/myclientlibs/publicmain` 客户端库文件夹嵌入了 `/apps/myapp/clientlib` 客户端库文件夹。 将参数附加到网页会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开 `publicmain.css` 文件将显示以下代码：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL：

   `?debugClientLibs=true`
1. 加载页面时，查看页面源。
1. 单击作为链接元素的href提供的链接，以打开文件并查看源代码。

### 发现客户端库 {#discover-client-libraries}

此 `/libs/cq/granite/components/dumplibs/dumplibs` 组件生成一个页面，其中包含有关系统上所有客户端库文件夹的信息。 此 `/libs/granite/ui/content/dumplibs` 节点将组件作为资源类型。 要打开该页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

这些信息包括库路径和类型（CSS或JS）以及库属性的值（如类别和依赖项）。 页面上的后续表将显示每个类别和渠道中的库。

### 查看生成的输出 {#see-generated-output}

此 `dumplibs` 组件包括一个测试选择器，该选择器显示为生成的源代码 `ui:includeClientLib` 标记之间。 该页面包含js、css和主题化属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：

   * 从 `dumplibs.html` 页面上，单击以下位置中的链接： **单击此处进行输出测试** 文本。

   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）：

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   默认页面显示没有categories属性值的标记的输出。

1. 要查看某个类别的输出，请键入客户端库的 `categories` 属性并单击 **提交查询**.

## 配置用于开发和生产的库处理 {#configuring-library-handling-for-development-and-production}

HTML库管理器服务进程 `cq:ClientLibraryFolder` 标记并在运行时生成库。 环境的类型（开发或生产）决定了应如何配置服务：

* 提高安全性：禁用调试
* 提高性能：删除空白并压缩库。
* 提高可读性：包含空格而不压缩。

有关配置服务的信息，请参见 [AEMHTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
