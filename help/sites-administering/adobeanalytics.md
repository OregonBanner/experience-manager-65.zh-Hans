---
title: 与 Adobe Analytics 集成
seo-title: 与 Adobe Analytics 集成
description: 了解如何将AEM与Adobe Analytics集成。
seo-description: 了解如何将AEM与Adobe Analytics集成。
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 21%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics和AEM集成后，您可以跟踪网页活动:

* Adobe Analytics配置使AEM能够与Adobe Analytics进行身份验证。
* 框架标识发送到您的Adobe Analytics报告包的数据。

数据包括页面和用户数据；例如：

* aem组件收集的数据
* 链接点击
* 视频使用信息
* 来自Adobe Analytics的页面访问次数

以下页面可帮助您配置集成：

* [连接Adobe Analytics和创建框架](/help/sites-administering/adobeanalytics-connect.md)
* [为Adobe Analytics配置链接跟踪](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md)
* [为Adobe Analytics配置视频跟踪](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分类](/help/sites-administering/adobeanalytics-classifications.md)

您还可以使用[选择加入向导](/help/sites-administering/opt-in.md)轻松执行集成。

>[!NOTE]
>
>另请参阅操作方法文章：[使用DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)将AEM与Adobe Target和Adobe Analytics集成。

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics](/help/sites-developing/extending-analytics.md) 集成，以了解有关开发收集用户数据的组件和自定义Adobe Analytics框架的信息。
* 知识库文章[Adobe Analytics集成——疑难排解问题](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以了解有关Adobe Analytics集成疑难排解的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](/help/sites-deploying/configuring-osgi.md)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置:
>
>* **Day Commons HTTP Client 3.1** 配置3.x API;
   >  例如[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components Proxy** Configuration配置4.x API;
   >  例如[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



