---
title: 将反向链接筛选条件设置为允许为空
description: 了解反向链接筛选条件。 要允许Adobe Experience Manager (AEM)移动应用程序查看器查看创作实例上的应用程序，您必须将HTML反向链接筛选条件设置为“允许为空”。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 3%

---

# 将反向链接筛选条件设置为允许为空{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

要允许Adobe Experience Manager (AEM)移动应用程序查看器查看创作实例上的应用程序，您必须将HTML反向链接筛选条件设置为“允许为空”。

如果您不打算使用Application Viewer来查看处于开发和暂存状态的应用程序，则无需更改反向链接筛选器的默认设置。

在正在运行的AEM创作实例中，导航到： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 和搜索“Apache Sling引用过滤器”。 单击以编辑反向链接筛选条件，并选中“允许为空”复选框（请参阅下图）。 接下来，点击“保存”按钮并关闭浏览器页面。

![反向链接筛选设置](assets/chlimage_1-106.png)
