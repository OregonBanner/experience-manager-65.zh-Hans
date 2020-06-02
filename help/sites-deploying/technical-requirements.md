---
title: 技术要求
seo-title: 技术要求
description: AEM支持的客户端和服务器平台的列表。
seo-description: AEM支持的客户端和服务器平台的列表。
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: f16c25468418b6f228132e9d06017d32466cf43a
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 1%

---


# 技术要求{#technical-requirements}

Adobe在平台上支持Adobe Experience Manager(AEM)，详情请见本文档的以下信息。

有关与平台相关的任何问题，请与平台供应商联系。

>[!NOTE]
>
>根据您安装AEM的平台，可能会有不同的用户管理要求集。

## 前提条件 {#prerequisites}

安装Adobe Experience Manager的最低要求：

* 已安装Java Platform、Standard Edition JDK或其他支持的 [Java虚拟机](#java-virtual-machines)
* Experience Manager Quickstart文件（独立JAR或Web应用程序部署WAR）

### 最小规模要求 {#minimum-sizing-requirements}

运行Adobe Experience Manager的最低要求：

* 安装目录中有5 GB可用磁盘空间
* 2 GB内存

>[!NOTE]
>
>* 数字资产使用案例需要更多基本内存。 有关详 [细信息，请参阅](/help/sites-deploying/deploy.md#default-local-install) “部署和维护”。
>* [AEM Forms加载项包需要](/help/forms/using/installing-configuring-aem-forms-osgi.md) 15 GB临时空间。
>



有关详细信息，请参阅硬 [件大小调整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支持级别 {#support-levels}

此文档列表Adobe Experience Manager支持的客户端和服务器平台。 Adobe提供多种支持级别，包括推荐配置和其他配置。

### 支持的配置 {#supported-configurations}

Adobe建议这些配置并作为标准软件维护协议的一部分提供全面支持。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>答： 支持</strong></td>
   <td>Adobe为此配置提供全面支持和维护。 此配置由Adobe的质量保证流程涵盖。</td>
  </tr>
  <tr>
   <td><strong>R: 受限支持</strong></td>
   <td>为确保我们的客户项目成功，Adobe在受限的支持项目内提供全面支持，这要求满足特定条件。 R级支持需要Adobe正式的客户请求和确认。 有关详细信息，请与Adobe客户关怀部门联系。</td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z: 不支持** | 不支持此配置。 Adobe不对配置是否有效发表任何声明，也不支持配置。 |

## 支持的平台 {#supported-platforms}

### Java虚拟机 {#java-virtual-machines}

该应用程序需要运行Java虚拟机，该虚拟机由Java开发工具包(JDK)分发提供。

Adobe Experience Manager可运行以下版本的Java虚拟机：

>[!CAUTION]
>
>建议跟踪Java供应商的安全公告，以确保生产环境的安全和安全，并安装最新的Java更新。

<table>
 <tbody>
  <tr>
   <td>平台</td>
   <td>支持级别<br /> </td>
  </tr>
  <tr>
   <td>Oracle Java SE 12 JDK [1]</td>
   <td>Z: 不支持 </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64位</strong></td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK [1]</td>
   <td>Z: 不支持 </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK [1]</td>
   <td>Z: 不支持</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64位</td>
   <td>答： 支持[3]</td>
  </tr>
  <tr>
   <td>IBM J9 VM —— 内部版本2.9,JRE 1.8.0 [2]</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>IBM J9 VM —— 内部版本2.8,JRE 1.8.0 [2]</td>
   <td>答： 支持</td>
  </tr>
 </tbody>
</table>

1. Oracle 已经转向 Oracle Java SE 产品的“长期支持”(LTS) 模型。Java 9, Java 10, and Java 12 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). 要在生产环境中部署AEM,Adobe仅提供对Java LTS版本的支持。

1. IBM JRE仅与WebSphere Application Server一起受支持。
1. Adobe将直接支持所有使用Oracle Java SE技术的AEM客户支持Oracle Java SE JDK的支持和分发，包括在公共更新结束后对LTS版本的所有维护更新。 有关详 [细信息，请参阅Adobe Experience Manager问题与答案的Oracle](assets/adobe-oracle-java-license-agreement.pdf) Java支持。

### 存储和持久性 {#storage-persistence}

存在各种选项来部署Adobe Experience Manager的存储库。 有关支持的技术和列表选项，请参阅以下存储。

| **平台** | **描述** | **支持级别** |
|---|---|---|
| **具有TAR文件1的文件[系统&#x200B;]** | 存储库 | 答： 支持 |
| **带有Datastore 1的文件[系统&#x200B;]** | 二进制文件 | 答： 支持 |
| 在文件系统1的TAR文件中存储二进制文 [件] | 二进制文件 | Z: 不支持生产 |
| Amazon S3 | 二进制文件 | 答： 支持 |
| Microsoft Azure Blob存储 | 二进制文件 | 答： 支持 |
| MongoDB Enterprise 4.0 | 存储库 | 答： 支 [持2、3] |
| MongoDB Enterprise 3.6 | 存储库 | Z: 不支持 |
| MongoDB Enterprise 3.4 | 存储库 | Z: 不支持 |
| IBM DB2 10.5 | 存储库和表单数据库 | R: 受限支持 [4] |
| Oracle Database 12c(12.1.x) | 存储库和表单数据库 | R: 受限支持 |
| Microsoft SQL Server 2016 | 表单数据库 | 答： 支持 |
| **Apache Lucene（Quickstart内置）** | 搜索服务 | 答： 支持 |
| 阿帕奇索尔 | 搜索服务 | 答： 支持 |

1. “文件系统”包括符合POSIX的块存储。 这包括网络存储技术。 请注意，文件系统性能可能会有所不同，并影响总体性能。 建议将AEM与网络／远程文件系统一起加载测试。
1. AEM不支持MongoDB共享。
1. 仅支持MongoDB存储引擎WiredTiger。
1. 支持AEM Forms升级客户。 不支持新安装。

>[!NOTE]
>
>有关 [AEM Communities](/help/communities/deploy-communities.md) 功能的其他信息，请参阅部署社区。

>[!NOTE]
>
>MongoDB是第三方软件，不包含在AEM授权许可包中。 有关详细信息，请参 [阅MongoDB授权策略](https://www.mongodb.org/about/licensing/) 页。
>
>为了充分利用MongoDB的AEM部署，Adobe建议授权许可MongoDB企业版以从专业支持中受益。 有关详 [细信息](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) ，请参阅推荐的部署。
>
>该许可证包含一个标准副本集，该副本集由一个主实例和两个可用于作者或发布部署的辅助实例组成。
>
>如果要在MongoDB上运行作者和发布，则需要购买两个单独的许可证。
>
>Adobe客户关怀将协助解决与在AEM中使用MongoDB相关的资格问题。
>
>有关详细信息，请参 [阅MongoDB for Adobe Experience Manager页](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

>[!NOTE]
>
>上面列出的受支持的关系数据库是第三方软件，不包含在AEM授权许可包中。
>
>要使用受支持的关系数据库运行AEM 6.5，需要与数据库供应商签订单独的支持合同。 Adobe客户关怀将帮助确定与在AEM 6.5中使用关系数据库相关的问题。
>
>**AEM 6.5的Level-R中当前支持大多数关系项目库，它附带支持标准和支持，如上面的Level-R说明中所述。**

### Servlet引擎／应用程序服务器 {#servlet-engines-application-servers}

Adobe Experience Manager可以作为独立服务器（快速入门JAR文件）或作为第三方应用程序服务器（WAR文件）中的Web应用程序运行。

Servlet 3.1要求的最低Servlet API版本

| 平台 | 支持级别 |
|---|---|
| **快速启动内置Servlet引擎(Jetty 9.4)** | 答： 支持 |
| Oracle WebLogic Server 12.2(12cR2) | Z: 不支持 |
| IBM WebSphere Application Server Continuous投放(LibertyProfile)，带Web用户档案7.0和IBM JRE 1.8 | R: 对新合同的限制支 [持2] |
| IBM WebSphere Application Server 9.0和IBM JRE 1.8 | R: 对新合同的限制支 [持] 1 [2] |
| Apache Tomcat 8.5.x | R: 对新合同的限制支 [持2] |
| JBoss EAP 7.2.x（带JBoss应用程序服务器） | Z: 不支持 |
| JBoss EAP 7.1.4（带JBoss应用程序服务器） | R: 对新合同的限制支 [持] 1 [2] |
| JBoss EAP 7.0.x（带JBoss应用程序服务器） | Z: 不支持 |

1. 建议用于AEM Forms部署。
1. 在应用程序服务器上启动AEM 6.5部署将转向受限支持。 现有客户可升级到AEM 6.5并继续使用应用程序服务器。 对于新客户，它附带支持标准和支持项目，如上面的R级说明所述。

### 服务器操作系统 {#server-operating-systems}

Adobe Experience Manager可与以下针对生产环境的服务器平台结合使用：

| **平台** | **支持级别** |
|---|---|
| **Linux，基于Red Hat分发** | 答： 支 [持][1 3] |
| Linux，基于Debian分发，包括 乌本图 | 答： 支持的 [2] |
| Linux，基于SUSE分发 | 答： 支持 |
| Microsoft Windows Server 2019 [4] | R: 对新合同的限制支持 |
| Microsoft Windows Server 2016 [4] | R: 对新合同的限制支 [持5] |
| Microsoft Windows Server 2012 R2 | Z: 不支持 |
| Oracle Solaris 11 | Z: 不支持 |
| IBM AIX 7.2 | Z: 不支持 |

1. Linux内核2.6、3.x和4.x包含Red Hat分发的衍生产品，包括Red Hat Enterprise Linux、CentOS、Oracle Linux和Amazon Linux。 仅CentOS 7和Red Hat Enterprise Linux 7支持AEM表单加载项功能。
1. AEM Forms仅在Ubuntu 16.04 LTS上受支持
1. Adobe Managed Services支持的Linux分发
1. 升级到6.5的客户支持Microsoft Windows生产部署，并且无生产使用。 AEM Sites和Assets的新部署可应要求提供。
1. Microsoft Window Server支持AEM Forms，但不受支持级别R限制

### 虚拟和云计算环境 {#virtual-cloud-computing-environments}

支持在云计算环境(如Microsoft Azure和Amazon Web Services(AWS))上的虚拟机中运行Adobe Experience Manager，符合本页列出的技术要求并符合Adobe的标准支持条款。

Adobe建议使用Adobe Managed Services在Azure或AWS上部署AEM。 Adobe Managed Services为专家提供在这些云计算环境中部署和操作AEM的经验和技能。 请参 [阅有关Adobe Managed Services的其他文档](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)。

在Azure或AWS或任何其他云计算环境上部署AEM的所有其他情况下，将根据本页所列的技术规范，将Adobe对虚拟计算环境的支持包含在虚拟计算环境中。 与任何这些云环境中运行的AEM相关的任何报告问题都需要独立于特定于云计算环境的任何云服务进行可复制，除非云服务作为本页所列技术要求(例如Azure Blob存储或AWS S3)的一部分得到特别支持。

有关如何在Azure或AWS上部署AEM的建议，请在Adobe Managed Services之外，Adobe强烈建议直接与云提供商或Adobe合作伙伴合作，在您选择的云环境中支持AEM的部署。 选定的云提供商或合作伙伴将负责架构的规模规范、设计和实施。以满足您的特定性能、负载、可扩展性和安全要求。

### 调度程序平台（Web服务器） {#dispatcher-platforms-web-servers}

调度程序是缓存和负载平衡组件。 [下载最新的Dispatcher版本](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)。 Experience Manager 6.5需要Dispatcher版本4.3.2或更高版本。

支持以下Web服务器与Dispatcher 4.3.2版一起使用：

| 平台 | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** [1,2] | 答： 支持 |
| Microsoft IIS 10(Internet Information Server) | 答： 支持 |
| Microsoft IIS 8.5(Internet Information Server) | Z: 不支持 |

1. 基于Apache httpd源代码构建的Web服务器将具有与其所基于的httpd版本相同的支持级别。 如果有疑问，请向Adobe咨询，以确认与相应服务器产品相关的支持级别。 以下情况：

   1. HTTP服务器是仅使用Apache源正式分发或
   1. HTTP服务器作为运行它的操作系统的一部分进行传送。 示例： IBM HTTP Server、Oracle HTTP Server

1. Dispatcher不适用于Windows操作系统的Apache 2.4.x。

## 支持的客户端平台 {#supported-client-platforms}

### 支持创作用户界面的浏览器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager用户界面可用于以下客户端平台。 所有浏览器都使用默认的插件和加载项集进行测试。

AEM用户界面针对大屏幕（通常是笔记本和台式计算机）和平板电脑外形（如Apple iPad或Microsoft Surface）进行了优化。 不支持手机外形。

>[!NOTE]
>
>**支持发布周期快的浏览器：**
>
>Mozilla Firefox、Google Chrome和Microsoft Edge版本每几个月更新一次。 Adobe承诺为Adobe Experience Manager提供更新，以保持以下支持级别，即这些浏览器即将推出的版本。

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>UI支持<br /> </strong></td>
   <td><strong>经典UI支持</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome(Evergreen)</strong></td>
   <td>答： 支持</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>Microsoft Edge(Evergreen)</td>
   <td>答： 支持</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: 不支持</td>
   <td>Z: 不支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>答： 支持</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox最后一个ESR [1]</td>
   <td>答： 支持</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari(Evergreen)</td>
   <td>答： 支持</td>
   <td>答： 支持</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari 11.x</td>
   <td>Z: 不支持</td>
   <td>Z: 不支持</td>
  </tr>
  <tr>
   <td>iOS 12.x上的Apple Safari</td>
   <td>答： 支持[2]</td>
   <td>Z: 不支持</td>
  </tr>
  <tr>
   <td>iOS 11.x上的Apple Safari</td>
   <td>Z: 不支持</td>
   <td>Z: 不支持</td>
  </tr>
 </tbody>
</table>

1. Firefox长期支持版本了 [解有关此内容的更多信息，请访问mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. 支持Apple iPad

### 支持的网站浏览器 {#supported-browsers-for-websites}

通常，AEM Sites渲染的网站的浏览器支持取决于AEM页面模板、设计和组件输出的实现，因此由实施这些部分的一方控制。

### WebDAV客户端 {#webdav-clients}

**Microsoft Windows 7+**

要成功与Microsoft Windows 7+连接到未通过SSL保护的AEM实例，必须在Windows中启用通过不安全网络进行的基本身份验证。 这需要在WebClient的Windows注册表中进行更改：

1. 找到注册表子项：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更大值将BasicAuthLevel注册表项添加到此子项。

要提高Windows下WebDav客户端的响应性——请参 [阅Microsoft支持KB 2445570](https://support.microsoft.com/kb/2445570)

## 其他平台说明 {#additional-platform-notes}

本节提供有关运行Adobe Experience Manager及其加载项的特别说明和更多详细信息。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager（实例、调度程序）的所有元素都可以安装在IPv4和IPv6网络中。

操作是无缝的，因为不需要特殊配置。 如有必要，您只需使用适合您的网络类型的格式指定IP地址。

这意味着，当需要指定IP地址时，您可以从以下位置（根据需要）进行选择：

* IPv6地址示例 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址示例 `https://123.1.1.4:4502`

* 例如， `https://www.yourserver.com:4502`

* IPv4和IPv6 `localhost` 网络安装的默认情况将被解释为， `https://localhost:4502`

### AEM Dynamic Media Add-on的要求 {#requirements-for-aem-dynamic-media-add-on}

默认情况下，AEM Dynamic Media处于禁用状态。 请参阅此处 [启用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)。

启用Dynamic Media后，将适用以下附加技术要求。

>[!NOTE]
>
>仅当您使 **用** Dynamic Media —— 混合模式时，这些系统要求才适用； Dynamic Media —— 混合模式具有嵌入式图像服务器，该服务器仅在某些操作系统上得到认证。
>
>对于运行Dynamic Media - Scene7模式(即dynamicmedia_scene7 **运行模式** )的Dynamic Media客户，没有其他系统要求； 系统要求与AEM相同。 Dynamic Media - Scene7模式体系结构使用基于云的图像服务，而不是嵌入在AEM中的服务。

#### 硬件 {#hardware}

以下硬件要求适用于Linux和Windows:

* 至少具有4个内核的Intel Xeon或AMD Opteron CPU
* 至少16 GB内存

#### Linux {#linux}

如果您在Linux上使用Dynamic Media，则需要满足以下先决条件：

* RedHat Enterprise 7或CentOS 7及更高版本以及最新的修补程序
* 64位操作系统
* 交换已禁用（建议）
* 禁用SELinux（请参阅以下注意事项）

>[!NOTE]
>
>如果设置区域设置为LC_CTYPE不等于，则 `en_US.UTF-8`会阻止Dynamic Media工作。 在命令提示符下查看其值是什么。 如果未设置为此值，请在运行AEM之前键入“export LC_CTYPE=”将LC_CTYPE环境变量设置为空字符串。

>[!NOTE]
>
>**禁用SELinux:** 打开SELinux时图像服务不工作。 此选项默认处于启用状态。 要解决此问题，请编 **辑/etc/selinux/config文件** ，并将SELinux值从：
>
>`SELINUX=enforcing` **到** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA架构：** 具有AMD64和Intel EM64T处理器的系统通常配置为非统一内存架构(NUMA)平台，这意味着内核在启动时构建多个内存节点，而不是构建单个内存节点。
>
>该多节点构造可导致在其它节点耗尽之前，一个或多个节点上的内存耗尽。 当内存耗尽时，内核可决定终止进程（例如，映像服务器或平台服务器），即使内存可用。
>
>因此，Adobe建议您运行这样的系统，以便使用numa=off引导选项关 **闭NUMA** ，以避免内核杀死这些进程。

>[!NOTE]
>
>**服务器主机名必须解析：** 确保服务器的主机名可解析为IP地址。 如果这不可能，请将完全限定的主机名和IP地址添 **加到/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 交换空间至少等于物理内存(RAM)量的两倍

要在Windows上使用Dynamic Media，请为x64和x86安装Microsoft Visual Studio 2010、2013和2015可再发行版。

对于Windows x64:

* 从https://www.microsoft.com/en-us/download/details.aspx?id=13523获取Microsoft Visual Studio 2010可再分发版 [本](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* 获取Microsoft Visual Studio 2013可再发行版，网址为 [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 从https://www.microsoft.com/en-us/download/details.aspx?id=48145获取Microsoft Visual Studio 2015可再分发版 [本](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

对于Windows x86:

* 从https://www.microsoft.com/en-in/download/details.aspx?id=5555获取Microsoft Visual Studio 2010可再分发版 [本](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* 获取Microsoft Visual Studio 2013可再发行版，网址为 [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 从https://www.microsoft.com/en-us/download/details.aspx?id=52685获取Microsoft Visual Studio 2015可再分发版 [本](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### MacOS {#macos}

* 10.9.x及更高版本
* 仅支持试用和演示目的

### AEM Forms PDF Generator的要求 {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>支持的转换为PDF的格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017经典音轨</a> ，最新版本</td>
   <td>XPS，图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、TIF、 PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator仅支持支持的操作系统和应用程序的英语、法语、德语和日语版本。
>
>此外：
>
>* PDF Generator需要32位版本的 [Acrobat 2017经典音轨版本17.011.30078或更高版本](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) ，才能执行转换。
>* PDF Generator仅支持Microsoft Office Professional Plus的32位零售版以及转换所需的其他软件。
>* PDF Generator不支持Microsoft Office 365。
>* 仅Windows和Linux支持OpenOffice的PDF Generator转换。
>* OCR PDF、优化PDF和导出PDF功能仅在Windows上受支持。
>* 某个版本的Acrobat与AEM Forms捆绑在一起，以启用PDF Generator功能。 在AEM Forms许可证的期限内，只能通过AEM Forms以编程方式访问捆绑版本，以便与AEM Forms PDF Generator一起使用。 有关详细信息，请参阅AEM Forms产品说明([按部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)[或Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
   >
   >
* PDF Generator服务不支持Microsoft Windows 10。
>



### 对AEM Assets XMP元数据回写的要求 {#requirements-for-aem-assets-xmp-metadata-write-back}

支持XMP回写并支持以下平台和文件格式：

* **操作系统：**

   * Linux（64位系统上支持32位和32位应用程序）。 有关安装32位客户端库的步骤，请参 [阅如何在64位RedHat Linux上启用XMP提取和回写](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。

   * Windows Server
   * Mac OS X（64位）

* **文件格式**: JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM资产在Linux上处理大量元数据资产的要求 {#assetsonlinux}

XMPFilesProcessor进程需要库GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux内核，例如Linux内核版本3.1.x。 它改进了处理包含大量元数据（如PSD文件）的资产的性能。 使用GLIBC的先前版本会导致日志中出现错误，以开始 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`。
