---
title: 搜索功能
description: 向Communities站点添加和配置搜索
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 搜索功能 {#search-feature}

搜索功能可与各种其他功能（如论坛）配合使用，以提供搜索内容的功能。

添加搜索由社区成员输入的帖子(称为用户生成内容(UGC))的功能时，有两个组件： [Search](#search) 和 [搜索结果](#search-results).

包含 `Search Results` 组件支持搜索和显示结果。

包含 `Search` 组件提供了一个位置，可用于启动搜索，搜索结果会显示在 `Search Results` 页面。

搜索功能可与允许网站访客和成员查看内容的任何其他功能一起使用。

## 搜索 {#search-features}

### 将搜索添加到页面 {#add-search-to-a-page}

添加 `Search` 组件到创作模式下的页面，请使用组件浏览器查找 `Communities / Search` 并将其拖动到页面上的适当位置。 使用 `Search` 需要第二页用于 `Search Results.`

有关必要信息，请访问 [社区组件基础知识](basics.md).

当所需的客户端库时， `cq.social.hbs.search`，包括，这是如何 `Search` 组件随即出现。

![add-search](assets/add-search.png)

### 配置添加的搜索 {#configure-the-added-search}

选择已放置的 `Search` 组件以访问和选择 `Configure` 图标打开“编辑”对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 搜索设置]** 选项卡，指定访客输入查询时搜索路径的方式。

![搜索设置](assets/search-settings.png)

* **[!UICONTROL 搜索路径]**
通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。 例如，要将搜索限制到特定论坛，请选择放置在页面中的论坛组件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 结果页]**
结果将显示在使用浏览器选择包含 `Search Results` 组件。

## 搜索结果 {#search-results}

### 将搜索结果添加到页面 {#add-search-results-to-a-page}

添加 `Search Results` 组件到创作模式下的页面，请使用组件浏览器查找

* `Communities / Search Results`

并将其拖动到页面上的适当位置。 与搜索组件不同，不需要第二页，因为结果将显示在同一页上。

如果使用网站中的其他位置搜索，则此页面具有 `Search Results` 可以配置为 `Result Page` 对于的任何或所有实例 `Search`.

有关必要信息，请访问 [社区组件基础知识](basics.md).

当所需的客户端库时， `cq.social.hbs.search`，包括，这是如何 `Search Result` 组件将显示：

![search-result](assets/search-result1.png)

### 配置添加的搜索结果 {#configure-the-added-search-result}

选择已放置的 `Search Results` 组件以访问和选择 `Configure` 图标打开“编辑”对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 搜索结果设置]** 选项卡中，可以指定在访客输入查询时搜索中包含哪些路径。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每页的搜索结果数]**

  定义每个页面显示的主题/帖子数。 默认值为10。

* **[!UICONTROL 搜索路径]**

  通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [Search Essentials](search-implementation.md) 适用于开发人员的页面。
