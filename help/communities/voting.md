---
title: 使用投票
seo-title: 使用投票
description: 将投票组件添加到页面
seo-description: 将投票组件添加到页面
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# 使用投票 {#using-voting}

组 `Voting` 件是一个有用的工具，它允许社区成员对特定内容（如问题与答案组件中的答案）进行评级。 使用组 `Voting` 件，成员选择向上或向下箭头以指示其意见。

## 向页面添加投票 {#adding-voting-to-a-page}

要在创作 `Voting` 模式下将组件添加到页面，请使用组件浏览器 `Communities / Voting` 在页面上查找并将其拖动到相应位置，如用户要投票时相对于该功能的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包 [含所需的客户端库](essentials-voting.md#essentials-for-client-side) ，组件的显示 `Voting` 方式即为此。

![投票组件](assets/voting-component.png)

## 配置投票 {#configuring-voting}

选择要访问的 `Voting` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![配置](assets/configure-new.png)

在“文 **[!UICONTROL 本和标签]** ”选项卡下，指定用于记录投票的属性。

![投票标签](assets/voting-label.png)

* **[!UICONTROL 正面响应标签]**

   (*必需*)正向响应的内部属性名称。

* **[!UICONTROL 负面响应标签]**

   (*必需*)负响应的内部属性名称。

* **[!UICONTROL 标签名称]**

   (必&#x200B;*需*)此投票组件实例的内部可识别属性名称。

## 站点访客体验 {#site-visitor-experience}

### 成员 {#members}

成员只能投一票，但可随时更改其投票。

### 匿名 {#anonymous}

不支持匿名投票。 网站访客必须注册（成为会员）并登录一次以参加投票。

## 附加信息 {#additional-information}

有关开发人员的详细信息， [请参阅](essentials-voting.md) “投票基础”页。
