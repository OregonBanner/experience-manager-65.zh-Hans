---
title: 与Adobe Analytics集成
seo-title: 与Adobe Analytics集成
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

---


# 与Adobe Analytics集成{#integrating-with-adobe-analytics}

将Adobe Analytics与AEM集成后，您可以跟踪网页活动：

* Adobe Analytics配置使AEM能够使用Adobe Analytics进行身份验证。
* 框架可标识发送到Adobe Analytics报告包的数据。

数据包括页面数据和用户数据；例如：

* AEM组件收集的数据
* 链接点击
* 视频使用信息
* Adobe Analytics的页面访问次数

以下页面可帮助您配置集成：

* [连接到Adobe Analytics和创建框架](/help/sites-administering/adobeanalytics-connect.md)
* [为Adobe Analytics配置链接跟踪](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md)
* [为Adobe Analytics配置视频跟踪](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分类](/help/sites-administering/adobeanalytics-classifications.md)

您还可以使用 [加入向导](/help/sites-administering/opt-in.md) ，轻松执行集成。

>[!NOTE]
>
>另请参阅操作方法文章：使 [用DTM将AEM与Adobe Target和Adobe Analytics集成](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics集成](/help/sites-developing/extending-analytics.md) ，以了解有关开发收集用户数据的组件和自定义Adobe Analytics框架的信息。
* 有关Adobe Analytics集成疑难 [解答的信息，请参阅知识库文章](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html),Adobe Analytics集成——疑难解答问题。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的Adobe Analytics，则需要配置 [Apache HTTP Client Proxy配置所需的两个OSGi包](/help/sites-deploying/configuring-osgi.md)**** （例如，使用Web控制台）。 这两者都是必需的，因为AEM的某些功能使用3.x API，而其他功能使用4.x API。 配置:
>
>* **Day Commons HTTP Client 3.1** ，配置3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components代理配置** ，用于配置4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



