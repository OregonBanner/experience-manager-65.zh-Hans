---
title: 与 Adobe Analytics 集成
description: 了解如何将Adobe Experience Manager (AEM)与Adobe Analytics集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 58%

---

# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html) |
| AEM 6.5 | 本文 |


通过将Adobe Analytics与AEM集成，您可以跟踪您的网页活动：

* Adobe Analytics 配置可让 AEM 通过 Adobe Analytics 进行身份验证。
* 框架标识发送到 Adobe Analytics 报告包的数据。

该数据包括页面和用户数据；例如：

* AEM 组件收集的数据
* 链接点击次数
* 视频使用信息
* 来自 Adobe Analytics 的页面访问次数

以下页面可帮助您配置集成：

* [连接到Adobe Analytics并创建框架](/help/sites-administering/adobeanalytics-connect.md)
* [为Adobe Analytics配置链接跟踪](/help/sites-administering/adobeanalytics-link.md)
* [将组件数据映射到Adobe Analytics属性](/help/sites-administering/adobeanalytics-mapping.md)
* [为Adobe Analytics配置视频跟踪](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分类](/help/sites-administering/adobeanalytics-classifications.md)

您也可以使用 [选择加入向导](/help/sites-administering/opt-in.md) 以轻松执行集成。

>[!NOTE]
>
>另请参阅操作方法文章： [使用DTM将AEM与Adobe Target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics集成](/help/sites-developing/extending-analytics.md) 有关开发用于收集用户数据的组件和自定义Adobe Analytics框架的信息。
* 知识库文章 [Adobe Analytics 集成 – 解决问题](https://helpx.adobe.com/cn/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，了解有关排查 Adobe Analytics 集成问题的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](/help/sites-deploying/configuring-osgi.md)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置：
>
>* **Day Commons HTTP 客户端 3.1** 以配置 3.x API；
>  例如，[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP 组件代理配置**以配置 4.x API；
>  例如，[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
