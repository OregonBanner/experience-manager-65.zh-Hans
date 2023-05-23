---
title: SEO和URL管理最佳作法
description: 瞭解AEM實作的SEO最佳實務和建議。
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '3678'
ht-degree: 65%

---

# SEO和URL管理最佳作法{#seo-and-url-management-best-practices}

SEO （搜尋引擎最佳化）已成為許多行銷人員的重要考量。 因此，許多AEM專案都必須解決SEO問題。

本檔案首先介紹了一些 [SEO最佳作法](#seo-best-practices) 和AEM實作的相關建議。 然后，本文档更深入地介绍了第一节中提出的一些更加[复杂的实施步骤](#aem-configurations)。

## SEO 最佳实践 {#seo-best-practices}

本节介绍了一些常规的 SEO 最佳实践。

### URL {#urls}

URL有一些公認的最佳實務。

在 AEM 项目中评估 URL 时，请问自己以下问题：

「如果使用者看見此URL但頁面上沒有任何內容，他們能否說明此頁面？」

如果能做到，那么可能该 URL 对于搜索引擎可正常工作。

以下是有关如何构建 URL 以实施 SEO 的一些常规方法：

* 使用连字符来分隔单词。

   * 使用连字符 (-) 作为分隔符来命名页面。
   * 避免使用驼峰式拼写、下划线和空格。

* 尽量避免使用查询参数。如有必要，请将查询参数限制在两个以内。

   * 如果可用，请使用目录结构指示信息架构。
   * 如果无法使用目录结构，请在 URL 中使用 Sling 选择器而非查询字符串。除了提供SEO值之外，Sling選擇器也會讓頁面可供Dispatcher快取。

* URL越易懂越好。在URL中顯示關鍵字可提升值。

   * 在页面上使用选择器时，首选提供语义值的选择器。
   * 如果人们无法读取您的 URL，则搜索引擎也无法读取。
   * 例如：
      `mybrand.com/products/product-detail.product-category.product-name.html`
优先 
`mybrand.com/products/product-detail.1234.html`

* 儘可能避免子網域，因為搜尋引擎會將子網域視為不同實體，進而分割網站的SEO值。

   * 相反，请使用第一级子路径。例如，使用 `www.mybrand.com/es/home.html`，而不是 `es.mybrand.com/home.html`。

   * 根據本指引規劃內容階層，以符合內容的呈現方式。

* URL 中的关键字有效性与 URL 长度和关键字位置成反比，URL 长度越长和关键字位置越靠后有效性越低。换句话说，URL 越短越好。

   * 使用 AEM 提供的 URL 缩短技术和功能删除不必要的 URL 片段。
   * 例如，`mybrand.com/en/myPage.html` 比 `mybrand.com/content/my-brand/en/myPage.html` 更可取。

* 使用规范 URL。

   * 当 URL 来自不同路径或具有不同参数或选择器时，请确保在页面上使用 `rel=canonical` 标记。

   * 在AEM範本的程式碼中包含標準URL。

* 尽量将 URL 与页面标题匹配。

   * 应该鼓励内容作者遵循这种做法。

* 支持 URL 请求不区分大小写。

   * 配置 Dispatcher 以使其将所有入站请求都重写为小写字母。
   * 为内容作者提供使用小写字母创建页面的培训。

* 确保每个页面仅通过一种协议提供。

   * 有时，网站会通过 `http` 提供，直到用户访问包含结账或登录表单等内容的页面时为止，此时网站将切换成 `https`。從這個頁面連結時，如果使用者可以返回 `http` 頁面並透過以下方式存取： `https`，搜尋引擎會以兩個個別頁面來追蹤這些頁面。

   * 目前，Google 首选的页面是 `https` 而不是 `http`。它們有助於讓每個人的生活更輕鬆提供整個網站 `https`.

### 服务器配置 {#server-configuration}

在服务器配置方面，您可以采取以下步骤来确保仅爬取正确的内容：

* 使用 `robots.txt` 文件阻止爬取任何不应建立索引的内容。

   * 阻止对测试环境的&#x200B;**所有**&#x200B;爬网。

* 在启动包含更新的 URL 的新站点时，请实施 301 重定向以确保不会丢失现有 SEO 排名。
* 包含您的站点的网站图标。
* 若要讓搜尋引擎更容易對您的內容進行編目，請實作XML Sitemap。 确保纳入适用于移动和/或响应式站点的移动站点地图。

## AEM 配置 {#aem-configurations}

本節說明使用下列SEO建議設定AEM的實施步驟。

### 使用 Sling 选择器 {#using-sling-selectors}

以前在构建企业 Web 应用程序时使用查询参数是公认的惯例。

近年來的趨勢是移除引數，讓URL更容易閱讀。 在許多平台上，此移除程式涉及在網頁伺服器或內容傳遞網路(CDN)上實作重新導向，但Sling可讓程式變得簡單明瞭。 Sling 选择器能够：

* 提高 URL 可读性。
* 可讓您在Dispatcher上快取頁面，並提高安全性。
* 可讓您直接處理內容，而不是使用一般servlet來擷取內容。 它會授予您套用至存放庫的ACL和套用至Dispatcher的篩選器的優點。

#### 为 Servlet 使用选择器 {#using-selectors-for-servlets}

在编写 Servlet 时，AEM 提供两个选项：

* **bin** servlet
* **Sling** servlet

以下示例阐述如何注册遵循这两个模式的 Servlet 以及使用 Sling Servlet 获得的利益。

#### Bin Servlet（下一级） {#bin-servlets-one-level-down}

**Bin** Servlet 遵循许多开发人员惯用的 J2EE 编程模式。此servlet註冊於特定路徑，而在AEM中，該路徑通常位於 `/bin`，並從查詢字串中擷取所需的請求引數。

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
* URL中存在查詢引數，代表Dispatcher無法快取回應。
* 如果您想要保護此servlet的安全，請在servlet中實作您自己的自訂安全邏輯。
* 必须（仔细地）配置 Dispatcher 以公开 `/bin/myApp/myServlet`。仅公开 `/bin` 可能会允许访问某些不应对站点访客开放的 Servlet。

#### Sling servlet（下一级） {#sling-servlets-one-level-down}

**Sling** Servlet 允许您以相反的方式注册 Servlet。您定址的是您想要的內容，而不是定址servlet並指定要讓servlet根據查詢引數呈現的內容。 而且您可以根據Sling選擇器指定應呈現內容的servlet。

此类 Servlet 的 SCR 注释如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

在此案例中，URL所處理的資源 —  `myPageType` resource — 可在servlet中自動存取。 若要存取，請呼叫下列專案：

```
Resource myPage = req.getResource();
```

使用的生成 URL 如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

这种方法的好处是：

* 您可以通过站点层次结构和页面名称中存在的语义来获得 SEO 价值。
* 既然不存在查询参数，因此 Dispatcher 可缓存响应。此外，对已寻址的页面作出任何更改，都将在激活该页面时使此缓存无效。
* 所有应用于 `/content/my-brand/my-page` 的 ACL 在用户尝试访问此 Servlet 时生效。
* Dispatcher已設定為將此內容當做網站服務的函式來提供。 无需其他配置。

### URL 重写 {#url-rewriting}

在 AEM 中，所有网页都存储在 `/content/my-brand/my-content` 下面。雖然從存放庫資料管理的角度來看，此位置很有用，但並不一定是您希望客戶如何檢視您的網站。 此外，儘可能縮短URL可能會與SEO指引衝突。 此外，您可能正在从不同域名通过同一个 AEM 实例提供多个网站。

本节会回顾 AEM 中用于管理 URL 并以更易读和 SEO 友好的方式向用户展示这些 URL 的可用选项。

#### 虚 URL {#vanity-urls}

如果作者出于促销目的，希望从另一个位置访问页面，则 AEM 逐页定义的虚 URL 可能会有用。要为页面添加虚 URL，请在&#x200B;**站点**&#x200B;控制台中导航到该页面，并编辑页面属性。在&#x200B;**基本**&#x200B;选项卡的底部，您会看到可添加虚 URL 的部分。请记住，通过多个 URL 访问特定页面会分割该页面的 SEO 价值，因此，应向页面添加规范 URL 标记以避免出现此问题。

#### 本地化的页面名称 {#localized-page-names}

您可能希望向用户显示本地化页面名称中已翻译的内容。例如：

* 不要让讲西班牙语的用户导航到：
   `www.mydomain.com/es/home.html`

* 而最好是让用户访问以下 URL：
   `www.mydomain.com/es/casa.html`。

本地化頁面名稱的挑戰在於AEM平台上許多可用的本地化工具，都仰賴讓不同地區設定的頁面名稱相符，以保持內容同步。

此 `sling:alias` 屬性可讓您同時享用Adobe蛋糕和美食。 您可以新增 `sling:alias` 作為任何資源的屬性，以允許資源的別名。 在上一個範例中，您會遇到以下問題：

* JCR 中的页面指向：
   `…/es/home`

* 然后，向其添加属性：
   `sling:alias` = `casa`

此流程可讓AEM翻譯工具（例如多網站管理員）繼續維護以下各項之間的關係：

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

要创建映射，请在 `/http` 或 `/https` 下面的此位置创建一个 `sling:Mapping` 节点。根据在此节点上设置的 `sling:match` 和 `sling:internalRedirect` 属性，AEM 会将匹配 URL 的所有流量重定向到 `internalRedirect` 属性中指定的值。

雖然此方法已記錄在官方AEM和Sling檔案中，但與使用提供的選項相比，此實作提供的規則運算式支援範圍有限。 `SlingResourceResolver` 直接。 此外，以这种方式实现映射可能会导致 Dispatcher 缓存失效问题。

以下示例简要介绍了这个问题是如何发生的：

1. 用户访问您的网站并请求 `https://www.mydomain.com/my-page.html`
1. Dispatcher 将此请求转发到发布服务器。
1. 通过使用 `/etc/map`，发布服务器将此请求解析到 `/content/my-brand/my-page` 并呈现该页面。

1. Dispatcher 在 `/my-page.html` 处缓存响应并将响应返回给用户。
1. 内容作者更改此页面并激活它。
1. Dispatcher 刷新代理发送对 `/content/my-brand/my-page`**的无效请求。** 由於Dispatcher在此路徑上沒有經過快取的頁面，因此系統會維持對舊內容進行快取，導致內容過時。

有多种方法可配置自定义调度-刷新规则，这些规则会将较短的 URL 映射到较长的 URL，以便使缓存失效。

不過，也有更簡單的方法可管理此問題：

1. **SlingResourceResolver 规则**

   使用 Web 控制台（例如，localhost:4502/system/console/configMgr），您可以配置 Sling 资源解析程序：

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。
   Adobe建議您建置所需對應來將URL縮短為規則運算式，然後在OsgiConfignode下定義這些設定。 `config.publish` 包含在您的組建中。

   可以将这些配置直接分配给属性 **URL 映射** ( `resource.resolver.mapping`)，而不是在 `/etc/map` 中定义您的映射。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在这个简单的示例中，您将删除位于任何 URL 开头位置的 `/content/my-brand/`。

   它會轉換URL：

   * 从 `/content/my-brand/my-page.html`
   * 转换为 `/my-page.html`

   此轉換符合將URL儘量縮短的建議做法。

1. **在页面上映射 URL 输出**

   在Apache Sling Resource Resolver中定義對應後，請在元件中使用這些對應，以確保您在頁面上輸出的URL簡短且整齊。 您可以使用 `ResourceResolver`.

   例如，如果您正在实施一个自定义导航组件，该组件列出了当前页面的子页面，则可以使用如下映射方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

到目前為止，您已經與元件中的邏輯一起實作對應，以便在將URL輸出至頁面時使用這些對應。

最后一步就是缩短的 URL 进入 Dispatcher 后如何进行处理，这正是 `mod_rewrite` 发挥作用的时候。使用 `mod_rewrite` 最大的好处是，在将 URL 发送到 Dispatcher 模块&#x200B;*之前*，该 URL 会映射回其长格式。此流程意味著Dispatcher會向發佈伺服器請求長URL並據以快取。 因此，從發佈伺服器傳入的任何Dispatcher排清請求都可以成功讓此內容失效。

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

规范 URL 标记是指放置到 HTML 文档标题中的链接标记，用于阐明搜索引擎在索引内容时应如何处理页面。这些标记带来的好处是，即使指向页面的 URL 可能存在差异，也能确保（不同版本的）页面的索引是相同的。

例如，如果站点要提供打印机友好版本的页面，则搜索引擎可能会将该页面与常规版本的页面分开进行索引。规范标记会告诉搜索引擎，它们是相同的。

示例：

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

二者均会将以下标记应用于页面的标题：

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

`href` 可以是相对位置或绝对位置。该代码应包含在页面标记中，以确定页面的规范 URL 并输出此标记。

### 将 Dispatcher 配置为不区分大小写 {#configuring-the-dispatcher-for-case-insensitivity}

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

在爬取站点之前，搜索引擎&#x200B;*应该*&#x200B;检查站点根目录中是否存在 `robots.txt` 文件。雖然Google、Yahoo或Bing等主要搜尋引擎都會遵守此檔案，但有些外國搜尋引擎並不遵循。

阻止访问整个站点的最简单方法是，将名为 `robots.txt` 的文件放置到站点根目录下，并包含以下内容：

```xml
User-agent: *
Disallow: /
```

或者，在实时环境中，您可以选择禁止某些不希望索引的路径。

放置 `robots.txt` 網站根目錄中的檔案表示Dispatcher排清請求可能會清除此檔案。 此外，URL對應可能會將網站根目錄放置在與 `DOCROOT` 如Apache HTTP Server設定中所定義。 因此，通常将该文件放在站点根目录的作者实例上，并将其复制到发布实例。

### 在 AEM 上构建 XML Sitemap {#building-an-xml-sitemap-on-aem}

爬取程序使用 XML 站点地图来更好地理解网站的结构。虽然提供站点地图无法保证会提高 SEO 排名，但这是公认的最佳实践。您可以在網頁伺服器上手動維護XML檔案，以做為網站地圖。 不過，Adobe建議您以程式設計方式產生Sitemap，以確保在作者建立內容時，Sitemap會自動反映其變更。

AEM 使用 [Apache Sling Sitemap 模块](https://github.com/apache/sling-org-apache-sling-sitemap)生成 XML 站点地图，这将为开发人员和编辑人员提供一系列广泛的选项，以使站点的 XML 站点地图保持最新。

>[!NOTE]
>
>自Adobe Experience Manager 6.5.11.0版起可做為產品功能使用。
> 
>若是舊版，您可以自行註冊Sling Servlet，以便接聽 `sitemap.xml` 呼叫。 使用透過servlet API提供的資源來查詢目前頁面及其子系，以輸出 `sitemap.xml` 檔案。

Apache Sling Sitemap 模块将区分为 `sling:sitemapRoot` 属性设置为 `true` 的任何资源生成的顶级站点地图和嵌套站点地图。 通常，使用树的顶级站点地图路径上的选择器来呈现站点地图，而顶级站点地图是没有其他站点地图根祖先的资源。 此顶级站点地图根还公开站点地图索引，该索引通常是站点所有者将在搜索引擎的配置门户中配置或添加到站点的 `robots.txt` 的内容。

例如，考虑一个在 `my-page` 定义顶级站点地图并在 `my-page/news` 定义嵌套站点地图的网站，以便为新闻子树中的页面生成专用站点地图。 生成的相关 URL 将为

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>选择器 `sitemap` 和 `sitemap-index` 可能会干扰自定义实现。如果您不想使用产品功能，请使用高于 0 的 `service.ranking` 来配置用于这些选择器的自己的 servlet。

在默认配置中，“页面属性”对话框提供了一个选项，用于将页面标记为 Sitemap 根（如上所述）并生成 Sitemap 本身及其后代。此行为通过实施 `SitemapGenerator` 接口来实现，并且可以通过添加替代实施进行扩展。不過，由於重新產生XML Sitemap的頻率取決於內容製作工作流程和工作負載，因此產品未提供任何內容 `SitemapScheduler` 設定。 如此一來，此功能就能有效選擇加入。

啟用產生XML Sitemap的背景工作 `SitemapScheduler` 必須設定。 为此，可为 PID `org.apache.sling.sitemap.impl.SitemapScheduler` 创建 OSGI 配置。调度程序表达式 `0 0 0 * * ?` 可用作起点，以在每天的午夜重新生成所有 XML Sitemap 一次。

![Apache Sling Sitemap - 调度程序](assets/sling-sitemap-scheduler.png)

Sitemap產生工作可在作者和發佈層執行個體上執行。 通常建議在發佈層執行個體上執行產生，因為只能在那裡產生適當的規範URL（因為Sling資源對應規則通常只存在於發佈層執行個體上）。 不過，您可以透過實作 [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) 介面。 如果自訂實作能在作者層級執行個體上產生Sitemap的標準URL，則 `SitemapScheduler` 可以為作者執行模式設定。 此外，XML Sitemap產生工作負載可分佈於製作服務叢集的執行個體上。 在此案例中，處理尚未發佈、已修改或僅對受限使用者群組可見的內容時，必須小心。

AEM Sites 包含 `SitemapGenerator` 的默认实施，它将遍历页面树以生成 Sitemap。它预先配置为仅输出站点的规范 URL 和任何语言替代项（如果可用）。如果需要，它还可以配置为包含页面的上次修改日期。若要這麼做，請啟用 _新增上次修改時間_ 的選項 _AdobeAEM SEO — 頁面樹狀Sitemap產生器_ 設定並選取 _上次修改來源_. 在发布层上生成站点地图时，建议使用 `cq:lastModified` 日期。

![Adobe AEM SEO - 页面树 Sitemap 生成器配置](assets/sling-sitemap-pagetreegenerator.png)

要限制 Sitemap 的内容，可以在需要时实施以下服务接口：

* 可以实施 [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html)，以在由 AEM Sites 特定的 Sitemap 生成器生成的 XML Sitemap 中隐藏页面
* 可以实施 [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) 或 [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html)，以从由 [Commerce 集成框架](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html)特定的 Sitemap 生成器生成的 XML Sitemap 筛选出产品或类别

如果預設實作不適用於特定使用案例，或擴充功能點不夠靈活，請實作自訂 `SitemapGenerator` 以完全控制所產生Sitemap的內容。 以下範例使用AEM Sites的預設實作邏輯。 它使用 [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) 作为起点来遍历页面树：

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, etc
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

此外，針對XML Sitemap實作的功能也可用於不同的使用案例，例如新增規範連結或語言替代專案至頁面標題。 另請參閱 [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) 介面以取得詳細資訊。

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
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
