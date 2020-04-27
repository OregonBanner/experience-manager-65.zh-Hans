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
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# 使用评级 {#using-ratings}

该组 `Rating` 件单独使用，或与其他Communities功能一起使用。 此组件允许已登录的社区成员通过对内容进行评级来表达其意见。

## Adding a Rating to a Page {#adding-a-rating-to-a-page}

要在创作模 `Rating``Communities / Rating` 式下将组件添加到页面，请找到该组件并将其拖动到页面上的相应位置，如相对于要评级的成员的功能的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含 [所需的客户端库时](rating-basics.md#essentials-for-client-side) ，组件的显示方式 `Rating` 就是这样的。

![chlimage_1-493](assets/chlimage_1-493.png)

## 配置评级 {#configuring-rating}

选择要访问 `Rating` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-494](assets/chlimage_1-494.png)

在“文 **[!UICONTROL 本和标签]** ”选项卡下，指定评级的内部标识符。

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Tally Name]**(*Required*)唯一标识此实例的 `Rating`简单名称。 必须为存储库的有效节点名称。

## 站点访客体验 {#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个评级。 会员可随时更改其评级。

### 匿名 {#anonymous}

不支持匿名发布评级。 站点访客必须注册（成为会员）并登录以参与。

## 附加信息 {#additional-information}

有关详细信息，请参阅面向开发 [人员的Rating Essentials](rating-basics.md) （评级基本信息）页面。
