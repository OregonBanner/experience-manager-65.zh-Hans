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
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# 社区订阅 {#communities-subscriptions}

## 概述 {#overview}

自Communities [FP1起](deploy-communities.md#latestfeaturepack)，社区成员可以使用称为订阅的功能通过电子邮件与社区交互。

订阅与通知类 [似](notifications.md) ，因为会员在关注博客文章、论坛主题或问题与答案问题时可能会订阅通知。

订阅与通知的区别在于：

* 会员在与其他会员联系时不得订阅。
* 对于成员，只有在进行以下操作时才 `Email Subscriptions` 能进行选择。
* 配置电子邮件回复后，会员只需回复收到的电子邮件即可有效地发布内容。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件，以使订阅能够正常工作，并使成员能通过电子邮件回复。

有关设置电子邮件的说明，请参阅配 [置电子邮件](email.md)。

**启用订阅并关注**

必须配置组件才能启用订阅 *和* 后续。 允许订阅的功 [能有博客](blog-feature.md)、 [论坛](forum.md)[和](working-with-qna.md)QnA。

## 订阅自以下 {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

“跟 **踪** ”按钮提供了一种方法，可以按活动、订阅和／或通知跟踪条目。 每次选择“ **跟随** ”按钮时，都可以打开或关闭选择。

如果选择了以下任何方法，则按钮的文本将变为“以下 **”**。 为方便起见，可以选择 `Unfollow All` 关闭所有方法。

“关 **注** ”按钮仅在将论坛、问题 `Email Subscriptions` 与答案或博客配置为启用电子邮件订阅时才包含此选项。 此按钮将显示：

* 在启用的论坛的主功能页面上，问题与答案或博客将针对该功能下的所有活动发送电子邮件。

* 对于特定条目，如论坛主题、问题与答案问题或博客文章。当该特定条目有活动时，将发送电子邮件。

## 通过电子邮件回复 {#reply-by-email}

当电子邮件配 [置为通过电子邮件回复时](email.md#configure-polling-importer)，订阅的会员将收到一封电子邮件，其中包含已发布的内容和指向在线内容的链接。

如果他们回复了电子邮件，则他们在回复中输入的内容将显示为在线内容。

![chlimage_1-6](assets/chlimage_1-6.png)

轮询导入程序的更新间隔控制发布回复所 [需的时间](email.md#configure-polling-importer)。

![chlimage_1-7](assets/chlimage_1-7.png)

