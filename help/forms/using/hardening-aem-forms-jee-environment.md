---
title: 在JEE环境中强化AEM Forms
description: 了解各种安全强化设置，以增强在公司内联网中运行的JEE上的AEM Forms的安全性。
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 451fb472e170a79f9854efadf9be1d4fe0628b94
workflow-type: tm+mt
source-wordcount: '7662'
ht-degree: 1%

---

# 在JEE环境中强化AEM Forms {#hardening-your-aem-forms-on-jee-environment}

了解各种安全强化设置，以增强在公司内联网中运行的JEE上的AEM Forms的安全性。

本文介绍了有关保护在JEE上运行AEM Forms的服务器安全的建议和最佳实践。 这不是针对您的操作系统和应用程序服务器的全面主机强化文档。 本文改为介绍各种安全强化设置，您应该实施这些设置来增强在公司内联网中运行的JEE上的AEM Forms的安全性。 但是，要确保JEE应用程序服务器上的AEM Forms保持安全，您还应该实施安全监控、检测和响应过程。

本文介绍了在安装和配置生命周期的以下阶段中应应用的强化技术：

* **预安装：** 在JEE上安装AEM Forms之前，请使用这些技术。
* **安装：** 在AEM Forms on JEE安装过程中使用这些技术。
* **安装后：** 安装后以及安装后定期使用这些技术。

JEE上的AEM Forms具有高度可自定义性，可以在许多不同的环境中工作。 某些建议可能不符合您组织的需求。

## 预安装 {#preinstallation}

在JEE上安装AEM Forms之前，您可以将安全解决方案应用到网络层和操作系统。 本节介绍了一些问题，并提出了减少这些领域安全漏洞的建议。

**在UNIX和Linux上的安装和配置**

您不应在JEE上使用根shell来安装或配置AEM Forms。 默认情况下，文件安装在/opt目录下，执行安装的用户需要/opt下的所有文件权限。 或者，也可以在单个用户的/user目录下执行安装，在该目录下，用户已经拥有所有文件权限。

**在Windows上的安装和配置**

如果您在JBoss上的JEE上使用turnkey方法安装AEM Forms或者安装PDF Generator，则应该以管理员身份在Windows上执行安装。 此外，在具有本机应用程序支持的Windows上安装PDF Generator时，必须以安装Microsoft Office的同一Windows用户身份运行安装。 有关安装权限的更多信息，请参阅*在JEE上安装和部署AEM Forms*文档以了解您的应用程序服务器。

### 网络层安全性 {#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器的首要威胁之一。 本节将介绍增强网络主机抵御这些漏洞的过程。 它涉及网络分段、传输控制协议/Internet协议(TCP/IP)栈栈强化以及使用防火墙进行主机保护。

