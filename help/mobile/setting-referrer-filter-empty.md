---
title: 将引用过滤器设置为允许空
seo-title: 将引用过滤器设置为允许空
description: 可查看本页以了解“引用过滤器”。 要允许AEM Mobile应用程序查看器查看您的作者实例上的应用程序，您需要将HTML引用过滤器设置为“允许空”。
seo-description: 可查看本页以了解“引用过滤器”。 要允许AEM Mobile应用程序查看器查看您的作者实例上的应用程序，您需要将HTML引用过滤器设置为“允许空”。
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 将引用过滤器设置为允许空{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

要允许AEM Mobile应用程序查看器查看您的作者实例上的应用程序，您需要将HTML引用过滤器设置为“允许空”。

如果不想使用应用程序查看器来查看开发和暂存状态中的应用程序，则无需更改引用过滤器的默认设置。

在AEM的正在运行的作者实例中，导航到：http://localhost:4502/system/console/configMgr [下载](http://localhost:4502/system/console/configMgr) ，并搜索“Apache Sling Referrer Filter”。 单击以编辑引用过滤器并选中“允许空”复选框（请参阅下图）。 然后，单击保存按钮并关闭浏览器页面。

![引用过滤器设置](assets/chlimage_1-106.png)
