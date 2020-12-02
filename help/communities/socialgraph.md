---
title: 使用社交图
seo-title: 使用社交图
description: 向页面添加以下组件
seo-description: 向页面添加以下组件
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# 使用社交图{#using-social-graph}

## 简介 {#introduction}

社区成员遵循[活动](activities.md)并遵循的能力通过两个组件建立：`Follow`和`Following`。

`Follow`组件必须与其他资源关联，并且已为社区成员和功能建立此关联。

`Following`组件只列表当前成员之后或当前成员后面的成员。 在为[社区站点](overview.md#communitiessites)建立的用户用户档案中，包含成员之间关系的社交图。

## 向页面{#adding-following-to-a-page}添加以下内容

如果希望在创作模式下向页面添加`Following`组件，请找到该组件`Communities / Following`，并将其拖动到应显示社交图的页面上。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[必需的客户端库](essentials-socialgraph.md#essentials-for-client-side)时，`Following`组件的显示方式如下：

![以下](assets/following.png)

## 配置以下{#configuring-following}

当前，必须设置属性以确定组件显示`follows`关系还是`following`关系。

## 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[Social Graph Essentials](essentials-socialgraph.md)页面。
