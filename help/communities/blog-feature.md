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
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 6%

---

# 博客功能{#blog-feature}

## 简介 {#introduction}

AEM Communities的博客功能已从创作活动转变为在发布环境中进行的真正社区活动。

博客功能支持以日志格式提供社区信息。 博客条目由授权成员（已注册、已登录的用户）在发布环境中进行。

博客功能提供：

* 在发布端创建博客文章和评论
* 富文本编辑
* 内联图像（支持拖放）
* 嵌入式社交网络内容([oEmbed support](/help/communities/blog-developer-basics.md#allowing-rich-media))
* 草稿模式
* 计划发布
* 代表撰写（[特权成员](/help/communities/users.md#privileged-members-group)可以代表其他社区成员创建内容）
* [对博客文章和评论](/help/communities/moderate-ugc.md) 进行上下文和批量审核

文档的此部分描述：

* 将博客功能添加到AEM网站
* 博客组件的配置设置

>[!NOTE]
>
>组件`Journal`和`Journal Sidebar`的标题分别为`Blog`和`Blog Sidebar`。
>
>现在，已删除AEM 6.0及更早版本中的博客功能。 它基于模板，只允许作者在创作环境中创建内容。

## 将博客组件添加到页面{#adding-blog-components-to-a-page}

如果需要在创作模式下将博客添加到页面，请使用组件浏览器找到

* `Communities / Blog`
* `Communities / Blog Sidebar`

并将它们拖动到应显示博客的页面上。

有关必要信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/blog-developer-basics.md#essentials-for-client-side)时，将显示`Blog`组件：

![add-blog-component](assets/add-blog-component.png)

### 配置博客{#configuring-blog}

选择要访问的已放置的`Blog`组件，然后选择`Configure`图标以打开编辑对话框。

![配置](assets/configure-new.png)

![博客设置](assets/blog-configure.png)

#### “设置”选项卡{#settings-tab}

在&#x200B;**设置**&#x200B;选项卡下，指定博客的基本功能：

* **允许附加缩略图**

   如果选中此选项，则会创建附加图像的缩略图。

* **附加缩略图时的大小上限**

   附件缩略图图像的最大大小（以像素为单位）。 默认值为800 x 800。

* **缩略图的最小图像大小**

   用于为内联图像生成缩略图的图像的最小大小（以字节为单位）。 默认值为100000字节(100kb)。

* **缩略图大小最大值**

   内联图像的缩略图最大大小（以像素为单位）。 默认值为800 x 800。

* **允许拥有权限的成员**

   如果选中此项，则仅允许特权成员创建内容。

* **允许的拥有权限的成员**

   添加允许创建内容的特权成员。

* **在作者编辑模式下阻止“用户生成内容”**

   如果启用，则在创作模式下编辑时会阻止用户生成的内容。

* **日志标题**

   要在页面上显示的博客标题。

>[!NOTE]
>
>日志标题用于自动为博客创建URL。
>
>您在此处指定的日志标题中，最多使用50个字符（其余5个字符的唯一性）来创建博客的URL。

* **日志描述**

   博客描述。

* **每页主题数**

   定义每页显示的博客条目/评论数。 默认为 10。

* **已审核**

   如果选中此项，则必须批准发布博客条目和评论，然后才能在已发布的网站上显示这些条目和评论。 默认为未选中。

* **关闭**

   如果选中，则博客将不会显示新的博客条目和评论。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以使用标记输入博客条目和评论。 默认选中。

* **允许标记**

   如果选中此选项，则允许成员向其帖子中添加标签（请参阅&#x200B;**标签字段**&#x200B;选项卡）。 默认为未选中。

* **允许文件上传**

   如果选中此项，则允许将文件附件添加到博客条目或评论中。 默认为未选中。

* **最大文件大小**

   仅当选中`Allow File Uploads`时相关。 此字段将限制已上传文件的大小（以字节为单位）。 默认为104857600(10 Mb)。

* **允许的文件类型**

   仅当选中`Allow File Uploads`时相关。 以逗号分隔的文件扩展名列表，其中带有“圆点”分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则将不允许上载未指定的文件类型。 默认值未指定，以便允许使用所有文件类型。

* **附加图像文件最大大小**

   仅当选中允许文件上传时相关。 上传的图像文件可能具有的最大字节数。 默认为2097152(2 Mb)。

* **允许回复**

   如果选中此项，则允许对发布到博客条目的评论做出回复。 默认为未选中。

* **允许投票**

   如果选中此项，则在博客条目中包含投票功能。 默认为未选中。

* **允许用户删除评论和主题**

   如果选中，则允许成员删除他们发布的评论和博客条目。 默认为未选中。

* **允许关注**

   如果选中此项，请为博客文章添加以下功能，该功能允许成员在新帖子中[收到通知](/help/communities/notifications.md)。 默认为未选中。

* **允许电子邮件订阅**

   如果选中此项，则允许成员通过电子邮件([subscription](/help/communities/subscriptions.md))接收新帖子的通知。 需要检查`Allow Following`并[电子邮件配置](/help/communities/email.md)。 默认为未选中。

* **显示徽章**

   如果选中此项，则使用成员的博客条目显示已获得的和已分配的[徽章](/help/communities/implementing-scoring.md)。 默认为未选中。

* **不在列表页上获取回复**

* **允许专题内容**

   如果选中，则该构思能够被标识为[特色内容](/help/communities/featured.md)。 默认为未选中。

* **启用提及功能**

   如果启用，则允许注册的社区用户识别其他注册成员（使用名、姓、用户名），并使用通用@user-name法标记他们。 标记用户会收到有关其提及次数的通知。

* **最大提及次数**

   限制帖子中允许的最大提及次数。 默认值为10。

* **UI 提及模式**

   指定允许的模式字符串以标记帖子中注册用户(@mention)。 例如~{{familyName}}{{givenName}}。

#### “用户审核”选项卡{#user-moderation-tab}

在&#x200B;**用户审核**&#x200B;选项卡下，指定审核设置：

* **拒绝帖子**

   如果选中，则允许受信任的成员审核者拒绝帖子并阻止帖子出现在公共论坛中。 默认为未选中。

* **关闭/重新打开主题**

   如果选中，受信任的成员审核者可以关闭主题以进一步编辑和评论，也可以重新打开主题。 默认为未选中。

* **标记帖子**

   如果选中，则允许成员将他人的主题或评论标记为不适当。 默认为未选中。

* **标记原因列表**

   如果选中，允许成员从下拉列表中选择其标记主题或评论为不适当的原因。 默认为未选中。

* **自定义标记原因**

   如果选中，则允许成员输入自己将主题或评论标记为不适当的原因。 默认为未选中。

* **审核阈值**

   输入在通知审核者之前必须由成员标记主题或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入在主题或评论在公共视图中隐藏之前必须标记的次数。 如果设置为–1，则标记的主题或评论永远不会在公共视图中隐藏。 否则，此数字必须大于或等于审核阈值。 默认值为5。

#### 标记字段选项卡{#tag-field-tab}

在&#x200B;**标记字段**&#x200B;选项卡下，指定在&#x200B;**设置**&#x200B;选项卡上选中&#x200B;**允许标记**&#x200B;时可应用的标记：

* **允许的命名空间**

   如果在&#x200B;**设置**&#x200B;选项卡下选中`Allow Tagging`，则相关。 可应用的标记仅限于所选命名空间类别中的标记。 命名空间列表包括“标准标记”（默认命名空间）以及“包括所有标记”。 默认为“未选中”，这表示允许使用所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 值为–1表示没有限制。 默认值为0。

### 配置博客侧栏{#configuring-blog-sidebar}

双击`Blog Sidebar`组件时，将打开一个编辑对话框。

在&#x200B;**日志侧栏设置**&#x200B;选项卡下，指定存档的日期格式以及要在侧栏中显示的条目类型：

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **日期格式**

   用于显示博客条目存档的格式。 格式使用遵循Java约定的占位符。

   * yyyy :全年，比如’2015年”
   * yy :短年，就像’15年”
   * MMMMMM :整个月，象6月
   * MMM :短月份，就像6月
   * MM :月数，如06

   默认值为“yyyy MMMM”，例如，将显示“2015年6月”

* **视图类型**

   要在侧栏中显示的博客条目的标题和类型。 选择是

   * 作者
   * 类别
   * 归档

* **Blopg组件路径**

   *（可选）* 要从中列出博客文章的博客资源的位置。如果留为空白，将使用在同一页面上显示的resourceType `social/journal/components/hbs/journal`组件。

   * 例如，`/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **建议限制**

   要显示的博客文章数。 值为–1表示无限制。 默认值为–1。

## 网站访客体验{#site-visitor-experience}

在发布环境中，博客功能将以降序方式显示最新的博客文章，随后将显示旧的博客文章。 博客侧栏允许网站访客应用过滤器以限制所显示的博客文章的选择。

在博客文章后面添加一个用于发布或查看评论的链接。

选择博客文章后，将显示博客文章和评论（如果启用）。

其他功能取决于网站访客是审核者、管理员、社区成员、特权成员还是匿名。

### 使用文章{#working-with-articles}

创建新博客文章时，可以选择：

1. 立即发布
1. 发布草稿
1. 在计划的日期和时间发布

博客文章将显示在相应的选项卡（已发布、草稿或已计划）下方，以供能够在发布时进行创作的成员使用。

#### 审核者和管理员{#moderators-and-administrators}

当登录用户具有审核者或管理员权限时，他们能够对发布到博客的所有博客文章和评论执行[审核任务](/help/communities/moderate-ugc.md)（组件配置允许）。

![审查方主页](assets/moderator-homepage.png)

#### 成员 {#members}

当登录用户是社区成员或[特权成员](/help/communities/users.md#privileged-members-group)（取决于配置）时，他们能够选择`New Article`以创建和发布新的博客文章。

具体而言，他们可以：

* 创建新的博客文章
* 代表其他成员发布新的博客文章
* 将评论发布到博客文章
* 编辑自己的博客文章或评论
* 删除自己的博客文章或评论
* 标记他人的博客文章或评论

![member-homepage](assets/member-homepage.png)

![创建博客](assets/create-blog.png)

#### 匿名 {#anonymous}

未登录的网站访客只能阅读发布的博客文章和评论，如果支持，可以翻译，但不得添加博客文章或评论，也不得标记他人的文章或评论。

![anonymous-user-view](assets/anonymous-user-view.png)

## 附加信息 {#additional-information}

有关更多信息，请参阅[Blog Essentials](/help/communities/blog-developer-basics.md)页面，供开发人员使用。

有关审核博客条目和评论的信息，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记博客条目和评论，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。

有关博客条目和评论的翻译，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。
