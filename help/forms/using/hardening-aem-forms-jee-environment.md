---
title: 强化您对JEEAEM Forms的环境
seo-title: 强化您对JEEAEM Forms的环境
description: 了解各种安全强化设置，以增强在公司内部网中运行的JEE上AEM Forms的安全性。
seo-description: 了解各种安全强化设置，以增强在公司内部网中运行的JEE上AEM Forms的安全性。
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 36c9b3d60331e7482655bc8039153b6b86d721f9
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 0%

---


# 强化您对JEEAEM Forms的环境 {#hardening-your-aem-forms-on-jee-environment}

了解各种安全强化设置，以增强在公司内部网中运行的JEE上AEM Forms的安全性。

本文描述了保护在JEE上运行AEM Forms的服务器的建议和最佳实践。 这对于您的操作系统和应用程序服务器来说不是一个全面的主机强化文档。 相反，本文描述了您应实施的各种安全强化设置，以增强在公司内部网中运行的JEE上AEM Forms的安全性。 但是，为确保JEE应用程序服务器上的AEM Forms保持安全，您还应实施安全监控、检测和响应过程。

本文描述了在安装和配置生命周期的以下阶段应用的强化技术：

* **预安装：** 在JEE上安装AEM Forms之前，请使用这些技术。
* **安装：** 在JEE安装过程的AEM Forms中使用这些技术。
* **安装后：** 安装后使用这些技术，然后定期使用。

JEE上的AEM Forms可以高度自定义，并可以在许多不同的环境中工作。 某些建议可能不符合您组织的需求。

## 预安装 {#preinstallation}

在JEE上安装AEM Forms之前，您可以将安全解决方案应用到网络层和操作系统。 本节介绍一些问题，并就减少这些领域的安全漏洞提出建议。

**在UNIX和Linux上安装和配置**

您不应使用根外壳程序在JEE上安装或配置AEM Forms。 默认情况下，文件安装在/opt目录下，执行安装的用户需要/opt下的所有文件权限。 或者，也可以在用户已拥有所有文件权限的/user目录下进行安装。

**在Windows上安装和配置**

如果要在JBoss上的JEE上使用统包方法安装AEM Forms，或者要安装PDF生成器，则应以管理员身份在Windows上进行安装。 此外，在具有本机应用程序支持的Windows上安装PDF Generator时，必须以安装Microsoft Office的同一Windows用户身份运行安装。 有关安装权限的详细信息，请参阅*在JEE上安装和部署AEM Forms*文档，该适用于您的应用程序服务器。

### 网络层安全 {#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一。 本节介绍针对这些漏洞强化网络上主机的过程。 它解决了网络分段、传输控制协议／因特网协议(TCP/IP)栈加固以及使用防火墙保护主机的问题。

下表描述了减少网络安全漏洞的常用进程。

