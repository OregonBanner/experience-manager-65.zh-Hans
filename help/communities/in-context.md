---
title: 上下文审核
seo-title: In-Context Moderation
description: 如何执行审查方操作
seo-description: How to perform moderator actions
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 上下文审核 {#in-context-moderation}

对于AEM Communities，管理员和受信任的社区成员可以直接在发布社区内容的已发布页面上执行审核。

使用 [审核控制台](moderation.md)中，为内容显示的信息包含指向已发布页面的链接，通过该链接可访问在上下文中进行审核时可用的其他审核操作。

## 审核操作 {#moderation-actions}

有关的描述，请访问审核概述 [审核操作](moderate-ugc.md#moderation-actions).

## 审核用户界面 {#moderation-ui}

在发布实例上向审查方呈现的UI包含在用于发布和管理用户生成内容(UGC)的对话框中。 UI的元素由网站访客的状态决定，无论它们是否……

1. 发布内容的成员。
1. 受信任的成员审查方。
1. 管理员。
1. 已登录，但不是内容的管理员、审查方或作者。
1. 未登录。

## 示例 {#example}

使用 [Geometrixx参与](http://localhost:4503/content/sites/engage/en.html) 站点创建时间 [AEM Communities快速入门](getting-started.md)，可在论坛中快速设置主题，以便在发布环境中体验各种审核活动，如下所示。

Aaron McDonald (aaron.mcdonald@mailinator.com)在创建站点时添加了community-engage-moderators组，被认定为受信任的社区成员。

Rebekah Larsen (rebekah.larsen@trashymail.com)可以通过以下方式添加为community-engage-members组的成员： [成员控制台](members.md).

有关社区用户组的更多信息，请访问 [管理用户和用户组](users.md).

### 创建论坛帖子 {#create-the-forum-posts}

* 以Rebekah Larsen的身份登录(rebekah.larsen@trashymail.com)

   * 选择论坛
   * 选择新帖子
   * 输入主题

     蜂鸣喂鸟机什么时候换花蜜

   * 输入正文文本

     我每年都挂一只蜂鸟喂食器，可没取得多少成功。 他们似乎来了一两天，就这样了。 我每周换一次会不会太长？ 我是否需要更快地更改它？

   * 选择帖子
   * 选择注销

* 以Aaron McDonald (aaron.mcdonald@mailinator.com)登录

   * 选择论坛
   * 对于“蜂鸟”主题，请选择“阅读更多”
   * 为帖子回复输入评论

     我每周换一次衣服，从5月到10月都有。

   * 选择回复
   * 选择注销

* 以Andrew Schaeffer身份登录(andrew.schaeffer@trashymail.com)

   * 选择论坛
   * 对于“蜂鸟”主题，请选择“阅读更多”
   * 为帖子回复输入评论

     我销售花蜜和饲料 — 请访问https://my.viral.url/

   * 选择回复
   * 选择注销

### 匿名网站访客(#5) {#anonymous-site-visitor}

以下是未登录(5)的站点访客所看到的论坛视图。

匿名网站访客只能查看论坛，但不能发布任何内容或执行任何审核操作。

![community-forum-visitor](assets/community-forum-visitor.png)

### 新成员(#4) {#new-member}

boyd.larsen@dodgit.com在作者上，以管理员身份登录，并使用 [成员控制台](members.md)，然后注销。

在发布时，以Boyd Larsen身份登录，并通过选择 `Forum`，然后 `Read more` 来做蜂鸟贴文。

通知:

* 博伊德没有参加论坛。
* 博伊德无法删除任何内容。
* Boyd已登录，可以回复或标记内容。

让Boyd选择Flag来标记Andrew发布的内容。

注销

![community-forum-ember](assets/community-forum-member.png)

### 管理员(#3) {#administrator}

以管理员（管理员）身份登录，并通过选择“论坛”访问该会话，然后选择“阅读更多帖子”。

通知:

* 管理员可以标记、删除、编辑、拒绝、剪切、关闭、固定、功能。
* 管理员可以选择管理以访问审核控制台。

![community-admin-forum](assets/community-admin-forum.png)

选择管理菜单项以访问 [审核控制台](moderation.md) 从发布环境中。

请注意，对于管理员，所有可审核内容均可见，而不仅仅是Geometrixx参与社区网站中的内容。

搜索过滤器是切换打开或关闭的侧面板。

注销.

![moderation-console-publish](assets/moderation-console-publish.png)

### 社区审查方(#2) {#community-moderator}

以社区审查方Aaron McDonald (aaron.mcdonal@mailinator.com)身份登录，并通过选择“论坛”访问该会话，然后阅读蜂鸟帖子的更多信息。

通知:

* Aaron可以回复、删除、编辑或拒绝自己的帖子。
* Aaron还可以标记/允许、回复、删除、编辑、拒绝其他内容。
* Aaron可以剪切论坛主题，将其移至他主持的另一个论坛。
* Aaron可以选择管理以访问审核控制台。

![community-forum-moder](assets/community-forum-moderator.png)

选择管理菜单项以访问 [审核控制台](moderation.md) 从发布环境中。

请注意，对于社区审查方，只能看到GeometrixxEngage社区站点中的可审查内容。

请注意，社区审查方具有与管理员相同的选项（图像已关闭搜索侧栏），但无法访问其他AEM控制台。

注销.

![moderator-access](assets/moderator-access.png)

### 内容作者(#1) {#content-author}

以Rebekah Larsen (rebekah.larsen@mailinator.com)登录，他是启动该会话的社区成员，并通过选择“论坛”访问该会话，然后阅读hummingbird帖子的更多信息。

通知:

* 丽贝卡可以删除或编辑自己的帖子。
* Rebekah还可以回复或标记其他内容。
* Rebekah无法访问审核控制台。

![community-forum-author](assets/community-forum-author.png)
