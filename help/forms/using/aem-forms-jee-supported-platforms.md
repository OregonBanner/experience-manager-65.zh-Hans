---
title: JEE上AEM Forms支持的平台
seo-title: JEE上AEM Forms支持的平台
description: 列表在JEE上安装AEM Forms所需和支持的基础结构组件
seo-description: 列表在JEE上安装AEM Forms所需和支持的基础结构组件
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3310'
ht-degree: 1%

---


# JEE{#supported-platforms-for-aem-forms-on-jee}上AEM Forms支持的平台

## 支持的平台 {#supported-platforms}

### 支持级别{#support-levels}

可以使用支持的操作系统、应用程序服务器、数据库、数据库驱动程序、JDK、LDAP服务器和电子邮件服务器的任意组合来设置JEE服务器上的AEM Forms。

此文档列表JEE上AEM Forms支持的客户端和服务器平台。 Adobe为我们的推荐配置和其他配置提供了多个级别的支持。 该文档还列表了其他受支持的软件及其版本、异常、修补程序定义和第三方软件修补程序支持策略。

>[!NOTE]
>
>* 有关受支持服务器平台的例外的完整列表，请参阅[受支持服务器平台的例外](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)。
>* AEM Forms on JEE仅支持英语、法语、德语和日语版的受支持操作系统和应用程序。
>



### 建议的配置{#recommendedconfigurations}

Adobe建议进行这些配置，并作为标准软件维护协议的一部分提供完全或受限的支持：

<table>
 <tbody>
  <tr>
   <th>支持级别</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>答：支持的<br /> </td>
   <td>Adobe为此配置提供全面支持和维护。 此配置由Adobe的质量保证流程涵盖。</td>
  </tr>
  <tr>
   <td>R:受限支持</td>
   <td>Adobe在满足特定先决条件后提供对此配置的完全支持。 请与Adobe企业支持联系，了解先决条件并请求支持。</td>
  </tr>
  <tr>
   <td>L:有限支持</td>
   <td>Adobe在满足特定先决条件后为此配置提供全面支持和维护。 并非所有功能都在配置中可用。 请与Adobe企业支持联系，了解先决条件并请求支持。<br /> </td>
  </tr>
 </tbody>
</table>

### 不支持的配置{#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| E:预期可以工作 | 预计该配置将起作用，没有相反的报告。 |
| Z:不支持 | 不支持该配置。 Adobe不会就配置是否有效发表任何声明，也不支持配置。 |

>[!NOTE]
>
>为帮助AEM Forms客户降低拥有成本、简化部署体系结构和使开发堆栈现代化，Adobe Experience Manager企业平台正从基于应用程序服务器的部署转向基于独立OSGi的部署。 Adobe继续支持AEM Forms JEE堆栈，并减少了基础架构组件矩阵。
>
>随着6.5的发布，客户中使用率最低的基础架构组件不再受支持，如下所示：
>· IBM DB2数据库
>· IBM AIX和Sun Solaris操作系统
>
>对于新安装，建议在可行时在现代OSGi堆栈上部署AEM Forms，以利用响应式Adaptive Forms中的最新创新功能，使用表单数据模型实现移动、多渠道交互通信和后端数据集成。
>
>我们认识到现有用户需要继续在JEE堆栈上部署AEM Forms。 在这种情况下，Adobe需要如本文档所述在受支持的基础架构上部署AEM Forms JEE。 如果您要升级到AEM 6.5 Forms并在上一个AEM Forms版本上使用不受支持的平台，则可以与Adobe支持联系，以获取有关升级到受支持平台的帮助。

### Java虚拟机(JVM){#java-virtual-machines-jvm}

Adobe Experience Manager Forms要求运行Java虚拟机，该虚拟机由Java开发工具包(JDK)分发提供。 Adobe Experience Manager使用以下版本的Java虚拟机：

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11（64位）</p> </td>
   <td><p>Z:不支持</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8（64位）</td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（内部版本2.8,JRE 1.8.0）</td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine(build 2.9,JRE 1.8.0)<br /> </td>
   <td>答：支持</td>
   <td>次要版本和更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 建议跟踪Java供应商的安全公告，以确保生产环境的安全和安全，并安装最新的Java更新。
>* AEM Forms on JEE仅支持生产环境上的64位JVM。


