---
title: 搜索功能
seo-title: 搜索功能
description: 添加和配置搜索到社区站点
seo-description: 添加和配置搜索到社区站点
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---


# 搜索功能{#search-feature}

搜索功能可与各种其他功能（如论坛）配合使用，以提供搜索内容的功能。

添加搜索社区成员输入的帖子(称为用户生成的内容(UGC))的功能时，有两个组件：[搜索](#search)和[搜索结果](#search-results)。

包含`Search Results`组件的页面既支持搜索，又支持结果显示。

包含`Search`组件的页面提供了启动搜索的位置，搜索结果显示在`Search Results`页面上。

该搜索功能可以与允许站点访客和成员视图内容的任何其他功能一起使用。

## 搜索 {#search-features}

### 将搜索添加到页面{#add-search-to-a-page}

要在创作模式下将`Search`组件添加到页面，请使用组件浏览器找到`Communities / Search`并将其拖动到页面上的位置。 使用`Search`需要为`Search Results.`添加第二页

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含所需的客户端库`cq.social.hbs.search`时，将显示`Search`组件。

![添加搜索](assets/add-search.png)

### 配置添加的搜索{#configure-the-added-search}

选择要访问的已放置`Search`组件，然后选择打开编辑对话框的`Configure`图标。

![配](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜索设置]**&#x200B;选项卡下，指定在访客输入查询时如何搜索路径。

![搜索设置](assets/search-settings.png)

* **[!UICONTROL 搜索]**
路径通过使用添加项目按钮添加搜索路径，内容搜索受到限制。例如，要将搜索限制到特定论坛，请选择放在页面中的论坛组件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 结果]**
页使用浏览器选择包含 
`Search Results` 组件.

## 搜索结果 {#search-results}

### 将搜索结果添加到页面{#add-search-results-to-a-page}

要在创作模式下将`Search Results`组件添加到页面，请使用组件浏览器查找

* `Communities / Search Results`

并将其拖动到页面上的位置。 与搜索组件不同，无需再创建第二页，因为结果将显示在同一页面上。

如果在网站的其他位置使用“搜索”，则此页面的`Search Results`可配置为`Search`的任何或所有实例的`Result Page`。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含所需的客户端库`cq.social.hbs.search`时，`Search Result`组件的显示方式如下：

![搜索结果](assets/search-result1.png)

### 配置添加的搜索结果{#configure-the-added-search-result}

选择要访问的已放置`Search Results`组件，然后选择打开编辑对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜索结果设置]**&#x200B;选项卡下，可以指定当访客输入查询时，搜索中包含哪些路径。

![搜索结果设置](assets/search-result-settings.png)

* **[!UICONTROL 每页的搜索结果数]**

   定义每页显示的主题／帖子数。 默认值为10。

* **[!UICONTROL 搜索路径]**

   通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。

## 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[Search Essentials](search-implementation.md)页面。
