---
title: 使用评级
seo-title: 使用评级
description: 向页面添加评级组件
seo-description: 向页面添加评级组件
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---


# 使用评级 {#using-ratings}

该组 `Rating` 件单独使用，或与其他Communities功能结合使用。 此组件允许已登录的社区成员通过对内容进行评级来表达其意见。

## Adding a Rating to a Page {#adding-a-rating-to-a-page}

要在创作 `Rating` 模式下将组件添加到页面，请找到该组 `Communities / Rating` 件并将其拖动到页面上的位置，如要对成员进行评级的相对于功能的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包 [含所需的客户端库](rating-basics.md#essentials-for-client-side) ，组件的显示 `Rating` 方式即为此。

![评级](assets/rating.png)

## 配置等级 {#configuring-rating}

选择要访问的 `Rating` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![configure-new](assets/configure-new.png)

在“文 **[!UICONTROL 本和标签]** ”选项卡下，指定“评级”的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**(*必需*)唯一标识此实例 `Rating` 的简单名称。 必须为存储库的有效节点名称。

## 站点访客体验 {#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个等级。 会员可随时更改其评级。

### 匿名 {#anonymous}

不支持匿名发布评级。 站点访客必须注册（成为会员）并登录才能参加。

## 附加信息 {#additional-information}

有关更多信息，请参阅开发 [人员的“Rating](rating-basics.md) Essentials”页面。
