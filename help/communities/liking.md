---
title: 使用点赞
seo-title: Using Liking
description: 添加和配置链接组件
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# 使用点赞 {#using-liking}

此 `Liking` 组件是一种非常有用的工具，它允许用户表达对特定内容（如论坛中的评论）的意见。 使用 `Liking` 组件时，成员选择心形图标以指示正面意见。

## 向页面添加点赞 {#adding-liking-to-a-page}

添加 `Liking` 组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Liking`

并将其拖动到页面上的适当位置，例如用户喜欢的相对于该功能的位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-liking.md#essentials-for-client-side) 包括，这就是 `Liking` 组件随即出现。

![liking-component](assets/liking-component.png)

## 配置点赞 {#configuring-liking}

选择已放置的 `Liking` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，指定用于记录“赞”的属性。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

   (*必需*)积极响应的属性名称。

* **[!UICONTROL 负面响应标签]**

   (*必需*)负响应的属性名称。

* **[!UICONTROL 标签名称]**

   (*必需*)投票组件的此实例的内部可识别属性名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

成员可随时更改其喜好。

### 匿名 {#anonymous}

不支持匿名点赞。 网站访客必须注册（成为会员）并登录才能参与点赞。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [点赞Essentials](essentials-liking.md) 适用于开发人员的页面。
