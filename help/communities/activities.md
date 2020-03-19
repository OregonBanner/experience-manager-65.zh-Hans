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
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# 活动流功能 {#activity-streams-feature}

## 简介 {#introduction}

已登录社区成员的活动，例如发布到论坛或博客，被收集到流中，该流可以通过组件的配置以各种方式过滤和显 `Activity Streams` 示。

关注功能可添加社区成员关注感兴趣的帖子或关注其他社区成员的活动时的活动的另一种视图。

文档描述：

* 将“活动流”组件添加到AEM站点
* “活动流”组件的配置设置

### 将活动流添加到页面 {#adding-activity-streams-to-a-page}

如果希望在创作模式 `Activity Streams` 下将组件添加到页面，请使用组件浏览器查找

* `Communities / Activity Streams`

并将其拖动到应显示活动流的页面上。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包含 [所需的客户端库时](/help/communities/essentials-activities.md#essentials-for-client-side) ，组件的显示方式 `Activity Streams` 如下：

![chlimage_1-24](assets/chlimage_1-24.png)

### 配置活动流 {#configuring-activity-streams}

选择要访问 `Activity Streams` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-25](assets/chlimage_1-25.png)

在“用户 **活动** ”选项卡下，指定要显示的活动：

![chlimage_1-26](assets/chlimage_1-26.png)

* **活动最大数量**

   要显示的活动数

* **流资源路径**

   留空将默认为社区站点或社区组。 流资源路径标识活动的源。 默认值为空。

* **显示“用户活动”视图**

   如果选中此项，则活动页面将包含一个选项卡，该选项卡根据当前成员在社区中生成的活动筛选活动。 选中默认值。

* **显示“全部活动”视图**

   如果选中此项，则活动页面将包含一个选项卡，其中包含当前成员有权访问的社区中生成的所有活动。 选中默认值。

* **显示“关注”视图**

   如果选中此项，则活动页面将包含一个选项卡，该选项卡将根据当前成员所跟踪的活动筛选活动。 选中默认值。

### 后视图 {#following-view}

必须配置组件才能启用以下功能。 允许以下功能：博客 [、论坛](/help/communities/blog-feature.md)、QnQnQn [、日历、](/help/communities/forum.md)FilaryBrary [、elibrbr](/help/communities/working-with-qna.md)[](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)和Comments评论。

![chlimage_1-27](assets/chlimage_1-27.png)

“跟 **踪** ”按钮提供了以活动、通知或订阅等形式跟踪 [条目](/help/communities/notifications.md)的 [方法](/help/communities/subscriptions.md)。 每次选择“ **跟随** ”按钮时，都可以打开或关闭选择。 仅 `Email Subscriptions` 在配置后才显示选择。

如果选择了以下任何方法，则按钮的文本将变为“以下 **”**。 为方便起见，可以选择 `Unfollow All` 关闭所有方法。

将显 **示** “关注”按钮

* 查看其他成员的配置文件时
* 在主功能页面上，如论坛、问题与答案和博客

   * 遵循了该常规功能的所有活动

* 对于特定条目，如论坛主题、问题与答案问题或博客文章

   * 跟踪该特定条目的所有活动

### 附加信息 {#additional-information}

有关详细信息，请参阅面向开 [发人员的Activity Streams](/help/communities/essentials-activities.md) Essentials页。
