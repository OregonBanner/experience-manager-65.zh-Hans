---
title: 特色内容功能
seo-title: 特色内容功能
description: “特色内容”功能允许登录网站访客突出显示内容
seo-description: “特色内容”功能允许登录网站访客突出显示内容
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: cbb5a6bac5e9932fd36abf20d4424890080d39bf
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---


# 特色内容功能 {#featured-content-feature}

## 简介 {#introduction}

特色内容功能为发布环境中的登录站点访客（社区成员）提供了一个区域，用于突出显示以下内容：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [论坛](forum.md)
* [构思](ideation-feature.md)
* [问题与解答](working-with-qna.md)

一旦将内容标记为特色，它将列在此组件中，该组件可能会放在容易引起社区成员注意的特定登陆页或区域中。

每个组件可能允许或禁止功能显示内容。

文档的本节介绍：

* 向社区站点添加特色内容。
* 组件的配置 `Featured Content` 设置。

## 将特色内容添加到页面 {#adding-featured-content-to-a-page}

要在创作模 `Featured Content` 式下将组件添加到页面，请使用组件浏览器来查找

* `Communities / Featured Content`

并将其拖动到应显示特色内容的页面上。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包 [含所需的客户端库](essentials-featured.md#essentials-for-client-side) ，组件的显示 `Featured Content` 方式如下：

![chlimage_1-13](assets/chlimage_1-13.png)

## 配置特色内容 {#configuring-featured-content}

选择要访问的 `Featured Content` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-14](assets/chlimage_1-14.png)

![chlimage_1-15](assets/chlimage_1-15.png)

### “设置”选项卡 {#settings-tab}

在“设 **[!UICONTROL 置]** ”选项卡下，标识要显示的内容：

* **[!UICONTROL 显示名称]**

   特色内容列表的标题。 For example `Featured Questions` or `Featured Ideas`. 如果留 `Featured Content` 空，则默认值为。

* **[!UICONTROL 专题内容的位置]**

   *（必需）浏览* 至包含可能具有功能的内容的页面（该页面的组件必须配置为允许特色内容）。 For example, `/content/sites/engage/en/forum`.

* **[!UICONTROL 显示限制]**

   要显示的特色内容的最大数量。 默认值为5。

## 站点访客体验 {#site-visitor-experience}

将内容标记为特色内容需要审查方权限。

审查方视图发布内容时，他们有权访问上下文中的审核标志，该标志包括新标 `Feature` 志。

![chlimage_1-16](assets/chlimage_1-16.png)

标记为功能后，模型标志将变 `Unfeature`为。

现在，包含该 `Featured Content` 组件的页面将包含此帖子。

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` 是指向实际帖子的链接。

## 附加信息 {#additional-information}

有关更多信息，请参阅面向开 [发人员的](essentials-featured.md) “特色内容”页。

有关将内容标记为特色的信息，请参 [阅调节用户生成的内容](moderate-ugc.md)。
