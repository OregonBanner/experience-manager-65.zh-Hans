---
title: 活动趋势
seo-title: 活动趋势
description: 将社区活动列表组件添加到页面
seo-description: 将社区活动列表组件添加到页面
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 17088abc71bb820693259088c8a9b938a43cd9d3
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# 活动趋势 {#activity-trends}

## 简介 {#introduction}

该 `Community Activity List` 组件能够按成员以及帖子和视图内容添加有关帖子和视图的趋势信息。

文档描述：

* 将组件 `Community Activity List` 添加到社 [区站点](/help/communities/overview.md#community-sites)。

* 组件的配置 `Community Activity List` 设置。

### 要求 {#requirement}

只有在为社 `Community Activity List` 区站点授权和配置AdobeAnalytics时，才提供该站点的数据。

请参 [阅社区功能的Analytics配置](/help/communities/analytics.md)。

### 将社区活动列表添加到页面 {#adding-a-community-activity-list-to-a-page}

要在创作模 `Community Activity List` 式下将组件添加到页面，请找到该组件

* `Communities / Community Activity List`

并将其拖动到页面上的位置。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

首次放置到社区站点的页面时，组件的显示方式如下：

![社区活动](assets/community-activity.png)

### 配置社区活动列表  {#configuring-community-activity-list}

选择要访问的 `Community Activity List` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-55](assets/chlimage_1-55.png)

在“注 **释** ”选项卡下，指定是否显示已上载文件的注释以及如何显示：

![chlimage_1-56](assets/chlimage_1-56.png)

* **类型**

   指定是显示有关社区成员还是用户生成的内容(UGC)的数据。

   选择自：

   * `Members`
   * `Content`

   Default is `Members`.

* **显示标题**

   要在数据上方显示的描述性标题，如 `Trending Content`。
默认为无标题。

* **显示数量**

   要列表的项目数。
默认值为10。

* **活动类型**

   选择以下选项之一：

   * `Views`（页面访问）
   * `Posts`（创建UGC）
   * `Follows`
   * `Likes`

   默认为视图。

* **时间段**

   选择以下选项之一：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   Default is `Total`.

* **上下文路径**

   提供将活动范围限定到站点的子集（如特定博客）的功能。
默认为整个社区站点。

* **成员数量整合**

   取消选择（关闭）时，只计算顶级帖子。 例如，如果上下文是根页面（默认），则 `Activity Type` 其中 `Posts` 的一个活动将不会显示任何内容，因为无法将内容发布到根页面。 选中后，将包括所有子页面上的计数。
选中默认值。

### 包含4个组件的示例页面 {#example-page-with-components}

**顶级访客** 配置： 类型=成员，活动类型=视图

**顶级参与者** 配置： 类型=成员，活动类型=帖子

**主要内容** 配置： 类型=内容，活动类型=视图,

**趋势内容** 配置： 类型=内容，活动类型=帖子

![chlimage_1-57](assets/chlimage_1-57.png)

