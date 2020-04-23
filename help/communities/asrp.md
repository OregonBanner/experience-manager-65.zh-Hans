---
title: ASRP - Adobe存储资源提供商
seo-title: ASRP - Adobe存储资源提供商
description: 设置AEM Communities以使用关系数据库作为其公用存储
seo-description: 设置AEM Communities以使用关系数据库作为其公用存储
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# ASRP - Adobe存储资源提供商 {#asrp-adobe-storage-resource-provider}

## 关于ASRP {#about-asrp}

将AEM Communities配置为使用ASRP作为其公用存储时，用户生成的内容(UGC)可从所有作者和发布实例访问，无需同步或复制。

另请参 [阅SRP选项的特性](/help/communities/working-with-srp.md#characteristics-of-srp-options) 和建 [议的拓扑](/help/communities/topologies.md)。

## 要求 {#requirements}

使用ASRP需要额外的许可。

要将AEM Communities站点配置为使用UGC的ASRP，请与您的客户代表联系，以了解：

* 数据中心URL（ASRP端点的地址）
* 使用者密钥
* 密钥
* 报告套件ID

消费者密钥和机密密钥在所有报表包中共享，用于公司。 每个租户有一个报告套件。

## 配置 {#configuration}

### 选择ASRP {#select-asrp}

存储配 [置控制台允许选择默认存储配置](/help/communities/srp-config.md) ，该配置标识要使用的SRP的实现。

**在AEM作者实例上：**

* 从全局导航中，导航到工 **[!UICONTROL 具>社区>存储配置]** ，然后选择 **[!UICONTROL Adobe存储资源提供商(ASRP)]**。

![chlimage_1-30](assets/chlimage_1-30.png)

以下信息来自供应过程：

* **数据中心URL**:下拉框可选择由您的客户代表标识的生产数据中心。
* **默认报表包**:输入默认报表包的名称。
* **消费方密钥**:输入消费方密钥。
* **秘密**:输入机密。
* 选择&#x200B;**提交**。

准备发布实例：

* [复制加密密钥](#replicate-the-crypto-key)
* [复制配置](#publishing-the-configuration)

提交配置后，测试连接：

* 选择 **测试配置**。

   对于每个作者实例和发布实例，从“存储配置”控制台测试与数据中心的连接。

* 通过将链接外置，确保用户档案数据的站点URL可从数据中心 [路由](#externalize-links)。

### 复制加密密钥 {#replicate-the-crypto-key}

消费方密钥和密钥已加密。 要正确加密／解密密钥，主Granite加密密钥必须在所有AEM实例上相同。

请按照复制加密 [密钥中的说明操作](/help/communities/deploy-communities.md#replicate-the-crypto-key)。

### 将链接外置 {#externalize-links}

要获得正确的用户档案和用户档案图像链接，请务必正确 [配置链接外部器](/help/sites-developing/externalizer.md)。

请务必将域设置为可从数据中心URL（ASRP端点）路由的URL。

### 时间同步 {#time-synchronization}

要成功与ASRP端点进行身份验证，运行托管AEM Communities的计算机必须进行时间同步，如与网络时间协议( [NTP)同步](https://www.ntp.org/)。

### 发布配置 {#publishing-the-configuration}

ASRP必须被标识为所有作者实例和发布实例上的公用商店。

要在发布环境中提供相同的配置，请执行以下操作：

在AEM作者实例上：

* 从主菜单导航到工 **[!UICONTROL 具>操作>复制]**。
* 选择 **激活树**
* **开始路径**:浏览至 `/etc/socialconfig/srpc/`
* 取消选择 **仅已修改**
* 选择激 **活**

## 从AEM 6.0升级 {#upgrading-from-aem}

>[!CAUTION]
>
>如果在已发布的社区站点上启用ASRP，则 [JCR](/help/communities/jsrp.md) 中已存储的任何UGC都不再可见，因为内部部署存储和云存储之间不会同步数据。

**`AEM Communities Extension`** 之前在AEM 6.0社交社区中作为云服务引入。 自AEM 6.1 Communities起，无需云配置，只需从存储配置控制台中选择 [ASRP即可](/help/communities/srp-config.md)。

由于新的存储结构，从社交社区升级到社区时，必 [须按照](/help/communities/upgrade.md#adobe-cloud-storage) “升级说明”进行操作。

## 管理用户数据 {#managing-user-data}

有关用户、用 *户用户档案****、用户*&#x200B;环境和用户组的信息，请访问

* [用户同步](/help/communities/sync.md)
* [管理用户和用户组](/help/communities/users.md)

## 疑难解答 {#troubleshooting}

### 升级后UGC消失 {#ugc-disappears-after-upgrade}

如果从现有AEM 6.0社交社区站点升级，请务必按照升级说 [明操作](/help/communities/upgrade.md#adobe-cloud-storage)，否则UGC将丢失。

### 身份验证错误 {#authentication-errors}

如果收到针对数据中心URL的身份验证错误，且AEM error.log包含有关过时时间戳的消息，则验证是否正在进行时间同步。

使用网络时间协 [议(NTP)等工具](https://www.ntp.org/) ，对所有AEM作者和发布服务器进行时间同步。

### 搜索中不显示新内容 {#new-content-does-not-appear-in-searches}

Adobe云存储基础结构使用最 *终的一致性* ，实现其扩展和性能目标。 因此，新内容不会立即可用，并且在搜索结果中显示需要几秒钟。

当监视影响最终一致性的间隔时，如果新内容在搜索中显示的时间超过几秒，请与您的帐户代表联系。

### UGC在ASRP中不可见 {#ugc-not-visible-in-asrp}

通过检查存储选项的配置，确保ASRP已配置为默认提供者。 默认情况下，存储资源提供者是JSRP，而不是ASRP。

在所有作者和发布AEM实例上，重新访问存储配置控制台或检查AEM存储库。

在JCR中，if [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 不包含 [srpc节点](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，这表示存储提供者是JSRP。
* 如果srpc节点存在并包含节点 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则默认配置的属性将ASRP定义为默认提供者。

