---
title: 使用评级
description: 了解如何向页面添加评级组件，该页面允许登录社区成员通过评级内容来表达他们的意见。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# 使用评级 {#using-ratings}

此 `Rating` 组件可单独使用，也可与其他Communities功能一起使用。 此组件允许登录的社区成员通过评级内容来表达他们的意见。

## 向页面添加评级 {#adding-a-rating-to-a-page}

添加 `Rating` 组件到创作模式下的页面，找到该组件 `Communities / Rating` 并将其拖动到页面上的适当位置，例如相对于该特征的位置以供成员评级。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](rating-basics.md#essentials-for-client-side) 包括，这就是 `Rating` 组件出现。

![评级](assets/rating.png)

## 配置评级 {#configuring-rating}

选择已放置的 `Rating` 组件，以便您能够访问和选择 `Configure` 图标打开“编辑”对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，您可以指定评分的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL 标签名称]**
(*必填*)的简单名称 `Rating` 唯一地标识此实例。 必须为存储库的有效节点名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个评级。 会员可以随时变更等级。

### 匿名 {#anonymous}

不支持匿名发布评级。 网站访客必须注册（成为会员）并登录才能参与。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [Rating Essentials](rating-basics.md) 适用于开发人员的页面。
