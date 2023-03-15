---
title: 使用注释
seo-title: Using Comments
description: “评论”功能允许登录的网站访客分享其意见和知识
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 4%

---

# 使用注释 {#using-comments}

## 简介 {#introduction}

“评论”功能用于允许已登录的网站访客（成员）分享他们关于网站内容的意见和知识。 此功能通常已存在于其他功能中，但可以添加到任何网站。

本文档描述了：

* 添加 `Comments` 到页面。
* 的配置设置 `Comments` 组件。

>[!NOTE]
>
>不支持匿名发布评论。 网站访客必须注册（成为会员）并登录才能参与。

### 向页面添加评论 {#adding-comments-to-a-page}

添加 `Comments` 组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Comments`

并将其拖动到页面上的适当位置，例如相对于供用户评论的功能的一个位置，或仅拖动到页面底部。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

当 [所需的客户端库](/help/communities/essentials-comments.md#essentials-for-client-side) 包括，这就是 `Comments` 组件出现。

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>只有一个 `Comments` 组件可能存在于页面上。 请注意，多个Communities功能已经包含评论，例如博客、日历、论坛、问题与解答以及评论。

### 配置评论 {#configuring-comments}

选择已放置的 `Comments` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![配置图标](assets/configure.png)

![注释设置](assets/commentssettings.png)

#### “评论”选项卡 {#comments-tab}

在 **评论** 选项卡，指定访客输入评论的方式。

* **允许回复**

   如果选中，则允许成员回复现有注释。 默认已取消选中。

* **每页的评论数**

   限制每页显示的评论数和显示的回复数。 默认值为10。

* **允许文件上传**

   如果选中，上载文件的选项将显示为文本输入框。 默认已取消选中。

* **最大文件大小**

   仅在选中允许文件上传时才相关。 此值限制上传的文件大小。 默认限制为10 MB。

* **最大消息长度**

   文本框中可以输入的最大字符数。 默认值为4096个字符。

* **允许的文件类型**

   仅在选中允许文件上传时才相关。 以“点”分隔符分隔的文件名扩展名列表。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许未指定的文件类型。 缺省值为none以便允许所有文件类型。

* **富文本编辑器**

   如果选中，则输入注释时带有标记。 默认已取消选中。

* **允许投票**

   如果选中，则会显示文本输入框中的向上或向下投票选项。 默认已取消选中。

* **允许关注**

   如果选中，则允许成员关注注释。 默认已取消选中。

* **显示徽章**

   如果选中，则允许显示已获得和已授予的徽章。 默认已取消选中。

#### “用户审核”选项卡 {#user-moderation-tab}

在 **用户审核** 选项卡，指定如何管理已发布的评论。 有关更多信息，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

* **预审**

   如果选中，评论必须先获得批准，然后才能显示在发布网站上。 默认已取消选中。

* **删除评论**

   如果选中，则为发布评论的成员提供删除评论的功能。 默认已取消选中。

* **拒绝评论**

   如果选中，则允许审查方拒绝评论。 默认已取消选中。

* **关闭/重新打开注释**

   如果选中，则允许审查方关闭和重新打开注释。 默认已取消选中。

* **标记注释**

   如果选中，则允许成员将评论标记为不适当。 默认已取消选中。

* **标记原因列表**

   如果选中，则允许成员从下拉列表中选择将评论标记为不适当的原因。 默认已取消选中。

* **自定义标志原因**

   如果选中，则允许成员输入将评论标记为不适当的原因。 默认已取消选中。

* **审核阈值**

   输入在通知版主之前，评论必须由成员标记的次数。 默认值为一次(1)。

* **标记限制**

   输入在将评论从公开视图隐藏之前必须对其标记的次数。 此数字必须大于或等于 **审核阈值**. 默认值为5。

#### “排序设置”选项卡 {#sort-settings-tab}

在 **排序设置** 选项卡，指定在显示时如何对已发布的评论进行排序。

* **排序字段**

   下拉以选择其中一项 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`，或 `Most Liked`.

* **排序顺序**

   下拉以选择其中一项 `Ascending` 或 `Descending`.

### 更改为自定义评论类型 {#changing-to-a-custom-comment-type}

通过更改注释资源类型，注释系统不再使用默认值生成注释的实例，而是生成由开发人员自定义（扩展）的实例。

在已知自定义资源类型后，输入 [设计模式](/help/sites-authoring/default-components-designmode.md) 并双击所放置的 `Comments` 组件打开带有额外选项卡的对话框。

在 **资源类型** 选项卡，为的新实例指定自定义资源类型 `Comments or Voting` 组件：

![resource-type](assets/resource-type.png)

* **评论资源类型**

   导航到扩展的资源类型 `comment` /apps中的组件（单个注释）。 例如，`/apps/social/commons/components/hbs/comments/comment`

   此资源标识访客发表评论时创建的UGC的resourceType。

* **投票资源类型**

   导航到扩展的资源类型 `voting` /apps中的组件 例如，`/apps/social/components/hbs/voting`

   此资源标识访客发表投票时创建的UGC的资源类型。

* **评论系统资源类型**

   导航到扩展的资源类型 `comments`/apps中的组件（注释系统）。 除非页面模板，否则保留为空 [动态包括](/help/communities/scf.md#add-or-include-a-communities-component) 基础脚本中的注释系统，而不是作为资源（注释节点）添加到页面中。 通过阅读有关 [{{include}} 辅助函数](/help/communities/handlebars-helpers.md#include).

### 网站访客体验 {#site-visitor-experience}

#### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审阅人或管理员权限时，他们能够执行组件配置允许的审阅任务，无论评论的作者是谁。

#### 成员 {#members}

当站点访客登录时，根据配置，他们可能

* 发布新评论
* 编辑他们自己的评论
* 删除他们自己的评论
* 标记其他人的评论

#### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的评论，如果支持则进行翻译，但不得添加评论或标记其他人的评论。

### 附加信息 {#additional-information}

欲知更多信息，请访问 [注释要点](/help/communities/essentials-comments.md) 适用于开发人员的页面。

有关审核已发布的评论，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

有关已发布评论的翻译，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md).
