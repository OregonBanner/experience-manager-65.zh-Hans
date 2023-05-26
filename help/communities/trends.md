---
title: 活动趋势
seo-title: Activity Trends
description: 将社区活动列表组件添加到页面
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# 活动趋势 {#activity-trends}

## 简介 {#introduction}

此 `Community Activity List` 组件提供添加有关成员的帖子与视图以及帖子与内容视图的趋势信息的功能。

本文档描述了：

* 添加 `Community Activity List` 组件到 [社区站点](/help/communities/overview.md#community-sites).

* 的配置设置 `Community Activity List` 组件。

### 要求 {#requirement}

的数据 `Community Activity List` 仅当Adobe Analytics获得许可并为社区站点配置时，才可用。

参见 [适用于社区功能的Analytics配置](/help/communities/analytics.md).

### 将社区活动列表添加到页面 {#adding-a-community-activity-list-to-a-page}

添加 `Community Activity List` 组件到创作模式下的页面，找到该组件

* `Communities / Community Activity List`

并将其拖动到页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

首次放置到社区站点的页面上时，以下是组件的显示方式：

![社区活动](assets/community-activity.png)

### 配置社区活动列表  {#configuring-community-activity-list}

选择已放置的 `Community Activity List` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![配置](assets/configure-new.png)

在 **评论** 选项卡，指定是否以及如何显示已上载文件的注释：

![属性](assets/activity-list-properties.png)

* **类型**

   指定是否显示有关社区成员或用户生成内容(UGC)的数据。

   选择自：

   * `Members`
   * `Content`

   默认为 `Members`.

* **显示标题**

   在数据上方显示的描述性标题，例如 `Trending Content`.
默认无标题。

* **显示数量**

   要列出的项目数。
默认值为10。

* **活动类型**

   选择以下选项之一：

   * `Views`（页面访问量）
   * `Posts`（创建UGC）
   * `Follows`
   * `Likes`

   默认值为“视图”。

* **时间段**

   选择以下选项之一：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   默认为 `Total`.

* **上下文路径**

   提供将活动范围限定为网站子集（如特定博客）的功能。
默认设置是整个社区站点。

* **成员数量整合**

   取消选择（关闭）时，仅计数顶级帖子。 例如，如果上下文是根页面（默认），则 `Activity Type` 之 `Posts` 绝不会显示任何活动，因为无法将内容发布到根页面。 选中后，将包含所有下级页面上的计数。
默认值为已选中。

### 带4个组件的示例页面 {#example-page-with-components}

**热门访客** config：类型=成员，活动类型=视图

**顶级参与者** 配置：类型=成员，活动类型=帖子

**热门内容** 配置：类型=内容，活动类型=视图，

**趋势内容** 配置：类型=内容，活动类型=帖子

![组件](assets/activity-list-components.png)
