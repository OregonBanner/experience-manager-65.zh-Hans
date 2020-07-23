---
title: 构思功能
seo-title: 构思功能
description: 添加和配置构思功能
seo-description: 添加和配置构思功能
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
translation-type: tm+mt
source-git-commit: f62fb1eb760ddd7baee9ba5a631ff4b921e2d08b
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 9%

---


# 构思功能 {#ideation-feature}

## 简介 {#introduction}

构思功能为发布环境中的登录站点访客（社区成员）提供了一个区域，用于：

* 创建想法并与社区分享。
* 视图和评论想法。
* 遵循一个想法。
* 投一票。

文档的本节介绍：

* 将构思功能添加到AEM站点。
* 标识组件的配置设置。

### Adding a Ideation to a Page {#adding-a-ideation-to-a-page}

要在创作模 `Ideation` 式下将组件添加到页面，请使用组件浏览器来查找

* `Communities / Ideation`

并将其拖动到应显示构思的页面上。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包 [含所需的客户端库](/help/communities/ideation.md#essentials-for-client-side) ，组件的显示 `Ideation` 方式如下：

![构思](assets/ideation.png)

### 配置构思 {#configuring-an-ideation}

选择要访问的 `Ideation` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![configure-new](assets/configure-new.png)

![视频设置](assets/ideation-settings.png)

#### “设置”选项卡 {#settings-tab}

在“设 **[!UICONTROL 置]** ”选项卡下，指定构思和注释的设置：

* **允许附加缩略图**
* **附加缩略图时的大小上限**
* **缩略图的最小图像大小**
* **缩略图大小最大值**
* **允许拥有权限的成员**
* **允许的拥有权限的成员**
* **在作者编辑模式下阻止“用户生成内容”**
* **构思标题**

* 构思的显示标题。 Default is `Ideation`.
* **构思描述**

   要显示为构思子标题的说明。 默认为无说明。

* **每页主题数**

   定义每页显示的想法／帖子数。 默认值为10。

* **已审核**

   如果选中此项，则发布创意和评论必须获得批准，然后才能在发布站点上显示。 默认为未选中。

* **关闭**

   如果选中此选项，则构思论坛将不会显示新想法和新注释。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以输入带有标记的想法和注释。 默认为未选中。

* **允许标记**

   如果选中此项，则允许成员向其帖子中添加标记标签(请参 **[!UICONTROL 阅标记字段]** 选项卡)。 默认为未选中。

* **允许文件上传**

   如果选中，则允许将文件附件添加到构思或注释中。 默认为未选中。

* **最大文件大小**

   仅在选中时 `Allow File Uploads` 相关。 此字段将限制已上载文件的大小（以字节为单位）。 默认值为104857600(10 Mb)。

* **允许的文件类型**

   仅在选中时 `Allow File Uploads` 相关。 以逗号分隔的文件扩展名列表，以“点”分隔。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **附加图像文件最大大小**

   仅当选中“允许文件上传”时相关。 上传的图像文件可能具有的最大字节数。 默认为2097152(2 Mb)。

* **允许回复**

   如果选中，则允许回复发布到构思的注释。 默认为未选中。

* **允许投票**

   如果选中，允许对某个想法的注释进行投票。 默认为未选中。

* **允许用户删除评论和主题**

   如果选中此项，则允许成员删除其发布的评论和想法。 默认为未选中。

* **允许关注**

   如果选中此项，则为创意帖子添加以下功能，允许成员 [收到](/help/communities/notifications.md) 新帖子的通知。 默认为未选中。

* **允许电子邮件订阅**

   如果选中此项，则允许成员通过电子邮件(订阅)通知[新帖](/help/communities/subscriptions.md)子。 需要 `Allow Following` 检查并配置电 [子邮件](/help/communities/email.md)。 默认为未选中。

* **允许投票**

   如果选中，允许对某个想法的注释进行投票。 默认为未选中。

* **显示徽章**

   如果选中，则用会员的 [想法](/help/communities/implementing-scoring.md) ，显示已获得和分配的徽章。 默认为未选中。

* **列表页面上不收到回复**

* **允许专题内容**

   如果选中，则可以将该想法标识为特色 [内容](/help/communities/featured.md)。 默认为未选中。

* **启用提及功能**
* **最大提及次数**
* **UI 提及模式**

#### “用户审核”选项卡 {#user-moderation-tab}

在“用 **[!UICONTROL 户协调]** ”选项卡下，指定如何管理已发布的想法和评论（用户生成的内容）。 有关详细信息，请参 [阅调节用户生成的内容](/help/communities/moderate-ugc.md)。

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

在“标 **[!UICONTROL 记”字段]** (Tag field)选项卡下 **[!UICONTROL ，根据所选的命名空间，在“设置”(Settings)选项卡下允许的情况下，]** 可以应用的标记会受到限制。

* **允许的命名空间**

   如果在“设 `Allow Tagging` 置”选项卡下选中， **[!UICONTROL 则相关]** 。 可应用的标记仅限于所选命名空间类别内的标记。 命名空间的列表包括“标准标记”(默认命名空间)和“包括所有标记”。 默认值为“无”(none checked)，这意味着允许所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 值-1 **表示** 无限制。 默认值为0。

#### “排序设置”选项卡 {#sort-settings-tab}

在“排 **[!UICONTROL 序设置]** ”选项卡下，指定显示已发布注释时的排序方式。

* **排序方式**

   检查所有允许的排序选择： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Default is `Newest, Oldest, Last Updated`.

* **设置为默认**

   下拉以选择一个选中的排序选项作为默认值显示。 Default is `Newest`.

* **选择分析排序的时间选项**

   下拉以选择其中一个 `All, Last 24 Hours, Last 7 Days, Last 30 Days`。 Default is `All`.

## 站点访客体验 {#site-visitor-experience}

### 创建构思 {#creating-idea}

与所有社区功能一样，如果未登录，站点访客只能阅读想法并视图他人的意见（通过评论和投票／喜欢）。

登录后，会员可能会创建新想法。

![create-new-idea](assets/create-new-idea.png)

在提交构思之前，成员可以保存草稿。

通过选择按 `Save as Draft` 钮，将保存草稿。

![保存构思](assets/save-idea.png)

在选项卡中查看保存的 `My Drafts` 草稿时， `Read More` 选择以重新进入编辑模式：

![编辑构思](assets/edit-idea.png)

#### 提供反馈 {#providing-feedback}

构思发布后，其他成员可以登录，打开构思() `Read More`并像该构思一样，从而增加投票数并发表评论。

![反馈](assets/feedback-idea.png)

### 附加信息 {#additional-information}

有关详细信息，请参阅适 [用于开发人](/help/communities/ideation.md) 员的Idetation Essentials页。

有关审核已发布的主题和评论，请参 [阅审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记已发布的主题和评论，请参 [阅标记用户生成的内容](/help/communities/tag-ugc.md)。
