---
title: Communities 订阅
seo-title: Communities 订阅
description: 社区成员通过电子邮件与其他成员互动
seo-description: 社区成员通过电子邮件与其他成员互动
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# Communities 订阅 {#communities-subscriptions}

## 概述 {#overview}

从社区[FP1](deploy-communities.md#latestfeaturepack)开始，社区成员可以使用称为订阅的功能通过电子邮件与社区互动。

订阅与[notifications](notifications.md)类似，因为在关注博客文章、论坛主题或问题与答案问题时，会员可以订阅。

订阅与通知的区别在于：

* 会员在关注其他会员时，不得订阅。
* 对于成员，只需在以下情况下选择`Email Subscriptions`。
* 配置电子邮件回复后，会员只需回复收到的电子邮件即可有效地发布内容。

### 要求{#requirements}

**配置电子邮件**

必须配置电子邮件，以使订阅能够正常工作，并使成员通过电子邮件回复。

有关设置电子邮件的说明，请参阅[配置电子邮件](email.md)。

**启用订阅并关注**

必须配置组件以启用以下订阅&#x200B;*和*。 允许订阅的功能有[blog](blog-feature.md)、[论坛](forum.md)和[QnA](working-with-qna.md)。

## 订阅自以下{#subscriptions-from-following}

![订阅跟踪](assets/subscription-following.png)

**“跟踪”按钮提供了一种方法，可以跟踪作为活动、订阅和/或通知的条目。**&#x200B;每次选择&#x200B;**“跟随”**&#x200B;按钮时，都可以打开或关闭选择。

如果选择了以下任何方法，则按钮的文本将更改为&#x200B;**Following**。 为方便起见，可以选择`Unfollow All`以关闭所有方法。

**只有在将论坛、QnA或博客配置为启用电子邮件订阅时，Follow**&#x200B;按钮才会包含`Email Subscriptions`选项。 此按钮将显示：

* 在启用的论坛的主功能页面上，问题与答案或博客将针对该功能下的所有活动发送电子邮件。

* 对于特定条目（如论坛主题、问题与答案问题或博客文章），将在活动特定条目时发送电子邮件。

## 通过电子邮件{#reply-by-email}回复

当电子邮件[配置为通过电子邮件](email.md#configure-polling-importer)回复时，订阅会员将收到一封包含已发布内容和指向联机内容的链接的电子邮件。

如果他们回复了电子邮件，则他们在回复中输入的内容将显示为在线内容。

![电子邮件回复](assets/email-reply.png)

回复的发布时间由[轮询导入程序的更新间隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)

