---
title: SEO 和 URL 管理最佳实践
seo-title: SEO 和 URL 管理最佳实践
description: 了解SEO最佳实践和建议，以便在AEM实施时实现这些目标。
seo-description: 了解SEO最佳实践和建议，以便在AEM实施时实现这些目标。
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7
workflow-type: tm+mt
source-wordcount: '3119'
ht-degree: 98%

---


# SEO 和 URL 管理最佳实践{#seo-and-url-management-best-practices}

搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，需要解决许多AEM项目的SEO问题。

本文档首先介绍了一些 [SEO 最佳实践](#seo-best-practices)以及在 AEM 实施上实现这些最佳实践的建议。然后，本文档更深入地介绍了第一节中提出的一些更加[复杂的实施步骤](#aem-configurations)。

## SEO 最佳实践 {#seo-best-practices}

本节介绍了一些常规的 SEO 最佳实践。

### URL {#urls}

说到构建 URL，有一些广泛接受的最佳实践。

在 AEM 项目中评估 URL 时，请问自己以下问题：

“如果用户要查看此 URL 而页面上没有内容，他们会怎样描述此页面？”

如果答案是“是”，则很可能此 URL 非常适用于搜索引擎。

以下是有关如何构建 URL 以实施 SEO 的一些常规方法：

* 使用连字符来分隔单词。

   * 使用连字符 (-) 作为分隔符来命名页面。
   * 避免使用驼峰式拼写、下划线和空格。

* 尽量避免使用查询参数。如有必要，请将查询参数限制在两个以内。

   * 如果可用，请使用目录结构指示信息架构。
   * 如果目录结构不可用，请在 URL 中使用 Sling 选择器，而不是查询字符串。除了它们提供的 SEO 价值之外，Sling 选择器还会使调度程序可以缓存页面。

* URL 的可读性越强，越好；在 URL 中显示关键字会提高 SEO 价值。

   * 在页面上使用选择器时，首选提供语义值的选择器。
   * 如果人们无法读取您的 URL，则搜索引擎也无法读取。
   * 例如：
      `mybrand.com/products/product-detail.product-category.product-name.html` 比  更可取 
`mybrand.com/products/product-detail.1234.html`

* 尽量避免使用子域，因为搜索引擎会将子域视为不同的实体，进而分割站点的 SEO 价值。

   * 相反，请使用第一级子路径。例如，使用 `www.mybrand.com/es/home.html`，而不是 `es.mybrand.com/home.html`。

   * 根据本准则，规划内容层次结构以便与内容的呈现方式匹配。

* URL 中的关键字有效性与 URL 长度和关键字位置成反比，URL 长度越长和关键字位置越靠后有效性越低。换句话说，URL 越短越好。

   * 使用 AEM 提供的 URL 缩短技术和功能删除不必要的 URL 片段。
   * 例如，`mybrand.com/en/myPage.html` 比 `mybrand.com/content/my-brand/en/myPage.html` 更可取。

* 使用规范 URL。

   * 当 URL 来自不同路径或具有不同参数或选择器时，请确保在页面上使用 `rel=canonical` 标记。

   * 可将其纳入 AEM 模板的代码中。

* 尽量将 URL 与页面标题匹配。

   * 应该鼓励内容作者遵循这种做法。

* 支持 URL 请求不区分大小写。

   * 将调度程序配置为将所有入站请求重写为小写字母。
   * 为内容作者提供使用小写字母创建页面的培训。

* 确保每个页面仅通过一种协议提供。

   * 有时，网站会通过 `http` 提供，直到用户访问包含结账或登录表单等内容的页面时为止，此时网站将切换成 `https`。当从这个页面进行链接时，如果用户可以返回到 `http` 页面并通过 `https` 进行访问，则搜索引擎会将二者作为两个单独的页面进行跟踪。

   * 目前，Google 首选的页面是 `https` 而不是 `http`。因此，通过 `https` 提供整个站点，往往会为人们的生活带来便利。

### 服务器配置 {#server-configuration}

在服务器配置方面，您可以采取以下步骤来确保仅爬取正确的内容：

* 使用 `robots.txt` 文件阻止爬取任何不应建立索引的内容。

   * 阻止对测试环境的&#x200B;**所有**&#x200B;爬网。

* 在启动包含更新的 URL 的新站点时，请实施 301 重定向以确保不会丢失现有 SEO 排名。
* 包含您的站点的网站图标。
* 实施 XML 站点地图，以更便于搜索引擎爬取您的内容。确保纳入适用于移动和/或响应式站点的移动站点地图。

## AEM 配置 {#aem-configurations}

本节介绍了配置 AEM 以遵循这些 SEO 建议所需的实施步骤。

### 使用 Sling 选择器 {#using-sling-selectors}

以前，构建企业 Web 应用程序的惯例做法是使用查询参数。

近年来的趋势是删除这些查询参数，以提高 URL 的可读性。在许多平台上，这涉及在 Web 服务器或内容分发网络 (CDN) 上实施重定向，但 Sling 让这种做法变得简单明了。Sling 选择器能够：

* 提高 URL 可读性。
* 允许您在调度程序上缓存页面，这通常会提高安全性。
* 允许您直接寻址内容，而不是让通用的 Servlet 来检索内容。这可让您体验到应用于存储库的 ACL 以及应用于调度程序的过滤器带来的好处。

#### 使用 Servlet 选择器 {#using-selectors-for-servlets}

在编写 Servlet 时，AEM 提供两个选项：

* **bin** servlet
* **Sling** servlet

以下示例说明了如何注册 Servlet 才能做到既遵循这两种模式又获得使用 Sling Servlet 的好处。

#### Bin Servlet（下一级）{#bin-servlets-one-level-down}

**Bin** Servlet 遵循许多开发人员惯用的 J2EE 编程模式。Servlet 在特定路径下注册（对于 AEM，该路径通常位于 `/bin` 下），您可以从查询字符串中提取所需的请求参数。

此类 Servlet 的 SCR 注释如下所示：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

然后，通过 `doGet` 方法中包含的 `SlingHttpServletRequest` 对象，从查询字符串中提取参数，例如：

```
String myParam = req.getParameter("myParam");
```

使用的生成 URL 如下所示：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

使用这种方法需要考虑以下几点：

* URL 本身会丢失 SEO 价值。访问站点（包括搜索引擎）的用户不会从 URL 收到任何语义价值，因为 URL 代表着程序化路径，而不是内容层次结构。
* URL 中存在查询参数，这意味着调度程序将无法缓存响应。
* 如果要保护此 Servlet 的安全，您需要在 Servlet 中实施自己的自定义安全逻辑。
* 必须（仔细）配置调度程序以公开 `/bin/myApp/myServlet`。仅公开 `/bin` 可能会允许访问某些不应对站点访客开放的 Servlet。

#### Sling servlet（下一级）{#sling-servlets-one-level-down}

**Sling** Servlet 允许您以相反的方式注册 Servlet。您无需寻址 Servlet 并根据查询参数指定希望该 Servlet 呈现的内容，而是寻址所需内容并根据 Sling 选择器指定应呈现相应内容的 Servlet。

此类 Servlet 的 SCR 注释如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

在这种情况下，URL 寻址的资源（`myPageType` 资源的一个实例）可在 Servlet 中自动访问。要访问该资源，请使用以下调用：

```
Resource myPage = req.getResource();
```

使用的生成 URL 如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

这种方法的好处是：

* 您可以通过站点层次结构和页面名称中存在的语义来获得 SEO 价值。
* 由于不存在查询参数，调度程序可以缓存响应。此外，在激活页面时，对已寻址页面进行的任何更新将使该缓存失效。
* 当用户尝试访问此 Servlet 时，应用到 `/content/my-brand/my-page` 的所有 ACL 都会生效。
* 调度程序可能已经配置为将此内容作为一项功能提供给网站。无需其他配置。

### URL 重写 {#url-rewriting}

在 AEM 中，所有网页都存储在 `/content/my-brand/my-content` 下面。虽然从存储库数据管理的角度来看这可能有用，但对您希望客户如何浏览网站来说却不一定有用，并且可能与尽量保持 URL 简短的 SEO 指导建议相冲突。此外，您可能正在从不同域名通过同一个 AEM 实例提供多个网站。

本节会回顾 AEM 中用于管理 URL 并以更易读和 SEO 友好的方式向用户展示这些 URL 的可用选项。

#### 虚 URL{#vanity-urls}

如果作者出于促销目的，希望从另一个位置访问页面，则 AEM 逐页定义的虚 URL 可能会有用。要为页面添加虚 URL，请在&#x200B;**站点**&#x200B;控制台中导航到该页面，并编辑页面属性。在&#x200B;**基本**&#x200B;选项卡的底部，您会看到可添加虚 URL 的部分。请记住，通过多个 URL 访问特定页面会分割该页面的 SEO 价值，因此，应向页面添加规范 URL 标记以避免出现此问题。

#### 本地化的页面名称 {#localized-page-names}

您可能希望向用户显示本地化页面名称中已翻译的内容。例如：

* 不要让讲西班牙语的用户导航到：
   `www.mydomain.com/es/home.html`

* 而最好是让用户访问以下 URL：
   `www.mydomain.com/es/casa.html`。

本地化页面名称的挑战在于，AEM 平台上的许多可用本地化工具都依赖于让页面名称在各个不同区域环境中匹配，以保持内容同步。

`sling:alias` 属性让您能够一举两得。可将 `sling:alias` 作为属性添加到任何资源，以便使用该资源的别名。在上一个示例中，您将拥有：

* JCR 中的页面指向：
   `…/es/home`

* 然后，向其添加属性：
   `sling:alias` = `casa`

这将允许 AEM 翻译工具（例如，多站点管理器）继续保持以下两项之间的关系：

* `/en/home`

* `/es/home`

同时，还允许最终用户与使用其母语的页面名称进行交互。

>[!NOTE]
>
>可通过[编辑“页面属性”时使用别名属性](/help/sites-authoring/editing-page-properties.md#advanced)来设置 `sling:alias` 属性。

#### /etc/map {#etc-map}

在标准 AEM 安装中：

* 对于 OSGi 配置
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 属性
   **映射位置** ( `resource.resolver.map.location`)

* 默认设置为 `/etc/map`。

可以在此位置添加映射定义来映射入站请求，和/或在 AEM 中重写页面上的 URL。

要创建新映射，请在 `/http` 或 `/https` 下的这个位置创建一个新的 `sling:Mapping` 节点。根据在此节点上设置的 `sling:match` 和 `sling:internalRedirect` 属性，AEM 会将匹配 URL 的所有流量重定向到 `internalRedirect` 属性中指定的值。

虽然这是官方 AEM 和 Sling 文档中记录的方法，但与直接使用 `SlingResourceResolver` 提供的选项相比，这种实施提供的正则表达式支持范围比较有限。此外，以这种方式实施映射可能会导致调度程序缓存失效问题。

以下示例简要介绍了这个问题是如何发生的：

1. 用户访问您的网站并请求 `https://www.mydomain.com/my-page.html`
1. 调度程序将此请求转发到发布服务器。
1. 使用 `/etc/map` 时，发布服务器将此请求解析为 `/content/my-brand/my-page` 并呈现页面。

1. 调度程序在 `/my-page.html` 处缓存响应并将响应返回给用户。
1. 内容作者对此页面进行了更改并将其激活。
1. 调度程序刷新代理发送 `/content/my-brand/my-page`**的失效请求。**&#x200B;由于调度程序没有将页面缓存在此路径中，因此仍然会缓存旧内容且该内容会过时。

有多种方法可配置自定义调度程序刷新规则，这些规则会将较短的 URL 映射到较长的 URL，以便使缓存失效。

但是，还有一个更简单的方法来处理这种情况：

1. **SlingResourceResolver 规则**

   使用 Web 控制台（例如，localhost:4502/system/console/configMgr），您可以配置 Sling 资源解析程序：

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。
   建议您将缩短 URL 所需的映射构建为正则表达式，然后在 OsgiConfignode（包含在生成中的 `config.publish`）下定义这些配置。

   可以将这些配置直接分配给属性 **URL 映射** ( `resource.resolver.mapping`)，而不是在 `/etc/map` 中定义您的映射。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在这个简单的示例中，您将删除位于任何 URL 开头位置的 `/content/my-brand/`。

   这种做法会将 URL：

   * 从 `/content/my-brand/my-page.html`
   * 转换为 `/my-page.html`

   这与尽量保持 URL 简短的建议做法是一致的。

1. **在页面上映射 URL 输出**

   在 Apache Sling 资源解析程序中定义映射后，您需要在组件中使用这些映射，以确保在页面上输出的 URL 简短整洁。为此，您可以使用 `ResourceResolver` 的 map 函数。

   例如，如果您正在实施一个自定义导航组件，该组件列出了当前页面的子页面，则可以使用如下映射方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

到目前为止，您已经与组件中的逻辑一起实施了映射，以便在将 URL 输出到页面时使用这些映射。

最后一步就是缩短的 URL 进入调度程序后如何进行处理，这正是 `mod_rewrite` 发挥作用的时候。使用 `mod_rewrite` 最大的好处是在将 URL 发送到调度程序模块&#x200B;*之前*，该 URL 会映射回其长格式。这意味着，调度程序将向发布服务器请求长 URL 并相应地对其进行缓存。因此，从发布服务器传入的任何调度程序刷新请求都将能够成功地使此内容失效。

要实施这些规则，可以在 Apache HTTP Server 配置的虚拟主机下添加 `RewriteRule` 元素。如果要将前面示例中缩短的 URL 展开，您可以实施如下规则：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 规范 URL 标记 {#canonical-url-tags}

规范 URL 标记是指放置到 HTML 文档标题中的链接标记，用于阐明搜索引擎在索引内容时应如何处理页面。这些标记带来的好处是，即使指向页面的 URL 可能存在差异，也能确保（不同版本）页面的索引是相同的。

例如，如果站点要提供打印机友好版本的页面，则搜索引擎可能会将该页面与常规版本的页面分开进行索引。规范标记会告诉搜索引擎，它们是相同的。

示例：

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

二者均会将以下标记应用于页面的标题：

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href` 可以是相对位置或绝对位置。该代码应包含在页面标记中，以确定页面的规范 URL 并输出此标记。

### 将调度程序配置为不区分大小写 {#configuring-the-dispatcher-for-case-insensitivity}

最佳实践是使用小写字母来提供所有页面。但是，您不希望当用户在 URL 中使用大写字母访问您的网站时得到 404 错误。因此，Adobe 建议您在 Apache HTTP Server 配置中添加重写规则，以将所有传入的 URL 映射为小写。此外，必须为内容作者提供使用小写字母创建页面的培训。

要配置 Apache 将所有入站流量强制转换为小写，请在 `vhost` 配置中添加以下内容：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，在 `htaccess` 文件的最上方添加以下内容：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 实施 robots.txt 以保护开发环境 {#implementing-robots-txt-to-protect-development-environments}

在爬取站点之前，搜索引擎&#x200B;*应该*&#x200B;检查站点根目录中是否存在 `robots.txt` 文件。这里强调“应该”是因为尽管 Google、Yahoo 或 Bing 等主要搜索引擎都尊循这一规则，但一些外国搜索引擎并不一定遵循。

阻止访问整个站点的最简单方法是，将名为 `robots.txt` 的文件放置到站点根目录下，并包含以下内容：

```xml
User-agent: *
Disallow: /
```

或者，在实时环境中，您可以选择禁止某些不希望索引的路径。

将 `robots.txt` 文件放在站点根目录时应当注意，调度程序刷新请求可能会清除此文件，同时 URL 映射可能会将该站点根目录放置在与 Apache HTTP Server 配置中定义的 `DOCROOT` 不同的位置。因此，通常将该文件放在站点根目录下的作者实例上，并将其复制到发布实例。

### 在 AEM 上构建 XML 站点地图 {#building-an-xml-sitemap-on-aem}

爬取程序使用 XML 站点地图来更好地理解网站的结构。虽然提供站点地图无法保证会提高 SEO 排名，但这是公认的最佳实践。您可以在 Web 服务器上手动维护要用作站点地图的 XML 文件，但我们建议以编程方式生成站点地图，这种方法可确保当作者创建新内容时，站点地图会自动反映内容更改。

要以编程方式生成站点地图，请注册一个 Sling Servlet 用于侦听 `sitemap.xml` 调用。然后，Servlet 可使用通过 Servlet API 提供的资源来查看当前页面及其子页面，以输出的 XML。随后，将该 XML 缓存在调度程序中。这个位置应在 `robots.txt` 文件的站点地图属性中引用。此外，还需要实施自定义刷新规则，以确保在激活新页面时刷新此文件。

>[!NOTE]
>
>您可以注册一个 Sling Servlet 来侦听带有 `xml` 扩展名的选择器 `sitemap`。这会让 Servlet 随时处理以如下内容结尾的 URL 请求：
>    `/<path-to>/page.sitemap.xml`
然后，您可以从请求中获取所请求的资源，并通过使用 JCR API 从内容树中的该点生成站点地图。
此类方法带来的好处是您可以从同一实例为多个网站提供提供。对 `/content/siteA.sitemap.xml` 的请求将生成 `siteA` 的站点地图，对 `/content/siteB.sitemap.xml` 的请求将生成 `siteB` 的站点地图，而无需编写额外的代码。

### 为旧版 URL 创建 301 重定向 {#creating-redirects-for-legacy-urls}

由于以下两个原因，在启动具有新结构的站点时，应在 Apache HTTP Server 中测试和实施 301 重定向，这一点很重要：

* 随着时间的推移，旧版 URL 已积累了 SEO 价值。通过实施重定向，搜索引擎可以将此价值应用于新的 URL。
* 您站点的用户可能已经为这些页面创建了书签。通过实施重定向，您可以确保将用户定向到新站点上与他们尝试访问的旧站点最匹配的页面。

请务必查看下面的“其他资源”部分，以获取关于实施 301 重定向的操作说明，以及测试重定向是否按预期工作的工具。

## 其他资源 {#additional-resources}

有关详细信息，请参阅以下其他资源：

* [资源映射](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)

