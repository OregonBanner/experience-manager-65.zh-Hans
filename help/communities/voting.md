---
title: 使用投票
description: 了解如何将投票组件添加到允许登录社区成员对特定内容（例如答案）进行评级的页面。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

# 使用投票 {#using-voting}

此 `Voting` 组件是一个非常有用的工具，它允许社区成员对特定内容片段（如QnA组件中的答案）进行评级。 使用 `Voting` 组件，成员选择向上箭头或向下箭头来指示其意见。

## 向页面添加投票 {#adding-voting-to-a-page}

添加 `Voting` 组件添加到创作模式下的页面，请使用组件浏览器。 定位 `Communities / Voting` 并将其拖动到页面上的适当位置，例如相对于供用户投票的功能位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](essentials-voting.md#essentials-for-client-side) 包括，这就是 `Voting` 组件出现。

![投票组件](assets/voting-component.png)

## 配置投票 {#configuring-voting}

选择已放置的 `Voting` 组件，以便您能够访问和选择 `Configure` 图标打开“编辑”对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 文本和标签]** 选项卡，指定用于记录投票的属性。

![投票标签](assets/voting-label.png)

* **[!UICONTROL 正面响应标签]**

  (*必填*)积极响应的内部属性名称。

* **[!UICONTROL 负面响应标签]**

  (*必填*)负面响应的内部属性名称。

* **[!UICONTROL 标签名称]**

  (*必填*)投票组件的此实例的内部可识别属性名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

成员只能投票一次，但可随时更改投票。

### 匿名 {#anonymous}

不支持匿名投票。 网站访客必须注册（成为会员）并登录才能参加投票一次。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [Voting Essentials](essentials-voting.md) 适用于开发人员的页面。
