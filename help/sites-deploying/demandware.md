---
title: SalesforceCommerce Cloud
seo-title: SalesforceCommerce Cloud/ Demandware
description: 了解如何使用SalesforceCommerce Cloud/ Demandware部署电子商务。
seo-description: 了解如何使用SalesforceCommerce Cloud/ Demandware部署电子商务。
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# SalesforceCommerce Cloud{#salesforce-commerce-cloud}

部署必要的电子商务包将提供电子商务框架的完整功能，以及随SalesforceCommerce Cloud/Demandware实施（包括演示目录）提供的电子商务功能的参考实施。

## 使用SalesforceCommerce Cloud{#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}进行电子商务所需的包

要安装电子商务功能，您需要：

* AEM电子商务框架：

   * 这是标准AEM安装的一部分

* AEM Demandware Commerce内容包

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>此集成支持配置为使用OCAPI版本17.6或更高版本的SalesforceCommerce Cloud/ Demandware实例。

### 使用SalesforceCommerce Cloud{#installation-of-ecommerce-with-salesforce-commerce-cloud}安装电子商务

要安装AEM和Demandware Commerce集成配置(使用演示目录和Geometrixx Outdoors)，基本步骤如下：

1. [安装AEM](/help/sites-deploying/deploy.md)。
1. 使用[包管理器](/help/sites-administering/package-manager.md)安装内容包：
1. [](/help/sites-authoring/page-authoring.md) 创作您在AEM中需要的任何补充页面。

>[!NOTE]
>
>要下载包，请导航到[包共享](/help/sites-administering/package-manager.md#package-share)。

需要配置AEM与Demandware沙盒之间的服务器连接。 大多数配置都已预配置为使用提供的SiteGenis演示内容包（使用默认路径、库等）。 如果连接器与其他站点和库一起使用，则需要更新此配置。

1. 导航到[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 单击&#x200B;**Demandware Client**。
1. 根据需要输入&#x200B;**实例端点ip或主机名**。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 单击&#x200B;**保存**。
1. 单击&#x200B;**Demandware TransportHandler Plugin for WebDAV**。
1. 设置&#x200B;**WebDAV用户**&#x200B;和&#x200B;**WebDAV用户密码**。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 单击&#x200B;**保存**。

#### 复制 {#replication}

应在安装包后启用复制，您可以在此处验证：[https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>默认情况下，复制代理配置为信息日志级别。 如果您想了解更多信息，可以将日志级别切换为调试。

#### OAuth {#oauth}

OAuth客户端配置为与Demandware沙盒实例一起使用。 出于测试目的，无需进行任何更改。

对于暂存和生产系统，需要为OAuth客户端配置适当的客户端ID和密码。

1. 导航到[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 单击&#x200B;**Demandware访问令牌提供程序**。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 根据需要修改值，然后单击&#x200B;**Save**。

### SalesforceCommerce Cloud沙盒{#salesforce-commerce-cloud-sandbox}

必须将Demandware沙盒配置为运行新的Velocity模板引擎。

>[!NOTE]
>
>以下向导不是AEM Demandware连接器的一部分。 它作为演示内容包的一部分提供，以帮助快速设置SiteGenesis演示页面。

1. 导航到[https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html)。
1. 单击&#x200B;**编辑。**
1. 验证值并单击&#x200B;**确定**。
1. 单击&#x200B;**初始化**。
1. 转到WebDAV文件夹并检查已发布的模板文件，例如在`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`下。

   >[!NOTE]
   >
   >扩展将为`.vs`。

1. 另请检查导出的JS和CSS文件，例如在`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`下。

