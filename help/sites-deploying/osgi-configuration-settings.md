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

[OSG](https://www.osgi.org/) 是AEM技术堆栈中的一个基本元素。它用于控制AEM的复合束及其配置。

OSGi &quot;*提供了标准化的基元，它允许应用程序由小的、可重用的和协作的组件构建。 这些组件可以组成应用程序并部署*”。

这样，可以轻松管理捆绑套件，因为可以单独停止、安装和启动捆绑套件。 互依关系将自动处理。 每个OSGi组件（请参见[OSGi规范](https://www.osgi.org/Specifications/HomePage)）都包含在各种捆绑包中。 使用AEM时，有多种方法管理此类包的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

以下OSGi配置设置（根据捆绑包列出）与项目实施相关。 并非所有列出的设置都需要调整，其中有些设置可以帮助您了解AEM的操作方式。

>[!CAUTION]
>
>该列表旨在作为准则，并非详尽无遗。 并不列出所有捆绑包，也不列出某些捆绑包的所有参数。
>
>所需的配置因项目而异。
>
>请参阅Web控制台，了解所用值和有关参数的详细信息。

>[!NOTE]
>
>OSGi配置差异工具是[AEM工具](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)的一部分，可用于列表默认OSGi配置。

>[!NOTE]
>
>AEM中的特定功能区域可能需要进一步的捆绑套件。 在这些情况下，可在与相应功能相关的页面上找到配置详细信息。

**AEM复制事件监** 听器配置：

* **运行模式**，其中复制事件将分发到监听器。 例如，如果定义为作者，则此系统将“启动”复制。

* 如果项目代码在发布事件中处理复制环境（反向复制），则需要添加运行模式&#x200B;**publish**。 例如，当调度程序用于从发布环境刷新时，或者当标准复制到其他发布实例时。

**AEM存储库更改** listenerConfigure:

* **路径**，用于侦听准备分发的存储库事件的位置。

**CRX Sling Client Repository** 配置对基础内容存储库的访问。

* 安装后应更改&#x200B;**管理员密码**，以确保实例的[安全性](/help/sites-administering/security-checklist.md)。
* 其他更改不必进行，必须小心，因为它们可能会影响对存储库的访问。

**Wiki邮件服** 务为Wiki发送的电子邮件配置电子邮件设置。

**Apache Felix OSGi管理控** 制台配置：

* **插件**,Apache Felix Web Management Console顶级菜单项中 **提供的主导** 航项目（控制台插件）。禁用您不需要的任何内容，因为每个内容都需要空间和资源。

>[!CAUTION]
>
>请务必配置以下各项：
>
>**用户** 名和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。
>初始安装后必须更改密码，以确保实例的[security](/help/sites-administering/security-checklist.md)。

>[!NOTE]
>
>此配置应在启动时根据需要使用Felix Console进行，然后再使用存储库。

**Apache Sling可自定义请求数据记录** 器配置：

* **记录** 器名 **称和日** 志格式，用于配置请求和访问记录的位置和格式(默认： `request.log`)。在分析与Web链相关的性能或调试功能时，此日志文件是必不可少的。
这与[Apache Sling请求记录器](#apacheslingrequestlogger)成对。

有关详细信息，请参阅[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling事件线程池** 配置：

* **最小** 池大 **小和最大池大小**，用于保存事件线程的池大小。

* **队列大小**，当池已用尽时线程队列的最大大小。建议的值为`-1`，因为这会将队列设置为“无限制”;如果设置了限制，则超出限制时可能会发生损失。

* 更改这些设置有助于在事件数较多的情况下实现性能；例如，繁重的AEM DAM或工作流使用。
* 应使用测试建立特定于您方案的值。
* 这些设置会影响实例的性能，因此，不要无故更改它们，并且要充分考虑。

**Apache SlingGET** Servlet配置渲染的一些方面：

* **自动** 索引，启用／禁用用于浏览的目录渲染。
* **启用** （或禁用）默认再现 **，如** HTML **、**&#x200B;纯文本 **** 、JSON **或** XML 。您不应禁用JSON。

>[!NOTE]
>
>如果在[生产就绪模式](/help/sites-administering/production-ready.md)中运行AEM，则会自动为生产实例配置此设置。

**Apache Sling Java Script** Handler配置将。java文件编译为脚本(servlet)的设置。

某些设置可能会影响性能，应尽可能禁用这些设置，尤其是对于生产实例。

* 源VM **和**&#x200B;目标VM **，将JDK版本定义为用作运行时JVM**

* 对于生产实例：

   * 禁用&#x200B;**生成调试信息**

**Apache Sling JCR安** 装程序这些参数可能不需要配置，但在开发或调试时可能很有用。例如，安装文件夹可用于签入／签出或创建包。

* **安装文件夹** 名称重 **新展开安装文件夹的最大层次结构深度** -指定在何处以及到哪个深度搜索存储库文件夹以查找要安装的资源。当使用通配符时（如中所示）。*/install)将搜索所有适当的匹配项，例如`/libs/sling/install`和`/libs/cq/core/install`。

* **搜索路径**、jcrinstall搜索要安装的资源的路径列表，以及一个表示该路径的权重因子的数字。

**Apache Sling作业事件处** 理程序配置管理作业调度的参数：

* **重试间隔** **、**&#x200B;最大重试、 **最大并行作业**、 **确认等待时间**，等等。

* 更改这些设置可以在大量作业的情况下提高性能；例如，大量使用AEM DAM和工作流。
* 应使用测试建立特定于您方案的值。
* 请勿随意更改这些设置，只有在适当考虑后更改。

**Apache Sling JSP脚本处** 理程序为JSP脚本处理程序配置性能相关设置。要提高性能，您应尽可能禁用。

特别是对于生产实例：

* 禁用&#x200B;**生成调试信息**
* 禁用&#x200B;**保持生成的Java**
* 禁用&#x200B;**映射的内容**
* 禁用&#x200B;**显示源片段**

>[!NOTE]
>
>如果在[生产就绪模式](/help/sites-administering/production-ready.md)中运行AEM，则会自动为生产实例配置此设置。

**Apache Sling日志记** 录配置：

* **日志** 级 **别和日志文件**，用于定义中央日志配置的位置和日志级别(error.log)。该级别可设置为`DEBUG`、`INFO`、`WARN`、`ERROR`和`FATAL`之一。

* **用于定义日** 志文 **件的大** 小和版本旋转的日志文件和日志文件阈值数。

* **消息** 模式定义日志消息的格式。

有关详细信息，请参阅[AEM Logging](/help/sites-deploying/configure-logging.md#global-logging)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling日志记录器配置（工厂配置）** 配置：

* **日志级**&#x200B;别、 **日志文** 件和消 **息格式** 定义日志文件和消息的详细信息。

* **** Loggerto定义类别;例如，仅com.day.cq的日志。

* 通过使用&#x200B;**工厂配置**，可以添加任意数量的附加配置以满足所需的各种日志级别和类别。
* 这种配置在开发过程中很有帮助；例如，在特定日志文件中记录特定服务的TRACE消息。
* 此类配置在生产环境中很有用；例如，将有关特定服务的消息记录到单个日志文件中，以便更轻松地进行监视。

有关详细信息，请参阅[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling日志记录编写器配置（工厂配置）** 配置：

* **日** 志文件，用于定义日志文件的存在性。
* **用于定义版** 本旋转的日志文件数。

* 编写器可以由&#x200B;**Apache Sling日志记录器配置**&#x200B;配置使用。

* 这种配置在开发过程中很有帮助；例如，在特定日志文件中记录特定服务的TRACE消息。
* 此类配置在生产环境中很有用；例如，将有关特定服务的消息记录到单个日志文件中，以便更轻松地进行监视。

有关详细信息，请参阅[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling主Servlet** 配置：

* **每个请求和递归** 深度 **的调** 用数，以保护系统免受无限递归和过多脚本调用的影响。

**Apache Sling MIME类型服** 务配置：

* **MIME** 类型，将项目所需的类型添加到系统。这允许对文件发出`GET`请求，以设置链接文件类型和应用程序的正确内容类型头。

**Apache Sling推荐人** 过滤器要解决CRX WebDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，您需要配置推荐人过滤器。

推荐人过滤器服务是一种OSGi服务，允许您配置：

* 应过滤哪些http方法
* 是否允许空推荐人头
* 以及允许除服务器主机外的列表服务器。

有关更多详细信息，请参阅[安全清单——跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。

>[!NOTE]
>
>Apache Sling推荐人过滤器取决于快速修复包的安装。

**Apache Sling Request** LoggerConfigure:

* 定义请求记录方式的各种参数。
* **启用请求日志**，以启用或禁用。

* **启用访问日志**，以启用或禁用。

这与[Apache Sling可自定义请求数据记录器](#apacheslingcustomizablerequestdatalogger)成对。

有关详细信息，请参阅[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Resource Resolver Factory配置** Sling资源解析的核心方面：

* **资源搜索路**&#x200B;径，添加任何项目特定路径(但不删除 `/libs` 或 `/apps`)。

* **虚拟** URL用于定义虚URL映射。

* **用于定** 义任何别名的URL映射；例如从 `/content` 到 `/`。

* **映射位置**，中外部的映射器配置 `/etc/map`。

* 使用本地安装（例如，使用`https://localhost:4502/system/console/jcrresolver`）确定哪个资源解析程序处于活动状态。

有关详细信息，请参阅：[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>特别是，这些选项必须在存储库中配置。
>
>否则，在下次启动时，AEM可能会覆盖使用Felix控制台对&#x200B;**URL映射**&#x200B;所做的更改。

**Apache Sling Servlet/Script Resolver和错误处理** 程序Sling Servlet和脚本解析程序具有多个任务:

1. 它用作`ServletResolver`来选择要调用的Servlet或Script来处理请求。

1. 它充当`SlingScriptResolver`。

1. 它通过使用与用于解析请求处理servlet和脚本相同的算法实现`ErrorHandler`接口来管理错误处理，以选择错误处理servlet和脚本。

可以设置各种参数，包括：

* **执行** 路径会滑动搜索可执行脚本的路径；通过配置特定路径，您可以限制可以执行的脚本。如果未配置路径，则使用默认值(`/` = root)，这允许执行所有脚本。
如果配置的路径值以斜杠结尾，则搜索整个子树。 如果没有这样的尾随斜杠，则只有在脚本完全匹配时，才会执行脚本。

* **脚本用户** -此可选属性可指定用于读取脚本的存储库用户帐户。如果未指定帐户，则默认情况下使用`admin`用户。

* **默** 认扩展将使用默认行为的扩展的列表。这意味着资源类型的最后一个路径段可用作脚本名称。

**Day Commons GFX Font Helper在** 渲染图形时，可以使用DrawText嵌入文本。对于此，您还可以安装您自己的字体：

* 定义要搜索项目特定字体的&#x200B;**字体路径**。
例如，`/apps/myapp/fonts`。

**Apache HTTP Components代理配** 置使用Apache HTTP客户端（在创建HTTP时使用）的所有代码的代理配置；例如，在复制时。

创建新配置时，请勿更改工厂配置，而应使用此处提供的配置管理器为此组件创建新工厂配置：**https://localhost:4502/system/console/configMgr/**。 代理配置在&#x200B;**org.apache.http.proxyconfigurator中可用。**

>[!NOTE]
>
>在AEM 6.0及更早版本中，代理在Day Commons HTTP Client中配置。 自AEM 6.1和更高版本发布以来，代理配置已移至“Apache HTTP Components Proxy Configuration”（Apache HTTP Components代理配置），而非“Day Commons HTTP Client”（Day Commons HTTP客户端）配置。

**Day CQ反** 垃圾邮件配置使用的反垃圾邮件服务(Akismet)。这要求您注册：

* **提供程序**
* **API密钥**
* **注册URL**

**AdobeGranite HTML库管** 理器配置此选项以控制客户端库（css或js）的处理；例如，包括如何看到底层结构。

* 对于生产实例：

   * 启用&#x200B;**Minify**（以删除CRLF和空格字符）。
   * 启用&#x200B;**Gzip**（以允许使用一个请求对文件进行gzip和访问）。
   * 禁用&#x200B;**调试**
   * 禁用&#x200B;**计时**

* 对于JS开发（尤其是当防火墙调试／调试时）:

   * 禁用&#x200B;**Minify**
   * 启用&#x200B;**Debug**&#x200B;以分离文件进行调试并与firebug一起使用。
   * 如果对计时感兴趣，请启用&#x200B;**计时**。
   * 启用&#x200B;**调试**&#x200B;控制台可查看JS控制台日志消息。

>[!CAUTION]
>
>更改&#x200B;**Minify**&#x200B;或&#x200B;**Gzip**&#x200B;的设置时，您还需要删除`/var/clientlibs`的内容。 这是clientlibs的缓存版本，将在下次请求时重新构建。

>[!NOTE]
>
>如果在[生产就绪模式](/help/sites-administering/production-ready.md)中运行AEM，则会自动为生产实例配置此设置。

**Day CQ HTTP头身份验证处** 理程序HTTP请求的基本身份验证方法的系统宽设置。

使用[已关闭的用户组](/help/sites-administering/cug.md)时，您可以配置（以及其他）:

* **HTTP领域**
* **默认登录页**

**Day CQ Link Checker ServiceCheck(第CQ天链** 接检查器服务)，并根据需要配置：

* **调度程序** 周期：定义自动检查外部链接的间隔。

* 检查&#x200B;**链路容差间隔**，在此期间，不成功的外部链路被视为错误。
* **链接检查覆盖模式**，以定义要从链接检查中排除的任何路径。

**Day CQ链接检查器任** 务为单个链接检查器任务(检查外部链接的任务)配置设置：

* 检查在&#x200B;**良好链路测试间隔**&#x200B;和&#x200B;**坏链路测试间隔**&#x200B;中定义的间隔

* 检查链接时外部访问所需的与Internet访问代理和NTLM相关的各种参数。

**Day CQ Mail Service为邮** 件服务器配置主机名和访问详细信息。请参阅配置邮件服务部分。

**第CQ天MCM** 新闻稿配置与Newsletter一起使用的各种设置。

**第CQ天根映** 射配置：

* **目标** 路径，用于定义“ ”的 `/`请求将重定向到的位置。

AEM中有两个可用的UI:

* 触屏优化UI是标准UI
* 而弃用的经典UI仍完全可操作

使用AEM根映射，您可以配置要作为实例默认值的UI:

* 要使触屏优化UI作为默认UI,**目标路径**&#x200B;应指向：

   ```
      /projects.html
   ```

* 要使经典UI作为默认UI,**目标路径**&#x200B;应指向：

   ```
      /welcome.html
   ```

>[!NOTE]
>
>在标准安装后，触屏优化UI是默认UI。

**AdobeGranite SSO身份验证** 处理程序配置单点登录(SSO)详细信息；在企业创作设置中，通常需要与LDAP结合使用。

有各种配置属性可用：

* **此身**
份验证处理程序处于活动状态的PathPath。如果此参数留空，则禁用身份验证处理程序。 例如，路径／会使身份验证处理程序用于整个存储库。

* **服务**
排名OSGi框架服务排名值用于指示用于调用此服务的顺序。这是 
`int` 值，其中值越高，则指定的优先级越高。默认值为 `0`.

* **标**
头名称可能包含用户ID的标题的名称。

* **Cookie**
名称可能包含用户ID的Cookie的名称。

* **参**
数名称可能提供用户ID的请求参数的名称。

* **用**
户映射对于选定用户，从HTTP请求提取的用户名可替换为凭据对象中的其他用户名。此处定义映射。 如果用户名 
`admin` 显示在映射的任一侧，将忽略映射。请注意，字符“=”必须用前导“\”进行转义。

* **格**
式指示提供用户ID的格式。用法:

   * `Basic` 用户ID是否以HTTP基本身份验证格式进行编码
   * `AsIs` 如果用户ID以纯文本形式提供，或者应按原样使用任何常规表达式应用值或任何常规表达式

**Day CQ WCM调试筛** 选器这在开发时很有用，因为它允许在访问页面时使用后缀，如？debug=layout。例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout将提供开发人员可能感兴趣的布局信息。

* 在生产实例上禁用此功能可确保性能和安全性。

**Day CQ WCM过** 滤器配置：

* **WCM模式**以定义默认模式。
* 在创作实例中，它可能为`edit`、`disable,preview`或`analytics`。
其他模式可以从Sidekick访问，或者后缀`?wcmmode=disabled`可用于模拟生产环境。

* 在发布实例上，必须将此值设置为`disabled`，以确保不能访问其他模式。

>[!NOTE]
>
>如果在[生产就绪模式](/help/sites-administering/production-ready.md)中运行AEM，则会自动为生产实例配置此设置。

**Day CQ WCM链接检查器配置** 器配置：

* **重写配置** 列表，以指定基于内容的链接检查器配置的位置列表。配置可以基于运行模式；这对于区分创作和发布环境很重要，因为linkchecker设置可能不同。

**Day CQ WCM页面处理** 器配置：

* **路径**，系统在触发之前监听页面修改的列表 `jcr:Event`。

**Adobe页印象** 跟踪器对于创作实例，请配置：

* **sling.auth.requirements**:将此属性的值设置为  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此配置将允许对跟踪服务进行匿名请求。

>[!NOTE]
>
>有关详细信息，请参阅[页面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM页面统** 计信息对于发布实例配置：

* **用于发送数** 据的URL配置用于跟踪页面统计信息的URL（如果跟踪器请求通过调度程序，该URL至关重要）;例如，默认值为 `https://localhost:4502/libs/wcm/stats/tracker`。

* **启用** 跟踪脚本以启 `true`用()或禁用( `false`)在页面上包含跟踪脚本。默认值为 `false`.

>[!NOTE]
>
>有关详细信息，请参阅[页面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM Version** Manager控制是否以及如何在系统中管理版本：

* **在激活时创建版本**，在标准安装中启用
* **启用清除**

* **清除路径**，搜索操作将搜索的路径
* **隐式版本控制路径**，即隐式版本控制处于活动状态的路径。

* **最大版本**，版本的最大年龄（以天为单位）

* **最大版本数**，要保留的最大版本数

有关详细信息，请参阅[版本清除](/help/sites-deploying/version-purging.md)。

**Day CQ Workflow Email Notification Service(日CQ工作流电** 子邮件通知服务)为工作流发送的通知配置电子邮件设置。

**Day CQSE HTTP** Service控制CQ Servlet引擎：

* **NIO for HTTP,**是否将NIO用于HTTP。 默认设置为 true。仅在启用HTTP时使用。
* **连接超时，**连接超时（以毫秒为单位）。 此属性同时适用于HTTP和HTTPS连接。 默认为60秒。

* **启用HTTPS,** 无论是否启用HTTPS。默认为false。
* **会话超时**，以分钟为单位指定的HTTP会话的默认生命周期。如果超时为0或更少，则会话永远不会超时。 默认为10分钟。
* **调试日志**，是否写入DEBUG级别消息。默认为false。
* **请求缓冲区大小**，请求的缓冲区大小（以字节为单位）。默认值为8KB。
* **最大线程数**，用于处理请求的线程数。默认值为200。

以下属性仅在启用HTTPS时适用。

* **HTTPS端口**，监听HTTPS请求的端口。默认为 433.
* **NIO for HTTPS**，是否将NIO用于HTTP。默认为NIO for HTTP属性的值。
* **密钥**&#x200B;库，用于HTTPS的密钥库的绝对路径。启用HTTPS时必需。
* **密钥库密码**，用于访问密钥库的密码。
* **密钥别名**，密钥库中密钥的别名。
* **密钥密码**、用于在密钥库中解锁密钥的密码。
* **客户端证书**，客户端提供有效证书的要求。默认为无。

另请参阅[启用HTTP over SSL](/help/sites-administering/ssl-by-default.md)，以了解与SSL相关的选项的详细信息以及如何为CQSE启用HTTPS的完整说明。

**CQ重写器HTML分析器工厂**

控制CQ重写器的HTML分析器。

* **要处理的其他标** 记——您可以添加或删除要由分析器处理的HTML标记。默认情况下，会处理以下标记：A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD。
* **保留大小写** -默认情况下，HTML分析器将大小写为大小写的属性（如eBay）转换为小写的属性（如ebay）。您可以关闭此选项以保留大小写混合属性。 当使用Angular 2等前框架时，此功能很有用。

**Day Commons JDBC Connections** Pool配置对用作内容源的外部数据库的访问。

这是工厂配置，因此可以配置多个实例。

**Adobe CQ媒体DPS会** 话服务管理DPS会话以与出版物一起使用。

具体而言，您可以定义`dps.session.service.url.name`:default设置为[https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN重** 写程序必须确保AEM与CDN之间的通信，以便以安全的方式向最终用户交付资源／二进制文件。这涉及两个任务:

* 第一次（或在缓存中过期后）通过CDN从AEM访问资源。
* 安全地访问在CDN中缓存的资源，因为一旦在CDN中缓存资源，请求将不会转到AEM，所有有权访问该资源的用户都应从CDN提供服务。

AEM提供一个重写程序，用于将内部资源URL重写到外部CDN URL。 它会重写要传递到CDN的链接，包括JWS签名和过期时间，以便安全地访问资产。 此功能将用于创作实例。

总体流程如下：

1. 用户通过AEM进行身份验证，并请求具有资产的页面。
1. 请求的页面包含类似于`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`的资产
1. 重写器将链接转换为包含JWS签名的CDN URL:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然后，用户的浏览器将资产请求转发到CDN服务器
1. 应将CDN配置为将请求与`cdn_sign`参数一起转发到AEM。
1. 身份验证处理程序验证`cdn_sign`参数并将资产返回给CDN，然后将CDN发送给用户

用户浏览器、CDN和AEM之间的流可以按如下方式进行可视化。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能当前仅对AEM作者实例启用。

**CDNConfigService** Impl提供CDN配置

通过在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的配置中提供&#x200B;**CDN分发域名**，可以启用CDN重写功能。

该服务还包含其他配置选项，如启用／禁用CDN重写、执行CDN重写的路径前缀、TTL值和协议（HTTP或HTTPS）。

**CDNRewriter** 用于将内部图像URL重写到CDN URL的重写程序

可以定义com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的&#x200B;**标记属性**&#x200B;值，以便只重写选择性图像链接。
