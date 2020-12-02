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


# 特色内容功能{#featured-content-feature}

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
* `Featured Content`组件的配置设置。

## 将特色内容添加到页面{#adding-featured-content-to-a-page}

要在创作模式下将`Featured Content`组件添加到页面，请使用组件浏览器查找

* `Communities / Featured Content`

并将其拖动到应显示特色内容的页面上。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[必需的客户端库](essentials-featured.md#essentials-for-client-side)时，`Featured Content`组件的显示方式如下：

![chlimage_1-13](assets/chlimage_1-13.png)

## 配置特色内容{#configuring-featured-content}

选择要访问的已放置`Featured Content`组件，然后选择打开编辑对话框的`Configure`图标。

![chlimage_1-14](assets/chlimage_1-14.png)

![chlimage_1-15](assets/chlimage_1-15.png)

### 设置选项卡{#settings-tab}

在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡下，确定要显示的内容：

* **[!UICONTROL 显示名称]**

   特色内容列表的标题。 例如`Featured Questions`或`Featured Ideas`。 如果留空，则默认值为`Featured Content`。

* **[!UICONTROL 专题内容的位置]**

   *（必需）浏* 览到包含可能具有功能的内容的页面（该页面的组件必须配置为允许特色内容）。例如，`/content/sites/engage/en/forum`。

* **[!UICONTROL 显示限制]**

   要显示的特色内容的最大数量。 默认值为5。

## 站点访客体验{#site-visitor-experience}

将内容标记为特色内容需要审查方权限。

审查方视图发布内容时，他们有权访问上下文中的审核标志，该标志包括新的`Feature`标志。

![chlimage_1-16](assets/chlimage_1-16.png)

标记为功能后，模型标志变为`Unfeature`。

包含`Featured Content`组件的页面现在将包含此帖子。

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` 是指向实际帖子的链接。

## 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[特色内容](essentials-featured.md)页面。

有关标记特色内容，请参阅[协调用户生成的内容](moderate-ugc.md)。
