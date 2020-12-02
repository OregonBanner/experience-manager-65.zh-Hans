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


# 使用评级{#using-ratings}

`Rating`组件单独使用，或与其他Communities功能结合使用。 此组件允许已登录的社区成员通过对内容进行评级来表达其意见。

## 向页面{#adding-a-rating-to-a-page}添加评级

要在创作模式下将`Rating`组件添加到页面，请找到该组件`Communities / Rating`并将其拖动到页面上的位置，如要对成员进行评级的相对于功能的位置。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[必需的客户端库](rating-basics.md#essentials-for-client-side)时，将显示`Rating`组件。

![评级](assets/rating.png)

## 配置等级{#configuring-rating}

选择要访问的已放置`Rating`组件，然后选择打开编辑对话框的`Configure`图标。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文本和标签]**&#x200B;选项卡下，指定评级的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*必需*)唯一标识此实例 `Rating` 的简单名称。必须为存储库的有效节点名称。

## 站点访客体验{#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个等级。 会员可随时更改其评级。

### 匿名 {#anonymous}

不支持匿名发布评级。 站点访客必须注册（成为会员）并登录才能参加。

## 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[ Rating Essentials](rating-basics.md)页面。
