---
title: 社区通知
description: AEM Communities具有显示登录社区成员感兴趣的事件的通知
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 社区通知 {#communities-notifications}

## 概述 {#overview}

AEM Communities提供了一个通知部分，用于显示已登录社区成员感兴趣的事件。

通知类似于 [活动](/help/communities/essentials-activities.md) 和 [订阅](/help/communities/subscriptions.md) 原因可能是：

* 成员过帐内容。
* 选择跟随其他成员的成员。
* 选择遵循特定主题、文章和其他内容线程的成员。
* 用户生成内容中的成员标记(@mention)另一个社区成员。

通知与活动和订阅的不同之处在于：

* 指向通知部分的链接始终显示在社区站点的标题中：

   * 活动需要 [活动流函数](/help/communities/functions.md#activity-stream-function) 社区站点结构中包含的所有区段。
   * 订阅需要 [电子邮件的配置](/help/communities/email.md).

* 通知的实施是通过可扩展且可插拔的渠道实现的：

   * 活动只能在Web上进行。
   * 只能使用电子邮件进行订阅。

截止社区 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知渠道包括：

* Web渠道，访问时使用 `Notifications` 链接。
* 电子邮件渠道，在正确配置电子邮件时可用。

未来的渠道包括移动和桌面。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件才能使通知的电子邮件渠道正常工作。

有关设置电子邮件的说明，请参阅 [配置电子邮件](/help/communities/analytics.md).

**启用关注**

必须配置组件才能启用以下功能。 允许跟踪的功能包括 [博客](/help/communities/blog-feature.md)， [论坛](/help/communities/forum.md)， [问题与解答](/help/communities/working-with-qna.md)， [日历](/help/communities/calendar.md)， [文件库](/help/communities/file-library.md)、和 [评论](/help/communities/comments.md).

**注意**：

* 社区中使用的组件 [站点模板](/help/communities/sites.md) 和 [组模板](/help/communities/tools-groups.md) 可能已配置为遵循。

* 成员配置文件已配置为允许其他成员关注。

## 来自以下项的通知 {#notifications-from-following}

![通知](assets/notifications.png)

此 **[!UICONTROL 关注]** 按钮提供了一种将条目作为活动、订阅和/或通知进行跟踪的方法。 每次 **[!UICONTROL 关注]** 按钮时，可以打开或关闭选择。 此 `Email Subscriptions` 仅在配置时才存在选择。

如果选择了任何后续方法，则按钮的文本将更改为 **[!UICONTROL 关注]**. 为方便起见，可以选择 `Unfollow All` 以关闭所有方法。

此 **[!UICONTROL 关注]** 按钮将显示：

* 查看其他成员的配置文件时。
* 在主要功能页面（如论坛、问题与解答和博客）上：

   * 遵循该常规功能的所有活动。

* 对于特定条目，例如论坛主题、问题或博客文章：

   * 关注该特定条目的所有活动。

## 管理通知设置 {#managing-notification-settings}

通过从“通知”页面中选择“通知设置”链接，每个成员都可以管理接收通知的方式。

Web渠道始终处于启用状态。

![通知14](assets/notifications1.png)

电子邮件渠道，它依赖于适当的 [电子邮件的配置](/help/communities/email.md)，提供与Web渠道相同的设置。

默认情况下，电子邮件渠道处于关闭状态。

![通知2](assets/notifications2.png)

它可以由成员启用，但仍取决于配置的电子邮件。

![通知3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### Web通知 {#web-notifications}

A [向导已创建社区站点](/help/communities/sites-console.md) 现在包含指向 `Notifications` 在网站标题栏的横幅上方显示的功能。 与消息不同，通知是为每个社区站点创建的，而消息必须在站点创建过程中启用。

访问已发布的站点时，选择 `Notifications` 链接将显示成员的所有通知。

![通知4](assets/notifications4.png)

### 电子邮件通知 {#email-notifications}

启用电子邮件渠道后，成员会收到一封电子邮件，其中包含指向Web上内容的链接。

![通知5](assets/notifications5.png)

## 自定义电子邮件通知 {#customize-email-notifications}

组织可以通过自定义电子邮件通知 [覆盖](/help/communities/client-customize.md#overlays) 模板位于 **/libs/settings/community/templates/email/html**.

例如，要修改提及电子邮件通知（对于社区组件），请添加 **如果** 动词的条件 **提及** 在您为其启用的组件的模板中 **@mentions** 支持。

要修改博客评论中发@mention的电子邮件通知模板，请将现成模板放置在： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
