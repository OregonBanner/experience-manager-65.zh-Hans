---
title: 在JEE环境中强化AEM Forms
seo-title: 在JEE环境中强化AEM Forms
description: 了解各种安全强化设置，以增强在企业内部网中运行的JEE上的AEM Forms的安全性。
seo-description: 了解各种安全强化设置，以增强在企业内部网中运行的JEE上的AEM Forms的安全性。
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '7696'
ht-degree: 0%

---

# 在JEE环境中强化AEM Forms {#hardening-your-aem-forms-on-jee-environment}

了解各种安全强化设置，以增强在企业内部网中运行的JEE上的AEM Forms的安全性。

本文介绍了为保护在JEE上运行AEM Forms的服务器而提供的建议和最佳实践。 这不是适用于您的操作系统和应用程序服务器的全面的主机强化文档。 相反，本文介绍了您应该实施的各种安全强化设置，以增强在公司内部网内运行的JEE上AEM Forms的安全性。 但是，为了确保JEE应用程序服务器上的AEM Forms保持安全，您还应实施安全监控、检测和响应过程。

本文介绍了在安装和配置生命周期的以下阶段应用的硬化技术：

* **安装前：** 在JEE上安装AEM Forms之前，请使用这些技术。
* **安装：** 在JEE上的AEM Forms安装过程中使用这些技术。
* **安装后：** 安装后使用这些技术，之后会定期使用。

AEM Forms on JEE是高度可自定义的，并且可以在许多不同的环境中工作。 某些建议可能不符合您组织的需求。

## 预安装 {#preinstallation}

在JEE上安装AEM Forms之前，您可以将安全解决方案应用到网络层和操作系统。 本节介绍了一些问题，并就减少这些领域的安全漏洞提出建议。

**在UNIX和Linux上安装和配置**

您不应在JEE上使用根Shell安装或配置AEM Forms。 默认情况下，文件安装在/opt目录下，执行安装的用户需要在/opt目录下拥有所有文件权限。 或者，也可以在单个用户的/user目录下执行安装，在该目录下，他们已经拥有所有文件权限。

**在Windows上安装和配置**

如果您在JBoss的JEE上使用统包方法安装AEM Forms，或者您正在安装PDF生成器，则您应以管理员身份在Windows上执行安装。 此外，在具有本机应用程序支持的Windows上安装PDF生成器时，必须与安装Microsoft Office的Windows用户一样运行安装。 有关安装权限的更多信息，请参阅*在JEE上安装和部署AEM Forms*文档，以了解您的应用程序服务器。

### 网络层安全性 {#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器的首要威胁之一。 本节介绍如何针对这些漏洞强化网络上的主机。 它解决了网络分段、传输控制协议/互联网协议(TCP/IP)堆栈强化以及防火墙用于主机保护的问题。

