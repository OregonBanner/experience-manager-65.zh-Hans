---
title: 社区通知
seo-title: 社区通知
description: AEM Communities有通知，显示已登录社区成员感兴趣的事件
seo-description: AEM Communities有通知，显示已登录社区成员感兴趣的事件
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# 社区通知{#communities-notifications}

## 概述 {#overview}

AEM Communities提供通知部分，其中显示已登录社区成员感兴趣的事件。

通知与[活动](/help/communities/essentials-activities.md)和[订阅](/help/communities/subscriptions.md)类似，因为它们可能来自：

* 成员发布内容。
* 选择跟随另一个成员的成员。
* 成员选择遵循特定主题、文章和其他内容线程。
* 用户生成的内容中的成员标记（@提及）另一个社区成员。

通知与活动和订阅的区别在于：

* 通知部分的链接始终显示在社区站点的标题中：

   * 活动需要[活动流函数](/help/communities/functions.md#activity-stream-function)包含在社区站点的结构中。
   * 订阅需要[配置email](/help/communities/email.md)。

* 通知的实现是通过可扩展的可插拔渠道:

   * 活动仅在Web上可用。
   * 订阅仅可通过电子邮件使用。

从社区[FP1](/help/communities/deploy-communities.md#latestfeaturepack)开始，可用的通知渠道包括：

* 使用`Notifications`链接访问的Web渠道。
* 电子邮件渠道，在正确配置电子邮件时可用。

未来的渠道是移动和桌面。

### 要求{#requirements}

**配置电子邮件**

必须配置电子邮件，以便电子邮件渠道通知正常工作。

有关设置电子邮件的说明，请参阅[配置电子邮件](/help/communities/analytics.md)。

**启用跟踪**

必须配置组件以启用以下功能。 允许以下功能：[blog](/help/communities/blog-feature.md)、[论坛](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日历](/help/communities/calendar.md)、[文件库](/help/communities/file-library.md)和[注释](/help/communities/comments.md)。

**注意**:

* 在社区[站点模板](/help/communities/sites.md)和[组模板](/help/communities/tools-groups.md)中使用的组件可能已配置为遵循。

* 成员用户档案已配置为允许其他成员遵循。

## 来自以下的通知{#notifications-from-following}

![通知](assets/notifications.png)

**[!UICONTROL Follow]**&#x200B;按钮提供了一种方法，可以按活动、订阅和／或通知跟踪条目。 每次选择&#x200B;**[!UICONTROL “跟随”按钮时，都可以打开或关闭选择。]**`Email Subscriptions`选择仅在配置后出现。

如果选择了以下任何方法，则按钮的文本将变为&#x200B;**[!UICONTROL Following]**。 为方便起见，可以选择`Unfollow All`以关闭所有方法。

将显示&#x200B;**[!UICONTROL Follow]**&#x200B;按钮：

* 查看其他成员的用户档案时。
* 在主功能页面上，如论坛、问题与解答和博客：

   * 遵循该一般功能的所有活动。

* 对于特定条目，如论坛主题、问题与答案问题或博客文章：

   * 遵循该特定条目的所有活动。

## 管理通知设置{#managing-notification-settings}

通过从“通知”页面选择“通知设置”链接，每个成员都可以管理接收通知的方式。

始终启用Web渠道。

![通知14](assets/notifications1.png)

电子邮件渠道基于电子邮件](/help/communities/email.md)的正确[配置，它提供与Web渠道相同的设置。

电子邮件渠道默认为关闭状态。

![通知2](assets/notifications2.png)

成员可以打开它，但仍取决于配置电子邮件。

![通知3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### Web通知{#web-notifications}

[创建的社区站点](/help/communities/sites-console.md)现在包含指向横幅上方站点标题栏中`Notifications`功能的链接。 与消息不同，每个社区站点都会创建通知，而站点创建过程中必须启用消息。

访问已发布的站点时，选择`Notifications`链接将显示该成员的所有通知。

![通知4](assets/notifications4.png)

### 电子邮件通知{#email-notifications}

启用电子邮件渠道后，成员会收到一封电子邮件，其中包含指向Web上内容的链接。

![通知5](assets/notifications5.png)

## 自定义电子邮件通知{#customize-email-notifications}

组织可以通过[覆盖](/help/communities/client-customize.md#overlays)**/libs/settings/community/templates/email/html**&#x200B;中的模板来自定义电子邮件通知。

例如，要修改提及电子邮件通知（针对社区组件），请在启用了&#x200B;**@mentions**&#x200B;支持的组件的模板中为动词&#x200B;**提及**&#x200B;添加&#x200B;**if**&#x200B;条件。

要在博客评论中修改@tunite的电子邮件通知模板，请将开箱即用模板置于：**/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

