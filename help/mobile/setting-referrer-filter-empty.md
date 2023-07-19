---
title: 将反向链接筛选器设置为允许为空
seo-title: Setting Your Referrer Filter to Allow Empty
description: 关注此页面，了解反向链接过滤器。 为了允许AEM Mobile应用程序查看器查看创作实例上的应用程序，您需要将HTML反向链接筛选器设置为“允许为空”。
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 3%

---

# 将反向链接筛选器设置为允许为空{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

为了允许AEM Mobile应用程序查看器查看创作实例上的应用程序，您需要将HTML反向链接筛选器设置为“允许为空”。

如果您不打算使用Application Viewer查看处于开发和暂存状态的应用程序，则无需更改反向链接筛选器的默认设置。

在正在运行的AEM创作实例中，导航到： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 和搜索“Apache Sling引用过滤器”。 单击以编辑反向链接筛选条件，并选中“允许为空”复选框（请参阅下图）。 接下来，点击“保存”按钮并关闭浏览器页面。

![反向链接筛选设置](assets/chlimage_1-106.png)
