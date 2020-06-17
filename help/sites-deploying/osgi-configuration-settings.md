---
title: OSGi配置设置
seo-title: OSGi配置设置
description: 本文详细介绍了与项目实施相关的OSGi配置设置（根据捆绑包列出）。 该列表充当指南，并非详尽无遗。
seo-description: 本文详细介绍了与项目实施相关的OSGi配置设置（根据捆绑包列出）。 该列表充当指南，并非详尽无遗。
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '3805'
ht-degree: 0%

---


# OSGi配置设置{#osgi-configuration-settings}

[OSGi是](https://www.osgi.org/) AEM技术堆栈中的一个基本元素。 它用于控制AEM的复合捆绑包及其配置。

OSGi&quot;提&#x200B;*供了标准化的基元，它允许应用程序由小的、可重用的和协作的组件构建。 这些组件可以组成一个应用程序并进行部署*”。

这样，可以轻松管理捆绑套件，因为可以单独停止、安装和启动捆绑套件。 互依关系将自动处理。 每个OSGi组件(请参 [阅OSGi规范](https://www.osgi.org/Specifications/HomePage))都包含在各种包中的一个中。 When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

以下OSGi配置设置（根据捆绑包列出）与项目实施相关。 并非列出的所有设置都需要调整，其中有些设置可以帮助您了解AEM的操作方式。

>[!CAUTION]
>
>该列表旨在作为准则，并非详尽无遗。 并不列出所有捆绑包，也不列出某些捆绑包的所有参数。
>
>所需的配置因项目而异。
>
>请参阅Web控制台，了解所用值和有关参数的详细信息。

>[!NOTE]
>
>OSGi配置差异工具是AEM工具的一 [部分](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)，可用于列表默认OSGi配置。

>[!NOTE]
>
>AEM中的特定功能区域可能需要其他捆绑套件。 在这些情况下，可在与相应功能相关的页面上找到配置详细信息。

**AEM复制事件监听器** 配置：

* 运 **行模式**，其中复制事件将分发到监听器。 例如，如果定义为作者，则此系统将“启动”复制。

* 如果项目代 **码在** 发布环境中处理复制事件（反向复制），则需要添加运行模式发布。 例如，当调度程序用于从发布环境刷新时，或者当标准复制到其他发布实例时。

**AEM Repository更改监听程序** Configure:

* 路 **径**，用于侦听准备分发的存储库事件的位置。

**CRX Sling客户端存储库** -配置对基础内容存储库的访问。

* 安 **装后** ，应更改管理员密码，以确 [保实](/help/sites-administering/security-checklist.md) 例的安全。
* 其他更改不必进行，必须小心，因为它们可能会影响对存储库的访问。

**Wiki邮件服务** 为Wiki发送的电子邮件配置电子邮件设置。

**Apache Felix OSGi管理控制台** 配置：

* **插件**,Apache Felix Web管理控制台中要作为顶级菜单项 **提供的主导航项目** （控制台插件）。 禁用您不需要的任何内容，因为每个内容都需要空间和资源。

>[!CAUTION]
>
>请务必配置以下各项：
>
>**用户名** 和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。
>初始安装后必须更改密码，以确保实 [例的](/help/sites-administering/security-checklist.md) 安全性。

>[!NOTE]
>
>此配置应在启动时根据需要使用Felix Console进行，然后再使用存储库。

**Apache Sling可自定义请求数据记录器** 配置：

* **记录器名** 和 **日志格式** ，用于配置请求和访问日志的位置和格式(默认值： `request.log`)。 在分析与Web链相关的性能或调试功能时，此日志文件是必不可少的。
这与Apache Sling Request [Logger成对](#apacheslingrequestlogger)。

有关详细信息，请 [参阅AEM日志](/help/sites-deploying/configure-logging.md) 和 [Sling日志](https://sling.apache.org/site/logging.html)。

**Apache Sling事件线程池配置** :

* **最小池大小** 和 **最大池大小**，用于保存事件线程的池的大小。

* **队列大小**，当池已用尽时线程队列的最大大小。
建议的值为 `-1` 此设置队列为“无限制”; 如果设置了限制，则超出限制时可能会发生损失。

* 更改这些设置有助于在事件数较多的情况下实现性能； 例如，大量使用AEM DAM或工作流。
* 应使用测试建立特定于您方案的值。
* 这些设置会影响实例的性能，因此，不要无故更改它们，并且要充分考虑。

**Apache Sling GET Servlet** 配置渲染的某些方面：

* **自动索引** ，启用／禁用用于浏览的目录渲染。
* **启用** （或禁用）默认再现 **，如** HTML、 **纯文本、** JSON **或******XML。
您不应禁用JSON。

>[!NOTE]
>
>如果您在生产就绪模式下运行AEM，将自动为生产实 [例配置此设置](/help/sites-administering/production-ready.md)。

**Apache Sling Java脚本处理程序** -配置将。java文件编译为脚本(servlet)的设置。

某些设置可能会影响性能，应尽可能禁用这些设置，尤其是对于生产实例。

* 源&#x200B;**VM****和TargetVM**，将JDK版本定义为运行时JVM

* 对于生产实例：

   * 禁用 **生成调试信息**

**Apache Sling JCR Installer** 这些参数可能不需要配置，但在开发或调试时可能很有用。 例如，安装文件夹可用于签入／签出或创建包。

* **安装文件夹名称** regexp和 **安装文件夹的最大层次结构深度** -指定在何处和到哪个深度搜索存储库文件夹以查找要安装的资源。 当使用通配符时（如中所示）。*/install)将搜索所有相应匹配项，例如 `/libs/sling/install` 和 `/libs/cq/core/install`。

* **搜索路径**、jcrinstall搜索要安装的资源的路径列表，以及一个表示该路径的权重因子的数字。

**Apache Sling作业事件处理程序** 配置管理作业调度的参数：

* **重试间隔****、**&#x200B;最大重试、 **最大并行作业**、 **确认等待时间**，等等。

* 更改这些设置可以在大量作业的情况下提高性能； 例如，大量使用AEM DAM和工作流。
* 应使用测试建立特定于您方案的值。
* 请勿随意更改这些设置，只有在适当考虑后更改。

**Apache Sling JSP脚本处理程序** 为JSP脚本处理程序配置性能相关设置。 要提高性能，您应尽可能禁用。

特别是对于生产实例：

* 禁用 **生成调试信息**
* 禁用 **保留生成的Java**
* 禁用映 **射的内容**
* 禁用 **显示源片段**

>[!NOTE]
>
>如果您在生产就绪模式下运行AEM，将自动为生产实 [例配置此设置](/help/sites-administering/production-ready.md)。

**Apache Sling日志记录配置** :

* **日志级** 别 **和日志文件**，用于定义中央日志配置的位置和日志级别(error.log)。 该级别可以设置为、 `DEBUG`、 `INFO`、 `WARN`和 `ERROR` 之一 `FATAL`。

* **用于定义日志文** 件大小和版本旋 **转的日志文件数** 和日志文件阈值。

* **消息模式** 定义日志消息的格式。

有关详细信息，请 [参阅AEM日志](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling日志](https://sling.apache.org/site/logging.html)。

**Apache Sling日志记录器配置（工厂配置）** 配置：

* **日志级**、 **日志文件和** 消息格式 **** ，用于定义日志文件和消息的详细信息。

* **Logger** to define the类别; 例如，仅com.day.cq的日志。

* 通过使 **用工厂配置**，可以添加任意数量的附加配置以满足所需的各种日志级别和类别。
* 这种配置在开发过程中很有帮助； 例如，在特定日志文件中记录特定服务的TRACE消息。
* 此类配置在生产环境中很有用； 例如，将有关特定服务的消息记录到单个日志文件中，以便更轻松地进行监视。

有关详细信息，请 [参阅AEM日志](/help/sites-deploying/configure-logging.md) 和 [Sling日志](https://sling.apache.org/site/logging.html)。

**Apache Sling日志记录编写器配置(工厂配置** )配置：

* **日志文件** ，用于定义日志文件的存在性。
* **定义版本旋转** 的日志文件数。

* 编写器可以由Apache Sling记 **录程序配置使用** 。

* 这种配置在开发过程中很有帮助； 例如，在特定日志文件中记录特定服务的TRACE消息。
* 此类配置在生产环境中很有用； 例如，将有关特定服务的消息记录到单个日志文件中，以便更轻松地进行监视。

有关详细信息，请 [参阅AEM日志](/help/sites-deploying/configure-logging.md) 和 [Sling日志](https://sling.apache.org/site/logging.html)。

**Apache Sling主Servlet配置** :

* **每个请求的调用数** 和 **递归深度** ，可保护系统免受无限递归和过多脚本调用的影响。

**Apache Sling MIME类型服务** Configure:

* **MIME类型** ，将项目所需的类型添加到系统。 这允许对文 `GET` 件进行请求，以设置用于链接文件类型和应用程序的正确内容类型标题。

**Apache Sling推荐人过滤器** -要解决CRX WebDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，您需要配置推荐人过滤器。

推荐人过滤器服务是一种OSGi服务，允许您配置：

* 应过滤哪些http方法
* 是否允许空推荐人头
* 以及允许除服务器主机外的列表服务器。

有关更 [多详细信息，请参阅安全核对清单——跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 。

>[!NOTE]
>
>Apache Sling推荐人过滤器取决于快速修复包的安装。

**Apache Sling Request Logger** Configure:

* 定义请求记录方式的各种参数。
* **启用请求日志**，以启用或禁用。

* **启用访问日志**，以启用或禁用。

这与Apache Sling可自 [定义请求数据记录器配对](#apacheslingcustomizablerequestdatalogger)。

有关详细信息，请 [参阅AEM日志](/help/sites-deploying/configure-logging.md) 和 [Sling日志](https://sling.apache.org/site/logging.html)。

**Apache Sling Resource Resolver Factory配置Sling** Resource Resolution的核心方面：

* **资源搜索路**&#x200B;径，添加任何项目特定路径(但不删除或 `/libs` 删除 `/apps`)。

* **用于定义虚** URL映射的虚拟URL。

* **用于定义** 任何别名的URL映射； 例如，从 `/content` 到 `/`。

* **映射位置**，中外部的映射器配置 `/etc/map`。

* 使用本地安装（例如，使用） `https://localhost:4502/system/console/jcrresolver`确定哪个资源解析程序处于活动状态。

有关详细信息，请参阅： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>特别是，这些选项必须在存储库中配置。
>
>否则，在下次 **启动时** ,AEM可能会覆盖使用Felix控制台对URL映射所做的更改。

**Apache Sling Servlet/Script Resolver和错误处理程序** Sling Servlet和脚本解析程序具有多个任务:

1. 它用作选择 `ServletResolver` 要调用的Servlet或脚本来处理请求。

1. 它充当 `SlingScriptResolver`。

1. 它通过使用与用于解析请求处 `ErrorHandler` 理servlet和脚本相同的算法来实现接口来管理错误处理，以选择处理servlet和脚本的错误。

可以设置各种参数，包括：

* **执行路径** 列表搜索可执行脚本的路径； 通过配置特定路径，您可以限制可以执行的脚本。 如果未配置路径，则使用默认路径( `/` = root)，这允许执行所有脚本。
如果配置的路径值以斜杠结尾，则搜索整个子树。 如果没有这样的尾随斜杠，则只有在脚本完全匹配时，才会执行脚本。

* **脚本用户** -此可选属性可指定用于读取脚本的存储库用户帐户。 如果未指定帐户，则 `admin` 默认使用用户。

* **默认扩展** 将使用默认行为的扩展的列表。 这意味着资源类型的最后一个路径段可用作脚本名称。

**Day Commons GFX Font Helper** 在渲染图形时，可以使用DrawText嵌入文本。 对于此，您还可以安装您自己的字体：

* 定义要 **搜索的字体** ，以查找项目特定字体。
For example, `/apps/myapp/fonts`.

**Apache HTTP Components代理配置** Apache HTTP客户端用于所有代码的代理配置（创建HTTP时使用）; 例如，在复制时。

创建新配置时，请勿更改工厂配置，而应使用此处提供的配置管理器为此组件创建新工厂配置： **https://localhost:4502/system/console/configMgr/**。 代理配置在org.apache. **http.proxyconfigurator中可用。**

>[!NOTE]
>
>在AEM 6.0及早期版本中，代理已在Day Commons HTTP Client中配置。 自AEM 6.1和更高版本发布起，代理配置已移至“Apache HTTP Components Proxy Configuration”（Apache HTTP Components代理配置），而非“Day Commons HTTP Client”(Day Commons HTTP Client)配置。

**Day CQ Antispam** 配置使用的防垃圾邮件服务(Akismet)。 这要求您注册：

* **提供程序**
* **API密钥**
* **注册URL**

**Adobe Granite HTML Library Manager** Configure this to controll thandling client libraries（css或js）; 例如，包括如何看到底层结构。

* 对于生产实例：

   * 启用 **Minify** （删除CRLF和空格字符）。
   * 启 **用Gzip** （允许通过一个请求对文件进行Gzip压缩和访问）。
   * 禁用调 **试**
   * 禁用计 **时**

* 对于JS开发（尤其是当防火墙调试／调试时）:

   * 禁用微 **型**
   * 启 **用调试** ，将文件分开进行调试并与firebug一起使用。
   * 在 **对时** 间感兴趣的情况下启用时间。
   * 启用 **调试** 控制台可查看JS控制台日志消息。

>[!CAUTION]
>
>更改Minify或 **Gzip的****设置时** ，您还需要删除的 `/var/clientlibs`内容。 这是clientlibs的缓存版本，将在下次请求时重新构建。

>[!NOTE]
>
>如果您在生产就绪模式下运行AEM，将自动为生产实 [例配置此设置](/help/sites-administering/production-ready.md)。

**Day CQ HTTP Header Authentication Handler** HTTP请求的基本身份验证方法的系统宽设置。

使用关闭 [的用户组](/help/sites-administering/cug.md) ，您可以配置（以及其他）:

* **HTTP领域**
* 默 **认登录页**

**Day CQ Link Checker Service Check** and if necured configure:

* **调度程序期** ：定义自动检查外部链接的间隔。

* 检 **查失败的外部链** 接在其后被视为错误的期间的“错误链接容差间隔”。
* **链接检查覆盖模式**，以定义要从链接检查中排除的任何路径。

**Day CQ Link Checker任务** 为单个链接检查器任务配置设置(检查外部链接的任务):

* 检查在“Good Link Test Interval(良好链 **接测试间隔)”和“Bad Link** Test Interval(不良链 **接测试间隔)”中定义的间隔**

* 检查链接时外部访问所需的与Internet访问代理和NTLM相关的各种参数。

**Day CQ Mail Service** 为邮件服务器配置主机名和访问详细信息。 请参阅配置邮件服务部分。

**第CQ天MCM新闻稿** 配置与Newsletter一起使用的各种设置。

**Day CQ Root Mapping** Configure:

* **Target路径** ，用于定义“ ”的 `/`请求将重定向到的位置。

AEM中有两个可用的UI:

* 触屏优化UI是标准UI
* 而弃用的经典UI仍完全可操作

使用AEM根映射，您可以配置要作为实例默认值的UI:

* 要使触屏优化UI成为默认UI, **Target路** 径应指向：

   ```
      /projects.html
   ```

* 要使经典UI作为默认UI, **Target路** 径应指向：

   ```
      /welcome.html
   ```

>[!NOTE]
>
>在标准安装后，触屏优化UI是默认UI。

**Adobe Granite SSO身份验证处理程序** ，配置单点登录(SSO)详细信息； 在企业创作设置中，通常需要与LDAP结合使用。

有各种配置属性可用：

* **路径**&#x200B;此身份验证处理程序处于活动状态的路径。 如果此参数留空，则禁用身份验证处理程序。 例如，路径／会使身份验证处理程序用于整个存储库。

* **服务排**&#x200B;名OSGi框架服务排名值用于指示调用此服务所使用的顺序。 这是 
`int` 值，其中值越高，则指定的优先级越高。
默认值为 `0`.

* **标题**&#x200B;名称可能包含用户ID的标题的名称。

* **Cookie名**&#x200B;称可能包含用户ID的Cookie的名称。

* **参数名**&#x200B;可能提供用户ID的请求参数的名称。

* **用户映**&#x200B;射对于选定用户，从HTTP请求提取的用户名可以替换为凭据对象中的其他用户名。 此处定义映射。 如果用户名 
`admin` 显示在映射的任一侧，将忽略映射。 请注意，字符“=”必须用前导“\”进行转义。

* **格式**&#x200B;指示提供用户ID的格式。 用法:

   * `Basic` 用户ID是否以HTTP基本身份验证格式进行编码
   * `AsIs` 如果用户ID以纯文本形式提供，或者应按原样使用任何常规表达式应用值或任何常规表达式

**Day CQ WCM调试过滤器** ：在开发时，此功能很有用，因为它允许在访问页面时使用后缀，如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout将提供开发人员可能感兴趣的布局信息。

* 在生产实例上禁用此功能可确保性能和安全性。

**Day CQ WCM过滤器配置** :

* **WCM模式**以定义默认模式。
* 在创作实例中，此 `edit`可能 `disable,preview` 为或 `analytics`。
其他模式可从Sidekick访问，或者后缀 `?wcmmode=disabled` 可用于模拟生产环境。

* 在发布实例上，必须将其设置为 `disabled` 确保不能访问其他模式。

>[!NOTE]
>
>如果您在生产就绪模式下运行AEM，将自动为生产实 [例配置此设置](/help/sites-administering/production-ready.md)。

**Day CQ WCM链接检查器配置器** 配置：

* **列表重写配置** ，以指定基于内容的链接检查器配置的列表位置。 配置可以基于运行模式； 这对于区分创作和发布环境很重要，因为linkchecker设置可能不同。

**Day CQ WCM页面处理器配置** :

* **路径**，系统在触发之前监听页面修改的列表 `jcr:Event`。

**Adobe页面展示数跟踪器** ，对于创作实例，请配置：

* **sling.auth.requirements**: 将此属性的值设置为 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此配置将允许对跟踪服务进行匿名请求。

>[!NOTE]
>
>有关更 [多信息](/help/sites-deploying/configuring.md#enabling-page-impressions) ，请参阅页面展示。

**Day CQ WCM页面统计信息** 发布实例的配置：

* **发送数据的URL** ，以配置用于跟踪页面统计信息的URL（如果跟踪器请求通过调度程序，该URL至关重要）; 例如，默认值为 `https://localhost:4502/libs/wcm/stats/tracker`。

* **启用跟踪脚本** ，以启 `true`用()或禁用( `false`)在页面上包含跟踪脚本。 默认值为 `false`.

>[!NOTE]
>
>有关更 [多信息](/help/sites-deploying/configuring.md#enabling-page-impressions) ，请参阅页面展示。

**Day CQ WCM Version Manager** Control if and how, versions manager manager manager in your system:

* **在激活时创建版本**，在标准安装中启用
* **启用清除**

* **清除路径**，搜索操作将搜索的路径
* **隐式版本控制路径**，即隐式版本控制处于活动状态的路径。

* **最大版本**，版本的最大年龄（以天为单位）

* **最大版本数**，要保留的最大版本数

请参 [阅版本清](/help/sites-deploying/version-purging.md) 除以了解详细信息。

**Day CQ Workflow电子邮件通知服务** 为工作流发送的通知配置电子邮件设置。

**Day CQSE HTTP Service控制** CQ Servlet引擎：

* **NIO for HTTP,**是否将NIO用于HTTP。 默认设置为 true。仅在启用HTTP时使用。
* **连接超时，**连接超时（以毫秒为单位）。 此属性同时适用于HTTP和HTTPS连接。 默认为60秒。

* **启用HTTPS** ，无论是否启用HTTPS。 默认为false。
* **会话超时**，以分钟为单位指定的HTTP会话的默认生命周期。 如果超时为0或更少，则会话永远不会超时。 默认为10分钟。
* **调试日志**，是否写入DEBUG级别消息。 默认为false。
* **请求缓冲区大小**，请求的缓冲区大小（以字节为单位）。 默认值为8KB。
* **最大线程数**，用于处理请求的线程数。 默认值为200。

以下属性仅在启用HTTPS时适用。

* **HTTPS端口**，监听HTTPS请求的端口。 默认为 433.
* **NIO for HTTPS**，是否将NIO用于HTTP。 默认为NIO的HTTP属性值。
* **密钥**&#x200B;库，用于HTTPS的密钥库的绝对路径。 启用HTTPS时必需。
* **密钥库密码**，用于访问密钥库的密码。
* **密钥别名**，密钥库中密钥的别名。
* **密钥密码**、用于在密钥库中解锁密钥的密码。
* **客户端证书**，客户端提供有效证书的要求。 默认为无。

另请参 [阅启用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) ，以了解有关SSL相关选项的详细信息以及如何为CQSE启用HTTPS的完整说明。

**CQ重写器HTML分析器工厂**

控制CQ重写器的HTML分析器。

* **要处理的其他标记** -您可以添加或删除要由分析器处理的HTML标记。 默认情况下，会处理以下标记： A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD。
* **保留大小写** -默认情况下，HTML分析器将大小写为大小写的属性（如eBay）转换为小写的属性（如ebay）。 您可以关闭此选项以保留大小写混合属性。 当使用Angular 2等前框架时，此功能很有用。

**Day Commons JDBC Connections Pool** 配置对用作内容源的外部数据库的访问。

这是工厂配置，因此可以配置多个实例。

**Adobe CQ Media DPS Sessions Service** Manage DPS Sessions for use with Publications。

特别是，您可以定义 `dps.session.service.url.name`: 默认值设置为 [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**必须确保** AEM与CDN之间的CDN重写程序通信，以便以安全方式将资源／二进制文件交付给最终用户。 这涉及两个任务:

* 第一次（或在缓存中过期后）通过CDN从AEM访问资源。
* 安全地访问在CDN中缓存的资源，因为一旦在CDN中缓存资源，请求将不会转到AEM，应从CDN向所有有权访问该资源的用户提供服务。

AEM提供了一个重写程序，可将内部资产URL重写为外部CDN URL。 它会重写要传递到CDN的链接，包括JWS签名和过期时间，以便安全地访问资产。 此功能将用于创作实例。

总体流程如下：

1. 用户通过AEM进行身份验证，并请求包含资产的页面。
1. 请求的页面包含的资产与 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重写器将链接转换为包含JWS签名的CDN URL:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然后，用户的浏览器将资产请求转发到CDN服务器
1. 应将CDN配置为将请求与参数一起转发到 `cdn_sign` AEM。
1. 身份验证处理程序 `cdn_sign` 验证参数并将资产返回给CDN，然后将CDN交付给用户

用户浏览器、CDN和AEM之间的流可以按如下方式进行可视化。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能当前仅对AEM作者实例启用。

**CDNonfigServiceImpl提供** CDN配置

可通过在com.adobe.cq.cdn.rewriter.impl.CDNonfigServiceImpl **的配置中提供** CDN分发域名来启用CDN重写功能。

该服务还包含其他配置选项，如启用／禁用CDN重写、执行CDN重写的路径前缀、TTL值和协议（HTTP或HTTPS）。

**CDNRewriter** —— 用于将内部图像URL重写为CDN URL的重写程序

可 **以定义com.adobe.cq.cdn** .rewriter.impl.CDNRewriter中的“标记属性”值，以便只重写选择性图像链接。