下表描述了减少网络安全漏洞的常见流程。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非军事区(DMZ)</p> </td> 
   <td><p>在非军事区(DMZ)中部署Forms服务器。 分段应至少存在两个级别，并且用于在JEE上运行AEM Forms的应用程序服务器应置于内部防火墙之后。 将外部网络与包含Web服务器的DMZ分开，而后者则必须与内部网络分开。 使用防火墙实现分隔层。 对经过每个网络层的流量进行分类并加以控制，以确保仅允许所需数据的绝对最小值。</p> </td> 
  </tr> 
  <tr> 
   <td><p>私有IP地址</p> </td> 
   <td><p>在AEM Forms应用程序服务器上将网络地址转换(NAT)与RFC 1918专用IP地址结合使用。 分配私有IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难以通过Internet在NAT的内部主机之间路由流量。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火墙</p> </td> 
   <td><p>使用以下条件选择防火墙解决方案：</p> 
    <ul> 
     <li><p>实施支持代理服务器和/或 <em>状态检测</em> 而不是简单的数据包过滤解决方案。</p> </li> 
     <li><p>使用支持 <em>拒绝所有服务（明确允许的除外）</em> 安全模式。</p> </li> 
     <li><p>实施双宿主或多宿主的防火墙解决方案。 此体系结构提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙的安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>数据库端口</p> </td> 
   <td><p>请勿使用数据库的默认侦听端口(MySQL - 3306，Oracle- 1521，MS SQL - 1433)。 有关更改数据库端口的信息，请参阅数据库文档。</p> <p>使用其他数据库端口会影响JEE上的整个AEM Forms。 如果更改默认端口，则必须在配置的其他方面(例如JEE上的AEM Forms的数据源)进行相应的修改。</p> <p>有关在JEE上的AEM Forms中配置数据源的信息，请参阅JEE上的安装和升级AEM Forms或在JEE上为您应用程序服务器升级到AEM Forms ，网址为 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms用户指南</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 操作系统安全 {#operating-system-security}

下表介绍了最小化操作系统中的安全漏洞的一些可能方法。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p></th> 
   <th><p>描述</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全修补程序</p></td> 
   <td><p>如果未及时应用供应商的安全补丁程序和升级，则未经授权的用户可能会获得对应用程序服务器的访问权限，这种风险会增加。 在将安全修补程序应用到生产服务器之前，请对其进行测试。</p><p>此外，还可以创建策略和过程以定期检查并安装修补程序。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防护软件</p></td> 
   <td><p>病毒扫描程序可以通过扫描特征码或观察异常行为来识别感染病毒的文件。 扫描仪将病毒特征码保存在文件中，该文件通常存储在本地硬盘上。 由于经常发现新病毒，因此您应该经常为病毒扫描程序更新此文件以识别所有当前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>网络时间协议(NTP)</p></td> 
   <td><p>为了进行取证分析，请在表单服务器上保留准确的时间。 使用NTP同步所有直接连接到Internet的系统上的时间。</p></td> 
  </tr> 
 </tbody> 
</table>

有关操作系统的其他安全信息，请参阅 [操作系统安全信息](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## 安装 {#installation}

此部分介绍在AEM Forms安装过程中可用于减少安全漏洞的技术。 在某些情况下，这些技术会使用安装过程中的选项。 下表描述了这些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>特权</p> </td> 
   <td><p>使用安装软件所需的最少权限。 使用不在Administrators组中的帐户登录到计算机。 在Windows上，您可以使用“运行方式”命令以管理用户的身份运行AEM Forms on JEE安装程序。 在UNIX和Linux系统上，使用命令，例如 <code>sudo</code> 安装软件。</p> </td> 
  </tr> 
  <tr> 
   <td><p>软件源</p> </td> 
   <td><p>请勿在JEE上从不受信任的来源下载或运行AEM Forms。</p> <p>恶意程序可能包含代码，以通过多种方式违反安全性，包括数据盗窃、修改和删除以及拒绝服务。 从AdobeDVD或仅从可信来源在JEE上安装AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁盘分区</p> </td> 
   <td><p>将JEE上的AEM Forms放置在专用磁盘分区上。 磁盘分段是将服务器上的特定数据保留在单独的物理磁盘上的过程，以提高安全性。 以此方式排列数据可降低目录遍历攻击的风险。 计划创建一个独立于系统分区的分区，您可以在该分区上安装AEM Forms on JEE内容目录。 （在Windows上，系统分区包含system32目录或引导分区。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>组件</p> </td> 
   <td><p>评估现有服务并禁用或卸载任何不需要的服务。 请勿安装不必要的组件和服务。</p> <p>应用程序服务器的默认安装可能包含您不需要使用的服务。 您应在部署之前禁用所有不必要的服务，以最大限度地减少攻击的进入点。 例如，在JBoss上，您可以在META-INF/jboss-service.xml描述符文件中注释掉不必要的服务。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略文件</p> </td> 
   <td><p>存在 <code>crossdomain.xml</code> 服务器上的文件可能会立即削弱该服务器。 建议您尽可能限制域列表。 不要放置 <code>crossdomain.xml</code> 使用Guides在开发到生产环境期间使用的文件 <em>（已弃用）</em>. 对于使用Web服务的指南，如果该服务位于提供该指南的同一服务器上，则 <code>crossdomain.xml</code> 根本不需要文件。 但是，如果服务在另一台服务器上，或者如果涉及群集，则存在 <code>crossdomain.xml</code> 文件是必需的。 请参阅 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>，以了解有关crossdomain.xml文件的更多信息。</p> </td> 
  </tr> 
  <tr> 
   <td><p>操作系统安全设置</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，请确保您安装了 <code>pkcs11_softtoken_extra.so</code> 而不是 <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安装后步骤 {#post-installation-steps}

在JEE上成功安装AEM Forms后，请务必从安全角度定期维护环境。

以下部分详细描述了为保护已部署的Forms Server而建议执行的各项任务。

### AEM Forms安全 {#aem-forms-security}

以下推荐设置适用于管理Web应用程序以外的JEE服务器上的AEM Forms 。 要降低服务器的安全风险，请在JEE上安装AEM Forms后立即应用这些设置。

**安全修补程序**

如果未及时应用供应商的安全补丁程序和升级，则未经授权的用户可能获得对应用程序服务器的访问权限的风险会增加。 在将安全修补程序应用于生产服务器之前，请先测试安全修补程序，以确保应用程序的兼容性和可用性。 此外，还可以创建策略和过程以定期检查并安装修补程序。 JEE上的AEM Forms更新位于企业产品下载网站上。

**服务帐户（仅限Windows上的JBoss全包式）**

默认情况下，JEE上的AEM Forms会使用LocalSystem帐户安装服务。 内置LocalSystem用户帐户具有高级别的可访问性；它是Administrators组的一部分。 如果工作进程标识以LocalSystem用户帐户身份运行，则该工作进程具有对整个系统的完全访问权限。

要使用特定的非管理帐户运行部署AEM Forms on JEE的应用程序服务器，请按照以下说明操作：

1. 在Microsoft Management Console (MMC)中，为Forms Server服务创建一个本地用户，以如下方式登录：

   * 选择 **用户无法更改密码**.
   * 在 **成员** 选项卡，确保 **用户** 组已列出。

   >[!NOTE]
   >
   >您无法为PDF Generator更改此设置。

1. 选择 **开始** > **设置** > **管理工具** > **服务**.
1. 双击JEE上适用于AEM Forms的JBoss并停止该服务。
1. 在 **登录** 选项卡，选择 **此帐户**，浏览您创建的用户帐户，然后输入该帐户的密码。
1. 在MMC中，打开 **本地安全设置** 并选择 **本地策略** > **用户权限分配**.
1. 将以下权限分配给运行Forms服务器的用户帐户：

   * 拒绝通过终端服务登录
   * 拒绝本地登录
   * 以服务身份登录（应已设置）

1. 向新用户帐户授予对以下目录的修改权限：
   * **全局文档存储(GDS)目录**：在AEM Forms安装过程中，会手动配置GDS目录的位置。 如果在安装期间位置设置保持为空，则该位置默认为应用程序服务器安装下的目录： `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目录**：默认位置为 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**：
      * (Windows)在环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux) /var/tmp或/usr/tmp
      * (AIX) /tmp或/usr/tmp
      * (Solaris) /var/tmp或/usr/tmp
1. 向新用户帐户授予对以下目录的写入权限：
   * [JBoss-directory]\独立\部署
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的默认安装位置：
   >
   >* Windows： C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux： /opt/jboss/

1. 启动应用程序服务器。

**禁用Configuration Manager引导servlet**

Configuration Manager使用部署在您的应用程序服务器上的servlet对JEE数据库上的AEM Forms执行引导过程。 由于Configuration Manager在配置完成之前访问此servlet，因此授权用户访问它时不会受到保护，并且在您成功使用Configuration Manager在JEE上配置AEM Forms后应该禁用它。

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
1. 注释掉adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 war模块，如下所示：

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
1. 压缩EAR文件并将其重新部署到应用程序服务器。
1. 启动AEM Forms服务器。
1. 在浏览器中键入以下URL以测试更改并确保其不再有效。

   https://&lt;localhost>：&lt;port>/adobe-bootstrapper/bootstrap

**锁定对信任存储区的远程访问**

通过Configuration Manager，您可以将Acrobat Reader DC扩展凭据上传到JEE信任存储区上的AEM Forms 。 这意味着通过远程协议（SOAP和EJB）访问Trust Store Credential Service在默认情况下处于启用状态。 在使用Configuration Manager上载权限凭据或决定稍后使用管理控制台管理凭据后，不再需要此访问。

您可以按照一节中的步骤禁用对所有Trust Store服务的远程访问 [禁用对服务的非必要远程访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**禁用所有非必要的匿名访问**

某些Forms Server服务具有可能被匿名调用者调用的操作。 如果不需要匿名访问这些服务，请按照中的步骤将其禁用 [禁用对服务的非基本匿名访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### 更改默认管理员密码 {#change-the-default-administrator-password}

安装JEE上的AEM Forms后，将为用户Super Administrator/login-id Administrator配置一个默认用户帐户，默认密码为 *密码*. 您应立即使用Configuration Manager更改此密码。

1. 在Web浏览器中键入以下URL：

   ```java
   https://[host name]:[port]/adminui
   ```

   默认端口号为以下端口之一：

   **JBoss：** 8080

   **WebLogic服务器：** 7001

   **WebSphere：** 9080。

1. 在 **用户名** 字段，类型 `administrator` 并且，在 **密码** 字段，类型 `password`.
1. 单击 **设置** > **User Management** > **用户和组**.
1. 类型 `administrator` 在 **查找** 字段，然后单击 **查找**.
1. 单击 **超级管理员** 从用户列表中。
1. 单击 **更改密码** 在“编辑用户”页面上。
1. 指定新密码并单击 **保存**.

此外，建议通过执行以下步骤来更改CRX管理员的默认密码：

1. 登录 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 使用默认用户名/密码。
1. 在搜索字段中键入管理员，然后单击 **开始**.
1. 选择 **管理员** ，然后单击 **编辑** 图标（位于用户界面的右下方）。
1. 在中指定新密码 **新密码** 字段和旧密码 **您的密码** 字段。
1. 单击用户界面右下方的保存图标。

#### 禁用WSDL生成 {#disable-wsdl-generation}

Web服务定义语言(WSDL)生成应该仅对开发环境启用，在这些环境中，开发人员使用WSDL生成来构建其客户端应用程序。 您可以选择在生产环境中禁用WSDL生成，以避免公开服务的内部详细信息。

1. 在Web浏览器中键入以下URL：

   ```java
   https://[host name]:[port]/adminui
   ```

1. 选择 **“设置”>“核心系统设置”>“配置”**.
1. 取消选择 **启用WSDL**，然后选择 **确定**.

### 应用程序服务器安全 {#application-server-security}

下表介绍了在安装AEM Forms on JEE应用程序后保护应用程序服务器的一些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>应用程序服务器管理控制台</p> </td> 
   <td><p>在应用程序服务器上的JEE上安装、配置和部署AEM Forms后，应禁用对应用程序服务器管理控制台的访问。 有关详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>应用程序服务器Cookie设置</p> </td> 
   <td><p>应用程序Cookie由应用程序服务器控制。 在部署应用程序时，应用程序服务器管理员可以基于服务器范围或特定于应用程序指定Cookie首选项。 默认情况下，服务器设置具有优先权。</p> <p>应用程序服务器生成的所有会话Cookie应包括 <code>HttpOnly</code> 属性。 例如，在使用JBoss应用程序服务器时，您可以将SessionCookie元素修改为 <code>httpOnly="true"</code> 在 <code>WEB-INF/web.xml</code> 文件。</p> <p>您可以限制仅使用HTTPS发送Cookie。 因此，它们不会通过HTTP进行未加密发送。 应用程序服务器管理员应在全局基础上为服务器启用安全Cookie。 例如，在使用JBoss Application Server时，可以将连接器元素修改为 <code>secure=true</code> 在 <code>server.xml</code> 文件。</p> <p>有关Cookie设置的更多详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目录浏览</p> </td> 
   <td><p>当有人请求不存在的页面或请求控制器的名称(请求字符串以正斜杠(/)结尾)时，应用程序服务器不应返回该目录的内容。 要防止出现这种情况，您可以在应用程序服务器上禁用目录浏览。 您应该对管理控制台应用程序以及服务器上运行的其他应用程序执行此操作。</p> <p>对于JBoss，请设置 <code>DefaultServlet</code> 属性至 <code>false</code> 在web.xml文件中，如以下示例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;默认&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;列表&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>对于WebSphere，设置 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi文件中的属性 <code>false</code>.</p> <p>对于WebLogic，请将weblogic.xml文件中的index-directories属性设置为 <code>false</code>，如以下示例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 数据库安全 {#database-security}

保护数据库时，您应该实施数据库供应商所述的措施。 您应该分配一个数据库用户，该用户具有最低所需的数据库权限，可供AEM Forms on JEE使用。 例如，不要使用具有数据库管理员权限的帐户。

oracle时，您使用的数据库帐户只需要CONNECT、RESOURCE和CREATE VIEW权限。 有关对其他数据库的类似要求，请参见 [准备在JEE（单服务器）上安装AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### 为Windows上的SQL Server for JBoss配置集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]要添加的\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 到连接URL，如以下示例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径中。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 将本地系统登录身份的JBoss Windows服务(JEE上的AEM Forms的JBoss)属性修改为具有AEM Forms数据库和最小权限集的登录帐户。 如果是从命令行运行JBoss而不是作为Windows服务运行，则无需执行此步骤。
1. 从设置SQL Server的安全性 **混合** 模式至 **仅Windows身份验证**.

#### 为Windows for WebLogic上的SQL Server配置集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 通过在Web浏览器的URL行中键入以下URL来启动WebLogic服务器管理控制台：

   ```java
   https://[host name]:7001/console
   ```

1. 在更改中心下，单击 **锁定并编辑**.
1. 在“域结构”下，单击 *[base_domain]* > **服务** > **JDBC** > **数据源** 在右窗格中，单击 **IDP_DS**.
1. 在下一个屏幕上，在 **配置** 选项卡，单击 **连接池** 选项卡，在 **属性** 框，键入 `integratedSecurity=true`.
1. 在“域结构”下，单击 **[base_domain]** > **服务** > **JDBC** > **数据源** 在右窗格中，单击 **RM_DS**.
1. 在下一个屏幕上，在 **配置** 选项卡，单击 **连接池** 选项卡，在 **属性** 框，键入 `integratedSecurity=true`.
1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径中。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 从设置SQL Server的安全性 **混合** 模式至 **仅Windows身份验证**.

#### 为Windows上的SQL Server for WebSphere配置集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，仅当使用外部SQL Server JDBC驱动程序时，才能配置集成安全性，而不能使用随WebSphere嵌入的SQL Server JDBC驱动程序。

1. 登录到WebSphere管理控制台。
1. 在导航树中，单击 **资源** > **JDBC** > **数据源** 在右窗格中，单击 **IDP_DS**.
1. 在右窗格中的“Additional Properties（其它属性）”下，单击 **自定义属性**，然后单击 **新建**.
1. 在 **名称** 框，键入 `integratedSecurity` 并且，在 **值** 框，键入 `true`.
1. 在导航树中，单击 **资源** > **JDBC** > **数据源** 在右窗格中，单击 **RM_DS**.
1. 在右窗格中的“Additional Properties（其它属性）”下，单击 **自定义属性**，然后单击 **新建**.
1. 在 **名称** 框，键入 `integratedSecurity` 并且，在 **值** 框，键入 `true`.
1. 在安装了WebSphere的计算机上，将sqljdbc_auth.dll文件添加到Windows系统路径(C:\Windows)。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 1.2驱动程序安装位于同一位置(默认为 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86)。
1. 选择 **开始** > **控制面板** > **服务**，右键单击用于WebSphere (IBM WebSphere Application Server)的Windows服务 &lt;version> - &lt;node>)并选择 **属性**.
1. 在“属性”对话框中，单击 **登录** 选项卡。
1. 选择 **此帐户** 并提供设置要使用的登录帐户所需的信息。
1. 从设置SQL Server的安全性 **混合** 模式至 **仅Windows身份验证**.

### 保护对数据库中敏感内容的访问 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms数据库架构包含有关系统配置和业务流程的敏感信息，应隐藏在防火墙之后。 数据库应被视为与Forms服务器处于同一信任边界内。 为了防止信息泄露和业务数据失窃，数据库必须由数据库管理员(DBA)配置，以仅允许授权管理员访问。

作为附加的预防措施，您应该考虑使用特定于数据库供应商的工具来加密包含以下数据的表中的列：

* Rights Management文档密钥
* 信任存储区HSM PIN加密密钥
* 本地用户密码散列

有关特定于供应商的工具的信息，请参见 [数据库安全信息](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP安全 {#ldap-security}

轻型目录访问协议(LDAP)目录通常由AEM Forms on JEE用作企业用户和组信息的源，以及执行口令验证的方法。 您应确保将LDAP目录配置为使用安全套接字层(SSL)，并将JEE上的AEM Forms配置为使用其SSL端口访问LDAP目录。

#### LDAP拒绝服务 {#ldap-denial-of-service}

使用LDAP的常见攻击是指攻击者故意多次未能进行身份验证。 这会强制LDAP目录服务器从所有依赖于LDAP的服务中锁定用户。

您可以设置当用户反复向AEM Forms验证失败时，AEM Forms实施的失败尝试和后续锁定时间的次数。 在“管理控制台”中，选择低值。 在选择失败尝试次数时，请务必了解一点，即在所有尝试完成后，AEM Forms会在LDAP目录服务器尝试之前锁定用户。

#### 设置自动帐户锁定 {#set-automatic-account-locking}

1. 登录到Administration Console。
1. 单击 **设置** > **User Management** > **域管理**.
1. 在“自动帐户锁定设置”下，设置 **最大连续身份验证失败次数** 更改为较低的值，例如3。
1. 单击&#x200B;**保存**。

### 审核和日志记录 {#auditing-and-logging}

正确而安全地使用应用程序审核和日志记录有助于确保尽快跟踪和检测安全和其他异常事件。 在应用程序中有效使用审核和日志记录功能包括跟踪成功和失败的登录以及关键应用程序事件（如创建或删除关键记录）。

您可以使用审核功能检测多种类型的攻击，包括：

* 暴力密码攻击
* 拒绝服务攻击
* 注入恶意输入和脚本攻击的相关类

此表介绍了可用于减少服务器漏洞的审计和日志记录技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>日志文件ACL</p> </td> 
   <td><p>在JEE日志文件访问控制列表(ACL)中设置适当的AEM Forms 。</p> <p>设置适当的凭据有助于防止攻击者删除文件。</p> <p>对于管理员和SYSTEM组，日志文件目录上的安全权限应该是“完全控制”。 AEM Forms用户帐户应仅具有读取和写入权限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日志文件冗余</p> </td> 
   <td><p>如果资源允许，使用Syslog、Tivoli、Microsoft Operations Manager (MOM)服务器或其他机制将日志实时发送到攻击者无法访问的另一台服务器（仅写服务器）。</p> <p>以这种方式保护日志有助于防止篡改。 此外，将日志存储在中央存储库中有助于进行关联和监控（例如，如果正在使用多个表单服务器，并且在多台计算机上发生密码猜测攻击，其中每台计算机都查询密码）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 允许非管理员用户运行PDF Generator

您可以允许非管理员用户使用PDF Generator。 通常，只有具有管理权限的用户才能使用PDF Generator。 执行以下步骤以使非管理员用户能够运行PDF Generator：

1. 创建环境变量名称PDFG_NON_ADMIN_ENABLED。

1. 将变量的值设置为TRUE。

1. 重新启动AEM Forms实例。

## 在JEE上配置AEM Forms以实现企业以外的访问 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安装AEM Forms后，请务必定期维护环境的安全性。 此部分介绍了为维护JEE生产服务器上的AEM Forms的安全而建议执行的任务。

### 为Web访问设置反向代理 {#setting-up-a-reverse-proxy-for-web-access}

A *反向代理* 可用于确保一组用于AEM Forms on JEE Web应用程序的URL可供外部和内部用户使用。 此配置比允许用户直接连接到JEE上运行AEM Forms的应用程序服务器更安全。 反向代理为在JEE上运行AEM Forms的应用程序服务器执行所有HTTP请求。 用户仅具有对反向代理的网络访问权限，并且只能尝试反向代理支持的URL连接。

**JEE根URL上的AEM Forms，用于反向代理服务器**

JEE Web应用程序中每个AEM Forms的以下应用程序根URL。 您应仅配置反向代理，以便公开要提供给最终用户的Web应用程序功能的URL。

某些URL会高亮显示为面向最终用户的Web应用程序。 您应该避免将Configuration Manager的其他URL公开为通过反向代理访问外部用户。

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
   <td><p>Acrobat Reader DC扩展最终用户Web应用程序，用于将使用权限应用于PDF文档</p> </td> 
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
   <td><p>Rights Management的Web服务URL</p> </td> 
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
   <td><p>/workspace/*</p> </td> 
   <td><p>工作区最终用户Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Workspace客户端应用程序所需的Workspace servlet和数据服务</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>用于在JEE存储库中引导AEM Forms的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Forms Server Web服务的信息页面</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>所有Forms Server服务的Web服务URL</p> </td> 
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
   <td><p>“管理控制台”主页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>有抵押/*</p> </td> 
   <td><p>“信任存储区管理”管理页面</p> </td> 
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
   <td><p>用于测试和调试输出服务的输出IVS应用程序</p> </td> 
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
   <td><p>“JEE上的AEM Forms核心配置设置”页面</p> </td> 
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
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>通过启用HTTP文档的SOAP传输或EJB传输上载和下载访问远程端点、SOAP WSDL端点和Java SDK时要处理的文档。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨站点请求伪造攻击 {#protecting-from-cross-site-request-forgery-attacks}

跨站点请求伪造(CSRF)攻击利用网站对用户的信任来传输未经授权且用户无意中的命令。 将链接或脚本包含在网页中，或将URL包含在电子邮件中，以访问用户已验证过的其他站点，从而设置攻击。

例如，您可以在同时浏览其他网站时登录到Administration Console。 其中一个网页可以包含具有一个HTML图像标签的 `src` 定位受攻击网站上的服务器端脚本的属性。 利用Web浏览器提供的基于Cookie的会话认证机制，攻击网站可以伪装成合法用户，向这个受到攻击的服务器端脚本发送恶意请求。 有关更多示例，请参阅 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

以下是CSRF共有的特征：

* 涉及依赖用户身份的网站。
* 利用站点对该标识的信任。
* 欺骗用户的浏览器向目标站点发送HTTP请求。
* 涉及有副作用的HTTP请求。

JEE上的AEM Forms使用反向链接筛选条件功能来阻止CSRF攻击。 此部分中使用以下术语来描述反向链接筛选机制：

* **允许的反向链接：** 反向链接是向服务器发送请求的源页面的地址。 对于JSP页或表单，反向链接通常是浏览历史记录中的上一页。 图像的反向链接通常是显示图像的页面。 您可以通过将允许访问服务器资源的反向链接添加到允许的反向链接列表，来识别这些反向链接。
* **允许的反向链接例外：** 您可能希望限制允许的反向链接列表中特定反向链接的访问范围。 要强制执行此限制，您可以将该反向链接的单个路径添加到“允许的反向链接例外”列表。 阻止从允许的反向链接例外列表中的路径发起的请求调用Forms服务器上的任何资源。 您可以为特定应用程序定义“允许的反向链接例外”，也可以使用适用于所有应用程序的例外全局列表。
* **允许的URI：** 这是无需检查反向链接标头即可提供的资源列表。 可以将资源（例如，不会导致服务器上的状态更改的帮助页面）添加到此列表中。 反向链接筛选器不会阻止允许URI列表中的资源，无论反向链接是谁。
* **Null反向链接：** 与父网页无关或不源自父网页的服务器请求被视为来自Null反向链接的请求。 例如，当您打开新的浏览器窗口，键入地址，然后按Enter键时，发送到服务器的反向链接为空。 向Web服务器发出HTTP请求的桌面应用程序（.NET或SWING）也会向服务器发送Null反向链接。

### 反向链接筛选 {#referer-filtering}

“反向链接筛选”过程可描述如下：

1. Forms服务器检查用于调用的HTTP方法：

   1. 如果POST，Forms服务器将执行反向链接标头检查。
   1. 如果是GET，则Forms服务器会绕过反向链接检查，除非 *CSRF_CHECK_GETS* 设置为true，在这种情况下，它会执行反向链接标头检查。 *CSRF_CHECK_GETS* 指定于 *web.xml* 您的应用程序的文件。

1. Forms服务器检查请求的URI是否存在允许列表：

   1. 如果URI被列入允许列表，则服务器接受请求。
   1. 如果请求的URI未列入允许列表，则服务器检索请求的反向链接。

1. 如果请求中存在Referrer，则服务器会检查它是否为Allowed Referrer。 如果允许，服务器将检查反向链接异常：

   1. 如果出现异常，则请求会被阻止。
   1. 如果不是例外，则会传递请求。

1. 如果请求中没有反向链接，则服务器会检查是否允许使用Null反向链接：

   1. 如果允许使用Null反向链接，则会传递请求。
   1. 如果不允许使用Null反向链接，则服务器会检查请求的URI是否是Null反向链接的例外并相应地处理请求。

### 管理反向链接筛选 {#managing-referer-filtering}

JEE上的AEM Forms提供了一个反向链接筛选条件，用于指定允许访问您的服务器资源的反向链接。 默认情况下，反向链接筛选条件不会筛选使用安全HTTP方法(例如GET)的请求，除非 *CSRF_CHECK_GETS* 设置为true。 如果“允许的反向链接”条目的端口号设置为0，则JEE上的AEM Forms将允许从该主机发起所有包含反向链接的请求，而不管端口号如何。 如果未指定端口号，则仅允许来自默认端口80 (HTTP)或端口443 (HTTPS)的请求。 如果删除了允许的反向链接列表中的所有条目，则会禁用反向链接筛选。

首次安装Document Services时，“允许的反向链接”列表会更新为安装Document Services的服务器上的地址。 服务器的条目包括服务器名称、 IPv4地址、 IPv6地址（如果已启用IPv6） 、环回地址和localhost条目。 添加到允许的反向链接列表中的名称由主机操作系统返回。 例如，IP地址为10.40.54.187的服务器将包括以下条目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 列入允许列表对于主机操作系统返回的任何未限定的名称（没有IPv4地址、IPv6地址或限定的域名的名称），将不更新。 修改允许的反向链接列表以适合您的业务环境。 不要在生产环境中使用默认的“允许的反向链接”列表部署Forms Server。 修改任何允许的反向链接、反向链接异常或URI后，请确保重新启动服务器以使更改生效。

**管理允许的引用列表**

您可以从管理控制台的用户管理界面中管理允许的反向链接列表。 用户管理界面为您提供了创建、编辑或删除列表的功能。 请参阅* [防止CSRF攻击](/help/forms/using/admin-help/preventing-csrf-attacks.md)*部分 *管理帮助* 有关使用允许的反向链接列表的详细信息。

**管理允许的反向链接异常和允许的URI列表**

JEE上的AEM Forms提供了多个API来管理允许的反向链接异常列表和允许的URI列表。 您可以使用这些API检索、创建、编辑或删除列表。 以下是可用API的列表：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

有关API的更多信息，请参阅* AEM Forms on JEE API参考* 。

使用 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 全局层的“允许的反向链接例外”列表，即定义适用于所有应用程序的例外。 此列表仅包含具有绝对路径的URI(例如， `/index.html`)或相对路径(例如， `/sample/`)。 您还可以将正则表达式附加到相对URI的末尾，例如， `/sample/(.)*`.

此 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 列表ID在中定义为常数 `UMConstants` 的类 `com.adobe.idp.um.api` 命名空间，可在 `adobe-usermanager-client.jar`. 您可以使用AEM Forms API创建、修改或编辑此列表。 例如，要创建“全局允许的反向链接例外”列表，请使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用 ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** 特定于应用程序的例外列表。

**禁用反向链接筛选条件**

如果反向链接筛选条件完全阻止对Forms服务器的访问，并且您无法编辑允许的反向链接列表，则可以更新服务器启动脚本并禁用反向链接筛选。

包括 `-Dlc.um.csrffilter.disabled=true` 启动脚本中的JAVA参数并重新启动服务器。 请确保在适当重新配置允许的反向链接列表后删除JAVA参数。

**自定义WAR文件的反向链接筛选**

您可能已创建自定义WAR文件以与AEM Forms on JEE配合使用以满足业务要求。 要为自定义WAR文件启用反向链接筛选，请包括 ***adobe-usermanager-client.jar*** 在WAR的类路径中，并在* web.xml*文件中包含一个过滤器条目，该条目具有以下参数：

**CSRF_CHECK_GETS** 控制对GET请求的反向链接检查。 如果未定义此参数，则默认值设置为false。 仅当您要筛选GET请求时，才应包含此参数。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是允许的反向链接例外列表的ID。 反向链接筛选条件可阻止来自列表ID所标识列表中反向链接的请求，从而防止这些请求在Forms服务器上调用任何资源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是允许的URI列表的ID。 无论请求中的反向链接标头的值如何，反向链接筛选条件都不会阻止针对列表ID所标识的列表中任何资源的请求。

**CSRF_ALLOW_NULL_REFERER** 控制反向链接为null或不存在时的反向链接筛选行为。 如果未定义此参数，则默认值设置为false。 仅当您希望允许Null反向链接时才包含此参数。 允许空反向链接可能会允许某些类型的跨站点请求伪造攻击。

**CSRF_NULL_REFERER_EXCEPTIONS** 是URI列表，当反向链接为null时，不会对其执行反向链接检查。 此参数仅在 *CSRF_ALLOW_NULL_REFERER* 设置为false。 用逗号分隔列表中的多个URI。

以下是 *web.xml* 文件 ***示例*** WAR文件：

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

如果CSRF过滤器阻止了合法的服务器请求，请尝试以下方法之一：

* 如果被拒绝的请求具有反向链接标头，请仔细考虑将其添加到允许的反向链接列表。 仅添加您信任的反向链接。
* 如果被拒绝的请求没有Referrer标头，请修改您的客户端应用程序以包含Referrer标头。
* 如果客户端可以在浏览器中工作，请尝试使用该部署模型。
* 作为最后手段，您可以将资源添加到允许的URI列表中。 建议不要使用此设置。

## 安全网络配置 {#secure-network-configuration}

本节介绍AEM Forms on JEE所需的协议和端口，并提供在安全网络配置中部署AEM Forms on JEE的建议。

### AEM Forms on JEE使用的网络协议 {#network-protocols-used-by-aem-forms-on-jee}

配置安全网络体系结构时（如上一节所述），需要以下网络协议才能在JEE上的AEM Forms与企业网络中的其他系统之间进行交互。

<table> 
 <thead> 
  <tr> 
   <th><p>协议</p> </th> 
   <th><p>使用</p> </th> 
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
     <li><p>Web服务客户端应用程序，如.NET应用程序</p> </li> 
     <li><p>Adobe Reader®对JEE服务器Web服务上的AEM Forms使用SOAP</p> </li> 
     <li><p>AdobeFlash®应用程序使用SOAP进行Forms Server Web服务</p> </li> 
     <li><p>在SOAP模式下使用时，对JEE SDK调用使用AEM Forms</p> </li> 
     <li><p>Workbench设计环境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在Enterprise JavaBeans (EJB)模式下使用时，在JEE SDK调用上使用AEM Forms</p> </td> 
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
   <td><p>AEM Forms on JEE监视用于输入到服务的观察文件夹（观察文件夹端点）</p> </td> 
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
     <li><p>使用JDBC服务执行进程期间对外部数据库进行的查询和过程调用</p> </li> 
     <li><p>内部访问JEE存储库上的AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>支持任何WebDAV客户端在JEE设计时存储库（表单、片段等）上远程浏览AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash应用程序，其中JEE服务器服务上的AEM Forms配置了远程端点</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE上的AEM Forms公开了用于使用JMX进行监视的MBean</p> </td> 
  </tr> 
 </tbody> 
</table>

### 应用程序服务器的端口 {#ports-for-application-servers}

本节介绍支持的每种类型的应用程序服务器的默认端口（和备用配置范围）。 必须在内部防火墙上启用或禁用这些端口，具体取决于您希望允许客户端连接到JEE上运行AEM Forms的应用程序服务器的网络功能。

>[!NOTE]
>
>默认情况下，服务器在adobe.com命名空间下公开多个JMX MBean。 只公开对服务器运行状况监控有用的信息。 但是，为了防止信息泄漏，您应该阻止不受信任网络中的呼叫者查找JMX MBean并访问运行状况量度。

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
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[数据库].xml</p> <p>HTTP/1.1连接器端口8080</p> <p>AJP 1.3连接器端口8009</p> <p>SSL/TLS连接器端口8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支持</p> </td> 
   <td><p>[JBoss根]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>奥斯普洛特3529</p> </td> 
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
     <li><p>为受控服务器配置的端口，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>访问JEE上的AEM Forms不需要WebLogic管理端口</p> </td> 
   <td> 
    <ul> 
     <li><p>受控服务器侦听端口：可从1到65534配置</p> </li> 
     <li><p>托管服务器SSL侦听端口：可从1到65534配置</p> </li> 
     <li><p>Node Manager侦听端口：默认值为5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere端口**

有关AEM Forms on JEE所需的WebSphere端口的信息，请转到WebSphere应用程序服务器UI中的端口号设置。

### 配置SSL {#configuring-ssl}

请参阅一节中介绍的物理体系结构 [AEM Forms on JEE物理架构](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您应该为计划使用的所有连接配置SSL。 具体而言，必须通过SSL执行所有SOAP连接，以防止网络上用户凭据泄露。

有关如何在JBoss、WebLogic和WebSphere上配置SSL的说明，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_64).

有关如何将证书导入为AEM Forms服务器配置的JVM （Java虚拟机）的说明，请参阅中的相互身份验证部分 [AEM Forms Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_65).

### 配置SSL重定向 {#configuring-ssl-redirect}

将应用程序服务器配置为支持SSL后，必须确保对应用程序和服务的所有HTTP通信都强制使用SSL端口。

要为WebSphere或WebLogic配置SSL重定向，请参阅应用程序服务器文档。

1. 打开命令提示符，导航到/JBOSS_HOME/standalone/configuration目录，然后执行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 打开JBOSS_HOME/standalone/configuration/standalone.xml文件进行编辑。

   在 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />域:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素，添加以下详细信息：:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https连接器元素中添加以下代码：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存并关闭独立的.xml文件。

## 特定于Windows的安全建议 {#windows-specific-security-recommendations}

此部分包含在JEE上运行AEM Forms时特定于Windows的安全建议。

### JBoss服务帐户 {#jboss-service-accounts}

AEM Forms on JEE统包安装默认使用Local System帐户设置服务帐户。 内置的本地系统用户帐户具有高级别的可访问性；它是管理员组的一部分。 如果工作进程标识以“本地系统”用户帐户身份运行，则该工作进程具有对整个系统的完全访问权限。

#### 使用非管理帐户运行应用程序服务器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft Management Console (MMC)中，为Forms Server服务创建一个本地用户，以如下方式登录：

   * 选择 **用户无法更改密码**.
   * 在 **成员** 选项卡中，确保列出了Users组。

1. 选择 **设置** > **管理工具** > **服务**.
1. 双击应用程序服务器服务并停止该服务。
1. 在 **登录** 选项卡，选择 **此帐户**，浏览您创建的用户帐户，然后输入该帐户的密码。
1. 在“本地安全设置”窗口的“用户权限分配”下，将以下权限授予运行Forms服务器的用户帐户：

   * 拒绝通过终端服务登录
   * 拒绝在locallyxx上登录
   * 以服务身份登录（应已设置）

1. 向新用户帐户授予对以下目录的修改权限：
   * **全局文档存储(GDS)目录**：在AEM Forms安装过程中，会手动配置GDS目录的位置。 如果在安装期间位置设置保持为空，则该位置默认为应用程序服务器安装下的目录： `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目录**：默认位置为 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms临时目录**：
      * (Windows)在环境变量中设置的TMP或TEMP路径
      * （AIX、Linux或Solaris）登录用户的主目录在基于UNIX的系统上，非根用户可以使用以下目录作为临时目录：
      * (Linux) /var/tmp或/usr/tmp
      * (AIX) /tmp或/usr/tmp
      * (Solaris) /var/tmp或/usr/tmp
1. 向新用户帐户授予对以下目录的写入权限：
   * [JBoss-directory]\独立\部署
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的默认安装位置：
   >
   >* Windows： C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux： /opt/jboss/。

1. 启动应用程序服务器服务。

### 文件系统安全 {#file-system-security}

JEE上的AEM Forms通过以下方式使用文件系统：

* 存储处理文档输入和输出时使用的临时文件
* 将文件存储在全局存档存储区，这些文件用于支持已安装的解决方案组件
* 观察文件夹存储从文件系统文件夹位置用作服务输入的已删除文件

当通过Forms Server服务使用观察文件夹来发送和接收文档时，请采取文件系统安全方面的额外预防措施。 当用户将内容放入watched文件夹时，该内容会通过watched文件夹公开。 在这种情况下，服务不会验证实际的最终用户。 相反，它依赖于在文件夹级别设置的ACL和共享级别安全性来确定谁能够有效地调用服务。

## 特定于JBoss的安全建议 {#jboss-specific-security-recommendations}

此部分包含在JEE上运行AEM Forms时特定于JBoss 7.0.6的应用程序服务器配置建议。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

使用统包安装方法在JBoss上的JEE上安装AEM Forms时，已配置对JBoss管理控制台和JMX控制台的访问（禁用JMX监控）。 如果您使用自己的JBoss应用程序服务器，请确保对JBoss管理控制台和JMX监控控制台的访问权限是安全的。 对JMX监视控制台的访问是在名为jmx-invoker-service.xml的JBoss配置文件中设置的。

### 禁用目录浏览 {#disable-directory-browsing}

登录到Administration Console后，可以通过修改URL来浏览控制台的目录列表。 例如，如果将URL更改为以下URL之一，则可能会显示一个目录列表：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## 特定于WebLogic的安全建议 {#weblogic-specific-security-recommendations}

此部分包含在JEE上运行AEM Forms时用于保护WebLogic 9.1安全的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-1}

将weblogic.xml文件中的index-directories属性设置为 `false`，如以下示例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 启用WebLogic SSL端口 {#enable-weblogic-ssl-port}

默认情况下，WebLogic不启用默认的SSL侦听端口7002。 在配置SSL之前，请在WebLogic服务器管理控制台中启用此端口。

## 特定于WebSphere的安全建议 {#websphere-specific-security-recommendations}

此部分包含用于保护在JEE上运行AEM Forms的WebSphere的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-2}

设置 `directoryBrowsingEnabled` 属性。 `false`.

### 启用WebSphere管理安全 {#enable-websphere-administrative-security}

1. 登录到WebSphere管理控制台。
1. 在导航树中，转到 **安全性** > **全局安全**
1. 选择 **启用管理安全性**.
1. 取消选择两者 **启用应用程序安全** 和 **使用Java 2安全性**.
1. 单击 **确定** 或 **应用**.
1. 在 **消息** 框中，单击 **直接保存到主配置**.
