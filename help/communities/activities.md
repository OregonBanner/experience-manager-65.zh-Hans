---
title: 活动流功能
seo-title: 活动流功能
description: 已登录社区成员的活动
seo-description: 已登录社区成员的活动
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# 活动流功能{#activity-streams-feature}

## 简介 {#introduction}

已登录社区成员的活动（如向论坛或博客发布）被收集到流中，该流可通过配置`Activity Streams`组件以各种方式过滤和显示。

跟踪功能为社区成员关注感兴趣的帖子或关注其他社区成员的活动添加了另一种活动视图。

文档描述：

* 将活动流组件添加到AEM站点
* 活动流组件的配置设置

### 向页面{#adding-activity-streams-to-a-page}添加活动流

如果需要在创作模式下向页面添加`Activity Streams`组件，请使用组件浏览器找到

* `Communities / Activity Streams`

并将其拖动到应显示活动流的页面上的位置。

有关必要信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/essentials-activities.md#essentials-for-client-side)时，将显示`Activity Streams`组件：

![活动流](assets/activity-component.png)

### 配置活动流{#configuring-activity-streams}

选择要访问的已放置的`Activity Streams`组件，然后选择`Configure`图标以打开编辑对话框。

![配置](assets/configure-new.png)

在&#x200B;**用户活动**&#x200B;选项卡下，指定要显示的活动：

![用户活动](assets/user-activities.png)

* **活动最大数量**

   要显示的活动数

* **流资源路径**

   将留空，默认为社区站点或社区组。 流资源路径可标识活动源。 默认值为空。

* **显示“用户活动”视图**

   如果选中此项，则活动页面将包含一个选项卡，该选项卡会根据当前成员在社区中生成的活动筛选活动。 默认选中。

* **显示“全部活动”视图**

   如果选中此项，则活动页面将包含一个选项卡，其中包含在当前成员有权访问的社区中生成的所有活动。 默认选中。

* **显示“关注”视图**

   如果选中此项，则活动页面将包含一个选项卡，该选项卡会根据当前成员关注的活动筛选活动。 默认选中。

### 查看{#following-view}之后

必须配置组件才能启用以下功能。 允许以下功能： [blog](/help/communities/blog-feature.md)、[论坛](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日历](/help/communities/calendar.md)、[filelibrary](/help/communities/file-library.md)和[评论](/help/communities/comments.md)。

![后视图](assets/following-activities.png)

**Follow**&#x200B;按钮提供了一种方法，可以跟踪作为活动、[通知](/help/communities/notifications.md)或[订阅](/help/communities/subscriptions.md)的条目。 每次选择&#x200B;**Follow**&#x200B;按钮时，都可以打开或关闭选定内容。 `Email Subscriptions`选项仅在配置后才存在。

如果选择了以下任何方法，则按钮的文本将变为&#x200B;**Following**。 为方便起见，可以选择`Unfollow All`以关闭所有方法。

将显示&#x200B;**Follow**&#x200B;按钮：

* 查看其他成员的用户档案时。
* 在主功能页面上，如论坛、QnA和博客。

   * 遵循该常规功能的所有活动。

* 对于特定条目，例如论坛主题、问题解答问题或博客文章。

   * 跟踪该特定条目的所有活动。

### 附加信息 {#additional-information}

有关更多信息，请参阅面向开发人员的[Activity Streams Essentials](/help/communities/essentials-activities.md)页面。
