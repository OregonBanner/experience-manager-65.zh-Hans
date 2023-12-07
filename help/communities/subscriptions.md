---
title: Communities 订阅
description: 社区成员通过电子邮件与其他成员进行交互
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Communities 订阅 {#communities-subscriptions}

## 概述 {#overview}

截止社区 [FP1](deploy-communities.md#latestfeaturepack)，社区成员可以使用称为订阅的功能通过电子邮件与社区交互。

订阅类似于 [通知](notifications.md) 成员可以在关注博客文章、论坛主题或问题与解答时订阅。

订阅与通知的区别在于：

* 当成员跟随其他成员时，不能订阅。
* 成员唯一要采取的操作是选择 `Email Subscriptions` 进行以下操作时。
* 配置电子邮件回复后，成员只需回复收到的电子邮件，即可有效地发布内容。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件以使订阅正常工作并使成员通过电子邮件回复。

有关设置电子邮件的说明，请参阅 [配置电子邮件](email.md).

**启用订阅并关注**

必须配置组件以启用订阅 *和* 关注。 允许订阅的功能包括 [博客](blog-feature.md)， [论坛](forum.md) 和 [问题与解答](working-with-qna.md).

## 来自以下项的订阅 {#subscriptions-from-following}

![subscription-flowing](assets/subscription-following.png)

此 **关注** 按钮提供了一种将条目作为活动、订阅和/或通知进行跟踪的方法。 每次 **关注** 按钮时，可以打开或关闭选择。

如果选择了任何后续方法，则按钮的文本将更改为 **关注**. 为方便起见，可以选择 `Unfollow All` 以关闭所有方法。

此 **关注** 按钮将包括 `Email Subscriptions` 选项，但仅限于将论坛、问题与解答或博客配置为启用电子邮件订阅时。 将显示此按钮：

* 在启用的论坛、问题与解答或博客的主功能页上，将为该功能下的所有活动发送电子邮件。

* 对于特定条目，例如论坛主题、问题或博客文章。当存在针对该特定条目的活动时，将发送电子邮件。

## 通过电子邮件回复 {#reply-by-email}

当电子邮件为 [已配置为通过电子邮件进行回复](email.md#configure-polling-importer)，订阅的成员将收到一封包含已发布内容的电子邮件以及一个指向在线内容的链接。

如果他们回复电子邮件，则他们在回复中输入的内容将显示为在线内容。

![email-reply](assets/email-reply.png)

发布回复所花费的时间由 [轮询导入程序的更新间隔](email.md#configure-polling-importer).

![QA](assets/qa.png)
