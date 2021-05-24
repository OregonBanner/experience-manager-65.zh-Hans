---
title: AEM核心概念
seo-title: 基本信息
description: 概述了AEM的结构方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
seo-description: 概述了AEM的结构方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 78e28636eec331314c2f29c93d516215b1572f20
workflow-type: tm+mt
source-wordcount: '3367'
ht-degree: 0%

---

# AEM核心概念{#aem-core-concepts}

>[!NOTE]
>
>在深入研究AEM的核心概念之前，Adobe建议先完成[AEM Sites开发入门](/help/sites-developing/getting-started.md)文档中的WKND教程，以了解AEM开发流程概述和核心概念简介。

## 在AEM {#prerequisites-for-developing-on-aem}上开发的先决条件

要在AEM上进行开发，您需要以下技能：

* Web应用技术的基本知识，包括：

   * 请求 — 响应(XMLHttpRequest / XMLHttpResponse)周期
   * HTML
   * CSS
   * JavaScript

* Experience Server(CRX)（包括内容资源管理器）的工作知识
* 要在经典UI中进行开发，还需要具备JSP(JavaServer Pages)的基本知识，包括理解和修改简单JSP示例的能力。

还建议您阅读并遵循[准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java内容存储库{#java-content-repository}

Java内容存储库(JCR)标准[JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)指定了一种独立于供应商和独立于实施的方式，用于在内容存储库的粒度级别上双向访问内容。

Adobe研究公司（瑞士）AG持有规范领先。

[JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html)包， javax.jcr。&amp;ast;用于直接访问和处理存储库内容。

## Experience Server(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供AEM构建的Experience Services，并可利用该Experience Services构建自定义应用程序，同时它基于Jackrabbit嵌入内容存储库。

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis是JCR API 2.0的开放源代码，完全符合其实施要求。

## Sling请求处理{#sling-request-processing}

### Sling {#introduction-to-sling}简介

AEM是使用[Sling](https://sling.apache.org/site/index.html)构建的，Sling是一个基于REST原则的Web应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit）作为其数据存储，对于AEM，则使用CRX内容存储库。 Sling已对Apache Software Foundation做出了贡献 — 有关更多信息，请参阅Apache 。

使用Sling时，要呈现的内容类型不是首要处理考虑事项。 相反，主要考虑的是URL是否解析为内容对象，随后可以找到用于执行渲染的脚本。 这为Web内容作者构建可轻松根据其要求进行自定义的页面提供了绝佳支持。

在具有多种不同内容元素的应用程序中，或者您需要能够轻松自定义的页面时，这种灵活性的优势显而易见。 特别是，在实施Web内容管理系统(如AEM解决方案中的WCM)时。

请参阅[在15分钟内发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) ，了解使用Sling进行开发的首要步骤。

下图说明了Sling脚本解析：它显示了如何从HTTP请求到内容节点、从内容节点到资源类型、从资源类型到脚本，以及哪些脚本变量可用。

![了解Apache Sling脚本解析](assets/sling-cheatsheet-01.png)

下图说明了处理SlingPostServlet时可以使用的所有隐藏但功能强大的请求参数，SlingPostServlet是所有POST请求的默认处理程序，为您提供了无穷尽的选项，用于在存储库中创建、修改、删除、复制和移动节点。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心{#sling-is-content-centric}

Sling以&#x200B;*以内容为中心*。 这意味着当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理重点会放在内容上：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示或脚本是与请求的某些部分（例如，选择器和/或扩展）组合在资源属性中找到的

### RESTful Sling {#restful-sling}

由于以内容为中心的理念，Sling实施了面向REST的服务器，因此在Web应用程序框架中具有新的概念。 优点是：

* 非常RESTful，不仅仅在表面；资源和表示在服务器内正确建模
* 删除一个或多个数据模型

   * 以前需要满足以下条件：URL结构、业务对象、数据库模式；
   * 现在已简化为：URL = resource = JCR结构

### URL分解{#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这定义了要由相应脚本显示的内容。 为此，将从URL中提取信息。

如果我们分析以下URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以把它分解成复合部分：

| 协议 | 主机 | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/间谍 | .printable.a4. | html | / | a/b | ? | x=12 |

**** protocolHTTP

**** hostName网站。

**content** path指定要呈现的内容的路径。与扩展结合使用；在本例中，它们将转换为tools/spy.html。

**选择器** ，用于呈现内容的替代方法；在本例中，是A4格式的打印机友好版本。

**** extensionContent格式；还指定用于渲染的脚本。

**** suffixCanable用于指定其他信息。

**参数** 动态内容所需的任何参数。

#### 从URL到内容和脚本{#from-url-to-content-and-scripts}

使用以下原则：

* 映射使用从请求提取的内容路径来查找资源
* 在找到相应的资源后，将提取sling资源类型，并用于找到用于渲染内容的脚本

下图说明了所使用的机制，将在以下各节中详细讨论该机制。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪个脚本渲染特定实体（通过在JCR节点中设置`sling:resourceType`属性）。 此机制比脚本在其中访问数据实体（如PHP脚本中的SQL语句那样）的自由度更高，因为资源可以具有多个演绎版。

#### 将请求映射到资源{#mapping-requests-to-resources}

请求被划分，并提取必要的信息。 在存储库中搜索所请求的资源（内容节点）：

* 首先， Sling检查某个节点是否位于请求中指定的位置；例如`../content/corporate/jobs/developer.html`
* 如果找不到节点，则删除扩展并重复搜索；例如`../content/corporate/jobs/developer`
* 如果未找到节点，则Sling将返回http代码404（未找到）。

Sling还允许JCR节点以外的其他内容作为资源，但这是一项高级功能。

### 查找脚本{#locating-the-script}

在找到相应的资源（内容节点）后，将提取&#x200B;**sling资源类型**。 这是一个路径，用于查找用于呈现内容的脚本。

`sling:resourceType`指定的路径可以是：

* 绝对
* 相对于配置参数

   Adobe建议使用相对路径，因为它们可增加可移植性。

所有Sling脚本都存储在`/apps`或`/libs`的子文件夹中，这些子文件夹将按此顺序进行搜索（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

需要注意的其他几点是：

* 当需要方法(GET、POST)时，它将根据HTTP规范(如jobs.POST.esp)以大写形式指定（请参阅下文）
* 支持各种脚本引擎：

   * HTL(HTML模板语言 — Adobe Experience Manager首选和推荐的HTML服务器端模板系统):`.html`
   * ECMAScript(JavaScript)页面（服务器端执行）：`.esp, .ecma`
   * Java服务器页面（服务器端执行）：`.jsp`
   * Java Servlet编译器（服务器端执行）：`.java`
   * JavaScript模板（客户端执行）：`.jst`

给定AEM实例支持的脚本引擎列表列在Felix管理控制台(`http://<host>:<port>/system/console/slingscripting`)上。

此外，Apache Sling支持与其他常用脚本引擎（例如Groovy、JRuby、Freemarker）集成，并提供了一种集成新脚本引擎的方法。

使用上例，如果`sling:resourceType`为`hr/jobs`，则表示：

* GET/HEAD请求和以.html结尾的URL（默认请求类型，默认格式）

   脚本为/apps/hr/jobs/jobs.esp;sling:resourceType的最后一部分构成文件名。

* POST请求(除GET/HEAD以外的所有请求类型，方法名称必须大写)

   POST将用在脚本名称中。

   脚本将为`/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以.html结尾

   例如`../content/corporate/jobs/developer.pdf`

   脚本将为`/apps/hr/jobs/jobs.pdf.esp`;后缀会添加到脚本名称中。

* 包含选择器的URL

   选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、rss源或摘要。

   如果我们查看打印机友好版本，其中选择器可以是&#x200B;*print*;如`../content/corporate/jobs/developer.print.html`

   脚本将为`/apps/hr/jobs/jobs.print.esp`;选择器即会添加到脚本名称中。

* 如果尚未定义sling:resourceType，则：

   * 内容路径将用于搜索相应的脚本（如果基于路径的ResourceTypeProvider处于活动状态）。

      例如，`../content/corporate/jobs/developer.html`的脚本将在`/apps/content/corporate/jobs/`中生成搜索。

   * 将使用主节点类型。

* 如果根本找不到脚本，则将使用默认脚本。

   默认呈现版本当前支持纯文本(.txt)、HTML(.html)和JSON(.json)格式，所有这些格式都将列出节点的属性（格式合适）。 扩展名.res或没有请求扩展名的请求的默认呈现形式是将资源设置为假脱机（如果可能）。
* 对于http错误处理（代码403或404），Sling将在以下任一位置查找脚本：

   * 用于[自定义脚本](/help/sites-developing/customizing-errorhandler-pages.md)的/apps/sling/servlet/errorhandler位置
   * 或标准脚本/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果给定请求应用多个脚本，则会选择具有最佳匹配项的脚本。 比赛越具体，越好；换言之，无论任何请求扩展名或方法名称是否匹配，选择器越匹配越好。

例如，考虑请求访问资源
`/content/corporate/jobs/developer.print.a4.html`
类型
`sling:resourceType="hr/jobs"`

假设我们在正确位置中有以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

然后，优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型（主要由`sling:resourceType`属性定义）之外，还有资源超类型。 这通常由`sling:resourceSuperType`属性指示。 在尝试查找脚本时，还会考虑这些超类型。 资源超级类型的优势在于，它们可以形成资源层次结构，其中默认资源类型`sling/servlet/default`（默认Servlet使用）实际上是根。

资源的资源超类型可以通过两种方式进行定义：

* 按资源的`sling:resourceSuperType`属性。
* `sling:resourceType`所指向节点的`sling:resourceSuperType`属性。

例如：

* /

   * 某个 
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




以下类型的层次结构类型：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 而`/y`
   * 层级为`[ c, a, <default>]`

这是因为`/y`具有`sling:resourceSuperType`属性，而`/x`没有，因此其超类型从其资源类型中获取。

#### 不能直接调用{#sling-scripts-cannot-be-called-directly} Sling脚本

在Sling中，无法直接调用脚本，因为这会破坏REST服务器的严格概念；您将混合使用资源和表示法。

如果您直接调用表示法（脚本），则会将资源隐藏在脚本中，这样框架(Sling)就不再知道该资源了。 因此，您会丢失某些功能：

* 自动处理除GET以外的http方法，包括：

   * POST、PUT、DELETE，通过sling默认实施进行处理
   * sling:resourceType位置中的`POST.jsp`脚本

* 您的代码架构不再像原来那样清晰，结构也不那么清晰；对大规模发展至关重要

### Sling API {#sling-api}

它使用Sling API包org.apache.sling。&amp;ast；和标记库。

### 使用sling:include {#referencing-existing-elements-using-sling-include}引用现有元素

最后需要考虑的是需要引用脚本中的现有元素。

更复杂的脚本（聚合脚本）可能需要访问多个资源（例如，导航、侧栏、页脚、列表的元素），并通过包含&#x200B;*resource*&#x200B;来执行此操作。

要实现此目的，您可以使用sling:include（&quot;/&lt;路径>/&lt;资源>&quot;）命令。 这将有效地包括引用资源的定义，如以下语句中所示，该语句引用了呈现图像的现有定义：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定义了用于开发和部署模块化应用程序和库的架构（又称为Dynamic Module System for Java）。 利用OSGi容器，可将应用程序划分为多个模块（是带有附加元信息的jar文件，在OSGi术语中称为包），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器内实施的服务
* 容器与应用程序之间的合同

这些服务和合同提供了一个架构，使各个元素能够动态地发现彼此以进行协作。

然后，OSGi框架可为您提供这些包的动态加载/卸载、配置和控制 — 无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问[OSGi网站](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此架构允许您使用应用程序特定模块扩展Sling。 Sling以及CQ5使用OSGi（开放服务网关计划）的[Apache Felix](https://felix.apache.org/)实施，并基于OSGi Service Platform 4版本4.2规范。 它们都是在OSGi框架中运行的OSGi包集合。

这样，您就可以对安装中的任意包执行以下操作：

* 安装
* 开始
* stop
* 更新
* 卸载
* 查看当前状态
* 访问有关特定包的更多详细信息（如符号名称、版本、位置等）

有关更多信息，请参阅[Web控制台](/help/sites-deploying/web-console.md)、[OSGi配置](/help/sites-deploying/configuring-osgi.md)和[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

## AEM环境中的开发对象{#development-objects-in-the-aem-environment}

以下是对发展感兴趣的方面：

**** 项目项目是节点或属性。

有关处理项目对象的详细信息，请参阅Interface javax.jcr.Item的[Javaocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html)

**节点（及其属性）** 节点及其属性在JCR API 2.0规范(JSR 283)中定义。它们存储内容、对象定义、渲染脚本和其他数据。

节点定义内容结构，其属性存储实际内容和元数据。

内容节点驱动渲染。 Sling从传入请求中获取内容节点。 此节点的属性sling:resourceType指向要使用的Sling呈现组件。

节点（即JCR名称）在Sling环境中也称为资源。

例如，要获取当前节点的属性，您可以在脚本中使用以下代码：

`PropertyIterator properties = currentNode.getProperties();`

将currentNode作为当前节点对象。

有关操作节点对象的详细信息，请参阅[Javaocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**** WidgetIn AEM中，所有用户输入均由小组件管理。它们通常用于控制内容段的编辑。

对话框通过组合小组件来构建。

AEM是使用ExtJS小组件库开发的。

**** 对话框对话框是一种特殊类型的小组件。

要编辑内容，AEM会使用应用程序开发人员定义的对话框。 这些组件可组合一系列小组件，用于向用户显示编辑相关内容所需的所有字段和操作。

对话框还用于编辑元数据以及各种管理工具。

**** 组件软件组件是提供预定义服务或事件并能够与其他组件进行通信的系统元素。

在AEM中，组件通常用于呈现资源的内容。 当资源是页面时，呈现该资源的组件称为顶级组件或页面组件。 但是，组件既无需渲染内容，也无需链接到特定资源；例如，导航组件将显示有关多个资源的信息。

组件的定义包括：、

* 用于呈现内容的代码
* 用于用户输入和结果内容配置的对话框。

**** 模板模板是特定类型页面的基础。在“网站”选项卡中创建页面时，用户必须选择模板。 然后，复制此模板以创建新页面。

模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。

它定义用于呈现页面和默认内容（主要顶级内容）的页面组件。 该内容定义了如何将其呈现为以内容为中心的AEM。

**页面组件（顶级组件）** 用于呈现页面的组件。

**** 页面A页面是模板的“实例”。

页面具有类型cq:Page的层次结构节点和类型cq:PageContent的内容节点。 内容节点的属性sling:resourceType指向用于渲染页面的页面组件。

例如，要获取当前页面的名称，您可以在脚本中使用以下代码：

S`tring pageName = currentPage.getName();`

将currentPage作为当前页面对象。 有关处理页面对象的详细信息，请参阅[Javaocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)。

**页面** 管理器页面管理器是一个界面，提供页面级别操作的方法。

例如，要获取资源的容器页面，您可以在脚本中使用以下代码：

页面myPage = pageManager.getContainingPage(myResource);

将pageManager作为页面管理器对象，将myResource作为资源对象。 有关页面管理器提供的方法的详细信息，请参阅[Javaocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 存储库{#structure-within-the-repository}内的结构

以下列表概述了您将在存储库中看到的结构。

>[!CAUTION]
>
>应谨慎更改此结构或其中的文件。
>
>开发时需要进行更改，但您应当确保完全了解所做的任何更改的含义。

>[!CAUTION]
>
>不得更改`/libs`路径中的任何内容。 对于配置和其他更改，请将项目从`/libs`复制到`/apps`，并在`/apps`中进行任何更改。

* `/apps`

   与申请相关；包括特定于您网站的组件定义。 您开发的组件可以基于`/libs/foundation/components`上提供的现成组件。

* `/content`

   为您的网站创建的内容。

* `/etc`

* `/home`

   用户和组信息。

* `/libs`

   属于AEM核心的库和定义。 `/libs`中的子文件夹表示开箱即用的AEM功能，例如搜索或复制。 不应修改`/libs`中的内容，因为它会影响AEM的工作方式。 特定于您网站的功能应在`/apps`下开发（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

* `/tmp`

   临时工作区。

* `/var`

   系统更改和更新的文件；例如审核日志、统计信息、事件处理。

## 环境 {#environments}

使用AEM，生产环境通常包含两种不同类型的实例：[创作实例和发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)。

## 调度程序{#the-dispatcher}

Dispatcher是Adobe用于缓存和/或负载平衡的工具。 有关更多信息，请参阅[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)下。

## FileVault（源修订版系统）{#filevault-source-revision-system}

FileVault为JCR存储库提供文件系统映射和版本控制。 它可用于管理AEM开发项目，并完全支持在标准版本控制系统（例如，Subversion）中存储和版本控制项目代码、内容、配置等。

有关详细信息，请参阅[FileVault工具](/help/sites-developing/ht-vlttool.md)文档。

## 工作流 {#workflows}

您的内容通常受组织流程的约束，包括由不同参与者批准和注销等步骤。 这些流程可以表示为在AEM](/help/sites-developing/workflows-models.md)中定义和开发的工作流[，然后根据需要应用于[相应的内容页面](/help/sites-administering/workflows.md)或[数字资产](/help/assets/assets-workflow.md)。

工作流引擎用于管理工作流的实施及其后续对内容的应用程序。

## 多站点管理{#multi-site-management}

多站点管理器(MSM)使您能够轻松管理共享公共内容的多个网站。 MSM允许您定义站点之间的关系，以便一个站点中的内容更改可以自动复制到其他站点中。

例如，网站通常以多种语言为国际受众提供。 如果使用同一语言的网站数量较少（三到五个），则可以通过手动流程来跨网站同步内容。 但是，一旦网站数量增加或涉及多种语言，自动化该过程就会变得更加高效。

* 有效管理网站的不同语言版本。
* 基于源网站自动更新一个或多个网站：

   * 强制实施通用的基本结构并跨多个站点使用通用内容。
   * 最大限度地利用可用资源。
   * 保持一种共同的外观。
   * 将精力集中在管理网站中不同的内容上。

有关更多信息，请参阅[多站点管理器](/help/sites-administering/msm.md)。
