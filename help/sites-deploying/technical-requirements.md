---
title: 技术要求
seo-title: Technical Requirements
description: AEM支持的客户端和服务器平台列表。
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 72ed4ceee560839c6573461cb5d4d6cbccfd696f
workflow-type: tm+mt
source-wordcount: '3525'
ht-degree: 1%

---

# 技术要求{#technical-requirements}

Adobe在平台上支持Adobe Experience Manager(AEM)，如本文档中的以下信息所述。

如果遇到与平台特别相关的问题，请联系平台供应商。

>[!NOTE]
>
>根据您安装AEM的平台，用户管理要求可能会有不同的组。

## 前提条件 {#prerequisites}

安装Adobe Experience Manager的最低要求：

* 已安装的Java平台、标准版JDK或其他受支持的 [Java虚拟机](#java-virtual-machines)
* Experience Manager快速入门文件（独立JAR或Web应用程序部署WAR）

### 最低大小要求 {#minimum-sizing-requirements}

运行Adobe Experience Manager的最低要求：

* 安装目录中有5 GB可用磁盘空间
* 2 GB内存

>[!NOTE]
>
>* 数字资产用例需要更多基本内存。 请参阅 [部署和维护](/help/sites-deploying/deploy.md#default-local-install) 以了解详细信息。
>* [AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md) 需要15 GB的临时空间。
>


有关详细信息，请参阅 [硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md).

### 支持级别 {#support-levels}

本文档列出了Adobe Experience Manager支持的客户端和服务器平台。 Adobe为建议的配置和其他配置提供了多个级别的支持。

### 支持的配置 {#supported-configurations}

Adobe建议这些配置，并作为标准软件维护协议的一部分提供完全支持。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支持</strong></td>
   <td>Adobe对此配置提供完全支持和维护。 此配置由Adobe的质量保证流程涵盖。</td>
  </tr>
  <tr>
   <td><strong>R:受限支持</strong></td>
   <td>为确保客户项目成功，Adobe在受限支持计划中提供全面支持，该计划要求满足特定条件。 R级支持需要正式的客户请求和Adobe确认。 有关更多信息，请联系Adobe客户关怀团队。</td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z:不支持** | 不支持配置。 Adobe不会就配置是否正常进行任何声明，也不支持配置。 |

## 支持的平台 {#supported-platforms}

### Java虚拟机 {#java-virtual-machines}

应用程序需要运行Java虚拟机，该虚拟机由Java开发工具包(JDK)分发提供。

Adobe Experience Manager使用以下版本的Java虚拟机：

>[!CAUTION]
>
>建议跟踪Java供应商提供的安全公告，以确保生产环境的安全和安全，并安装最新的Java更新。

| **平台** | **支持级别** | **链接** |
|---|---|---|
| OracleJava SE 11 JDK - 64位 | 答：支持 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| OracleJava SE 10 JDK | Z:不支持 `[1]` |
| OracleJava SE 9 JDK | Z:不支持 `[1]` |
| OracleJava SE 8 JDK - 64位 | 答：支持 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM — 内部版本2.9、JRE 1.8.0 | 答：支持 `[2]` |
| IBM J9 VM — 内部版本2.8、JRE 1.8.0 | 答：支持 `[2]` |
| Azul Zulu OpenJDK 11 - 64位 | 答：支持 `[3]` |  |
| Azul Zulu OpenJDK 8 - 64位 | 答：支持 `[3]` |  |

1. Oracle 已经转向 Oracle Java SE 产品的“长期支持”(LTS) 模型。Java 9、Java 10和Java 12是按Oracle划分的非LTS版本(请参阅 [OracleJava SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html))。 要在生产环境中部署AEM,Adobe仅支持LTS版本的Java。 Adobe将直接为所有使用OracleJava SE技术的AEM客户支持和分发OracleJava SE JDK，包括公共更新结束后对LTS版本进行的所有维护更新。 请参阅 [适用于Adobe Experience Manager的Java支持策略](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 以了解更多信息。


1. IBM JRE仅与WebSphere Application Server一起受支持。

1. 从版本6.5 SP9开始，本地AEM部署支持Azul OpenJDK LTS版本。 我们的客户必须直接从Azul获得对Azul JDK LTS版本的支持和分发许可。


### 存储和持久性 {#storage-persistence}

部署Adobe Experience Manager存储库时存在多种选项。 有关支持的技术和存储选项，请参阅以下列表。

| **平台** | **描述** | **支持级别** |
|---|---|---|
| **具有TAR文件的文件系统** `[1]` | 存储库 | 答：支持 |
| **具有数据存储的文件系统** `[1]` | 二进制文件 | 答：支持 |
| 将二进制文件存储在文件系统上的TAR文件中 `[1]` | 二进制文件 | Z:不支持生产 |
| Amazon S3 | 二进制文件 | 答：支持 |
| Microsoft Azure Blob Storage | 二进制文件 | 答：支持 |
| MongoDB Enterprise 4.2 | 存储库 | 答：支持 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | 存储库 | Z:不支持 |
| MongoDB Enterprise 3.6 | 存储库 | Z:不支持 |
| MongoDB Enterprise 3.4 | 存储库 | Z:不支持 |
| IBM DB2 10.5 | 存储库和Forms数据库 | R:受限支持 `[5]` |
| Oracle数据库12c(12.1.x) | 存储库和Forms数据库 | R:受限支持 |
| Microsoft SQL Server 2016 | Forms数据库 | 答：支持 |
| **Apache Lucene（Quickstart内置）** | 搜索服务 | 答：支持 |
| Apache Solr | 搜索服务 | 答：支持 |

1. “文件系统”包括符合POSIX的块存储。 这包括网络存储技术。 请注意，文件系统性能可能会有所不同，并会影响整体性能。 建议将测试AEM与网络/远程文件系统结合加载。
1. MongoDB Enterprise 4.2至少需要AEM 6.5 SP9。
1. AEM不支持MongoDB Sharding。
1. 仅支持MongoDB Storage Engine WiredTiger。
1. 支持AEM Forms升级客户。 新安装不支持。

>[!NOTE]
>
>请参阅 [部署社区](/help/communities/deploy-communities.md) 有关AEM Communities功能的其他信息。

>[!NOTE]
>
>MongoDB是第三方软件，未包含在AEM授权包中。 有关详细信息，请参阅 [MongoDB许可策略](https://www.mongodb.org/about/licensing/) 页面。
>
>为了充分利用MongoDB的AEM部署，Adobe建议授权MongoDB企业版以从专业支持中受益。 请参阅 [推荐的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 以了解更多信息。
>
>该许可证包含一个标准副本集，该副本集由一个主实例和两个辅助实例组成，这两个实例可用于创作或发布部署。
>
>如果要在MongoDB上同时运行创作和发布，则需要购买两个单独的许可证。
>
>Adobe客户关怀团队将协助确定与将MongoDB与AEM结合使用相关的问题。
>
>有关更多信息，请参阅 [用于Adobe Experience Manager的MongoDB页](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>上面列出的受支持的关系数据库是第三方软件，不包含在AEM授权包中。
>
>要使用受支持的关系数据库运行AEM 6.5，需要与数据库供应商签订单独的支持合同。 Adobe客户关怀团队将帮助确定与AEM 6.5中的关系数据库的使用相关的问题。
>
>**AEM 6.5的Level-R中当前支持大多数关系数据库，该Level-R中附带支持标准和支持计划，如上面Level-R描述中所述。**

### Servlet引擎/应用程序服务器 {#servlet-engines-application-servers}

Adobe Experience Manager可以作为独立服务器（快速入门JAR文件）运行，也可以作为第三方应用程序服务器（WAR文件）中的Web应用程序运行。

所需的Servlet API最低版本为Servlet 3.1

| 平台 | 支持级别 |
|---|---|
| **快速入门内置Servlet引擎(Jetty 9.4)** | 答：支持 |
| OracleWebLogic Server 12.2(12cR2) | Z:不支持 |
| IBM WebSphere Application Server连续交付(LibertyProfile)，带有Web Profile 7.0和IBM JRE 1.8 | R:限制对新合同的支持 `[2]` |
| IBM WebSphere Application Server 9.0和IBM JRE 1.8 | R:限制对新合同的支持 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R:限制对新合同的支持 `[2]` |
| JBoss EAP 7.2.x与JBoss应用程序服务器 | Z:不支持 |
| JBoss EAP 7.1.4，带JBoss应用程序服务器 | R:限制对新合同的支持 `[1]` `[2]` |
| JBoss EAP 7.0.x与JBoss应用程序服务器 | Z:不支持 |

1. 建议使用AEM Forms进行部署。
1. 在应用程序服务器上启动AEM 6.5部署时，将变为“受限支持”。 现有客户可以升级到AEM 6.5并继续使用应用程序服务器。 对于新客户，将提供支持标准和支持计划，如上面R级描述中所述。

### 服务器操作系统 {#server-operating-systems}

Adobe Experience Manager可与以下服务器平台配合使用以用于生产环境：

| **平台** | **支持级别** |
|---|---|
| **Linux，基于Red Hat分发** | 答：支持 `[1]` `[3]` |
| Linux，基于Debian分发，包括 乌本图 | 答：支持 `[1]` `[2]` |
| Linux，基于SUSE分发 | 答：支持 `[1]` |
| Microsoft Windows Server 2019 `[4]` | R:限制对新合同的支持 `[5]` |
| Microsoft Windows Server 2016 `[4]` | R:限制对新合同的支持 `[5]` |
| Microsoft Windows Server 2012 R2 | Z:不支持 |
| OracleSolaris 11 | Z:不支持 |
| IBM AIX 7.2 | Z:不支持 |

1. Linux内核2.6、3.x、4.x和5.x包含Red Hat分发版的衍生产品，包括Red Hat Enterprise Linux、CentOS、OracleLinux和Amazon Linux。 AEM Forms附加功能仅在CentOS 7、Red Hat Enterprise Linux 7和Red Hat Enterprise Linux 8上受支持。
1. AEM Forms在Ubuntu 20.04 LTS上受支持。
1. Adobe Managed Services支持的Linux分发。
1. 升级到6.5的客户和非生产用户支持Microsoft Windows生产部署。 新部署是应AEM Sites和Assets的请求进行的。
1. AEM Forms在Microsoft Window Server上不受支持级别R限制。

>[!NOTE]
>
>如果您正在安装AEM Forms 6.5，请确保已安装以下32位Microsoft Visual C++可再发行版。
>
>* Microsoft Visual C++ 2008可再发行
>* Microsoft Visual C++ 2010可再发行
>* Microsoft Visual C++ 2012可再发行
>* Microsoft Visual C++ 2013可再分发（自6.5起）



### 虚拟和云计算环境 {#virtual-cloud-computing-environments}

支持在云计算环境(如Microsoft Azure和Amazon Web Services(AWS))的虚拟机中运行Adobe Experience Manager，以符合本页中列出的技术要求，并且符合Adobe的标准支持条款。

对于云原生环境，请从AEM产品线查看最新的产品：Adobe Experience Manager as a Cloud Service。 请参阅 [Adobe Experience Manager as a Cloud Service文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) 以了解详细信息。

Adobe还提供Adobe Managed Services以在Azure或AWS上部署AEM。 Adobe Managed Services为专家提供了在这些云计算环境中部署和操作AEM的经验和技能。 请参阅 [关于Adobe Managed Services的其他文档](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

在Azure或AWS或任何其他云计算环境上部署AEM的所有其他情况下，将根据本页中列出的技术规范，将从Adobe支持包含在虚拟计算环境中。 与在任何这些云环境中运行的AEM相关的任何报告问题都必须能够独立于特定于云计算环境的任何云服务进行重现，除非云服务是本页中列出的技术要求(例如Azure Blob Storage或AWS S3)的一部分而专门受支持。

有关如何在Adobe Managed Services之外的Azure或AWS上部署AEM的建议，Adobe强烈建议直接与云提供商或Adobe合作伙伴合作，在您选择的云环境中支持部署AEM。 选定的云提供商或合作伙伴将负责架构的大小调整规范、设计和实施，以满足您的特定性能、负载、可扩展性和安全要求。

### 调度程序平台（Web服务器） {#dispatcher-platforms-web-servers}

Dispatcher是缓存和负载平衡组件。 [下载最新的Dispatcher版本](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager6.5需要Dispatcher版本4.3.2或更高版本。

支持将以下Web服务器与Dispatcher版本4.3.2一起使用：

| 平台 | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支持 |
| Microsoft IIS 10(Internet Information Server) | 答：支持 |
| Microsoft IIS 8.5(Internet Information Server) | Z:不支持 |

1. 基于Apache httpd源代码构建的Web服务器将具有与其所基于httpd版本相同的支持级别。 如有疑问，请向Adobe请求确认与相应服务器产品相关的支持级别。 以下情况：

   1. HTTP服务器是仅使用官方的Apache源分发版本构建的，或者
   1. HTTP服务器作为运行该服务器的操作系统的一部分进行传送。 示例：IBM HTTP Server，OracleHTTP Server

1. Dispatcher不适用于适用于Windows操作系统的Apache 2.4.x。

## 支持的客户端平台 {#supported-client-platforms}

### 用于创作用户界面的支持的浏览器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager用户界面适用于以下客户端平台。 所有浏览器均使用一组默认的插件和加载项进行测试。

AEM用户界面针对大屏幕（通常是笔记本电脑和台式计算机）和平板电脑外形(如Apple iPad或Microsoft Surface)进行了优化。 不支持手机外形规格。

>[!NOTE]
>
>**支持发布周期快的浏览器：**
>
>Mozilla Firefox、Google Chrome和Microsoft Edge版本每几个月更新一次。 Adobe承诺提供Adobe Experience Manager更新，以便通过这些浏览器即将推出的版本保持下面所述的支持级别。

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>支持UI<br /> </strong></td>
   <td><strong>支持经典UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome（常绿版）</strong></td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft Edge(Evergreen)</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z:不支持</td>
   <td>Z:不支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox的最后一个ESR [1]</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Apple Safari on macOS（常绿）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x on macOS</td>
   <td>Z:不支持</td>
   <td>Z:不支持</td>
  </tr>
  <tr>
   <td>Apple Safari on iOS 12.x</td>
   <td>答：支持的[2]</td>
   <td>Z:不支持</td>
  </tr>
  <tr>
   <td>Apple Safari on iOS 11.x</td>
   <td>Z:不支持</td>
   <td>Z:不支持</td>
  </tr>
 </tbody>
</table>

1. Firefox的扩展支持版本 [在mozilla.org上了解有关此内容的更多信息](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. 支持Apple iPad

### 支持的网站浏览器 {#supported-browsers-for-websites}

通常，浏览器对AEM Sites呈现的网站的支持取决于AEM页面模板、设计和组件输出的实施，因此由实施这些部分的一方控制。

### WebDAV客户端 {#webdav-clients}

**Microsoft Windows 7+**

要成功与Microsoft Windows 7及更高版本连接到未使用SSL保护的AEM实例，必须在Windows中启用不安全网络上的基本身份验证。 这要求在WebClient的Windows注册表中进行更改：

1. 找到注册表子项：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更多将BasicAuthLevel注册表项添加到此子项。

要提高Windows下WebDav客户端的响应性，请参阅 [Microsoft支持KB 2445570](https://support.microsoft.com/kb/2445570)

## 其他平台说明 {#additional-platform-notes}

本节提供有关运行Adobe Experience Manager及其加载项的特殊说明和更多详细信息。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager的所有元素（实例、调度程序）都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置。 您只需使用适合您网络类型的格式指定IP地址即可（如有必要）。

这意味着当需要指定IP地址时，您可以（根据需要）从以下位置进行选择：

* 例如IPv6地址 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* 例如IPv4地址 `https://123.1.1.4:4502`

* 例如， `https://www.yourserver.com:4502`

* 默认大小写 `localhost` 将解释为IPv4和IPv6网络安装，例如 `https://localhost:4502`

### AEM Dynamic Media附加组件的要求 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media默认处于禁用状态。 请参阅此处 [启用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

启用Dynamic Media后，将应用以下其他技术要求。

>[!NOTE]
>
>这些系统要求 **仅** 使用Dynamic Media — 混合模式时应用；Dynamic Media — 混合模式具有嵌入式图像服务器，该服务器仅在某些操作系统上获得认证。
>
>对于运行Dynamic Media - Scene7模式的Dynamic Media客户(即 **dynamicmedia_scene7** 运行模式)，没有其他系统要求；只有与AEM相同的系统要求。 Dynamic Media - Scene7模式架构使用基于云的图像服务，而不是AEM中嵌入的服务。

#### 硬件 {#hardware}

以下硬件要求适用于Linux和Windows:

* 至少具有4个内核的英特尔至强或AMD皓龙CPU
* 至少16 GB的RAM

#### Linux {#linux}

如果您在Linux上使用Dynamic Media，则需要满足以下先决条件：

* RedHat Enterprise 7或CentOS 7及更高版本，带有最新的修补程序
* 64位操作系统
* 禁用交换（建议）
* 已禁用SELinux（请参阅以下注释）

>[!NOTE]
>
>如果设置了LC_CTYPE不等于 `en_US.UTF-8`，则会阻止Dynamic Media工作。 要在命令提示符下查看其值是什么，请键入“locale”。 如果未将其设置为，请在运行AEM之前，通过键入“export LC_CTYPE=”将LC_CTYPE环境变量设置为空字符串。

>[!NOTE]
>
>**禁用SELinux:** 打开SELinux时，图像提供不起作用。 默认情况下，此选项处于启用状态。 要解决此问题，请编辑 **/etc/selinux/config** 文件，并将SELinux值从：
>
>`SELINUX=enforcing` **到** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA架构：** 具有AMD64和Intel EM64T处理器的系统通常配置为非均匀内存架构(NUMA)平台，这意味着内核在启动时构建多个内存节点，而不是构建单个内存节点。
>
>该多节点构造可导致在其它节点耗尽之前一个或多个节点上的内存耗尽。 当内存耗尽时，内核可能会决定终止进程（例如，图像服务器或平台服务器），即使内存可用。
>
>因此，Adobe建议，如果您运行的系统使用 **numa=off** 引导选项，以避免内核杀死这些进程。

>[!NOTE]
>
>**服务器主机名必须解析：** 确保服务器的主机名可解析为IP地址。 如果无法实现，请将完全限定的主机名和IP地址添加到 **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 交换空间至少等于物理内存(RAM)量的两倍

要在Windows上使用Dynamic Media，请安装适用于x64和x86的Microsoft Visual Studio 2010、2013和2015可再发行版。

对于Windows x64:

* 获取Microsoft Visual Studio 2010的可再发行版本： [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* 获取Microsoft Visual Studio 2013可再发行版本，具体位置为 [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 获取Microsoft Visual Studio 2015可再发行版本，网址为 [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

对于Windows x86:

* 获取Microsoft Visual Studio 2010的可再发行版本： [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* 获取Microsoft Visual Studio 2013可再发行版本，具体位置为 [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 获取Microsoft Visual Studio 2015可再发行版本，网址为 [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x及更高版本
* 仅支持试用和演示目的

### AEM FormsPDF生成器的要求 {#requirements-for-aem-forms-pdf-generator}

### 对PDF生成器的软件支持 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>支持的转换为PDF格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020经典曲目</a> 最新版本</td>
   <td>XPS，图像格式(BMP，GIF,JPEG,JPG, TIF，TIFF, PNG， JPF， JPX， JP2, J2K， J2C， JPC),HTML, HTM， DWG， DXF和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017款经典曲目</a> 最新版本（已弃用）</td>
   <td>XPS，图像格式(BMP，GIF,JPEG,JPG, TIF，TIFF, PNG， JPF， JPX， JP2, J2K， J2C， JPC),HTML, HTM， DWG， DXF和DWF</td>
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
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（已弃用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（已弃用）<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016（已弃用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLS、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JP2、J2K、J2C、JPC、JPC、HTML、HTM和RT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2（已弃用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLS、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JP2、J2K、J2C、JPC、JPC、HTML、HTM和RT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF生成器仅支持受支持操作系统和应用程序的英语、法语、德语和日语版本。
>
>此外：
>
>* PDF生成器需要32位版本的 [Acrobat 2020 Classic跟踪版本20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017版本17.011.30078来执行转换。
>* PDF生成器转换仅在Windows和Linux上受支持。
>* PDF生成器仅支持Microsoft Office Professional Plus的32位零售版本以及在Windows操作系统上进行转换所需的其他软件。
>* PDF生成器支持Linux操作系统上OpenOffice的32位和64位版本。
>* PDF生成器不支持Microsoft Office 365。
>* OCRPDF、Optimize PDF和Export PDF功能仅在Windows上受支持。
>* Acrobat版本与AEM Forms捆绑在一起，以启用PDF生成器功能。 在AEM Forms许可证有效期内，捆绑版本只应通过AEM Forms以编程方式访问，以便与AEM FormsPDF生成器一起使用。 有关更多信息，请参阅根据您的部署对AEM Forms产品进行描述([内部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* PDF生成器服务不支持Microsoft Windows 10。
>* PDF生成器无法使用Microsoft Visio 2019转换文件。 您可以继续使用Microsoft Visio 2016来转换.VSD和.VSDX文件。
>* PDF生成器无法使用Microsoft Project 2019转换文件。 您可以继续使用Microsoft Project 2016来转换.VSD和.VSDX文件。
>


### AEM Forms Designer的要求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
* 支持PAE、NX和SSE2的1 GHz或更快的处理器。
* 1 GB的RAM（32位）或2 GB的RAM（64位操作系统）
* 对于32位或20 GB的磁盘空间，对于64位操作系统，为16 GB的磁盘空间
* 图形内存 — 128 MB的GPU（建议256 MB）
* 2.35 GB可用硬盘空间
* 1024 X 768像素或更高的显示器分辨率
* 视频硬件加速（可选）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
* 安装Designer的管理权限。

### AEM Assets XMP元数据回写的要求 {#requirements-for-aem-assets-xmp-metadata-write-back}

支持并启用以下平台和文件格式的XMP写回：

* **操作系统：**

   * Linux（在64位系统上支持32位和32位应用程序）。 有关安装32位客户端库的步骤，请参阅 [如何在64位RedHat Linux上启用XMP提取和回写](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X（64位）

* **文件格式**:JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux上处理元数据密集型资产的要求 {#assetsonlinux}

XMPFilesProcessor进程需要库GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux内核，例如Linux内核版本3.1.x。它改进了处理包含大量元数据(如PSD文件)的资产的性能。 使用以前版本的GLIBC会导致日志中以 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