下表描述了减少网络安全漏洞的常见过程。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>隔离区(DMZ)</p> </td> 
   <td><p>在隔离区(DMZ)内部署表单服务器。 分段应至少存在于两个级别中，应用程序服务器用于在JEE上运行AEM Forms，位于内部防火墙之后。 将外部网络与包含Web服务器的DMZ分隔开，Web服务器又必须与内部网络分隔开。 使用防火墙来实现分层。 对通过每个网络层的流量进行分类和控制，以确保仅允许绝对最小的所需数据。</p> </td> 
  </tr> 
  <tr> 
   <td><p>专用IP地址</p> </td> 
   <td><p>在AEM Forms应用程序服务器上将网络地址转换(NAT)与RFC 1918专用IP地址结合使用。 分配专用IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难通过Internet路由NAT内部主机与NAT内部主机之间的通信。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火墙</p> </td> 
   <td><p>使用以下标准选择防火墙解决方案：</p> 
    <ul> 
     <li><p>实施支持代理服务器和/或<em>状态检查</em>的防火墙，而不是简单的数据包过滤解决方案。</p> </li> 
     <li><p>使用支持<em>拒绝除明确允许的</em>安全范例之外的所有服务的防火墙。</p> </li> 
     <li><p>实施双宿主或多宿主的防火墙解决方案。 此架构可提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>数据库端口</p> </td> 
   <td><p>请勿对数据库使用默认监听端口(MySQL - 3306、Oracle- 1521、MS SQL - 1433)。 有关更改数据库端口的信息，请参阅数据库文档。</p> <p>使用其他数据库端口会影响JEE上的整个AEM Forms配置。 如果更改默认端口，则必须在其他配置区域(例如JEE上的AEM Forms的数据源)中进行相应的修改。</p> <p>有关在JEE上的AEM Forms中配置数据源的信息，请参阅<a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms用户指南</a>中的在JEE上安装和升级AEM Forms或在JEE上升级到AEM Forms以获取应用程序服务器。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 操作系统安全性 {#operating-system-security}

下表描述了在操作系统中发现的一些尽可能减少安全漏洞的潜在方法。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p></th> 
   <th><p>描述</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全修补程序</p></td> 
   <td><p>如果供应商安全补丁和升级未及时应用，则未经授权的用户可能获得对应用程序服务器的访问权，这种风险增加。 在将安全修补程序应用到生产服务器之前，请先测试这些修补程序。</p><p>此外，还应创建策略和程序，以定期检查和安装修补程序。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防护软件</p></td> 
   <td><p>病毒扫描程序可以通过扫描签名或监视异常行为来识别受感染的文件。 扫描程序将其病毒签名保留在文件中，该文件通常存储在本地硬盘上。 由于经常发现新病毒，因此您应该经常更新此文件，以便病毒扫描程序识别所有当前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>网络时间协议(NTP)</p></td> 
   <td><p>要进行法证分析，请在表单服务器上保留准确的时间。 使用NTP来同步所有直接连接到Internet的系统上的时间。</p></td> 
  </tr> 
 </tbody> 
</table>

有关操作系统的其他安全信息，请参阅[&quot;操作系统安全信息&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安装 {#installation}

本节介绍在AEM Forms安装过程中可用于减少安全漏洞的技术。 在某些情况下，这些技术会使用安装过程中包含的选项。 下表介绍了这些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>权限</p> </td> 
   <td><p>使用安装软件所需的最少权限数。 使用“管理员”组中未包含的帐户登录到您的计算机。 在Windows上，您可以使用“运行方式”命令在JEE安装程序上以管理用户身份运行AEM Forms。 在UNIX和Linux系统上，使用<code>sudo</code>之类的命令来安装软件。</p> </td> 
  </tr> 
  <tr> 
   <td><p>软件源</p> </td> 
   <td><p>请勿在JEE上从不受信任的源下载或运行AEM Forms。</p> <p>恶意程序可能包含以多种方式违反安全的代码，包括数据窃取、修改和删除以及拒绝服务。 在JEE上从AdobeDVD或仅从可信来源安装AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁盘分区</p> </td> 
   <td><p>将AEM Forms置于JEE上的专用磁盘分区上。 磁盘分段是一个过程，它会将服务器上的特定数据保留在单独的物理磁盘上，以增强安全性。 以这种方式安排数据可降低目录遍历攻击的风险。 计划创建一个与系统分区分开的分区，您可以在JEE内容目录上安装AEM Forms。 （在Windows上，系统分区包含system32目录或引导分区。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>组件</p> </td> 
   <td><p>评估现有服务，并禁用或卸载任何不需要的服务。 请勿安装不必要的组件和服务。</p> <p>应用程序服务器的默认安装可能包含您不需要的服务。 您应在部署之前禁用所有不必要的服务，以最大限度地减少攻击的入口点。 例如，在JBoss上，您可以在META-INF/jboss-service.xml描述符文件中注释掉不必要的服务。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略文件</p> </td> 
   <td><p>服务器上存在<code>crossdomain.xml</code>文件可能会立即削弱该服务器。 建议您尽可能限制域列表。 使用指南<em>（已弃用）</em>时，请勿将开发期间使用的<code>crossdomain.xml</code>文件放入生产中。 对于使用Web服务的指南，如果服务位于提供该指南的同一服务器上，则根本不需要<code>crossdomain.xml</code>文件。 但是，如果服务位于另一台服务器上，或者如果涉及群集，则需要存在<code>crossdomain.xml</code>文件。 有关crossdomain.xml文件的更多信息，请参阅<a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p>操作系统安全设置</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，请确保安装<code>pkcs11_softtoken_extra.so</code>而不是<code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安装后步骤 {#post-installation-steps}

在JEE上成功安装AEM Forms后，务必从安全角度定期维护环境。

以下部分详细介绍为保护已部署的表单服务器而建议执行的不同任务。

### AEM Forms安全 {#aem-forms-security}

以下推荐设置适用于管理Web应用程序以外的JEE服务器上的AEM Forms。 要降低服务器的安全风险，请在JEE上安装AEM Forms后立即应用这些设置。

**安全修补程序**

如果供应商安全补丁和升级未及时应用，则未经授权的用户可能会获得对应用程序服务器的访问权限，这种风险会增加。 在将安全修补程序应用到生产服务器之前，先测试这些修补程序，以确保应用程序的兼容性和可用性。 此外，还应创建策略和程序，以定期检查和安装修补程序。 AEM Forms on JEE更新位于企业产品下载网站上。

**服务帐户（仅Windows上的JBoss统包）**

AEM Forms on JEE默认使用LocalSystem帐户安装服务。 内置的LocalSystem用户帐户具有高级别的可访问性；它属于管理员组。 如果工作进程标识作为LocalSystem用户帐户运行，则该工作进程拥有对整个系统的完全访问权限。

要使用特定的非管理帐户运行部署了JEE上的AEM Forms的应用程序服务器，请按照以下说明操作：

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建本地用户以登录为：

   * 选择&#x200B;**用户无法更改密码**。
   * 在&#x200B;**成员**&#x200B;选项卡上，确保列出&#x200B;**用户**&#x200B;组。

   >[!NOTE]
   >
   >无法更改PDF生成器的此设置。

1. 选择&#x200B;**开始** > **设置** > **管理工具** > **服务**。
1. 双击JEE上的JBoss for AEM Forms并停止服务。
1. 在&#x200B;**登录**&#x200B;选项卡上，选择&#x200B;**此帐户**，浏览您创建的用户帐户，然后输入该帐户的密码。
1. 在MMC中，打开&#x200B;**本地安全设置**，然后选择&#x200B;**本地策略** > **用户权限分配**。
1. 将以下权限分配给表单服务器在下运行的用户帐户：

   * 通过终端服务拒绝登录
   * 拒绝本地登录
   * 以服务身份登录（应已设置）

1. 为新用户帐户授予对以下目录的修改权限：
   * **全局文档存储(GDS)目录**:GDS目录的位置在AEM Forms安装过程中手动配置。如果位置设置在安装期间保持为空，则位置默认为`[JBoss root]/server/[type]/svcnative/DocumentStorage`应用程序服务器安装下的目录
   * **CRX-Repository目录**:默认位置为  `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**:
      * (Windows)在环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录
在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 为以下目录授予新的用户帐户写入权限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss应用程序服务器的默认安装位置：
   > * Windows:C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/

1. 启动应用程序服务器。

**禁用Configuration Manager引导Servlet**

配置管理器使用部署在应用程序服务器上的servlet在JEE数据库上执行AEM Forms的引导。 由于配置管理器在配置完成之前访问此servlet，因此对授权用户的访问尚未获得安全，并且在您成功使用配置管理器在JEE上配置AEM Forms后，应该禁用此Servlet。

1. 解压缩adobe-livecycle-[appserver].ear文件。
1. 打开META-INF/application.xml文件。
1. 搜索adobe-bootstrapper.war部分：

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. 停止AEM Forms服务器。
1. 注释掉adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 战争模块如下：

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. 保存并关闭META-INF/application.xml文件。
1. 压缩EAR文件，并将其重新部署到应用程序服务器。
1. 启动AEM Forms服务器。
1. 在浏览器中键入以下URL以测试更改并确保其不再有效。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**锁定对信任存储的远程访问**

配置管理器允许您将Acrobat Reader DC扩展凭据上传到JEE信任存储上的AEM Forms。 这意味着，默认情况下已启用通过远程协议（SOAP和EJB）访问信任存储凭据服务的功能。 在您使用配置管理器上传权限凭据后或者如果您决定稍后使用管理控制台来管理凭据，则不再需要此访问。

您可以按照[禁用对服务的非基本远程访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)部分中的步骤，禁用对所有信任存储服务的远程访问。

**禁用所有非必需的匿名访问**

某些表单服务器服务具有可由匿名调用者调用的操作。 如果不需要匿名访问这些服务，请按照[禁用对服务的非必要匿名访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)中的步骤禁用它。

#### 更改默认管理员密码 {#change-the-default-administrator-password}

安装JEE上的AEM Forms时，会为用户Super Administrator/login-id Administrator配置一个默认用户帐户，其默认密码为&#x200B;*password*。 您应使用配置管理器立即更改此密码。

1. 在Web浏览器中键入以下URL:

   ```java
   https://[host name]:[port]/adminui
   ```

   默认端口号为以下端口之一：

   **JBoss:** 8080

   **WebLogic服务器：** 7001

   **WebSphere:** 9080。

1. 在&#x200B;**用户名**&#x200B;字段中，键入`administrator`，在&#x200B;**密码**&#x200B;字段中，键入`password`。
1. 单击&#x200B;**设置** > **用户管理** > **用户和组**。
1. 在&#x200B;**Find**&#x200B;字段中键入`administrator`，然后单击&#x200B;**Find**。
1. 从用户列表中单击&#x200B;**Super Administrator**。
1. 单击“编辑用户”页上的&#x200B;**更改密码**。
1. 指定新密码，然后单击&#x200B;**Save**。

此外，还建议通过执行以下步骤来更改CRX管理员的默认密码：

1. 使用默认的用户名/密码登录`https://[server]:[port]/lc/libs/granite/security/content/useradmin.html`。
1. 在搜索字段中键入Administrator ，然后单击&#x200B;**Go**。
1. 从搜索结果中选择&#x200B;**Administrator** ，然后单击用户界面右下方的&#x200B;**编辑**&#x200B;图标。
1. 在&#x200B;**New Password**&#x200B;字段中指定新密码，在&#x200B;**Your Password**&#x200B;字段中指定旧密码。
1. 单击用户界面右下方的保存图标。

#### 禁用WSDL生成 {#disable-wsdl-generation}

Web服务定义语言(WSDL)生成应仅为开发环境启用，开发人员在开发环境中使用WSDL生成来构建其客户端应用程序。 可以选择在生产环境中禁用WSDL生成，以避免公开服务的内部详细信息。

1. 在Web浏览器中键入以下URL:

   ```java
   https://[host name]:[port]/adminui
   ```

1. 单击&#x200B;**设置>核心系统设置>配置**。
1. 取消选择&#x200B;**启用WSDL**&#x200B;并单击&#x200B;**确定**。

### 应用程序服务器安全性 {#application-server-security}

下表介绍了在安装JEE应用程序上的AEM Forms后保护应用程序服务器的一些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>应用程序服务器管理控制台</p> </td> 
   <td><p>在应用程序服务器的JEE上安装、配置和部署AEM Forms后，您应该禁用对应用程序服务器管理控制台的访问。 有关详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>应用程序服务器Cookie设置</p> </td> 
   <td><p>应用程序Cookie由应用程序服务器控制。 部署应用程序时，应用程序服务器管理员可以在服务器范围或特定于应用程序的基础上指定Cookie首选项。 默认情况下，服务器设置会首选。</p> <p>应用程序服务器生成的所有会话Cookie都应包含<code>HttpOnly</code>属性。 例如，使用JBoss应用程序服务器时，可以将SessionCookie元素修改为<code>WEB-INF/web.xml</code>文件中的<code>httpOnly="true"</code>。</p> <p>您可以限制使用仅限HTTPS发送Cookie。 因此，不会通过HTTP发送这些文件并对其进行未加密。 应用程序服务器管理员应全局启用服务器的安全Cookie。 例如，使用JBoss应用程序服务器时，可以将连接器元素修改为<code>server.xml</code>文件中的<code>secure=true</code>。</p> <p>有关Cookie设置的更多详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目录浏览</p> </td> 
   <td><p>当有人请求不存在的页面或请求控制器名称(请求字符串以正斜杠(/)结尾)时，应用程序服务器不应返回该目录的内容。 要防止出现这种情况，您可以禁用应用程序服务器上的目录浏览。 您应该为管理控制台应用程序以及服务器上运行的其他应用程序执行此操作。</p> <p>对于JBoss，请在web.xml文件中将<code>DefaultServlet</code>属性的列表初始化参数的值设置为<code>false</code>，如以下示例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;默认&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;列表&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>对于WebSphere，将ibm-web-ext.xmi文件中的<code>directoryBrowsingEnabled</code>属性设置为<code>false</code>。</p> <p>对于WebLogic，将weblogic.xml文件中的index-directories属性设置为<code>false</code>，如以下示例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 数据库安全 {#database-security}

在保护数据库时，应实施数据库供应商描述的措施。 您应当为数据库用户分配最低要求的数据库权限，该权限授予AEM Forms在JEE上使用的权限。 例如，请勿使用具有数据库管理员权限的帐户。

在Oracle时，您使用的数据库帐户只需要CONNECT、资源和“创建视图”权限。 有关其他数据库的类似要求，请参阅[准备在JEE（单服务器）上安装AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上为JBoss配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改[JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml}以将`integratedSecurity=true`添加到连接URL，如以下示例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径中。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 6.2.1.0驱动程序安装一起找到。
1. 将“从本地系统登录为”的JBoss Windows服务(JBoss for AEM Forms on JEE)属性修改为具有AEM Forms数据库和最低权限集的登录帐户。 如果您从命令行而不是作为Windows服务运行JBoss，则无需执行此步骤。
1. 将&#x200B;**混合**&#x200B;模式的SQL Server安全设置为&#x200B;**仅Windows身份验证**。

#### 在Windows上为WebLogic配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 通过在Web浏览器的URL行中键入以下URL，启动WebLogic服务器管理控制台：

   ```java
   https://[host name]:7001/console
   ```

1. 在“更改中心”下，单击&#x200B;**锁定并编辑**。
1. 在“域结构”下，单击&#x200B;*[base_domain]* > **服务** > **JDBC** > **数据源**，然后在右侧窗格中单击&#x200B;**IDP_DS**。
1. 在下一个屏幕的&#x200B;**Configuration**&#x200B;选项卡上，单击&#x200B;**连接池**&#x200B;选项卡，然后在&#x200B;**Properties**&#x200B;框中，键入`integratedSecurity=true`。
1. 在“域结构”下，单击&#x200B;**[base_domain]** > **服务** > **JDBC** > **数据源**，然后在右侧窗格中单击&#x200B;**RM_DS**。
1. 在下一个屏幕的&#x200B;**Configuration**&#x200B;选项卡上，单击&#x200B;**连接池**&#x200B;选项卡，然后在&#x200B;**Properties**&#x200B;框中，键入`integratedSecurity=true`。
1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径中。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 6.2.1.0驱动程序安装一起找到。
1. 将&#x200B;**混合**&#x200B;模式的SQL Server安全设置为&#x200B;**仅Windows身份验证**。

#### 在Windows上为WebSphere配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，仅当使用外部SQL Server JDBC驱动程序时，才能配置集成安全，而不是使用WebSphere嵌入的SQL Server JDBC驱动程序时。

1. 登录到WebSphere管理控制台。
1. 在导航树中，单击&#x200B;**资源** > **JDBC** > **数据源**，然后在右窗格中单击&#x200B;**IDP_DS**。
1. 在右窗格的“其他属性”下，单击&#x200B;**自定义属性**，然后单击&#x200B;**新建**。
1. 在&#x200B;**名称**&#x200B;框中，键入`integratedSecurity`，在&#x200B;**值**&#x200B;框中，键入`true`。
1. 在导航树中，单击&#x200B;**资源** > **JDBC** > **数据源**，然后在右窗格中单击&#x200B;**RM_DS**。
1. 在右窗格的“其他属性”下，单击&#x200B;**自定义属性**，然后单击&#x200B;**新建**。
1. 在&#x200B;**名称**&#x200B;框中，键入`integratedSecurity`，在&#x200B;**值**&#x200B;框中，键入`true`。
1. 在安装了WebSphere的计算机上，将sqljdbc_auth.dll文件添加到Windows系统路径(C:\Windows)中。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 1.2驱动程序安装位置相同（默认为&#x200B;*[InstallDir]*/sqljdbc_1.2/enu/auth/x86）。
1. 选择&#x200B;**开始** > **控制面板** > **服务**，右键单击WebSphere的Windows服务（IBM WebSphere应用程序服务器&lt;version> - &lt;node>），然后选择&#x200B;**属性**。
1. 在“属性”对话框中，单击&#x200B;**登录**&#x200B;选项卡。
1. 选择&#x200B;**此帐户**&#x200B;并提供设置要使用的登录帐户所需的信息。
1. 在SQL Server上将安全性从&#x200B;**混合**&#x200B;模式设置为&#x200B;**仅Windows身份验证**。

### 保护对数据库中敏感内容的访问 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms数据库模式包含有关系统配置和业务流程的敏感信息，应隐藏在防火墙之后。 数据库应视为与表单服务器位于同一信任边界内。 为防止信息泄漏和业务数据失窃，数据库必须由数据库管理员(DBA)配置，以仅允许授权管理员访问。

为此，应当考虑使用数据库供应商专用工具来加密包含以下数据的表中的列：

* Rights Management文档键
* 信任存储HSM PIN加密密钥
* 本地用户密码哈希

有关特定于供应商的工具的信息，请参阅[&quot;数据库安全信息&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全 {#ldap-security}

轻型目录访问协议(LDAP)目录通常由JEE上的AEM Forms用作企业用户和组信息的源，以及执行密码验证的方法。 您应确保LDAP目录配置为使用安全套接字层(SSL)，并且JEE上的AEM Forms配置为使用其SSL端口访问LDAP目录。

#### LDAP拒绝服务 {#ldap-denial-of-service}

使用LDAP的常见攻击涉及攻击者故意多次未能进行身份验证。 这会强制LDAP目录服务器将用户从所有依赖LDAP的服务中锁定。

您可以设置当用户多次无法对AEM Forms进行身份验证时，AEM Forms实施的失败尝试次数和随后的锁定时间。 在管理控制台中，选择低值。 在选择失败尝试次数时，请务必了解，在进行所有尝试后，AEM Forms会在LDAP目录服务器之前锁定用户。

#### 设置自动帐户锁定 {#set-automatic-account-locking}

1. 登录到管理控制台。
1. 单击&#x200B;**设置** > **用户管理** > **域管理**。
1. 在自动帐户锁定设置下，将&#x200B;**最大连续身份验证失败数**&#x200B;设置为低数，如3。
1. 单击&#x200B;**保存**。

### 审核和日志记录 {#auditing-and-logging}

正确且安全地使用应用程序审核和日志记录有助于确保尽快跟踪和检测安全和其他异常事件。 在应用程序内有效使用审核和日志记录包括跟踪成功登录和失败登录等项目，以及关键应用程序事件（如创建或删除关键记录）。

您可以使用审核来检测多种类型的攻击，包括：

* 暴力密码攻击
* 拒绝服务攻击
* 脚本攻击的恶意输入和相关类的攻击

此表介绍了可用于减少服务器漏洞的审核和日志记录技术。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>日志文件ACL</p> </td> 
   <td><p>在JEE日志文件访问控制列表(ACL)中设置相应的AEM Forms。</p> <p>设置适当的凭据有助于防止攻击者删除文件。</p> <p>对于管理员和系统组，日志文件目录的安全权限应为“完全控制”。 AEM Forms用户帐户应仅具有读取和写入权限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日志文件冗余</p> </td> 
   <td><p>如果资源允许，请实时将日志发送到攻击者无法访问的其他服务器（仅写入），方法是使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他机制。</p> <p>以这种方式保护日志有助于防止篡改。 此外，在中央存储库中存储日志有助于进行关联和监控（例如，如果使用了多个表单服务器，并且在多台计算机上对每台计算机查询密码进行了猜测攻击）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 允许非管理员用户运行PDF生成器

您可以让非管理员用户使用PDF生成器。 通常，只有具有管理权限的用户才能使用PDF生成器。 执行以下步骤，使非管理员用户能够运行PDF生成器：

1. 创建环境变量名称PDFG_NON_ADMIN_ENABLED。

1. 将变量的值设置为TRUE。

1. 重新启动AEM Forms实例。

## 在JEE上配置AEM Forms以访问企业以外的 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安装AEM Forms后，务必定期维护环境的安全性。 本节介绍为维护JEE生产服务器上AEM Forms的安全性而建议执行的任务。

### 为Web访问设置反向代理 {#setting-up-a-reverse-proxy-for-web-access}

可以使用&#x200B;*反向代理*&#x200B;来确保JEE Web应用程序上AEM Forms的一组URL可供外部和内部用户使用。 此配置比允许用户直接连接到JEE上运行AEM Forms的应用程序服务器更加安全。 反向代理为在JEE上运行AEM Forms的应用程序服务器执行所有HTTP请求。 用户只能通过网络访问反向代理，并且只能尝试反向代理支持的URL连接。

**AEM Forms（在JEE根URL上），用于反向代理服务器**

JEE Web应用程序上每个AEM Forms的以下应用程序根URL。 您应该配置反向代理，以便仅向最终用户显示要提供的Web应用程序功能的URL。

某些URL会作为面向最终用户的Web应用程序突出显示。 为了通过反向代理访问外部用户，您应避免公开Configuration Manager的其他URL。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和/或关联的Web应用程序</p> </th> 
   <th><p>基于Web的界面</p> </th> 
   <th><p>最终用户访问权限</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC扩展最终用户web应用程序，用于对PDF文档应用使用权限</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management最终用户Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>用于Rights Management的Web服务URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF生成器管理Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/工作区/*</p> </td> 
   <td><p>工作区最终用户Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>工作区客户端应用程序需要的Servlet和数据服务</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>用于在JEE存储库上引导AEM Forms的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>表单服务器Web服务的信息页</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>所有表单服务器服务的Web服务URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management管理Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>管理控制台主页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>已保护/*</p> </td> 
   <td><p>“信任存储管理”页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Forms IVS应用程序，用于测试和调试表单渲染</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>输出IVS应用在测试和调试输出服务中</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>用于Rights Management的REST URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>输出管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms Web应用程序文件</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>用于在HTML转换期间获取JavaScript</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>用于WebDAV（调试）访问的URL</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>应用程序和服务用户界面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>工作区管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Rest支持页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms on JEE核心配置设置页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>用户管理身份验证</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>用户管理管理界面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>在启用了HTTP文档的SOAP传输或EJB传输上，上传和下载在访问远程端点、SOAP WSDL端点和Java SDK时要处理的文档。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨站点请求伪造攻击 {#protecting-from-cross-site-request-forgery-attacks}

跨站点请求伪造(CSRF)攻击利用网站对用户的信任来传输未经授权和无意的命令。 攻击的设置方式是：在网页中包含链接或脚本，或在电子邮件中包含URL，以访问用户已经通过身份验证的其他网站。

例如，您可能在同时浏览其他网站的同时登录到管理控制台。 其中一个网页可以包括具有`src`属性的HTML图像标记，该属性针对受害者网站上的服务器端脚本。 攻击网站利用Web浏览器提供的基于Cookie的会话身份验证机制，可以向此受害服务器端脚本发送恶意请求，伪装成合法用户。 有关更多示例，请参阅[https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples)。

CSRF具有以下共性：

* 涉及依赖用户身份的网站。
* 利用站点对该身份的信任。
* 诱使用户的浏览器向目标站点发送HTTP请求。
* 涉及具有副作用的HTTP请求。

AEM Forms on JEE使用反向链接过滤器功能阻止CSRF攻击。 本节使用以下术语来描述反向链接过滤机制：

* **允许的反向链接：** 反向链接是指向服务器发送请求的源页面的地址。对于JSP页或表单，反向链接通常是浏览历史记录中的上一页。 图像的反向链接通常是显示图像的页面。 您可以通过将服务器资源添加到允许的反向链接列表来识别允许访问这些资源的反向链接。
* **允许的反向链接例外：** 您可能希望限制允许的反向链接列表中特定反向链接的访问范围。要强制实施此限制，您可以将该反向链接的单个路径添加到允许的反向链接例外列表。 阻止从允许的反向链接例外列表中的路径发起的请求在表单服务器上调用任何资源。 您可以为特定应用程序定义允许的反向链接例外，还可以使用适用于所有应用程序的例外的全局列表。
* **允许的URI:** 这是在不检查反向链接标头的情况下提供的资源列表。例如，不会导致服务器上状态更改的帮助页面，可以将资源添加到此列表。 反向链接筛选器从不阻止允许的URI列表中的资源，而不管反向链接是谁。
* **Null反向链接：** 与父网页无关联或不源自父网页的服务器请求被视为来自Null反向链接的请求。例如，当您打开新的浏览器窗口，键入地址并按Enter时，发送到服务器的反向链接为Null。 桌面应用程序（.NET或SWING）向Web服务器发出HTTP请求，也会向服务器发送空反向链接。

### 反向链接过滤 {#referer-filtering}

反向链接过滤过程可描述如下：

1. 表单服务器检查用于调用的HTTP方法：

   1. 如果是POST，表单服务器将执行反向链接标题检查。
   1. 如果是GET，则Forms服务器会绕过反向链接检查，除非将&#x200B;*CSRF_CHECK_GETS*&#x200B;设置为true，在这种情况下，它会执行反向链接标头检查。 *CSRF_CHECK_GETS是在* 应用程序的web. *xml* 文件中指定的。

1. 表单服务器检查请求的URI是否存在于允许列表中：

   1. 如果URI被列入允许列表，则服务器接受该请求。
   1. 如果未请求的URI列入允许列表，则服务器将检索请求的反向链接。

1. 如果请求中存在反向链接，则服务器会检查它是否为允许的反向链接。 如果允许，则服务器会检查是否存在反向链接异常：

   1. 如果是异常，则阻止请求。
   1. 如果不是例外，则会传递请求。

1. 如果请求中没有反向链接，则服务器会检查是否允许空反向链接：

   1. 如果允许Null反向链接，则会传递请求。
   1. 如果不允许空反向链接，则服务器会检查请求的URI是否为空反向链接的例外，并相应地处理该请求。

### 管理反向链接过滤 {#managing-referer-filtering}

AEM Forms on JEE提供了反向链接过滤器，用于指定允许访问您的服务器资源的反向链接。 默认情况下，反向链接过滤器不会过滤使用安全HTTP方法(例如GET)的请求，除非将&#x200B;*CSRF_CHECK_GETS*&#x200B;设置为true。 如果允许的反向链接条目的端口号设置为0，则JEE上的AEM Forms将允许来自该主机的具有反向链接的所有请求，而不考虑端口号。 如果未指定端口号，则仅允许从默认端口80(HTTP)或端口443(HTTPS)发出请求。 如果删除了允许的反向链接列表中的所有条目，则会禁用反向链接过滤。

首次安装Document Services时，将使用安装Document Services的服务器的地址更新允许的反向链接列表。 服务器的条目包括服务器名称、IPv4地址、启用IPv6时的IPv6地址、环回地址和本地主机条目。 主机操作系统会返回添加到允许的反向链接列表的名称。 例如，IP地址为10.40.54.187的服务器将包含以下条目：`https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`。 对于由主机操作系统重新调整的任何不合格名称（没有IPv4地址、IPv6地址或合格域名的名称），允许列表不会更新。 修改允许的反向链接列表以适合您的业务环境。 请勿在生产环境中使用默认允许的反向链接列表部署表单服务器。 修改任何允许的反向链接、反向链接例外或URI后，确保重新启动服务器以使更改生效。

**管理允许的反向链接列表**

您可以从管理控制台的用户管理界面管理允许的反向链接列表。 用户管理界面提供了创建、编辑或删除列表的功能。 有关使用允许的反向链接列表的更多信息，请参阅&#x200B;*管理帮助*&#x200B;的* [防止CSRF攻击](/help/forms/using/admin-help/preventing-csrf-attacks.md)*部分。

**管理允许的反向链接异常和允许的URI列表**

AEM Forms on JEE提供了用于管理允许的反向链接异常列表和允许的URI列表的API。 您可以使用这些API来检索、创建、编辑或删除列表。 以下是可用API列表：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

有关API的更多信息，请参阅* Jee API参考上的AEM Forms* 。

在全局级别使用&#x200B;***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION***&#x200B;列表，以定义适用于所有应用程序的例外。 此列表仅包含具有绝对路径(例如，`/index.html`)或相对路径(例如`/sample/`)。 您还可以在相对URI(例如，`/sample/(.)*`。

***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION***&#x200B;列表ID在`com.adobe.idp.um.api`命名空间的`UMConstants`类中定义为常量，该类位于`adobe-usermanager-client.jar`中。 您可以使用AEM Forms API创建、修改或编辑此列表。 例如，要创建全局允许的反向链接例外列表，请使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

对于特定于应用程序的异常，请使用&#x200B;***CSRF_ALLOWED_REFERER_EXCEPTIONS***&#x200B;列表。

**禁用反向链接过滤器**

如果反向链接过滤器完全阻止对表单服务器的访问，并且您无法编辑允许的反向链接列表，则可以更新服务器启动脚本并禁用反向链接过滤。

在启动脚本中包含`-Dlc.um.csrffilter.disabled=true` JAVA参数并重新启动服务器。 确保在正确重新配置允许的反向链接列表后删除JAVA参数。

**自定义WAR文件的反向链接过滤**

您可能已创建自定义WAR文件以在JEE上与AEM Forms一起使用，以满足您的业务要求。 要为自定义WAR文件启用反向链接过滤，请在WAR的类路径中包含&#x200B;***adobe-usermanager-client.jar***，并在* web.xml*文件中包含一个过滤器条目，并包含以下参数：

**CSRF_CHECK_GETS控制** 对GET请求进行反向链接检查。如果未定义此参数，则默认值设置为false。 仅当您想要过滤GET请求时，才应包含此参数。

**CSRF_ALLOWED_REFERER_EXCEPTIONS是“允** 许的反向链接例外”列表的ID。反向链接过滤器可阻止来自由列表ID标识的列表中反向链接的请求在表单服务器上调用任何资源。

**CSRF_ALLOWED_URIS_LIST_NAME是** 允许的URI列表的ID。反向链接过滤器不会阻止对列表ID标识的列表中任何资源的请求，而与请求中反向链接标头的值无关。

**当反向链接为空或不存** 在时，CSRF_ALLOW_NULL_REFERER控制反向链接过滤器行为。如果未定义此参数，则默认值设置为false。 仅当您希望允许空反向链接时，才包含此参数。 允许空反向链接可能会允许某些类型的跨站点请求伪造攻击。

**CSRF_NULL_REFERER_EXCEPTIONS是URI的列** 表，当反向链接为空时，不会对其执行反向链接检查。仅当&#x200B;*CSRF_ALLOW_NULL_REFERER*&#x200B;设置为false时，才启用此参数。 在列表中用逗号分隔多个URI。

以下是&#x200B;***SAMPLE*** WAR文件&#x200B;*web.xml*&#x200B;文件中过滤器条目的示例：

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**疑难解答**

如果CSRF筛选器阻止了合法的服务器请求，请尝试以下任一操作：

* 如果被拒绝的请求具有反向链接标头，请仔细考虑将其添加到允许的反向链接列表。 仅添加您信任的反向链接。
* 如果被拒绝的请求没有反向链接标头，请修改您的客户端应用程序以包含反向链接标头。
* 如果客户端可以在浏览器中工作，请尝试该部署模型。
* 作为最后的选择，您可以将资源添加到允许的URI列表。 这不是推荐的设置。

## 安全网络配置 {#secure-network-configuration}

本节介绍AEM Forms on JEE所需的协议和端口，并提供了在安全网络配置中部署AEM Forms on JEE的建议。

### AEM Forms在JEE上使用的网络协议 {#network-protocols-used-by-aem-forms-on-jee}

如上节所述，当您配置安全网络架构时，在JEE上的AEM Forms与企业网络中的其他系统之间进行交互时，需要以下网络协议。

<table> 
 <thead> 
  <tr> 
   <th><p>协议</p> </th> 
   <th><p>用法</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>浏览器显示配置管理器和最终用户Web应用程序</p> </li> 
     <li><p>所有SOAP连接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服务客户端应用程序，如.NET应用程序</p> </li> 
     <li><p>Adobe Reader®在JEE服务器Web服务上使用AEM Forms的SOAP</p> </li> 
     <li><p>AdobeFlash®应用程序使用SOAP来提供表单服务器Web服务</p> </li> 
     <li><p>AEM Forms（在SOAP模式中使用时）</p> </li> 
     <li><p>Workbench设计环境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在企业JavaBeans(EJB)模式中使用时，JEE上的AEM Forms SDK调用</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>基于电子邮件的服务输入（电子邮件端点）</p> </li> 
     <li><p>通过电子邮件发送用户任务通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC文件IO</p> </td> 
   <td><p>AEM Forms on JEE监控已监视文件夹以输入到服务（已监视文件夹端点）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>目录中组织用户和组信息的同步</p> </li> 
     <li><p>交互式用户的LDAP身份验证</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>在使用JDBC服务执行进程期间对外部数据库进行的查询和过程调用</p> </li> 
     <li><p>JEE存储库上的内部访问AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>允许任何WebDAV客户端在JEE设计时存储库（表单、片段等）上远程浏览AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash应用程序，其中JEE服务器服务上的AEM Forms配置了远程处理端点</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms on JEE公开MBean以使用JMX进行监控</p> </td> 
  </tr> 
 </tbody> 
</table>

### 应用程序服务器的端口 {#ports-for-application-servers}

本节介绍支持的每种类型应用程序服务器的默认端口（和备用配置范围）。 必须在内部防火墙上启用或禁用这些端口，具体取决于您希望允许连接到在JEE上运行AEM Forms的应用程序服务器的客户端的网络功能。

>[!NOTE]
>
>默认情况下，服务器会在adobe.com命名空间下公开多个JMX MBean。 只有对服务器运行状况监控有用的信息才会公开。 但是，为防止信息泄露，您应防止不受信任的网络中的呼叫者查找JMX MBean并访问运行状况量度。

**JBoss端口**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>端口</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>访问Web应用程序</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1连接器端口8080</p> <p>AJP 1.3连接器端口8009</p> <p>SSL/TLS连接器端口8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支持</p> </td> 
   <td><p>[JBoss根]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic端口**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>端口</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>访问Web应用程序</p> </td> 
   <td> 
    <ul> 
     <li><p>管理服务器侦听端口：默认值为7001</p> </li> 
     <li><p>管理服务器SSL侦听端口：默认值为7002</p> </li> 
     <li><p>为托管服务器配置的端口，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>在JEE上访问AEM Forms不需要WebLogic管理端口</p> </td> 
   <td> 
    <ul> 
     <li><p>托管服务器侦听端口：可从1到65534进行配置</p> </li> 
     <li><p>托管服务器SSL侦听端口：可从1到65534进行配置</p> </li> 
     <li><p>节点管理器监听端口：默认值为5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere端口**

有关JEE上的AEM Forms所需的WebSphere端口的信息，请转到WebSphere应用程序服务器UI中的端口号设置。

### 配置SSL {#configuring-ssl}

有关JEE物理架构](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)上的AEM Forms部分[中描述的物理架构，您应当为计划使用的所有连接配置SSL。 具体而言，所有SOAP连接都必须通过SSL进行，以防止用户凭据在网络上泄露。

有关如何在JBoss、WebLogic和WebSphere上配置SSL的说明，请参阅[管理帮助](https://www.adobe.com/go/learn_aemforms_admin_64)中的“配置SSL”。

有关如何将证书导入为AEM Forms服务器配置的JVM（Java虚拟机）的说明，请参阅[AEM Forms Workbench帮助](http://www.adobe.com/go/learn_aemforms_workbench_65)中的“相互身份验证”部分。

### 配置SSL重定向 {#configuring-ssl-redirect}

在将应用程序服务器配置为支持SSL后，必须确保对应用程序和服务的所有HTTP流量都强制执行，以使用SSL端口。

要为WebSphere或WebLogic配置SSL重定向，请参阅您的应用程序服务器文档。

1. 打开命令提示符，导航到/JBOSS_HOME/standalone/configuration目录，然后执行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 打开JBOSS_HOME/standalone/configuration/standalone.xml文件进行编辑。

   在&lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素之后，添加以下详细信息：

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. 在https连接器元素中添加以下代码：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存并关闭standalone.xml文件。

## 特定于Windows的安全建议 {#windows-specific-security-recommendations}

本节包含特定于Windows的安全建议，当这些建议用于在JEE上运行AEM Forms时。

### JBoss服务帐户 {#jboss-service-accounts}

默认情况下， JEE上的AEM Forms统包安装使用本地系统帐户来设置服务帐户。 内置的本地系统用户帐户具有高级别的可访问性；它属于管理员组。 如果工作进程标识作为本地系统用户帐户运行，则该工作进程拥有对整个系统的完全访问权限。

#### 使用非管理帐户运行应用程序服务器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建本地用户以登录为：

   * 选择&#x200B;**用户无法更改密码**。
   * 在&#x200B;**成员**&#x200B;选项卡上，确保列出用户组。

1. 选择&#x200B;**设置** > **管理工具** > **服务**。
1. 双击应用程序服务器服务并停止该服务。
1. 在&#x200B;**登录**&#x200B;选项卡上，选择&#x200B;**此帐户**，浏览您创建的用户帐户，然后输入该帐户的密码。
1. 在“本地安全设置”窗口的“用户权限分配”下，为表单服务器在下运行的用户帐户提供以下权限：

   * 通过终端服务拒绝登录
   * 拒绝本地登录xx
   * 以服务身份登录（应已设置）

1. 为新用户帐户授予对以下目录的修改权限：
   * **全局文档存储(GDS)目录**:GDS目录的位置在AEM Forms安装过程中手动配置。如果位置设置在安装期间保持为空，则位置默认为`[JBoss root]/server/[type]/svcnative/DocumentStorage`应用程序服务器安装下的目录
   * **CRX-Repository目录**:默认位置为  `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**:
      * (Windows)在环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录
在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 为以下目录授予新的用户帐户写入权限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss应用程序服务器的默认安装位置：
   > * Windows:C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/。


1. 启动应用程序服务器服务。

### 文件系统安全性 {#file-system-security}

AEM Forms on JEE通过以下方式使用文件系统：

* 存储处理文档输入和输出时使用的临时文件
* 将用于支持已安装解决方案组件的文件存储在全局存档存储中
* 监视文件夹存储从文件系统文件夹位置用作服务输入的已丢弃文件

使用监视文件夹作为通过表单服务器服务发送和接收文档的方式时，请对文件系统安全性采取额外的预防措施。 当用户在已监视文件夹中放置内容时，该内容将通过已监视文件夹公开。 在这种情况下，服务不会验证实际的最终用户。 相反，它依赖在文件夹级别设置的ACL和共享级别安全性来确定谁可以有效地调用服务。

## 特定于JBoss的安全建议 {#jboss-specific-security-recommendations}

本节包含特定于JBoss 7.0.6的应用程序服务器配置建议，当这些建议用于在JEE上运行AEM Forms时。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

在JBoss上的JEE上使用统包安装方法安装AEM Forms时，已配置对JBoss管理控制台和JMX控制台的访问权限（禁用JMX监视）。 如果您使用自己的JBoss应用程序服务器，请确保对JBoss管理控制台和JMX监控控制台的访问是安全的。 在名为jmx-invoker-service.xml的JBoss配置文件中设置对JMX监控控制台的访问权限。

### 禁用目录浏览 {#disable-directory-browsing}

登录到管理控制台后，可以通过修改URL浏览控制台的目录列表。 例如，如果将URL更改为以下URL之一，则可能会显示目录列表：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## 特定于WebLogic的安全建议 {#weblogic-specific-security-recommendations}

本节包含有关在JEE上运行AEM Forms时保护WebLogic 9.1的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-1}

将weblogic.xml文件中的index-directories属性设置为`false`，如以下示例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 启用WebLogic SSL端口 {#enable-weblogic-ssl-port}

默认情况下， WebLogic不启用默认的SSL侦听端口7002。 在配置SSL之前，请在WebLogic服务器管理控制台中启用此端口。

## 特定于WebSphere的安全建议 {#websphere-specific-security-recommendations}

本节包含有关保护在JEE上运行AEM Forms的WebSphere的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-2}

将ibm-web-ext.xml文件中的`directoryBrowsingEnabled`属性设置为`false`。

### 启用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登录到WebSphere管理控制台。
1. 在导航树中，转到&#x200B;**Security** > **Global Security**
1. 选择&#x200B;**启用管理安全**。
1. 取消选择&#x200B;**启用应用程序安全**&#x200B;和&#x200B;**使用Java 2安全**。
1. 单击&#x200B;**确定**&#x200B;或&#x200B;**应用**。
1. 在&#x200B;**消息**&#x200B;框中，单击&#x200B;**直接保存到主控配置**。
