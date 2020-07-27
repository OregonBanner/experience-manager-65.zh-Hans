---
title: 使用喜欢
seo-title: 使用喜欢
description: 添加和配置“喜欢”组件
seo-description: 添加和配置“喜欢”组件
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用喜欢 {#using-liking}

该 `Liking` 组件是一个有用的工具，它允许用户对特定内容（如论坛中的评论）发表意见。 使用组 `Liking` 件，成员选择心形图标以表示积极的意见。

## 为页面添加喜欢 {#adding-liking-to-a-page}

要在创作模 `Liking` 式下将组件添加到页面，请使用组件浏览器来查找

* `Communities / Liking`

并将其拖动到页面上的位置，如用户喜欢的功能的相对位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包 [含所需的客户端库](essentials-liking.md#essentials-for-client-side) ，组件的显示 `Liking` 方式即为此。

![喜欢组件](assets/liking-component.png)

## 配置喜欢 {#configuring-liking}

选择要访问的 `Liking` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![configure-new](assets/configure-new.png)

在“文 **[!UICONTROL 本和标签]** ”选项卡下，指定用于记录喜欢的属性。

![配置类型](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

   (*必需*)正向响应的属性名称。

* **[!UICONTROL 负面响应标签]**

   (*必需*)负响应的属性名称。

* **[!UICONTROL 标签名称]**

   (必&#x200B;*需*)此投票组件实例的内部可识别属性名称。

## 站点访客体验 {#site-visitor-experience}

### 成员 {#members}

会员可随时更改其类型。

### 匿名 {#anonymous}

不支持匿名喜欢。 站点访客必须注册（成为会员）并登录以参与喜欢活动。

## 附加信息 {#additional-information}

有关更多信息，请参阅开发 [人员的](essentials-liking.md) “喜欢基本工具”页。