<table> 
 <thead> 
  <tr> 
   <th><p>带有 OS 剪贴板</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非军事区(DMZ)</p> </td> 
   <td><p>在非军事区(DMZ)中部署表单服务器。 分段至少应存在于两个级别中，应用程序服务器用于在位于内部防火墙后的JEE上运行AEM Forms。 将外部网络与包含Web服务器的DMZ分离，而Web服务器又必须与内部网络分离。 使用防火墙实现分层。 对通过每个网络层的流量进行分类和控制，以确保仅允许所需数据的绝对最小值。</p> </td> 
  </tr> 
  <tr> 
   <td><p>专用IP地址</p> </td> 
   <td><p>将网络地址转换(NAT)与AEM Forms应用程序服务器上的RFC 1918专用IP地址结合使用。 指定专用IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难通过Internet将通信路由到NAT内部主机和从NAT内部主机发送通信。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火墙</p> </td> 
   <td><p>使用以下条件选择防火墙解决方案：</p> 
    <ul> 
     <li><p>实施支持代理服务器和／或状态检 <em>查的防火墙</em> ，而不是简单的数据包过滤解决方案。</p> </li> 
     <li><p>使用防火墙，它支持拒绝除 <em>明确允许的安全范式外的所</em> 有服务。</p> </li> 
     <li><p>实施双宿主或多宿主防火墙解决方案。 此体系架构提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙安全。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>数据库端口</p> </td> 
   <td><p>请勿对数据库使用默认监听端口(MySQL - 3306、Oracle - 1521、MS SQL - 1433)。 有关更改数据库端口的信息，请参阅数据库文档。</p> <p>使用不同的AEM Forms库端口会影响JEE配置的整体数据。 如果更改默认端口，则必须在配置的其他区域进行相应的修改，如JEE上的AEM Forms的数据源。</p> <p>有关在JEE上的AEM Forms中配置数据源的信息，请参阅《AEM Forms用户指南》中的“在JEE上安装并升级AEM Forms”或“升级到JEE上的AEM Forms”(针对您的应用 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">程序服务器)</a>。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 操作系统安全 {#operating-system-security}

下表描述了一些使操作系统中发现的安全漏洞最小化的潜在方法。

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
   <td><p>如果供应商安全补丁和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问的风险增加。 在将安全修补程序应用到生产服务器之前，先测试这些安全修补程序。</p><p>此外，还可以创建定期检查和安装修补程序的策略和程序。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防护软件</p></td> 
   <td><p>病毒扫描程序可以通过扫描签名或监视异常行为来识别感染病毒的文件。 扫描程序将其病毒签名保留在文件中，该文件通常存储在本地硬盘上。 由于经常发现新的病毒，您应该经常为病毒扫描程序更新此文件以识别所有当前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>网络时间协议(NTP)</p></td> 
   <td><p>要进行取证分析，请在表单服务器上保持准确的时间。 使用NTP同步直接连接到Internet的所有系统上的时间。</p></td> 
  </tr> 
 </tbody> 
</table>

有关操作系统的其他安全信息，请 [参阅“操作系统安全信息”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安装 {#installation}

本节介绍在AEM Forms安装过程中可用于减少安全漏洞的技术。 在某些情况下，这些技术会使用作为安装过程一部分的选项。 下表介绍了这些技术。

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
   <td><p>使用安装软件所需的最少权限数。 使用管理员组中不存在的帐户登录到计算机。 在Windows上，您可以使用“运行方式”命令以管理用户身份在JEE安装程序上运行AEM Forms。 在UNIX和Linux系统上，使用诸如 <code>sudo</code> 的命令安装软件。</p> </td> 
  </tr> 
  <tr> 
   <td><p>软件源</p> </td> 
   <td><p>请勿从不受信任的来源下载或运行JEE上的AEM Forms。</p> <p>恶意项目可能包含以多种方式违反安全性的代码，包括数据盗窃、修改和删除以及拒绝服务。 在JEE上从Adobe DVD或仅从可信源安装AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁盘分区</p> </td> 
   <td><p>将AEM Forms放在JEE上的专用磁盘分区上。 磁盘分段是一个过程，它将服务器上的特定数据保留在单独的物理磁盘上，以增加安全性。 这样安排数据可以降低目录遍历攻击的风险。 计划创建与系统分区分开的分区，您可以在该分区上安装JEE内容目录上的AEM Forms。 （在Windows上，系统分区包含system32目录或引导分区。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>组件</p> </td> 
   <td><p>评估现有服务并禁用或卸载任何不需要的服务。 请勿安装不必要的组件和服务。</p> <p>应用程序服务器的默认安装可能包含您使用时不需要的服务。 在部署之前，您应禁用所有不必要的服务，以最大限度地减少攻击的入口点。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符文件中注释掉不必要的服务。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略文件</p> </td> 
   <td><p>服务器上存在 <code>crossdomain.xml</code> 文件可能会立即削弱该服务器。 建议您尽可能限制域的列表。 使用参考 <code>crossdomain.xml</code> 线时，不要将开发过程中使用的文件放 <em>入生产中</em>。 对于使用Web服务的指南，如果该服务位于提供该指南的同一台服务器上，则根 <code>crossdomain.xml</code> 本不需要文件。 但是，如果服务位于另一台服务器上，或者如果涉及群集，则需 <code>crossdomain.xml</code> 要存在文件。 有关 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">crossdomain</a>.xml文件的详细信息，请参阅https://kb2.adobe.com/cps/142/tn_14213.html。</p> </td> 
  </tr> 
  <tr> 
   <td><p>操作系统安全设置</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，请确保安装而不是 <code>pkcs11_softtoken_extra.so</code> 安装 <code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安装后步骤 {#post-installation-steps}

在JEE上成功安装AEM Forms后，必须从安全角度定期维护环境。

以下部分详细描述了建议保护已部署的表单服务器的不同任务。

### AEM Forms安全 {#aem-forms-security}

以下推荐设置适用于JEE服务器上非管理Web应用程序的AEM Forms。 要降低服务器的安全风险，请在JEE上安装AEM Forms后立即应用这些设置。

**安全修补程序**

如果供应商安全修补程序和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问权限的风险增加。 在将安全修补程序应用到生产服务器之前，先测试它们，以确保应用程序的兼容性和可用性。 此外，还可以创建定期检查和安装修补程序的策略和程序。 JEE更新的AEM Forms可以访问企业产品下载站点。

**服务帐户（仅限Windows上的JBoss turnkey）**

JEE上的AEM Forms默认情况下使用LocalSystem帐户安装服务。 内置的LocalSystem用户帐户具有高级别的可访问性； 它是管理员组的一部分。 如果工作进程标识作为LocalSystem用户帐户运行，则该工作进程对整个系统具有完全访问权限。

要使用特定的非管理帐户运行部署JEE上的AEM Forms的应用程序服务器，请按照以下说明操作：

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建一个本地用户以登录：

   * 选择 **用户无法更改密码**。
   * 在“成 **员** ”选项卡上，确保列 **出“** 用户”组。

   >[!NOTE]
   >
   >无法更改PDF生成器的此设置。

1. 选择 **开始** >设 **置** >管 **理工具** > **** Services。
1. 多次-单击JEE上的AEM Forms的JBoss并停止该服务。
1. 在“登 **录** ”选项卡上，选 **择“此帐户**”，浏览您创建的用户帐户，然后输入帐户的口令。
1. 在MMC中，打开“ **本地安全设置** ”，然 **后选择“本地策略** ”>“ **用户权限分配”**。
1. 为运行表单服务器的用户帐户分配以下权限：

   * 通过终端服务拒绝登录
   * 拒绝本地登录
   * 以服务身份登录（应已设置）

1. 为以下目录赋予新用户帐户修改权限：
   * **全局文档存储(GDS)目录**: 在AEM Forms安装过程中，将手动配置GDS目录的位置。 如果安装过程中位置设置保持为空，则位置默认为应用程序服务器安装位置下的目录 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目录**: 默认位置为 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**:
      * (Windows)环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 为以下目录赋予新用户帐户写入权限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的默认安装位置：
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/

1. 开始应用程序服务器。

**禁用Configuration Manager引导servlet**

配置管理器使用部署在应用程序服务器上的servlet执行JEEAEM Forms库上的引导。 由于配置管理器在配置完成前访问此servlet，因此对其的访问尚未得到授权用户的保护，并且在您成功使用配置管理器配置JEE上的AEM Forms后，应禁用它。

1. 解压缩adobe-livecycle-[appserver].ear文件。
1. 打开META-INF/application.xml文件。
1. 搜索adobe-bootstrapper.war部分：

   ```as3
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

   ```as3
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
1. 开始AEM Forms服务器。
1. 在浏览器中键入以下URL以测试更改并确保其不再工作。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**锁定对信任存储的远程访问**

Configuration Manager允许您将Acrobat Reader DC扩展凭据上传到JEE信任存储上的AEM Forms。 这意味着，默认情况下已启用通过远程协议（SOAP和EJB）访问信任存储凭据服务。 使用Configuration Manager上传权限凭据后，或者如果您决定稍后使用管理控制台管理凭据，则不再需要此访问。

您可以按照禁用对服务的非基本远程访问部分中的步骤，禁 [用对所有信任存储服务的远程访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)。

**禁用所有非基本匿名访问**

某些表单服务器服务具有可由匿名调用者调用的操作。 如果不需要匿名访问这些服务，请按照禁用非基本匿名 [访问服务中的步骤禁用](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)。

#### 更改默认管理员密码 {#change-the-default-administrator-password}

安装JEE上的AEM Forms后，将为用户Super Administrator/login-id Administrator配置一个默认用户帐户，默认密码为 *密码*。 您应立即使用配置管理器更改此密码。

1. 在Web浏览器中键入以下URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

   默认端口号是以下任一端口号：

   **JBoss:** 8080

   **WebLogic服务器：** 7001

   **WebSphere:** 9080。

1. 在“用 **户名** ”字段中， `administrator` 键入并在“口 **令** ”字段中键入 `password`。
1. 单击 **设置** >用 **户管理** >用 **户和用户组**。
1. 在“ `administrator` 查找 **”字** 段中键入 **，然后单击“**&#x200B;查找”。
1. 单击 **用户列表** 中的“超级管理员”。
1. 单击 **“编辑用户** ”页面上的“更改口令”。
1. 指定新密码，然后单击“ **保存**”。

此外，还建议通过执行以下步骤来更改CRX Administrator的默认密码：

1. 使用默 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 认的用户名／密码登录。
1. 在搜索字段中键入Administrator，然后单击“ **开始**”。
1. 从搜 **索结果** 中选择Administrator（管理员），然后 **单击** User Interface右下方的Edit（编辑）图标。
1. 在“新密码”字 **段中指定** 新密码，在“密码”字 **段中指定旧密码** 。
1. 单击用户界面右下方的“保存”图标。

#### 禁用WSDL生成 {#disable-wsdl-generation}

Web服务定义语言(WSDL)生成应仅对开发环境启用，开发者使用WSDL生成来构建其客户端应用程序。 您可以选择在生产环境中禁用WSDL生成，以避免暴露服务的内部详细信息。

1. 在Web浏览器中键入以下URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

1. 单击 **设置>核心系统设置>配置**。
1. 取消选 **择“启用WSDL** ”，然后 **单击“确定**”。

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
   <td><p>在应用程序服务器上的JEE上安装、配置和部署AEM Forms后，您应禁用对应用程序服务器管理控制台的访问。 有关详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>应用程序服务器Cookie设置</p> </td> 
   <td><p>应用程序Cookie由应用程序服务器控制。 部署应用程序时，应用程序服务器管理员可以指定服务器范围或特定于应用程序的cookie首选项。 默认情况下，服务器设置为首选项。</p> <p>由应用程序服务器生成的所有会话cookie都应包含该 <code>HttpOnly</code> 属性。 例如，使用JBoss Application Server时，可以将SessionCookie元素修改为 <code>httpOnly="true"</code> 文件 <code>WEB-INF/web.xml</code> 中。</p> <p>您可以限制使用仅HTTPS发送Cookie。 因此，不会通过HTTP发送未加密的文件。 应用程序服务器管理员应全局为服务器启用安全cookie。 例如，使用JBoss Application Server时，可以将连接器元素修改为 <code>secure=true</code> 文件 <code>server.xml</code> 中的。</p> <p>有关Cookie设置的更多详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目录浏览</p> </td> 
   <td><p>当有人请求不存在的页面或请求控制器的名称(请求字符串以正斜杠(/)结尾)时，应用程序服务器不应返回该目录的内容。 要防止这种情况发生，您可以禁用应用程序服务器上的目录浏览。 您应该为管理控制台应用程序和服务器上运行的其他应用程序执行此操作。</p> <p>对于JBoss，将属性的列表初始化参 <code>DefaultServlet</code> 数的值 <code>false</code> 设置为web.xml文件中，如下例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>对于WebSphere，将 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi文件中的属性设置为 <code>false</code>。</p> <p>对于WebLogic，将weblogic.xml文件中的index-directories属性设置为 <code>false</code>，如以下示例所示：</p> <p>&lt;容器描述符&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/容器描述符&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 数据库安全 {#database-security}

在保护数据库时，应执行数据库供应商描述的度量。 您应当为AEM Forms分配具有允许在JEE上使用的最低数据库权限的数据库用户。 例如，请勿使用具有数据库管理员权限的帐户。

在Oracle上，您使用的视图库帐户只需要CONNECT、RESOURCE和CREATE权限。 有关其他AEM Forms库的类似要求， [请参阅准备在JEE（单台服务器）上安装](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上为JBoss配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修 [改JBOSS_]HOME\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 以添加到连接URL，如本例所示：

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 将“从本地系统登录为”的JBoss Windows服务(JBoss forAEM Forms在JEE上)属性修改为具有AEM Forms数据库和最少权限集的登录帐户。 如果您从命令行而不是作为Windows服务运行JBoss，则无需执行此步骤。
1. 将SQL Server的安全性从混 **合模式** 设置 **为仅Windows身份验证**。

#### 在Windows上为WebLogic配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 开始WebLogic服务器管理控制台，方法是在Web浏览器的URL行中键入以下URL:

   ```as3
   https://[host name]:7001/console
   ```

1. 在“更改中心”下，单 **击“锁定并编辑”**。
1. 在“域结构”下，单 *[击“基域]* ” > **Services** > **JDBC** > **Data Sources** ，并在右侧窗 ****&#x200B;格中单击IDP ，再单击IDP。
1. 在下一个屏幕的“配 **置** ”选项卡上，单 **击“连接池** ”选项卡，在“属 **性”框中** ，键入 `integratedSecurity=true`。
1. 在“域结构”下，单 **[击“基域]** ” > **Services** > **JDBC** > **Data Sources** ，然后在右 ****&#x200B;窗格中单击DS RM。
1. 在下一个屏幕的“配 **置** ”选项卡上，单 **击“连接池** ”选项卡，在“属 **性”框中** ，键入 `integratedSecurity=true`。
1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 将SQL Server的安全性从混 **合模式** 设置 **为仅Windows身份验证**。

#### 在Windows上为WebSphere配置SQL Server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有使用外部SQL Server JDBC驱动程序（而非嵌入WebSphere的SQL Server JDBC驱动程序）时，才能配置集成安全性。

1. 登录到WebSphere管理控制台。
1. 在导航树中，单 **击** “资 **源** ” > **JDBC** > **Data Sources**，然后在右窗格中单击IDP_DS。
1. 在右侧窗格的“其他属性”下，单击“自 **定义属性**”，然后单击“ **新建”**。
1. 在“名 **称** ”框中，键 `integratedSecurity` 入并在“值” **框中** 键入 `true`。
1. 在导航树中，单 **击** “资 **源** ” > **JDBC** > **Data Sources**，在右窗格中单击RM_DS。
1. 在右侧窗格的“其他属性”下，单击“自 **定义属性**”，然后单击“ **新建”**。
1. 在“名 **称** ”框中，键 `integratedSecurity` 入并在“值” **框中** 键入 `true`。
1. 在安装WebSphere的计算机上，将sqljdbc_auth.dll文件添加到Windows系统路径(C:\Windows)。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 1.2驱动程序安装位置相同(默 *[认为]* InstallDir/sqljdbc_1.2/enu/auth/x86)。
1. 选择 **“开始** ” **>“控制面板** ”>“服务”，右键单击WebSphere的Windows服务(IBM WebSphere Application Server &lt;version> - &lt;node>)，然后选择 ******** Properties。
1. 在“属性”对话框中，单击“登 **录”选** 项卡。
1. 选 **择此帐户** ，并提供设置要使用的登录帐户所需的信息。
1. 将SQL Server上的安全性从混 **合模式** 设置 **为仅Windows身份验证**。

### 保护对数据库中敏感内容的访问 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms模式库包含有关系统配置和业务流程的敏感信息，应隐藏在防火墙后。 应将数据库考虑在与表单服务器相同的信任边界内。 要防止信息泄露和业务数据失窃，必须由数据库管理员(DBA)配置数据库以仅允许授权管理员访问。

为了增加预防措施，您应考虑使用数据库供应商特定工具来加密表中包含以下数据的列：

* Rights Management文档键
* 信任存储HSM PIN加密密钥
* 本地用户密码哈希

有关供应商特定工具的信息，请参 [阅“数据库安全信息”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全性 {#ldap-security}

轻量级目录访问协议(LDAP)目录通常由JEE上的AEM Forms用作企业用户和组信息的源以及执行口令身份验证的方法。 您应确保将LDAP目录配置为使用安全套接字层(SSL)，并将JEE上的AEM Forms配置为使用其SSL端口访问LDAP目录。

#### LDAP拒绝服务 {#ldap-denial-of-service}

使用LDAP的常见攻击涉及攻击者故意多次无法进行身份验证。 这会强制LDAP目录服务器将用户从所有依赖LDAP的服务中锁定。

您可以设置AEM Forms在用户反复无法向AEM Forms进行身份验证时执行的失败尝试次数和随后的锁定时间。 在管理控制台中，选择低值。 在选择失败尝试次数时，请务必了解，在进行所有尝试后，AEM Forms会在LDAP目录服务器尝试之前锁定用户。

#### 设置自动帐户锁定 {#set-automatic-account-locking}

1. 登录到管理控制台。
1. 单击 **设置** >用 **户管理** > **域管理**。
1. 在“自动帐户锁定设置” **下，将“最大连续身份验证失败** ”设置为一个低数，如3。
1. 单击&#x200B;**保存**。

### 审核和记录 {#auditing-and-logging}

正确、安全地使用应用程序审计和记录有助于确保尽快跟踪和检测安全性和其他异常事件。 有效使用应用程序中的审核和日志记录包括跟踪成功和失败登录等项目，以及关键应用程序事件，如创建或删除关键记录。

您可以使用审核来检测多种类型的攻击，包括：

* 暴力密码攻击
* 拒绝服务攻击
* 恶意输入和相关类脚本攻击的注入

此表介绍了可用于减少服务器漏洞的审计和日志记录技术。

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
   <td><p>为JEE日志文件访问控制列表(ACL)设置适当的AEM Forms。</p> <p>设置适当的凭据有助于防止攻击者删除文件。</p> <p>日志文件目录上的安全权限应为管理员和系统组的完全控制权。 AEM Forms用户帐户应仅具有“读取”和“写入”权限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日志文件冗余</p> </td> 
   <td><p>如果资源允许，则通过使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他机制将日志实时发送到攻击者无法访问的其他服务器（仅写入）。</p> <p>这样保护日志有助于防止篡改。 此外，将日志存储在中央存储库有助于进行关联和监控（例如，当多个表单服务器正在使用，并且密码猜测攻击正在跨多台计算机进行，其中每台计算机都被查询密码）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 使非管理员用户能运行PDF生成器

您可以允许非管理员用户使用PDF生成器。 通常，只有具有管理权限的用户才能使用PDF生成器。 执行以下步骤，使非管理员用户能运行PDF生成器：

1. 创建环境变量名PDFG_NON_ADMIN_ENABLED。

1. 将变量的值设置为TRUE。

1. 重新启动AEM表单实例。

## 在JEE上配置AEM Forms，以便在企业之外进行访问 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安装AEM Forms后，务必定期维护环境的安全。 本节介绍建议哪些任务可以维护JEE生产服务器上AEM Forms的安全性。

### 为Web访问设置反向代理 {#setting-up-a-reverse-proxy-for-web-access}

反向 *代理* ，可用于确保外部和内部用户均可使用JEE Web应用程序上AEM Forms的一组URL。 此配置比允许用户直接连接到JEE上AEM Forms正在运行的应用程序服务器更安全。 反向代理对正在JEE上运行AEM Forms的应用程序服务器执行所有HTTP请求。 用户只能通过网络访问反向代理，并且只能尝试反向代理支持的URL连接。

**JEE根URL上的AEM Forms与反向代理服务器一起使用**

JEE Web应用程序上每个AEM Forms的以下应用程序根URL。 您应配置反向代理，仅向最终用户提供Web应用程序功能的URL。

某些URL会高亮显示为面向最终用户的Web应用程序。 您应避免暴露Configuration Manager的其他URL，以便通过反向代理访问外部用户。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和／或关联的Web应用程序</p> </th> 
   <th><p>基于Web的界面</p> </th> 
   <th><p>最终用户访问</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC扩展用于将使用权限应用于PDF文档的最终用户Web应用程序</p> </td> 
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
   <td><p>Web服务URL，用于权限管理</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator管理Web应用程序</p> </td> 
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
   <td><p>工作区客户端应用程序需要的工作区Servlet和数据服务</p> </td> 
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
   <td><p>/TruststoreComponent/</p> <p>安全/*</p> </td> 
   <td><p>“信任存储管理”页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>用于测试和调试表单渲染的Forms IVS应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>输出IVS应用程序以测试和调试输出服务</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>用于权限管理的REST URL</p> </td> 
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
   <td><p>表单Web应用程序文件</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>用于在HTML转换过程中获取JavaScript</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>表单管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV（调试）访问的URL</p> </td> 
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
   <td><p>其余支持页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>“JEE核心配置设置”页上的AEM Forms</p> </td> 
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
   <td><p>用户管理界面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>在启用HTTP文档的SOAP传输或EJB传输中，上传和下载在访问远程端点、SOAP WSDL端点和Java SDK时要处理的文档。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨站点请求伪造攻击 {#protecting-from-cross-site-request-forgery-attacks}

跨站点请求伪造(CSRF)攻击利用网站对用户的信任来传输未经授权和用户无意的命令。 通过在网页中包含链接或脚本或电子邮件中的URL来设置攻击，以访问用户已通过身份验证的其他站点。

例如，您可能在同时浏览其他网站时登录到管理控制台。 网页之一可以包括HTML图像标签，该HTML图像标 `src` 签具有目标受害者网站上的服务器端脚本的属性。 通过利用Web浏览器提供的基于cookie的会话身份验证机制，攻击网站可以向此受害服务器端脚本发送恶意请求，伪装成合法用户。 有关更多示例，请参 [阅https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples)。

CSRF共有以下特征：

* 涉及依赖用户身份的站点。
* 利用站点对该身份的信任。
* 诱骗用户的浏览器向目标站点发送HTTP请求。
* 涉及具有副作用的HTTP请求。

JEE上的AEM Forms使用推荐人过滤器功能来阻止CSRF攻击。 本节中使用以下术语来描述推荐人过滤机制：

* **允许的推荐人:** 推荐人是向服务器发送请求的源页面的地址。 对于JSP页或表单，推荐人通常是浏览历史记录中的上一页。 图像的推荐人通常是显示图像的页面。 您可以通过将服务器资源添加到允许的推荐人列表来标识允许访问的推荐人。
* **允许的推荐人例外：** 您可能希望在允许的推荐人列表中限制特定推荐人的访问范围。 要强制实施此限制，您可以将该推荐人的单个路径添加到允许的推荐人例外列表。 禁止从允许推荐人异常列表中的路径发出的请求调用表单服务器上的任何资源。 您可以为特定应用程序定义允许的推荐人例外，还可以使用适用于所有应用程序的例外的全局列表。
* **允许的URI:** 这是一列表资源，无需检查推荐人头即可提供。 例如，帮助页面可以添加到此列表中，这些资源不会导致服务器上的状态更改。 “允许的URI”列表中的资源不会被推荐人过滤器阻止，而不管推荐人是谁。
* **空推荐人:** 未与父网页关联或未从父网页源出的服务器请求被视为来自Null推荐人的请求。 例如，当您打开新的浏览器窗口，键入地址并按Enter时，发送到服务器的推荐人为null。 向Web服务器发出HTTP请求的桌面应用程序（.NET或SWING）也会向服务器发送空推荐人。

### 推荐人过滤 {#referer-filtering}

推荐人过滤过程可以描述如下：

1. 表单服务器检查用于调用的HTTP方法：

   1. 如果是POST，表单服务器将执行推荐人头检查。
   1. 如果它为GET，则表单服务器将绕过推荐人检查，除非 *将CSRF_CHECK_GETS* 设置为true，在这种情况下，它将执行推荐人头检查。 *CSRF_CHECK_GETS在* web.xml文 *件中为应用程* 序指定。

1. 表单服务器检查请求的URI是否存在于允许列表中：

   1. 如果已列入允许列表URI，则服务器接受该请求。
   1. 如果未已列入允许列表请求的URI，则服务器检索请求的推荐人。

1. 如果请求中有推荐人，服务器将检查它是否为允许推荐人。 如果允许，服务器将检查推荐人异常：

   1. 如果此请求为例外，则阻止该请求。
   1. 如果不是例外，则会通过请求。

1. 如果请求中没有推荐人，服务器将检查是否允许空推荐人:

   1. 如果允许Null推荐人，则会传递请求。
   1. 如果不允许Null推荐人，则服务器检查所请求的URI是否为Null推荐人的例外，并相应地处理该请求。

### 管理推荐人过滤 {#managing-referer-filtering}

JEE上的AEM Forms提供推荐人过滤器以指定允许访问服务器资源的推荐人。 默认情况下，推荐人过滤器不过滤使用安全HTTP方法（如GET）的请求，除非 *将CSRF_CHECK_GETS* 设置为true。 如果允许的推荐人项的端口号设置为0，则JEE上的AEM Forms将允许来自该主机的所有具有推荐人的请求，而不管端口号。 如果未指定端口号，则仅允许来自默认端口80(HTTP)或端口443(HTTPS)的请求。 如果“允许的推荐人”列表中的所有条目都被删除，则“推荐人过滤”将被禁用。

首次安装文档服务时，允许的推荐人列表将更新为安装文档服务的服务器的地址。 服务器的条目包括服务器名称、IPv4地址、启用IPv6时的IPv6地址、环回地址和localhost条目。 添加到允许的推荐人列表的名称由主机操作系统返回。 例如，IP地址为10.40.54.187的服务器将包括以下条目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 对于由主机操作系统重新调整的任何非限定名称（没有IPv4地址、IPv6地址或限定域名的名称）允许列表将不更新。 修改允许的推荐人列表以适合您的业务环境。 请勿在生产环境中使用默认的允许推荐人列表部署表单服务器。 修改任何允许的推荐人、推荐人例外或URI后，请确保重新启动服务器以使更改生效。

**管理允许的推荐人列表**

您可以从管理控制台的用户管理界面管理允许的推荐人列表。 用户管理界面为您提供创建、编辑或删除列表的功能。 有关使用“允 [许的推荐人](/help/forms/using/admin-help/preventing-csrf-attacks.md)”列表的 *更多信息，请参* 阅管理帮助的*防止CSRF攻击*一节。

**管理允许的推荐人异常和允许的URI列表**

JEE上的AEM Forms提供API来管理允许的推荐人异常列表和允许的URI列表。 您可以使用这些API检索、创建、编辑或删除列表。 以下是可用API的列表:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

有关API的更多信息，请参阅* JEE API参考AEM Forms*。

在全局 ***级别对允许的推荐人异常使用LC_GLOBAL_ALLOWED_REFERER*** _EXCEPTION列表，即定义适用于所有应用程序的异常。 此列表只包含具有绝对路径(例如， `/index.html`)或相对路径(例如， `/sample/`)。 您还可以在相对URI的末尾附加一个常规表达式，例如， `/sample/(.)*`.

LC_ ***GLOBAL_ALLOWED_REFERER_EXCEPTION*** 列表ID在命名空间的类中 `UMConstants` 定义为常 `com.adobe.idp.um.api` 数，位于 `adobe-usermanager-client.jar`。 您可以使用AEM FormsAPI创建、修改或编辑此列表。 例如，要创建“全局允许推荐人例外”列表，请使用：

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

对于特 ***定于应用程序的异常，请使用CSRF_ALLOWED_REFERER*** _EXCEPTIONS列表。

**禁用推荐人筛选器**

在推荐人过滤器完全阻止访问表单服务器且您无法编辑允许的推荐人列表的事件下，您可以更新服务器启动脚本并禁用推荐人过滤。

在启动 `-Dlc.um.csrffilter.disabled=true` 脚本中包含JAVA参数并重新启动服务器。 确保在正确重新配置“允许”推荐人列表后删除JAVA参数。

**自定义WAR文件的推荐人过滤**

您可能已创建自定义WAR文件以与JEE上的AEM Forms协作，以满足您的业务要求。 要为自定义WAR文件启用推荐人过滤，请 ***在WAR的类路径中包含adobe-usermanager-client*** .jar，并在* web.xml*文件中包含一个包含以下参数的过滤器条目：

**CSRF_CHECK_GETS控制** GET请求的推荐人检查。 如果未定义此参数，则默认值将设置为false。 仅当要过滤GET请求时，才包含此参数。

**CSRF_ALLOWED_REFERER_EXCEPTIONS是“允许的推荐人例外”列表的ID。** 推荐人筛选器可阻止来自推荐人ID所标识列表中的列表的请求在表单服务器上调用任何资源。

**CSRF_ALLOWED_URIS_列表** _NAME是允许的URI列表的ID。 推荐人筛选器不会阻止对由列表ID标识的列表中任何资源的请求，而不管请求中推荐人头的值如何。

**CSRF_ALLOW_NULL_REFERER** 控制推荐人过滤器行为(当推荐人为null或不存在)。 如果未定义此参数，则默认值将设置为false。 仅当要允许Null推荐人时，才包含此参数。 允许空推荐人可能允许某些类型的跨站点请求伪造攻击。

**CSRF_NULL_REFERER_EXCEPTIONS** 是URI的列表，当推荐人为null时，不对其执行推荐人检查。 仅当CSRF_ALLOW_ *NULL_REFERER设置为false时* ，才启用此参数。 在列表中用逗号分隔多个URI。

以下是SAMPLE WAR文件web.xml *文件中的* filter项 ***的示例*** :

```as3
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

如果CSRF过滤器阻止了合法服务器请求，请尝试以下任一方法：

* 如果拒绝的请求具有推荐人头，请仔细考虑将其添加到允许的推荐人列表。 仅添加您信任的推荐人。
* 如果拒绝的请求没有推荐人头，请修改您的客户端应用程序以包含推荐人头。
* 如果客户端可以在浏览器中工作，请尝试该部署模型。
* 作为最后的选择，您可以将资源添加到允许的URI列表。 这不是推荐的设置。

## 安全网络配置 {#secure-network-configuration}

本节介绍JEEAEM Forms所需的协议和端口，并为在安全网络配置中部署JEEAEM Forms提供建议。

### AEM Forms在JEE上使用的网络协议 {#network-protocols-used-by-aem-forms-on-jee}

如前一节所述，配置安全网络架构时，JEE上的AEM Forms与企业网络中的其他系统之间的交互需要以下网络协议。

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
     <li><p>浏览器显示Configuration Manager和最终用户Web应用程序</p> </li> 
     <li><p>所有SOAP连接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服务客户端应用程序，如。NET应用程序</p> </li> 
     <li><p>Adobe Reader®将SOAP用于JEE服务器Web服务上的AEM Forms</p> </li> 
     <li><p>Adobe Flash®应用程序使用SOAP提供表单服务器Web服务</p> </li> 
     <li><p>AEM Forms在SOAP模式下使用时JEE SDK调用</p> </li> 
     <li><p>工作台设计环境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在Enterprise JavaBeans(EJB)模式中使用时JEE SDK调用的AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>向服务输入基于电子邮件的内容（电子邮件端点）</p> </li> 
     <li><p>通过电子邮件发送用户任务通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC文件IO</p> </td> 
   <td><p>AEM FormsJEE监视已监视文件夹以输入服务（已监视文件夹端点）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>同步目录中的组织用户和组信息</p> </li> 
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
   <td><p>支持任何WebDAV客户端在JEE设计时存储库（表单、片段等）上远程浏览AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe Flash应用程序，其中JEE服务器服务上的AEM Forms配置了远程处理端点</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE上的AEM Forms显示MBean以使用JMX进行监视</p> </td> 
  </tr> 
 </tbody> 
</table>

### 应用程序服务器的端口 {#ports-for-application-servers}

本节介绍支持的每种类型的应用程序服务器的默认端口（和备用配置范围）。 必须在内部防火墙上启用或禁用这些端口，具体取决于您希望允许连接到运行JEEAEM Forms的应用程序服务器的客户端的网络功能。

>[!NOTE]
>
>默认情况下，服务器在adobe.com命名空间下显示多个JMX MBean。 仅公开对服务器运行状况监视有用的信息。 但是，为了防止信息泄露，您应防止不可信网络中的呼叫者查找JMX MBean并访问运行状况指标。

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
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
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
     <li><p>Admin Server侦听端口： 默认值为7001</p> </li> 
     <li><p>Admin Server SSL侦听端口： 默认值为7002</p> </li> 
     <li><p>为Managed Server配置的端口，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>访问JEE上的AEM Forms不需要WebLogic管理端口</p> </td> 
   <td> 
    <ul> 
     <li><p>受控服务器侦听端口： 可配置1到65534</p> </li> 
     <li><p>受控服务器SSL侦听端口： 可配置1到65534</p> </li> 
     <li><p>节点管理器监听端口： 默认为5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere端口**

有关JEE上AEM Forms需要的WebSphere端口的信息，请转到WebSphere应用程序服务器UI中的端口号设置。

### 配置SSL {#configuring-ssl}

有关JEE物理架构的部分AEM Forms中 [描述的物理架构](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您应为计划使用的所有连接配置SSL。 具体而言，所有SOAP连接都必须通过SSL进行，以防止用户凭据暴露在网络上。

有关如何在JBoss、WebLogic和WebSphere上配置SSL的说明，请参阅管理帮助中的“配置 [SSL”](https://www.adobe.com/go/learn_aemforms_admin_64)。

### 配置SSL重定向 {#configuring-ssl-redirect}

在将应用程序服务器配置为支持SSL后，必须确保应用程序和服务的所有HTTP通信都强制使用SSL端口。

要为WebSphere或WebLogic配置SSL重定向，请参阅应用程序服务器文档。

1. 打开命令提示符，导航到/JBOSS_HOME/standalone/configuration目录并执行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 打开JBOSS_HOME/standalone/configuration/standalone.xml文件进行编辑。

   在&lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素后，添加以下详细信息：

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https连接器元素中添加以下代码：

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存并关闭standalone.xml文件。

## 特定于Windows的安全建议 {#windows-specific-security-recommendations}

本节包含在JEE上运行AEM Forms时特定于Windows的安全建议。

### JBoss服务帐户 {#jboss-service-accounts}

JEE统包安装的AEM Forms默认使用本地系统帐户设置服务帐户。 内置的本地系统用户帐户具有高度的可访问性； 它是管理员组的一部分。 如果工作进程标识作为本地系统用户帐户运行，则该工作进程对整个系统具有完全访问权限。

#### 使用非管理帐户运行应用程序服务器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建一个本地用户以登录：

   * 选择 **用户无法更改密码**。
   * 在“成 **员** ”选项卡上，确保列出用户组。

1. 选择 **设置** > **管理工具** > **服**&#x200B;务。
1. 多次单击应用程序服务器服务并停止该服务。
1. 在“登 **录** ”选项卡上，选 **择“此帐户**”，浏览您创建的用户帐户，然后输入帐户的口令。
1. 在“本地安全设置”窗口的“用户权限分配”下，为表单服务器在下运行的用户帐户授予以下权限：

   * 通过终端服务拒绝登录
   * 拒绝本地xx登录
   * 以服务身份登录（应已设置）

1. 为以下目录赋予新用户帐户修改权限：
   * **全局文档存储(GDS)目录**: 在AEM Forms安装过程中，将手动配置GDS目录的位置。 如果安装过程中位置设置保持为空，则位置默认为应用程序服务器安装位置下的目录 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目录**: 默认位置为 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**:
      * (Windows)环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 为以下目录赋予新用户帐户写入权限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的默认安装位置：
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/。


1. 开始应用程序服务器服务。

### 文件系统安全性 {#file-system-security}

JEE上的AEM Forms通过以下方式使用文件系统：

* 存储处理文档输入和输出时使用的临时文件
* 将文件存储在全局存档存储中，这些存储用于支持已安装的解决方案组件
* 监视文件夹存储已丢弃的文件，这些文件用作文件系统文件夹位置中服务的输入

使用监视的文件夹作为通过表单服务器服务发送和接收文档的方式时，请在文件系统安全性方面采取额外的预防措施。 当用户删除监视文件夹中的内容时，该内容会通过监视文件夹公开。 在这种情况下，服务不会验证实际的最终用户。 而是依赖ACL和共享级别安全性来在文件夹级别进行设置，以确定谁可以有效调用服务。

## 特定于JBoss的安全建议 {#jboss-specific-security-recommendations}

本节包含特定于JBoss 7.0.6(当用于在JEE上运行AEM Forms时)的应用程序服务器配置建议。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

在JBoss上的JEE上使用统包安装方法安装AEM Forms时，已配置对JBoss管理控制台和JMX控制台的访问（禁用JMX监视）。 如果您使用自己的JBoss Application Server，请确保对JBoss管理控制台和JMX监控控制台的访问是安全的。 在名为jmx-invoker-service.xml的JBoss配置文件中设置对JMX监视控制台的访问权限。

### 禁用目录浏览 {#disable-directory-browsing}

登录到管理控制台后，可以通过修改URL浏览控制台的目录列表。 例如，如果将URL更改为以下URL之一，则可能会显示目录列表：

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## 特定于WebLogic的安全建议 {#weblogic-specific-security-recommendations}

本节包含在JEE上运行AEM Forms时保护WebLogic 9.1的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-1}

将weblogic.xml文件中的index-directories属性设置为 `false`，如以下示例所示：

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 启用WebLogic SSL端口 {#enable-weblogic-ssl-port}

默认情况下，WebLogic不启用默认的SSL侦听端口7002。 在配置SSL之前，请在WebLogic服务器管理控制台中启用此端口。

## 特定于WebSphere的安全建议 {#websphere-specific-security-recommendations}

本节包含用于保护在JEE上运行AEM Forms的WebSphere的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-2}

将ibm- `directoryBrowsingEnabled` web-ext.xml文件中的属性设置为 `false`。

### 启用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登录到WebSphere管理控制台。
1. 在导航树中，转到“安全 **性** ”>“ **全局安全性”**
1. 选择 **启用管理安全**。
1. 取消选择“ **启用应用程序安** 全 **性”和“使用Java 2安全性”**。
1. 单击 **确定** 或 **应用**。
1. 在“消 **息** ”框中，单 **击“直接保存至主控配置”**。