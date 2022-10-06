---
title: 使用称赞
seo-title: Using Liking
description: 添加和配置称赞组件
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

# 使用称赞 {#using-liking}

的 `Liking` 组件是一个有用的工具，它允许用户对特定内容（如论坛中的评论）发表意见。 使用 `Liking` 组件中，成员选择心图标以指示积极意见。

## 向页面添加称赞 {#adding-liking-to-a-page}

添加 `Liking` 组件添加到创作模式下的页面，可使用组件浏览器找到

* `Communities / Liking`

并将其拖动到页面上的位置，如用户喜欢的相对于该功能的位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-liking.md#essentials-for-client-side) 包含，这是 `Liking` 组件。

![称赞组件](assets/liking-component.png)

## 配置称赞 {#configuring-liking}

选择已放置的 `Liking` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，指定用于记录称赞的属性。

![配置称赞](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

   (*必需*)正向响应的属性名称。

* **[!UICONTROL 负面响应标签]**

   (*必需*)负响应的属性名称。

* **[!UICONTROL 标签名称]**

   (*必需*)此投票组件实例的内部可识别属性名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

会员可以随时更改其样式。

### 匿名 {#anonymous}

不支持匿名称赞。 网站访客必须注册（成为会员）并登录以参与称赞。

## 附加信息 {#additional-information}

有关 [称赞要点](essentials-liking.md) 页面。
