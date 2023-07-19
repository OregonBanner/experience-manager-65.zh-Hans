---
title: AEM核心概念
seo-title: The Basics
description: 概述了AEM的结构以及如何在此基础上进行开发的核心概念，包括了解JCR、Sling、OSGi、Dispatcher、工作流和MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '3327'
ht-degree: 1%

---

# AEM核心概念 {#aem-core-concepts}

>[!NOTE]
>
>在深入了解AEM的核心概念之前，Adobe建议完成 [AEM Sites开发入门](/help/sites-developing/getting-started.md) 概述AEM开发过程和核心概念介绍的文档。

## 在AEM上进行开发的先决条件 {#prerequisites-for-developing-on-aem}

您需要具备以下技能才能在AEM之上进行开发：

* Web应用技术的基本知识，包括：

   * request -response (XMLHttpRequest / XMLHttpResponse)循环
   * HTML
   * CSS
   * JavaScript

* Experience Server (CRX)（包括Content Explorer）的工作知识
* 对于在经典UI中进行开发，还需要JSP (JavaServer Pages)的基本知识，包括理解和修改简单JSP示例的能力。

此外，建议您阅读并遵循 [准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md).

## Java™内容存储库 {#java-content-repository}

Java™内容存储库(JCR)标准、 [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)，指定了一种独立于供应商和实现的方法，用于在内容存储库中的粒度级别双向访问内容。

规范牵头机构为Adobe研究（瑞士） AG。

此 [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包javax.jcr。&amp;ast；用于直接访问和处理存储库内容。

## Experience Server (CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供了AEM所基于的Experience Services（可用于构建自定义应用程序），并嵌入了基于Jackrabbit的内容存储库。

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) 是一个完全符合要求的开源JCR API 2.0实施。

## Sling请求处理 {#sling-request-processing}

### Sling简介 {#introduction-to-sling}

