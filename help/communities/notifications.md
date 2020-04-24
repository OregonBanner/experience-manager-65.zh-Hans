---
title: 社区通知
seo-title: 社区通知
description: AEM Communities具有通知，可显示登录社区成员感兴趣的事件
seo-description: AEM Communities具有通知，可显示登录社区成员感兴趣的事件
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# 社区通知 {#communities-notifications}

## 概述 {#overview}

AEM Communities提供了通知部分，其中显示已登录社区成员感兴趣的事件。

通知与活动和 [订阅类似](/help/communities/essentials-activities.md) , [](/help/communities/subscriptions.md) 它们可能来自：

* 成员发布内容。
* 选择跟随另一个成员的成员。
* 成员选择遵循特定主题、文章和其他内容线索。
* 用户生成内容中的成员标记（@提及）另一个社区成员。

通知与活动和订阅的区别在于：

* 指向通知部分的链接始终显示在社区站点的标题中：

   * 活动需要 [活动流函数](/help/communities/functions.md#activity-stream-function) ，才能包含在社区站点的结构中。
   * 订阅需 [要配置电子邮件](/help/communities/email.md)。

* 通知的实现是通过可扩展的可插拔渠道:

   * 活动仅在Web上提供。
   * 订阅仅可通过电子邮件获取。

自Communities [FP1起](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知渠道包括：

* Web渠道，使用链接访 `Notifications` 问。
* 电子邮件渠道，在正确配置电子邮件时可用。

未来的渠道是移动和桌面。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件，才能使通知正常工作的电子邮件渠道。

有关设置电子邮件的说明，请参阅配 [置电子邮件](/help/communities/analytics.md)。

**启用关注**

必须配置组件才能启用以下功能。 允许以下功能：博客 [、论坛](/help/communities/blog-feature.md)、QnQnQn [、日历、](/help/communities/forum.md)FilaryBrary [、elibrbr](/help/communities/working-with-qna.md)[](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)和Comments评论。

**注意**:

* 在社区站点模 [板和组模板](/help/communities/sites.md)[中使用的组件](/help/communities/tools-groups.md) ，可能已配置为遵循。

* 会员用户档案已配置为允许其他会员遵循。

## 来自以下渠道的通知 {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

“跟 **[!UICONTROL 踪]** ”按钮提供了一种方法，可以按活动、订阅和／或通知跟踪条目。 每次选择“ **[!UICONTROL 跟随]** ”按钮时，都可以打开或关闭选择。 仅 `Email Subscriptions` 在配置后才显示选择。

如果选择了以下任何方法，则按钮的文本将变为“以下 **[!UICONTROL ”]**。 为方便起见，可以选择 `Unfollow All` 关闭所有方法。

将显 **[!UICONTROL 示]** “关注”按钮：

* 查看其他成员的用户档案时。
* 在主功能页面上，如论坛、问题与解答和博客：

   * 遵循该常规功能的所有活动。

* 对于特定条目，如论坛主题、问题与答案问题或博客文章：

   * 遵循该特定条目的所有活动。

## 管理通知设置 {#managing-notification-settings}

通过从“通知”页面中选择“通知设置”链接，每个成员都可以管理接收通知的方式。

始终启用Web渠道。

![chlimage_1-244](assets/chlimage_1-244.png)

电子邮件渠道依赖于电子邮 [件的正确配置](/help/communities/email.md)，它提供的设置与Web渠道相同。

默认情况下，电子邮件渠道处于关闭状态。

![chlimage_1-245](assets/chlimage_1-245.png)

它可能由成员打开，但仍取决于电子邮件的配置。

![chlimage_1-246](assets/chlimage_1-246.png)

## 查看通知 {#viewing-notifications}

### Web通知 {#web-notifications}

向导 [创建的社区站点](/help/communities/sites-console.md) ，现在在横幅上 `Notifications` 方站点标题栏中包含指向该功能的链接。 与消息不同，系统会为每个社区站点创建通知，而在站点创建过程中必须启用消息。

访问已发布的站点时，选择链 `Notifications` 接将显示该成员的所有通知。

![chlimage_1-247](assets/chlimage_1-247.png)

### 电子邮件通知 {#email-notifications}

启用电子邮件渠道后，成员会收到一封电子邮件，其中包含指向Web上内容的链接。

![chlimage_1-248](assets/chlimage_1-248.png)

## 自定义电子邮件通知 {#customize-email-notifications}

组织可以通过覆盖位 [于](/help/communities/client-customize.md#overlays) /libs/settings/community/templates/email/html的模 **板来自定义电子邮件通知**。

例如，要修改提及电子邮件通知（针对社区组件），请在启用了@mentions支持的组件的模板中为动词提及添加 **if** 条件 ******** 。

要修改博客评论中@tuntice的电子邮件通知模板，请将开箱即用模板放在： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/cn**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

