---
title: Salesforce商务云
seo-title: Salesforce Commerce Cloud / Demandware
description: 了解如何使用Salesforce Commerce Cloud / Demandware部署电子商务。
seo-description: 了解如何使用Salesforce Commerce Cloud / Demandware部署电子商务。
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Salesforce商务云{#salesforce-commerce-cloud}

部署必要的电子商务包将提供电子商务框架的完整功能，以及随Salesforce Commerce Cloud/Demandware实施（包括演示目录）提供的电子商务功能的参考实施。

## 使用Salesforce Commerce cloud进行电子商务所需的包 {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}

要安装电子商务功能，您需要：

* AEM eCommerce framework:

   * 这是标准AEM安装的一部分

* AEM Demandware商务内容包

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>此集成支持配置为使用OCAPI 17.6版或更高版本的Salesforce Commerce Cloud / Demandware实例。

### 使用Salesforce Commerce cloud安装电子商务 {#installation-of-ecommerce-with-salesforce-commerce-cloud}

要安装AEM及Demandware Commerce集成配置（使用演示目录Geometrixx Outdoors），基本步骤为：

1. [安装AEM](/help/sites-deploying/deploy.md)。
1. 使用包管理器安装内 [容包](/help/sites-administering/package-manager.md):
1. [在AEM中](/help/sites-authoring/page-authoring.md) ，创作您需要的任何补充页面。

>[!NOTE]
>
>要下载包，请导航到包 [共享](/help/sites-administering/package-manager.md#package-share)。

需要配置AEM与Demandware沙箱之间的服务器连接。 大多数配置都已预配置为使用默认路径、库等与提供的SiteGenisis演示内容包一起使用。 如果该连接器与其他站点和库一起使用，您需要更新此配置。

1. 导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 单击“ **Demandware客户端**”。
1. 根据需要 **输入实例端点ip或hostname** 。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 单击&#x200B;**保存**。
1. 单击 **Demandware TransportHandler Plugin for webDAV**。
1. 设置 **WebDAV用户和****WebDAV用户密码**。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 单击&#x200B;**保存**。

#### 复制 {#replication}

在安装包后应启用复制，您可以在此处验证： [https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>默认情况下，复制代理配置为信息日志级别。 如果您想获得更多信息，可以将日志级别切换为调试。

#### OAuth {#oauth}

OAuth客户端配置为与Demandware沙箱实例一起使用。 出于测试目的，无需更改。

对于暂存和生产系统，需要为OAuth客户端配置相应的客户端ID和密码。

1. 导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 单击“ **Demandware访问令牌提供程序”**。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 根据需要修改值，然后单击“保 **存”**。

### Salesforce商务云沙箱 {#salesforce-commerce-cloud-sandbox}

必须将Demandware沙箱配置为运行新的Velocity模板引擎。

>[!NOTE]
>
>以下向导不是AEM Demandware连接器的一部分。 它按原样提供，作为演示内容包的一部分，以帮助快速设置SiteGenesis演示页面。

1. 导航到 [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html)。
1. Click **Edit.**
1. 验证值，然后单击“ **确定”**。
1. 单击 **初始化**。
1. 转到WebDAV文件夹并检查已发布的模板文件，例如在下 `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`。

   >[!NOTE]
   >
   >此扩展将为 `.vs`。

1. 另请检查导出的JS和CSS文件，例如 `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`。

