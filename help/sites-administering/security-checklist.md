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
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 0%

---


# 安全清单{#security-checklist}

本节介绍您应采取的各种步骤，以确保AEM安装在部署时是安全的。 清单应自上而下应用。

>[!NOTE]
>
>有关Open Security Project(OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)发布的最危险安全威胁的详细信息[也可用。

>[!NOTE]
>
>在开发阶段还有一些其他[安全注意事项](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)。

## 主要安全措施{#main-security-measures}

### 在生产就绪模式{#run-aem-in-production-ready-mode}中运行AEM

有关详细信息，请参阅[在生产就绪模式](/help/sites-administering/production-ready.md)中运行AEM。

### 为传输层安全性启用HTTPS {#enable-https-for-transport-layer-security}

对于具有安全实例，必须在创作和发布实例上启用HTTPS传输层。

>[!NOTE]
>
>有关详细信息，请参阅[启用HTTP over SSL](/help/sites-administering/ssl-by-default.md)部分。

### 安装安全修补程序{#install-security-hotfixes}

确保已安装Adobe](https://helpx.adobe.com/cn/experience-manager/kb/aem63-available-hotfixes.html)提供的最新[安全修补程序。

### 更改AEM和OSGi控制台管理员帐户的默认密码{#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe强烈建议在安装后更改特权&#x200B;[**AEM** `admin`帐户](#changing-the-aem-admin-password)的口令（在所有实例上）。

这些帐户包括：

* AEM `admin`帐户

   更改AEM admin帐户的密码后，您在访问CRX时需要使用新密码。

* OSGi Web控制台的`admin`密码

   此更改还将应用于用于访问Web控制台的管理员帐户，因此您在访问该控制台时需要使用相同的口令。

这两个帐户使用不同的凭据，并且每个帐户都具有不同的强口令，这对于安全部署至关重要。

#### 更改AEM管理员密码{#changing-the-aem-admin-password}

可通过[Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md)控制台更改AEM管理员帐户的口令。

您可以在此编辑`admin`帐户并更改密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。[

>[!NOTE]
>
>更改管理员帐户也会更改OSGi Web控制台帐户。 更改管理员帐户后，您应将OSGi帐户更改为其他帐户。

#### 更改OSGi Web控制台口令{#importance-of-changing-the-osgi-web-console-password}的重要性

除AEM `admin`帐户外，如果无法更改OSGi Web控制台密码的默认密码，则可能导致：

* 在启动和关闭期间，使用默认密码暴露服务器（对于大型服务器，可能需要几分钟）;
* 当存储库关闭／重新启动捆绑——并且OSGI正在运行时，服务器的暴露。

有关更改Web控制台口令的详细信息，请参阅下面的[更改OSGi Web控制台管理员口令](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)。

#### 更改OSGi Web控制台管理员密码{#changing-the-osgi-web-console-admin-password}

您还必须更改用于访问Web控制台的口令。 通过配置[Apache Felix OSGi管理控制台](/help/sites-deploying/osgi-configuration-settings.md)的以下属性，可完成此操作：

**用户** 名和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。初始安装后必须更改密码，以确保实例的安全性。

要执行此操作：

1. 导航到位于`<server>:<port>/system/console/configMgr`的Web控制台。
1. 导航到&#x200B;**Apache Felix OSGi管理控制台**&#x200B;并更改&#x200B;**用户名**&#x200B;和&#x200B;**密码**。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 单击&#x200B;**保存**。

### 实现自定义错误处理程序{#implement-custom-error-handler}

Adobe建议定义自定义错误处理程序页面，尤其是404和500 HTTP响应代码，以防止信息泄露。

>[!NOTE]
>
>有关更多详细信息，请参阅[如何创建自定义脚本或错误处理程序](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html)知识库文章。

### 完整的调度程序安全清单{#complete-dispatcher-security-checklist}

AEM Dispatcher是您基础架构的关键组成部分。 Adobe强烈建议您完成[调度程序安全核对清单](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html)。

>[!CAUTION]
>
>使用调度程序时，必须禁用“.form”选择器。

## 验证步骤{#verification-steps}

### 配置复制和传输用户{#configure-replication-and-transport-users}

AEM的标准安装指定`admin`作为默认[复制代理](/help/sites-deploying/replication.md)内传输凭据的用户。 此外，管理员用户还用于在作者系统上源复制。

出于安全考虑，应更改这两种方法，以反映手头的特定用例，同时考虑到以下两个方面：

* **传输用户**&#x200B;不应是管理员用户。 而是在发布系统上设置一个用户，该用户仅对发布系统的相关部分具有访问权限，并将该用户的凭据用于传输。

   您可以从捆绑的复制接收者用户进行开始，并配置此用户的访问权限以匹配您的情况

* **复制用户**&#x200B;或&#x200B;**代理用户Id**&#x200B;也不应是管理员用户，而应是只能看到应被复制内容的用户。 复制用户用于收集要在创作系统上复制的内容，然后再将其发送到发布者。

### 检查操作仪表板安全运行状况检查{#check-the-operations-dashboard-security-health-checks}

AEM 6引入了新的“操作”仪表板，旨在帮助系统操作员解决问题并监控实例的运行状况。

该仪表板还附带一组安全运行状况检查。 建议您在与生产实例一起上线之前检查所有安全运行状况检查的状态。 有关详细信息，请参阅[操作仪表板文档](/help/sites-administering/operations-dashboard.md)。

### 检查示例内容是否存在{#check-if-example-content-is-present}

所有示例内容和用户(例如Geometrixx项目及其组件)都应在生产系统上完全卸载和删除，然后才能公开访问。

>[!NOTE]
>
>如果此实例在[生产就绪模式](/help/sites-administering/production-ready.md)中运行，则删除示例We.Retail应用程序。 如果由于某种原因，不是这样，您可以通过转到包管理器来卸载示例内容，然后搜索并卸载所有We.Retail包。 有关详细信息，请参阅[使用包](package-manager.md)。

### 检查CRX开发包是否存在{#check-if-the-crx-development-bundles-are-present}

应先在创作和发布生产系统上卸载这些开发OSGi捆绑包，然后再使其可访问。

* AdobeCRXDE支持（com.adobe.granite.crxde支持）
* AdobeGranite CRX Explorer(com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 检查Sling开发包是否存在{#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md)部署了Apache Sling Tooling Support Install(org.apache.sling.toolbing.support.install)。

应在创作和发布生产系统上卸载此OSGi捆绑包，然后再使其可访问。

### Protect反跨站点请求伪造{#protect-against-cross-site-request-forgery}

#### CSRF保护框架{#the-csrf-protection-framework}

AEM 6.1附带一种有助于防止跨站点请求伪造攻击的机制，称为&#x200B;**CSRF保护框架**。 有关如何使用它的详细信息，请查阅[文档](/help/sites-developing/csrf-protection.md)。

#### Sling推荐人过滤器{#the-sling-referrer-filter}

要解决CRX WebDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，您需要为推荐人过滤器添加配置才能使用它。

推荐人过滤器服务是一种OSGi服务，允许您配置：

* 应过滤哪些http方法
* 是否允许空推荐人头
* 以及允许除服务器主机外的列表服务器。

   默认情况下，服务器绑定的所有localhost和当前主机名变体都在列表中。

要配置推荐人筛选器服务，请执行以下操作：

1. 打开Apache Felix控制台(**Configurations**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 以`admin`身份登录。
1. 在&#x200B;**配置**&#x200B;菜单中，选择：

   `Apache Sling Referrer Filter`

1. 在`Allow Hosts`字段中，输入允许用作推荐人的所有主机。 每个条目都必须是表单

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允许来自此服务器的所有具有给定端口的请求。
   * 如果还要允许https请求，则必须输入第二行。
   * 如果允许来自该服务器的所有端口，可以使用`0`作为端口号。

1. 如果要允许空／缺少推荐人标头，请检查`Allow Empty`字段。

   >[!CAUTION]
   >
   >建议在使用命令行工具（如`cURL`）时提供推荐人，而不是允许空值，因为该值可能会使您的系统遭受CSRF攻击。

1. 编辑此过滤器应用于检查`Filter Methods`字段的方法。

1. 单击&#x200B;**保存**&#x200B;以保存更改。

### OSGI设置{#osgi-settings}

某些OSGI设置是默认设置，以便更轻松地调试应用程序。 您需要在发布和创作生产实例时更改这些内容，以避免内部信息泄露给公众。

>[!NOTE]
>
>除&#x200B;**The Day CQ WCM Debug Filter**&#x200B;外，以下所有设置都自动由[生产就绪模式](/help/sites-administering/production-ready.md)覆盖。 因此，我们建议在高效环境中部署实例之前先查看所有设置。

对于以下每项服务，需要更改指定的设置：

* [AdobeGranite HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 启用&#x200B;**Minify**（以删除CRLF和空格字符）。
   * 启用&#x200B;**Gzip**（以允许使用一个请求对文件进行gzip和访问）。
   * 禁用&#x200B;**调试**
   * 禁用&#x200B;**计时**

* [Day CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消选中&#x200B;**启用**

* [Day CQ WCM过滤器](/help/sites-deploying/osgi-configuration-settings.md):

   * 仅在发布时，将&#x200B;**WCM模式**&#x200B;设置为“disabled”

* [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 禁用&#x200B;**生成调试信息**

* [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 禁用&#x200B;**生成调试信息**
   * 禁用&#x200B;**映射的内容**

有关详细信息，请参阅[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

与AEM合作时，有多种方法管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

## 进一步阅读{#further-readings}

### 减轻拒绝服务(DoS)攻击{#mitigate-denial-of-service-dos-attacks}

拒绝服务(DoS)攻击是试图使计算机资源对其预期用户不可用。 这通常是通过超载资源来实现的；例如：

* 来自外部源的大量请求。
* 请求的信息比系统可以成功传送的信息多。

   例如，整个存储库的JSON表示形式。

* 通过请求具有不限数量URL的内容页面，URL可以包括句柄、某些选择器、扩展和后缀——其中任何一个都可以修改。

   例如，`.../en.html`也可以请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   调度程序将对所有有效变量（例如返回`200`响应并配置为缓存）进行缓存，最终将生成完整的文件系统，并且不提供用于进一步请求的服务。

防止此类攻击有许多配置点，此处我们只讨论与AEM直接相关的攻击。

**配置Sling以防止DoS**

Sling是&#x200B;*以内容为中心的*。 这意味着，当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理将集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）。
* 其次，呈现器或脚本与请求的某些部分（如选择器和／或扩展）一起从资源属性中定位。

>[!NOTE]
>
>这在[Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing)中有更详细的介绍。

这种方法使Sling功能强大且非常灵活，但与以往一样，需要谨慎管理的灵活性。

为帮助防止DoS滥用，您可以：

1. 在应用程序级加入控件；由于可能的变量数，默认配置不可行。

   在您的应用程序中，您应：

   * 控制应用程序中的选择器，这样您&#x200B;*只*&#x200B;提供所需的显式选择器，并返回所有其他选择器的`404`。
   * 防止输出不限数量的内容节点。

1. 检查默认呈示器的配置，该呈示器可能是问题区域。

   * 尤其是JSON渲染器，它可以跨多个级别横向于树结构。

      例如，请求：

      `http://localhost:4502/.json`

      可以将整个存储库转储为JSON表示形式。 这会导致严重的服务器问题。 因此，Sling对最大结果数设置限制。 要限制JSON渲染的深度，您可以为以下对象设置值：

      **JSON最大结果** ( `json.maximumresults`)

      在[Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)的配置中。 超过此限制时，渲染将折叠。 AEM中的Sling的默认值为`200`。

   * 作为预防措施，禁用其他默认呈示器（HTML、纯文本、XML）。 再次通过配置[Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。
   >[!CAUTION]
   >
   >请勿禁用JSON渲染器，这是AEM正常操作所必需的。

1. 使用防火墙过滤对实例的访问。

   * 必须使用操作系统级别的防火墙，以过滤对实例中可能导致拒绝服务攻击的点的访问（如果未受保护）。

**缓解使用表单选择器导致的DoS**

>[!NOTE]
>
>此缓解措施应仅对不使用Forms的AEM环境执行。

由于AEM不为`FormChooserServlet`提供现成索引，在查询中使用表单选择器将触发代价高昂的存储库遍历，通常会使AEM实例陷入停顿。 表单选择器可以通过存在&#x200B;**&amp;ast;.form来检测。&amp;ast;**&#x200B;字符串(查询)。

要减轻此问题，请执行以下步骤：

1. 将浏览器指向&#x200B;*https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*，转到Web控制台

1. 搜索&#x200B;**Day CQ WCM表单选择器Servlet**
1. 单击该条目后，请在以下窗口中禁用&#x200B;**高级搜索要求**。

1. 单击&#x200B;**保存**。

**缓解由资产下载Servlet引起的DoS**

AEM中默认的资产下载Servlet允许经过身份验证的用户发出任意大的并发下载请求，以创建对他们可见的资产的ZIP文件，这些文件可能会使服务器和／或网络过载。

为了减轻此功能导致的潜在DoS风险，默认情况下，对于最新AEM版本上的发布实例，`AssetDownloadServlet` OSGi组件处于禁用状态。

如果您的设置要求启用资产下载服务器，请参阅[此文章](/help/assets/download-assets-from-aem.md)以了解更多信息。

### 禁用WebDAV {#disable-webdav}

应在创作和发布环境上禁用WebDAV。 这可以通过停止相应的OSGi包来完成。

1. 连接到运行于以下位置的&#x200B;**Felix管理控制台**:

   `https://<*host*>:<*port*>/system/console`

   例如`http://localhost:4503/system/console/bundles`。

1. 在包的列表中，找到名为：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 单击“停止”按钮（在“操作”列中）以停止此捆绑。

1. 在包的列表中，找到名为：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 单击停止按钮以停止此捆绑。

   >[!NOTE]
   >
   >不需要重新启动AEM。

### 验证您是否未在用户主路径{#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}中显示个人可识别信息

通过确保不在存储库用户主路径中显示任何个人识别信息，保护用户非常重要。

自AEM 6.1起，用户（也称为可授权）ID节点名称的存储方式会随着`AuthorizableNodeName`接口的新实现而改变。 新界面将不再在节点名称中显示用户ID，而是生成随机名称。

无需执行任何配置即可启用它，因为现在这是在AEM中生成可授权ID的默认方式。

尽管不推荐，但您可以禁用它，以防需要旧的实现以向后兼容现有应用程序。 为此，您需要：

1. 转到Web控制台，从&#x200B;**Apache Jackrabbit Oak Security提供者**&#x200B;的属性&#x200B;**requiredServicePids**&#x200B;中删除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**条目。

   您还可以在OSGi配置中查找&#x200B;**org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID，找到Oak安全提供商。

1. 从Web控制台中删除&#x200B;**Apache Jackrabbit Oak随机可授权节点名称** OSGi配置。

   为便于查找，请注意此配置的PID是&#x200B;**org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**。

>[!NOTE]
>
>有关详细信息，请参阅[可授权节点名称生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)上的Oak文档。

### 防止Clickjacking {#prevent-clickjacking}

为防止点击劫持，我们建议您配置Web服务器以提供设置为`SAMEORIGIN`的`X-FRAME-OPTIONS` HTTP头。

有关点击劫持的更多[信息，请参阅OWASP站点](https://www.owasp.org/index.php/Clickjacking)。

### 确保在需要时正确复制加密密钥{#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份验证方案要求您在所有AEM实例中复制加密密钥。

在执行此操作之前，请注意，密钥复制在不同版本之间的操作方式不同，因为6.3和更早版本之间存储密钥的方式不同。

有关更多信息，请参见下文。

#### 复制AEM 6.3 {#replicating-keys-for-aem}的密钥

而在旧版本中，复制密钥存储在存储库中，从AEM 6.3开始，它们存储在文件系统中。

因此，为了跨实例复制密钥，您需要将它们从源实例复制到文件系统上目标实例的位置。

更具体地说，您需要：

1. 访问AEM实例，通常是包含要复制的关键材料的作者实例；
1. 在本地文件系统中找到com.adobe.granite.crypto.file捆绑。 例如，在此路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   每个文件夹中的`bundle.info`文件将标识捆绑名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥重复到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴之前复制的两个文件。
1. [如果目标](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 实例已运行，请刷新Crypto Bundle。
1. 对要将密钥复制到的所有实例重复上述步骤。

>[!NOTE]
>
>您可以在首次安装AEM时添加以下参数，还原到6.3之前存储密钥的方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 复制AEM 6.2和旧版本{#replicating-keys-for-aem-and-older-versions}的密钥

在AEM 6.2及更早版本中，密钥存储在`/etc/key`节点下的存储库中。

在实例中安全复制密钥的建议方法是仅复制此节点。 您可以通过CRXDE Lite有选择地复制节点：

1. 转到&#x200B;*https://&lt;serveraddress>:4502/crx/de/index.jsp*&#x200B;打开CRXDE Lite
1. 选择`/etc/key`节点。
1. 转到&#x200B;**复制**&#x200B;选项卡。
1. 按&#x200B;**复制**&#x200B;按钮。

### 执行渗透测试{#perform-a-penetration-test}

Adobe强烈建议在开始生产之前对AEM基础架构执行渗透测试。

### 开发最佳实践{#development-best-practices}

新开发必须遵循[安全最佳实践](/help/sites-developing/security.md)，以确保AEM环境的安全。
