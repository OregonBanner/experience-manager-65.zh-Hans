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
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 部署社区{#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities许可证

* 针对以下对象的可选许可证：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [用于MSRP的MongoDB](/help/communities/msrp.md)
   * [适用于ASRP的Adobe Cloud](/help/communities/asrp.md)

## 安装核对清单 {#installation-checklist}

**对于[AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**

* 安装最 [新AEM 6.5更新](#aem64updates)

* 如果不使用默认端口(4502、4503)，则配置复 [制代理](#replication-agents-on-author)
* [复制加密密钥](#replicate-the-crypto-key)
* 如果支持全球化， [则设置自动翻译](/help/sites-administering/translation.md)（提供示例设置以供开发）

**对于“社[区”功能](/help/communities/overview.md)**

* 如果部署发 [布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [请标识主发布者](#primary-publisher)

* [启用隧道服务](#tunnel-service-on-author)
* [启用社交登录](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [配置Adobe Analytics](/help/communities/analytics.md)
* 设置默认 [电子邮件服务](/help/communities/email.md)
* 确定共享UGC [存储](/help/communities/working-with-srp.md) (**SRP**)的选择

   * 如果MongoDB SRP( [MSRP)](/help/communities/msrp.md)

      * [安装和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [选择MSRP](/help/communities/srp-config.md)
   * 如果关系数据库SRP( [DSRP)](/help/communities/dsrp.md)

      * [安装MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
      * [安装和配置MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [选择DSRP](/help/communities/srp-config.md)
   * 如果是Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * 与您的客户代表合作进行配置
      * [选择ASRP](/help/communities/srp-config.md)
   * 如果JCR SRP( [JSRP)](/help/communities/jsrp.md)

      * 不是共享的UGC存储：

         * UGC从未被复制
         * UGC仅在输入AEM实例或群集中可见
      * 默认为JSRP
   针对启 **[用功能](/help/communities/overview.md#enablement-community)**

   * [安装和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安装MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
   * [安装AEM Communities SCORM-Engine](#scorm-package)
   * [安装和配置MySQL以启用](/help/communities/mysql.md)






## Latest Releases {#latest-releases}

AEM 6.5 Communities GA随Communities包一起提供。 要了解AEM 6.5 [Communities的更新](/help/release-notes/release-notes.md#experiencemanagercommunities)，请参 [阅AEM 6.5发行说明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新 {#aem-updates}

从AEM 6.4开始，对Communities的更新将作为AEM累积修复包和服务包的一部分提供。

有关AEM 6.5的最新更新，请参阅 [Adobe Experience Manager 6.4累积修复包和服务包](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。

### 版本历史 {#version-history}

与在AEM 6.4及更高版本中一样，AEM Communities功能和修补程序是AEM Communities累积修复包和服务包的一部分。 因此，没有单独的功能包。

### MySQL的JDBC驱动程序 {#jdbc-driver-for-mysql}

“两个社区”功能使用MySQL数据库：

* 对于 [启用](/help/communities/enablement.md) :记录SCORM活动和学员
* 对于 [DSRP](/help/communities/dsrp.md) :存储用户生成的内容(UGC)

必须单独获取和安装MySQL连接器。

必要的步骤有：

1. 从https://dev.mysql.com/downloads/connector/j/下载ZIP存档文 [件](https://dev.mysql.com/downloads/connector/j/)

   * 版本必须>= 5.1.38

1. 从存档中提取mysql-connector-java-&lt;version>-bin.jar(bundle)
1. 使用Web控制台安装和开始捆绑包：

   * 例如，https://localhost:4502/system/console/bundles
   * 选择 **`Install/Update`**
   * 浏览……以选择从下载的ZIP存档中提取的包
   * 检查 *Oracle Corporation的MySQLcom.mysql.jdbc* JDBC驱动程序是否处于活动状态，如果未激活，请开始它（或检查日志）

1. 如果在配置JDBC后在现有部署上进行安装，则通过从Web控制台中重新保存JDBC配置，将JDBC重新绑定到新连接器：

   * 例如，https://localhost:4502/system/console/configMgr
   * 查找配 `Day Commons JDBC Connections Pool` 置
   * 选择以打开
   * 选择 `Save`

1. 对所有作者实例和发布实例重复步骤3和4

有关安装捆绑包的更多信息，请参阅 [Web控制台页](/help/sites-deploying/web-console.md) 。

#### 示例：已安装的MySQL连接器包 {#example-installed-mysql-connector-bundle}

![](/help/communities/assets/chlimage_1-125.png)

### SCORM包 {#scorm-package}

可共享内容对象参考模型(SCORM)是电子教学的标准和规范的集合。 SCORM还定义如何将内容打包到可转让的ZIP文件中。

AEM Communities SCORM引擎是启用功能的必 [需](/help/communities/overview.md#enablement-community) 。 AEM 6.5 Communities支持的Scorm包：

* [cq-social-scorm-package，版本2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ，其中包括 [SCORM 2017.1引擎](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 。

**安装SCORM包**

1. 从包 [共享安装cq-social-scorm-package版本2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) 。
1. 从cq `/libs/social/config/scorm/database_scormengine_data.sql` 实例下载并在mysql服务器中执行它以创建升级的scormEngineDB模式。
1. 在发 `/content/communities/scorm/RecordResults` 布者上的CSRF过滤器的“排除的路径”属性 `https://<hostname>:<port>/system/console/configMgr` 中添加。


#### SCORM日志记录 {#scorm-logging}

安装后，所有启用活动都会直接记录到系统控制台。

如果需要，可将包的日志级别设置为“警告” `RusticiSoftware.*` 。

有关使用日志的信息，请参 [阅使用审核记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。

### AEM Advanced MLS {#aem-advanced-mls}

为了支持高级多语言搜索(MLS)的SRP集合（MSRP或DSRP），除了自定义模式和Solr配置外，还需要新的Solr插件。 所有必需项都打包到一个可下载的zip文件中。

高级MLS下载（也称为“phasetwo”）可从Adobe存储库下载：

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 版本1.2.40,2016年4月6日
   * 下载AEM-SOLR-MLS-phasetwo-1.2.40.zip

有关详细信息和安装信息，请访 [问SRP的Solr Configuration](/help/communities/solr.md) 。

### 关于包共享的链接 {#about-links-to-package-share}

**Adobe AEM Cloud中可见的包**

此页面上指向包的链接不需要AEM的正在运行实例，因为它们要在上进行包共享 `adobeaemcloud.com`。 当可查看包时，该按 `Install` 钮用于将包安装到Adobe托管站点中。 如果打算安装在本地AEM实例上，选择 `Install` 将导致错误。

**如何在本地AEM实例上安装**

要安装本地AEM实例中 `adobeaemcloud.com` 可见的包，必须先将包下载到本地磁盘：

* Select the **Assets** tab
* 选择 **下载到磁盘**

在本地AEM实例上，使用包管理器(例如 [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))上传到本地AEM的包存储库。

或者，也可以使用包共享从本地AEM实例(例如， [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))访问包，该按钮将下载 `Download` 到本地AEM实例的包存储库。

进入本地AEM实例的包存储库后，使用包管理器安装该包。

有关详细信息，请 [访问How to Work With Packages](/help/sites-administering/package-manager.md#package-share)。

## 建议的部署 {#recommended-deployments}

在AEM Communities中，公用存储用于存储用户生成的内容(UGC)，通常称为 [存储资源提供商(SRP)](/help/communities/working-with-srp.md)。 建议的部署中心是为公用商店选择SRP选项。

公共存储支持发布环境中UGC的协调和分析，同时消除了复制UGC [的需](/help/communities/sync.md) 求。

* [社区内容商店](/help/communities/working-with-srp.md) :讨论AEM社区的SRP存储选项

* [推荐的拓扑](/help/communities/topologies.md) :根据用例和SRP选择讨论要使用的拓扑

## 升级 {#upgrading}

从AEM的先前版本升级到AEM 6.5平台时，请务必阅读升 [级到AEM 6.5](/help/sites-deploying/upgrade.md)。

除了升级平台，请阅读升 [级到AEM Communities 6.5](/help/communities/upgrade.md) ，了解社区更改。

## 配置 {#configurations}

### 主发布者 {#primary-publisher}

如果选择的部署是 [发布场](/help/communities/topologies.md#tarmk-publish-farm)，则必须将一个AEM发布实例标识为不应出现在所有实例(如依赖通知或 **`primary publisher`** Adobe Analytics的功能)上的活动 ********。

默认情况下， `AEM Communities Publisher Configuration` OSGi配置中选中了该复选 **`Primary Publisher`** 框，这样发布群中的所有发布实例都将自标识为主实例。

因此，必须编辑所有次 **要发布实例上的配置** ，以取消选中此复 **`Primary Publisher`** 选框。

![](/help/communities/assets/chlimage_1-126.png)

对于发布场中的所有其他（辅助）发布实例：

* 以管理员权限登录
* 访问Web [控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到 `AEM Communities Publisher Configuration`
* 选择编辑图标
* 取消选中“ **主发布者** ”框
* Select **Save**

### 作者上的复制代理 {#replication-agents-on-author}

复制用于在发布环境中创建的站点内容（如社区组），以及使用隧道服务管理创作环境的成员和成 [员组](#tunnel-service-on-author)。

对于主发布者，确保复 [](/help/sites-deploying/replication.md) 制代理配置正确标识发布服务器和授权用户。 默认的授权用 `admin,` 户已拥有相应权限(是的成员 `Communities Administrators`)。

要使某些其他用户具有相应的权限，必须将他们添加为用户组(也 `administrators` 是用户组的成员 `Communities Administrators`)。

创作环境中有两个复制代理需要正确配置传输配置。

* 在创作时访问复制控制台

   * 在全局导航中，导航到工 **[!UICONTROL 具>部署>复制>作者代理]**

* 对于两个代理，请遵循相同的流程：

   * **默认代理（发布）**
   * **反向复制代理（发布反向）**

      1. 选择代理
      1. Select **edit**
      1. Select the **Transport** tab
      1. 如果不是端 `4503`口，请编辑 **URI** ，以指定正确的端口

      1. 如果不是用 `admin`户，请编辑 **“用户** ”和“口 **令** ”以指定用户组的 `administrators` 成员

下图显示了将端口从4503更改为6103的结果：

#### 默认代理（发布） {#default-agent-publish}

![](/help/communities/assets/chlimage_1-127.png)

#### 反向复制代理（发布反向） {#reverse-replication-agent-publish-reverse}

![](/help/communities/assets/chlimage_1-128.png)

### 作者通道服务 {#tunnel-service-on-author}

使用创作环境创 [建站点](/help/communities/sites-console.md)、修改站点属性 [或管理社区成员时](/help/communities/sites-console.md#modifying-site-properties)[](/help/communities/members.md)，必须访问在发布环境中注册的成员（用户），而不是访问在创作中注册的用户。

隧道服务使用作者上的复制代理提供此访问。

要启用隧道服务，请执行以下操作：

* 论作 **者**
* 使用管理权限登录
* 如果发布者不是localhost:4503或传输用户不是， `admin`请配 [置复制代理](#replication-agents-on-author)

* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到 `AEM Communities Publish Tunnel Service`
* 选择编辑图标
* 选中“ **启用** ”框
* Select **Save**

![](/help/communities/assets/chlimage_1-129.png)

### 复制加密密钥 {#replicate-the-crypto-key}

AEM Communities有两项功能，它们要求所有AEM服务器实例使用相同的加密密钥。 这些是 [Analytics](/help/communities/analytics.md) 和 [ASRP](/help/communities/asrp.md)。

从AEM 6.3开始，密钥材料存储在文件系统中，而不再存储在存储库中。

要将关键材料从作者复制到所有其他实例，必须：

* 访问AEM实例（通常为作者实例），该实例包含要复制的关键材料

   * 在本地 `com.adobe.granite.crypto.file` 文件系统中找到捆绑包，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * 文 `bundle.info` 件将识别捆绑包
   * 导航到数据文件夹，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 复制hmac和主文件



* 对于每个目标AEM实例

   * 导航到数据文件夹，例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 粘贴之前复制的2个文件
   * 如果目标AEM实 [例当前正在运行](#refresh-the-granite-crypto-bundle) ，则必须刷新Granite Crypto包


>[!CAUTION]
>
>如果已经配置了基于加密密钥的其他安全功能，则复制加密密钥可能会损坏配置。 要获得帮助，请 [联系客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)。

#### 存储库复制 {#repository-replication}

将关键材料存储在存储库中（与AEM 6.2及更早版本一样），可通过在每个AEM实例（创建初始存储库）的首次启动时指定以下系统属性来保留：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>请务必验证作者上的复 [制代理是否正确配置](#replication-agents-on-author) 。

将密钥材料存储在存储库中后，将加密密钥从作者复制到其他实例的方式如下：

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* 浏览 [到https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 选择 `/etc/key`
* 打开选 `Replication` 项卡
* 选择 `Replicate`

* [刷新Granite加密捆绑](#refresh-the-granite-crypto-bundle)

![](/help/communities/assets/chlimage_1-130.png)

#### 刷新Granite加密捆绑 {#refresh-the-granite-crypto-bundle}

* 在每个发布实例上，访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找 `Adobe Granite Crypto Support` 到捆绑包(com.adobe.granite.crypto)
* 选择刷 **新**

![](/help/communities/assets/chlimage_1-131.png)

* 稍后，应显示“ **成功** ”对话框：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP服务器，请确保对所有相关条目使用正确的服务器名称。

尤其要注意在中使用正确的服务器名 `localhost`称，而不是 `RedirectMatch`。

#### httpd.conf示例 {#httpd-conf-sample}

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

* AEM的 [Dispatcher文档](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [安装 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [为社区配置调度程序](/help/communities/dispatcher.md)
* [已知问题](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相关社区文档 {#related-communities-documentation}

* 访问 [管理社区站点](/help/communities/administer-landing.md) ，了解如何创建社区站点、配置社区站点模板、协调社区内容、管理成员和配置消息。

* 访问 [开发社区](/help/communities/communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问 [创作社区组件](/help/communities/author-communities.md) ，了解如何创作和配置社区组件。

