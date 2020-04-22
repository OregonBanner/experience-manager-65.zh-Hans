---
title: 特色内容功能
seo-title: 特色内容功能
description: 通过“特色内容”功能，登录网站访客可以突出显示内容
seo-description: 通过“特色内容”功能，登录网站访客可以突出显示内容
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# 特色内容功能 {#featured-content-feature}

## 简介 {#introduction}

特色内容功能为发布环境中的登录站点访客（社区成员）提供了一个区域，用于突出显示

* [博客](blog-feature.md)
* [日历](calendar.md)
* [论坛](forum.md)
* [构思](ideation-feature.md)
* [问题与解答](working-with-qna.md)

将内容标记为特色后，它将列在此组件中，该组件可能放在容易引起社区成员注意的特定登陆页或区域中。

可能允许或禁止每个组件使用功能内容。

本文档的这一部分描述了：

* 将特色内容添加到社区站点
* 组件的配置设 `Featured Content` 置

## 将特色内容添加到页面 {#adding-featured-content-to-a-page}

要在创作模 `Featured Content` 式下将组件添加到页面，请使用组件浏览器查找

* `Communities / Featured Content`

并将其拖动到应显示特色内容的页面上的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含 [所需的客户端库时](essentials-featured.md#essentials-for-client-side) ，组件的显示方式 `Featured Content` 如下：

![chlimage_1-13](assets/chlimage_1-13.png)

## 配置特色内容 {#configuring-featured-content}

选择要访问 `Featured Content` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-14](assets/chlimage_1-14.png) ![chlimage_1-15](assets/chlimage_1-15.png)

### 设置选项卡 {#settings-tab}

在“设 **[!UICONTROL 置]** ”选项卡下，标识要实现的内容：

* **[!UICONTROL 显示名]**&#x200B;称列表特色内容的标题。 For example `Featured Questions` or `Featured Ideas`. 如果留空， `Featured Content` 则默认为。

* **[!UICONTROL 专题内容的位置]**
   *（必需）* 浏览到包含可能具有功能的内容的页面（该页面的组件必须配置为“允许特色内容”）。 例如，`/content/sites/engage/en/forum`

* **[!UICONTROL 显示限]**&#x200B;制要显示的特色内容的最大数量。 默认为5。

## 站点访客体验 {#site-visitor-experience}

将内容标记为特色内容的能力需要审查方权限。

审查方视图发布内容时，他们可以访问上下文内审核标志，该标志包括新标 `Feature` 志。

![chlimage_1-16](assets/chlimage_1-16.png)

标记为功能后，建模标记将变 `Unfeature`为。

现在，包含该 `Featured Content` 组件的页面将包含此帖子。

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` 是指向实际帖子的链接。

## 附加信息 {#additional-information}

有关更多信息，请参阅面向开发 [人员的“特色内](essentials-featured.md) 容”页面。

有关将内容标记为特色的信息，请参 [阅审核用户生成的内容](moderate-ugc.md)。
