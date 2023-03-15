---
title: 构思特征
seo-title: Ideation Feature
description: 添加和配置构思功能
seo-description: Adding and configuring the Ideation feature
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 9%

---

# 构思特征 {#ideation-feature}

## 简介 {#introduction}

构思功能为发布环境中的登录站点访客（社区成员）提供了一个区域，可用于：

* 提出想法并与社区分享。
* 查看和评论想法。
* 遵循一个想法。
* 投票支持一个想法。

本文档的这一部分描述了：

* 将构思功能添加到AEM站点。
* 构思组件的配置设置。

### 向页面添加构思 {#adding-a-ideation-to-a-page}

添加 `Ideation` 组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Ideation`

并将其拖动到应该显示创意的页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

当 [所需的客户端库](/help/communities/ideation.md#essentials-for-client-side) 包括，这就是 `Ideation` 组件将显示：

![构思](assets/ideation.png)

### 配置构思 {#configuring-an-ideation}

选择已放置的 `Ideation` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

![构思设置](assets/ideation-settings.png)

#### “设置”选项卡 {#settings-tab}

在 **[!UICONTROL 设置]** 选项卡，指定想法和评论的设置：

* **允许附加缩略图**
* **附加缩略图时的大小上限**
* **缩略图的最小图像大小**
* **缩略图大小最大值**
* **允许拥有权限的成员**
* **允许的拥有权限的成员**
* **在作者编辑模式下阻止“用户生成内容”**
* **构思标题**

* 创意的显示标题。 默认为 `Ideation`.
* **构思描述**

   要显示为创意子标题的描述。 默认为无描述。

* **每页主题数**

   定义每个页面显示的想法/帖子数。 默认值为10。

* **已审核**

   如果选中，必须先批准发布想法和评论，然后才能将其显示在发布网站上。 默认值为未选中。

* **关闭**

   如果选中，创意论坛将禁止新创意和评论。 默认值为未选中。

* **富文本编辑器**

   如果选中，则可以在输入想法和注释时添加标记。 默认值为未选中。

* **允许标记**

   如果选中，则允许成员将标记标签添加到其帖子(请参阅 **[!UICONTROL 标记字段]** 选项卡)。 默认值为未选中。

* **允许文件上传**

   如果选中，则允许将文件附件添加到创意或注释中。 默认值为未选中。

* **最大文件大小**

   相关条件仅限于 `Allow File Uploads` 已选中。 此字段将限制已上传文件的大小（以字节为单位）。 默认值为104857600 (10 Mb)。

* **允许的文件类型**

   相关条件仅限于 `Allow File Uploads` 已选中。 包含“点”分隔符的逗号分隔文件扩展名列表。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传未指定的文件类型。 缺省值为none以便允许所有文件类型。

* **附加图像文件最大大小**

   仅在选中允许文件上传时才相关。 上传的图像文件可以包含的最大字节数。 默认值为2097152 (2 Mb)。

* **允许回复**

   如果选中，则允许对发布到创意的评论进行回复。 默认值为未选中。

* **允许投票**

   如果选中，则允许对创意的评论进行投票。 默认值为未选中。

* **允许用户删除评论和主题**

   如果选中，则允许成员删除他们发表的评论和想法。 默认值为未选中。

* **允许关注**

   如果选中，则为创意帖子包括以下功能，该功能允许成员成为 [已通知](/help/communities/notifications.md) 新帖子的数量。 默认值为未选中。

* **允许电子邮件订阅**

   如果选中，则允许成员通过电子邮件接收新帖子的通知([订阅](/help/communities/subscriptions.md))。 需要 `Allow Following` 将检查和 [已配置电子邮件](/help/communities/email.md). 默认值为未选中。

* **允许投票**

   如果选中，则允许对创意的评论进行投票。 默认值为未选中。

* **显示徽章**

   如果选中，则显示已获得和已分配 [徽章](/help/communities/implementing-scoring.md) 一个会员的主意。 默认值为未选中。

* **不在列表页上获取回复**

* **允许专题内容**

   如果选中，该创意能够被标识为 [专题内容](/help/communities/featured.md). 默认值为未选中。

* **启用提及功能**
* **最大提及次数**
* **UI 提及模式**

#### “用户审核”选项卡 {#user-moderation-tab}

在 **[!UICONTROL 用户审核]** 选项卡，指定如何管理已发布的想法和评论（用户生成的内容）。 有关更多信息，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

* **拒绝帖子**

   如果选中，将允许受信任的成员版主拒绝帖子并阻止帖子出现在公共论坛上。 默认值为未选中。

* **关闭/重新打开主题**

   如果选中，受信任的成员审查方可以关闭主题以进一步编辑和注释，也可以重新打开主题。 默认值为未选中。

* **标记帖子**

   如果选中，则允许成员将其他人的主题或评论标记为不适当。 默认值为未选中。

* **标记原因列表**

   如果选中，则允许成员从下拉列表中选择他们标记主题或评论为不适当的原因。 默认值为未选中。

* **自定义标志原因**

   如果选中，则允许成员输入他们自己的原因，将主题或评论标记为不适当。 默认值为未选中。

* **审核阈值**

   输入在通知版主之前，成员必须标记主题或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入在将主题或评论从公开视图隐藏之前必须对其标记的次数。 如果设置为–1，则标记的主题或评论永远不会从公共视图中隐藏。 否则，此数字必须大于或等于审核阈值。 默认值为5。

#### “标记”字段选项卡 {#tag-field-tab}

在 **[!UICONTROL 标记字段]** 选项卡中，如果下方允许，则可能应用的标记 **[!UICONTROL 设置]** 选项卡，将根据选择的命名空间进行限制。

* **允许的命名空间**

   相关，如果 `Allow Tagging` 已检查 **[!UICONTROL 设置]** 选项卡。 可以应用的标记仅限于已检查的命名空间类别中的标记。 命名空间列表包括“标准标记”（默认命名空间）和“包括所有标记”。 默认设置为none选中，这意味着允许使用所有命名空间。

* **建议限制**

   输入要显示为向论坛发布成员建议的标记数。 值 **-1** 表示没有限制。 默认值为0。

#### “排序设置”选项卡 {#sort-settings-tab}

在 **[!UICONTROL 排序设置]** 选项卡，指定在显示时如何对已发布的评论进行排序。

* **排序方式**

   选中所有允许的排序选择： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. 默认为 `Newest, Oldest, Last Updated`.

* **设置为默认**

   下拉以选择其中一个选中的排序选项以显示为默认值。 默认为 `Newest`.

* **选择分析排序的时间选项**

   下拉以选择其中一项 `All, Last 24 Hours, Last 7 Days, Last 30 Days`. 默认为 `All`.

## 网站访客体验 {#site-visitor-experience}

### 创建构思 {#creating-idea}

与所有Communities功能一样，如果未登录，则网站访客只能阅读想法并查看其他人的意见（通过评论和投票/点赞）。

登录后，成员可以创建一个新想法。

![create-new-idea](assets/create-new-idea.png)

在提交构思之前，成员可以保存草稿。

通过选择 `Save as Draft` 按钮，将保存草稿。

![save-idea](assets/save-idea.png)

在中查看已保存的草稿时 `My Drafts` 选项卡，选择 `Read More` 要重新进入编辑模式，请执行以下操作：

![edit-idea](assets/edit-idea.png)

#### 提供反馈 {#providing-feedback}

一旦该创意发布后，其他成员可以登录，打开该创意( `Read More`)，并赞同此想法，从而增加票数，并发表评论。

![反馈](assets/feedback-idea.png)

### 附加信息 {#additional-information}

欲知更多信息，请访问 [Ideation Essentials](/help/communities/ideation.md) 适用于开发人员的页面。

有关审核已发布的主题和评论，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

有关标记已发布的主题和评论，请参阅 [标记用户生成的内容](/help/communities/tag-ugc.md).
