---
title: 安全核对清单
seo-title: 安全核对清单
description: 了解配置和部署AEM时的各种安全注意事项。
seo-description: 了解配置和部署AEM时的各种安全注意事项。
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Security Checklist {#security-checklist}

本节介绍您应采取的各种步骤，以确保部署AEM时的安全安装。 清单应自上而下应用。

>[!NOTE]
>
>还有关 [于由Open web应用程序安全项目(OWASP)发布的最危险安全威胁的更多信息](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)。

>[!NOTE]
>
>在开发阶段，还 [有一些其他安](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 全注意事项。

## 主要安全措施 {#main-security-measures}

### 在生产就绪模式下运行AEM {#run-aem-in-production-ready-mode}

有关详细信息，请参 [阅在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)。

### 为传输层安全启用HTTPS {#enable-https-for-transport-layer-security}

对于具有安全实例，必须在创作和发布实例上启用HTTPS传输层。

>[!NOTE]
>
>有关详细 [信息，请参阅启用HTTP over SSL](/help/sites-administering/ssl-by-default.md) 一节。

### 安装安全修补程序 {#install-security-hotfixes}

确保您已安装Adobe提供的 [最新安全修补程序](https://helpx.adobe.com/experience-manager/kb/aem63-available-hotfixes.html)。

### 更改AEM和OSGi Console管理帐户的默认密码 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe强烈建议在安装后更改特权 [**AEM **`admin`帐户的口令](#changing-the-aem-admin-password)（在所有实例上）。

这些帐户包括：

* AEM帐 `admin` 户

   更改AEM管理员帐户的密码后，您在访问CRX时需要使用新密码。

* OSGi `admin` Web控制台的口令

   此更改还将应用于用于访问Web控制台的管理员帐户，因此您在访问该控制台时需要使用相同的口令。

这两个帐户使用单独的凭据，并且每个帐户都具有不同的强口令，这对于安全部署至关重要。

#### 更改AEM管理员密码 {#changing-the-aem-admin-password}

AEM管理员帐户的密码可通过 [Granite Operations - Users控制台进行更改](/help/sites-administering/granite-user-group-admin.md) 。

您可以在此编辑 `admin` 帐户并 [更改密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。

>[!NOTE]
>
>更改管理员帐户也会更改OSGi web控制台帐户。 更改管理员帐户后，您应将OSGi帐户更改为其他帐户。

#### 更改OSGi web控制台口令的重要性 {#importance-of-changing-the-osgi-web-console-password}

除AEM帐户外， `admin` 如果无法更改OSGi web控制台密码的默认密码，则可能会导致：

* 在启动和关闭期间，使用默认密码暴露服务器（对于大型服务器，可能需要几分钟）;
* 当存储库关闭／重新启动捆绑并且OSGI正在运行时，服务器暴露。

有关更改Web控制台口令的详细信息，请参 [阅以下更改OSGi web控制台管理员口令](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 。

#### 更改OSGi web控制台管理员密码 {#changing-the-osgi-web-console-admin-password}

您还必须更改用于访问Web控制台的口令。 这是通过配置 [Apache Felix OSGi管理控制台的以下属性来完成的](/help/sites-deploying/osgi-configuration-settings.md):

**用户名** 和 **密码**，用于访问Apache Felix web管理控制台本身的凭据。
初始安装后必须更改密码，以确保实例的安全性。

要执行此操作：

1. 导航到位于的Web控制台 `<server>:<port>/system/console/configMgr`。
1. 导航到 **Apache Felix OSGi Management Console** ，并更改用 **户名和** 密码 ****。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 单击&#x200B;**保存**。

### 实现自定义错误处理程序 {#implement-custom-error-handler}

Adobe建议定义自定义错误处理程序页面，尤其是404和500个HTTP响应代码，以防止信息泄露。

>[!NOTE]
>
>有关更 [多详细信息，请参阅如何创建自定义脚本或错误处理程序](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) 知识库文章。

### 完整的调度程序安全清单 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您的基础架构的关键部分。 Adobe强烈建议您填写调度程序安 [全核对清单](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html)。

>[!CAUTION]
>
>使用调度程序时，必须禁用“.form”选择器。

## 验证步骤 {#verification-steps}

### Configure replication and transport users {#configure-replication-and-transport-users}

AEM的标准安装指定 `admin` 为默认复制代理内的传输凭据 [用户](/help/sites-deploying/replication.md)。 此外，管理员用户还用于在作者系统上源复制。

出于安全考虑，应将两者都更改为反映手头的特定用例，同时考虑以下两个方面：

* 传输 **用户不应** 是管理员用户。 相反，在发布系统上设置仅对发布系统的相关部分具有访问权限的用户，并将该用户的凭据用于传输。

   您可以从捆绑的复制接收者用户开始，并配置此用户的访问权限以匹配您的情况

* 复 **制用户** 或代 **** 理用户Id不应是管理员用户，而应是只能查看应被复制内容的用户。 复制用户用于收集要在创作系统上复制的内容，然后再将其发送到发布者。

### 检查Operations Dashboard安全性运行状况检查 {#check-the-operations-dashboard-security-health-checks}

AEM 6引入了新的操作控制板，旨在帮助系统操作员解决问题并监控实例的运行状况。

仪表板还附带一组安全运行状况检查。 建议您在与生产实例一起上线之前检查所有安全运行状况检查的状态。 有关详细信息，请参阅 [Operations Dashboard文档](/help/sites-administering/operations-dashboard.md)。

### 检查示例内容是否存在 {#check-if-example-content-is-present}

所有示例内容和用户（例如Geometrixx项目及其组件）应在生产系统上完全卸载和删除，然后才能公开访问。

>[!NOTE]
>
>如果此实例在生产就绪模式下运行，则删除示例We.Retail应 [用程序](/help/sites-administering/production-ready.md)。 如果由于任何原因，情况并非如此，您可以通过转到“包管理器”，然后搜索并卸载所有We.Retail包来卸载示例内容。 有关详细信息，请参 [阅使用包](package-manager.md)。

### 检查CRX开发包是否存在 {#check-if-the-crx-development-bundles-are-present}

应先在创作和发布生产系统上卸载这些开发OSGi捆绑包，然后才能访问它们。

* Adobe CRXDE支持（com.adobe.granite.crxde支持）
* Adobe Granite CRX Explorer(com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite(com.adobe.granite.crxde-lite)

### 检查Sling开发包是否存在 {#check-if-the-sling-development-bundle-is-present}

适用 [](/help/sites-developing/aem-eclipse.md) 于Eclipse的AEM开发人员工具部署了Apache Sling工具支持安装(org.apache.sling.tooling.support.install)。

应在创作和发布生产系统上卸载此OSGi捆绑包，然后才能使其可访问。

### 防止跨站点请求伪造 {#protect-against-cross-site-request-forgery}

#### CSRF保护框架 {#the-csrf-protection-framework}

AEM 6.1附带一种机制，可帮助防止跨站点请求伪造攻击，该机制称为 **CSRF保护框架**。 有关如何使用它的详细信息，请查阅 [文档](/help/sites-developing/csrf-protection.md)。

#### Sling Referrer过滤器 {#the-sling-referrer-filter}

要解决CRX webDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，您需要为引用过滤器添加配置以使用它。

引用过滤器服务是允许您配置的OSGi服务：

* 应过滤哪些http方法
* 是否允许空的引用标题
* 以及除服务器主机外还允许的服务器白名单。

默认情况下，绑定到服务器的所有localhost变体和当前主机名都在白名单中。

要配置引用过滤器服务，请执行以下操作：

1. 打开Apache Felix控制台(**配置**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 登录名 `admin`为。
1. 在“配 **置** ”菜单中，选择：

   `Apache Sling Referrer Filter`

1. 在字段 `Allow Hosts` 中，输入所有允许作为引用的主机。 每个条目都必须是表单

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允许来自此服务器的所有请求以及给定端口。
   * 如果还要允许https请求，则必须输入第二行。
   * 如果允许来自该服务器的所有端口，则可 `0` 以用作端口号。

1. 如果要 `Allow Empty` 允许空／缺少引用标题，请选中该字段。

   >[!CAUTION]
   >
   >建议在使用命令行工具（如）时提供引 `cURL` 用，而不是允许空值，因为该值可能会使系统受到CSRF攻击。

1. 编辑此过滤器应用于对字段进行检查的方 `Filter Methods` 法。

1. 单击 **保存** ，以保存更改。

### OSGI设置 {#osgi-settings}

某些OSGI设置是默认设置，以便更轻松地调试应用程序。 您需要在发布和创作生产实例时更改这些内容，以避免内部信息泄露给公众。

>[!NOTE]
>
>除Day CQ WCM调试过滤器 **外，以下所有设置都自动由生产就绪模** 式覆盖 [](/help/sites-administering/production-ready.md)。 因此，我们建议在生产环境中部署实例之前先查看所有设置。

对于以下每项服务，都需要更改指定的设置：

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 启用 **Minify** （删除CRLF和空格字符）。
   * 启 **用Gzip** （允许通过一个请求对文件进行压缩和访问）。
   * 禁用调 **试**
   * 禁用时 **间**

* [Day CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消选中 **启用**

* [Day CQ WCM过滤器](/help/sites-deploying/osgi-configuration-settings.md):

   * 仅在发布时，将 **WCM模式设置为** “disabled”

* [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 禁用“ **生成调试信息”**

* [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 禁用“ **生成调试信息”**
   * 禁用映 **射的内容**

有关更多详细信息，请 [参阅OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## 进一步阅读 {#further-readings}

### 减轻拒绝服务(DoS)攻击 {#mitigate-denial-of-service-dos-attacks}

拒绝服务(DoS)攻击是使计算机资源对其目标用户不可用的尝试。 这通常是通过超载资源实现的；例如：

* 来自外部源的大量请求。
* 请求的信息量超出系统可以成功传送的信息量。

   例如，整个存储库的JSON表示形式。

* 通过请求具有不限数量URL的内容页面，URL可以包括句柄、某些选择器、扩展和后缀——其中任何一个都可以修改。

   例如，也 `.../en.html` 可以请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`
   调度程序将缓存所有有效的变量（例如，返回响应并配置为缓存），最终导致完整的文件系统，并且不提供用于进一步请求的服务。 `200`

有许多用于防止此类攻击的配置点，此处我们仅讨论与AEM直接相关的配置点。

**配置Sling以防止DoS**

Sling以内 *容为中心*。 这意味着，当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理会集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）。
* 其次，渲染器或脚本与请求的某些部分（例如选择器和／或扩展）一起从资源属性中定位。

>[!NOTE]
>
>Sling请求处理中将详细 [介绍此内容](/help/sites-developing/the-basics.md#sling-request-processing)。

这种方法使Sling功能强大且非常灵活，但与以往一样，需要谨慎管理的灵活性也是其灵活性。

为帮助防止DoS滥用，您可以：

1. 在应用程序级别合并控件；由于可能的变量数，默认配置不可行。

   在您的应用程序中，您应：

   * 控制应用程序中的选择器，以便您只 *提供* 所需的显式选择器，并返 `404` 回给所有其他选择器。
   * 防止输出不限数量的内容节点。

1. 检查默认呈示器的配置，该呈示器可能是一个问题区域。

   * 尤其是JSON渲染器，它可以跨多个级别横向于树结构。

      例如，请求：

      `http://localhost:4502/.json`

      可以将整个存储库转储为JSON表示形式。 这会导致严重的服务器问题。 因此，Sling对最大结果数设置限制。 要限制JSON渲染的深度，您可以为以下对象设置值：

      **JSON最大结果** ( `json.maximumresults`)

      在 [Apache Sling GET servlet的配置中](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。 超出此限制时，渲染将折叠。 AEM中Sling的默认值是 `200`。

   * 作为预防措施，请禁用其他默认呈示器（HTML、纯文本、XML）。 再次通过配置 [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。
   >[!CAUTION]
   >
   >请勿禁用JSON渲染器，这是AEM正常操作所必需的。

1. 使用防火墙过滤对实例的访问。

   * 必须使用操作系统级防火墙才能过滤对实例中可能导致拒绝服务攻击的点的访问（如果未受保护）。

**缓解使用表单选择器导致的DoS**

>[!NOTE]
>
>此缓解措施应仅在未使用表单的AEM环境中执行。

由于AEM不为提供现成的索引 `FormChooserServlet`，在查询中使用表单选择器将触发代价高昂的存储库遍历，通常会使AEM实例停止运行。 表单选择器可以通过存在 **&amp;ast;.form来检测。** &amp;ast;字符串。

为了减轻此问题，请按照以下步骤操作：

1. 通过将浏览器指向https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr，转 *到Web控制台*

1. 搜索 **Day CQ WCM表单选择器Servlet**
1. 单击该条目后，请在以下窗口中 **禁用“高级搜索要求** ”。

1. 单击&#x200B;**保存**。

**缓解由资产下载Servlet引起的DoS**

AEM中的默认资产下载Servlet允许经过身份验证的用户发出任意大小的并发下载请求，以创建对他们可见的资产的ZIP文件，这些文件可能会使服务器和／或网络过载。

为了减轻由此功能引起的潜在DoS风险， `AssetDownloadServlet` OSGi组件在最新AEM版本上的发布实例默认处于禁用状态。

如果您的设置要求启用资产下载服务器，请参阅 [此文章](/help/assets/download-assets-from-aem.md) ，了解详细信息。

### 禁用WebDAV {#disable-webdav}

应在创作和发布环境中禁用WebDAV。 这可以通过停止相应的OSGi包来完成。

1. 连接到运 **行于以下位置的Felix Management Console** :

   `https://<*host*>:<*port*>/system/console`

   For example `http://localhost:4503/system/console/bundles`.

1. 在包列表中，找到名为：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 单击“停止”按钮（在“操作”列中）以停止此包。

1. 同样在包列表中，找到名为：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 单击停止按钮以停止此捆绑。

   >[!NOTE]
   >
   >不需要重新启动AEM。

### 确认您没有在用户主路径中透露个人身份信息 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

务必确保不会在存储库用户主路径中显示任何个人身份识别信息，从而保护用户。

自AEM 6.1起，用户（也称为可授权）ID节点名称的存储方式会随接口的新实现而改 `AuthorizableNodeName` 变。 新界面将不再提供节点名称中的用户ID，而是生成随机名称。

无需执行任何配置即可启用它，因为这是在AEM中生成可授权ID的默认方式。

尽管不推荐，但是您可以禁用它，以防需要旧的实现以向后兼容现有应用程序。 为此，您需要：

1. 转到Web控制台，从 **Apache Jackrabbit Oak SecurityProvider中属性requiredServicePids** ，删除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**条目 ****。

   您还可以通过在OSGi配置中查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID来查找Oak安全提供商。

1. 从Web控 **制台中删除Apache Jackrabbit Oak随机可授权节点名称** OSGi配置。

   为便于查找，请注意此配置的PID是 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**。

>[!NOTE]
>
>有关详细信息，请参阅Oak文档中有关可授权节 [点名称生成的信息](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)。

### 防止Clickjacking {#prevent-clickjacking}

为防止点击劫持，我们建议您配置Web服务器以提供 `X-FRAME-OPTIONS` 设置为的HTTP头 `SAMEORIGIN`。

有关Clickjacking [的更多信息，请参阅OWASP站点](https://www.owasp.org/index.php/Clickjacking)。

### 确保在需要时正确复制加密密钥 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份验证方案要求您在所有AEM实例中复制加密密钥。

在执行此操作之前，请注意，密钥复制在不同版本之间的操作方式不同，因为6.3和更早版本之间密钥的存储方式不同。

请参阅下文以了解更多信息。

#### 复制AEM 6.3的密钥 {#replicating-keys-for-aem}

而在旧版本中，复制密钥存储在存储库中，从AEM 6.3开始，它们存储在文件系统中。

因此，为了跨实例复制密钥，您需要将它们从源实例复制到目标实例在文件系统中的位置。

具体而言，您需要：

1. 访问AEM实例（通常是作者实例），该实例包含要复制的关键材料；
1. 在本地文件系统中找到com.adobe.granite.crypto.file包。 例如，在此路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
   每个 `bundle.info` 文件夹中的文件将标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴之前复制的两个文件。
1. [如果目标实例已运行](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) ，请刷新Crypto Bundle。
1. 对要将密钥复制到的所有实例重复上述步骤。

>[!NOTE]
>
>在首次安装AEM时，可通过添加以下参数，还原到6.3之前存储密钥的方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 复制AEM 6.2及更早版本的密钥 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2及更早版本中，密钥存储在节点下的存储库 `/etc/key` 中。

在实例中安全复制密钥的建议方法是仅复制此节点。 您可以通过CRXDE Lite选择性地复制节点：

1. 通过转到https://&lt;serveraddress>: *4502/crx/de/index.jsp打开CRXDE Lite*
1. 选择节 `/etc/key` 点。
1. 转到“复 **制** ”选项卡。
1. 按“复 **制** ”按钮。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe强烈建议在开始生产之前对AEM基础架构执行渗透测试。

### 开发最佳实践 {#development-best-practices}

新开发必须遵循安全最佳 [实践](/help/sites-developing/security.md) ，以确保AEM环境安全。
