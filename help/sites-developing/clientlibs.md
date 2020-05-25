---
title: 使用客户端库
seo-title: 使用客户端库
description: AEM提供客户端库文件夹，通过这些文件夹，您可以在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何将每个类别的代码提供给客户端
seo-description: AEM提供客户端库文件夹，通过这些文件夹，您可以在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何将每个类别的代码提供给客户端
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: da233b2d58e13bf86c88115a78f2fecf1be12ba9
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---


# 使用客户端库{#using-client-side-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提 **供了客户端库文件夹**，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每个类别的代码。 然后，客户端库系统负责在最终网页中生成正确的链接以加载正确的代码。

## 客户端库在AEM中的工作方式 {#how-client-side-libraries-work-in-aem}

在页面的HTML中包含客户端库（即JS或CSS文件）的标准方式是，在该页面的JSP中包含一个或 `<script>` 标 `<link>` 签，其中包含该文件的路径。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

虽然此方法在AEM中有效，但在页面及其组成组件变得复杂时，可能会导致问题。 在这种情况下，同一JS库的多个副本可能会包含在最终HTML输出中。 要避免这种情况，并允许对客户端库进行逻辑组织，AEM将使 **用客户端库文件夹**。

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`。 CND表示法的定 [义是](https://jackrabbit.apache.org/node-type-notation.html)

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

默认情 `cq:ClientLibraryFolder` 况下，节点可以放置在存储库的任 `/apps`何位置 `/libs` ，并且可以通过System Console的Adobe `/etc` Granite HTML Library Manager面板控 ****[](https://localhost:4502/system/console/configMgr)制其他设置。

每个 `cq:ClientLibraryFolder` 文件都会填入一组JS和／或CSS文件，以及一些支持文件（请参阅下文）。 属性配置 `cq:ClientLibraryFolder` 如下：

* `categories`: 标识今秋内JS和／或CSS文件集所属的类别 `cq:ClientLibraryFolder` 符。 该 `categories` 属性具有多值，允许库文件夹成为多个类别的一部分（请参见下面，了解这可能有何用）。

* `dependencies`: 这是此库文件夹所依赖的其他客户端库类别的列表。 例如，给定两个 `cq:ClientLibraryFolder` 节点 `F` ，如果某个文件需要另一个文件才能正常工作，则至少其中一个节点 `G`应该 `F``G``categories``G``dependencies``F`位于中。

* `embed`: 用于嵌入来自其他库的代码。 如果节点F嵌入节点G和H，则生成的HTML将是节点G和H中的内容集中。
* `allowProxy`: 如果客户端库位于下 `/apps`方，则此属性允许通过代理servlet访问它。 请参 [阅查找客户端库文件夹和使用下面的代理客户端库](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) Servlet。

## 引用客户端库 {#referencing-client-side-libraries}

由于HTL是开发AEM站点的首选技术，因此应使用HTL在AEM中包含客户端库。 但是，也可以使用JSP进行此操作。

### 使用HTL {#using-htl}

在HTL中，客户端库通过AEM提供的帮助程序模板加载，该模板可通过以下方式进行访问 [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)。 此文件中提供了三个模板，可通过以下方式调用 [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** —— 仅加载引用的客户端库的CSS文件。
* **js** —— 仅加载引用的客户端库的JavaScript文件。
* **all** —— 加载引用的客户端库的所有文件（CSS和JavaScript）。

每个帮助程序模板都 `categories` 需要一个用于引用所需客户端库的选项。 该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

有关更多详细信息和用法示例，请参 [阅文档HTML模板语言入门](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

向JSP `ui:includeClientLib` 代码中添加标签，以在生成的HTML页面中添加指向客户端库的链接。 要引用库，请使用节点 `categories` 属性的 `ui:includeClientLib` 值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，该节 `/etc/clientlibs/foundation/jquery` 点的类型 `cq:ClientLibraryFolder` 为类别属性值 `cq.jquery`。 JSP文件中的以下代码引用库：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML页包含以下代码：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有关包括筛选JS、CSS或主题库的属性在内的完整信息，请参 [阅ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`（过去常用于包含客户端库）自AEM 5.6起已弃用 [ 。 `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 应改用如上所述。

## 创建客户端库文件夹 {#creating-client-library-folders}

创建一个 `cq:ClientLibraryFolder` 节点以定义JavaScript和层叠样式表库，并使它们可用于HTML页面。 使用节 `categories` 点的属性来标识它所属的库类别。

该节点包含一个或多个在运行时合并为单个JS和／或CSS文件的源文件。 生成的文件的名称是扩展名为或文件 `.js` 名的 `.css` 节点名称。 例如，名为的库节点 `cq.jquery` 将生成名为或的 `cq.jquery.js` 文件 `cq.jquery.css`。

客户端库文件夹包含以下项目：

* 要合并的JS和／或CSS源文件。
* 支持CSS样式的资源，如图像文件。

   **注意：** 您可以使用子文件夹来组织源文件。
* 一个 `js.txt` 文件和／或一 `css.txt` 个文件，用于标识要合并到生成的JS和／或CSS文件中的源文件。

![clientlibarch](assets/clientlibarch.png)

有关构件的客户端库特定要求的信息，请参 [阅使用和扩展构件](/help/sites-developing/widgets.md)。

Web客户端必须具有访问节点的 `cq:ClientLibraryFolder` 权限。 您还可以从存储库的安全区域中显示库（请参阅下面的“从其他库嵌入代码”）。

### 覆盖/lib中的库 {#overriding-libraries-in-lib}

位于以下的客户端库文 `/apps` 件夹优先于位于中的同名文件夹 `/libs`。 例如，优先 `/apps/cq/ui/widgets` 于以下项 `/libs/cq/ui/widgets`目。 当这些库属于同一类别时，将使用下 `/apps` 面的库。

### 查找客户端库文件夹并使用代理客户端库Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客户端库文件夹位 `/etc/clientlibs` 于存储库的下方。 这仍受支持，但建议现在在下方放置客户端库 `/apps`。 这是在其他脚本附近找到客户端库，这些脚本通常位于 `/apps` 和下 `/libs`。

>[!NOTE]
>
>客户端库文件夹下的静态资源必须位于名为resources的文 *件夹中*。 如果文件夹资源下没有静态资源（如图像），则 *不能*&#x200B;在发布实例上引用它。 以下是一个示例： https://localhost:4503/etc.clientlibs/geometrixx/components/clinetlibs/resources/example.gif

>[!NOTE]
>
>为了更好地将代码与内容和配置隔离，建议在下面找到客户端库，并 `/apps` 通过利用属 `/etc.clientlibs` 性来公开 `allowProxy` 它们。

为了能够访问下的客 `/apps` 户端库，使用代理服务器。 ACL仍然强制在客户端库文件夹上，但如果属性设置为，则Servlet允许 `/etc.clientlibs/` 通过 `allowProxy` 读取内容 `true`。

静态资源只能通过代理访问，如果它位于客户端库文件夹下的资源下。

例如：

* 您有一个clientlib `/apps/myproject/clientlibs/foo`
* 您的静态图像 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然后将属 `allowProxy` 性设置为 `foo` true。

* 然后，您可以请求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然后，您可以通过 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>使用代理客户端库时，AEM Dispatcher配置可能需要更新，以确保允许具有扩展客户端库的URI。

>[!CAUTION]
>
>Adobe建议在下面查找客 `/apps` 户端库，并使用代理servlet提供它们。 但是，请记住，最佳做法仍然要求公共站点不要包含任何直接在某个或路径上提供服务 `/apps` 的内 `/libs` 容。

### 创建客户端库文件夹 {#create-a-client-library-folder}

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 选择要在其中找到客户端库文件夹的文件夹，然后单击“ **创建”>“创建节点**”。
1. 输入库文件的名称，并在“类型”列表中选择 `cq:ClientLibraryFolder`。 单击 **确定** ，然后单击 **全部保存**。
1. 要指定库所属的类别或类别，请选 `cq:ClientLibraryFolder` 择节点，添加以下属性，然后单击“全 **部保存**:

   * 名称： 类别
   * 类型： 字符串
   * 值： 类别名称
   * 多： 选择

1. 通过任何方式将源文件添加到库文件夹。 例如，使用WebDav客户端复制文件，或创建文件并手动创作内容。

   **注意：** 如果需要，可以在子文件夹中组织源文件。

1. 选择客户端库文件夹，然后单击“ **创建”>“创建文件**”。
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”:

   * **`js.txt`:**使用此文件名生成JavaScript文件。
   * **`css.txt`:**使用此文件名生成层叠样式表。

1. 打开文件并键入以下文本以标识源文件路径的根：

   `#base=*[root]*`

   将* `[root]`*替换为包含源文件的文件夹（相对于TXT文件）的路径。 例如，当源文件与TXT文件位于同一文件夹中时，请使用以下文本：

   `#base=.`

   下面的代码将根设置为节点下名为mobile的文 `cq:ClientLibraryFolder` 件夹：

   `#base=mobile`

1. 在下面的行 `#base=[root]`中，键入源文件相对于根的路径。 将每个文件名放在单独的行上。
1. 单击“ **全部保存**”。

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，将其他库标识为依赖关系。 在JSP中，引 `ui:includeClientLib` 用客户端库文件夹的标记会导致HTML代码包含指向生成的库文件的链接以及依赖关系。

依赖关系必须是另一个 `cq:ClientLibraryFolder`。 要标识依赖关系，请向节点添 `cq:ClientLibraryFolder` 加具有以下属性的属性：

* **名称：** 依赖
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq:ClientLibraryFolder节点的类别属性值。

例如，/ `etc/clientlibs/myclientlibs/publicmain` 对库具有依 `cq.jquery` 赖性。 引用主客户端库的JSP生成包含以下代码的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 从其他库嵌入代码 {#embedding-code-from-other-libraries}

可以将客户端库中的代码嵌入到另一个客户端库中。 在运行时，嵌入库生成的JS和CSS文件包括嵌入库的代码。

嵌入代码对于提供对存储在存储库的安全区域中的库的访问非常有用。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最好将所有与应用程序相关的文件保留在下面的应用程序文件夹中 `/app`。 拒绝网站访客访问该文件夹也是最佳做 `/app` 法。 为了同时满足这两种最佳实践，请在嵌入以下客户端库 `/etc` 的文件夹下创建一个客户端库文件夹 `/app`。

使用类别属性标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性属 `cq:ClientLibraryFolder` 性向嵌入节点添加属性：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 要嵌入的节点的类别 `cq:ClientLibraryFolder` 属性值。

#### 使用嵌入最小化请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现，发布实例为典型页面生成的最终HTML包含相对大量的元素 `<script>` ，尤其是当您的站点使用Client Context信息进行分析或定位时。 例如，在未优化的项目中，您可能会在页面的HTML `<script>` 中找到以下一系列元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/underscore.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在这种情况下，将所有所需的客户端库代码合并到单个文件中，以减少页面加载时来回请求的数量，这是非常有用的。 为此，您可以使用 `embed` 节点的embed属性将所需的库添加到特定于应用程序的客户端 `cq:ClientLibraryFolder` 库中。

AEM包含以下客户端库类别。 您应仅嵌入特定站点运行所需的内容。 但是， **您应维护此处列出的订单**:

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

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源的路径。 例如，可公开访问的库嵌 `/etc/client/libraries/myclientlibs/publicmain` 入客户端 `/apps/myapp/clientlib` 库：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

文 `main.css` 件包含以下样式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

节点生成的CSS `publicmain` 文件包含以下样式（使用原始图像的URL）:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 将库用于特定移动组 {#using-a-library-for-specific-mobile-groups}

使用客 `channels` 户端库文件夹的属性来标识使用库的移动组。 当为 `channels` 不同的设备功能设计相同类别的库时，该属性很有用。

要将客户端库文件夹与设备组关联，请向节点添加具有以 `cq:ClientLibraryFolder` 下属性的属性：

* **名称：** 渠道
* **类型：** 字符串[]
* **值：** 移动组的名称。 要将库文件夹从组中排除，请在名称前加感叹号(“!”)。

例如，下表列表了该类别的每 `channels` 个客户端库文件夹的属性 `cq.widgets` 值：

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

## 使用预处理器 {#using-preprocessors}

AEM支持可插拔的预处理器，附带 [对UYI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) Compressor for CSS和JavaScript以及Google Closure Compiler(GCC) [](https://developers.google.com/closure/compiler/) for JavaScript的支持，并将YU设置为AEM的默认预处理器。

可插拔预处理器允许灵活使用，包括：

* 定义可处理脚本源的脚本处理器
* 处理器可配置选项
* 处理器可用于微型化，但也可用于非微型化情况
* clientlib可以定义要使用哪个处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 有关一 [列表已知问题](https://github.com/yui/yuicompressor/issues) ，请参阅YUI Compressor GitHub文档。 对于特定客户端，切换到GCC压缩程序可解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>不要将精简库放在客户端库中。 而是提供原始库，如果需要进行微型化，请使用预处理器的选项。

### 使用 {#usage}

您可以选择根据客户端库或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 并 `jsProcessor` 在clientlibrary节点上添加

* 或通过HTML库管理器OSGi配置 **定义系统默认** 配置。

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

#### YUI压缩程序，用于CSS微型化和GCC，用于JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript to Preprocess, and GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有关GCC选项的更多详细信息，请参 [阅GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 设置系统默认迷你符 {#set-system-default-minifier}

在AEM中，YUI设置为默认的迷你符。 要将此更改为GCC，请执行以下步骤。

1. 转到Apache Felix Config Manager，网址为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 查找并编 **辑Adobe Granite HTML库管理器**。
1. 启用 **Minify** 选项（如果尚未启用）。
1. 将“JS处理 **器默认配置”值设** 置 `min:gcc`为。

   如果以分号分隔，则可以传递选项，例如 `min:gcc;obfuscate=true`.

1. Click **Save** to save the changes.

## 调试工具 {#debugging-tools}

AEM提供多种工具，用于调试和测试客户端库文件夹。

### 请参阅嵌入的文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库生成预期结果，您可以在运行时查看嵌入的文件名称。 要查看文件名，请将参 `debugClientLibs=true` 数追加到网页的URL。 生成的库包含语 `@import` 句而不是嵌入代码。

在上一个“从其他库 [嵌入代码”部分的示例中](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) ，客户端库 `/etc/client/libraries/myclientlibs/publicmain` 文件夹会嵌入客户端 `/apps/myapp/clientlib` 库文件夹。 将参数追加到网页后，将在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开文 `publicmain.css` 件会显示以下代码：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本追加到HTML的URL:

   `?debugClientLibs=true`
1. 载入页面时，视图页面源。
1. 单击作为链接元素的href提供的链接以打开文件并视图源代码。

### 发现客户端库 {#discover-client-libraries}

组 `/libs/cq/granite/components/dumplibs/dumplibs` 件会生成有关系统上所有客户端库文件夹的信息页面。 节 `/libs/granite/ui/content/dumplibs` 点将组件作为资源类型。 要打开页面，请使用以下URL（根据需要更改主机和端口）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

信息包括库路径和类型（CSS或JS）以及库属性的值，如类别和依赖关系。 页面上的后续表显示了每个类别和渠道中的库。

### 请参阅生成的输出 {#see-generated-output}

该 `dumplibs` 组件包含一个测试选择器，它显示为标记生成的源 `ui:includeClientLib` 代码。 该页面包含js、css和主题属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：

   * 在该页 `dumplibs.html` 面中，单击“单击此处 **以输出测试”文本中的链接** 。

   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）:

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   默认页显示没有类别属性值的标记的输出。

1. 要查看类别的输出，请键入客户端库属性的值，然 `categories` 后单击“提 **交查询”**。

## 为开发和生产配置库处理 {#configuring-library-handling-for-development-and-production}

HTML库管理器服务在运 `cq:ClientLibraryFolder` 行时处理标记并生成库。 环境、开发或生产类型决定了您应如何配置服务：

* 提高安全性： 禁用调试
* 提高性能： 删除空白并压缩库。
* 提高可读性： 包括空格，不压缩。

有关配置服务的信息，请参 [阅AEM HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
