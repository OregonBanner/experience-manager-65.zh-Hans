---
title: 文件库功能
seo-title: 文件库功能
description: “文件库”功能允许登录站点的访客上传、管理和下载文件
seo-description: “文件库”功能允许登录站点的访客上传、管理和下载文件
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 7%

---

# 文件库功能{#file-library-feature}

## 简介 {#introduction}

文件库功能为已登录的站点访客（社区成员）上传、管理和下载社区站点中的文件提供了一个位置。

文档的此部分描述：

* 将文件库功能添加到AEM站点。
* `File Library`组件的配置设置。

### 将文件库添加到页面{#adding-a-file-library-to-a-page}

要在创作模式下向页面添加`File Library`组件，请找到该组件：

* `Communities / File Library`

并将其拖动到页面上的位置。

有关必要信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/essentials-file-library.md#essentials-for-client-side)时，将显示`File Library`组件：

![file-library1](assets/file-library1.png)

### 配置文件库{#configuring-file-library}

选择要访问的已放置的`File Library`组件，然后选择`Configure`图标以打开编辑对话框。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### “注释”选项卡{#comments-tab}

在&#x200B;**注释**&#x200B;选项卡下，指定上载文件的注释是否以及显示方式：

* **允许对文件发表评论**

   如果选中此项，则允许对已上传的文件进行注释。 默认为未选中。

* **每页的评论数**

   限制每页显示的评论数以及显示的回复数。 默认值为&#x200B;**10**。

* **最大文件大小**

   此值将限制上传的文件大小。 默认限制为104857600(10 Mb)。

* **最大消息长度**

   可在文本框中输入的最大字符数。 默认为4096个字符。

* **允许的文件类型**

   以逗号分隔的文件扩展名列表，其中带有“圆点”分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则将不允许指定未指定的文件类型。 未指定默认值，以允许使用所有文件类型。

* **富文本编辑器**

   如果选中，则可以输入带有标记的注释。 默认为未选中。

* **删除评论**

   如果选中，则允许用户删除其自己的评论。 默认选中。

* **允许标记**

   如果选中此项，则将启用向文件添加标记的功能。 默认为未选中。

* **允许的命名空间**

   如果选中允许标记，则可用的标记将限制为选中的命名空间。 如果未选中“无”，则允许使用所有选项。 默认值是所有命名空间。

* **建议限制**

   如果选中允许标记，则此设置将限制要显示的建议标记数。 如果设置为–1，则没有限制。 默认值为–1。

* **允许投票**

   如果选中，则将启用选民文件的功能。 默认为未选中。

* **允许关注**

   如果选中此项，请为博客文章添加以下功能，该功能允许成员在新帖子中[收到通知](/help/communities/notifications.md)。 默认为未选中。

* **启用提及功能**

   如果启用，则允许注册的社区用户识别其他注册成员（使用名、姓、用户名），并使用通用@user-name法标记他们。 标记用户会收到有关其提及次数的通知。

* **最大提及次数**

   限制帖子中允许的最大提及次数。 默认值为10。

* **UI 提及模式**

   指定允许的模式字符串以标记帖子中注册用户(@mention)。 例如~{{familyName}}{{givenName}}。

* **允许主题回复**

   如果选中此项，则允许对已发布的评论进行回复。 默认为未选中。

#### “用户审核”选项卡{#user-moderation-tab}

在&#x200B;**用户审核**&#x200B;选项卡下，配置评论的审核（如果允许评论）：

* **预审**

   如果选中此项，则必须批准注释，然后注释才会显示在发布网站上。 默认为未选中。

* **删除评论**

   如果选中，则发布评论的访客将能够删除该评论。 默认选中。

* **拒绝评论**

   如果选中，则允许受信任的成员审核者拒绝评论。 默认为未选中。

* **关闭/重新打开评论**

   如果选中，则允许受信任的成员审核者关闭并重新打开注释。 默认为未选中。

* **标记评论**

   如果选中此选项，则允许访客将评论标记为不适当。 默认为未选中。

* **标记原因列表**

   如果选中，则允许访客从下拉列表中选择将评论标记为不适当的原因。 默认为未选中。

* **自定义标记原因**

   如果选中，则允许访客输入自己将评论标记为不适当的原因。 默认为未选中。

* **审核阈值**

   输入在通知审核者之前，访客必须标记评论的次数。 默认值为一次(**1**)。

* **标记限制**

   输入在注释在公共视图中隐藏之前必须标记的次数。 此数字必须大于或等于&#x200B;**审核阈值**。 默认值为5。

### 排序设置选项卡{#sort-settings-tab}

排序方式

设置为默认

### 附加信息 {#additional-information}

有关更多信息，请参阅面向开发人员的[File Library Essentials](/help/communities/essentials-file-library.md)页面。

有关审核已发布的主题和评论，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记已发布的主题和评论，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。
