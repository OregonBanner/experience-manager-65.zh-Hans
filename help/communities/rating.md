---
title: 使用评级
seo-title: Using Ratings
description: 向页面添加评级组件
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 使用评级 {#using-ratings}

此 `Rating` 组件可独立使用或与其他Communities功能结合使用。 此组件允许已登录的社区成员通过评级内容来表达他们的意见。

## 向页面添加评级 {#adding-a-rating-to-a-page}

添加 `Rating` 组件到创作模式下的页面，找到该组件 `Communities / Rating` 并将其拖动到页面上的适当位置，例如相对于该特征的位置以供成员评级。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](rating-basics.md#essentials-for-client-side) 包括，这就是 `Rating` 组件随即出现。

![评级](assets/rating.png)

## 配置评级 {#configuring-rating}

选择已放置的 `Rating` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，指定评分的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL 标签名称]**
(*必需*)的简单名称 `Rating` 唯一地标识此实例。 必须为存储库的有效节点名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个评级。 会员可以随时变更等级。

### 匿名 {#anonymous}

不支持匿名发布评级。 网站访客必须注册（成为会员）并登录才能参与。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [Rating Essentials](rating-basics.md) 适用于开发人员的页面。
