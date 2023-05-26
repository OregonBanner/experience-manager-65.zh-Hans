---
title: AEM Forms on JEE的支持平台
seo-title: Supported Platforms for AEM Forms on JEE
description: 在JEE上安装AEM Forms所需和受支持的基础架构组件列表
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 26e71c5f09eb9fa3f3eda01deb871ac63e348a30
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---


# AEM Forms on JEE的支持平台 {#supported-platforms-for-aem-forms-on-jee}

## 支持的平台 {#supported-platforms}

<div class="preview">

Adobe已发布 [完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) JEE上的AEM 6.5 Forms Service Pack 12 (6.5.12.0)以及修补程序安装程序。 完整安装程序提供对新平台的支持，而修补程序安装程序仅包含错误修复。

如果您正在执行全新安装或计划在JEE环境中使用AEM 6.5 Forms的最新软件，Adobe建议使用 [AEM 6.5.12.0 Forms on JEE完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 2022年3月3日发布，而不是2019年4月8日发布的AEM 6.5 Forms安装程序。

</div>

### 支持级别 {#support-levels}

JEE服务器上的AEM Forms可以使用支持的操作系统、应用程序服务器、数据库、数据库驱动程序、JDK、LDAP服务器和电子邮件服务器的任意组合进行设置。

本文档列出了AEM Forms on JEE支持的客户端和服务器平台。 Adobe为我们推荐的配置和其他配置提供了多个级别的支持。 本文档还列出了其他支持的软件及其版本、例外、修补程序定义以及第三方软件修补程序支持策略。

>[!NOTE]
>
>- 有关受支持的服务器平台的例外情况的完整列表，请参见 [支持的服务器平台例外](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- JEE上的AEM Forms仅支持所支持的操作系统和应用程序的英语、法语、德语和日语版本。


### 建议的配置 {#recommendedconfigurations}

Adobe建议使用这些配置，并在标准软件维护协议中提供完全支持或有限支持：

<table>
 <tbody>
  <tr>
   <th>支持级别</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>答：支持<br /> </td>
   <td>Adobe为此配置提供完全支持和维护。 Adobe的质量保证流程涵盖此配置。</td>
  </tr>
  <tr>
   <td>R：受限支持</td>
   <td>在满足某些先决条件后，Adobe将为此配置提供完全支持。 联系Adobe企业支持部门以了解先决条件并提出支持请求。</td>
  </tr>
  <tr>
   <td>L：有限支持</td>
   <td>在满足某些先决条件后，Adobe将为此配置提供完全支持和维护。 并非所有功能在配置上都可用。 联系Adobe企业支持部门以了解先决条件并提出支持请求。<br /> </td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E：预期工作 | 该配置应可正常工作，但无相反的报告。 |
| Z：不支持 | 不支持该配置。 Adobe不发表任何关于配置是否有效的声明，也不支持配置。 |

>[!NOTE]
>
>为帮助AEM Forms客户降低拥有成本、简化部署架构和使开发栈栈现代化，Adobe Experience Manager企业平台正从基于应用程序服务器的部署转向基于OSGi的独立部署。 Adobe通过减少的基础架构组件列表，继续支持AEM Forms JEE栈栈。
>
>在6.5版本中，我们不再支持使用率最低的客户的基础架构组件，如下所示：
>
>- IBM DB2数据库
>- IBM AIX和Sun Solaris操作系统
>
>对于新安装，建议在可行的情况下，在现代OSGi栈栈上部署AEM Forms，以利用围绕响应式自适应Forms的最新创新，实现使用表单数据模型的移动、多渠道交互式通信以及后端数据集成。
>
>我们认识到现有用户需要继续在JEE栈栈上部署AEM Forms。 在此类情况下，Adobe需要在受支持的基础架构上部署AEM Forms JEE，如本文档中所述。 如果您要升级到AEM 6.5 Forms并在以前的AEM Forms版本上使用不受支持的平台，则可以联系Adobe支持部门以获取有关升级到受支持的平台的帮助。

### Java虚拟机(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms需要由Java开发工具包(JDK)分发提供的Java虚拟机才能运行。 Adobe Experience Manager可与以下版本的Java虚拟机配合使用：

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr> 
   <td><p>oracleJava™ SE 11（64位） <sup> [8] </sup> </p>  </td>
   <td><p>答：支持</p> </td>
   <td><p>次要版本和更新 </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64位</td>
   <td>Z：不支持</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64位</td>
   <td>Z：不支持</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>oracleJava™ SE 8（64位）</td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM® J9虚拟机（内部版本2.9、JRE 1.8.0）IBM® JDK SR6-FP26<br /> </td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM JAVA1.8.0_291（内部版本8.0.6.30）<br /> </td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- 建议跟踪Java供应商的安全公告，以确保生产环境的安全性和安全性，并安装最新的Java更新。
>- JEE上的AEM Forms在生产环境中仅支持64位JVM。


### 数据库和CRX持久性 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> 描述</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
  </tr>
  <tr>
   <td><p>文件系统</p> </td>
   <td><p>存储库微内核（TAR MK文件）</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0（已弃用） </p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>oracle数据库12c版本2 (12.2.0.1.0)（已弃用）</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
   <tr>
   <td>oracle数据库19c(Standard、Real Application Clusters (RAC)和Enterprise版) </td>
   <td>存储库微内核 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016（已弃用）</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1（已弃用）</td>
   <td>存储库微内核</td>
   <td>R：受限支持</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35（已弃用） </td>
   <td>-</td>
   <td>R：受限支持</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R：受限支持</td>
  </tr>
 </tbody>
</table>

- 全新安装不支持IBM DB2。 它仅支持现有客户升级到AEM 6.5 Forms。
- MongoDB是第三方软件，未包含在AEM许可包中。 欲了解更多信息，请参见 [MongoDB许可策略](https://www.mongodb.org/about/licensing/) 页面。
- 为了充分利用AEM部署，Adobe建议许可MongoDB Enterprise版本，以便获得专业支持。
- Adobe客户关怀团队将协助解决与AEM使用MongoDB相关的资格确认问题。 欲了解更多信息，请参见 [适用于Adobe Experience Manager的MongoDB页](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- “文件系统”包括符合POSIX的块存储。 这包括网络存储技术。 请记住，文件系统性能可能会有所不同，并影响整体性能。 建议将AEM与网络/远程文件系统结合使用来进行负载测试。
- 仅支持MongoDB存储引擎WiredTiger。
- AEM不支持MongoDB分片。
- JEE上的AEM Forms不支持MySQL for RDBMK持久性。
- Document Security模块不使用内容存储库。 这意味着，如果您只使用Document Security，并且不打算使用HTML工作区、HTML5表单或自适应表单，则不要安装Content Repository。
- JEE上的AEM Forms不支持使用MySQL来保留AEM存储库(CRX-Repository)。

### 数据库驱动程序 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>数据库 </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar（版本5.1.44）</p> </td>
   <td><p>在JEE安装时随AEM Forms提供</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驱动程序6.2.1.0（已弃用） <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>随AEM Forms一起提供的关于JEE的安装。</p> </td>
  </tr>
    <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驱动程序6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>随AEM Forms一起提供的关于JEE的安装。</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驱动程序8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>从Microsoft网站下载。</p> </td>
  </tr>
  <tr>
   <td>oracle</td>
   <td><p>oracle数据库19.3.0.0.0 JDBC驱动程序</p> <p>ojdbc8.jar（版本19.3.0.0.0）<br /> </p> </td>
   <td><p>下载自 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">oracle网站</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 应用程序服务器 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
   <td><p><strong>支持的修补程序定义</strong></p> </td>
  </tr>
  <tr>
   <td>oracleWebLogic Server 12.2.1 (12c R2)</td>
   <td>答：支持</td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>答：支持</td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup> （已弃用） </p> </td>
   <td><p>答：支持</p> </td>
   <td><p>支持的EAP版本的补丁程序和累积补丁程序</p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>答：支持</p> </td>
   <td><p>支持的EAP版本的补丁程序和累积补丁程序</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>仅网络部署版本支持IBM® WebSphere®群集。

### 服务器操作系统 {#server-operating-systems}

#### 生产环境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft Windows Server 2019（64位）</td>
   <td>答：支持</td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>答：支持</td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td> Microsoft Windows Server 2016（64位）（已弃用）</td>
   <td>答：支持</td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8（内核4.x）（64位）</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>次要版本、累积更新和关键更新</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7（内核3.x）（64位）（已弃用）</td>
   <td><p>答：支持</p> </td>
   <td><p>次要版本、累积更新和关键更新</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64位）</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>服务包、累积修补程序和关键安全更新</p> </td>
  </tr>
  <tr>
   <td>oracleLinux® 7 Update 3（64位）</td>
   <td>答：支持</td>
   <td>服务包、累积修补程序和关键安全更新</td>
  </tr>
  <tr>
   <td>CentOS 7（64位）<sup> [6]</sup></td>
   <td>答：支持</td>
   <td>服务包、累积修补程序和关键安全更新</td>
  </tr>
 </tbody>
</table>

#### 虚拟化环境 {#virtualized-environment}

您可以在JEE上的物理计算机或虚拟环境中运行AEM Forms。 但是，如果您在虚拟环境中遇到AEM Forms的任何问题，请尝试在物理计算机上复制此问题。 如果问题在物理计算机上仍然存在，请联系Adobe支持部门寻求解决方案。 对于无法在物理计算机上复制的问题，请与虚拟环境供应商联系。

#### 开发环境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台（基本版本）</strong></p> </th>
   <th>支持级别</th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64位</p> </td>
   <td>E：预期工作</td>
   <td><p>Service Pack和关键更新</p> </td>
  </tr>
 </tbody>
</table>

### 支持的服务器平台例外 {#exceptions-to-supported-server-platforms}

选择在JEE服务器上设置AEM Forms的平台时，请考虑以下异常。

1. JEE上的AEM Forms不支持带有MySQL的IBM® WebSphere®。
1. JEE上的AEM Forms不支持SUSE Linux Enterprise Server 12上的JBoss。 SUSE Linux Enterprise Server 12仅支持IBM WebSphere。
1. 除OracleJava™ SE外，JEE上的AEM Forms不支持任何带JBoss®JDK。
1. 除IBM® JDK之外，JEE上的AEM Forms不支持任何包含IBM® WebSphere® JDK的JDK。
1. CRX-repository支持TarMK、MongoDB和关系数据库(RDBMK)类型的持久性。 应用程序服务器和CRX-repository之间不能有两个不同的数据库系统。 但是，在JEE上的AEM Forms环境中，您可以将MongoMK与CRX-repository结合使用，并将支持的关系数据库与应用程序服务器结合使用。
1. JEE上的AEM Forms不支持CentOS上的WebSphere应用程序服务器。
1. JEE上的AEM Forms不支持基于JBoss角色的访问控制(RBAC)。
1. JEE上的AEM Forms仅支持应用程序服务器JBoss EAP 7.4的OracleJava™ SE 11 （64位） SDK。

此外，在选择用于AdobeJEE上AEM Forms的软件时，请考虑以下几点：

- JEE上的AEM Forms支持基于受支持软件的指定主要和次要版本的更新、修补程序和修复包。 但是，除非另外指定，否则不支持更新到下一个主要版本或次要版本。
- 基于群集的安装不支持TarMK持久性。 有关支持的持久性的信息，请参见 [为AEM Forms安装选择持久性类型](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE支持各种第三方软件，具体如下 [第三方软件支持政策](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- 根据第三方供应商提供的支持，JEE上的AEM Forms支持平台。 第三方供应商可能不允许某些组合。 例如，许多供应商尚未通过Oracle认证其应用程序服务器。 因此，JEE上的AEM Forms也不支持这些组合。 要确保您选择支持的软件版本，请查阅第三方供应商的支持列表。
- JEE上的AEM Forms不支持TarMK冷备用。
- JEE上的AEM Forms不支持垂直群集。
- JEE上的AEM Forms不支持群集环境上的MySQL数据库。
- 有关已删除或更新平台的列表，请参阅 [AEM 6.5 Forms新增功能摘要](../../forms/using/whats-new.md) 文档。

### LDAP服务器（可选） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品（基本版本）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>维护版本和修复包</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>功能包和临时修复</p> </td>
  </tr>
 </tbody>
</table>

### 电子邮件服务器（可选） {#email-servers-optional}

| 产品 |
| ----------------------- |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### 内容管理器和相应的连接器 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>产品<br /> </strong></td>
   <td><strong>版本</strong></td>
  </tr>
  <tr>
   <td>emc Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server（已弃用） </td>
   <td>8.5修复包2</td>
  </tr>
  <tr>
   <td> IBM内容管理器客户端（已弃用）</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2016（已弃用）<br /> </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### 支持Cordova {#support-for-cordova}

AEM Forms应用程序现在支持Apache Cordova。 以下是受支持的特定于平台的Cordova版本：

- Apache Cordova 6.4.0
- 科尔多瓦iOS 4.3.0
- Cordova Android 6.0.0
- Cordova Windows 4.4.3

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
PDF生成器仅支持所支持的操作系统和应用程序的英语、法语、德语和日语版本。
此外：
- PDF生成器需要32位版本的 [Acrobat 2020 classic途径20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017版本17.011.30078来执行此转换。
- PDF生成器仅支持32位零售版的Microsoft Office Professional Plus以及转换所需的其他软件。
- PDF生成器不支持Microsoft Office 365。
- 仅在Windows和Linux上支持用于OpenOffice的PDF生成器转换。
- 仅在Windows上支持OCRPDF、Optimize PDF和Export PDF功能。
- Acrobat的一个版本与AEM Forms捆绑在一起，用于启用PDF生成器功能。 在AEM Forms许可证有效期内，捆绑版本只能通过AEM Forms以编程方式访问，以用于AEM FormsPDF生成器。 有关更多信息，请参阅根据您的部署确定的AEM Forms产品描述([内部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
- PDF生成器服务不支持Microsoft Windows 10。
- PDF生成器无法使用Microsoft Visio 2019转换文件。 您可以继续使用Microsoft Visio 2016转换.VSD和.VSDX文件。
- PDF生成器无法使用Microsoft Project 2019转换文件。 您可以继续使用Microsoft Project 2016转换.MPP文件。
>


### 辅助功能支持的异常 {#exceptions-to-accessibility-support}

AEM Forms的以下子系统不是 [508](https://www.section508.gov/) 合规：

- 自适应Forms创作UI
- Forms Manager创作UI
- 通信管理创作UI
- Admin UI (Administration Console UI)

## JEE上的AEM Forms的系统要求 {#system-requirements-for-aem-forms-on-jee}

### 最低硬件要求 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>最低硬件要求</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>英特尔®至强® E5-2680、2.4 GHz处理器或同等处理器<br /> VMWare ESX 5.1或更高版本<br /> RAM：6 GB（64位OS和64位JVM）<br /> 可用磁盘空间：15GB临时空间加上22GB<br /> 适用于AEM Forms on JEE的</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>英特尔至强E5-2670v2,1个vCPU，2.5 GHz处理器<br /> AWS m3.medium（3个ECU）<br /> RAM：6 GB（64位OS和64位JVM）<br /> 可用磁盘空间：6 GB临时空间加上22 GB<br /> 适用于AEM Forms on JEE的</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>英特尔至强E5-2670v2,1个vCPU，2.5 GHz处理器<br /> AWS m3.medium（3个ECU）<br /> RAM：6 GB（64位OS和64位JVM）<br /> 可用磁盘空间：6 GB临时空间加上22 GB<br /> 适用于AEM Forms on JEE的<br /> </td>
  </tr>
  <tr>
   <td>小型生产环境的硬件要求</td>
   <td>
    <ul>
     <li><strong>英特尔支持的环境</strong>：英特尔®至强® E5-2680,2.4 GHz或更高。 使用双核处理器将进一步增强性能</li>
     <li><strong>内存： </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

有关其他要求，请参阅：

- [JEE上单服务器AEM Forms部署的系统要求](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [JEE部署上的群集AEM Forms的系统要求](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## AEM Forms on JEE支持的客户端 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise、Pro、Basic)</p> <p>32位或64位版本</p> <p> </p> </td>
   <td>Service Pack和关键更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Pack和关键更新</td>
  </tr>
 </tbody>
</table>

- 用于安装的磁盘空间：1.7 GB（仅适用于Workbench），2.7 GB（仅适用于Workbench、Designer和示例程序集的完整安装）在单个驱动器上为400 MB（适用于临时安装目录），200 MB位于用户临时目录中，200 MB位于Windows临时目录中。 如果所有这些位置都驻留在单个驱动器上，则安装期间必须有1.5 GB的可用空间。 安装完成后，将删除复制到临时目录的文件。

- 用于运行Workbench的内存：2 GB RAM
- 硬件要求：英特尔®奔腾® 4或等效的AMD，1 GHz处理器
- 最低1024 X 768像素或更高的显示器分辨率（使用16位颜色或更高）
- 与JEE服务器上AEM Forms的TCP/IPv4或TCP/IPv6网络连接
- 必须具有管理权限才能在Windows上安装Workbench。 如果您使用非管理员帐户进行安装，安装程序将提示您输入相应帐户的凭据。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
- 1 GHz或更快的处理器，支持PAE、NX和SSE2。
- 32位RAM为1 GB，64位OS为2 GB
- 16 GB的磁盘空间用于32位操作系统，20 GB的磁盘空间用于64位操作系统
- 图形内存 — 128 MB的GPU（建议使用256 MB）
- 2.35 GB可用硬盘空间
- 1024 X 768像素或更高的显示器分辨率
- 视频硬件加速（可选）
- Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
- 安装Designer的管理权限。

### Adobe Acrobat和Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat和Adobe Reader（基本）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020（经典路线）</td>
   <td>版本20.004.30006或更高版本<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 (Classic Track)（已弃用）</td>
   <td>版本17.011.30078或更高版本<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
Acrobat DC产品系列为Acrobat和Reader引入了两个路径，这两个路径本质上是不同的产品：“Classic”和“Continuous”。 有关详细信息和两个轨道的比较，请参阅 [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### 浏览器 {#browsers}

#### 台式机 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>浏览器（基本）</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge （常绿市）</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>Service Pack和更新</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox （常绿）</p> </td>
   <td><p>答：支持</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E：预期工作</td>
   <td> 所有更新</td>
  </tr>
  <tr>
   <td><p>Google Chrome （常绿）</p> </td>
   <td><p>答：支持</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari</td>
   <td>答：支持</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
台式机的一些与浏览器相关的例外情况如下：
- 只有Macintosh OS X支持Safari。
- Workspace支持带有Acrobat DC或更高版本的Macintosh OS X 10.6和10.7上的Safari 5.1。 有关Safari 5.1与Adobe Reader、Acrobat兼容性的更多信息，请参阅 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
- Safari不支持管理控制台。
- 通信管理不支持Windows® Internet Explorer 9.0 for AEM 6.1表单。
- Forms portal支持Internet Explorer 11上的JAWS 14.0屏幕阅读器软件以便访问。


#### 移动客户端 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>浏览器（基本）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2及更高版本上的Chrome</p> </td>
   <td><p>所有更新</p> </td>
  </tr>
  <tr>
   <td>iOS 15.1及更高版本上的Safari</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>所有更新<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4及更高版本上的本机Android浏览器</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
- 仅iPad上的Safari支持Forms Portal。


### AEM Forms应用程序 {#aem-forms-workspace-app}

#### 移动设备支持 {#mobile-device-support}

AEM Forms应用程序在以下平台上可用：

| **Platform** | **支持的设备** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone、iPad、iPad Air和运行iOS 15.1及更高版本的iPad mini。 |
| Google Android | Android 5.1及更高版本。 AEM Forms应用程序通过7英寸和10英寸三星Galaxy平板电脑和流行智能手机的认证。 |
| Microsoft Windows | 运行Microsoft Windows 10操作系统的Microsoft Surface设备、平板电脑、笔记本电脑和台式机。 |

### AdobeMicrosoft Office的Document Security Extension {#adobe-rights-management-extension-for-microsoft-office}

单击 [此处](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) 查看AdobeDocument Security Extension for Microsoft® Office的系统要求。

### 客户端支持的异常 {#exceptions-to-client-support}

JEE上的AEM Forms支持基于受支持软件的指定主要和次要版本的更新、修补程序和修复包。 但是，除非另外指定，否则不支持更新到下一个主要版本或次要版本。

## 第三方修补程序支持策略 {#third-party-patch-support-policy}

AEM Forms on JEE的第三方软件要求记录在其各自产品文档的“系统要求”部分。 所有文档都可从以下位置访问： [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

AEM Forms on JEE的第三方参考平台说明了开发和发布AEM Forms on JEE期间第三方基础架构的特定当前修补程序级别，以及该AEM Forms on JEE版本支持的基础架构的最低修补程序/Service Pack级别。

Adobe支持第三方供应商在发布后发布的紧急或推荐修补程序，前提是第三方供应商保证与AEM Forms on JEE支持的版本向后兼容。 Adobe将仅支持在AEM Forms on JEE文档中规定的最低修补程序级别之后发布的修补程序。

在某些情况下，Adobe不支持更改主要功能的第三方更新，因此不支持完全向后兼容性。 有关支持的更新的详细信息，请参阅 [支持的修补程序定义](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) Adobe支持的特定供应商产品和修补程序类型。

在Adobe无法控制的情况下，声称向后兼容的第三方修补程序可能会对Adobe产品或客户环境产生负面影响。 在这种情况下，Adobe建议客户在将第三方提供的任何紧急修补程序应用于关键系统之前，评估这些修补程序的影响。 Adobe将与第三方合作，通过正常的Adobe支持计划或通过第三方纠正补丁中的问题，利用合理的商业努力来解决此类问题。 这并不保证新发布的受Adobe支持的第三方修补程序将按供应商记录的方式工作，或者在JEE上与AEM Forms配合工作。

Adobe保留在任意给定时刻更改AEM Forms on JEE版本支持的第三方参考平台及其支持的修补程序定义的权利。

还可以通过搜索Adobe企业支持站点来查找与您的产品相关的知识库文章，从而找到第三方修补程序的其它信息。

## 平台更新 {#platform-updates}

以下平台在2022年6月2日发行的AEM Forms 6.5.13.0中被标记为已弃用：

- Microsoft SharePoint 2016

以下平台在2022年3月3日发行的AEM Forms 6.5.12.0中被标记为已弃用：

- MongoDB Enterprise 4.0
- IBM DB2 11.1
- oracle数据库12c版本2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC驱动程序6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM Content Manager Server 8.5修复包2
- IBM Content Manager客户端8.5
- Microsoft SQL Server 2016

以下平台在2021年9月7日的AEM Forms 6.5.10.0版本中被标记为已弃用：

- Adobe Acrobat 2017 - [对Adobe Acrobat 2017的核心支持将于2022年6月6日终止](https://helpx.adobe.com/cn/support/programs/eol-matrix.html).
- Microsoft Windows Server 2016（64位）
- Red Hat Enterprise Linux 7（内核3.x）（64位）
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
平台标记为 [在AEM Forms 6.5.12.0和6.5.10.0上弃用，在AEM Forms 6.5 Service Pack 18 (6.5.18.0)版本发布之前，仍将继续支持它们](https://helpx.adobe.com/cn/support/programs/eol-matrix.html).

## 修订历史记录 {#revision-history}

- 2022年9月01日

   - 添加了对OracleJava™ SE 11 （64位） SDK for Application Server JBoss EAP 7.4的支持。

- 2022年3月03日

   - 删除了对以下内容的支持：
      - IBM® J9虚拟机（内部版本2.8、JRE 1.8.0）
      - oracle数据库12c版本1
      - oracle数据库18c
      - oracle统一目录(OUD) 11g版本2
      - IBM Lotus Domino 9.0
      - IBM Filenet 5.2
      - AdobeFlash Player

- 2021年10月10日

   - 已将支持的适用于AEM Forms应用程序的iOS版本更改为iOS 15.1。以前的版本是iOS 12。

- 2021年9月07日
   - **平台更新**： [!DNL Adobe Experience Manager Forms] on JEE已添加对以下平台的支持：
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]

- 2020年12月03日
   - AEM Forms 6.5.7.0或更高版本为以下平台添加了支持：
      - [!DNL Microsoft SQL Server 2019]

- 2020年9月09日

   - 已将支持的适用于AEM Forms应用程序的iOS版本更改为iOS 12。 以前的版本是iOS 11。

