---
title: 与 Adobe Analytics 集成
seo-title: Integrating with Adobe Analytics
description: 瞭解如何將AEM與Adobe Analytics整合。
seo-description: Learn how to integrate AEM with Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 73%

---

# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEM可讓您追蹤網頁活動：

* Adobe Analytics 配置可让 AEM 通过 Adobe Analytics 进行身份验证。
* 框架标识发送到 Adobe Analytics 报告包的数据。

資料包含頁面和使用者資料；例如：

* AEM 组件收集的数据
* 链接点击次数
* 视频使用信息
* 来自 Adobe Analytics 的页面访问次数

下列頁面可協助您設定整合：

* [連線到Adobe Analytics和建立框架](/help/sites-administering/adobeanalytics-connect.md)
* [为 Adobe Analytics 配置链接跟踪](/help/sites-administering/adobeanalytics-link.md)
* [建立组件数据与 Adobe Analytics 属性的映射](/help/sites-administering/adobeanalytics-mapping.md)
* [为 Adobe Analytics 配置视频跟踪](/help/sites-administering/adobeanalytics-video.md)
* [Adobe 分类](/help/sites-administering/adobeanalytics-classifications.md)

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) 以輕鬆執行整合。

>[!NOTE]
>
>另請參閱作法文章： [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## 更多信息 {#further-information}

请参阅：

* [扩展 Adobe Analytics 集成](/help/sites-developing/extending-analytics.md)，了解有关开发用于收集用户数据的组件和自定义 Adobe Analytics 框架的信息。
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

