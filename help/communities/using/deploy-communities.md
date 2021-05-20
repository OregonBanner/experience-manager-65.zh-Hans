---
title: 部署社区
seo-title: 部署社区
description: 如何部署AEM Communities
seo-description: 如何部署AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 2%

---


# 部署Communities{#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities许可证

* 可选许可证：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [用于MSRP的MongoDB](/help/communities/msrp.md)
   * [适用于ASRP的Adobe云](/help/communities/asrp.md)

## 安装核对清单{#installation-checklist}

**对于 [AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**:

* 安装最新的[AEM 6.5更新](#aem64updates)。

* 如果未使用默认端口(4502、4503)，则[配置复制代理](#replication-agents-on-author)。
* [复制加密密钥](#replicate-the-crypto-key)
* 如果支持全球化，请[设置自动翻译](/help/sites-administering/translation.md)
（提供开发示例设置）。

**对于“社 [区”功能](/help/communities/overview.md)**:

* 如果部署[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，则[标识主发布者](#primary-publisher)

* [启用隧道服务](#tunnel-service-on-author)
* [启用社交登录](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [配置Adobe Analytics](/help/communities/analytics.md)
* 设置[默认电子邮件服务](/help/communities/email.md)
* 识别[共享UGC存储](/help/communities/working-with-srp.md)(**SRP**)的选择

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安装和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [选择MSRP](/help/communities/srp-config.md)
   * 如果关系数据库SRP [(DSRP)](/help/communities/dsrp.md)

      * [安装MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
      * [安装和配置用于DSRP的MySQL](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [选择DSRP](/help/communities/srp-config.md)
   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 与您的客服专员合作进行配置。
      * [选择ASRP](/help/communities/srp-config.md)
   * 如果JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共享的UGC存储：

         * UGC从未复制过。
         * UGC仅在输入UGC的实例或群集上可见。
      * 默认值为JSRP

   对于&#x200B;**[启用功能](/help/communities/overview.md#enablement-community)**

   * [安装和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安装MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
   * [安装AEM Communities SCORM引擎](#scorm-package)
   * [安装和配置MySQL以启用](/help/communities/mysql.md)






## 最新版本{#latest-releases}

AEM 6.5 Communities GA包含Communities包。 要了解AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)的更新，请参阅[AEM 6.5发行说明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新{#aem-updates}

从AEM 6.4开始，对Communities的更新将作为AEM累积修补程序包和Service Pack的一部分提供。

有关AEM 6.5的最新更新，请参阅[Adobe Experience Manager 6.4累积修补程序包和Service Pack](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。

### 版本历史记录{#version-history}

与AEM 6.4及更高版本一样，AEM Communities功能和修补程序是AEM Communities累积修补程序包和Service Pack的一部分。 因此，没有单独的功能包。

### MySQL {#jdbc-driver-for-mysql}的JDBC驱动程序

“两个社区”功能使用MySQL数据库：

* 对于[enablement](/help/communities/enablement.md):记录SCORM活动和学习者
* 对于[DSRP](/help/communities/dsrp.md):存储用户生成的内容(UGC)

必须单独获取和安装MySQL连接器。

必要步骤包括：

1. 从[https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)下载ZIP存档

   * 版本必须>= 5.1.38

1. 提取 `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. 使用Web控制台安装并启动包：

   * 例如， https://localhost:4502/system/console/bundles
   * 选择 **`Install/Update`**
   * 浏览……以选择从下载的ZIP存档中提取的包
   * 检查&#x200B;*Oracle公司的MySQLcom.mysql.jdbc* JDBC驱动程序是否处于活动状态，如果未活动，则启动该驱动程序（或检查日志）

1. 如果在配置JDBC后在现有部署上进行安装，则通过从Web控制台重新保存JDBC配置，将JDBC重新绑定到新连接器：

   * 例如， https://localhost:4502/system/console/configMgr
   * 找到`Day Commons JDBC Connections Pool`配置，然后选择以打开该配置。
   * 选择 `Save`.

1. 对所有创作实例和发布实例重复步骤3和4。

有关安装包的更多信息，请参阅[Web控制台](/help/sites-deploying/web-console.md#bundles)页面。

#### 示例：已安装的MySQL连接器包{#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### SCORM包{#scorm-package}

可共享内容对象引用模型(SCORM)是用于电子学习的标准和规范的集合。 SCORM还定义如何将内容打包到可传输的ZIP文件中。

[enablement](/help/communities/overview.md#enablement-community)功能需要AEM Communities SCORM引擎。 AEM 6.5 Communities支持的Scorm包：

* [cq-social-scorm-package，版本2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ，其中包含 [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

**安装SCORM包**

1. 从包共享中安装[cq-social-scorm-package，版本2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)
1. 从cq实例下载`/libs/social/config/scorm/database_scormengine_data.sql`并在mysql服务器中执行该实例，以创建已升级的scormEngineDB模式。
1. 在发布者的`https://<hostname>:<port>/system/console/configMgr`筛选器中的CSRF的“排除的路径”属性中添加`/content/communities/scorm/RecordResults`。

#### SCORM日志记录{#scorm-logging}

安装后，所有启用活动都会被垂直记录到系统控制台。

如果需要，可以将`RusticiSoftware.*`包的日志级别设置为“警告”。

有关使用日志的信息，请参阅[使用审核记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。

### AEM Advanced MLS {#aem-advanced-mls}

为了支持高级多语言搜索(MLS),SRP集合（MSRP或DSRP）除了自定义架构和Solr配置外，还需要新的Solr插件。 所有必需项目都打包到一个可下载的zip文件中。

高级MLS下载（也称为“第二阶段”）可从Adobe存储库中获取：

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 1.2.40版，2016年4月6日
   * 下载AEM-SOLR-MLS-phasetwo-1.2.40.zip

有关详细信息和安装信息，请访问[Solr Configuration](/help/communities/solr.md) for SRP。

### 关于包共享{#about-links-to-package-share}的链接

**包在AdobeAEM Cloud中可见**

指向此页面上的包的链接不需要运行AEM实例，因为它们要在`adobeaemcloud.com`上包共享。 当可以查看包时， `Install`按钮用于将包安装到Adobe托管站点中。 如果打算在本地AEM实例上安装，则选择`Install`将导致错误。

**如何在本地AEM实例上安装**

要在本地AEM实例上安装`adobeaemcloud.com`中可见的包，必须先将该包下载到本地磁盘：

* 选择&#x200B;**Assets**&#x200B;选项卡
* 选择&#x200B;**下载到磁盘**

在本地AEM实例上，使用包管理器(例如[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，将包上传到本地AEM包存储库。

或者，使用包共享从本地AEM实例访问包(例如，[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), `Download`按钮将下载到本地AEM实例的包存储库。

在本地AEM实例的包存储库中，使用包管理器安装包。

有关更多信息，请访问[如何使用包](/help/sites-administering/package-manager.md#package-share)。

## 建议的部署{#recommended-deployments}

在AEM Communities中，公共存储用于存储用户生成的内容(UGC)，通常称为[存储资源提供程序(SRP)](/help/communities/working-with-srp.md)。 推荐的部署中心是为公共存储选择SRP选项。

公共存储支持在发布环境中审核UGC并对其进行分析，同时无需复制UGC的[](/help/communities/sync.md)。

* [社区内容存储](/help/communities/working-with-srp.md) :讨论了AEM社区的SRP存储选项

* [推荐的拓扑](/help/communities/topologies.md) :根据用例和SRP选择，讨论要使用的拓扑

## 升级 {#upgrading}

从AEM的先前版本升级到AEM 6.5平台时，请务必阅读[升级到AEM 6.5](/help/sites-deploying/upgrade.md)。

除了升级平台之外，请阅读[升级到AEM Communities 6.5](/help/communities/upgrade.md)以了解社区更改。

## 配置 {#configurations}

### 主发布者{#primary-publisher}

如果选择的部署是[发布场](/help/communities/topologies.md#tarmk-publish-farm)，则对于不应出现在所有实例上的活动(例如依赖于&#x200B;**notifications**&#x200B;或&#x200B;**Adobe Analytics**&#x200B;的功能)，必须将一个AEM发布实例标识为&#x200B;**`primary publisher`**。

默认情况下， `AEM Communities Publisher Configuration` OSGi配置配置有选中的&#x200B;**`Primary Publisher`**&#x200B;复选框，这样发布场中的所有发布实例都将自标识为主实例。

因此，必须&#x200B;**编辑所有辅助发布实例上的配置**&#x200B;以取消选中&#x200B;**`Primary Publisher`**&#x200B;复选框。

![](../assets/primary-publisher.png)

对于发布场中的所有其他（辅助）发布实例：

* 使用管理员权限登录
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Publisher Configuration`
* 选择编辑图标
* 取消选中&#x200B;**Primary Publisher**&#x200B;复选框
* 选择&#x200B;**Save**

### 创作{#replication-agents-on-author}上的复制代理

复制用于在发布环境中创建的站点内容（如社区组），以及使用[tunnel service](#tunnel-service-on-author)从创作环境中管理成员和成员组。

对于主发布者，请确保[复制代理配置](/help/sites-deploying/replication.md)正确标识发布服务器和授权用户。 默认的授权用户`admin`已具有相应的权限（是`Communities Administrators`的成员）。

为了使某些其他用户具有相应的权限，必须将他们作为成员添加到`administrators`用户组（也是`Communities Administrators`的成员）。

创作环境中有两个复制代理需要正确配置传输配置。

* 在创作时访问复制控制台

   * 从全局导航：**工具、部署、复制、作者代理**

* 对于两个代理，请遵循相同的过程：

   * **默认代理（发布）**
   * **反向复制代理（发布反向）**

      1. 选择代理。
      1. 选择&#x200B;**edit**。
      1. 选择&#x200B;**传输**&#x200B;选项卡
      1. 如果不是端口`4503`，请编辑&#x200B;**URI**&#x200B;以指定正确的端口。

      1. 如果不是用户`admin`，请编辑&#x200B;**User**&#x200B;和&#x200B;**Password**&#x200B;以指定`administrators`用户组的成员。

下图显示了将端口从4503更改为6103的结果：

#### 默认代理（发布）{#default-agent-publish}

![配置限制](../assets/default-agent-publish.png)

#### 反向复制代理（发布反向）{#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### 创作{#tunnel-service-on-author}上的隧道服务

使用创作环境创建站点](/help/communities/sites-console.md)、[修改站点属性](/help/communities/sites-console.md#modifying-site-properties)或[管理社区成员](/help/communities/members.md)时，必须访问在发布环境中注册的成员（用户），而不是在创作中注册的用户。[

隧道服务使用作者上的复制代理提供此访问。

要启用隧道服务，请执行以下操作：

* 在&#x200B;**author**&#x200B;上，使用管理权限登录。
* 如果发布者不是localhost:4503或传输用户不是`admin`,
然后， [配置复制代理](#replication-agents-on-author)。

* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到`AEM Communities Publish Tunnel Service`
* 选择编辑图标
* 选中&#x200B;**enable**&#x200B;复选框
* 选择&#x200B;**Save**

![](../assets/tunnel-service.png)

### 复制加密密钥{#replicate-the-crypto-key}

AEM Communities有两项功能，要求所有AEM服务器实例使用相同的加密密钥。 这些参数为[Analytics](/help/communities/analytics.md)和[ASRP](/help/communities/asrp.md)。

自AEM 6.3起，关键材料将存储在文件系统中，而不再存储在存储库中。

要将关键材料从作者复制到所有其他实例，必须：

* 访问包含要复制的关键材料的AEM实例（通常为创作实例）

   * 在本地文件系统中找到`com.adobe.granite.crypto.file`包

      例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`文件将标识包
   * 导航到数据文件夹
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 复制hmac和主节点文件。



* 对于每个目标AEM实例

   * 导航到数据文件夹
例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 粘贴之前复制的2个文件
   * 如果目标AEM实例当前正在运行，则需要[刷新Granite Crypto包](#refresh-the-granite-crypto-bundle)。


>[!CAUTION]
>
>如果已配置基于加密密钥的其他安全功能，则复制加密密钥可能会损坏配置。 如需帮助，请[联系客户关怀团队](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)。

#### 存储库复制{#repository-replication}

与AEM 6.2及更早版本一样，将关键材料存储在存储库中，可通过在每个AEM实例（创建初始存储库）的首次启动时指定以下系统属性来保留该关键材料：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>务必验证作者](#replication-agents-on-author)上的[复制代理是否正确配置。

将密钥材料存储在存储库中后，将加密密钥从创作复制到其他实例的方式如下：

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* 浏览到[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 选择 `/etc/key`
* 打开`Replication`选项卡
* 选择 `Replicate`

* [刷新Granite加密包](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### 刷新Granite加密包{#refresh-the-granite-crypto-bundle}

* 在每个发布实例上，访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找到`Adobe Granite Crypto Support`包(com.adobe.granite.crypto)
* 选择&#x200B;**刷新**

![](../assets/refresh-granite-bundle.png)

* 片刻后，应会显示&#x200B;**Success**对话框：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP服务器，请确保对所有相关条目使用正确的服务器名称。

特别是，在`RedirectMatch`中要小心使用正确的服务器名称，而不是`localhost`。

#### httpd.conf示例{#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

如果使用Dispatcher，请参阅：

* AEM [ Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)文档
* [安装 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [为社区配置Dispatcher](/help/communities/dispatcher.md)
* [已知问题](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相关社区文档{#related-communities-documentation}

* 访问[管理社区站点](/help/communities/administer-landing.md) ，了解有关创建社区站点、配置社区站点模板、审核社区内容、管理成员和配置消息传送的信息。

* 访问[开发社区](/help/communities/communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问[创作社区组件](/help/communities/author-communities.md) ，了解如何使用和配置社区组件进行创作。

