---
title: SEO 和 URL 管理最佳实践
seo-title: SEO 和 URL 管理最佳实践
description: 了解SEO最佳实践以及在AEM实施中实现这些功能的建议。
seo-description: 了解SEO最佳实践以及在AEM实施中实现这些功能的建议。
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7

---


# SEO 和 URL 管理最佳实践{#seo-and-url-management-best-practices}

搜索引擎优化(SEO)已成为许多营销人员的一个关键问题。 因此，许多AEM项目需要解决SEO问题。

本文档首先介绍了在AEM实 [施中实现这些功能的一些](#seo-best-practices) SEO最佳实践和建议。 然后，本文档将更深入地介绍第一部分中提 [出的一些更复杂](#aem-configurations) 的实施步骤。

## SEO最佳实践 {#seo-best-practices}

本节介绍一些一般的SEO最佳实践。

### URL {#urls}

在URL方面，有一些公认的最佳实践。

在AEM项目中评估URL时，请询问您自己：

“如果用户要查看此URL，而页面上没有内容，他们能否描述此页面是什么？”

如果答案是“是”，则URL很可能适用于搜索引擎。

以下是有关如何为SEO构建URL的一些一般提示：

* 使用连字符分隔单词。

   * 使用连字符(-)作为分隔符命名页面。
   * 避免使用大写、下划线和空格。

* 尽可能避免使用查询参数。 必要时，将其限制为两个或更少。

   * 如果可用，请使用目录结构指示信息架构。
   * 如果目录结构不是选项，请使用URL中的Sling选择器，而不是查询字符串。 除了它们提供的SEO值之外，sling选择器还将使调度程序的页面可缓存。

* URL的可读性越强，越好；在URL中显示关键字将提升值。

   * 在页面上使用选择器时，首选提供语义值的选择器。
   * 如果人类无法读取您的URL，则搜索引擎也无法读取。
   * 例如：
      `mybrand.com/products/product-detail.product-category.product-name.html`
优先于 `mybrand.com/products/product-detail.1234.html`

* 尽可能避免子域，因为搜索引擎会将子域视为不同的实体，从而将站点的SEO值分段。

   * 请改用一级子路径。 例如，使用 `es.mybrand.com/home.html`代替 `www.mybrand.com/es/home.html`。

   * 根据本准则，规划内容层次结构以匹配内容的呈现方式。

* URL中的关键字有效性随URL长度和关键字位置的增加而降低。 换句话说，越短越好。

   * 使用AEM提供的URL缩短技术和功能删除不必要的URL段。
   * 例如， `mybrand.com/en/myPage.html` 首选 `mybrand.com/content/my-brand/en/myPage.html`。

* 使用规范URL。

   * 当URL可以来自不同路径或具有不同参数或选择器时，请确保在页面上 `rel=canonical` 使用标记。

   * 这可以包含在AEM模板的代码中。

* 尽可能将URL与页面标题匹配。

   * 应鼓励内容作者遵循此惯例。

* URL请求中的支持大小写不敏感。

   * 将调度程序配置为将所有入站请求重写为小写字母。
   * 培训内容作者以使用小写字母创建所有页面。

* 确保每个页面仅通过一个协议提供。

   * 有时，网站会一直供应到 `http` 用户到达包含结帐或登录表单（例如，在该表单上，用户会切换到该表单）的页面为止 `https`。 在从此页面链接时，如果用户可以返回到页面并 `http` 通过这些页面进行访问， `https`则搜索引擎将作为两个单独的页面跟踪这些页面。

   * 谷歌目前更喜欢 `https` 使用页面而 `http` 非页面。 因此，它通常使每个人的生活更轻松地为整个站点服务 `https`。

### Server configuration {#server-configuration}

在服务器配置方面，您可以采取以下步骤来确保仅搜索正确的内容：

* 使用文 `robots.txt` 件阻止搜索任何不应编制索引的内容。

   * 阻止 **测试环境** 上的所有搜索。

* 在启动包含已更新URL的新站点时，请实施301重定向，以确保不会丢失现有SEO排名。
* 为您的站点加入收藏夹。
* 实施XML站点地图，使搜索引擎能更轻松地搜索您的内容。 确保为移动和／或响应式站点包含移动站点地图。

## AEM Configurations {#aem-configurations}

本节介绍配置AEM以遵循这些SEO建议所需的实施步骤。

### 使用Sling选择器 {#using-sling-selectors}

以前，使用查询参数是构建企业Web应用程序时普遍接受的惯例。

近年来的趋势是删除这些URL，以便使URL更易读。 在许多平台上，这涉及在Web服务器或内容交付网络(CDN)上实施重定向，但Sling使这变得简单明了。 Sling选择器：

* 提高URL可读性。
* 允许您在调度程序上缓存页面，并经常提高安全性。
* 允许您直接地址内容，而不是具有检索内容的通用servlet。 这样，您就可以从应用到存储库的ACL以及应用到调度程序的过滤器中受益。

#### 使用Servlet的选择器 {#using-selectors-for-servlets}

AEM在编写Servlet时提供两个选项：

* **bin** Servlets
* **Sling** Servlets

以下示例说明如何注册遵循这两种模式的servlet以及使用Sling Servlets获得的好处。

#### Bin Servlets（一级向下） {#bin-servlets-one-level-down}

**Bin** Servlets遵循许多开发者在J2EE编程中使用的模式。 Servlet在特定路径中注册，在AEM的情况下，通常在下面 `/bin`，您可以从查询字符串中提取所需的请求参数。

此类servlet的SCR注释应类似于：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

然后，通过方法中包含的对象从查询 `SlingHttpServletRequest` 字符串中提取参 `doGet` 数；例如：

```
String myParam = req.getParameter("myParam");
```

使用的生成URL类似于：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

此方法需要考虑以下几点：

* URL本身会丢失SEO值。 访问网站（包括搜索引擎）的用户不会从URL收到任何语义值，因为URL代表程序化路径，而不是内容层次结构。
* URL中存在查询参数意味着调度程序将无法缓存响应。
* 如果要保护此servlet，您需要在servlet中实现您自己的自定义安全逻辑。
* 必须（仔细）配置调度程序才能公开 `/bin/myApp/myServlet`。 仅仅公开 `/bin` 即允许访问某些不应对站点访问者开放的Servlet。

#### Sling Servlets（一级向下） {#sling-servlets-one-level-down}

**Sling** servlet允许您以相反的方式注册Servlet。 您不需要为servlet寻址并根据查询参数指定希望servlet呈现的内容，而是需要为所需内容寻址，并指定应根据Sling选择器呈现内容的servlet。

此类servlet的SCR注释应类似于：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

在这种情况下，URL地址（资源的一个实例）的资 `myPageType` 源可在servlet中自动访问。 要访问它，请致电：

```
Resource myPage = req.getResource();
```

使用的生成URL类似于：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

此方法的好处是：

* 您可以将SEO值加入其中，该值由站点层次结构和页面名称中存在的语义获取。
* 由于不存在查询参数，调度程序可以缓存响应。 此外，对已寻址页面进行的任何更新将在激活页面时使此缓存失效。
* 当用户尝试访 `/content/my-brand/my-page` 问此servlet时，应用到的所有ACL都将生效。
* 调度程序将配置为将此内容作为服务网站的功能。 无需其他配置。

### URL重写 {#url-rewriting}

在AEM中，所有网页都存储在下面 `/content/my-brand/my-content`。 虽然从存储库数据管理的角度来看，这可能很有用，但并不一定是您希望客户如何查看您的站点，并且可能与SEO指导相冲突，以尽可能缩短URL。 此外，您可能正在从同一AEM实例和不同域名中提供多个网站。

本节将审阅AEM中可用的选项，以管理这些URL并以更易读和SEO友好的方式向用户显示它们。

#### Vanity URLs {#vanity-urls}

如果作者希望从另一个位置访问页面以进行促销，则AEM的虚URL（逐页定义）可能很有用。 要为页面添加虚URL，请在“站点”控制台中导航到该页 **面** ，然后编辑页面属性。 在“基本 **** ”选项卡的底部，您会看到可添加虚URL的部分。 请记住，通过多个URL访问页面将分割页面的SEO值，因此应向页面添加规范的URL标记以避免出现此问题。

#### 本地化的页面名称 {#localized-page-names}

您可能希望向已翻译内容的用户显示本地化的页面名称。 例如：

* 而不是让讲西班牙语的用户导航到：
   `www.mydomain.com/es/home.html`

* URL最好是：
   `www.mydomain.com/es/casa.html`.

对页面名称进行本地化的挑战在于，AEM平台上的许多可用本地化工具都依赖于让页面名称在不同区域设置之间匹配，以保持内容同步。

酒店 `sling:alias` 允许您拥有我们的蛋糕，并且也可以享用。 `sling:alias` 可以作为属性添加到任何资源，以便为该资源提供别名。 在上一个示例中，您将拥有：

* JCR中的页面：
   `…/es/home`

* 然后，向其添加属性：
   `sling:alias` = `casa`

这将允许AEM翻译工具（如多站点管理器）继续保持以下关系：

* `/en/home`

* `/es/home`

同时允许最终用户以其本机语言与页面名称进行交互。

>[!NOTE]
>
>在编 `sling:alias` 辑页面属性时，可以使用 [Alias属性设置该属性](/help/sites-authoring/editing-page-properties.md#advanced)。

#### /etc/map {#etc-map}

在标准AEM安装中：

* 对于OSGi配置
   **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 属性
   **映射位置** ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

可以在此位置添加映射定义，以映射入站请求，在AEM中重写页面上的URL，或同时映射两者。

要创建新映射，请在或下的此 `sling:Mapping` 位置创建一个新 `/http` 节点 `/https`。 根据在此节 `sling:match` 点上设 `sling:internalRedirect` 置的和属性，AEM会将匹配URL的所有通信重定向到属性中指定的 `internalRedirect` 值。

虽然这是官方AEM和Sling文档中记录的方法，但与直接使用的选项相比，此实施提供的正则表达式支持在范围上是有限 `SlingResourceResolver` 的。 此外，以这种方式实施映射可能会导致调度程序缓存失效问题。

以下是此问题发生方式的示例：

1. 用户访问您的网站和请求 `https://www.mydomain.com/my-page.html`
1. 调度程序将此请求转发到发布服务器。
1. 使用 `/etc/map`时，发布服务器将此请求解析 `/content/my-brand/my-page` 到并呈现页面。

1. 调度程序在处缓存响 `/my-page.html` 应并将响应返回给用户。
1. 内容作者对此页面进行了更改并将其激活。
1. 调度程序刷新代理发送的失效请求 `/content/my-brand/my-page`**。**由于调度程序没有在此路径上缓存的页面，因此旧内容将保持缓存并将失效。

有多种方法可配置自定义调度刷新规则，这些规则将较短的URL映射到较长的URL，以便缓存失效。

但是，管理这一点还有一个更简单的方法：

1. **SlingResourceResolver规则**

   使用Web控制台（例如，localhost:4502/system/console/configMgr），您可以配置Sling资源解析程序：

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   建议您构建将URL缩短为正则表达式所需的映射，然后在构建中包含的OsgiConfig节点下定义这些配置 `config.publish`。

   可以将映射直接分 `/etc/map`配给属性URL映射 **(**`resource.resolver.mapping`)，而不是在中定义映射：

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在这个简单的示例中，您将 `/content/my-brand/` 从任何URL的开头删除它。

   这将转换URL:

   * 起始日期: `/content/my-brand/my-page.html`
   * 仅 `/my-page.html`
   这符合尽可能保持URL短的建议做法。

1. **映射页面上的URL输出**

   在Apache Sling资源解析器中定义映射后，您需要在组件中使用这些映射以确保您在页面上输出的URL简短而整洁。 您可以使用的map函数执行此操作 `ResourceResolver`。

   例如，如果您正在实现一个列出当前页面子项的自定义导航组件，则可以使用映射方法，如：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

到目前为止，您已经实现了映射以及组件中的逻辑，以在将URL输出到我们的页面时使用这些映射。

拼图的最后一部分是当这些缩短的URL进入调度程序时，处理它们，这就是 `mod_rewrite` 开始发挥作用的地方。 使用URL的最大优 `mod_rewrite` 点是，在将URL发送到调度程序模块之前， *URL* 会映射回长表单。 这意味着调度程序将从发布服务器请求长URL并相应地缓存它。 因此，从发布服务器传入的任何调度程序刷新请求都将能够成功使此内容失效。

要实施这些规则，可以在Apache HTTP `RewriteRule` 服务器配置中在虚拟主机下添加元素。 如果要从前面的示例中展开缩短的URL，您可以实现如下规则：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 规范URL标记 {#canonical-url-tags}

规范的URL标记是放置到HTML文档头中的链接标记，用于阐明搜索引擎在为内容编制索引时应如何处理页面。 他们提供的好处是确保（不同版本）页面的索引将与相同的版本，即使页面的URL可能包含差异也是如此。

例如，如果站点要提供适合打印机的页面版本，则搜索引擎可能会将此页面与页面的常规版本分开索引。 标准标签将告诉搜索引擎它们是相同的。

示例:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

这两种方法都会将以下标记应用于页面的标题：

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

可以 `href` 是相对的或绝对的。 该代码应包含在页面标记中，以确定页面的规范URL并输出此标记。

### 配置调度程序以防区分大小写 {#configuring-the-dispatcher-for-case-insensitivity}

最佳实践是使用小写字母提供所有页面。 但是，当用户使用URL中的大写字母访问您的网站时，您不希望他们获得404。 因此，Adobe建议您在Apache HTTP server配置中添加重写规则，以将所有传入的URL映射为小写。 此外，必须培训内容作者以创建其页面时使用小写名称。

要配置Apache以强制所有入站通信使用小写，请在配置中添加以下 `vhost` 内容：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，在文件的最顶部添加以下内 `htaccess` 容：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 实施robots.txt以保护开发环境 {#implementing-robots-txt-to-protect-development-environments}

搜索 *引擎* ，应在搜索站点 `robots.txt` 之前检查站点根目录中是否存在文件。 这里应该强调，因为尽管谷歌、雅虎或必应等主要搜索引擎都尊重这一点，但一些外国搜索引擎却不尊重这一点。

阻止访问整个站点的最简单方法是将一个名为的文件放 `robots.txt` 置到站点根目录下，并包含以下内容：

```xml
User-agent: *
Disallow: /
```

或者，在实时环境中，您可以选择禁止某些不希望索引的路径。

将文件放在站点根目录 `robots.txt` 的注意事项是，调度程序刷新请求可能会清除此文件，而URL映射可能会将站点根目录放置在与Apache HTTP server配置中定义的 `DOCROOT` 不同之处。 因此，通常将此文件放在站点根目录下的作者实例上并将其复制到发布实例。

### 在AEM上构建XML站点地图 {#building-an-xml-sitemap-on-aem}

爬虫程序使用XML站点地图更好地理解网站的结构。 虽然无法保证提供站点地图将改善SEO排名，但这是一项经过商定的最佳实践。 您可以手动维护Web服务器上的XML文件以用作Sitemap，但建议以编程方式生成Sitemap，这可确保作者创建新内容时，Sitemap将自动反映其更改。

要以编程方式生成sitemap，请注册一个侦听调用的Sling Servlet `sitemap.xml` 。 Servlet然后可以使用通过Servlet API提供的资源查看当前页面及其子页面，输出XML。 然后，XML将缓存在调度程序中。 此位置应在文件的sitemap属性中引 `robots.txt` 用。 此外，需要实施自定义刷新规则，以确保在激活新页面时刷新此文件。

>[!NOTE]
>
>您可以注册一个Sling Servlet以侦听带扩展 `sitemap` 的选择器 `xml`。 这将导致Servlet在请求URL时处理请求，该URL以下结束：
>    `/<path-to>/page.sitemap.xml`
然后，您可以从请求中获取所请求的资源，并通过使用JCR API从内容树中的该点生成站点地图。
这样的方法的好处是当您有多个站点从同一实例提供服务时。 请求将生 `/content/siteA.sitemap.xml` 成站点地图，而请求将生 `siteA` 成站点地图，而无需 `/content/siteB.sitemap.xml``siteB` 编写额外的代码。

### 为传统URL创建301重定向 {#creating-redirects-for-legacy-urls}

在启动具有新结构的站点时，在Apache HTTP server中实施和测试301重定向很重要，原因有二：

* 传统URL已积累了SEO值。 通过实施重定向，搜索引擎可以将此值应用于新URL。
* 您站点的用户可能已创建了指向这些页面的书签。 通过实施重定向，您可以确保将用户定向到新站点上与他们试图访问旧站点的位置最接近的页面。

请务必检查下面的其他资源部分，以获取有关实施301重定向的说明以及测试重定向是否按预期工作的工具。

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

