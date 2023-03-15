---
title: JEE上AEM Forms的一般安全注意事项
seo-title: General Security Considerations for AEM Forms on JEE
description: 了解如何准备在JEE环境中强化AEM Forms。
seo-description: Learn how to prepare for hardening your AEM Forms on JEE environment.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 1%

---

# JEE上AEM Forms的一般安全注意事项{#general-security-considerations-for-aem-forms-on-jee}

本文提供了可帮助您准备强化AEM Forms环境的介绍性信息。 其中包括有关JEE上的AEM Forms、操作系统、应用程序服务器和数据库安全的先决条件信息。 在继续锁定环境之前，请查看此信息。

## 特定于供应商的安全信息 {#vendor-specific-security-information}

本节包含有关合并到AEM Forms on JEE解决方案中的操作系统、应用程序服务器和数据库的安全相关信息。

使用本节中的链接查找特定于供应商的操作系统、数据库和应用程序服务器的安全信息。

### 操作系统安全信息 {#operating-system-security-information}

保护操作系统时，请仔细考虑实施操作系统供应商所述的措施，其中包括：

* 定义和控制用户、角色和权限
* 监控日志和审核跟踪
* 删除不必要的服务和应用程序
* 备份文件

有关AEM Forms on JEE支持的操作系统的安全信息，请参阅表中的资源：

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
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全性和强化准则</a></p> </td>
  </tr>
  <tr>
   <td>oracleLinux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">版本7的安全指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保护文档</a></td>
  </tr>
 </tbody>
</table>

### 应用程序服务器安全信息 {#application-server-security-information}

保护应用程序服务器时，请仔细考虑实施服务器供应商所述的措施，其中包括：

* 使用不明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 按IP地址或域限制客户端
* 使用Java™安全管理器以编程方式限制权限

有关AEM Forms on JEE支持的应用程序服务器的安全信息，请参阅此表中的资源。

<table>
 <thead>
  <tr>
   <th><p>应用程序服务器</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>WebLogicOracle®</p> </td>
   <td><p>搜索以了解以下位置的WebLogic安全性： <a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>.</p> </td>
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

### 数据库安全信息 {#database-security-information}

在保护数据库时，请考虑实施数据库供应商所述的措施，其中包括：

* 使用访问控制列表(ACL)限制操作
* 使用非标准端口
* 将数据库隐藏在防火墙之后
* 在将敏感数据写入数据库之前对其进行加密（请参阅数据库制造商的文档）

有关AEM Forms on JEE支持的数据库的安全信息，请参阅此表中的资源。

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
   <td>在Web中搜索“SQL Server 2016：安全性”</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全问题</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全问题</a></p> </td>
  </tr>
  <tr>
   <td><p>oracle® 12c</p> </td>
   <td><p>请参阅《 》中的“安全”一章 <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">oracle12g文档</a></p> </td>
  </tr>
 </tbody>
</table>

此表描述了在AEM Forms on JEE配置过程中需要打开的默认端口。 如果通过https进行连接，请相应地调整端口信息和IP地址。 有关配置端口的详细信息，请参见 *在JEE上安装和部署AEM Forms* 应用程序服务器的文档。

<table>
 <thead>
  <tr>
   <th><p>产品或服务</p> </th>
   <th><p>端口号</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Jboss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic托管服务器</p> </td>
   <td><p>由管理员在配置期间设置</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060，如果启用了全局安全，则默认SSL端口值为9043。</p> <p>9080</p> </td>
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
   <td>&gt;<p>oracle</p> </td>
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
   <td><p>运行LDAP服务器的端口。 默认端口通常为389。 但是，如果选择SSL选项，则默认端口通常为636。 向您的LDAP管理员确认要指定的端口。</p> </td>
  </tr>
 </tbody>
</table>

### 将JBoss配置为使用非默认HTTP端口 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss应用程序服务器使用8080作为默认HTTP端口。 JBoss还具有预配置的端口8180、8280和8380，这些端口在jboss-service.xml文件中被注释掉。 如果您的计算机上有一个应用程序已使用此端口，请按照以下步骤更改AEM Forms on JEE使用的端口：

1. 打开以下文件以进行编辑：

   单服务器安装： [JBoss根]/standalone/configuration/standalone.xml

   群集安装： [JBoss根]/domain/configuration/domain.xml

1. 更改值 **端口** 中的属性 **&lt;socket-binding>** 标记到自定义端口号。 例如，以下端口使用端口8090：

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 保存并关闭文件。
1. 重新启动JBoss应用程序服务器。

## AEM Forms on JEE安全注意事项 {#aem-forms-on-jee-security-considerations}

本节介绍了一些关于JEE特定安全问题的部分AEM Forms，您应该了解这些问题。

### 数据库中未加密电子邮件凭据 {#email-credentials-not-encrypted-in-database}

应用程序存储的电子邮件凭据在存储在JEE数据库的AEM Forms中之前不会进行加密。 当您将服务端点配置为使用电子邮件时，在该端点配置中使用的任何密码信息存储在数据库中时都不会加密。

### 数据库中的敏感内容Rights Management {#sensitive-content-for-rights-management-in-the-database}

JEE上的AEM Forms使用JEE上的AEM Forms数据库来存储敏感文档密钥信息以及用于策略文档的其他加密材料。 保护数据库免受入侵有助于保护此敏感信息。

### 明文形式的密码 {#password-in-clear-text-format-in-adobe-ds-xml}

用于在JEE上运行AEM Forms的应用程序服务器需要其自身的配置，以便通过在该应用程序服务器上配置的数据源访问数据库。 确保应用程序服务器不会在其数据源配置文件中以明文形式公开数据库密码。

lc_[数据库].xml文件不应包含明文格式的密码。 有关如何为应用程序服务器加密这些密码的信息，请咨询应用程序服务器供应商。

>[!NOTE]
>
>AEM Forms on JEE JBoss全包安装程序加密数据库密码。

默认情况下，IBM WebSphere Application Server和OracleWebLogic Server可以加密数据源密码。 但是，请使用应用程序服务器文档进行确认，以确保确实发生此情况。

### 保护存储在信任存储区中的私钥 {#protecting-the-private-key-stored-in-trust-store}

在信任存储中导入的私钥或凭据存储在JEE数据库上的AEM Forms中。 采取适当的预防措施保护数据库安全，并限制仅访问指定的管理员。
