---
title: 使用注释
seo-title: 使用注释
description: 通过“注释”功能，登录网站的访问者可以共享他们的意见和知识
seo-description: 通过“注释”功能，登录网站的访问者可以共享他们的意见和知识
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# 使用注释 {#using-comments}

## 简介 {#introduction}

注释功能用于允许登录网站的访客（成员）共享他们对网站内容的意见和知识。 此功能通常已在其他功能中提供，但可以添加到任何网站。

文档描述：

* 添加 `Comments`到页面。
* 组件的配置 `Comments`设置。

>[!NOTE]
>
>不支持匿名发布评论。 站点访问者必须注册（成为会员）并登录才能参加。

### 向页面添加注释 {#adding-comments-to-a-page}

要在创作模 `Comments`式下将组件添加到页面，请使用组件浏览器查找

* `Communities / Comments`

并将其拖动到页面上的位置，如相对于用户可评论的功能的位置，或仅在页面底部。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包含 [所需的客户端库时](/help/communities/essentials-comments.md#essentials-for-client-side) ，组件的显示方式 `Comments`就是这样。

![chlimage_1-143](assets/chlimage_1-143.png)

>[!NOTE]
>
>一个页 `Comments`面上只能存在一个组件。 请注意，一些Communities功能已经包括评论，如博客、日历、论坛、问题与答案和评论。

### 配置注释 {#configuring-comments}

选择要访问 `Comments` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![配置图标](assets/configure.png)![注释设置](assets/commentssettings.png)

#### “注释”选项卡 {#comments-tab}

在“注 **释** ”选项卡下，指定访客如何输入注释。

* **允许回复**

   如果选中此项，则允许成员回复现有注释。 取消选择默认值。

* **每页的评论数**

   限制每页显示的注释数和显示的回复数。 默认值为10。

* **允许文件上传**

   如果选中此项，则会显示上传文件的选项以及文本输入框。 取消选择默认值。

* **最大文件大小**

   仅在选中“允许文件上传”时相关。 此值限制了上传的文件大小。 默认限制为10 MB。

* **最大消息长度**

   可输入到文本框中的最大字符数。 默认为4096个字符。

* **允许的文件类型**

   仅在选中“允许文件上传”时相关。 带有“点”分隔符的文件名扩展名列表，以逗号分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **富文本编辑器**

   如果选中此项，则输入带有标记的注释。 取消选择默认值。

* **允许投票**

   如果选中此项，则会显示向上或向下投票的选项和文本输入框。 取消选择默认值。

* **允许关注**

   如果选中此项，则允许成员关注评论。 取消选择默认值。

* **显示徽章**

   如果选中此项，则允许显示已获得和已获得奖励的徽章。 取消选择默认值。

#### “用户审核”选项卡 {#user-moderation-tab}

在“用户 **审核** ”选项卡下，指定如何管理已发布的评论。 有关详细信息，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md)。

* **预审**

   如果选中此项，则注释必须经过批准，才能显示在发布站点上。 取消选择默认值。

* **删除评论**

   如果选中此项，则向发布评论的成员提供删除评论的功能。 取消选择默认值。

* **拒绝评论**

   如果选中此项，则允许版主拒绝评论。 取消选择默认值。

* **关闭／重新打开注释**

   如果选中此项，则允许版主关闭并重新打开注释。 取消选择默认值。

* **标记注释**

   如果选中此项，允许成员将注释标记为不合适。 取消选择默认值。

* **标记原因列表**

   如果选中此项，允许成员从下拉列表中选择其标记评论为不合适的理由。 取消选择默认值。

* **自定义标志原因**

   如果选中此项，则允许成员输入自己将评论标记为不合适的原因。 取消选择默认值。

* **协调阈值**

   输入成员在通知版主之前必须标记评论的次数。 默认值是一次(1)。

* **标记限制**

   输入评论在公共视图中隐藏之前必须标记的次数。 此数字必须大于或等于审核 **阈值**。 默认为5。

#### “排序设置”选项卡 {#sort-settings-tab}

在“排 **序设置** ”选项卡下，指定显示已发布注释时的排序方式。

* **排序字段**

   下拉以选择其中 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`一个或 `Most Liked`。

* **排序顺序**

   下拉以选择或 `Ascending` 之一 `Descending`。

### 更改为自定义注释类型 {#changing-to-a-custom-comment-type}

通过更改“注释资源类型”，注释系统不再使用默认值生成注释实例，而是生成由开发人员自定义（扩展）的实例。

确定自定义资源类型后，进入 [设计模式](/help/sites-authoring/default-components-designmode.md) ，双击放置的组件以打开 `Comments` 带有额外选项卡的对话框。

在“资 **源类型** ”选项卡下，为组件的新实例指定自定义resourceType `Comments or Voting`:

![chlimage_1-144](assets/chlimage_1-144.png)

* **评论资源类型**

   导航到/apps中扩展组件( `comment`单个注释)的resourceType。 例如，`/apps/social/commons/components/hbs/comments/comment`

   此资源标识访客发布评论时创建的UGC的resourceType。

* **投票资源类型**

   导航到/apps中扩展组件 `voting`的resourceType。 例如，`/apps/social/components/hbs/voting`

   此资源标识访客发布投票时创建的UGC的资源类型。

* **注释系统资源类型**

   导航到/apps中扩展组件( `comments`评论系统)的resourceType。 除非页面模板在基础脚 [本中动态包含](/help/communities/scf.md#add-or-include-a-communities-component) “注释系统”，而不是作为资源（注释节点）添加到页面，否则将留空。 阅读有关 [{{include}}帮助程序的更多信息](/help/communities/handlebars-helpers.md#include)。

### 网站访客体验 {#site-visitor-experience}

#### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审查方或管理员权限时，他们可以执行组件配置所允许的审核任务，而不管评论的创作者是谁。

#### 成员 {#members}

当站点访客登录时，根据配置，他们可能

* 发布新评论
* 编辑他们自己的注释
* 删除自己的注释
* 标记其他人的注释

#### 匿名 {#anonymous}

未登录的站点访问者只能阅读已发布的评论，翻译这些评论（如果支持），但不能添加评论或标记他人的评论。

### 附加信息 {#additional-information}

有关详细信息，请参阅面向开 [发人员的](/help/communities/essentials-comments.md) “注释基本工具”页。

有关审核已发布的注释，请参阅审核 [用户生成的内容](/help/communities/moderate-ugc.md)。

有关已发布注释的翻译，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md)。
