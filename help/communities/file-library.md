---
title: 文件库功能
description: 利用文件库功能，已登录的网站访客可以上传、管理和下载文件
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 7%

---

# 文件库功能{#file-library-feature}

## 简介 {#introduction}

文件库功能为已登录站点访客（社区成员）提供了一个在社区站点中上传、管理和下载文件的位置。

本文档的这一部分描述了：

* 将文件库功能添加到AEM站点。
* 的配置设置 `File Library` 组件。

### 将文件库添加到页面 {#adding-a-file-library-to-a-page}

添加 `File Library` 组件到创作模式下的页面，找到组件：

* `Communities / File Library`

并将其拖动到页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

当 [所需的客户端库](/help/communities/essentials-file-library.md#essentials-for-client-side) 包括，它是 `File Library` 组件出现：

![file-library1](assets/file-library1.png)

### 配置文件库 {#configuring-file-library}

选择已放置的 `File Library` 组件，以便您可以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### “评论”选项卡 {#comments-tab}

在 **注释** 选项卡，指定是否以及如何显示已上载文件的注释：

* **允许对文件发表评论**

  如果选中，则允许对上传的文件添加注释。 默认值为未选中。

* **每页的评论数**

  限制每页显示的评论数和显示的回复数。 默认为 **10**.

* **最大文件大小**

  此值限制上传的文件大小。 默认限制为104857600 (10 MB)。

* **最大消息长度**

  文本框中可以输入的最大字符数。 默认值为4096个字符。

* **允许的文件类型**

  包含“点”分隔符的逗号分隔文件扩展名列表。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定任何文件类型。 默认值未指定，因此允许所有文件类型。

* **富文本编辑器**

  如果选中，则可以使用标记输入注释。 默认值为未选中。

* **删除评论**

  如果选中，则允许用户删除自己的注释。 默认值为已选中。

* **允许标记**

  如果选中，将启用向文件添加标记的功能。 默认值为未选中。

* **允许的命名空间**

  如果选中了“允许标记”，则可用标记将仅限于已选中命名空间。 如果未检查任何命名空间，则允许使用所有命名空间。 默认值为所有命名空间。

* **建议限制**

  如果选中了“允许标记”，则此设置将限制要显示的建议标记数量。 如果设置为–1，则无限制。 默认值为–1。

* **允许投票**

  如果选中，则启用对文件投票的功能。 默认值为未选中。

* **允许关注**

  如果选中，则为博客文章包括以下功能，此功能允许成员成为 [已通知](/help/communities/notifications.md) 新帖子的数量。 默认值为未选中。

* **启用提及功能**

  如果启用，则允许注册社区用户标识其他注册成员（使用名字、姓氏、用户名），并使用通用@user-name语法标记它们。 标记的用户会收到有关其提及的通知。

* **最大提及次数**

  限制帖子中允许的最多提及次数。 默认值为10。

* **UI 提及模式**

  指定允许的模式字符串，以便在帖子中标记(@mention)已注册的用户。 例如： `~{{familyName}}{{givenName}}`。

* **允许主题回复**

  如果选中，则允许回复已发布的评论。 默认值为未选中。

#### “用户审核”选项卡 {#user-moderation-tab}

在 **用户审核** 选项卡，配置评论的审核（如果允许评论）：

* **预审**

  如果选中，评论必须先获得批准，然后才能显示在发布网站上。 默认值为未选中。

* **删除评论**

  如果选中，发布评论的访客可以根据需要删除评论。 默认值为已选中。

* **拒绝评论**

  如果选中，则允许受信任的成员审查方拒绝评论。 默认值为未选中。

* **关闭/重新打开注释**

  如果选中，则允许受信任的成员审查方关闭和重新打开注释。 默认值为未选中。

* **标记注释**

  如果选中，则允许访客将评论标记为不适当。 默认值为未选中。

* **标记原因列表**

  如果选中，则允许访客从下拉列表中选择将评论标记为不适当的原因。 默认值为未选中。

* **自定义标志原因**

  如果选中，则允许访客输入将评论标记为不适当的原因。 默认值为未选中。

* **审核阈值**

  输入在通知审查方之前，访客必须标记评论的次数。 默认为一次(**1**)。

* **标记限制**

  输入在将评论从公开视图隐藏之前必须对其标记的次数。 此数字必须大于或等于 **审核阈值**. 默认值为5。

### “排序设置”选项卡 {#sort-settings-tab}

排序方式

设置为默认

### 附加信息 {#additional-information}

欲知更多信息，请访问 [文件库要点](/help/communities/essentials-file-library.md) 适用于开发人员的页面。

有关审核已发布的主题和评论，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

有关标记已发布的主题和评论，请参阅 [标记用户生成的内容](/help/communities/tag-ugc.md).
