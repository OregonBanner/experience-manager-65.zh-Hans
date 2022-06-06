---
title: OSGi配置设置
seo-title: OSGi Configuration Settings
description: 本文详细介绍了与项目实施相关的OSGi配置设置（按包列出）。 该列表是一项准则，并且并不详尽。
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: e8320b1dac681fd2c9e749344e8c126487d840ba
workflow-type: tm+mt
source-wordcount: '3557'
ht-degree: 0%

---

# OSGi配置设置{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 是AEM技术堆栈中的一个基本元素。 它用于控制AEM的复合包及其配置。

OSGi &quot;*提供标准化的基元，允许应用程序从可重用的小组件和协作组件构建。 这些组件可以组合成应用程序并进行部署*&quot;

这样可以轻松管理包，因为可以单独停止、安装和启动包。 互依关系会自动处理。 每个OSGi组件(请参阅 [OSGi规范](https://www.osgi.org/Specifications/HomePage))包含在各种包中的一个包中。 使用AEM时，可通过多种方法来管理此类包的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的实践。

以下OSGi配置设置（根据包列出）与项目实施相关。 列出的设置并非都需要调整，其中有些设置可帮助您了解AEM的操作方式。

>[!CAUTION]
>
>该列表旨在作为准则，并不详尽。 并非列出了所有包，也未列出某些包的所有参数。
>
>所需的配置因项目而异。
>
>有关使用的值以及有关参数的详细信息，请参阅Web控制台。

>[!NOTE]
>
>OSGi配置差异工具， [AEM工具](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)，可用于列出默认OSGi配置。

>[!NOTE]
>
>对于AEM中的特定功能区域，可能需要其他包。 在这些情况下，可以在与相应功能相关的页面上找到配置详细信息。

**AEM复制事件侦听器** 配置：

* 的 **运行模式**，其中复制事件将分发给侦听器。 例如，如果定义为作者，则系统将“启动”复制。

* 运行模式 **发布** 如果项目代码在发布环境中处理复制事件（反向复制），则需要添加。 例如，当使用调度程序从发布环境刷新时，或当发生到其他发布实例的标准复制时。

**AEM存储库更改侦听器** 配置：

* 的 **路径**，用于侦听准备分发的存储库事件的位置。

**CRX Sling客户端存储库** 配置对基础内容存储库的访问权限。

* 的 **管理员密码** 应在安装后进行更改，以确保 [安全](/help/sites-administering/security-checklist.md) 实例。
* 不应进行其他更改，并且必须谨慎，因为这些更改会影响对存储库的访问。

**维基邮件服务** 为Wiki发送的电子邮件配置电子邮件设置。

**Apache Felix OSGi管理控制台** 配置：

* **插件**，主导航项目（控制台插件）将在 **Apache Felix Web管理控制台** 作为顶级菜单项。 禁用您不需要的任何内容，因为每个内容都需要空间和资源。

>[!CAUTION]
>
>请务必配置以下内容：
>
>**用户名** 和 **密码**，用于访问Apache Felix Web Management Console本身的凭据。
>初始安装后必须更改密码，以确保 [安全](/help/sites-administering/security-checklist.md) 实例。

>[!NOTE]
>
>此配置应使用Felix控制台进行，因为启动时需要此配置 — 在存储库可用之前。

**Apache Sling可自定义的请求数据记录器** 配置：

* **记录器名称** 和 **日志格式** 要配置请求和访问日志记录的位置和格式(默认值： `request.log`)。 在分析与Web链相关的性能或调试功能时，此日志文件至关重要。
这与 [Apache Sling请求记录器](#apacheslingrequestlogger).

有关详细信息，请参阅 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/site/logging.html).

**Apache Sling事件线程池** 配置：

* **最小池大小** 和 **最大池大小**，用于保存事件线程的池大小。

* **队列大小**，池耗尽时线程队列的最大大小。
建议的值为 `-1` 这将队列设置为“无限制”；如果设置了限制，则在超出限制时可能会发生损失。

* 更改这些设置有助于在事件数量较多的情况下提高性能；例如，大量AEM DAM或工作流的使用情况。
* 应使用测试建立特定于您方案的值。
* 这些设置可能会影响实例的性能，因此请不要无故和适当考虑地更改它们。

**Apache SlingGETServlet** 配置渲染的某些方面：

* **自动索引** 启用/禁用用于浏览的目录渲染。
* **启用** （或禁用）默认演绎版，例如 **HTML**, **纯文本**, **JSON** 或 **XML**.
您不应禁用JSON。

>[!NOTE]
>
>如果您在 [生产就绪模式](/help/sites-administering/production-ready.md).

**Apache Sling Java脚本处理程序** 配置将.java文件编译为脚本(servlet)的设置。

某些设置可能会影响性能，应尽可能禁用这些设置，尤其是对于生产实例。

* **源虚拟机** 和 **目标虚拟机**，将JDK版本定义为用作运行时JVM的版本

* 对于生产实例：

   * 禁用 **生成调试信息**

**Apache Sling JCR安装程序** 这些参数可能不需要配置，但在开发或调试时可能有助于了解这些参数。 例如，安装文件夹可用于签入/签出或创建包。

* **安装文件夹名称正则表达式** 和 **安装文件夹的最大层次结构深度**  — 指定在何处和到哪个深度搜索要安装的资源库文件夹。 使用通配符时（如中所示）。&#42;/install)将搜索所有适当的匹配项，例如， `/libs/sling/install` 和 `/libs/cq/core/install`.

* **搜索路径**, jcrinstall搜索要安装的资源的路径列表，以及指示该路径的权重因子的数字。

**Apache Sling作业事件处理程序** 配置用于管理作业计划的参数：

* **重试间隔**, **最大重试次数**, **最大并行作业数**, **确认等待时间**&#x200B;等。

* 更改这些设置可以提高大量作业情况下的性能；例如，大量使用AEM DAM和工作流。
* 应使用测试建立特定于您方案的值。
* 请勿随意更改这些设置，只有在适当考虑后才进行更改。

**Apache Sling JSP脚本处理程序** 为JSP脚本处理程序配置与性能相关的设置。 要提高性能，应尽可能禁用。

特别是对于生产实例：

* 禁用 **生成调试信息**
* 禁用 **保留生成的Java**
* 禁用 **映射的内容**
* 禁用 **显示源片段**

>[!NOTE]
>
>如果您在 [生产就绪模式](/help/sites-administering/production-ready.md).

**Apache Sling日志记录配置** 配置：

* **日志级别** 和 **日志文件**，以定义中央日志记录配置(error.log)的位置和日志级别。 级别可设置为 `DEBUG`, `INFO`, `WARN`, `ERROR` 和 `FATAL`.

* **日志文件数** 和 **日志文件阈值** 定义日志文件的大小和版本旋转。

* **消息模式** 定义日志消息的格式。

有关详细信息，请参阅 [AEM日志记录](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling日志记录](https://sling.apache.org/site/logging.html).

**Apache Sling日志记录器配置（工厂配置）** 配置：

* **日志级别**, **日志文件** 和 **消息格式** 定义日志文件和消息的详细信息。

* **记录器** 定义类别；例如，仅对com.day.cq执行日志。

* 使用 **工厂配置**，则可以添加任意数量的其他配置以满足所需的各种日志级别和类别。
* 这种配置在开发过程中很有帮助；例如，将特定服务的TRACE消息记录到特定日志文件中。
* 此类配置在生产环境中非常有用；例如，将有关特定服务的消息记录到单个日志文件中，以便更便于监控。

有关详细信息，请参阅 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/site/logging.html).

**Apache Sling日志记录编写器配置（工厂配置）** 配置：

* **日志文件** 定义日志文件的存在性。
* **日志文件数** 定义版本旋转。

* 编写器可由 **Apache Sling日志记录器配置** 配置。

* 这种配置在开发过程中很有帮助；例如，将特定服务的TRACE消息记录到特定日志文件中。
* 此类配置在生产环境中非常有用；例如，将有关特定服务的消息记录到单个日志文件中，以便更便于监控。

有关详细信息，请参阅 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/site/logging.html).

**Apache Sling主Servlet** 配置：

* **每个请求的调用数** 和 **递归深度** 以防止系统出现无限递归和过多脚本调用。

**Apache Sling MIME类型服务** 配置：

* **MIME类型** 以将项目所需的内容添加到系统中。 这允许 `GET` 请求为链接文件类型和应用程序设置正确的content-type标头。

**Apache Sling反向链接过滤器** 要解决CRX WebDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，您需要配置反向链接过滤器。

反向链接过滤器服务是一种OSGi服务，可用于配置：

* 应筛选哪些http方法
* 是否允许空反向链接标头
* 以及除服务器主机外允许的服务器列表。

请参阅 [安全检查列表 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以了解更多详细信息。

>[!NOTE]
>
>Apache Sling反向链接过滤器依赖于快速修补程序包的安装。

**Apache Sling请求记录器** 配置：

* 用于定义请求记录方式的各种参数。
* **启用请求日志**、启用或禁用。

* **启用访问日志**、启用或禁用。

这与 [Apache Sling可自定义的请求数据记录器](#apacheslingcustomizablerequestdatalogger).

有关详细信息，请参阅 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Factory** 配置Sling资源解析的核心方面：

* **资源搜索路径**(s)，添加任何项目特定路径(但不删除 `/libs` 或 `/apps`)。

* **虚拟URL** 定义虚URL映射。

* **URL映射** 定义任何别名；例如 `/content` to `/`.

* **映射位置**，映射器配置外部化为 `/etc/map`.

* 使用本地安装(例如，使用 `https://localhost:4502/system/console/jcrresolver`)来确定哪个资源解析程序处于活动状态。

有关详细信息，请参阅： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>特别是，必须在存储库中配置这些选项。
>
>否则，将对 **URL映射** 下次启动时，AEM可能会覆盖使用Felix控制台的情况。

**Apache Sling Servlet/脚本解析程序和错误处理程序** Sling Servlet和脚本解析程序有多项任务：

1. 它用作 `ServletResolver` 来选择要调用以处理请求的Servlet或脚本。

1. 它充当 `SlingScriptResolver`.

1. 它通过实施 `ErrorHandler` 界面使用与用于解析请求处理servlet和脚本相同的算法来选择错误处理servlet和脚本。

可以设置各种参数，包括：

* **执行路径** 列出搜索可执行脚本的路径；通过配置特定路径，您可以限制可以执行的脚本。 如果未配置路径，则使用默认路径( `/` = root)，则允许执行所有脚本。
如果配置的路径值以斜杠结尾，则会搜索整个子树。 如果没有这样的尾随斜杠，则仅当脚本与脚本完全匹配时，才会执行脚本。

* **脚本用户**  — 此可选属性可指定用于读取脚本的存储库用户帐户。 如果未指定帐户，则 `admin` 默认使用用户。

* **默认扩展** 将使用默认行为的扩展的列表。 这意味着资源类型的最后一个路径段可用作脚本名称。

**Day Commons GFX字体助手** 在渲染图形时，可以使用DrawText嵌入文本。 为此，您还可以安装自己的字体：

* 定义 **字体路径** 搜索项目特定字体。
例如， `/apps/myapp/fonts`.

**Apache HTTP组件代理配置** 使用Apache HTTP客户端的所有代码的代理配置，在进行HTTP时使用；例如，复制时。

创建新配置时，请勿更改工厂配置，而是使用此处提供的配置管理器为此组件创建新的工厂配置： **https://localhost:4502/system/console/configMgr/**. 代理配置在 **org.apache.http.proxyconfigurator。**

>[!NOTE]
>
>在AEM 6.0及更早版本中，代理是在Day Commons HTTP客户端中配置的。 自AEM 6.1及更高版本起，代理配置已移至“Apache HTTP组件代理配置”，而不是“Day Commons HTTP Client”配置。

**Day CQ Antispam** 配置使用的反垃圾邮件服务(Akismet)。 这要求您注册：

* **提供程序**
* **API密钥**
* **注册的URL**

**AdobeGraniteHTML库管理器** 配置此设置以控制客户端库（css或js）的处理；包括如何查看底层结构。

* 对于生产实例：

   * 启用 **缩小** （删除CRLF和空格字符）。
   * 启用 **Gzip** （允许使用一个请求对文件进行压缩和访问）。
   * 禁用 **调试**
   * 禁用 **计时**

* 对于JS开发（尤其是在进行消息调试时）：

   * 禁用 **缩小**
   * 启用 **调试** 来分隔文件以进行调试和与firebug一起使用。
   * 启用 **计时** 对时间感兴趣。
   * 启用 **调试** 控制台以查看JS控制台日志消息。

>[!CAUTION]
>
>更改 **缩小** 或 **Gzip** 您还需要删除 `/var/clientlibs`. 这是Clientlibs的缓存版本，将在下次请求时重新构建。

>[!NOTE]
>
>如果您在 [生产就绪模式](/help/sites-administering/production-ready.md).

**Day CQ HTTP标头身份验证处理程序** HTTP请求的基本身份验证方法的系统范围设置。

使用 [封闭用户组](/help/sites-administering/cug.md) 您可以配置（其中包括）：

* **HTTP领域**
* 的 **默认登录页面**

**Day CQ Link Checker服务** 检查并（如有必要）配置：

* **调度程序周期** 定义自动检查外部链接的间隔。

* 检查 **链路容差间隔错误** 在失败的外部链接被视为坏的时段内。
* **链接检查覆盖模式**，以定义要从链接检查中排除的任何路径。

**Day CQ Link Checker任务** 为单个链接检查器任务（用于检查外部链接的任务）配置设置：

* 检查 **良好的链接测试间隔** 和 **链路测试间隔错误**

* 检查链接时外部访问所需的与Internet访问代理和NTLM相关的各种参数。

**Day CQ Mail Service** 为邮件服务器配置主机名和访问详细信息。 请参阅配置邮件服务一节。

**Day CQ MCM新闻稿** 配置新闻稿中使用的各种设置。

**Day CQ根映射** 配置：

* **目标路径** 定义请求“ `/`“ ”将被重定向到。

AEM中提供了两个UI:

* 触屏优化UI是标准UI
* 且已弃用的经典UI仍完全可操作

使用AEM根映射，您可以配置要作为实例默认UI的UI:

* 要将触屏优化UI作为默认UI，请执行以下操作： **目标路径** 应指向：

   ```shell
      /projects.html
   ```

* 要将经典UI作为默认UI，请在 **目标路径** 应指向：

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>标准安装后，触屏优化UI是默认UI。

**AdobeGranite SSO身份验证处理程序** 配置单点登录(SSO)详细信息；在企业创作设置中，通常需要使用这些参数，通常与LDAP结合使用。

提供了各种配置属性：

* **路径**
此身份验证处理程序处于活动状态的路径。 如果此参数留空，则禁用身份验证处理程序。 例如，路径/会导致将身份验证处理程序用于整个存储库。

* **服务排名**
OSGi框架服务排名值用于指示调用此服务的顺序。 这是 
`int` 值越高，则指定的优先级越高。
默认值为 `0`.

* **标题名称**
可能包含用户ID的标头的名称。

* **Cookie名称**
可能包含用户ID的Cookie的名称。

* **参数名称**
可能提供用户ID的请求参数的名称。

* **用户映射**
对于选定的用户，从HTTP请求提取的用户名可以在凭据对象中替换为不同的用户名。 此处定义了映射。 如果用户名 
`admin` 显示在映射的任一侧，将忽略映射。 请注意，字符“=”必须使用前导“\”进行转义。

* **格式**
指示提供用户ID的格式。 使用:

   * `Basic` 用户ID是否采用HTTP Basic Authentication格式进行编码
   * `AsIs` 如果用户ID以纯文本提供，或者应按原样使用任何已应用的正则表达式值或任何正则表达式

**Day CQ WCM调试过滤器** 当进行开发时，这非常有用，因为它允许在访问页面时使用后缀，如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout将提供开发人员可能感兴趣的布局信息。

* 在生产实例上禁用此功能，以确保性能和安全性。

**Day CQ WCM过滤器** 配置：

* **WCM模式**定义默认模式。
* 在创作实例上，这可能是 `edit`, `disable,preview` 或 `analytics`.
其他模式可以从Sidekick或后缀访问 `?wcmmode=disabled` 可用于模拟生产环境。

* 在发布实例上，必须将此参数设置为 `disabled` 以确保无其他模式可访问。

>[!NOTE]
>
>如果您在 [生产就绪模式](/help/sites-administering/production-ready.md).

**Day CQ WCM Link Checker配置器** 配置：

* **重写配置列表** ，以指定基于内容的链接检查器配置的位置列表。 配置可以基于运行模式；这对于区分创作环境和发布环境很重要，因为linkchecker设置可能不同。

**Day CQ WCM页面管理器工厂** 配置：

* **页面子树激活检查** （没有复制权限）来删除或移动页面（即使页面未激活）。

**Day CQ WCM页面处理器** 配置：

* **路径**，系统在触发 `jcr:Event`.

**Adobe页面展示次数跟踪器** 对于创作实例，配置：

* **sling.auth.requirements**:将此属性的值设置为 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此配置将允许对跟踪服务进行匿名请求。

>[!NOTE]
>
>请参阅 [页面展示次数](/help/sites-deploying/configuring.md#enabling-page-impressions) 以了解更多信息。

**Day CQ WCM页面统计信息** 对于发布实例配置：

* **用于发送数据的URL** 配置用于跟踪页面统计信息的URL（如果跟踪器请求通过调度程序，则此URL至关重要）；例如，默认值为 `https://localhost:4502/libs/wcm/stats/tracker`.

* **已启用跟踪脚本** 启用( `true`)或禁用( `false`)在页面中包含跟踪脚本。 默认值为 `false`。

>[!NOTE]
>
>请参阅 [页面展示次数](/help/sites-deploying/configuring.md#enabling-page-impressions) 以了解更多信息。

**Day CQ WCM版本管理器** 控制系统中是否以及如何管理版本：

* **激活时创建版本**，在标准安装中启用
* **启用清除**

* **清除路径**，搜索操作将搜索的路径
* **隐式版本控制路径**，隐式版本控制处于活动状态的路径。

* **最大版本年龄**，版本的最大年龄（以天为单位）

* **最大数量版本**，要保留的最大版本数

请参阅 [版本清除](/help/sites-deploying/version-purging.md) 以了解更多信息。

**Day CQ工作流电子邮件通知服务** 为工作流发送的通知配置电子邮件设置。

**CQ重写器HTML解析器工厂**

控制CQ重写器的HTML解析器。

* **要处理的其他标记**  — 您可以添加或删除HTML器要处理的标记。 默认情况下，会处理以下标记：A，IMG，AREA，FORM，BASE，LINK，SCRIPT，BODY，HEAD。
* **保留驼峰**  — 默认情况下，HTML解析器将驼峰式（例如eBay）属性转换为小写式（例如ebay）属性。 您可以关闭此选项以保留驼峰式大小写属性。 在使用前端框架(如Angular2)时，这非常有用。

**Day Commons JDBC连接池** 配置对用作内容源的外部数据库的访问。

这是工厂配置，因此可以配置多个实例。

**Adobe CQ Media DPS会话服务** 管理DPS会话以与发布结合使用。

特别是，您可以定义 `dps.session.service.url.name`:默认值设置为 [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN重写程序** 必须确保AEM与CDN之间的通信，以便以安全的方式将资产/二进制文件交付给最终用户。 这包括两项任务：

* 首次（或在缓存中过期后）通过CDN从AEM访问资源。
* 安全地访问缓存在CDN中的资源，因为一旦该资源缓存在CDN中，则该请求不会转到AEM，所有在上有权访问该资源的用户都应从CDN提供。

AEM提供了一个重写器，用于将内部资产URL重写到外部CDN URL。 它会重写要传递到CDN的链接，包括JWS签名和过期时间，以便安全地访问资产。 此功能将用于创作实例。

总体流程如下：

1. 用户通过AEM进行身份验证，并请求包含资产的页面。
1. 请求的页面包含类似于 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重写器将转换指向包含JWS签名的CDN URL的链接：
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然后，用户的浏览器将资产请求转发到CDN服务器
1. 应将CDN配置为将请求与 `cdn_sign` 参数。
1. 身份验证处理程序验证 `cdn_sign` 参数并将资产返回到CDN，然后再交付给用户

用户的浏览器、CDN和AEM之间的流量可以如下所示。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>当前仅为AEM创作实例启用此功能。

**CDNConfigServiceImpl** 提供CDN配置

可通过提供 **CDN分发域名** 在com.adobe.cq.cdn.rewriter.impl.CDNonfigServiceImpl的配置中。

该服务还包含其他配置选项，例如启用/禁用CDN重写、执行CDN重写的路径前缀、TTL值和协议（HTTP或HTTPS）。

**CDNRewriter** 用于将内部图像URL重写到CDN URL的重写器

的 **标记属性** com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的值可以定义，以便只重写选择性图像链接。
