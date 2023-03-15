---
title: 使用社交图
seo-title: Using Social Graph
description: 将以下组件添加到页面
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# 使用社交图 {#using-social-graph}

## 简介 {#introduction}

社区成员关注的功能 [活动](activities.md) 以及遵循通过两个组件来建立： `Follow` 和 `Following`.

此 `Follow` 组件必须与其他资源相关联，并且已为社区成员和功能建立此关联。

此 `Following` 组件仅列出位于当前成员后面或位于当前成员后面的成员。 成员之间关系的社交图包含在为创建的用户配置文件中 [社区站点](overview.md#communitiessites).

## 向页面添加以下内容 {#adding-following-to-a-page}

如果需要添加 `Following` 组件到创作模式下的页面，找到该组件 `Communities / Following` 并将其拖动到应显示社交图的页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-socialgraph.md#essentials-for-client-side) 包括，这就是 `Following` 组件将显示：

![关注](assets/following.png)

## 配置以下内容 {#configuring-following}

当前，需要设置属性以确定组件是否显示 `follows` 关系，或 `following` 关系。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [社交图要点](essentials-socialgraph.md) 适用于开发人员的页面。
