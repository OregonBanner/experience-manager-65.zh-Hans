---
title: 解决方案集成
description: 了解关于将Adobe Experience Manager (AEM)与其他Adobe或第三方服务集成的更多信息。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 11%

---

# 解决方案集成{#solutions-integration}

* [与Adobe Experience Cloud集成](/help/sites-administering/marketing-cloud.md)
* [与第三方服务集成](/help/sites-administering/third-party-services.md)
* [Analytics与外部提供程序](/help/sites-administering/external-providers.md)
* [目录生成器](/help/sites-administering/catalog-producer.md)
* [SharePoint连接器](/help/sites-administering/sharepoint-connector.md)
* [了解、应用和策划智能标记](/help/assets/enhanced-smart-tags.md)

以下信息可用于将AEM与其他Adobe或第三方服务集成：

>[!NOTE]
>
>如果您将自定义代理配置与集成一起使用，则必须同时配置HTTP客户端代理配置，因为AEM的某些功能使用的是3.x API，而其他一些功能使用的是4.x API：
>
>* 3.x 通过 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 进行配置
>* 4.x 通过 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) 进行配置
>
