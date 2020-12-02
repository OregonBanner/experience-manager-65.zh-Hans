---
title: 社区订阅
seo-title: 社区订阅
description: 社区成员通过电子邮件与其他成员互动
seo-description: 社区成员通过电子邮件与其他成员互动
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 社区订阅{#communities-subscriptions}

## 概述 {#overview}

从社区[FP1](deploy-communities.md#latestfeaturepack)开始，社区成员可以使用称为订阅的功能通过电子邮件与社区交互。

订阅与[notifications](notifications.md)类似，因为在关注博客文章、论坛主题或问题与答案时，成员可以订阅。

订阅与通知的区别在于：

* 成员在关注其他成员时不能订阅。
* 成员只能执行以下操作：选择`Email Subscriptions`。
* 配置电子邮件回复后，会员只需回复收到的电子邮件，即可有效地发布内容。

### 要求{#requirements}

**配置电子邮件**

必须配置电子邮件，以使订阅能够正常工作，并使成员能通过电子邮件回复。

有关设置电子邮件的说明，请参阅[配置电子邮件](email.md)。

**启用订阅并关注**

必须配置组件以启用订阅&#x200B;*和*。 允许订阅的功能有[blog](blog-feature.md)、[论坛](forum.md)和[QnA](working-with-qna.md)。

## 订阅自{#subscriptions-from-following}

![订阅跟踪](assets/subscription-following.png)

**Follow**&#x200B;按钮提供了一种方法，可以按活动、订阅和／或通知跟踪条目。 每次选择&#x200B;**“跟随”按钮时，都可以打开或关闭选择。**

如果选择了以下任何方法，则按钮的文本将变为&#x200B;**Following**。 为方便起见，可以选择`Unfollow All`以关闭所有方法。

仅当将论坛、 QnA或博客配置为启用电子邮件订阅时，**Follow**&#x200B;按钮将包含`Email Subscriptions`选项。 此按钮将显示：

* 在启用的论坛的主功能页面上，问题与答案或博客将根据该功能向所有活动发送电子邮件。

* 对于特定条目（如论坛主题、问题与答案问题或博客文章），当该特定条目具有活动时，将发送电子邮件。

## 通过电子邮件回复{#reply-by-email}

当电子邮件[配置为通过电子邮件](email.md#configure-polling-importer)回复时，订阅该电子邮件的成员将收到一封电子邮件，其中包含已发布的内容和指向在线内容的链接。

如果他们回复了电子邮件，则他们在回复中输入的内容将显示为在线内容。

![电子邮件回复](assets/email-reply.png)

回复的发布时间由[轮询导入程序的更新间隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)

