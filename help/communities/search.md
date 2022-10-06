---
title: 搜索功能
seo-title: Search Feature
description: 向社区站点添加和配置搜索
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# 搜索功能 {#search-feature}

搜索功能可与各种其他功能（如论坛）配合使用，以便能够搜索内容。

添加搜索社区成员输入的帖子(称为用户生成内容(UGC))的功能时，有两个组件： [搜索](#search) 和 [搜索结果](#search-results).

包含 `Search Results` 组件支持搜索和显示结果。

包含 `Search` 组件提供了启动搜索的位置，搜索结果会显示在 `Search Results` 页面。

搜索功能可与任何其他功能一起使用，该功能允许网站访客和成员查看内容。

## 搜索 {#search-features}

### 将搜索添加到页面 {#add-search-to-a-page}

添加 `Search` 组件添加到创作模式下的页面，可使用组件浏览器找到 `Communities / Search` 并将其拖动到页面上的位置。 使用 `Search` 需要第二个页面 `Search Results.`

有关必要信息，请访问 [社区组件基础知识](basics.md).

当需要的客户端库时， `cq.social.hbs.search`，这是 `Search` 组件。

![添加搜索](assets/add-search.png)

### 配置添加的搜索 {#configure-the-added-search}

选择已放置的 `Search` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 搜索设置]** 选项卡，指定访客输入查询时搜索路径的方式。

![搜索设置](assets/search-settings.png)

* **[!UICONTROL 搜索路径]**
通过使用“添加项目”按钮添加搜索路径，内容搜索会受到限制。 例如，要将搜索限制为特定论坛，请选择置于页面内的论坛组件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 结果页面]**
结果将显示在使用浏览器选择包含 
`Search Results` 组件.

## 搜索结果 {#search-results}

### 将搜索结果添加到页面 {#add-search-results-to-a-page}

添加 `Search Results` 组件添加到创作模式下的页面，可使用组件浏览器找到

* `Communities / Search Results`

并将其拖动到页面上的位置。 与搜索组件不同，由于结果将显示在同一页面上，因此无需再添加第二页。

如果在网站的其他位置使用搜索，则此页面包含 `Search Results` 可以配置为 `Result Page` 对于任何或所有实例 `Search`.

有关必要信息，请访问 [社区组件基础知识](basics.md).

当需要的客户端库时， `cq.social.hbs.search`，这是 `Search Result` 组件将显示：

![搜索结果](assets/search-result1.png)

### 配置添加的搜索结果 {#configure-the-added-search-result}

选择已放置的 `Search Results` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 搜索结果设置]** 选项卡，可以指定访客输入查询时搜索中包含的路径。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每页的搜索结果数]**

   定义每页显示的主题/帖子数。 默认值为10。

* **[!UICONTROL 搜索路径]**

   通过使用“添加项目”按钮添加搜索路径，内容搜索会受到限制。

## 附加信息 {#additional-information}

有关 [搜索要点](search-implementation.md) 页面。
