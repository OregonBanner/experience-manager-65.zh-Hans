---
title: 活动趋势
description: 将社区活动列表组件添加到页面
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---

# 活动趋势 {#activity-trends}

## 简介 {#introduction}

此 `Community Activity List` 组件允许您添加有关成员的帖子与视图以及内容的帖子与视图的趋势信息。

本文档描述了：

* 添加 `Community Activity List` 组件到 [社区站点](/help/communities/overview.md#community-sites).

* 的配置设置 `Community Activity List` 组件。

### 要求 {#requirement}

以下项的数据 `Community Activity List` 仅在为社区站点许可和配置Adobe Analytics时可用。

请参阅 [用于社区功能的Analytics配置](/help/communities/analytics.md).

### 将社区活动列表添加到页面 {#adding-a-community-activity-list-to-a-page}

添加 `Community Activity List` 组件到创作模式下的页面，找到该组件 `Communities / Community Activity List` 并将其拖动到页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

首次放到社区站点的页面时，该组件的显示方式如下：

![社区活动](assets/community-activity.png)

### 配置社区活动列表  {#configuring-community-activity-list}

选择已放置的 `Community Activity List` 组件，然后选择 `Configure` 图标，以打开编辑对话框。

![配置](assets/configure-new.png)

在 **评论** 选项卡，指定是否以及如何显示已上载文件的注释：

![属性](assets/activity-list-properties.png)

* **类型**

  指定显示有关社区成员还是用户生成内容(UGC)的数据。

  选择自：

   * `Members`
   * `Content`

  默认为 `Members`.

* **显示标题**

  在数据上方显示的描述性标题，如 `Trending Content`.
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

  缺省值为“视图”。

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

  这样，您可以将活动范围设定为网站的子集，如特定的博客。
默认设置是整个社区站点。

* **成员数量整合**

  取消选择（关闭）时，仅计数顶级帖子。 例如，如果上下文是根页面（默认），则 `Activity Type` 之 `Posts` 从不显示任何活动，因为无法将内容发布到根页面。 选中后，将包含所有下级页面上的计数。
默认值为选中。

### 具有四个组件的示例页面 {#example-page-with-components}

**顶级访客** 配置：类型=成员，活动类型=视图

**顶级参与者** 配置：类型=成员，活动类型=帖子

**热门内容** 配置：类型=内容，活动类型=视图，

**趋势内容** 配置：类型=内容，活动类型=帖子

![组件](assets/activity-list-components.png)
