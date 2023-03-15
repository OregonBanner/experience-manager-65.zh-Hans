---
title: 解决方案集成
seo-title: Solutions Integration
description: 详细了解AEM中的解决方案集成。
seo-description: Learn more about Solutions Integration in AEM.
uuid: 3bf56b1b-284d-4f14-8974-0a595ece5028
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b5ff918d-08ab-4307-a807-693468fc083b
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 32%

---

# 解决方案集成{#solutions-integration}

* [与Adobe Marketing Cloud集成](/help/sites-administering/marketing-cloud.md)
* [与第三方服务集成](/help/sites-administering/third-party-services.md)
* [Analytics与外部提供程序](/help/sites-administering/external-providers.md)
* [目录生成器](/help/sites-administering/catalog-producer.md)
* [SharePoint连接器](/help/sites-administering/sharepoint-connector.md)

以下信息介绍了如何将AEM与其他Adobe或第三方服务集成：

>[!NOTE]
>
>如果您将自定义代理配置与集成结合使用，则需要配置HTTP客户端代理配置，因为AEM的某些功能使用的是3.x API，而其他一些功能使用的是4.x API：
>
>* 3.x 通过 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 进行配置
>* 4.x 通过 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) 进行配置
>

