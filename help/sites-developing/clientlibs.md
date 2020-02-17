---
title: 使用客户端库
seo-title: 使用客户端库
description: AEM提供客户端库文件夹，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每类代码
seo-description: AEM提供客户端库文件夹，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每类代码
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 使用客户端库{#using-client-side-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了客户端库文件夹 ****，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每类代码。 然后，客户端库系统负责在最终网页中生成正确的链接以加载正确的代码。

## 客户端库在AEM中的工作方式 {#how-client-side-libraries-work-in-aem}

在页面的HTML中包含客户端库（即JS或CSS文件）的标准方法是在该页面的JSP中包含一个 `<script>``<link>` 或标签，其中包含该文件的路径。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

虽然此方法在AEM中有效，但在页面及其组成组件变得复杂时，它可能会导致问题。 在这种情况下，同一JS库的多个副本可能会包含在最终HTML输出中。 要避免这种情况并允许对客户端库进行逻辑组织，AEM将使用客 **户端库文件夹**。

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`。 CND表示法的定 [义是](https://jackrabbit.apache.org/node-type-notation.html)

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

默认情况下， `cq:ClientLibraryFolder` 节点可以放置在存储库的 `/apps`、 `/libs` 、子树中(这些默认值和其他设置可以通过 `/etc` System Console的 ****[](https://localhost:4502/system/console/configMgr)Adobe Granite HTML Library Manager面板控制)。

每个 `cq:ClientLibraryFolder` 文件都会填入一组JS和／或CSS文件，以及一些支持文件（请参阅下文）。 属性配置 `cq:ClientLibraryFolder` 如下：

* `categories`:标识今秋JS和／或CSS文件集所属的类 `cq:ClientLibraryFolder` 别。 该属 `categories` 性具有多值，允许库文件夹属于多个类别的一部分（请参阅下面，了解这可能有何用）。

* `dependencies`:这是此库文件夹所依赖的其他客户端库类别的列表。 例如，如果给定的 `cq:ClientLibraryFolder` 两个节点 `F` 和文件中的一个文件需要另一个文件才能正常工作，那么，在给定的节点和文件中，至少 `G`一个应 `F``G``categories``G``dependencies``F`该位于Adobe的Adobe中。

* `embed`:用于嵌入来自其他库的代码。 如果节点F嵌入节点G和H，则生成的HTML将是节点G和H中的内容的集中。
* `allowProxy`:如果客户端库位于下 `/apps`方，则此属性允许通过代理servlet访问它。 请参 [阅查找客户端库文件夹和使用下面的代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 。

## 引用客户端库 {#referencing-client-side-libraries}

由于HTL是开发AEM站点的首选技术，因此应使用HTL在AEM中包含客户端库。 但是，也可以使用JSP执行此操作。

### 使用HTL {#using-htl}

在HTL中，客户端库通过AEM提供的帮助模板加载，可通过访问该模板 [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)。 此文件中提供了三个模板，可通过以下方式调用这些模板 [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** —— 仅加载引用的客户端库的CSS文件。
* **js** —— 仅加载引用的客户端库的JavaScript文件。
* **all** —— 加载引用的客户端库的所有文件（CSS和JavaScript）。

每个帮助程序模板都需要 `categories` 一个用于引用所需客户端库的选项。 该选项可以是字符串值的数组，也可以是包含以逗号分隔的值列表的字符串。

有关更多详细信息和用法示例，请参阅 [HTML模板语言入门文档](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

向JSP代 `ui:includeClientLib` 码中添加标签，以在生成的HTML页面中添加指向客户端库的链接。 要引用库，请使用节点属 `categories` 性的值 `ui:includeClientLib` 。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，该节 `/etc/clientlibs/foundation/jquery` 点的类型为类 `cq:ClientLibraryFolder` 别，其类别属性为value `cq.jquery`。 JSP文件中的以下代码引用这些库：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML页包含以下代码：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有关完整信息（包括用于筛选JS、CSS或主题库的属性），请参 [阅ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`（过去，它通常用于包括客户端库）自AEM 5.6起已弃用。应 [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 按上述详细说明使用。

## 创建客户端库文件夹 {#creating-client-library-folders}

创建一 `cq:ClientLibraryFolder` 个节点以定义JavaScript和层叠样式表库，并使其可用于HTML页。 使用节 `categories` 点的属性可标识它所属的库类别。

该节点包含一个或多个在运行时合并为单个JS和／或CSS文件的源文件。 生成的文件的名称是扩展名为或的节 `.js` 点名 `.css` 称。 例如，名为的库节点会生 `cq.jquery` 成名为或的生成 `cq.jquery.js` 文件 `cq.jquery.css`。

客户端库文件夹包含以下项目：

* 要合并的JS和／或CSS源文件。
* 支持CSS样式的资源，如图像文件。

   **** 注意：您可以使用子文件夹来组织源文件。
* 一个 `js.txt` 文件和／或一个 `css.txt` 文件，用于标识要合并到生成的JS和／或CSS文件中的源文件。

![clientlibarch](assets/clientlibarch.png)

有关构件的客户端库特有的要求的信息，请参阅使用和 [扩展构件](/help/sites-developing/widgets.md)。

Web客户端必须具有访问该节点的权 `cq:ClientLibraryFolder` 限。 您还可以从存储库的安全区域中显示库（请参阅下面的“从其他库嵌入代码”）。

### 覆盖/lib中的库 {#overriding-libraries-in-lib}

位于以下位置的客户端库 `/apps` 文件夹优先于位于中的同名文件夹 `/libs`。 例如，优先 `/apps/cq/ui/widgets` 于 `/libs/cq/ui/widgets`。 当这些库属于同一类别时，将使用以下 `/apps` 库。

### 查找客户端库文件夹并使用代理客户端库Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客户端库文件夹位于存储库 `/etc/clientlibs` 的下方。 这仍受支持，但建议现在将客户端库放在下 `/apps`。 这是在其他脚本附近找到客户端库，这些脚本通常位于和 `/apps` 下面 `/libs`。

>[!NOTE]
>
>客户端库文件夹下的静态资源必须位于名为resources的文 *件夹中*。 如果文件夹资源下没有静态资源（如图像） **，则无法在发布实例上引用它。 以下是一个示例：https://localhost:4503/etc.clientlibs/geometrixx/components/clinetlibs/resources/example.gif

>[!NOTE]
>
>为了更好地将代码与内容和配置隔离，建议在下面找到客户端库，并 `/apps` 通过利用属 `/etc.clientlibs` 性来公开 `allowProxy` 它们。

为了能够访问所述客户端 `/apps` 库，使用代理服务器。 ACL仍然强制在客户端库文件夹上，但是，如果属性设置为，Servlet允许 `/etc.clientlibs/` 通过 `allowProxy` 读取内容 `true`。

静态资源只能通过代理访问，如果它位于客户端库文件夹下的资源下。

例如：

* 您有一个clientlib `/apps/myproject/clientlibs/foo`
* 您在 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然后，将该 `allowProxy` 属性设 `foo` 置为true。

* 然后，您可以请求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然后，您可以通过 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>使用代理客户端库时，AEM Dispatcher配置可能需要更新以确保允许具有扩展clientlibs的URI。

>[!CAUTION]
>
>Adobe建议在下面找到客户 `/apps` 端库，并使用代理servlet使其可用。 但是，请记住，最佳做法仍然要求公共站点不要包含直接在某个或路径上提供的任 `/apps` 何内 `/libs` 容。

### 创建客户端库文件夹 {#create-a-client-library-folder}

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 选择要在其中找到客户端库文件夹的文件夹，然后单击“创 **建”>“创建节点”**。
1. 输入库文件的名称，然后在“类型”(Type)列表中选择 `cq:ClientLibraryFolder`。 单击“ **确定** ”，然后单击“ **全部保存”**。
1. 要指定库所属的类别或类别，请选择节 `cq:ClientLibraryFolder` 点，添加以下属性，然后单击“全 **部保存”**:

   * 名称：类别
   * 类型：字符串
   * 值：类别名称
   * 多：选择

1. 通过任何方式将源文件添加到库文件夹。 例如，使用WebDav客户端复制文件，或创建文件并手动创作内容。

   **** 注意：您可以根据需要在子文件夹中组织源文件。

1. 选择客户端库文件夹，然后单击“ **创建”>“创建文件”**。
1. 在文件名框中，键入以下文件名之一，然后单击“确定”:

   * **`js.txt`**:使用此文件名生成JavaScript文件。
   * **`css.txt`**:使用此文件名生成层叠样式表。

1. 打开文件并键入以下文本以标识源文件路径的根：

   `#base=*[root]*`

   将* `[root]`*替换为包含源文件的文件夹（相对于TXT文件）的路径。 例如，当源文件与TXT文件位于同一文件夹中时，请使用以下文本：

   `#base=.`

   以下代码将根设置为节点下名为mobile的文 `cq:ClientLibraryFolder` 件夹：

   `#base=mobile`

1. 在下面几行 `#base=[root]`中，键入源文件相对于根的路径。 将每个文件名放在单独的行上。
1. 单击“ **全部保存**”。

### 链接到依赖关系 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，将其他库标识为依赖关系。 在JSP中，引用客 `ui:includeClientLib` 户端库文件夹的标记会导致HTML代码包含指向生成的库文件以及依赖关系的链接。

依赖关系必须是另一个 `cq:ClientLibraryFolder`。 要标识依赖关系，请向节点添加一 `cq:ClientLibraryFolder` 个具有以下属性的属性：

* **** 名称：依赖性
* **** 类型：字符串[]
* **** 值：当前库文件夹所依赖的cq:ClientLibraryFolder节点的categories属性的值。

例如，/具 `etc/clientlibs/myclientlibs/publicmain` 有对库的依 `cq.jquery` 赖性。 引用主客户端库的JSP生成包含以下代码的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 从其他库中嵌入代码 {#embedding-code-from-other-libraries}

您可以将客户端库中的代码嵌入到另一个客户端库中。 在运行时，嵌入库的生成JS和CSS文件包括嵌入库的代码。

嵌入代码对于提供对存储在存储库的安全区域中的库的访问是有用的。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最好将所有应用程序相关文件保留在下面的应用程序文件夹中 `/app`。 拒绝网站访问该文件夹的访客访问也是最佳做 `/app` 法。 为了同时满足这两种最佳实践，请在嵌入以下客户端库的 `/etc` 文件夹下创建一个客户端库文件夹 `/app`。

使用类别属性标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性属性向嵌 `cq:ClientLibraryFolder` 入节点添加属性：

* **** 名称：嵌入
* **** 类型：字符串[]
* **** 值：要嵌入的节点的categories属 `cq:ClientLibraryFolder` 性的值。

#### 使用嵌入最小化请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现，发布实例为典型页面生成的最终HTML包含相对大量的元素，尤其是当您的站点使用Client Context信息进行分析或定位时。 `<script>` 例如，在未优化的项目中，您可能会在页面的HTML中 `<script>` 找到以下一系列元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/underscore.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在这种情况下，将所有必需的客户端库代码合并到单个文件中以减少页面加载时来回请求的数量可能很有用。 为此，您可以使用 `embed` 节点的embed属性将所需的库添加到特定于应用程序的客户端 `cq:ClientLibraryFolder` 库中。

AEM包含以下客户端库类别。 您应仅嵌入特定站点运行所需的内容。 但是， **您应该维护此处列出的订单**:

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

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源的路径。 例如，可公开访问的库嵌入 `/etc/client/libraries/myclientlibs/publicmain` 了客户 `/apps/myapp/clientlib` 端库：

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

使用客 `channels` 户端库文件夹的属性标识使用该库的移动用户组。 当同 `channels` 一类别的库针对不同的设备功能进行设计时，该属性很有用。

要将客户端库文件夹与设备组关联，请向节点添加一个属性，该属 `cq:ClientLibraryFolder` 性具有以下属性：

* **** 名称：频道
* **** 类型：字符串[]
* **** 值：移动用户组的名称。 要从组中排除库文件夹，请在名称前加感叹号(“!”)。

例如，下表列出了类别中每个客 `channels` 户端库文件夹的属性 `cq.widgets` 值：

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

AEM支持可插拔的预处理器，并附带对 [UYI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) for CSS和JavaScript以及 [Google Closure Compiler(GCC)](https://developers.google.com/closure/compiler/) for JavaScript的支持，并且YUI设置为AEM的默认预处理器。

可插拔的预处理器允许灵活使用，包括：

* 定义可处理脚本源的脚本处理器
* 可配置处理器
* 处理器可用于微型化，但也可用于非微型化情况
* clientlib可以定义要使用哪个处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 有关已知 [问题的列表](https://github.com/yui/yuicompressor/issues) ，请参阅YUI压缩程序GitHub文档。 为特定客户端切换到GCC压缩程序可解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>请勿将受限库放在客户端库中。 请改为提供原始库，如果需要进行微型化，请使用预处理器的选项。

### 使用情况 {#usage}

您可以选择根据客户端库或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 并在 `jsProcessor` clientlibrary节点上添加

* 或通过 **HTML Library Manager** OSGi配置定义系统默认配置

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

#### YUI压缩程序，用于CSS缩小和GCC，用于JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript to Preproser and Then GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有关GCC选项的更多详细信息，请参阅 [GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 设置系统默认简写符 {#set-system-default-minifier}

在AEM中，YUI设置为默认的minifier。 要将此更改为GCC，请执行以下步骤。

1. 请访问Apache Felix Config Manager，网址为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 查找和编辑 **Adobe Granite HTML Library Manager**。
1. 启用“ **Minify** ”选项（如果尚未启用）。
1. 将“ **JS Processor Default Configs(** JS处理器默认配置)”值设置为 `min:gcc`。

   如果以分号(例如， `min:gcc;obfuscate=true`.

1. Click **Save** to save the changes.

## 调试工具 {#debugging-tools}

AEM提供了多种工具，用于调试和测试客户端库文件夹。

### 请参阅嵌入的文件 {#see-embedded-files}

要跟踪嵌入代码的源，或确保嵌入的客户端库生成预期的结果，您可以在运行时查看嵌入的文件名称。 要查看文件名，请在网 `debugClientLibs=true` 页的URL后面附加该参数。 生成的库包含语 `@import` 句而不是嵌入代码。

在上一个“从其他库 [嵌入代码”部分的示例中](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) ，客户端库文件夹 `/etc/client/libraries/myclientlibs/publicmain` 会嵌入客户端库 `/apps/myapp/clientlib` 文件夹。 将参数附加到网页后，将在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开文 `publicmain.css` 件会显示以下代码：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，在HTML的URL后面附加以下文本：

   `?debugClientLibs=true`
1. 载入页面时，查看页面源。
1. 单击作为链接元素的href提供的链接以打开文件并查看源代码。

### Discover客户端库 {#discover-client-libraries}

该组 `/libs/cq/ui/components/dumplibs/dumplibs` 件会生成有关系统上所有客户端库文件夹的信息页面。 节 `/libs/cq/ui/content/dumplibs` 点将组件作为资源类型。 要打开页面，请使用以下URL（根据需要使用不同的主机和端口）:

[https://localhost:4502/libs/cq/ui/content/dumplibs.test.html](https://localhost:4502/libs/cq/ui/content/dumplibs.test.html)

信息包括库路径和类型（CSS或JS）以及库属性的值，如类别和依赖关系。 页面上的后续表显示了每个类别和渠道中的库。

### 请参阅生成的输出 {#see-generated-output}

该组 `dumplibs` 件包括测试选择器，它显示为标记生成的源代 `ui:includeClientLib` 码。 该页面包含js、css和主题属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：

   * 在页面 `dumplibs.html` 中，单击单击此处以输 **出测试文本中的链接** 。

   * 在Web浏览器中打开以下URL（根据需要使用其他主机和端口）:

      [https://localhost:4502/libs/cq/ui/content/dumplibs.html](https://localhost:4502/libs/cq/ui/content/dumplibs.html)
   默认页面显示没有类别属性值的标记的输出。

1. 要查看类别的输出，请键入客户端库属性的值，然 `categories` 后单击“提 **交查询”**。

## 为开发和生产配置库处理 {#configuring-library-handling-for-development-and-production}

HTML库管理器服务在运行时 `cq:ClientLibraryFolder` 处理标记并生成库。 环境、开发或生产的类型决定了您应如何配置服务：

* 提高安全性：禁用调试
* 提高性能：删除空白并压缩库。
* 提高可读性：包括空格，但不压缩。

有关配置服务的信息，请参 [阅AEM HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
