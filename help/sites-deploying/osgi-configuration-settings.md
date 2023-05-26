---
title: OSGi配置
seo-title: OSGi Configuration Settings
description: 本文详细介绍了与项目实施相关的OSGi配置设置（按捆绑包列出）。 该列表用作指南，并非详尽无遗。
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
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '3430'
ht-degree: 0%

---

# OSGi配置{#osgi-configuration-settings}

[osgi](https://www.osgi.org/) 是AEM技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。

OSGi ”*提供标准化的基元，允许使用小型、可重用和协作组件构建应用程序。 这些组件可以组合为一个应用程序并部署*“。

此功能允许对捆绑包进行轻松管理，因为它们可以单独停止、安装和启动。 系统会自动处理相互依赖关系。 每个OSGi组件(请参见 [OSGi规范](https://docs.osgi.org/specification/))包含在多个捆绑包中的一个。 使用AEM时，可通过多种方法管理此类捆绑包的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息和建议的做法。

以下OSGi配置设置（按捆绑包列出）与项目实施相关。 并非列出的所有设置都需要调整，这里提到了一些设置以帮助您了解AEM的运行方式。

>[!CAUTION]
>
>该列表旨在用作指南，并非详尽无遗。 未列出所有包，也未列出某些已列出包的所有参数。
>
>所需的配置因项目而异。
>
>有关使用的值和参数的详细信息，请参阅Web控制台。

>[!NOTE]
>
>OSGi配置比较工具，属于 [AEM工具](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=zh-Hans)，可用于列出默认的OSGi配置。

>[!NOTE]
>
>对于AEM中的特定功能区域，可能需要其他捆绑包。 在这些情况下，可在与相应功能相关的页面上找到配置详细信息。

**AEM复制事件侦听器** 配置：

* 此 **运行模式**，其中复制事件将分发给侦听器。 例如，如果定义为作者，则是“启动”复制的系统。

* 添加运行模式 **发布** 如果项目代码在发布环境中处理复制事件（反向复制）。 例如，使用Dispatcher从发布环境刷新时，或发生到其他发布实例的标准复制时。

**AEM资料档案库更改监听程序** 配置：

* 此 **路径**，用于侦听可供分发的存储库事件的位置。

**CRX Sling客户端存储库** 配置对基础内容存储库的访问权限。

* 此 **管理员密码** 安装后应进行更改，以确保 [安全性](/help/sites-administering/security-checklist.md) 实例的URL。
* 其他更改可能影响到对存储库的访问，因此无需进行更改，必须谨慎。

**Apache Felix OSGi管理控制台** 配置：

* **插件**，则中可用的主导航项目（控制台插件） **Apache Felix Web管理控制台** 作为顶级菜单项。 禁用不需要的任何内容，因为每个内容都需要空间和资源。

>[!CAUTION]
>
>请务必配置以下内容：
>
>**用户名** 和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。
>初次安装后必须更改密码，以确保 [安全性](/help/sites-administering/security-checklist.md) 实例的URL。

>[!NOTE]
>
>应在启动时根据需要使用Felix控制台进行此配置 — 在存储库可用之前。

**Apache Sling可自定义请求数据记录器** 配置：

* **记录器名称** 和 **日志格式** 配置请求和访问日志记录的位置和格式(默认： `request.log`)。 在分析与Web链相关的性能或调试功能时，此日志文件至关重要。 它与 [Apache Sling请求记录器](#apacheslingrequestlogger).

参见 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling事件线程池** 配置：

* **最小池大小** 和 **最大池大小**，用于保存事件线程的池的大小。

* **队列大小**，池耗尽时线程队列的最大大小。
推荐值为 `-1` 因为它将队列设置为无限制。 如果设置了限制，则超出限制时可能会发生丢失。

* 更改这些设置有助于在具有大量事件的情况下提高性能。 例如，重型AEM DAM或工作流使用。
* 应使用测试建立特定于您的方案的值。
* 这些设置可能会影响实例的性能，因此请勿在没有适当考虑的情况下更改它们。

**Apache SlingGETServlet** 配置渲染的某些方面：

* **自动索引** 启用/禁用浏览的目录渲染。
* **启用** （或禁用）默认呈现版本，例如 **HTML**， **纯文本**， **JSON**，或 **XML**.
请勿禁用JSON。

>[!NOTE]
>
>如果您在中运行AEM，则会自动为生产实例配置此设置 [生产就绪模式](/help/sites-administering/production-ready.md).

**Apache Sling JavaScript处理程序** 将设置配置为将.java文件编译为脚本(servlet)。

某些设置可能会影响性能。 请尽可能禁用这些设置，特别是对于生产实例。

* **源VM** 和 **目标VM**，定义用作运行时JVM的JDK版本

* 对于生产实例：

   * disable **生成调试信息**

**Apache Sling JCR安装程序** 这些参数可能不需要配置，但在开发或调试时可用于了解这些参数。 例如，安装文件夹对于签入或签出或者创建包非常有用。

* **安装文件夹名称regexp** 和 **安装文件夹的最大层次结构深度**  — 指定在存储库文件夹中搜索要安装的资源的位置和深度。 当使用通配符时（如中的）。&#42;/install)搜索所有合适的匹配项，例如， `/libs/sling/install` 和 `/libs/cq/core/install`.

* **搜索路径**，jcrinstall搜索要安装的资源的路径列表，以及指示该路径的权重因子的数字。

**Apache Sling作业事件处理程序** 配置用于管理作业调度的参数：

* **重试间隔**， **最大重试次数**， **最大并行作业数**， **确认等待时间**，等等。

* 更改这些设置可以提高大量作业场景中的性能；例如，大量使用AEM DAM和工作流。
* 应使用测试建立特定于您的方案的值。
* 请勿无故更改这些设置，只有在经过适当考虑后才会更改。

**Apache Sling JSP脚本处理程序** 为JSP脚本处理程序配置与性能相关的设置。 要提高性能，您应该尽可能禁用。

特别是对于生产实例：

* disable **生成调试信息**
* disable **保留生成的Java™**
* disable **映射的内容**
* disable **显示源片段**

>[!NOTE]
>
>如果您在中运行AEM，则会自动为生产实例配置此设置 [生产就绪模式](/help/sites-administering/production-ready.md).

**Apache Sling日志记录配置** 配置：

* **日志级别** 和 **日志文件**，以定义中央日志记录配置(error.log)的位置和日志级别。 级别可以设置为以下之一 `DEBUG`， `INFO`， `WARN`， `ERROR`、和 `FATAL`.

* **日志文件数** 和 **日志文件阈值** 定义日志文件的大小和版本轮换。

* **消息模式** 定义日志消息的格式。

参见 [AEM日志记录](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling日志记录](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling日志记录器配置（工厂配置）** 配置：

* **日志级别**， **日志文件** 和 **消息格式** 定义日志文件和消息的详细信息。

* **Logger** 定义类别；例如，仅记录com.day.cq。

* 通过使用 **工厂配置**，可添加任意数量的其他配置，以满足各种所需日志级别和类别的要求。
* 在开发过程中，此类配置非常有用；例如，在特定日志文件中记录特定服务的TRACE消息。
* 在生产环境中，此类配置非常有用；例如，将有关特定服务的消息记录到单个日志文件以便更轻松地监视。

参见 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling日志记录编写器配置（工厂配置）** 配置：

* **日志文件** 定义日志文件的存在。
* **日志文件数** 以定义版本轮换。

* 编写器可由 **Apache Sling日志记录器配置** 配置。

* 在开发过程中，此类配置非常有用；例如，在特定日志文件中记录特定服务的TRACE消息。
* 在生产环境中，此类配置非常有用；例如，将有关特定服务的消息记录到单个日志文件以便更轻松地监视。

参见 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling主Servlet** 配置：

* **每个请求的调用数** 和 **递归深度** 保护您的系统免受无限递归和过多的脚本调用的影响。

**Apache Sling MIME类型服务** 配置：

* **MIME类型** 以将项目所需的类型添加到系统。 这样做允许 `GET` 请求对文件设置正确的content-type标头，以链接文件类型和应用程序。

**Apache Sling引用过滤器** 要解决CRX WebDAV和Apache Sling中的跨站点请求伪造(CSRF)的已知安全问题，您必须配置反向链接过滤器。

反向链接筛选服务是一个OSGi服务，它允许您配置：

* 应该筛选哪些http方法
* 是否允许空的反向链接标头
* 以及除服务器主机之外还允许使用的服务器列表。

请参阅 [安全核对清单 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 了解更多详细信息。

>[!NOTE]
>
>Apache Sling引用过滤器取决于快速修补程序包的安装。

**Apache Sling请求记录器** 配置：

* 用于定义如何记录请求的各种参数。
* **启用请求日志**，启用或禁用。

* **启用访问日志**，启用或禁用。

与 [Apache Sling可自定义请求数据记录器](#apacheslingcustomizablerequestdatalogger).

参见 [AEM日志记录](/help/sites-deploying/configure-logging.md) 和 [Sling日志记录](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling资源解析程序工厂** 配置Sling资源解析的中心方面：

* **资源搜索路径**，添加任何项目特定的路径(但不删除 `/libs` 或 `/apps`)。

* **虚拟URL** 以定义虚URL映射。

* **URL映射** 以定义任何别名。 例如，从 `/content` 到 `/`.

* **映射位置**，映射器配置已外部化 `/etc/map`.

* 使用本地安装(例如，使用 `https://localhost:4502/system/console/jcrresolver`)，以确定哪个Resource Resolver处于活动状态。

请参阅： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>在存储库中配置这些选项。
>
>否则，将对以下对象所做的更改 **URL映射** 下次启动时，AEM可能会覆盖使用Felix控制台的情况。

**Apache Sling Servlet/脚本解析器和错误处理程序** Sling Servlet和脚本解析程序有多个任务：

1. 它被用作 `ServletResolver` 选择要调用以处理请求的Servlet或脚本。

1. 它充当 `SlingScriptResolver`.

1. 它通过实施 `ErrorHandler` 使用与用于解决请求处理servlet和脚本的相同的算法来选择错误处理servlet和脚本的接口。

可以设置各种参数，包括：

* **执行路径**  — 列出搜索可执行脚本的路径。 通过配置特定路径，您可以限制可以运行的脚本。 如果未配置任何路径，则使用默认值( `/` = root)，允许运行所有脚本。
如果配置的路径值以斜杠结尾，则会搜索整个子树。 如果没有此类尾随斜杠，则只有在脚本完全匹配时才运行脚本。

* **脚本用户**  — 此可选属性可以指定用于读取脚本的存储库用户帐户。 如果未指定帐户，则 `admin` 默认使用用户。

* **默认扩展**  — 使用默认行为的扩展列表。 资源类型的最后一个路径段可用作脚本名称。

**Apache HTTP组件代理配置**  — 使用Apache HTTP客户端的所有代码的代理配置，在生成HTTP时使用。 例如，在复制时。

创建配置时，请勿更改出厂配置。 请改用此处提供的配置管理器为此组件创建工厂配置： **https://localhost:4502/system/console/configMgr/**. 代理配置位于 **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>在AEM 6.0及更早的版本中，代理是在Day Commons HTTP Client中配置的。 从AEM 6.1及更高版本开始，代理配置已移至“Apache HTTP组件代理配置”而不是“Day Commons HTTP Client”配置。

**Day CQ Antispam** 配置使用的反垃圾邮件服务(Akismet)。 此功能要求您注册以下内容：

* **提供程序**
* **API密钥**
* **已注册的URL**

**AdobeGraniteHTML库管理器** 配置以控制对客户端库（css或js）的处理，包括例如如何查看基础结构。

* 对于生产实例：

   * 启用 **Minify** （删除CRLF和空白字符）。
   * 启用 **Gzip** （允许通过一个请求来压缩和访问文件）。
   * disable **调试**
   * disable **计时**

* 对于JS开发（尤其是在firebugging/debugging时）：

   * disable **Minify**
   * 启用 **调试** 分隔文件进行调试并与fire bug一起使用。
   * 启用 **计时** 如果对时机的选择感兴趣。
   * 启用 **调试** 控制台以查看JS控制台日志消息。

>[!CAUTION]
>
>更改以下任一项的设置时： **Minify** 或 **Gzip**，删除clientlibs缓存的内容。 参见 [知识库文章](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=zh-Hans) 了解详细信息。

>[!NOTE]
>
>如果您在中运行AEM，则会自动为生产实例配置此设置 [生产就绪模式](/help/sites-administering/production-ready.md).

**Day CQ HTTP标头身份验证处理程序** HTTP请求的基本身份验证方法的系统范围设置。

使用时 [封闭用户组](/help/sites-administering/cug.md)，您可以配置（其中包括）以下各项：

* **HTTP领域**
* 此 **默认登录页面**

**Day CQ链接检查器服务** 检查并配置（如有必要）：

* **计划程序时段** 定义自动检查外部链接的间隔。

* Check **链路容差间隔错误** 不成功的外部链接被视为坏链接的时段。
* **链接检查覆盖模式**，以定义要从链接检查中排除的任何路径。

**Day CQ Link Checker任务** 配置单个链接检查器任务（检查外部链接的任务）的设置：

* 检查中定义的间隔 **良好链接测试间隔** 和 **错误链接测试间隔**

* 与检查链接时外部访问所需的Internet访问代理和NTLM相关的各种参数。

**Day CQ邮件服务** 配置邮件服务器的主机名和访问详细信息。 请参阅配置邮件服务一节。

**Day CQ MCM新闻稿** 配置新闻稿中使用的各种设置。

**Day CQ根映射** 配置：

* **目标路径** 以定义在何处向&quot; `/`“ ”已重定向至。

AEM中有两个可用的UI：

* 触屏优化UI是标准UI
* 并且已弃用的经典UI仍处于完全运行状态

使用AEM根映射，您可以配置要用作实例的默认UI：

* 要将触屏UI作为默认UI，请 **目标路径** 应指向以下内容：

   ```shell
      /projects.html
   ```

* 要将经典UI作为默认UI，请 **目标路径** 应指向以下内容：

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>在标准安装中，触摸优化UI是默认UI。

**AdobeGranite SSO身份验证处理程序**  — 配置SSO（单点登录）详细信息。 企业创作设置通常需要这些详细信息，通常使用LDAP。

可以使用各种配置属性：

* **路径**
此身份验证处理程序活动的路径。 如果此参数留空，则将禁用身份验证处理程序。 例如，路径/使身份验证处理程序用于整个存储库。

* **服务排名**
OSGi框架服务排名值用于指示调用此服务所用的顺序。 此值是一个 
`int` 值越高，表示优先级越高。
默认值为 `0`.

* **标题名称**
可能包含用户ID的标头的名称。

* **Cookie名称**
可能包含用户ID的Cookie的名称。

* **参数名称**
可能提供用户ID的请求参数的名称。

* **用户映射**
对于选定的用户，可以将从HTTP请求提取的用户名替换为凭据对象中的其他用户名。 此处定义了映射。 如果用户名称 
`admin` 显示在映射的任何一侧，映射将被忽略。 字符“=”必须使用前导“\”进行转义。

* **格式**
指示提供用户ID的格式。 使用:

   * `Basic` 如果用户ID采用HTTP基本身份验证格式编码
   * `AsIs` 如果用户ID以纯文本形式提供，或者任何正则表达式应按原样使用applied值，或者使用任何正则表达式

**Day CQ WCM调试过滤器** 这在开发时很有用，因为它允许在访问页面时使用后缀，例如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout提供了开发人员可能感兴趣的布局信息。

* 为确保性能和安全性，请在生产实例上禁用。

**Day CQ WCM过滤器** 配置：

* **WCM模式** 以定义默认模式。
* 在创作实例上，此模式可以是 `edit`， `disable,preview`，或 `analytics`.
其他模式可从sidekick或后缀访问 `?wcmmode=disabled` 可用于模拟生产环境。

* 在发布实例上，此模式必须设置为 `disabled` 以确保没有其他模式可访问。

>[!NOTE]
>
>如果您在中运行AEM，则会自动为生产实例配置此设置 [生产就绪模式](/help/sites-administering/production-ready.md).

**Day CQ WCM链接检查器配置器** 配置：

* **重写配置列表** 为基于内容的链接检查器配置指定位置列表。 这些配置可以基于运行模式。 这一事实对于区分创作环境和发布环境非常重要，因为链接检查器设置可能有所不同。

**Day CQ WCM页面管理器工厂** 配置：

* **页面子树激活检查** 用户（没有复制权限）删除或移动页面（即使页面未激活）。

**Day CQ WCM页面处理器** 配置：

* **路径**，即系统在触发之前侦听页面修改的位置列表 `jcr:Event`.

**Adobe页面展示次数跟踪器** 对于创作实例，请配置如下：

* **sling.auth.requirements**：将此属性的值设置为 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此配置允许向跟踪服务发出匿名请求。

>[!NOTE]
>
>参见 [页面展示次数](/help/sites-deploying/configuring.md#enabling-page-impressions) 了解更多信息。

**Day CQ WCM页面统计信息** 对于发布实例，请配置：

* **用于发送数据的URL** 配置用于跟踪页面统计信息的URL（在跟踪器请求通过Dispatcher时至关重要）；例如，默认为 `https://localhost:4502/libs/wcm/stats/tracker`.

* **已启用跟踪脚本** 以启用( `true`)或禁用( `false`)在页面上包含跟踪脚本。 默认值为 `false`。

>[!NOTE]
>
>参见 [页面展示次数](/help/sites-deploying/configuring.md#enabling-page-impressions) 了解更多信息。

**Day CQ WCM版本管理器** 控制是否在系统中管理版本以及管理版本的方式：

* **激活时创建版本**，在标准安装中启用
* **启用清除**

* **清除路径**，搜索操作搜索的路径。
* **隐式版本控制路径**：隐式版本控制处于活动状态的路径。

* **最大版本期限**，版本的最大保留时间（以天为单位）

* **最大版本数**，保留的最大版本数

参见 [版本清除](/help/sites-deploying/version-purging.md) 了解更多信息。

**Day CQ工作流电子邮件通知服务** 为工作流发送的通知配置电子邮件设置。

**CQ重写器HTML解析器工厂**

控制CQ重写器的HTML解析器。

* **要处理的其他标记**  — 您可以添加或删除要由解析器处理的HTML标记。 默认情况下，将处理以下标记：A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD。
* **保留驼峰式大小写**  — 默认情况下，HTML解析器以驼峰式大小写转换属性(例如， `eBay`)转换为小写(例如， `ebay`)。 您可以关闭此设置以保留驼峰式大小写属性。 当使用前端框架(如Angular2)时，此设置很有用。

**Day Commons JDBC连接池** 配置对用作内容源的外部数据库的访问权限。

工厂配置，因此可以配置多个实例。

**CDN重写器** 必须确保AEM和CDN之间的通信，以便以安全的方式将资产/二进制文件交付给最终用户。 此过程涉及以下两项任务：

* 首次通过CDN从AEM访问资源（或在缓存中资源过期后）。
* 安全地访问CDN中缓存的资源。 在CDN中缓存资源后，该请求不会转到AEM，并且所有有权访问该资源的用户都应从CDN提供服务。

AEM提供了一个重写器，用于将内部资产URL重写为外部CDN URL。 它重写要传递到CDN的链接，包括JWS签名和过期时间，以允许安全地访问资产。 此功能将用于创作实例。

整体流程如下：

1. 用户通过AEM进行身份验证，并请求包含资产的页面。
1. 请求的页面包含与类似的资源 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重写器将链接转换为包含JWS签名的CDN URL：
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然后，用户的浏览器将资产请求转发到CDN服务器
1. AEM CDN应配置为将请求与 `cdn_sign` 参数。
1. 身份验证处理程序验证 `cdn_sign` 参数并将资产返回到CDN，然后将其交付给用户

可以如下所示显示用户浏览器、CDN和AEM之间的流量。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能仅对AEM创作实例启用。

**CDNConfigServiceImpl** 提供CDN配置

CDN重写功能可以通过提供 **CDN分发域名** com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的配置中。

该服务还包含其他配置选项，如启用/禁用CDN重写、执行CDN重写的路径前缀、TTL值和协议（HTTP或HTTPS）。

**CDNRewriter** 用于将内部图像URL重写为CDN URL的重写器

此 **标记属性** 可以定义com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的值，以便只重写选择性图像链接。