### 数据库和CRX持久性{#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>平台</strong></p> </td>
   <td><p><strong> 描述</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
  </tr>
  <tr>
   <td><p>文件系统</p> </td>
   <td><p>存储库微内核（TAR MK文件）</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c版本1</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
   <tr>
   <td><p>Oracle Database 12c版本2(12.2.0.1.0)</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td>Oracle Database 18c </td>
   <td>存储库微内核</td>
   <td>支持</td>
  </tr> 
   <tr>
   <td>Oracle Database 19c(标准版、Real Application Clusters(RAC)和Enterprise版) </td>
   <td>存储库Microkernal </td>
   <td>支持</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>存储库微内核</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>存储库微内核</td>
   <td>R:受限支持</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R:受限支持</td>
  </tr>
 </tbody>
</table>

* IBM DB2不支持新安装。 仅对升级到AEM 6.5 Forms的现有客户支持。
* MongoDB是第三方软件，不包含在AEM许可包中。 有关详细信息，请参阅[MongoDB授权策略](https://www.mongodb.org/about/licensing/)页。
* 为了充分利用您的AEM部署，Adobe建议授权许可MongoDB企业版，以从专业支持中受益。
* Adobe客户关怀将协助解决与将MongoDB与AEM一起使用相关的资格认定问题。 有关详细信息，请参阅[Adobe Experience Manager的MongoDB页面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。
* “文件系统”包括符合POSIX的块存储。 这包括网络存储技术。 请注意，文件系统性能可能会有所不同，并影响总体性能。 建议将测试AEM与网络/远程文件系统结合加载。
* 仅支持MongoDB存储引擎WiredTiger。
* AEM中不支持MongoDB共享。
* AEM Forms on JEE不支持MySQL对RDBMK持久性。
* 文档安全模块不使用内容存储库。 这意味着，如果您仅使用文档 Security，并且不计划使用HTML Workspace、HTML5表单或自适应表单，则请勿安装内容存储库。
* AEM Forms on JEE不支持使用MySQL保持AEM存储库(CRX-Repository)。


### 数据库驱动程序{#database-drivers}

<table>
 <tbody>
  <tr>
   <th>数据库 </th>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar（5.1.44版）</p> </td>
   <td><p>在JEE安装时随AEM Forms提供</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驱动程序6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>在JEE安装时随AEM Forms提供。</p> </td>
  </tr>
  <tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驱动程序8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>从Microsoft网站下载。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC驱动程序</p> <p>ojdbc8.jar（版本19.3.0.0.0）<br /> </p> </td>
   <td><p>从<a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">Oracle网站</a>下载。</p> </td>
  </tr>
 </tbody>
</table>

### 应用程序服务器{#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> 平台</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
   <td><p><strong>支持的修补程序定义</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1(12c R2)</td>
   <td>答：支持</td>
   <td>服务包和关键更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>答：支持</td>
   <td>服务包和关键更新</td>
  </tr>
  <tr>
   <td><p>JBoss®企业应用程序平台(EAP)7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>答：支持</p> </td>
   <td><p>支持的EAP版本的修补程序和累积修补程序</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>IBM® WebSphere®群集仅在网络部署版本中受支持。

### 服务器操作系统{#server-operating-systems}

#### 生产环境{#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> 平台</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016（64位）</td>
   <td>答：支持</td>
   <td>服务包和关键更新</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7(Kernel 3.x)（64位）</br><b>注意：</b> <a href="https://access.redhat.com/articles/4665701">Red Hat Enterprise Linux 6</a>在2020年11月30日达到维护阶段结束并过渡到扩展生命周期支持阶段。 Adobe建议使用Red Hat Enterprise Linux 7进行升级和新安装。 现有安装可以在延长生命周期支持阶段使用Red Hat Enterprise Linux 6。</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>次要版本、累积更新和关键更新</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64位）</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>服务包、累积修补程序和关键安全更新</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3（64位）</td>
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

#### 虚拟化环境{#virtualized-environment}

您可以在物理机或虚拟环境上的JEE上运行AEM Forms。 但是，如果在虚拟环境上遇到与AEM Forms有关的任何问题，请尝试在物理机上复制问题。 如果问题在物理计算机上仍然存在，请与Adobe支持联系以获得解决。 对于无法在物理计算机上复制的问题，请与虚拟环境供应商联系。

#### 开发环境{#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台（基本版）</strong></p> </th>
   <th>支持级别</th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64位</p> </td>
   <td>E:预期可以工作</td>
   <td><p>服务包和关键更新</p> </td>
  </tr>
 </tbody>
</table>

### 受支持服务器平台{#exceptions-to-supported-server-platforms}的例外

在选择在JEE服务器上设置AEM Forms的平台时，请考虑以下例外。

1. AEM Forms on JEE不支持使用MySQL的IBM® WebSphere®。
1. AEM Forms on JEE在SUSE Linux Enterprise Server 12上不支持和JBoss。 SUSE Linux Enterprise Server 12仅支持IBM WebSphere。
1. AEM Forms on JEE不支持使用JBoss®的任何JDK，只支持Oracle Java™ SE。
1. AEM Forms on JEE不支持IBM® WebSphere®（IBM® JDK除外）中的任何JDK。
1. CRX-repository支持TarMK、MongoDB类型和关系数据库(RDBMK)的持久性。 应用程序服务器和CRX-repository之间不能有两个不同的数据库系统。 但是，在JEE环境上的AEM Forms上，您可以将MongoMK与CRX-repository一起使用，并将受支持的关系数据库与应用程序服务器一起使用。
1. AEM Forms on JEE不支持CentOS上的WebSphere应用程序服务器。
1. AEM Forms on JEE不支持基于JBoss角色的访问控制(RBAC)。

此外，在为JEE部署的Adobe AEM Forms选择软件时，请考虑以下几点：

* AEM Forms on JEE支持受支持软件的指定主要和次要版本的更新、修补程序和修复包。 但是，除非指定，否则不支持更新到下一个主版本或次版本。
* 基于群集的安装不支持TarMK持久性。 有关支持的持久性的信息，请参阅[为AEM Forms安装选择持久性类型](/help/forms/using/choosing-persistence-type-for-aem-forms.md)。
* AEM Forms on JEE根据我们的[第三方软件支持策略](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)支持各种第三方软件。
* AEM Forms on JEE根据第三方供应商提供的支持支持平台。 第三方供应商可能不允许某些组合。 例如，许多供应商尚未通过Oracle认证其应用程序服务器。 因此，JEE上的AEM Forms也不支持这些组合。 为确保您选择支持的软件版本，请同时检查第三方供应商的支持列表。
* AEM Forms on JEE不支持TarMK Cold Standby。
* AEM Forms on JEE不支持垂直群集。
* AEM Forms on JEE不支持群集环境上的MySQL数据库。
* 有关已删除或更新平台的列表，请参阅[AEM 6.5 Forms新增功能摘要](../../forms/using/whats-new.md)文档。

### LDAP服务器（可选）{#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品（基本版本）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle统一目录(OUD)11g版本2</td>
   <td>服务包</td>
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

### 电子邮件服务器（可选）{#email-servers-optional}

| 产品 |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### 内容管理器和相应的连接器{#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>产品<br /> </strong></td>
   <td><strong>版本号</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5修复包2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Client</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### 支持Cordova {#support-for-cordova}

AEM Forms应用程序现在支持Apache Cordova。 以下是支持的特定于平台的Cordova版本：

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### 对PDF生成器{#software-support-for-pdf-generator}的软件支持

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>支持的转换为PDF格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> 最新版本</td>
   <td>XPS，图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP，WPD</td>
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
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPG、TIF、TIF、TIF、TF、PNG、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator仅支持支持的操作系统和应用程序的英语、法语、德语和日语版本。
>
>此外：
>
>* PDF Generator需要32位版本的[Acrobat 2017经典轨道版本17.011.30078或更高版本](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)才能执行转换。
>* PDF Generator仅支持32位零售版Microsoft Office Professional Plus和转换所需的其他软件。
>* PDF Generator不支持Microsoft Office 365。
>* 仅Windows和Linux支持OpenOffice的PDF Generator转换。
>* 仅Windows支持OCR PDF、Optimize PDF和Export PDF功能。
>* Acrobat与AEM Forms捆绑在一起，以启用PDF Generator功能。 在AEM Forms许可证有效期内，只能通过AEM Forms以编程方式访问捆绑版本，以便与AEM Forms PDF Generator一起使用。 有关详细信息，请参阅AEM Forms产品说明(根据您的部署([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)或[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
   >
   >
* PDF Generator服务不支持Microsoft Windows 10。
>



### 辅助功能例外支持{#exceptions-to-accessibility-support}

AEM Forms的以下子系统不符合[508](https://www.section508.gov/):

* 自适应Forms创作UI
* Forms Manager创作UI
* 通信管理创作UI
* 管理员UI（管理控制台UI）

## JEE {#system-requirements-for-aem-forms-on-jee}上的AEM Forms系统要求

### 最低硬件要求{#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>平台</td>
   <td>最低硬件要求</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680、2.4 GHz处理器或等效的<br /> VMWare ESX 5.1或更高版本<br /> RAM:6 GB（64位操作系统，带64位JVM）<br />可用磁盘空间：15GB临时空间加上22GB<br />(适用于JEE上的AEM Forms)</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2,1个vCPU，2.5 GHz处理器<br /> AWS m3.medium（3个ECU）<br /> RAM:6 GB（64位操作系统，带64位JVM）<br />可用磁盘空间：6 GB临时空间，外加22 GB<br />(适用于JEE上的AEM Forms)</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2,1个vCPU，2.5 GHz处理器<br /> AWS m3.medium（3个ECU）<br /> RAM:6 GB（64位操作系统，带64位JVM）<br />可用磁盘空间：6 GB临时空间，加上JEE上的AEM Forms 22 GB<br /><br /> </td>
  </tr>
  <tr>
   <td>小型生产环境的硬件要求</td>
   <td>
    <ul>
     <li><strong>以英特尔为后盾的环境</strong>:英特尔®至强® E5-2680,2.4 GHz或更高。使用双核处理器将进一步提高性能</li>
     <li><strong>内存： </strong>4 GB  <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

有关其他要求，请参阅：

* [单服务器AEM Forms在JEE部署上的系统要求](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [JEE部署上的群集AEM Forms的系统要求](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## JEE {#supported-clients-for-aem-forms-on-jee}上AEM Forms支持的客户端

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise、Pro、Basic)</p> <p>32位或64位版本</p> <p> </p> </td>
   <td>服务包和关键更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>服务包和关键更新</td>
  </tr>
 </tbody>
</table>

* 用于安装的磁盘空间：仅限Workbench 1.7 GB，单个驱动器上为2.7 GB，可完整安装Workbench、Designer和示例程序集400 MB（临时安装目录） — 200 MB（用户临时目录）和200 MB（Windows临时目录）。 如果所有这些位置都位于单个驱动器上，则安装过程中必须有1.5 GB的可用空间。 安装完成后，将删除复制到临时目录的文件。

* 运行Workbench的内存：2 GB内存
* 硬件要求：Intel® Pentium® 4或AMD等效处理器，1 GHz处理器
* 最低1024 X 768像素或更高的显示器分辨率，16位颜色或更高
* 到JEE服务器上AEM Forms的TCP/IPv4或TCP/IPv6网络连接
* 您必须具有“管理”权限才能在Windows上安装Workbench。 如果您使用非管理员帐户进行安装，安装程序将提示您输入相应帐户的凭据。

### 设计器{#designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
* 1 GHz或更快的处理器，支持PAE、NX和SSE2。
* 32位需要1 GB内存，64位操作系统需要2 GB内存
* 32位为16 GB磁盘空间，64位操作系统为20 GB磁盘空间
* 图形内存 — 128 MB GPU（建议使用256 MB）
* 2.35 GB可用硬盘空间
* 1024 X 768像素或更高的显示器分辨率
* 视频硬件加速（可选）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
* 安装Designer的管理权限。

### Adobe Acrobat和Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat和Adobe Reader（基础）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017（经典版）</td>
   <td>版本17.011.30078或更高版本<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat DC产品系列为Acrobat和Reader引入了两条途径，这两条途径本质上是不同的产品：“经典”和“连续” 有关这两个轨道的详细信息和比较，请参阅[https://www.adobe.com/go/acrobatdctracks。](https://www.adobe.com/go/acrobatdctracks)

### 浏览器{#browsers}

#### 桌面{#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>浏览器（基础）</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge(Evergreen)</p> </td>
   <td><p>答：支持</p> </td>
   <td><p>服务包和更新</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox(Evergreen)</p> </td>
   <td><p>答：支持</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E:预期可以工作</td>
   <td> 所有更新</td>
  </tr>
  <tr>
   <td><p>Google Chrome(Evergreen)</p> </td>
   <td><p>答：支持</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>MAC OS X上的Google Chrome和Firefox</td>
   <td>答：支持<br /> <br /> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>答：支持</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>答：支持</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>桌面的某些与浏览器相关的例外如下：
>
>* 大多数现代浏览器不再支持基于NPAPI的插件。 有关它对AEM Forms应用程序和工作流的影响的信息，请参阅[停止NPAPI浏览器插件及其影响](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)。
>* 仅Macintosh OS X支持Safari。
>* Workspace在Acrobat DC或更高版本的Macintosh OS X 10.6和10.7上支持Safari 5.1。 有关Safari 5.1与Acrobat Adobe Reader的兼容性的详细信息，请参阅[https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html)。
>* Safari不支持管理控制台。
>* Corresponce Management不支持Windows® Internet Explorer 9.0 for AEM 6.1表单。
>* Forms门户支持Internet Explorer 11上的JAWS 14.0屏幕阅读器软件，以便访问。
>



#### 移动客户端{#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>浏览器（基础）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2及更高版本上的Chrome</p> </td>
   <td><p>所有更新</p> </td>
  </tr>
  <tr>
   <td>iOS 11.0及更高版本上的Safari</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>所有更新<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4及更高版本上的本机Andriod浏览器</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal仅在iPad上的Safari上受支持。
>



### AEM Forms应用程序{#aem-forms-workspace-app}

#### 移动设备支持{#mobile-device-support}

AEM Forms应用程序可用于以下平台：

| **平台** | **支持的设备** |
|---|---|
| Apple iOS | 运行iOS 12及更高版本的Apple iPhone、iPad、iPad Air和iPad mini。 |
| Google Android | Android 5.1及更高版本。 AEM Forms应用在7英寸和10英寸的三星Galaxy平板电脑和流行智能手机上获得认证。 |
| Microsoft Windows | 运行Microsoft Windows 10操作系统的Microsoft Surface设备、平板电脑、笔记本电脑和台式机。 |

### AdobeFlash Player{#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player（基础）</strong></p> </th>
   <th><p><strong>支持的修补程序定义</strong></p> </th>
  </tr>
  <tr>
   <td><p>Flash Player最新版本</p> </td>
   <td><p>次要版本和更新</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe将在2020年底](https://theblog.adobe.com/adobe-flash-update/)停止更新和分发Flash Player。[

### Adobe 文档 Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

单击[此处](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html)查看Adobe 文档 Security Extension for Microsoft® Office的系统要求。

### 客户端支持{#exceptions-to-client-support}的例外

AEM Forms on JEE支持受支持软件的指定主要和次要版本的更新、修补程序和修复包。 但是，除非指定，否则不支持更新到下一个主版本或次版本。

## 第三方修补程序支持策略{#third-party-patch-support-policy}

针对JEE的AEM Forms的第三方软件要求在其各自产品文档的“系统要求”部分中进行说明。 所有文档均可从[https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65)访问。

AEM Forms在JEE的第三方参考平台上陈述了在JEE上开发和发布AEM Forms时最新的第三方基础架构的特定修补程序级别，以及由JEE上该版本的AEM Forms支持的基础架构的最低修补程序/服务包级别。

Adobe支持第三方供应商在发布时发布的紧急或推荐的修补程序，前提是第三方供应商保证向后兼容AEM Forms在JEE上支持的版本。 Adobe将仅支持在AEM Forms on JEE文档中所述的最低修补程序级别之后发布的修补程序。

在某些情况下，Adobe不支持更改主要功能的第三方更新，因此不支持完全向后兼容性。 有关支持的更新的详细信息，请参阅[针对特定供应商产品和Adobe支持的修补程序类型的支持修补程序定义](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html)。

在Adobe无法控制的情况下，声称向后兼容的第三方修补程序可能会对Adobe产品或客户环境产生负面影响。 在这种情况下，Adobe建议客户在将任何紧急补丁程序应用到关键系统之前先评估第三方对它们的影响。 Adobe将与第三方合作，通过合理的业务努力解决此类问题，无论是通过正常的Adobe支持项目，还是通过第三方在其补丁中纠正该问题。 这不保证将受Adobe支持的新发布的第三方修补程序能够按供应商或AEM Forms在JEE上的文档运行。

Adobe保留在任何给定时刻更改由AEM Forms在JEE版本上支持的第三方参考平台及其支持的修补程序定义的权利。

通过搜索Adobe企业支持站点以找到与您的产品相关的知识库文章，还可以找到有关第三方修补程序的其他信息。

## 修订历史记录{#revision-history}

* 2020年9月9日
   * 将AEM Forms App支持的iOS版本更改为iOS 12。 以前的版本是iOS 11。
