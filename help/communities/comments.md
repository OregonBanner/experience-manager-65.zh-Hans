---
title: 使用注释
seo-title: 使用注释
description: 注释功能允许登录网站访客共享其意见和知识
seo-description: 注释功能允许登录网站访客共享其意见和知识
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 6be0aa7c3f6b21ad26221289a6cca2b4615ed3f4
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 4%

---


# 使用注释 {#using-comments}

## 简介 {#introduction}

注释功能用于允许登录网站访客（成员）分享他们对网站内容的意见和知识。 此功能通常已在其他功能中提供，但可以添加到任何网站。

文档描述：

* 添加 `Comments` 到页面。
* 组件的配置 `Comments` 设置。

>[!NOTE]
>
>不支持匿名发布评论。 站点访客必须注册（成为会员）并登录才能参加。


### 向页面添加注释 {#adding-comments-to-a-page}

要在创作模 `Comments` 式下将组件添加到页面，请使用组件浏览器来查找

* `Communities / Comments`

并将其拖动到页面上的位置，如相对于要用户评论的功能的位置，或仅在页面底部。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包 [含所需的客户端库](/help/communities/essentials-comments.md#essentials-for-client-side) ，组件的显示方式 `Comments` 为此。

![注释——组件](assets/comments-component.png)

>[!NOTE]
>
>页面上 `Comments` 只能存在一个组件。 请注意，一些社区功能已经包含评论，如博客、日历、论坛、问题与解答和评论。


### 配置注释 {#configuring-comments}

选择要访问的 `Comments` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![配置图标](assets/configure.png)

![注释设置](assets/commentssettings.png)

#### “注释”选项卡 {#comments-tab}

在“注 **释** ”选项卡下，指定访客如何输入注释。

* **允许回复**

   如果选中，允许成员回复现有注释。 “默认”(Default)为取消选择。

* **每页的评论数**

   限制每页显示的注释数和显示的回复数。 默认值为10。

* **允许文件上传**

   如果选中此项，则会显示用于上传文件的选项以及文本输入框。 “默认”(Default)为取消选择。

* **最大文件大小**

   仅当选中“允许文件上传”时相关。 此值限制已上载文件的大小。 默认限制为10 MB。

* **最大消息长度**

   可输入到文本框中的最大字符数。 默认为4096个字符。

* **允许的文件类型**

   仅当选中“允许文件上传”时相关。 带有“点”分隔符的以逗号分隔的文件扩展名列表。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **富文本编辑器**

   如果选中，则输入带有标记的注释。 “默认”(Default)为取消选择。

* **允许投票**

   如果选中，则将显示“向上或向下投票”选项和文本输入框。 “默认”(Default)为取消选择。

* **允许关注**

   如果选中，则允许成员关注注释。 “默认”(Default)为取消选择。

* **显示徽章**

   如果选中，则允许显示已获奖和已获奖的徽章。 “默认”(Default)为取消选择。

#### “用户审核”选项卡 {#user-moderation-tab}

在“用户 **审核** ”选项卡下，指定如何管理已发布的注释。 有关详细信息，请参 [阅调节用户生成的内容](/help/communities/moderate-ugc.md)。

* **预审**

   如果选中此项，则注释必须经过批准，才能显示在发布站点上。 “默认”(Default)为取消选择。

* **删除评论**

   如果选中，则向发布评论的成员提供删除评论的功能。 “默认”(Default)为取消选择。

* **拒绝评论**

   如果选中，则允许版主拒绝注释。 “默认”(Default)为取消选择。

* **关闭／重新打开注释**

   如果选中，允许版主关闭并重新打开注释。 “默认”(Default)为取消选择。

* **标记注释**

   如果选中，允许成员将注释标记为不合适。 “默认”(Default)为取消选择。

* **标志原因列表**

   如果选中，允许成员从下拉列表中选择其标记评论的理由不恰当。 “默认”(Default)为取消选择。

* **自定义标志原因**

   如果选中，允许成员输入自己将评论标记为不合适的原因。 “默认”(Default)为取消选择。

* **审核阈值**

   输入成员在通知版主之前必须标记评论的次数。 默认值为一次(1)。

* **标记限制**

   输入评论在隐藏之前必须标出的次数，使其不受公共视图。 此数字必须大于或等于仲裁 **阈值**。 默认值为5。

#### “排序设置”选项卡 {#sort-settings-tab}

在“排 **序设置** ”选项卡下，指定显示已发布注释时的排序方式。

* **排序字段**

   下拉以选择其中 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`一个或 `Most Liked`。

* **排序顺序**

   下拉以选择其中一个 `Ascending` 或 `Descending`。

### 更改为自定义注释类型 {#changing-to-a-custom-comment-type}

通过更改注释资源类型，注释系统不再使用默认值生成注释实例，而是生成由开发人员自定义（扩展）的实例。

确定自定义资源类型后，进入 [设计模式](/help/sites-authoring/default-components-designmode.md) ,多次单击放 `Comments` 置的组件以打开带有额外选项卡的对话框。

在“资 **源类型** ”选项卡下，为组件的新实例指定自定义resourceType `Comments or Voting` :

![资源类型](assets/resource-type.png)

* **评论资源类型**

   导航到/apps中扩展组件( `comment` 单个注释)的resourceType。 例如，`/apps/social/commons/components/hbs/comments/comment`

   此资源标识当访客发布评论时创建的UGC的resourceType。

* **投票资源类型**

   导航到/apps中扩展组 `voting` 件的resourceType。 例如，`/apps/social/components/hbs/voting`

   此资源标识在访客投票时创建的UGC的资源类型。

* **注释系统资源类型**

   导航到/apps中扩展组 `comments`件（注释系统）的resourceType。 除非页面模板在基础脚 [本中动](/help/communities/scf.md#add-or-include-a-communities-component) 态地包含评论系统，而不是作为资源（评论节点）添加到页面，否则将保留为空。 阅读有关{{include}}帮 [助程序的信息，了解更多](/help/communities/handlebars-helpers.md#include)。

### 站点访客体验 {#site-visitor-experience}

#### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审查方或管理员权限时，他们可以执行组件配置所允许的审核任务，而不管评论的创作者是谁。

#### 成员 {#members}

站点访客登录后，根据配置，可能会

* 发布新评论
* 编辑自己的注释
* 删除自己的注释
* 标记其他人的注释

#### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的注释，翻译这些注释（如果受支持），但不能添加注释或标记其他人的注释。

### 附加信息 {#additional-information}

有关详细信息，请参阅“注 [释要件](/help/communities/essentials-comments.md) ”页面。

有关审核已发布的注释，请参 [阅审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关已发布注释的翻译，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md)。
