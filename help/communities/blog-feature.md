---
title: 博客功能
seo-title: 博客功能
description: 以日志格式提供社区信息
seo-description: 以日志格式提供社区信息
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 8361f65f52c2a67658ef1b7b7615df149208777b
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 6%

---


# 博客功能 {#blog-feature}

## 简介 {#introduction}

AEM Communities的博客功能已从创作活动转变为在发布环境中发生的真正社区活动。

博客功能支持以日志格式提供社区信息。 博客条目由授权成员（注册、登录用户）在发布环境下创建。

博客功能提供：

* 在发布端创建博客文章和评论
* 富文本编辑
* 内联图像（支持拖放）
* 嵌入式社交网络内容([嵌入支持](/help/communities/blog-developer-basics.md#allowing-rich-media))
* 草稿模式
* 计划发布
* 代表起草(特权 [成员](/help/communities/users.md#privileged-members-group) 可以代表其他社区成员创建内容)
* [博客文章和评论的上下文](/help/communities/moderate-ugc.md) 、批量协调

文档的本节介绍：

* 将博客功能添加到AEM站点
* 博客组件的配置设置

>[!NOTE]
>
>组件 `Journal` 和 `Journal Sidebar` 标题 `Blog` 为和 `Blog Sidebar`。
>
>AEM 6.0及更早版本中的博客功能现已删除。 它基于模板，并且仅允许作者在创作环境中创建内容。


## 将博客组件添加到页面 {#adding-blog-components-to-a-page}

如果希望在创作模式下将博客添加到页面，请使用组件浏览器查找

* `Communities / Blog`
* `Communities / Blog Sidebar`

并将它们拖到应显示博客的页面上。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包 [含所需的客户端库](/help/communities/blog-developer-basics.md#essentials-for-client-side) ，组件的显示 `Blog` 方式如下：

![add-blog-component](assets/add-blog-component.png)

### 配置博客 {#configuring-blog}

选择要访问的 `Blog` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![配置](assets/configure-new.png)

![博客设置](assets/blog-configure.png)

#### “设置”选项卡 {#settings-tab}

在“设 **置** ”选项卡下，指定博客的基本功能：

* **允许附加缩略图**

   如果选中，则会创建附加图像的缩略图。

* **附加缩略图时的大小上限**

   附件缩略图图像的最大大小（以像素为单位）。 默认值为800 x 800。

* **缩略图的最小图像大小**

   用于为内联图像生成缩略图的最小图像大小（以字节为单位）。 默认值为100000字节(100kb)。

* **缩略图大小最大值**

   内联图像的缩略图最大大小（以像素为单位）。 默认值为800 x 800。

* **允许拥有权限的成员**

   如果选中此项，则仅允许特权成员创建内容。

* **允许的拥有权限的成员**

   添加允许创建内容的特权成员。

* **在作者编辑模式下阻止“用户生成内容”**

   如果启用，则在创作模式下编辑时阻止用户生成的内容。

* **日志标题**

   要在页面上显示的博客标题。

>[!NOTE]
>
>日志标题用于自动创建博客的URL。
>您在此指定的日志标题中最多使用50个字符（除5个字符外，还有5个字符可用于唯一性）来创建博客的URL。


* **日志描述**

   博客描述。

* **每页主题数**

   定义每页显示的博客条目／评论数。 默认为 10。

* **已审核**

   如果选中此项，则必须批准发布博客条目和评论，然后才能在发布的网站上显示这些条目和评论。 默认为未选中。

* **关闭**

   如果选中，则博客将关闭到新的博客条目和评论。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以使用标记输入博客条目和注释。 选中默认值。

* **允许标记**

   如果选中此项，则允许成员向其帖子中添加标记标签(请参 **阅标记字段** 选项卡)。 默认为未选中。

* **允许文件上传**

   如果选中，则允许将文件附件添加到博客条目或评论。 默认为未选中。

* **最大文件大小**

   仅在选中时 `Allow File Uploads` 相关。 此字段将限制已上载文件的大小（以字节为单位）。 默认值为104857600(10 Mb)。

* **允许的文件类型**

   仅在选中时 `Allow File Uploads` 相关。 以逗号分隔的文件扩展名列表，以“点”分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **附加图像文件最大大小**

   仅当选中“允许文件上传”时相关。 上传的图像文件可能具有的最大字节数。 默认为2097152(2 Mb)。

* **允许回复**

   如果选中，则允许回复发布到博客条目的评论。 默认为未选中。

* **允许投票**

   如果选中此项，则在博客条目中包含投票功能。 默认为未选中。

* **允许用户删除评论和主题**

   如果选中此项，则允许成员删除他们发布的评论和博客条目。 默认为未选中。

* **允许关注**

   如果选中此项，则为博客文章添加以下功能，允许成员 [收到](/help/communities/notifications.md) 新帖子的通知。 默认为未选中。

* **允许电子邮件订阅**

   如果选中此项，则允许成员通过电子邮件(订阅)通知[新帖](/help/communities/subscriptions.md)子。 需要 `Allow Following` 检查并配置电 [子邮件](/help/communities/email.md)。 默认为未选中。

* **显示徽章**

   如果选中，则使用会员的博 [客条目](/help/communities/implementing-scoring.md) ，显示已获得和分配的徽章。 默认为未选中。

* **不在列表页上获取回复**

* **允许专题内容**

   如果选中，则可以将该想法标识为特色 [内容](/help/communities/featured.md)。 默认为未选中。

* **启用提及功能**

   如果启用，允许注册社区用户识别其他注册成员（使用名、姓、用户名），并使用通用的@user-name语法标记这些成员。 标记用户会收到有关其提及次数的通知。

* **最大提及次数**

   限制帖子中允许的最大提及次数。 默认值为10。

* **UI 提及模式**

   在帖子中为注册用户标记（@提及）指定已允许的模式字符串。 例如~{{familyName}}{{givenName}}。

#### “用户审核”选项卡 {#user-moderation-tab}

在“用户 **审核** ”选项卡下，指定审核设置：

* **拒绝帖子**

   如果选中，则允许受信任的成员审核者拒绝帖子并阻止帖子显示在公共论坛中。 默认为未选中。

* **关闭／重新打开主题**

   如果选中，受信任的成员版主可以关闭主题以进一步编辑和评论，也可以重新打开主题。 默认为未选中。

* **旗标帖子**

   如果选中，允许成员将其他人的主题或注释标记为不合适。 默认为未选中。

* **标志原因列表**

   如果选中，允许成员从下拉式列表中选择其标记主题或评论为不合适的理由。 默认为未选中。

* **自定义标志原因**

   如果选中，允许成员输入其自己将主题或评论标记为不合适的原因。 默认为未选中。

* **审核阈值**

   输入在通知版主之前必须由成员标记主题或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入主题或评论在隐藏之前必须标出的次数，以免公开视图。 如果设置为-1，则标记的主题或评论从不隐藏于公共视图。 否则，此数字必须大于或等于仲裁阈值。 默认值为5。

#### 标记字段选项卡 {#tag-field-tab}

在“标记 **字段** ”选项卡下，指定在“设置”选项卡上选中“允 **许标记** ”时可应用的 **标记** :

* **允许的命名空间**

   如果在“设 `Allow Tagging` 置”选项卡下选中， **则相关** 。 可应用的标记仅限于所选命名空间类别内的标记。 命名空间的列表包括“标准标记”(默认命名空间)和“包括所有标记”。 默认值为“无”(none checked)，这意味着允许所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 值-1表示没有限制。 默认值为0。

### 配置博客提要栏 {#configuring-blog-sidebar}

多次单击组件 `Blog Sidebar` 时，将打开一个编辑对话框。

在“日志 **提要栏设置** ”选项卡下，指定存档的日期格式以及要在提要栏中显示的条目类型：

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **日期格式**

   用于显示博客条目存档的格式。 格式使用遵循Java约定的占位符。

   * yyyy:全年，比如2015年
   * yy:短年，比如15
   * MMMMMM:整月，如6月
   * 嗯：短月，如6月
   * MM:月号，如06

   默认值为“yyyy MMMM”，例如显示“2015年6月”

* **视图类型**

   标题和要在提要栏中显示的博客条目类型。 选择是

   * 作者
   * 类别
   * 归档

* **Blopg组件路径**

   *（可选）* 要从中列出博客文章的博客资源的位置。 如果留空，将使用同一页 `social/journal/components/hbs/journal` 面上显示的resourceType组件。

   * 例如，`/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **建议限制**

   要显示的博客文章数。 值-1表示无限制。 默认值为-1。

## 站点访客体验 {#site-visitor-experience}

在发布环境中，博客功能将按创建的降序显示最新的博客文章，后跟较旧的博客文章。 博客提要栏允许站点访客应用过滤器来限制所显示博客文章的选择。

博客文章后跟一个用于发表评论或视图评论的链接。

选择博客文章后，将显示博客文章和评论（如果启用）。

其他功能取决于站点访客是版主、管理员、社区成员、特权成员还是匿名。

### 使用文章 {#working-with-articles}

创建新博客文章时，可以选择：

1. 立即发布
1. 发布草稿
1. 按预定日期和时间发布

博客文章将显示在相应的选项卡（已发布、草稿或已计划）下，以供能够在发布时进行创作的成员使用。

#### 版主和管理员 {#moderators-and-administrators}

当登录用户具有版主或管理员权限时，他们能够对发布到博 [客的所有博客文章](/help/communities/moderate-ugc.md) 和评论执行审核任务（如组件的配置所允许）。

![版主页](assets/moderator-homepage.png)

#### 成员 {#members}

当登录用户是社区成员或特 [权成员](/help/communities/users.md#privileged-members-group) （取决于配置）时，他们可以选择 `New Article` 创建和发布新的博客文章。

具体而言，他们可以：

* 创建新博客文章
* 代表其他成员发布新的博客文章
* 将评论发布到博客文章
* 编辑自己的博客文章或评论
* 删除自己的博客文章或评论
* 标记他人的博客文章或评论

![会员主页](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### 匿名 {#anonymous}

未登录的网站访客只能阅读张贴的博客文章和评论，如果支持，可翻译这些文章和评论，但不得添加博客文章或评论，也不得标记他人的文章或评论。

![匿名用户视图](assets/anonymous-user-view.png)

## 附加信息 {#additional-information}

有关详细信息，请参阅开发人 [员的“Blog](/help/communities/blog-developer-basics.md) Essentials”页面。

有关审核博客条目和评论，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记博客条目和注释，请参 [阅标记用户生成的内容](/help/communities/tag-ugc.md)。

有关博客条目和注释的翻译，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md)。
