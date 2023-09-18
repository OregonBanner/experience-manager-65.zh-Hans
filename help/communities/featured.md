---
title: 特色内容功能
description: 特色内容功能允许登录的网站访客突出显示内容
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# 特色内容功能 {#featured-content-feature}

## 简介 {#introduction}

特色内容功能为发布环境中的登录站点访客（社区成员）提供了一个区域，用于突出显示以下内容：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [论坛](forum.md)
* [构思](ideation-feature.md)
* [问题与解答](working-with-qna.md)

将内容标记为特色内容后，即会在此组件中列出，这些内容可以放置在易于引起社区成员关注的特定登陆页面或区域中。

每个组件可能允许或不允许使用特征内容功能。

此文档的此部分描述了：

* 将精选内容添加到社区站点。
* 的配置设置 `Featured Content` 组件。

## 将精选内容添加到页面 {#adding-featured-content-to-a-page}

添加 `Featured Content` 组件到创作模式下的页面，请使用组件浏览器查找

* `Communities / Featured Content`

并将其拖动到应显示精选内容的页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-featured.md#essentials-for-client-side) 包括，这就是 `Featured Content` 组件出现：

![功能内容](assets/featuredcontent.png)

## 配置精选内容 {#configuring-featured-content}

选择已放置的 `Featured Content` 组件，以便您能够访问和选择 `Configure` 图标打开“编辑”对话框。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### “设置”选项卡 {#settings-tab}

在 **[!UICONTROL 设置]** 选项卡，标识要使用的内容：

* **[!UICONTROL 显示名称]**

  特色内容列表的标题。 例如， `Featured Questions` 或 `Featured Ideas`. 默认为 `Featured Content` 如果留空。

* **[!UICONTROL 专题内容的位置]**

  *（必需）* 浏览到包含可以精选内容的页面（该页面的组件必须配置为允许精选内容）。 例如：`/content/sites/engage/en/forum`。

* **[!UICONTROL 显示限制]**

  可显示的最大特色内容数量。 默认值为5。

## 网站访客体验 {#site-visitor-experience}

要将内容标记为精选内容，需要拥有审查方权限。

审查方查看已发布的内容时，可以访问上下文审查标志，包括新的 `Feature` 标志。

![site-visitor-experience](assets/site-visitor-experience.png)

标记为功能后，审核标记将变为 `Unfeature`.

包含 `Featured Content` 组件，现包含此帖子。

![site-visitor-experience1](assets/site-visitor-experience1.png)

此 `Read More` 实际帖子的链接。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [专题内容](essentials-featured.md) 适用于开发人员的页面。

要将内容标记为专题，请参阅 [审核用户生成的内容](moderate-ugc.md).
