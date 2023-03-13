---
title: 安全核对清单
seo-title: Security Checklist
description: 了解配置和部署AEM时的各种安全注意事项。
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: 7efe4a011d831c34f6aafd877654e8b41fec96e0
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 3%

---

# 安全核对清单 {#security-checklist}

本节介绍应执行的各种步骤，以确保在部署时您的AEM安装是安全的。 检查清单旨在从上到下应用。

>[!NOTE]
>
>此外，我们还提供了有关最危险的安全威胁的更多信息，发布者为 [打开Web应用程序安全项目(OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>还有一些额外的 [安全注意事项](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 适用于开发阶段。

## 主要安全措施 {#main-security-measures}

### 在生产就绪模式下运行AEM {#run-aem-in-production-ready-mode}

有关更多信息，请参阅 [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md).

### 为传输层安全性启用 HTTPS {#enable-https-for-transport-layer-security}

必须具有安全实例，必须在创作实例和发布实例上启用HTTPS传输层。

>[!NOTE]
>
>请参阅 [启用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 部分以了解更多信息。

### 安装安全修补程序 {#install-security-hotfixes}

确保您已安装最新的 [Adobe提供的安全修补程序](https://helpx.adobe.com/cn/experience-manager/kb/aem63-available-hotfixes.html).

### 更改AEM和OSGi Console管理帐户的默认密码 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe强烈建议您在安装后更改特权用户的口令 [**AEM** `admin` 帐户](#changing-the-aem-admin-password) （在所有实例上）。

这些帐户包括：

* AEM `admin` 帐户

   一旦更改了AEM管理员帐户的密码，您就需要在访问CRX时使用新密码。

* 此 `admin` OSGi Web控制台密码

   此更改也将应用于用于访问Web控制台的管理帐户，因此您在访问时需要使用相同的密码。

这两个帐户使用单独的凭据，并且每个帐户都有独特的强密码，这对于安全部署至关重要。

#### 更改AEM管理员密码 {#changing-the-aem-admin-password}

AEM管理员帐户的密码可通过 [Granite操作 — 用户](/help/sites-administering/granite-user-group-admin.md) 控制台。

您可以在此处编辑 `admin` 帐户和 [更改密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>更改管理员帐户也会更改OSGi Web控制台帐户。 更改管理员帐户后，您应该将OSGi帐户更改为其他帐户。

#### 更改OSGi Web控制台密码的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帐户，未能更改OSGi Web控制台密码的默认密码可能会导致：

* 在启动和关闭期间使用默认密码公开服务器（对于大型服务器可能需要几分钟时间）；
* 当存储库关闭/重新启动捆绑包并且OSGI正在运行时，服务器的曝光度。

有关更改Web控制台密码的详细信息，请参见 [更改OSGi Web控制台管理密码](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下面的。

#### 更改OSGi Web控制台管理密码 {#changing-the-osgi-web-console-admin-password}

您还必须更改用于访问Web控制台的密码。 此操作通过 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 更新以下属性 **Apache Felix OSGi管理控制台**：

* **用户名** 和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。
必须更改密码 *之后* 初始安装以确保实例的安全性。

要执行此操作：

>[!NOTE]
>
>参见 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 有关配置OSGi设置的完整详细信息。

1. 使用 **工具**， **操作** 菜单，打开 **Web控制台** 并导航到 **配置** 部分。
例如，在 `<server>:<port>/system/console/configMgr`.
1. 导航到并打开条目 **Apache Felix OSGi管理控制台**.
1. 更改 **用户名** 和 **密码**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 选择&#x200B;**保存**。

### 实施自定义错误处理程序 {#implement-custom-error-handler}

Adobe建议定义自定义错误处理程序页面，特别是对于404和500 HTTP响应代码，以防止信息泄漏。

>[!NOTE]
>
>参见 [如何创建自定义脚本或错误处理程序](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) 知识库文章，以了解更多详细信息。

### 完成Dispatcher安全核对清单 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您的基础架构中的一个关键部分。 Adobe强烈建议您完成 [Dispatcher安全核对清单](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>使用Dispatcher时，您必须禁用“.form”选择器。

## 验证步骤 {#verification-steps}

### 配置复制和转移用户 {#configure-replication-and-transport-users}

AEM的标准安装指定 `admin` 在默认情况下作为传输凭据的用户 [复制代理](/help/sites-deploying/replication.md). 此外，管理员用户还用于在创作系统上为复制提供源。

出于安全考虑，应将两者都更改为反映当前的特定用例，并牢记以下两个方面：

* 此 **转移用户** 不应为管理员用户。 而是要在发布系统上设置一个仅对发布系统的相关部分具有访问权限的用户，并将该用户的凭据用于传输。

   您可以从捆绑的复制接收者用户开始，并配置此用户的访问权限以符合您的情况

* 此 **复制用户** 或 **代理用户ID** 也不应该是管理员用户，而应该是只能查看应复制的内容的用户。 复制用户用于在将内容发送到发布者之前收集要在创作系统上复制的内容。

### 检查操作功能板安全运行状况检查 {#check-the-operations-dashboard-security-health-checks}

AEM 6引入了新的操作仪表板，旨在帮助系统操作员排除问题并监控实例的运行状况。

仪表板还随附一组安全运行状况检查。 建议您在使用生产实例上线之前，检查所有安全运行状况检查的状态。 欲知更多信息，请参见 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

### 检查是否存在示例内容 {#check-if-example-content-is-present}

所有示例内容和用户(例如Geometrixx项目及其组件)应在生产系统中完全卸载和删除，然后才能公开访问。

>[!NOTE]
>
>如果此实例在中运行，则将删除示例We.Retail应用程序 [生产就绪模式](/help/sites-administering/production-ready.md). 如果由于任何原因没有出现这种情况，您可以转到包管理器，然后搜索并卸载所有We.Retail包，以卸载示例内容。 有关更多信息，请参阅 [使用包](package-manager.md).

### 检查CRX开发包是否存在 {#check-if-the-crx-development-bundles-are-present}

在使这些开发OSGi捆绑包可访问之前，应在创作和发布生产系统上卸载这些捆绑包。

* AdobeCRXDE支持(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer (com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 检查Sling开发包是否存在 {#check-if-the-sling-development-bundle-is-present}

此 [适用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支持安装(org.apache.sling.tooling.support.install)。

在使创作和发布生产系统可访问之前，应卸载此OSGi捆绑包。

### Protect防止跨站点请求伪造 {#protect-against-cross-site-request-forgery}

#### CSRF保护框架 {#the-csrf-protection-framework}

AEM 6.1附带有助于抵御跨站点请求伪造攻击的机制，称为 **CSRF保护框架**. 有关如何使用的更多信息，请参阅 [文档](/help/sites-developing/csrf-protection.md).

#### Sling引用过滤器 {#the-sling-referrer-filter}

要解决CRX WebDAV和Apache Sling中的跨站点请求伪造(CSRF)的已知安全问题，您需要添加反向链接筛选器的配置才能使用它。

反向链接筛选服务是一个OSGi服务，它允许您配置：

* 应该筛选哪些http方法
* 是否允许空的反向链接标头
* 以及除服务器主机之外还允许使用的服务器列表。

   默认情况下，服务器绑定的本地主机和当前主机名的所有变体都位于列表中。

配置反向链接筛选服务：

1. 打开Apache Felix控制台(**配置**)：

   `https://<server>:<port_number>/system/console/configMgr`

1. 登录身份 `admin`.
1. 在 **配置** 菜单，选择：

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 字段中，输入允许作为反向链接的所有主机。 每个条目都必须采用格式

   &lt;protocol>：//&lt;server>：&lt;port>

   例如：

   * `https://allowed.server:80` 允许使用给定端口从此服务器发出所有请求。
   * 如果您还想允许https请求，则必须输入第二行。
   * 如果允许来自该服务器的所有端口，则可以使用 `0` 作为端口号。

1. 查看 `Allow Empty` 字段（如果要允许为空/缺少反向链接标头）。

   >[!CAUTION]
   >
   >建议在使用命令行工具（例如）时提供反向链接 `cURL` 而不是允许空值，因为它可能会使您的系统遭到CSRF攻击。

1. 编辑此筛选器应用于检查的方法，使用 `Filter Methods` 字段。

1. 单击 **保存** 以保存更改。

### OSGI设置 {#osgi-settings}

某些OSGI设置默认设置为更易于调试应用程序。 这些需要在您的发布和创作生产实例中进行更改，以避免内部信息泄露给公众。

>[!NOTE]
>
>以下所有设置，但以下除外 **Day CQ WCM调试过滤器** 自动包含在 [生产就绪模式](/help/sites-administering/production-ready.md). 因此，我们建议先查看所有设置，然后再将实例部署到高效环境中。

对于以下每项服务，需要更改指定的设置：

* [AdobeGraniteHTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager)：

   * 启用 **Minify** （删除CRLF和空白字符）。
   * 启用 **Gzip** （允许通过一个请求来压缩和访问文件）。
   * disable **调试**
   * disable **计时**

* [Day CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 取消选中 **启用**

* [Day CQ WCM过滤器](/help/sites-deploying/osgi-configuration-settings.md)：

   * 仅发布时，设置 **WCM模式** 更改为“已禁用”

* [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler)：

   * disable **生成调试信息**

* [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * disable **生成调试信息**
   * disable **映射的内容**

有关更多详细信息，请参阅 [OSGi配置](/help/sites-deploying/osgi-configuration-settings.md).

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息和建议的做法。

## 阅读更多内容 {#further-readings}

### 减轻拒绝服务(DoS)攻击 {#mitigate-denial-of-service-dos-attacks}

拒绝服务 (DoS) 攻击是一种试图让计算机资源对其目标用户不可用的攻击。这通常是通过使资源过载来实现的；例如：

* 来自外部源的大量请求。
* 通过请求获取系统无法成功投放的更多信息。

   例如，整个存储库的JSON表示形式。

* 通过请求包含无限量URL的内容页面，该URL可以包括句柄、某些选择器、扩展名和后缀 — 任何后缀都可以修改。

   例如， `.../en.html` 也可以请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效的变体(例如，返回 `200` 响应并配置为缓存)将由Dispatcher缓存，最终导致完整的文件系统，并且没有服务可用于进一步的请求。

对于防止此类攻击，有许多配置要点，这里我们仅讨论与AEM直接相关的配置要点。

**配置Sling以防范拒绝服务攻击**

Sling是 *以内容为中心*. 这意味着处理侧重于内容，因为每个(HTTP)请求都映射到JCR资源（存储库节点）形式的内容：

* 第一个目标是保存内容的资源（JCR节点）。
* 其次，呈现器或脚本与请求的某些部分（例如，选择器和/或扩展）结合从资源属性定位。

>[!NOTE]
>
>有关更多详细信息，请参见 [Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing).

这种方法使Sling功能非常强大且非常灵活，但像往常一样，需要谨慎管理灵活性。

为帮助防止误用DoS，您可以：

1. 在应用程序级别合并控件；由于可能的变体数量，默认配置不可行。

   在您的应用程序中，您应：

   * 控制应用程序中的选择器，以便 *仅限* 提供所需的显式选择器并返回 `404` 为其他所有人服务。
   * 阻止输出无限数量的内容节点。

1. 检查默认渲染器的配置，这可能是一个问题区域。

   * 特别是可在多个级别上横跨树结构的JSON渲染器。

      例如，请求：

      `http://localhost:4502/.json`

      可以将整个存储库转储为JSON表示形式。 这将导致严重的服务器问题。 因此，Sling对最大结果数进行了限制。 要限制JSON渲染的深度，您可以设置以下值：

      **JSON最大结果** ( `json.maximumresults`)

      在的配置中 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). 当超过此限制时，渲染将折叠。 AEM中Sling的默认值为 `1000`.

   * 作为预防措施，将禁用其他默认渲染程序(HTML、纯文本、XML)。 再次配置 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >请勿禁用JSON渲染器，这是AEM正常操作所必需的。

1. 使用防火墙筛选对实例的访问。

   * 若要过滤对实例点的访问（如果不加以保护，则可能会导致拒绝服务攻击），必须使用操作系统级别的防火墙。

**针对使用表单选择器引起的DoS采取缓解措施**

>[!NOTE]
>
>此缓解措施应仅在不使用Forms的AEM环境中执行。

由于AEM不提供开箱即用的索引 `FormChooserServlet`，在查询中使用表单选择器会触发代价高昂的存储库遍历，通常会导致AEM实例暂停。 表单选择器可以通过以下项的存在来检测 **&amp;ast；.form.&amp;ast；** 查询中的字符串。

为了缓解此问题，请按照以下步骤操作：

1. 通过将您的浏览器指向，转到Web控制台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*

1. 搜索 **Day CQ WCM表单选择器Servlet**
1. 单击该条目后，禁用 **高级搜索要求** 在下面的窗口中。

1. 单击“**保存**”。

**减轻因资产下载Servlet导致的DoS的影响**

默认的资源下载servlet允许经过身份验证的用户发出任意大小的并发下载请求，以创建资源的ZIP文件。 创建大型ZIP存档可能会使服务器和网络过载。 要降低由此行为导致的潜在拒绝服务(DoS)风险，请执行以下操作： `AssetDownloadServlet` 默认情况下，OSGi组件在下列日期处于禁用状态： [!DNL Experience Manager] 发布实例。 启用日期 [!DNL Experience Manager] 默认情况下，创作实例。

如果您不需要下载功能，请在创作和发布部署上禁用servlet。 如果您的设置要求启用资源下载功能，请参阅 [本文](/help/assets/download-assets-from-aem.md) 了解更多信息。 此外，您还可以定义您的部署可以支持的最大下载限制。

### 禁用WebDAV {#disable-webdav}

应在创作环境和发布环境中禁用WebDAV。 这可以通过停止相应的OSGi捆绑包来完成。

1. 连接到 **Felix管理控制台** 运行于：

   `https://<*host*>:<*port*>/system/console`

   例如 `http://localhost:4503/system/console/bundles`。

1. 在捆绑包列表中，找到名为的捆绑包：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 单击“停止”按钮（在“操作”列中）可停止此捆绑包。

1. 再次在包列表中找到名为的包：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 单击“停止”按钮可停止此捆绑包。

   >[!NOTE]
   >
   >不需要重新启动AEM。

### 验证您是否未在用户主页路径中披露个人身份信息 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

请务必确保不会在存储库用户主路径中公开任何个人身份信息，从而保护您的用户。

自AEM 6.1起，用户（也称为可授权）ID节点名称的存储方式会随着新的实施而改变。 `AuthorizableNodeName` 界面。 新界面将不再在节点名称中公开用户ID，而是会生成一个随机名称。

启用它无需执行任何配置，因为现在这是在AEM中生成可授权ID的默认方式。

虽然不建议使用，但您可以禁用它，以防您需要旧实施以便与现有应用程序向后兼容。 为此，您需要：

1. 转到Web控制台，然后从属性中删除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**条目 **requiredServicePids** 在 **Apache Jackrabbit Oak SecurityProvider**.

   您还可以通过查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** osgi配置中的PID。

1. 删除 **Apache Jackrabbit Oak随机可授权节点名称** Web控制台中的OSGi配置。

   为了更便于查找，请注意，此配置的PID为 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>有关更多信息，请参阅Oak文档，位于 [可授权的节点名称生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 防御点击劫持攻击 {#prevent-clickjacking}

要防御点击劫持攻击，建议您将 Web 服务器配置为将 `X-FRAME-OPTIONS` HTTP 标头集提供给 `SAMEORIGIN`。

有关[点击劫持攻击的更多信息，请参阅 OWASP 网站](https://www.owasp.org/index.php/Clickjacking)。

### 确保在需要时正确复制加密密钥 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份验证方案要求您在所有AEM实例之间复制加密密钥。

在执行此操作之前，请注意，不同版本之间的密钥复制执行方式不同，因为在6.3和更早版本之间，密钥的存储方式不同。

有关更多信息，请参阅下文。

#### 复制AEM 6.3的密钥 {#replicating-keys-for-aem}

而在旧版本中，复制密钥存储在存储库中，从AEM 6.3开始，它们存储在文件系统上。

因此，要跨实例复制密钥，您需要将它们从源实例复制到文件系统上的目标实例位置。

更具体地说，您需要：

1. 访问包含要复制的关键材料的AEM实例，通常是创作实例；
1. 在本地文件系统中找到com.adobe.granite.crypto.file包。 例如，在此路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   此 `bundle.info` 每个文件夹中的文件将标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴您之前复制的两个文件。
1. [刷新加密捆绑包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目标实例已在运行。
1. 对要将密钥复制到的所有实例重复上述步骤。

>[!NOTE]
>
>首次安装AEM时，您可以通过添加以下参数还原为6.3以前的密钥存储方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 复制AEM 6.2及更早版本的密钥 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2及更早版本中，密钥存储在存储库的 `/etc/key` 节点。

跨实例安全复制密钥的推荐方法是仅复制此节点。 您可以通过CRXDE Lite有选择地复制节点：

1. 打开CRXDE Lite，方法是转到 *https://&lt;serveraddress>：4502/crx/de/index.jsp*
1. 选择 `/etc/key` 节点。
1. 转到 **复制** 选项卡。
1. 按 **复制** 按钮。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe 强烈建议您在开始生产之前对 AEM 基础架构执行渗透测试。

### 开发最佳实践 {#development-best-practices}

新的开发必须遵循 [安全性最佳实践](/help/sites-developing/security.md) 以确保您的AEM环境保持安全。
