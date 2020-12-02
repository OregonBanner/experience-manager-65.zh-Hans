---
title: AEM Forms关于JEE的一般安全考虑
seo-title: AEM Forms关于JEE的一般安全考虑
description: 了解如何为强化AEM Forms的JEE环境做准备。
seo-description: 了解如何为强化AEM Forms的JEE环境做准备。
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---


# AEM FormsJEE{#general-security-considerations-for-aem-forms-on-jee}的一般安全注意事项

本文提供介绍性信息，帮助您准备强化AEM Forms环境。 它包括关于AEM FormsJEE、操作系统、应用程序服务器和数据库安全的先决条件信息。 在继续锁定环境之前，请查看此信息。

## 供应商特定安全信息{#vendor-specific-security-information}

本部分包含有关操作系统、应用程序服务器和数据库的与安全相关的信息，这些信息已并入您的AEM Forms的JEE解决方案中。

使用本节中的链接查找操作系统、数据库和应用程序服务器的供应商特定安全信息。

### 操作系统安全信息{#operating-system-security-information}

在保护操作系统时，请仔细考虑实施操作系统供应商描述的措施，包括：

* 定义和控制用户、角色和权限
* 监视日志和审计跟踪
* 删除不必要的服务和应用程序
* 备份文件

有关AEM FormsJEE支持的操作系统的安全信息，请参阅表中的资源：

<table>
 <thead>
  <tr>
   <th><p>操作系统</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM AIX安全优势</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP或ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat Enterprise Linux安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全和强化准则</a></p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7更新3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">版本7安全指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保护文档</a></td>
  </tr>
 </tbody>
</table>

### 应用程序服务器安全信息{#application-server-security-information}

在保护应用程序服务器时，请仔细考虑实施服务器供应商描述的措施，包括：

* 使用非明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 通过IP地址或域限制客户端
* 使用Java™ Security Manager以编程方式限制权限

有关AEM Forms在JEE上支持的应用程序服务器的安全信息，请参阅此表中的资源。

<table>
 <thead>
  <tr>
   <th><p>应用程序服务器</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>OracleWebLogic®</p> </td>
   <td><p>在<a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>中搜索了解WebLogic安全性。</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">保护应用程序及其环境</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">安全子系统配置</a></p> </td>
  </tr>
 </tbody>
</table>

### 数据库安全信息{#database-security-information}

保护数据库时，请考虑实施数据库供应商描述的措施，包括：

* 使用访问控制列表(ACL)限制操作
* 使用非标准端口
* 在防火墙后隐藏数据库
* 在将敏感数据写入数据库之前对其进行加密（请参阅数据库制造商的文档）

有关AEM FormsJEE上支持的数据库的安全信息，请参阅此表中的资源。

<table>
 <thead>
  <tr>
   <th><p>数据库</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2产品系列库</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>在Web上搜索“SQL Server 2016:安全性”</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全问题</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全问题</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>请参见<a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle12g文档</a>中的“安全”一章</p> </td>
  </tr>
 </tbody>
</table>

此表描述了在JEE配置过程的AEM Forms期间需要打开的默认端口。 如果通过https连接，请相应地调整端口信息和IP地址。 有关配置端口的详细信息，请参阅应用程序服务器的&#x200B;*在JEE上安装和部署AEM Forms*&#x200B;文档。

<table>
 <thead>
  <tr>
   <th><p>产品或服务</p> </th>
   <th><p>端口号</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic Managed Server</p> </td>
   <td><p>配置期间由管理员设置</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060，如果启用了“全局安全”，则默认的SSL端口值为9043。</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>BAM服务器</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>运行LDAP服务器的端口。 默认端口通常为389。 但是，如果选择SSL选项，则默认端口通常为636。 向LDAP管理员确认要指定的端口。</p> </td>
  </tr>
 </tbody>
</table>

### 将JBoss配置为使用非默认HTTP端口{#configuring-jboss-to-use-a-non-default-http-port}

JBoss Application Server使用8080作为默认HTTP端口。 JBoss还具有预配置的端口8180、8280和8380，这些端口在jboss-service.xml文件中被注释掉。 如果您的计算机上有已使用此端口的应用程序，请按照以下步骤更改JEE上的AEM Forms使用的端口：

1. 打开以下文件进行编辑：

   单服务器安装：[JBoss root]/standalone/configuration/standalone.xml

   群集安装：[JBoss root]/domain/configuration/domain.xml

1. 将&#x200B;**&lt;socket-binding>**&#x200B;标签中的&#x200B;**port**&#x200B;属性的值更改为自定义端口号。 例如，以下代码使用端口8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot; />

1. 保存并关闭文件。
1. 重新启动JBoss应用程序服务器。

## AEM Forms关于JEE安全考虑{#aem-forms-on-jee-security-considerations}

本节介绍一些您应了解的关于JEE特定安全问题的AEM Forms。

### 未在数据库{#email-credentials-not-encrypted-in-database}中加密电子邮件凭据

应用程序存储的电子邮件凭据在存储在AEM Forms的JEE数据库中之前不会经过加密。 将服务端点配置为使用电子邮件时，作为该端点配置的一部分使用的任何口令信息在存储在数据库中时都不会加密。

### Rights Management库{#sensitive-content-for-rights-management-in-the-database}中的敏感内容

AEM Formson JEE使用AEM Formson JEE文档库存储敏感密钥信息和用于策略文档的其他加密材料。 保护数据库免受入侵，有助于保护此敏感信息。

### 以明文形式{#password-in-clear-text-format-in-adobe-ds-xml}输入密码

用于在JEE上运行AEM Forms的应用程序服务器需要其自己的配置，以便通过应用程序服务器上配置的数据源访问数据库。 确保应用程序服务器不在其数据源配置文件中以明文显示数据库密码。

lc_[database].xml文件不应包含明文格式的口令。 请咨询应用程序服务器供应商，了解如何为应用程序服务器加密这些口令。

>[!NOTE]
>
>AEM Forms的JEE JBoss统包安装程序加密数据库密码。

默认情况下，IBM WebSphere Application Server和OracleWebLogic Server可以加密数据源口令。 但是，请通过应用程序服务器文档进行确认，以确保发生这种情况。

### 保护存储在信任存储{#protecting-the-private-key-stored-in-trust-store}中的私钥

在信任存储中导入的私钥或凭据存储在JEE数据库的AEM Forms。 采取适当预防措施保护数据库并仅限指定管理员访问。
