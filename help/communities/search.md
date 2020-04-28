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
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 搜索功能 {#search-feature}

搜索功能可与各种其他功能（如论坛）配合使用，以提供搜索内容的功能。

添加搜索社区成员输入的帖子(称为用户生成的内容(UGC))的功能时，有两个组件：搜索 [和](#search) 搜索结果 [](#search-results)。

包含该组件的页 `Search Results` 面支持搜索和结果显示。

包含组件的页面 `Search` 提供了启动搜索的位置，搜索结果显示在页 `Search Results` 面上。

该搜索功能可以与允许站点访客和成员视图内容的任何其他功能一起使用。

## 搜索 {#search-features}

### 将搜索添加到页面 {#add-search-to-a-page}

要在创作模 `Search` 式下将组件添加到页面，请使用组件浏览器在页面上 `Communities / Search` 找到并将其拖动到相应位置。 使用 `Search` 需要第二页 `Search Results.`

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含所需的客户端库 `cq.social.hbs.search`时，组件的显示方式 `Search` 为此。

![chlimage_1-373](assets/chlimage_1-373.png)

### 配置添加的搜索 {#configure-the-added-search}

选择要访问 `Search` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-374](assets/chlimage_1-374.png)

在“搜 **[!UICONTROL 索设置]** ”选项卡下，指定访客输入查询时搜索路径的方式。

![chlimage_1-375](assets/chlimage_1-375.png)

* **[!UICONTROL 搜索路径]**&#x200B;通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。 例如，要将搜索限制到特定论坛，请选择放置在页面内的论坛组件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 结果页]**&#x200B;结果将显示在使用浏览器选择包含组件的页面指定的单独页 `Search Results` 面上。

## 搜索结果 {#search-results}

### 将搜索结果添加到页面 {#add-search-results-to-a-page}

要在创作模 `Search Results` 式下将组件添加到页面，请使用组件浏览器查找

* `Communities / Search Results`

并将其拖动到页面上的位置。 与搜索组件不同，无需再创建第二页，因为结果将显示在同一页面上。

如果在网站的其他位置使用“搜索”，则此页 `Search Results` 面的配置可能是任何或 `Result Page` 所有实例的页面 `Search`。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含所需的客户端库 `cq.social.hbs.search`时，组件的显示方式 `Search Result` 如下：

![chlimage_1-376](assets/chlimage_1-376.png)

### 配置添加的搜索结果 {#configure-the-added-search-result}

选择要访问 `Search Results` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-377](assets/chlimage_1-377.png)

在“搜 **[!UICONTROL 索结果设置]** ”选项卡下，可以指定当访客输入了查询时，搜索中包含的路径。

![chlimage_1-378](assets/chlimage_1-378.png)

* **[!UICONTROL 每页的搜索结果数]**

   定义每页显示的主题／帖子数。 默认值为10。

* **[!UICONTROL 搜索路径]**

   通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。

## 附加信息 {#additional-information}

有关更多信息，请参阅 [Search Essentials页面](search-implementation.md) ，供开发人员使用。
