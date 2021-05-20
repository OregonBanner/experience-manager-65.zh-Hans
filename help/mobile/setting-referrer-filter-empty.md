---
title: 将反向链接过滤器设置为允许空
seo-title: 将反向链接过滤器设置为允许空
description: 请阅读本页以了解反向链接过滤器。 为了允许AEM Mobile应用程序查看器查看创作实例上的应用程序，您需要将HTML反向链接过滤器设置为“允许为空”。
seo-description: 请阅读本页以了解反向链接过滤器。 为了允许AEM Mobile应用程序查看器查看创作实例上的应用程序，您需要将HTML反向链接过滤器设置为“允许为空”。
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 3%

---

# 将反向链接过滤器设置为允许Empty{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

为了允许AEM Mobile应用程序查看器查看创作实例上的应用程序，您需要将HTML反向链接过滤器设置为“允许为空”。

如果您不打算使用应用程序查看器来查看处于开发和暂存状态的应用程序，则无需更改反向链接过滤器的默认设置。

在运行的AEM创作实例中，导航到：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)并搜索“Apache Sling反向链接过滤器”。 单击以编辑反向链接过滤器，并选中“允许空”复选框（请参阅下图）。 下一步，单击保存按钮并关闭浏览器页面。

![反向链接过滤器设置](assets/chlimage_1-106.png)
