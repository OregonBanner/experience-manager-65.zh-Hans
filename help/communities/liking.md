---
title: 使用点赞
description: 了解如何添加和配置Liking组件，以便用户可以就特定内容（如评论）发表意见。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---

# 使用点赞 {#using-liking}

此 `Liking` 组件是一种非常有用的工具，它允许用户表达对特定内容（如论坛中的评论）的意见。 使用 `Liking` 组件中，成员选择心形图标以指示积极的意见。

## 向页面添加点赞 {#adding-liking-to-a-page}

添加 `Liking` 组件到创作模式下的页面，请使用组件浏览器查找

* `Communities / Liking`

并将其拖动到页面上的适当位置，例如用户喜欢的相对于该功能的位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-liking.md#essentials-for-client-side) 包括，这就是 `Liking` 组件出现。

![liking-component](assets/liking-component.png)

## 配置点赞 {#configuring-liking}

选择已放置的 `Liking` 组件，以便您能够访问和选择 `Configure` 图标打开“编辑”对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，指定用于记录“赞”的属性。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

  (*必填*)肯定响应的属性名称。

* **[!UICONTROL 负面响应标签]**

  (*必填*)负面响应的属性名称。

* **[!UICONTROL 标签名称]**

  (*必填*)投票组件的此实例的内部可识别属性名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

成员可随时更改“赞”。

### 匿名 {#anonymous}

不支持匿名点赞。 网站访客必须注册（成为会员）并登录才能参与点赞。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [点赞Essentials](essentials-liking.md) 适用于开发人员的页面。
