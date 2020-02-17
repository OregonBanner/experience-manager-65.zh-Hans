---
title: AEM Core Concepts
seo-title: 基本信息
description: 概述AEM的结构化方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
seo-description: 概述AEM的结构化方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: 2d0e0325d1fce2587e4766bf2f60fc5d4accf45b

---


# AEM Core Concepts {#aem-core-concepts}

>[!NOTE]
>
>在深入了解AEM的核心概念之前，Adobe建议完成 [](/help/sites-developing/getting-started.md) Getting Started Developing AEM Sites文档中的WKND教程，以了解AEM开发过程的概述和核心概念的简介。

## 在AEM上进行开发的先决条件 {#prerequisites-for-developing-on-aem}

在AEM的基础上进行开发时，您需要以下技能：

* Web应用程序技术的基本知识，包括：

   * request -response(XMLHttpRequest / XMLHttpResponse)循环
   * HTML
   * CSS
   * JavaScript

* Experience Server(CRX)（包括Content Explorer）的工作知识
* 为了在经典UI中进行开发，还需要JSP(JavaServer Pages)的基本知识，包括理解和修改简单JSP示例的能力。

还建议您阅读并遵循准则和最 [佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java内容存储库 {#java-content-repository}

Java内容存储库(JCR)标准 [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)，指定了一种独立于供应商和独立于实施的方式，用于在内容存储库的粒度级别上双向访问内容。

Adobe Research(Switzerland)AG持有规范领先者。

JCR [API 2.0包](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) , javax.jcr。&amp;ast;用于直接访问和操作存储库内容。

## Experience Server(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience server提供AEM所构建并可用于构建自定义应用程序的Experience Services，并嵌入基于Jackrabbit的内容存储库。

[Apache Jackrabbit](https://jackrabbit.apache.org/) 是JCR API 2.0的一个开放源，完全符合要求。

## Sling请求处理 {#sling-request-processing}

### Sling简介 {#introduction-to-sling}

AEM是使用 [Sling](https://sling.apache.org/site/index.html)构建的，Sling是一个基于REST原则的Web应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit）或AEM（如为CRX内容存储库）作为其数据存储。 Sling已经为Apache Software Foundation提供了帮助——有关更多信息，请访问Apache。

使用Sling时，要呈现的内容类型不是第一个处理考虑事项。 而主要考虑的问题是URL是否解析到内容对象，然后可以找到脚本来执行呈现。 这为Web内容作者提供了极好的支持，以便构建可轻松根据其要求自定义的页面。

这种灵活性的优势在具有各种不同内容元素的应用程序中显而易见，或者当您需要可轻松自定义的页面时也显而易见。 特别是，在AEM解决方案中实施Web内容管理系统（如WCM）时。

请参 [阅15分钟后发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) ，了解使用Sling进行开发的最初步骤。

下图说明了Sling脚本分辨率：它演示了如何从HTTP请求到内容节点，从内容节点到资源类型，从资源类型到脚本，以及可以使用哪些脚本变量。

![chlimage_1-84](assets/chlimage_1-97.png)

下图说明了处理SlingPostServlet时可以使用的所有隐藏但功能强大的请求参数，SlingPostServlet是所有POST请求的默认处理函数，为您提供了在存储库中创建、修改、删除、复制和移动节点的无限选项。

![chlimage_1-85](assets/chlimage_1-98.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling以内 *容为中心*。 这意味着，当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理会集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示或脚本与请求的某些部分（例如选择器和／或扩展）一起从资源属性中定位

### RESTful Sling {#restful-sling}

由于以内容为中心的理念，Sling实现了面向REST的服务器，因此在Web应用程序框架中具有新的概念。 优点是：

* 非常RESTful，而不仅仅是表面上；资源和表示形式在服务器内部正确建模
* 删除一个或多个数据模型

   * 以前需要：URL结构、业务对象、数据库模式；
   * 现在，它已降低为：URL = resource = JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这定义了要由相应脚本显示的内容。 为此，将从URL中提取信息。

如果我们分析以下URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以把它分解成复合部分：

| 协议 | 主机 | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具／间谍 | .printable.a4. | html | / | a/b | ? | x=12 |

**协议** HTTP

**主机** 。

**内容路径** 指定要呈现的内容的路径。 与扩展结合使用；在此示例中，它们转换为tools/spy.html。

**selector(s)** ，用于呈现内容的替代方法；在此示例中，使用A4格式的打印机友好版本。

**extension** Content格式；还指定用于渲染的脚本。

**后缀** “可用于指定其他信息”。

**参数** ，动态内容所需的任何参数。

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用以下原则：

* 映射使用从请求中提取的内容路径来定位资源
* 找到相应的资源后，将提取sling资源类型，并用于查找要用于呈现内容的脚本

下图说明了所使用的机制，将在以下各节中详细讨论该机制。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪个脚本渲染特定实体(通过在JCR节 `sling:resourceType` 点中设置属性)。 此机制比脚本访问数据实体（PHP脚本中的SQL语句可以执行）的自由度更高，因为资源可以具有多个再现。

#### 将请求映射到资源 {#mapping-requests-to-resources}

将分解请求并提取必要的信息。 系统会搜索存储库以查找所请求的资源（内容节点）:

* first Sling检查节点是否位于请求中指定的位置；例如， `../content/corporate/jobs/developer.html`
* 如果找不到节点，则会丢弃扩展，重复搜索；例如， `../content/corporate/jobs/developer`
* 如果找不到节点，则Sling将返回http代码404（找不到）。

Sling还允许JCR节点以外的其他内容成为资源，但这是一个高级功能。

### 查找脚本 {#locating-the-script}

当找到相应的资源（内容节点）时，将提 **取sling资源类型** 。 这是一个路径，用于定位要用于呈现内容的脚本。

由指定的路径 `sling:resourceType` 可以是：

* 绝对
* 相对于配置参数

   Adobe建议使用相对路径来增加移植性。

所有Sling脚本都存储在或的子文件夹 `/apps` 中 `/libs`，将按此顺序搜索这些脚本(请参阅自定 [义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

需要注意的其他几点是：

* 当需要“方法”(GET, POST)时，将根据HTTP规范（如jobs.POST.esp）以大写形式指定该方法（见下文）
* 支持各种脚本引擎：

   * `.esp, .ecma`:ECMAScript(JavaScript)页面（服务器端执行）
   * `.jsp`:Java服务器页（服务器端执行）
   * `.java`:Java Servlet编译器（服务器端执行）
   * `.jst`:JavaScript模板（客户端执行）

Felix管理控制台( `http://<host>:<port>/system/console/slingscripting`)中列出了AEM的给定实例支持的脚本引擎列表。

此外，Apache Sling还支持与其他流行脚本引擎（例如Groovy、JRuby、Freemarker）的集成，并提供了集成新脚本引擎的方法。

使用上例，如果 `sling:resourceType` 是 `hr/jobs` :

* 以。html（默认请求类型，默认格式）结尾的GET/HEAD请求和URL

   脚本为/apps/hr/jobs/jobs.esp;sling:resourceType的最后一部分构成文件名。

* POST请求（除GET/HEAD外的所有请求类型，方法名称必须为大写）

   脚本名称中将使用POST。

   脚本是 `/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以。html结尾

   For example `../content/corporate/jobs/developer.pdf`

   剧本是 `/apps/hr/jobs/jobs.pdf.esp`,后缀将添加到脚本名称。

* 包含选择器的URL

   选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、rss源或摘要。

   如果我们查看打印机友好版本，选择器可以打印 *出来*;as in `../content/corporate/jobs/developer.print.html`

   剧本是 `/apps/hr/jobs/jobs.print.esp`,选择器将添加到脚本名称。

* 如果尚未定义sling:resourceType，则：

   * 内容路径将用于搜索相应的脚本（如果基于路径的ResourceTypeProvider处于活动状态）。

      例如，其脚本将 `../content/corporate/jobs/developer.html` 在中生成搜索 `/apps/content/corporate/jobs/`。

   * 将使用主节点类型。

* 如果根本找不到脚本，则将使用默认脚本。

   默认再现当前支持纯文本(.txt)、HTML(.html)和JSON(.json)格式，所有这些格式都将列出节点的属性（格式适当）。 扩展名。res（或不带请求扩展名的请求）的默认演绎版用于假脱机资源（如果可能）。
* 对于http错误处理（代码403或404）,Sling将在以下任一位置查找脚本：

   * 自定义脚本的/apps/sling/servlet/errorhandler [位置](/help/sites-developing/customizing-errorhandler-pages.md)
   * 或标准脚本/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果多个脚本应用于给定请求，则选择具有最佳匹配项的脚本。 比赛越具体，越好；换句话说，无论任何请求扩展名或方法名称匹配如何，选择器越匹配越好。

例如，考虑访问资源类型`/content/corporate/jobs/developer.print.a4.html`的请求`sling:resourceType="hr/jobs"`

假定我们在正确的位置有以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型（主要由属性定义）之外，还 `sling:resourceType` 有资源超类型。 这通常由属性表 `sling:resourceSuperType` 示。 在尝试查找脚本时，也会考虑这些超类型。 资源超类型的优势在于，它们可以构成资源的层次结构，其中默认资源类型（由默认Servlet使用） `sling/servlet/default` 实际上是根。

资源的资源超类型可以通过两种方式定义：

* 按资 `sling:resourceSuperType` 源的属性。
* 按点 `sling:resourceSuperType` 所在节点的属 `sling:resourceType` 性。

例如：

* /

   * a
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




/x的类型层次结构为 [ c、b、a、&lt;default>] ，而/y的类型层次结构为[c、a、

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，脚本不能直接调用，因为这会打破REST服务器的严格概念；您会混合资源和陈述。

如果您直接调用表示法（脚本），则将资源隐藏在脚本中，因此框架(Sling)不再了解它。 因此，您会失去某些功能：

* 自动处理除GET之外的http方法，包括：

   * POST、PUT、DELETE，它们是使用sling默认实现处理的
   * sling: `POST.jsp` resourceType位置中的脚本

* 您的代码架构不再像原来那样清晰，结构也不那么清晰；对于大规模开发至关重要

### Sling API {#sling-api}

这使用Sling API包org.apache.sling。&amp;ast；和标记库。

### 使用sling:include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要考虑的是引用脚本中的现有元素。

更复杂的脚本（聚合脚本）可能需要访问多个资源（例如，导航、提要栏、页脚、列表元素），并通过包括该资源来 *访问*。

为此，您可以使用sling:include(&quot;/&lt;path>/&lt;resource>&quot;)命令。 这将有效地包括引用资源的定义，如下面的语句中所示，该语句引用了渲染图像的现有定义：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定义了用于开发和部署模块化应用程序和库的架构（也称为Dynamic Module System for Java）。 OSGi容器允许您将应用程序分为各个模块（OSGi术语中带有附加元信息的jar文件称为绑定），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器内实现的服务
* 容器与应用程序之间的合同

这些服务和合同提供了一种架构，使各个元素能够动态地相互发现以进行协作。

然后，OSGi框架为您提供了这些包的动态加载／卸载、配置和控制——无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息可在 [OSGi网站上找到](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此架构允许您使用特定于应用程序的模块扩展Sling。 Sling，因此CQ5使用 [Apache Felix](https://felix.apache.org/) of OSGI（开放服务网关计划）的实施，并基于OSGi Service Platform Release 4 Version 4.2规范。 它们都是在OSGi框架中运行的OSGi包的集合。

这样，您就可以对安装中的任何包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看当前状态
* 访问有关特定包的更多详细信息（如符号名称、版本、位置等）

有关 [详细信息，请参](/help/sites-deploying/web-console.md)阅Web控制台、 [OSGI配置](/help/sites-deploying/configuring-osgi.md)[和OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md) 。

## AEM环境中的开发对象 {#development-objects-in-the-aem-environment}

以下是对发展感兴趣的内容：

**项目** 项目是节点或属性。

有关操作Item对象的详细信息，请参阅 [Interface javax](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) .jcr.Item的Javadocs。

**节点（及其属性）** JCR API 2.0规范(JSR 283)中定义了节点及其属性。 它们存储内容、对象定义、渲染脚本和其他数据。

节点定义内容结构，其属性存储实际内容和元数据。

内容节点驱动渲染。 Sling从传入的请求中获取内容节点。 此节点的属性sling:resourceType指向要使用的Sling渲染组件。

节点（即JCR名称）也称为Sling环境中的资源。

例如，要获取当前节点的属性，您可以在脚本中使用以下代码：

`PropertyIterator properties = currentNode.getProperties();`

将currentNode作为当前节点对象。

有关操作节点对象的详细信息，请参阅 [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**构件** 在AEM中，所有用户输入都由构件管理。 它们通常用于控制对某段内容的编辑。

对话框是通过组合构件来构建的。

AEM已使用ExtJS构件库进行开发。

**对话框** “对话框”是一种特殊类型的构件。

要编辑内容，AEM使用由应用程序开发人员定义的对话框。 这些组件组合了一系列构件，以向用户展示编辑相关内容所需的所有字段和操作。

对话框还用于编辑元数据和各种管理工具。

**组件** ：软件组件是提供预定义服务或事件并能够与其他组件通信的系统元素。

在AEM中，组件通常用于呈现资源的内容。 当资源是页面时，呈现它的组件称为顶级组件或页面组件。 但是，组件不必呈现内容，也不必链接到特定资源；例如，导航组件将显示有关多个资源的信息。

组件的定义包括：

* 用于呈现内容的代码
* 一个对话框，用于用户输入并配置生成的内容。

**模板** 模板是特定类型页面的基础。 在“网站”选项卡中创建页面时，用户必须选择模板。 然后，通过复制此模板创建新页面。

模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。

它定义用于呈现页面的页面组件和默认内容（主要顶级内容）。 内容定义了如何呈现它，因为AEM以内容为中心。

**页面组件（顶级组件）** ，用于呈现页面的组件。

**页面** A页面是模板的“实例”。

页面具有cq:Page类型的层次节点和cq:PageContent类型的内容节点。 内容节点的属性sling:resourceType指向用于呈现页面的页面组件。

例如，要获取当前页面的名称，您可以在脚本中使用以下代码：

S`tring pageName = currentPage.getName();`

将currentPage设置为当前页面对象。 有关操作页面对象的详细信息，请参阅 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)。

**页面管理器** “页面管理器”是一个界面，它提供了页面级别操作的方法。

例如，要获取资源的包含页面，您可以在脚本中使用以下代码：

页面myPage = pageManager.getContainingPage(myResource);

将pageManager作为页面管理器对象，将myResource作为资源对象。 有关页面管理器提供的方法的详细信息，请参阅 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 存储库中的结构 {#structure-within-the-repository}

以下列表概述了您将在存储库中看到的结构。

>[!CAUTION]
>
>应谨慎更改此结构或其中的文件。
>
>进行开发时需要更改，但您应当确保完全了解所做的任何更改的含义。

>[!CAUTION]
>
>不得更改路径中的任 `/libs` 何内容。 对于配置和其他更改，将项目从复制到 `/libs` 中并 `/apps` 在中进行任何更改 `/apps`。

* `/apps`

   与应用程序相关；包括特定于您网站的组件定义。 您开发的组件可以基于上提供的现成组件 `/libs/foundation/components`。

* `/content`

   为您的网站创建的内容。

* `/etc`

* `/home`

   用户和用户组信息。

* `/libs`

   属于AEM核心的库和定义。 中的子文件夹 `/libs` 表示AEM的现成功能，例如搜索或复制。 不应修改 `/libs` 中的内容，因为它会影响AEM的工作方式。 应在下面开发特定于您网站的功能 `/apps` (请参 [阅自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

* `/tmp`

   临时工作区。

* `/var`

   由系统更改和更新的文件；例如审核日志、统计、事件处理。 该子文件夹包 `/var/classes` 含源和编译表单中已从组件脚本生成的Java Servlet。

## 环境 {#environments}

对于AEM，生产环境通常由两种不同类型的实例组成：作者 [实例和发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)。

## 调度程序 {#the-dispatcher}

Dispatcher是Adobe的缓存和／或负载平衡工具。 有关详细信息，请参 [阅调度程序](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)。

## FileVault（源修订系统） {#filevault-source-revision-system}

FileVault为JCR存储库提供文件系统映射和版本控制。 它可用于管理AEM开发项目，并完全支持在标准版控制系统（例如，Subversion）中存储和版本化项目代码、内容、配置等。

有关详细信息， [请参阅](/help/sites-developing/ht-vlttool.md) FileVault工具文档。

## 工作流 {#workflows}

您的内容通常受组织流程的约束，包括由不同参加者批准和注销等步骤。 这些流程可以表示为在AEM中定 [义和开发的工作流](/help/sites-developing/workflows-models.md)，然后根据需要应用 [到相应的内容页面](/help/sites-administering/workflows.md)[或数字资产](/help/assets/assets-workflow.md) 。

工作流引擎用于管理工作流的实施及其后续内容应用程序。

## Multi-Site Management {#multi-site-management}

多站点管理器(MSM)使您能轻松管理共享公共内容的多个网站。 MSM允许您定义站点之间的关系，以便在一个站点中的内容更改自动复制到其他站点中。

例如，网站通常以多种语言为国际受众提供。 当同一语言的站点数量较少（3到5个）时，可以手动在站点间同步内容。 但是，当网站数量增加或涉及多种语言时，自动化流程会变得更加高效。

* 高效管理网站的不同语言版本。
* 根据源站点自动更新一个或多个站点：

   * 实施通用的基本结构并跨多个站点使用通用内容。
   * 最大限度地利用可用资源。
   * 保持相同的外观。
   * 将精力集中在管理网站之间不同的内容上。

有关详细信息，请参 [阅多站点管理器](/help/sites-administering/msm.md)。