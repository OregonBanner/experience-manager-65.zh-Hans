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
source-git-commit: 465d3e956ecdd36eea5fe095e250652eedd4b3c5
workflow-type: tm+mt
source-wordcount: '3005'
ht-degree: 1%

---

# 安全核对清单 {#security-checklist}

本节介绍为确保部署时AEM安装的安全而应执行的各个步骤。 检查清单旨在从上到下应用。

>[!NOTE]
>
>此外，我们还提供了有关最危险的安全威胁的更多信息，发布者为 [打开Web应用程序安全项目(OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>还有一些附加的 [安全注意事项](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 适用于开发阶段。

## 主要安全措施 {#main-security-measures}

### 在生产就绪模式下运行AEM {#run-aem-in-production-ready-mode}

有关更多信息，请参阅 [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md).

### 为传输层安全性启用 HTTPS {#enable-https-for-transport-layer-security}

对于拥有安全实例，必须在创作实例和发布实例上启用HTTPS传输层。

>[!NOTE]
>
>请参阅 [启用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 部分以了解更多信息。

### 安装安全修补程序 {#install-security-hotfixes}

确保您已安装最新的 [Adobe提供的安全修补程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans).

### 更改AEM和OSGi Console管理帐户的默认密码 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe建议在安装后更改特权用户的口令 [**AEM** `admin` 帐户](#changing-the-aem-admin-password) （在所有实例上）。

这些帐户包括：

* AEM `admin` 帐户

  更改AEM管理员帐户的密码后，在访问CRX时使用新密码。

* 此 `admin` osgi Web控制台的密码

  此更改也将应用于用于访问Web控制台的管理帐户，因此在访问时请使用相同的密码。

这两个帐户使用单独的凭据，并且每个帐户都有独特的强密码，这对于安全部署至关重要。

#### 更改AEM管理员密码 {#changing-the-aem-admin-password}

AEM管理员帐户的密码可通过 [Granite操作 — 用户](/help/sites-administering/granite-user-group-admin.md) 控制台。

您可以在此编辑 `admin` 帐户和 [更改密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>更改管理员帐户也会更改OSGi Web控制台帐户。 更改管理员帐户后，您应该将OSGi帐户更改为其他内容。

#### 更改OSGi Web控制台密码的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帐户，未能更改OSGi Web控制台密码的默认密码可能会导致：

* 在启动和关闭期间使用默认密码公开服务器（对于大型服务器可能需要几分钟时间）；
* 当存储库已关闭/重新启动捆绑包并且OSGI正在运行时，服务器的曝光度。

有关更改Web控制台密码的详细信息，请参阅 [更改OSGi Web控制台管理员密码](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下。

#### 更改OSGi Web控制台管理员密码 {#changing-the-osgi-web-console-admin-password}

更改用于访问Web控制台的密码。 使用 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 更新 **Apache Felix OSGi管理控制台**：

* **用户名** 和 **密码**，用于访问Apache Felix Web管理控制台本身的凭据。
必须更改密码 *之后* 初始安装以确保实例的安全性。

>[!NOTE]
>
>请参阅 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 有关配置OSGi设置的完整详细信息。

**更改OSGi Web控制台管理员密码**：

1. 使用 **工具**， **操作** 菜单，打开 **Web控制台** 并导航至 **配置** 部分。
例如，在 `<server>:<port>/system/console/configMgr`.
1. 导航到并打开条目 **Apache Felix OSGi管理控制台**.
1. 更改 **用户名** 和 **密码**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 选择&#x200B;**保存**。

### 实施自定义错误处理程序 {#implement-custom-error-handler}

Adobe建议定义自定义错误处理程序页面，特别是对于404和500 HTTP响应代码，以防止信息泄漏。

>[!NOTE]
>
>请参阅 [如何创建自定义脚本或错误处理程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) 以了解更多详细信息。

### 完成Dispatcher安全核对清单 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您的基础架构中的一个关键部分。 Adobe建议您完成 [Dispatcher安全核对清单](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>使用Dispatcher时，您必须禁用“.form”选择器。

## 验证步骤 {#verification-steps}

### 配置复制和转移用户 {#configure-replication-and-transport-users}

AEM的标准安装指定 `admin` 在默认范围内作为传输凭据的用户 [复制代理](/help/sites-deploying/replication.md). 此外，管理员用户还用于在创作系统上提供复制源。

出于安全考虑，应该对这两个部分都进行更改，以反映当前的特定用例，并牢记以下两个方面：

* 此 **传输用户** 不得为管理员用户。 而是要在发布系统上设置一个仅对发布系统的相关部分具有访问权限的用户，并将该用户的凭据用于传输。

  您可以从捆绑的复制接收者用户开始，并配置此用户的访问权限以符合您的情况

* 此 **复制用户** 或 **代理用户ID** 另外，用户不能是管理员用户，而只能查看所复制内容的用户。 复制用户用于在将内容发送到发布者之前，收集要在创作系统上复制的内容。

### 检查操作功能板安全运行状况检查 {#check-the-operations-dashboard-security-health-checks}

AEM 6引入了新的操作仪表板，旨在帮助系统操作员排除问题并监控实例的运行状况。

仪表板还随附一组安全运行状况检查。 建议您在使用生产实例上线之前，检查所有安全运行状况检查的状态。 欲知更多信息，请参见 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

### 检查是否存在示例内容 {#check-if-example-content-is-present}

应先卸载所有示例内容和用户(例如Geometrixx项目及其组件)，并在生产系统中将其完全删除，然后再将其公开访问。

>[!NOTE]
>
>示例 `We.Retail` 如果此实例在中运行，则将删除应用程序 [生产就绪模式](/help/sites-administering/production-ready.md). 如果不是这种情况，您可以转到包管理器，然后搜索并卸载示例内容 `We.Retail` 包。

请参阅 [使用包](package-manager.md).

### 检查CRX开发包是否存在 {#check-if-the-crx-development-bundles-are-present}

这些开发OSGi捆绑包应在创作和发布生产系统中卸载，然后才能访问。

* AdobeCRXDE支持(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer (com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 检查Sling开发包是否存在 {#check-if-the-sling-development-bundle-is-present}

此 [AEM Developer Tools](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支持安装(org.apache.sling.tooling.support.install)。

在使作者和发布生产系统可访问之前，应卸载此OSGi捆绑包。

### Protect防止跨站点请求伪造 {#protect-against-cross-site-request-forgery}

#### CSRF保护框架 {#the-csrf-protection-framework}

AEM 6.1附带有助于防御跨站点请求伪造攻击的机制，称为 **CSRF保护框架**. 有关如何使用的更多信息，请参阅 [文档](/help/sites-developing/csrf-protection.md).

#### Sling引用过滤器 {#the-sling-referrer-filter}

要解决CRX WebDAV和Apache Sling中跨站点请求伪造(CSRF)的已知安全问题，请添加反向链接筛选器的配置以使用它。

反向链接筛选服务是一个OSGi服务，您可以通过它配置以下内容：

* 应该筛选哪些http方法
* 是否允许空的反向链接标头
* 以及除服务器主机之外允许使用的服务器列表。

  默认情况下，服务器绑定到的本地主机和当前主机名的所有变体都位于列表中。

配置反向链接筛选服务：

1. 打开Apache Felix控制台(**配置**)位于：

   `https://<server>:<port_number>/system/console/configMgr`

1. 登录身份 `admin`.
1. 在 **配置** 菜单，选择：

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 字段中，输入允许作为反向链接的所有主机。 每个条目都必须采用格式

   &lt;protocol>：//&lt;server>：&lt;port>

   例如：

   * `https://allowed.server:80` 允许来自此服务器的具有给定端口的所有请求。
   * 如果您还想允许https请求，则必须输入第二行。
   * 如果允许来自该服务器的所有端口，则可以使用 `0` 作为端口号。

1. 查看 `Allow Empty` 字段。

   >[!CAUTION]
   >
   >Adobe建议您在使用命令行工具(例如 `cURL` 而不是允许空值，因为它可能会使您的系统遭受CSRF攻击。

1. 编辑此筛选器用于检查的方法，使用 `Filter Methods` 字段。

1. 单击 **保存** 以保存更改。

### OSGI设置 {#osgi-settings}

默认情况下，会设置一些OSGI设置，以便更轻松地调试应用程序。 在发布和创作生产实例中更改此类设置，以避免内部信息泄露给公众。

>[!NOTE]
>
>以下所有设置，但 **Day CQ WCM调试过滤器**，自动由 [生产就绪模式](/help/sites-administering/production-ready.md). 因此，Adobe建议您在将Instance部署到高效环境之前查看所有设置。

对于以下每个服务，必须更改指定的设置：

* [AdobeGraniteHTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager)：

   * 启用 **Minify** （删除CRLF和空白字符）。
   * 启用 **Gzip** （允许通过一个请求来压缩和访问文件）。
   * disable **调试**
   * disable **计时**

* [Day CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 取消选中 **启用**

* [Day CQ WCM过滤器](/help/sites-deploying/osgi-configuration-settings.md)：

   * 在仅发布时，设置 **WCM模式** 更改为“已禁用”

* [Apache Sling JavaScript处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler)：

   * disable **生成调试信息**

* [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * disable **生成调试信息**
   * disable **映射的内容**

请参阅 [osgi配置设置](/help/sites-deploying/osgi-configuration-settings.md).

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

## 阅读更多内容 {#further-readings}

### 减少拒绝服务(DoS)攻击 {#mitigate-denial-of-service-dos-attacks}

拒绝服务 (DoS) 攻击是一种试图让计算机资源对其目标用户不可用的攻击。此攻击通常通过使资源过载来实现；例如：

* 来自外部源的大量请求。
* 请求系统无法成功传递的更多信息。

  例如，整个存储库的JSON表示形式。

* 通过请求包含无限数量URL的内容页面，该URL可以包含句柄、某些选择器、扩展名和后缀 — 任何后缀都可以修改。

  例如， `.../en.html` 也可以请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  所有有效的变体(例如，返回 `200` 响应并配置为缓存)由Dispatcher缓存，最终导致完整的文件系统，并且没有服务来进一步请求。

对于防止此类攻击，有许多配置要点，但此处仅讨论与AEM相关的那些要点。

**配置Sling以防范拒绝服务攻击**

Sling是 *以内容为中心*. 处理侧重于内容，因为每个(HTTP)请求都映射到JCR资源（存储库节点）形式的内容：

* 第一个目标是保存内容的资源（JCR节点）。
* 其次，呈现器或脚本位于具有请求特定部分（例如，选择器和/或扩展）的资源属性中。

请参阅 [Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing) 以了解更多信息。

这种方法使Sling变得强大而灵活，但与往常一样，必须谨慎管理的正是灵活性。

为帮助防止DoS误用，您可以执行以下操作：

1. 在应用程序级别合并控件。 由于可能的变体数量，默认配置不可行。

   在您的应用程序中，您应：

   * 控制应用程序中的选择器，以便 *仅限* 提供所需的显式选择器并返回 `404` 为了其他所有人。
   * 阻止输出无限数量的内容节点。

1. 检查默认渲染器的配置，这可能是一个问题区域。

   * 尤其是，JSON渲染器跨多个级别遍历树结构。

     例如，请求：

     `http://localhost:4502/.json`

     可能会以JSON表示形式转储整个存储库，这可能会导致严重的服务器问题。 因此，Sling对最大结果数量设置了限制。 要限制JSON渲染的深度，请设置以下值：

     **JSON最大结果** ( `json.maximumresults`)

     在的配置中 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). 超过此限制时，渲染将折叠。 AEM中的Sling的默认值为 `1000`.

   * 作为预防措施，您应该禁用其它默认呈现程序(HTML、纯文本、XML)。 同样，通过配置 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).

   >[!CAUTION]
   >
   >请勿禁用JSON渲染器，因为AEM的正常操作需要它。

1. 使用防火墙筛选对实例的访问。

   * 使用操作系统级别的防火墙对于过滤对实例点的访问是必要的，如果不加以保护，可能会导致拒绝服务攻击。

**针对使用表单选择器导致的DoS做出缓解**

>[!NOTE]
>
>应仅在未使用Forms的AEM环境中执行这项缓解措施。

因为AEM不提供开箱即用的索引 `FormChooserServlet`，在查询中使用表单选择器可能会触发成本高昂的存储库遍历，通常会导致AEM实例陷入停顿。 表单选择器可以通过以下各项的存在来检测 **&amp;ast；.form.&amp;ast；** 查询中的字符串。

要缓解此问题，您可以执行以下步骤：

1. 通过将浏览器指向，转到Web控制台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*

1. 搜索 **Day CQ WCM表单选择器Servlet**
1. 单击该条目后，禁用 **需要高级搜索** 在下面的窗口中。

1. 单击&#x200B;**保存**。

**减轻因资产下载Servlet导致的DoS的影响**

默认的资源下载servlet允许经过身份验证的用户发出任意大小的并发下载请求，以创建资源的ZIP文件。 创建大型ZIP存档可能会导致服务器和网络过载。 要降低由此行为导致的潜在拒绝服务(DoS)风险， `AssetDownloadServlet` 默认情况下，上的OSGi组件处于禁用状态 [!DNL Experience Manager] 发布实例。 启用日期 [!DNL Experience Manager] 默认情况下，创作实例。

如果您不需要下载功能，请在创作和发布部署中禁用servlet。 如果您的设置要求启用资源下载功能，请参阅 [本文](/help/assets/download-assets-from-aem.md) 以了解更多信息。 此外，您还可以定义部署可以支持的最大下载限制。

### 禁用WebDAV {#disable-webdav}

通过停止相应的OSGi捆绑包，在创作环境和发布环境中禁用WebDAV。

1. 连接到 **Felix管理控制台** 运行时间：

   `https://<*host*>:<*port*>/system/console`

   例如：`http://localhost:4503/system/console/bundles`。

1. 在捆绑包列表中，找到名为的捆绑包：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 要停止此捆绑，请在“操作”列中单击停止按钮。

1. 再次在捆绑包列表中找到名为的捆绑包：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 要停止此捆绑，请单击停止按钮。

   >[!NOTE]
   >
   >不需要重新启动AEM。

### 确认您未在用户主页路径中披露个人身份信息 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

务必确保存储库用户主页路径中不会公开任何个人身份信息，以保护您的用户。

自AEM 6.1起，用户（也称为可授权）ID节点名称的存储方式会随着新的实施而改变 `AuthorizableNodeName` 界面。 新界面不再在节点名称中公开用户ID，而是生成随机名称。

启用它无需执行任何配置，因为现在是在AEM中生成可授权ID的默认方式。

虽然不建议使用，但您可以禁用它，以防您需要旧实施以便与现有应用程序向后兼容。 为此，您必须执行以下操作：

1. 转到Web控制台，然后从属性中删除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**条目 **requiredServicePids** 在 **Apache Jackrabbit Oak SecurityProvider**.

   您还可以通过查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** OSGi配置中的PID。

1. 删除 **Apache Jackrabbit Oak随机可授权节点名称** Web控制台中的OSGi配置。

   为便于查找，此配置的PID为 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>有关更多信息，请参阅Oak文档，位于 [可授权的节点名称生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 匿名权限强化包 {#anonymous-permission-hardening-package}

默认情况下，AEM存储系统元数据，例如 `jcr:createdBy` 或 `jcr:lastModifiedBy` 作为节点属性，位于存储库中的常规内容旁边。 根据配置和访问控制设置，在某些情况下，这可能会导致个人身份信息(PII)泄露，例如，当此类节点呈现为原始JSON或XML时。

与所有存储库数据一样，这些属性也由Oak授权栈栈来调节。 应根据最小特权原则限制对他们的访问。

为了支持这一点，Adobe提供了权限强化包，作为客户可以在此基础上进行构建的基础。 它的工作方式是在存储库根目录下安装“拒绝”访问控制条目，限制对常用系统属性的匿名访问。 该包可供下载 [此处](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) 并且可以安装在所有受支持的AEM版本上。

为了说明这些更改，我们可以比较在安装包之前可以匿名查看的节点属性：

![安装包之前](/help/sites-administering/assets/before_resized.png)

与安装包后可查看的那些组件进行比较，其中 `jcr:createdBy` 和 `jcr:lastModifiedBy` 不可见：

![安装包后](/help/sites-administering/assets/after_resized.png)

有关详细信息，请参阅包的发行说明。

### 防御点击劫持攻击 {#prevent-clickjacking}

为了防止点击劫持，Adobe建议您配置Web服务器以提供 `X-FRAME-OPTIONS` HTTP标头设置为 `SAMEORIGIN`.

有关点击劫持攻击的更多信息，请参见 [OWASP网站](https://www.owasp.org/index.php/Clickjacking).

### 确保在需要时正确复制加密密钥 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份验证方案要求您在所有AEM实例间复制加密密钥。

在执行此操作之前，不同版本之间的密钥复制执行方式不同，因为在6.3和更早版本之间，密钥的存储方式不同。

有关详细信息，请参阅下文。

#### 复制AEM 6.3的密钥 {#replicating-keys-for-aem}

而在旧版本中，复制密钥存储在存储库中，从AEM 6.3开始，它们存储在文件系统上。

因此，要跨实例复制密钥，请将密钥从源实例复制到文件系统上的目标实例位置。

更具体地说，您必须执行以下操作：

1. 访问包含要复制的关键资料的AEM实例（通常是创作实例）；
1. 在本地文件系统中找到com.adobe.granite.crypto.file包。 例如，在此路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   此 `bundle.info` 每个文件夹中的文件标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴您之前复制的两个文件。
1. [刷新加密捆绑包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目标实例已在运行。
1. 对要向其复制密钥的所有实例重复上述步骤。

#### 为AEM 6.2和更早版本复制密钥 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2及更早的版本中，密钥存储在存储库中的 `/etc/key` 节点。

跨实例安全复制密钥的推荐方法是仅复制此节点。 您可以通过CRXDE Lite有选择地复制节点：

1. 打开CRXDE Lite，方法是转到 *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. 选择 `/etc/key` 节点。
1. 转到 **复制** 选项卡。
1. 按 **复制** 按钮。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe建议您在开始生产之前对AEM基础架构执行渗透测试。

### 开发最佳实践 {#development-best-practices}

新的开发必须遵循 [安全最佳实践](/help/sites-developing/security.md) 以确保AEM环境保持安全。
