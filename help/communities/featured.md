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
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# 特色内容功能{#featured-content-feature}

## 简介 {#introduction}

特色内容功能在发布环境中为登录网站访客（社区成员）提供了一个区域，用于突出显示以下内容：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [论坛](forum.md)
* [构思](ideation-feature.md)
* [问题与解答](working-with-qna.md)

将内容标记为特有内容后，它将列在此组件中，该组件可能会放置在特定的登陆页面或容易引起社区成员注意的区域中。

每个组件可能允许或不允许功能显示内容。

文档的此部分描述：

* 向社区站点添加特色内容。
* `Featured Content`组件的配置设置。

## 向页面{#adding-featured-content-to-a-page}添加特色内容

要在创作模式下向页面添加`Featured Content`组件，请使用组件浏览器找到

* `Communities / Featured Content`

并将其拖动到应显示特色内容的页面上。

有关必要信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](essentials-featured.md#essentials-for-client-side)时，将显示`Featured Content`组件：

![功能内容](assets/featuredcontent.png)

## 配置特色内容{#configuring-featured-content}

选择要访问的已放置的`Featured Content`组件，然后选择`Configure`图标以打开编辑对话框。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### “设置”选项卡{#settings-tab}

在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡下，识别要显示的内容：

* **[!UICONTROL 显示名称]**

   特色内容列表的标题。 例如`Featured Questions`或`Featured Ideas`。 如果留空，则默认值为`Featured Content`。

* **[!UICONTROL 专题内容的位置]**

   *（必需）* 浏览到包含可能具有功能的内容的页面（该页面的组件必须配置为允许具有功能的内容）。例如，`/content/sites/engage/en/forum`。

* **[!UICONTROL 显示限制]**

   要显示的特色内容的最大数量。 默认值为5。

## 网站访客体验{#site-visitor-experience}

要将内容标记为特色内容的功能需要审核者权限。

审核者查看发布的内容时，有权访问上下文内审核标记，该标记包含新的`Feature`标记。

![site-visitor-experience](assets/site-visitor-experience.png)

标记为功能后，建模标记将变为`Unfeature`。

现在，包含`Featured Content`组件的页面将包含此帖子。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 是指向实际帖子的链接。

## 附加信息 {#additional-information}

有关更多信息，请参阅[特色内容](essentials-featured.md)页面，供开发人员使用。

要将内容标记为特有，请参阅[审核用户生成的内容](moderate-ugc.md)。
