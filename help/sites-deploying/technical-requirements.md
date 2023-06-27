---
title: 技术要求
description: Adobe Experience Manager支持的客户端和服务器平台列表。
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 3b08d5001e7d3c683caa021ecf051f44762bb9ac
workflow-type: tm+mt
source-wordcount: '3526'
ht-degree: 1%

---

# 技术要求{#technical-requirements}

Adobe在这些平台上支持(AEM) Adobe Experience Manager，如本文档中的以下信息中所详述。

有关平台的任何问题，请与平台供应商联系。

>[!NOTE]
>
>根据安装AEM的平台，用户管理可能会有不同的要求集。

## 前提条件 {#prerequisites}

安装Adobe Experience Manager的最低要求：

* 已安装的Java™平台、标准版JDK或其他受支持的 [Java™虚拟机](#java-virtual-machines)
* Experience Manager快速入门文件（独立JAR或Web应用程序部署WAR）

### 最小大小要求 {#minimum-sizing-requirements}

运行Adobe Experience Manager的最低要求：

* 安装目录中的5 GB可用磁盘空间
* 2 GB内存

>[!NOTE]
>
>* 数字资产用例需要更多基本内存。 参见 [部署和维护](/help/sites-deploying/deploy.md#default-local-install) 了解详细信息。
>* [AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md) 需要15 GB的临时空间。
>

欲了解更多信息，请参见 [硬件大小调整准则](/help/managing/hardware-sizing-guidelines.md).

### 支持级别 {#support-levels}

本文档列出了Adobe Experience Manager支持的客户端和服务器平台。 Adobe提供了多个级别的支持，包括推荐的配置和其他配置。

### 支持的配置 {#supported-configurations}

Adobe推荐这些配置，并在标准软件维护协议中提供全面支持。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支持</strong></td>
   <td>Adobe为此配置提供完全支持和维护。 Adobe的质量保证流程涵盖此配置。</td>
  </tr>
  <tr>
   <td><strong>R：受限支持</strong></td>
   <td>为确保客户项目成功，Adobe在有限支持计划内提供全面支持，该计划要求满足特定条件。 R级支持需要正式的客户请求和Adobe确认。 有关更多信息，请联系Adobe客户关怀部门。</td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z：不支持** | 不支持该配置。 Adobe不声明配置是否有效，也不支持配置。 |

## 支持的平台 {#supported-platforms}

### Java™虚拟机 {#java-virtual-machines}

应用程序需要由Java™开发工具包(JDK)分发提供的Java™虚拟机才能运行。

Adobe Experience Manager可与以下版本的Java™虚拟机配合使用：

>[!CAUTION]
>
>跟踪Java™供应商提供的安全公告。 这样做确保了生产环境的安全与保障。 此外，请始终安装最新的Java™更新。

| **Platform** | **支持级别** | **链接** |
|---|---|---|
| oracleJava™ SE 17 JDK | Z：不支持 `[1]` |
| oracleJava™ SE 11 JDK - 64位 | 答：支持 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| oracleJava™ SE 10 JDK | Z：不支持 `[1]` |
| oracleJava™ SE 9 JDK | Z：不支持 `[1]` |
| oracleJava™ SE 8 JDK - 64位 | 答：支持 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9虚拟机 — 内部版本2.9、JRE 1.8.0 | 答：支持 `[2]` |
| IBM® J9虚拟机 — 内部版本2.8、JRE 1.8.0 | 答：支持 `[2]` |
| Azul Zulu OpenJDK 11 - 64位 | 答：支持 `[3]` | |
| Azul Zulu OpenJDK 8 - 64位 | 答：支持 `[3]` | |

1. oracle已转为使用“长期支持”(LTS)模型来OracleJava™ SE产品。 Java™ 9、Java™ 10和Java™ 12是按Oracle划分的非LTS版本(请参阅 [oracleJava™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html))。 要在生产环境中部署AEM，Adobe仅支持Java™的LTS版本。 Adobe直接为所有使用OracleJava™ SE技术的AEM客户支持OracleJava™ SE JDK的支持和分发，包括在公共更新结束之后对LTS版本的所有维护更新。 请参阅 [适用于Adobe Experience Manager的Java™支持策略](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **重要信息：至少支持一直到2026年9月的OracleJava™ 11。 对OracleJava™ 17的支持正在准备中。**

1. IBM® JRE仅与WebSphere®应用程序服务器一起受支持。

1. 从版本6.5 SP9开始，本地AEM部署支持Azul Zulu OpenJDK LTS版本。 Azul Zulu JDK LTS版本的支持和分发必须由Adobe客户直接从Azul授予许可。


### 存储和持久性 {#storage-persistence}

可以使用各种选项来部署Adobe Experience Manager存储库。 请参阅下面的列表，以了解支持的技术和存储选项。

| **Platform** | **描述** | **支持级别** |
|---|---|---|
| **带有TAR文件的文件系统** `[1]` | 存储库 | 答：支持 |
| **具有数据存储的文件系统** `[1]` | 二进制文件 | 答：支持 |
| 将二进制文件存储在文件系统上的TAR文件中 `[1]` | 二进制文件 | Z：不支持生产 |
| Amazon S3 | 二进制文件 | 答：支持 |
| Microsoft® Azure Blob存储 | 二进制文件 | 答：支持 |
| MongoDB Enterprise 4.4 | 存储库 | 答：支持 `[2, 3, 4]` |
| MongoDB Enterprise 4.2 | 存储库 | 答：支持 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | 存储库 | Z：不支持 |
| MongoDB Enterprise 3.6 | 存储库 | Z：不支持 |
| MongoDB Enterprise 3.4 | 存储库 | Z：不支持 |
| IBM® DB2® 10.5 | 存储库和Forms数据库 | R：受限支持 `[5]` |
| oracle数据库12c (12.1.x) | 存储库和Forms数据库 | R：受限支持 |
| Microsoft® SQL Server 2016 | Forms数据库 | 答：支持 |
| **Apache Lucene（快速入门内置）** | 搜索服务 | 答：支持 |
| Apache Solr | 搜索服务 | 答：支持 |

1. “文件系统”包括符合POSIX的块存储。 包括网络存储技术。 请记住，文件系统性能可能会有所不同，并影响整体性能。 使用网络/远程文件系统对AEM进行负载测试。
1. MongoDB Enterprise版本4.2和4.4至少需要AEM 6.5 SP9。
1. AEM不支持MongoDB分片。
1. 仅支持MongoDB存储引擎WiredTiger。
1. 支持AEM Forms升级客户。 新安装不支持。

>[!NOTE]
>
参见 [部署社区](/help/communities/deploy-communities.md) 有关AEM Communities功能的其他信息。

>[!NOTE]
>
MongoDB是第三方软件，未包含在AEM许可包中。 欲了解更多信息，请参见 [MongoDB许可策略](https://www.mongodb.com/community/licensing) 页面。
>
为了利用MongoDB充分利用AEM部署，Adobe建议许可MongoDB企业版以受益于专业支持。 参见 [建议的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 了解更多信息。
>
该许可证包含一个标准副本集，该副本集由一个主实例和两个辅助实例组成，这两个实例可用于创作或发布部署。
>
如果要在MongoDB上同时运行author和publish，则必须购买两个单独的许可证。
>
Adobe客户关怀团队可协助解决与AEM配合使用MongoDB相关的资格确认问题。
>
欲了解更多信息，请参见 [适用于Adobe Experience Manager的MongoDB页](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
上面列出的受支持的关系数据库是第三方软件，未包含在AEM许可包中。
>
要使用受支持的关系数据库运行AEM 6.5，需要与数据库供应商签订单独的支持合同。 Adobe客户关怀团队协助处理与使用AEM 6.5的关系数据库相关的资格确认问题。
>
**目前，大多数关系数据库在AEM 6.5上的R级中受支持，该级别附带支持标准和支持计划，如上面R级说明中所述。**

### Servlet引擎/应用程序服务器 {#servlet-engines-application-servers}

Adobe Experience Manager可以作为独立服务器（快速入门JAR文件）运行，也可以作为第三方应用程序服务器中的Web应用程序（WAR文件）运行。

需要的最低Servlet API版本是Servlet 3.1

| Platform | 支持级别 |
|---|---|
| **快速入门内置Servlet引擎(Jetty 9.4)** | 答：支持 |
| oracleWebLogic Server 12.2 (12cR2) | Z：不支持 |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) with Web Profile 7.0和IBM® JRE 1.8 | R：对新合同的支持受到限制 `[2]` |
| IBM® WebSphere® Application Server 9.0和IBM® JRE 1.8 | R：对新合同的支持受到限制 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R：对新合同的支持受到限制 `[2]` |
| JBoss® EAP 7.2.x带JBoss®应用程序服务器 | Z：不支持 |
| JBoss® EAP 7.1.4带JBoss®应用程序服务器 | R：对新合同的支持受到限制 `[1]` `[2]` |
| JBoss® EAP 7.0.x带JBoss®应用程序服务器 | Z：不支持 |

1. 建议使用AEM Forms进行部署。
1. 在应用程序服务器中启动AEM 6.5部署后，将转为有限支持。 现有客户可以升级到AEM 6.5并继续使用应用程序服务器。 对于新客户，如上面R级描述中所述，它附带了支持标准和支持计划。

### 服务器操作系统 {#server-operating-systems}

Adobe Experience Manager可与以下服务器平台配合使用以用于生产环境：

| **Platform** | **支持级别** |
|---|---|
| **Linux®，基于Red Hat®分发** | 答：支持 `[1]` `[3]` |
| Linux®，基于Debian分布，包括 乌本图 | 答：支持 `[1]` `[2]` |
| Linux®，基于SUSE®分发 | 答：支持 `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R：对新合同的支持受到限制 `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R：对新合同的支持受到限制 `[5]` |
| Microsoft® Windows Server 2012 R2 | Z：不支持 |
| oracleSolaris™ 11 | Z：不支持 |
| IBM® AIX® 7.2 | Z：不支持 |

1. Linux®内核2.6、3。 x， 4. x和5. x包括来自Red Hat® Distribution的派生程序，包括Red Hat® Enterprise Linux®、CentOS、OracleLinux®和Amazon Linux®。 只有CentOS 7、Red Hat® Enterprise Linux® 7、Red Hat® Enterprise Linux® 8和Red Hat® Enterprise Linux® 9支持AEM Forms附加功能。
1. Ubuntu 20.04 LTS支持AEM Forms。
1. Adobe Managed Services支持的Linux®分发。
1. 升级到6.5的客户和非生产使用都支持Microsoft® Windows生产部署。 AEM Sites和Assets的新部署是应请求进行的。
1. Microsoft® Window Server支持AEM Forms，无支持级别R限制。

>[!NOTE]
>
如果要安装AEM Forms 6.5，请确保已安装以下32位Microsoft® Visual C++可再发行版本。
>
* Microsoft® Visual C++ 2008可再分发
* Microsoft® Visual C++ 2010可再分发
* Microsoft® Visual C++ 2012可再分发
* Microsoft® Visual C++ 2013可再分发
* Microsoft® Visual C++ 2019（VC14.28或更高版本）可再分发



### 虚拟和云计算环境 {#virtual-cloud-computing-environments}

支持在云计算环境中的虚拟机中运行Adobe Experience Manager。 这些环境包括Microsoft®Azure和Amazon Web Services (AWS)，它们按照本页中列出的技术要求和Adobe的标准支持条款运行。

对于云原生环境，请查看AEM产品线中的最新产品：Adobe Experience Manager as a Cloud Service。 参见 [Adobe Experience Manager as a Cloud Service文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) 了解详细信息。

Adobe还提供Adobe Managed Services以在Azure或AWS上部署AEM。 Adobe Managed Services为专家提供了在这些云计算环境中部署和操作AEM的经验和技能。 参见 [有关Adobe Managed Services的其他文档](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

在Azure或AWS或任何其他云计算环境中部署AEM的所有其他情况下，Adobe支持都包含在虚拟计算环境中。 该虚拟环境必须按照本页中列出的技术规范运行。 任何与在任何这些云环境中运行的AEM相关的已报告问题都必须可独立于特定于云计算环境的任何云服务进行重现。 也就是说，除非支持将云服务作为本页面上列出的技术要求的一部分，例如Azure Blob Storage或AWS S3。

有关如何在Adobe Managed Services之外的Azure或AWS上部署AEM的建议，Adobe建议直接与云提供商合作。 或者，与支持在您选择的云环境中部署AEM的Adobe合作伙伴合作。 选定的云提供商或合作伙伴负责架构的规模规格、设计和实施，以满足您的特定性能、负载、可扩展性和安全性要求。

### Dispatcher平台（Web服务器） {#dispatcher-platforms-web-servers}

Dispatcher是缓存和负载平衡组件。 [下载最新的Dispatcher版本](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en). Experience Manager6.5需要Dispatcher版本4.3.2或更高版本。

以下Web服务器支持与Dispatcher版本4.3.2一起使用：

| Platform | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支持 |
| Microsoft® IIS 10 (Internet Information Server) | 答：支持 |
| Microsoft® IIS 8.5 (Internet Information Server) | Z：不支持 |

1. 基于Apache httpd源代码构建的Web服务器与其所基于的httpd版本具有同样多的支持。 如有疑问，请要求Adobe确认与相应服务器产品相关的支持级别。 以下情况：

   1. HTTP服务器仅使用官方的Apache源分发生成，或者
   1. HTTP服务器作为运行它的操作系统的一部分提供。 示例： IBM® HTTP Server、OracleHTTP Server

1. Dispatcher不可用于Windows操作系统的Apache 2.4.x。

## 支持的客户端平台 {#supported-client-platforms}

### 用于创作用户界面的受支持的浏览器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager用户界面可与以下客户端平台配合使用。 所有浏览器都使用一组默认的插件和加载项进行测试。

AEM用户界面针对大屏幕（通常是笔记本电脑和台式计算机）和平板电脑外形规格(如Apple iPad或Microsoft® Surface)进行了优化。 不支持电话的外形规格。

>[!NOTE]
>
**支持具有快速发布周期的浏览器：**
>
Mozilla Firefox、Google Chrome和Microsoft® Edge每隔几个月发布一次更新。 Adobe承诺为Adobe Experience Manager提供更新，以在这些浏览器的即将发行版本中保持下述支持级别。

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>支持UI<br /> </strong></td>
   <td><strong>支持经典UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome （常绿）</strong></td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft® Edge （长青）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox （常绿）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox上一个ESR [1]</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari （常青）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari 11.x</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>iOS 12.x上的Apple Safari</td>
   <td>答：支持的[2]</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>iOS 11.x上的Apple Safari</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
 </tbody>
</table>

1. Firefox的扩展支持版本 [在mozilla.org上了解详情](https://www.mozilla.org/en-US/firefox/enterprise/)
1. 支持Apple iPad

### 支持的网站浏览器 {#supported-browsers-for-websites}

通常，浏览器对AEM Sites渲染的网站的支持取决于AEM页面模板的实施、设计和组件输出，因此由实施这些部分的各方控制。

### WebDAV客户端 {#webdav-clients}

**Microsoft® Windows 7+**

在与Microsoft® Windows 7+连接到未使用SSL进行保护的AEM实例时，必须在Windows中启用通过不安全网络进行的基本身份验证。 它需要在WebClient的Windows注册表中进行更改：

1. 找到注册表子项：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更多将BasicAuthLevel注册表项添加到此子项。

## 其他平台说明 {#additional-platform-notes}

本节提供有关运行Adobe Experience Manager及其加载项的特殊说明和更多详细信息。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager的所有元素（实例、Dispatcher）都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置。 如果需要，可以使用适合您的网络类型的格式指定IP地址。

当必须指定IP地址时，您可以根据需要从以下项中选择：

* IPv6地址。 例如，`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址。 例如，`https://123.1.1.4:4502`

* 服务器名称。 例如，`https://www.yourserver.com:4502`

* 默认大小写为 `localhost` 对于IPv4和IPv6网络安装，都会进行解释。 例如，`https://localhost:4502`

### AEM Dynamic Media加载项的要求 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media默认处于禁用状态。 请参阅此处 [启用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

启用Dynamic Media后，将满足以下附加技术要求。

>[!NOTE]
>
这些系统要求 **仅限** 如果您使用Dynamic Media — 混合模式，则应用；Dynamic Media — 混合模式具有嵌入式图像服务器，该服务器仅在特定操作系统上进行认证。
>
适用于运行Dynamic Media - Scene7模式的Dynamic Media客户(即， **dynamicmedia_scene7** 运行模式)，没有其他系统要求；只有与AEM相同的系统要求。 Dynamic Media - Scene7模式架构使用基于云的图像服务，而不是嵌入到AEM中的服务。

#### 硬件 {#hardware}

以下硬件要求适用于Linux®和Windows：

* 至少具有四个内核的英特尔至强®或AMD®皓龙CPU
* 至少16 GB内存

#### Linux® {#linux}

如果您在Linux®上使用Dynamic Media，则必须满足以下先决条件：

* Red Hat® Enterprise 7或CentOS 7及更高版本，带有最新的修复修补程序
* 64位操作系统
* 已禁用交换（推荐）
* 已禁用SELinux（请参阅以下注释）

>[!NOTE]
>
如果设置了locale ，则LC_CTYPE不等于 `en_US.UTF-8`，这会阻止Dynamic Media正常运行。 要查看其值，请在命令提示符下键入“locale”。 如果未正确设置，则在运行AEM之前键入“export LC_CTYPE=”，将LC_CTYPE环境变量设置为空字符串。

>[!NOTE]
>
**禁用SELinux：** 打开SELinux时，图像服务不起作用。 此选项默认处于启用状态。 要解决此问题，请编辑 **/etc/selinux/config** 文件并将SELinux值从以下位置更改：
>
`SELINUX=enforcing` **到** `SELINUX=disabled`

>[!NOTE]
>
**NUMA架构：** 处理器采用AMD64和英特尔® EM64T的系统通常配置为非统一内存架构(NUMA)平台。 也就是说，内核在引导时构建多个内存节点，而不是构建单个内存节点。
>
该多节点结构可导致一个或多个节点上的内存耗尽，而其它节点则被耗尽。 当内存耗尽时，即使存在可用内存，内核也可以决定终止进程（例如，图像服务器或平台服务器）。
>
因此，Adobe建议，如果运行的系统要求您使用关闭NUMA **numa=off** 引导选项，以避免内核终止这些进程。

>[!NOTE]
>
**服务器主机名必须解析：** 确保服务器的主机名可解析为IP地址。 如果无法执行此操作，请将完全限定的主机名和IP地址添加到 **/etc/hosts**：
>
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 交换空间至少相当于物理内存量(RAM)的两倍

要在Windows上使用Dynamic Media，请安装Microsoft®Visual Studio 2010、2013和2015 for x64和x86可再发行软件包。

对于Windows x64：

* 在以下位置获取Microsoft® Visual Studio 2010可再发行软件包： [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* 在以下位置获取Microsoft® Visual Studio 2013可再发行版本： [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 在以下位置获取Microsoft® Visual Studio 2015可再发行软件包： [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

对于Windows x86：

* 在以下位置获取Microsoft® Visual Studio 2010可再发行软件包： [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* 在以下位置获取Microsoft® Visual Studio 2013可再发行版本： [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 在以下位置获取Microsoft® Visual Studio 2015可再发行软件包： [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x及更高版本
* 仅支持试用和演示

### AEM Forms PDF Generator要求 {#requirements-for-aem-forms-pdf-generator}

### PDF生成器的软件支持 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>支持转换为PDF的格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 classic track</a> 最新版本</td>
   <td>XPS、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> 最新版本（已弃用）</td>
   <td>XPS、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016（已弃用）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP 、 WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（已弃用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft®出版商2019<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（已弃用）<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft®项目2016（已弃用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、和TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2（已弃用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、和TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
PDF生成器仅支持所支持的操作系统和应用程序的英语、法语、德语和日语版本。
>
此外，
>
* PDF Generator需要32位版本的 [Acrobat 2020 classic途径20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017版本17.011.30078来执行此转换。
* 仅在Windows和Linux®上支持用于OpenOffice的PDF生成器转换。
* PDF Generator仅支持32位零售版Microsoft® Office Professional Plus以及在Windows操作系统上进行转换所需的其他软件。
* PDF Generator支持Linux®操作系统上的32位和64位版本的OpenOffice。
* PDF Generator不支持Microsoft® Office 365。
* 仅在Windows上支持OCRPDF、Optimize PDF和Export PDF功能。
* Acrobat的一个版本与AEM Forms捆绑在一起，用于启用PDF生成器功能。 在AEM Forms许可证有效期内，仅以编程方式访问AEM Forms的捆绑版本，以用于AEM Forms PDF Generator。 有关更多信息，请参阅根据您的部署确定的AEM Forms产品描述([内部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* PDF Generator服务不支持Microsoft® Windows 10。
* PDF Generator无法使用Microsoft® Visio 2019转换文件。 您可以继续使用Microsoft® Visio 2016进行转换 `.VSD` 和 `.VSDX` 文件。
* PDF Generator无法使用Microsoft® Project 2019转换文件。 您可以继续使用Microsoft® Project 2016进行转换 `.VSD` 和 `.VSDX` 文件。
>

### AEM Forms Designer的要求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
* 1 GHz或更快的处理器，支持PAE、NX和SSE2。
* 32位RAM为1 GB，64位OS为2 GB
* 16 GB的磁盘空间，用于32位或20 GB的磁盘空间，用于64位操作系统
* 图形内存 — 128 MB的GPU（建议使用256 MB）
* 2.35 GB可用硬盘空间
* 1024 X 768像素或更高的显示器分辨率
* 视频硬件加速（可选）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC
* 安装设计器的管理权限
* Microsoft Visual C++ 2019（VC 14.28或更高版本） 32位运行时

### AEM Assets XMP元数据回写要求 {#requirements-for-aem-assets-xmp-metadata-write-back}

以下平台和文件格式支持并启用了XMP回写：

* **操作系统：**

   * Linux®（在64位系统上支持32位和32位应用程序）。 有关安装32位客户端库的步骤，请参阅 [如何在64位Red Hat® Linux®上启用XMP提取和回写](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X（64位）

* **文件格式**：JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux上处理大量元数据的资产的要求® {#assetsonlinux}

XMPFilesProcessor进程需要库GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux®内核，例如Linux®内核版本3.1.x。它提高了处理包含大量元数据的资源(如PSD文件)的性能。 使用以前版本的GLIBC会导致日志中出现错误，开始于 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
