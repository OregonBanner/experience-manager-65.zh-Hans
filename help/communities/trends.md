---
title: 活动趋势
seo-title: Activity Trends
description: 向页面添加社区活动列表组件
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

的 `Community Activity List` 组件提供添加与成员发布的帖子和查看次数以及帖子和内容查看次数有关的趋势信息的功能。

文档描述：

* 添加 `Community Activity List` 组件 [社区网站](/help/communities/overview.md#community-sites).

* 的配置设置 `Community Activity List` 组件。

### 要求 {#requirement}

的数据 `Community Activity List` 仅当Adobe Analytics获得社区站点的许可和配置时，才可用。

请参阅 [社区功能的Analytics配置](/help/communities/analytics.md).

### 向页面添加社区活动列表 {#adding-a-community-activity-list-to-a-page}

添加 `Community Activity List` 组件到创作模式下的页面，找到组件

* `Communities / Community Activity List`

并将其拖动到页面上的位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

首次将组件放置在社区站点的页面上时，组件的显示方式如下：

![社区活动](assets/community-activity.png)

### 配置社区活动列表  {#configuring-community-activity-list}

选择已放置的 `Community Activity List` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![配置](assets/configure-new.png)

在 **评论** 选项卡，指定上传文件的注释的显示方式和方式：

![属性](assets/activity-list-properties.png)

* **类型**

   指定是显示社区成员或用户生成内容(UGC)的数据。

   从以下位置选择：

   * `Members`
   * `Content`

   默认为 `Members`.

* **显示标题**

   要在数据上方显示的描述性标题，如 `Trending Content`.
默认为无标题。

* **显示数量**

   要列出的项目数。
默认值为10。

* **活动类型**

   选择以下选项之一：

   * `Views`（页面访问量）
   * `Posts`（创建UGC）
   * `Follows`
   * `Likes`

   默认为“视图”。

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

   提供将活动范围限定在网站子集（如特定博客）的功能。
默认为整个社区站点。

* **成员数量整合**

   取消选择（关闭）后，将只计为顶级帖子。 例如，如果上下文是根页面（默认），则 `Activity Type` of `Posts` 将不会显示任何活动，因为无法将内容发布到根页面。 选中此选项后，将包含所有子页面上的计数。
默认选中。

### 包含4个组件的示例页面 {#example-page-with-components}

**热门访客** 配置：类型=成员，活动类型=视图

**热门参与者** 配置：类型=成员，活动类型=帖子

**热门内容** 配置：类型=内容，活动类型=视图，

**趋势内容** 配置：类型=内容，活动类型=帖子

![组件](assets/activity-list-components.png)