AEM构建方式 [Sling](https://sling.apache.org/index.html)，这是一个基于REST原则的Web应用程序框架，它提供了易于开发的面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit）或CRX内容存储库(在AEM中)作为其数据存储。 Sling已对Apache Software Foundation做出了贡献 — 有关更多信息，请参阅Apache 。

使用Sling时，要呈现的内容类型不是第一个处理注意事项。 相反，主要考虑的问题是URL是否解析为内容对象，然后可以找到脚本来执行渲染。 这为Web内容作者提供了极好的支持，让他们能够构建可轻松根据自己的需求进行自定义的页面。

在包含各种不同内容元素的应用中，或者在您需要易于自定义的页面时，此灵活性的优势显而易见。 特别是在AEM解决方案中实施Web内容管理系统（如WCM）时。

参见 [在15分钟内发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 使用Sling进行开发的第一步。

下图说明了Sling脚本的解决方案：它显示了如何从HTTP请求获取到内容节点、从内容节点获取到资源类型、从资源类型获取到脚本，以及提供了哪些脚本变量。

![了解Apache Sling脚本解析](assets/sling-cheatsheet-01.png)

下图说明了可在处理SlingPostServlet时使用的所有隐藏但功能强大的请求参数，所有POST请求的默认处理程序为您提供了用于在存储库中创建、修改、删除、复制和移动节点的无限选项。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling是 *以内容为中心*. 这意味着处理侧重于内容，因为每个(HTTP)请求都映射到JCR资源（存储库节点）形式的内容：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示法（或脚本）从与请求的某些部分（例如，选择器和/或扩展）组合的资源属性中定位

### RESTful Sling {#restful-sling}

由于以内容为中心的理念，Sling实施了面向REST的服务器，从而在Web应用程序框架中引入了新概念。 其优点是：

* 非常RESTful，而不仅仅是在曲面上；资源和表示在服务器内正确建模
* 删除一个或多个数据模型

   * 以前需要用到的URL结构、业务对象、数据库模式；
   * 现在简化为： URL =资源= JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这会定义相应的脚本要显示的内容。 为此，将从URL中提取信息。

如果我们分析以下URL：

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以将其划分为复合部分：

| 协议 | 主机 | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/监视 | .printable.a4. | html | / | a/b | ? | x=12 |

**协议** HTTP

**主机** 网站的名称。

**内容路径** 指定要渲染的内容的路径。 与扩展结合使用；在此示例中，它们将转换为tools/spy.html。

**选择器** 用于呈现内容的替代方法；在本例中为A4格式的打印机友好版本。

**扩展** 内容格式；还指定用于渲染的脚本。

**后缀** 可用于指定其他信息。

**参数** 动态内容所需的任何参数。

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用以下原则：

* 映射使用从请求中提取的内容路径来定位资源
* 在找到相应的资源时，将提取sling资源类型，并用于定位要用于呈现内容的脚本

下图说明了所使用的机制，将在以下各节中更详细地讨论。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪个脚本渲染特定实体(通过设置 `sling:resourceType` 属性)。 此机制提供的自由度比脚本访问数据实体的自由度更大（正如PHP脚本中的SQL语句所做的那样），因为资源可以具有多个演绎版。

#### 将请求映射到资源 {#mapping-requests-to-resources}

将细分请求并提取必要信息。 在存储库中搜索请求的资源（内容节点）：

* 第一个Sling检查节点是否存在于请求中指定的位置；例如， `../content/corporate/jobs/developer.html`
* 如果未找到节点，则将丢弃扩展并重复搜索；例如， `../content/corporate/jobs/developer`
* 如果未找到节点，则Sling将返回http代码404（未找到）。

Sling还允许将JCR节点以外的内容作为资源，但这是一项高级功能。

### 定位脚本 {#locating-the-script}

找到相应的资源（内容节点）后， **sling资源类型** 被提取。 这是一个路径，用于定位要用于呈现内容的脚本。

指定的路径 `sling:resourceType` 可以是：

* 绝对
* 相对，相对于配置参数

  由于相对路径提高了可移植性，因此Adobe会推荐相对路径。

所有Sling脚本都存储在以下任一文件夹的子文件夹中： `/apps` 或 `/libs`，将按此顺序搜索(请参阅 [自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

其他几点需要注意的是：

* 当需要方法(GET、POST)时，将根据HTTP规范(例如jobs.job.esp.POST)以大写形式指定（见下文）
* 支持各种脚本引擎：

   * HTL(HTML模板语言 — Adobe Experience Manager首选和推荐的用于HTML的服务器端模板系统)： `.html`
   * ECMAScript (JavaScript)页面（服务器端执行）： `.esp, .ecma`
   * Java™ Server Pages（服务器端执行）： `.jsp`
   * Java™ Servlet编译器（服务器端执行）： `.java`
   * JavaScript模板（客户端执行）： `.jst`

Felix管理控制台上列出了给定的AEM实例支持的脚本引擎列表( `http://<host>:<port>/system/console/slingscripting`)。

此外，Apache Sling还支持与其他常用脚本引擎（例如Groovy、JRuby、Freemarker）集成，并提供了一种集成新脚本引擎的方法。

使用上面的示例，如果 `sling:resourceType` 是 `hr/jobs` 然后用于：

* 以.html结尾的GET/HEAD请求和URL（默认请求类型、默认格式）

  脚本是/apps/hr/jobs/jobs.esp ；文件名由sling：resourceType的最后一个部分构成。

* POST请求(除GET/HEAD之外的所有请求类型，方法名称必须大写)

  POST在脚本名称中使用。

  脚本为 `/apps/hr/jobs/jobs.POST.esp`.

* 其他格式的URL，不以.html结尾

  例如，`../content/corporate/jobs/developer.pdf`

  脚本将为 `/apps/hr/jobs/jobs.pdf.esp`；后缀将添加到脚本名称中。

* 带有选择器的URL

  选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、rss馈送或摘要。

  如果查看适合打印的版本，则选择器可能是 *打印*；如所示 `../content/corporate/jobs/developer.print.html`

  脚本将为 `/apps/hr/jobs/jobs.print.esp`；选择器将添加到脚本名称中。

* 如果未定义sling：resourceType ，则：

   * 内容路径将用于搜索适当的脚本（如果基于路径的ResourceTypeProvider处于活动状态）。

     例如，的脚本 `../content/corporate/jobs/developer.html` 会在以下位置生成搜索： `/apps/content/corporate/jobs/`.

   * 将使用主节点类型。

* 如果根本找不到脚本，则将使用默认脚本。

  当前支持以纯文本(.txt)、HTML(.html)和JSON (.json)格式呈现默认演绎版，所有这些演绎版都将列出节点的属性（格式合适）。 扩展名.res或不带请求扩展名的请求的默认演绎版是假脱机资源（如果可能）。
* 对于http错误处理（代码403或404），Sling将在以下任一位置查找脚本：

   * /apps/sling/servlet/errorhandler的位置 [自定义脚本](/help/sites-developing/customizing-errorhandler-pages.md)
   * 或标准脚本/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果给定请求应用了多个脚本，则会选择具有最佳匹配的脚本。 匹配项越具体，其效果就越好；换句话说，选择器越多，匹配效果就越好，无论请求扩展名或方法名是否匹配。

例如，考虑访问资源的请求
`/content/corporate/jobs/developer.print.a4.html`
类型
`sling:resourceType="hr/jobs"`

假设我们在正确的位置包含以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

那么优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型(主要由 `sling:resourceType` 属性)还有资源超类型。 这通常由 `sling:resourceSuperType` 属性。 在尝试查找脚本时，也会考虑这些超类型。 资源超级类型的优点在于，它们可以形成资源的层次结构，其中默认资源类型 `sling/servlet/default` （由默认servlet使用）实际上是根。

可以通过两种方式定义资源的资源超级类型：

* 按 `sling:resourceSuperType` 资源的属性。
* 按 `sling:resourceSuperType` 节点属性，该节点的 `sling:resourceType` 点数。

例如：

* /

   * a
   * b

      * sling：resourceSuperType = a

   * c

      * sling：resourceSuperType = b

   * x

      * sling：resourceType = c

   * y

      * sling：resourceType = c
      * sling：resourceSuperType = a

类型层次结构：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 而为 `/y`
   * 层次结构为 `[ c, a, <default>]`

这是因为 `/y` 具有 `sling:resourceSuperType` 属性，而 `/x` 不会，因此其超类型取自其资源类型。

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，不能直接调用脚本，因为这会破坏REST服务器的严格概念；您可以混合使用资源和表示法。

如果直接调用表示形式（脚本），则会在脚本中隐藏资源，因此框架(Sling)不再知道该表示形式。 因此，您将丢失某些特征：

* 自动处理GET以外的http方法，包括：

   * 通过sling默认实现处理的POST、PUT、DELETE
   * 此 `POST.jsp` sling：resourceType位置中的脚本

* 您的代码架构不再像以前那样干净和结构清晰；这对于大规模开发至关重要

### Sling API {#sling-api}

这会使用Sling API包org.apache.sling。&amp;ast；和标记库。

### 使用sling：include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要考虑的是在脚本中引用现有元素的需要。

更复杂的脚本（聚合脚本）可能需要访问多个资源（例如导航、侧栏、页脚、列表元素），为此，需要包含 *资源*.

为此，您可以使用sling：include(&quot;/&lt;path>/&lt;resource>“)命令。 这将有效地包括引用的资源的定义，如下面的语句所示，该语句引用了用于渲染图像的现有定义：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定义了用于开发和部署模块化应用程序和库（也称为Dynamic Module System for Java）的体系结构。 OSGi容器允许您将应用程序分成单独的模块（包含其他元信息的jar文件，在OSGi术语中称为捆绑包），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器中实现的服务
* 容器与您的应用程序之间的合同

这些服务和合同提供了一个体系结构，使各个元素能够动态地发现彼此进行协作。

随后，OSGi框架将为您提供这些捆绑包的动态加载/卸载、配置和控制，而无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问 [OSGi网站](https://www.osgi.org).
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此架构允许您使用特定于应用程序的模块扩展Sling。 Sling和CQ5使用 [Apache Felix](https://felix.apache.org/documentation/index.html) OSGI（开放服务网关计划）的实施基于OSGi服务平台4.2版规范。 它们都是在OSGi框架内运行的OSGi捆绑包的集合。

这样，您就可以对安装中的任何软件包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看当前状态
* 访问有关特定捆绑包的更多详细信息（例如，符号名称、版本、位置等）

参见 [Web控制台](/help/sites-deploying/web-console.md)， [OSGI配置](/help/sites-deploying/configuring-osgi.md) 和 [OSGi配置](/help/sites-deploying/osgi-configuration-settings.md) 了解更多信息。

## AEM环境中的开发对象 {#development-objects-in-the-aem-environment}

以下内容对开发很有帮助：

**项目** 项是节点或属性。

有关处理Item对象的详细信息，请参阅 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) 接口javax.jcr.Item的

**节点（及其属性）** 节点及其属性在JCR API 2.0规范(JSR 283)中定义。 它们存储内容、对象定义、渲染脚本和其他数据。

节点定义内容结构，其属性存储实际内容和元数据。

内容节点驱动渲染。 Sling从传入请求获取内容节点。 此节点的属性sling：resourceType指向要使用的Sling渲染组件。

在Sling环境中，节点（一个JCR名称）也称为资源。

例如，要获取当前节点的属性，您可以在脚本中使用以下代码：

`PropertyIterator properties = currentNode.getProperties();`

当前节点对象为currentNode。

有关处理Node对象的更多信息，请参阅 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**构件** 在AEM中，所有用户输入都由小组件管理。 这些通常用于控制一段内容的编辑。

对话框通过组合构件来构建。

AEM是使用ExtJS小组件库开发的。

**对话框** 对话框是一种特殊类型的构件。

要编辑内容，AEM使用应用程序开发人员定义的对话框。 这些组件组合了一系列构件，向用户展示编辑相关内容所需的所有字段和操作。

对话框也用于编辑元数据和各种管理工具。

**组件** 软件组件是一种系统元素，提供预定义的服务或事件，并能够与其他组件通信。

在AEM中，组件通常用于呈现资源的内容。 当资源是页面时，呈现它的组件称为顶级组件或页面组件。 但是，组件不必呈现内容，也不必链接到特定资源；例如，导航组件将显示有关多个资源的信息。

组件的定义包括：

* 用于呈现内容的代码
* 用于用户输入和配置结果内容的对话框。

**模板** 模板是特定类型页面的基础。 在“网站”选项卡中创建页面时，用户必须选择模板。 然后，通过复制此模板创建新页面。

模板是一种节点层次结构，其结构与要创建页面的结构相同，但没有任何实际内容。

它定义用于呈现页面的页面组件和默认内容（主要顶级内容）。 内容定义其呈现方式，因为AEM以内容为中心。

**页面组件（顶级组件）** 用于呈现页面的组件。

**页面** 页面是模板的“实例”。

页面具有cq：Page类型的层次结构节点和cq：PageContent类型的内容节点。 内容节点的属性sling：resourceType指向用于呈现页面的页面组件。

例如，要获取当前页面的名称，您可以在脚本中使用以下代码：

S`tring pageName = currentPage.getName();`

当前页面对象为currentPage。 有关处理Page对象的更多信息，请参阅 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**页面管理器** 页面管理器是一个提供页面级别操作方法的界面。

例如，要获取资源的包含页面，您可以在脚本中使用以下代码：

页面myPage = pageManager.getContainingPage(myResource)；

将pageManager作为页面管理器对象，将myResource作为资源对象。 有关页面管理器所提供方法的详细信息，请参阅 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## 存储库中的结构 {#structure-within-the-repository}

以下列表概述了您在存储库中看到的结构。

>[!CAUTION]
>
>对此结构或其中的文件所做的更改应谨慎进行。
>
>虽然在开发过程中需要进行更改，但是您应该注意要完全了解所做任何更改的影响。

>[!CAUTION]
>
>不更改中的任何内容 `/libs` 路径。 对于配置和其他更改，从复制项目 `/libs` 到 `/apps` 并在中进行任何更改 `/apps`.

* `/apps`

  与应用程序相关；包括特定于您网站的组件定义。 您开发的组件可以基于以下位置提供的现成组件 `/libs/foundation/components`.

* `/content`

  为您的网站创建的内容。

* `/etc`

* `/home`

  用户和组信息。

* `/libs`

  属于AEM核心的库和定义。 中的子文件夹 `/libs` 表示现成的AEM功能，例如搜索或复制。 中的内容 `/libs` 不应修改，因为它会影响AEM的工作方式。 您网站的特定功能应开发于 `/apps` (请参阅 [自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

* `/tmp`

  临时工作区。

* `/var`

  系统更改和更新的文件；例如审核日志、统计数据、事件处理。

## 环境 {#environments}

使用AEM时，生产环境通常包含两种不同类型的实例： [创作实例和发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs).

## 调度程序 {#the-dispatcher}

Dispatcher是Adobe用于缓存和/或负载平衡的工具。 欲知更多信息，请访问 [调度程序](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans).

## FileVault（源修订版系统） {#filevault-source-revision-system}

FileVault为JCR存储库提供文件系统映射和版本控制。 它可用于管理AEM开发项目，完全支持在标准版本控制系统（例如，Subversion）中存储和版本控制项目代码、内容、配置等。

请参阅 [FileVault工具](/help/sites-developing/ht-vlttool.md) 文档，以了解详细信息。

## 工作流 {#workflows}

您的内容通常受组织流程约束，包括各个参与者的批准和签署等步骤。 这些进程可以表示为工作流， [在AEM中定义和开发](/help/sites-developing/workflows-models.md)，然后应用于 [相应的内容页面](/help/sites-administering/workflows.md) 或 [数字资产](/help/assets/assets-workflow.md) 根据需要。

工作流引擎用于管理工作流的实施，以及工作流对内容的后续应用。

## 多站点管理 {#multi-site-management}

多站点管理器(MSM)使您能够轻松管理共享通用内容的多个网站。 MSM允许您定义站点之间的关系，以便将一个站点中的内容更改自动复制到其他站点。

例如，通常以多种语言为国际受众提供网站。 当使用同一语言的网站数量很少（三到五个）时，可以执行手动流程来同步网站中的内容。 但是，当网站数量增加或涉及多种语言时，自动化该过程会变得更加高效。

* 高效地管理网站的不同语言版本。
* 根据源站点自动更新一个或多个站点：

   * 强制实施通用基本结构并在多个站点中使用通用内容。
   * 最大限度地利用可用资源。
   * 保持统一的外观。
   * 将精力集中在管理不同站点之间的内容上。

有关更多信息，请参阅 [多站点管理器](/help/sites-administering/msm.md).
