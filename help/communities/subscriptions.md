---
title: Communities 订阅
seo-title: Communities 订阅
description: 社区成员通过电子邮件与其他成员进行交互
seo-description: 社区成员通过电子邮件与其他成员进行交互
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# Communities 订阅 {#communities-subscriptions}

## 概述 {#overview}

自社区[FP1](deploy-communities.md#latestfeaturepack)起，社区成员可以使用称为订阅的功能通过电子邮件与社区交互。

订阅与[notifications](notifications.md)类似，因为用户在关注博客文章、论坛主题或QnA问题时可能会订阅。

订阅与通知的区别在于：

* 成员在关注其他成员时不得订阅。
* 成员只需执行下列操作即可选择`Email Subscriptions`。
* 配置了电子邮件回复后，成员只需回复收到的电子邮件即可有效地发布内容。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件，以便订阅正常运行，并让成员通过电子邮件回复。

有关设置电子邮件的说明，请参阅[配置电子邮件](email.md)。

**启用订阅和关注**

必须将组件配置为在下面启用订阅&#x200B;*和*。 允许订阅的功能包括[blog](blog-feature.md)、[forum](forum.md)和[QnA](working-with-qna.md)。

## 以下订阅 {#subscriptions-from-following}

![订购](assets/subscription-following.png)

**Follow**&#x200B;按钮提供了作为活动、订阅和/或通知跟踪条目的方法。 每次选择&#x200B;**Follow**&#x200B;按钮时，都可以打开或关闭选定内容。

如果选择了以下任何方法，则按钮的文本将变为&#x200B;**Following**。 为方便起见，可以选择`Unfollow All`以关闭所有方法。

仅当将论坛、QnA或博客配置为启用电子邮件订阅时，**Follow**&#x200B;按钮才包含`Email Subscriptions`选项。 此按钮将显示：

* 在已启用论坛的主功能页面上，问题解答或博客将针对该功能下的所有活动发送电子邮件。

* 对于特定条目（如论坛主题、问题解答问题或博客文章），当该特定条目存在活动时，将发送电子邮件。

## 通过电子邮件回复 {#reply-by-email}

当电子邮件配置为[通过电子邮件](email.md#configure-polling-importer)回复时，订阅的成员将收到一封包含已发布内容的电子邮件和指向在线内容的链接。

如果他们回复了电子邮件，他们在回复中输入的内容将显示为在线内容。

![email-reply](assets/email-reply.png)

轮询导入程序的更新间隔[控制发布回复所花费的时间。](email.md#configure-polling-importer)

![QA](assets/qa.png)
