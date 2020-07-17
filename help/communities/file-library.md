---
title: 文件库功能
seo-title: 文件库功能
description: “文件库”功能允许登录站点访客上传、管理和下载文件
seo-description: “文件库”功能允许登录站点访客上传、管理和下载文件
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 9e941ce092f7d3248c11886d6bf1e54f2e726362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 6%

---


# 文件库功能{#file-library-feature}

## 简介 {#introduction}

文件库功能为登录站点访客（社区成员）提供了一个位置，供他们上传、管理和下载社区站点内的文件。

文档的本节介绍：

* 将文件库功能添加到AEM站点。
* 组件的配置 `File Library` 设置。

### 将文件库添加到页面 {#adding-a-file-library-to-a-page}

要在创作模 `File Library` 式下将组件添加到页面，请找到该组件：

* `Communities / File Library`

并将其拖动到页面上的位置。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包 [含所需的客户端库](/help/communities/essentials-file-library.md#essentials-for-client-side) ，组件的显示 `File Library` 方式如下：

![chlimage_1-430](assets/chlimage_1-430.png)

### 配置文件库 {#configuring-file-library}

选择要访问的 `File Library` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-431](assets/chlimage_1-431.png)

![chlimage_1-432](assets/chlimage_1-432.png)

#### “注释”选项卡 {#comments-tab}

在“注 **释** ”选项卡下，指定是否显示已上载文件的注释以及如何显示：

* **允许对文件发表评论**

   如果选中，则允许对已上载的文件进行注释。 默认为未选中。

* **每页的评论数**

   限制每页显示的注释数以及显示的回复数。 Default is **10**.

* **最大文件大小**

   此值将限制已上载文件的大小。 默认限制为104857600(10 Mb)。

* **最大消息长度**

   可输入到文本框中的最大字符数。 默认为4096个字符。

* **允许的文件类型**

   以逗号分隔的文件扩展名列表，以“点”分隔。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定那些未指定的文件类型。 未指定默认值，因此允许所有文件类型。

* **富文本编辑器**

   如果选中，则可以输入带有标记的注释。 默认为未选中。

* **删除评论**

   如果选中，则允许用户删除自己的注释。 选中默认值。

* **允许标记**

   如果选中，则将启用向文件添加标记的功能。 默认为未选中。

* **允许的命名空间**

   如果选中“允许标记”，则可用标记将限制为选中的命名空间。 如果未选中任何项，则允许全部选中。 默认为所有命名空间。

* **建议限制**

   如果选中“允许标记”，则此设置将限制要显示的建议标记数。 如果设置为-1，则没有限制。 默认值为-1。

* **允许投票**

   如果选中，则将启用文件的投票功能。 默认为未选中。

* **允许关注**

   如果选中此项，则为博客文章添加以下功能，允许成员 [收到](/help/communities/notifications.md) 新帖子的通知。 默认为未选中。

* **启用提及功能**

   如果启用，允许注册社区用户识别其他注册成员（使用名、姓、用户名），并使用通用的@user-name语法标记这些成员。 标记用户会收到有关其提及次数的通知。

* **最大提及次数**

   限制帖子中允许的最大提及次数。 默认值为10。

* **UI 提及模式**

   在帖子中为注册用户标记（@提及）指定已允许的模式字符串。 例如~{{familyName}}{{givenName}}。

* **允许主题回复**

   如果选中，则允许回复已发布的注释。 默认为未选中。

#### “用户审核”选项卡 {#user-moderation-tab}

在“用户 **审核** ”选项卡下，配置审核评论（如果允许进行评论）:

* **预审**

   如果选中此项，则注释必须经过批准，才能显示在发布站点上。 默认为未选中。

* **删除评论**

   如果选中，则向发布评论的访客提供删除评论的功能。 选中默认值。

* **拒绝评论**

   如果选中，则允许受信任的成员审核者拒绝评论。 默认为未选中。

* **关闭／重新打开注释**

   如果选中，则允许受信任的成员审核者关闭并重新打开注释。 默认为未选中。

* **标记注释**

   如果选中，允许访客将注释标记为不合适。 默认为未选中。

* **标志原因列表**

   如果选中，允许访客从下拉式列表中选择其标记评论的理由不恰当。 默认为未选中。

* **自定义标志原因**

   如果选中，允许访客输入自己将评论标记为不合适的原因。 默认为未选中。

* **审核阈值**

   输入访客在通知版主之前必须标记评论的次数。 默认值为一次(**1**)。

* **标记限制**

   输入评论在隐藏之前必须标出的次数，使其不受公共视图。 此数字必须大于或等于仲裁 **阈值**。 默认值为5。

### “排序设置”选项卡 {#sort-settings-tab}

排序方式

设置为默认

### 附加信息 {#additional-information}

有关开发人员的详细信息， [请参阅“文件库](/help/communities/essentials-file-library.md) Essentials”页。

有关审核已发布的主题和评论，请参 [阅审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记已发布的主题和评论，请参 [阅标记用户生成的内容](/help/communities/tag-ugc.md)。
