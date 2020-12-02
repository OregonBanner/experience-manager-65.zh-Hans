---
title: 上下文协调
seo-title: 上下文协调
description: 如何执行审查方操作
seo-description: 如何执行审查方操作
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: 917fceffb58883df83e96f60da4769046a18f3c0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# 上下文协调{#in-context-moderation}

对于AEM Communities，协调可由管理员和受信任的社区成员直接在发布社区内容的页面上执行。

当使用[仲裁控制台](moderation.md)时，为内容显示的信息包括指向已发布页面的链接，以允许访问在上下文中进行仲裁时可用的其他仲裁操作。

## 协调操作{#moderation-actions}

有关[协调操作](moderate-ugc.md#moderation-actions)的说明，请访问协调概述。

## 协调UI {#moderation-ui}

发布实例上呈现给审查方的UI包含在用于发布和管理用户生成内容(UGC)的对话框中。 UI的元素由站点访客的状态决定——是否……

1. 发布内容的成员。
1. 受信任的成员审查方。
1. 管理员。
1. 已登录，但既不是管理员、版主也不是内容作者。
1. 未登录。

## 示例 {#example}

使用在[AEM Communities入门](getting-started.md)时创建的[Geometrixx参与](http://localhost:4503/content/sites/engage/en.html)站点，可以快速在论坛中设置一个线程，在论坛中体验发布环境中的各种协调活动，如下所示。

Aaron McDonald(aaron.mcdonald@mailinator.com)在创建网站时将他加入社区参与主持人小组，被确认为值得信赖的社区成员。

Rebekah Larsen(rebekah.larsen@trashymail.com)可以使用[成员控制台](members.md)添加为社区参与成员组的成员。

有关社区用户组的详细信息，请访问[管理用户和用户组](users.md)。

### 创建论坛帖子{#create-the-forum-posts}

* 以丽贝卡·拉森(rebekah.larsen@trashymail.com)的身份登录

   * 选择论坛
   * 选择新建帖子
   * 输入主题

      《蜂鸟喂食器》的花蜜

   * 输入正文文本

      我每年都挂蜂鸟喂食器，但没有成功。 看来他们来了一两天，就是这样。 我一周换一次就太长了？ 我需要早点改变吗？

   * 选择发布
   * 选择注销

* 以Aaron McDonald的身份登录(aaron.mcdonald@mailinator.com)

   * 选择论坛
   * 对于Hummingbird主题，选择“阅读更多”
   * 输入帖子回复的注释

      我每周换一次，5月到10月。

   * 选择回复
   * 选择注销

* 以Andrew Schaeffer(andrew.schaeffer@trashymail.com)身份登录

   * 选择论坛
   * 对于Hummingbird主题，选择“阅读更多”
   * 输入帖子回复的注释

      我销售花蜜和饲料——请访问https://my.viral.url/

   * 选择回复
   * 选择注销

### 匿名站点访客(#5){#anonymous-site-visitor}

以下是未登录(5)的站点访客所看到的论坛的视图。

匿名网站访客只能视图论坛，但我不能发布任何内容，也不能执行任何审核操作。

![社区论坛-访客](assets/community-forum-visitor.png)

### 新成员(#4){#new-member}

在创作时，以管理员身份登录，使用[成员控制台](members.md)，然后注销，将Boyd Larsen(boyd.larsen@dodgit.com)添加为community-engage-members组的新成员。

在发布时，以Boyd Larsen身份登录，然后选择`Forum`，然后选择`Read more`作为蜂鸟帖子访问线程。

通知:

* 博伊德没有参加论坛。
* Boyd不能删除任何内容。
* Boyd已登录，可以回复或标记内容。

让Boyd选择Flag标记Andrew发布的内容。

注销

![社区论坛——成员](assets/community-forum-member.png)

### 管理员(#3){#administrator}

以管理员（管理员）身份登录，通过选择论坛，然后阅读帖子的更多内容来访问该线程。

通知:

* 管理员可以标记、删除、编辑、拒绝、剪切、关闭、固定、功能。
* 管理员可以选择“管理”以访问审核控制台。

![社区管理论坛](assets/community-admin-forum.png)

选择“管理”菜单项以从发布环境访问[协调控制台](moderation.md)。

请注意，对于管理员，所有可审核的内容都可见，而不仅仅是来自Geometrixx参与社区站点的内容。

搜索筛选器是打开或关闭的侧面板。

注销.

![仲裁控制台——发布](assets/moderation-console-publish.png)

### 社区审查方(#2){#community-moderator}

以社区主持人Aaron McDonald(aaron.mcdonal@mailinator.com)的身份登录，选择“论坛”，然后为蜂鸟帖子阅读更多内容，即可访问主题。

通知:

* Aaron可以回复、删除、编辑或拒绝自己的帖子。
* Aaron还可以标记／允许、回复、删除、编辑、拒绝其他内容。
* 艾伦·坎·库特将论坛话题转到他主持的另一个论坛。
* Aaron可以选择“管理”以访问协调控制台。

![社区论坛——主持人](assets/community-forum-moderator.png)

选择“管理”菜单项以从发布环境访问[协调控制台](moderation.md)。

请注意，对于社区审查方，只能看到“Geometrixx参与”社区站点中的可审核内容。

请注意，社区审查方具有与管理员相同的选项（图像处于搜索提要栏切换关闭状态），但无权访问其他AEM控制台。

注销.

![版主访问](assets/moderator-access.png)

### 内容作者(#1){#content-author}

以Rebekah Larsen(rebekah.larsen@mailinator.com)的身份登录，他是社区成员，他启动了此主题，通过选择“论坛”访问此主题，然后为蜂鸟帖子阅读更多内容。

通知:

* Rebekah可以删除或编辑她自己的帖子。
* Rebekah还可以回复或标记其他内容。
* Rebekah无法访问协调控制台。

![社区论坛——作者](assets/community-forum-author.png)

