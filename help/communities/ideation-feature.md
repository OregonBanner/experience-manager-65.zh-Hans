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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 构思功能 {#ideation-feature}

## 简介 {#introduction}

构思功能为发布环境中的登录站点访客（社区成员）提供了一个区域，用于：

* 创建想法并与社区共享。
* 视图和评论想法。
* 遵循一个想法。
* 就一个想法投票。

本文档的这一部分描述了：

* 将构思功能添加到AEM站点。
* 构思组件的配置设置。

### Adding a Ideation to a Page {#adding-a-ideation-to-a-page}

要在创作模 `Ideation` 式下将组件添加到页面，请使用组件浏览器查找

* `Communities / Ideation`

并将其拖动到应该出现构思的页面上的位置。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包含 [所需的客户端库时](/help/communities/ideation.md#essentials-for-client-side) ，组件的显示方式 `Ideation` 如下：

![chlimage_1-71](assets/chlimage_1-71.png)

### 配置构思 {#configuring-an-ideation}

选择要访问 `Ideation` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-72](assets/chlimage_1-72.png) ![Ideation-settings](assets/ideation-settings.png)

#### 设置选项卡 {#settings-tab}

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

   如果选中此项，则发布构思和评论必须经过批准，才能在发布站点上显示。 默认为未选中。

* **关闭**

   如果选中此项，则会关闭构思论坛以查看新构思和评论。 默认为未选中。

* **富文本编辑器**

   如果选中此项，则可以使用标记输入想法和注释。 默认为未选中。

* **允许标记**

   如果选中此项，则允许成员向其帖子中添加标记标签(请参阅 **[!UICONTROL 标记字段]** 选项卡)。 默认为未选中。

* **允许文件上传**

   如果选中此项，则允许将文件附件添加到构思或注释中。 默认为未选中。

* **最大文件大小**

   仅在选中时 `Allow File Uploads` 相关。 此字段将限制已上载文件的大小（以字节为单位）。 默认为104857600(10 Mb)。

* **允许的文件类型**

   仅在选中时 `Allow File Uploads` 相关。 以逗号分隔的文件扩展名列表（以“点”分隔）。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **附加图像文件最大大小**

   仅在选中“允许文件上传”时相关。 上传的图像文件可能具有的最大字节数。 默认为2097152(2 Mb)。

* **允许回复**

   如果选中此项，则允许回复发布到构思的评论。 默认为未选中。

* **允许投票**

   如果选中此项，则允许对某个想法的注释进行投票。 默认为未选中。

* **允许用户删除评论和主题**

   如果选中此项，则允许成员删除其发布的评论和想法。 默认为未选中。

* **允许关注**

   如果选中此项，则为创意帖子加入以下功能，允许成员收到 [新帖子](/help/communities/notifications.md) 的通知。 默认为未选中。

* **允许电子邮件订阅**

   如果选中此项，则允许会员通过电子邮件([订阅](/help/communities/subscriptions.md))通知新帖子。 需要 `Allow Following` 选中并配置电 [子邮件](/help/communities/email.md)。 默认为未选中。

* **允许投票**

   如果选中此项，则允许对某个想法的注释进行投票。 默认为未选中。

* **显示徽章**

   如果选中此项，则显示已获 [得的徽章](/help/communities/implementing-scoring.md) ，以及已分配的徽章。 默认为未选中。

* **不在列表页面上获取回复**

* **允许专题内容**

   如果选中此项，则可将该创意标识为特色 [内容](/help/communities/featured.md)。 默认为未选中。

* **启用提及功能**
* **最大提及次数**
* **UI 提及模式**

#### “用户审核”选项卡 {#user-moderation-tab}

在“用户 **[!UICONTROL 协调]** ”选项卡下，指定如何管理已发布的构思和评论（用户生成的内容）。 有关详细信息，请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md)。

* **拒绝帖子**

   如果选中此项，则允许受信任的成员审核者拒绝帖子并阻止帖子显示在公共论坛中。 默认为未选中。

* **关闭／重新打开主题**

   如果选中此项，则受信任的成员审核者可以关闭主题以进一步编辑和评论，也可以重新打开主题。 默认为未选中。

* **旗标帖子**

   如果选中此项，则允许成员将他人的主题或评论标记为不合适。 默认为未选中。

* **旗标原因列表**

   如果选中此项，允许成员从下拉列表中选择其标记主题或评论为不适当的理由。 默认为未选中。

* **自定义标志原因**

   如果选中此项，则允许成员输入自己将主题或评论标记为不合适的原因。 默认为未选中。

* **协调阈值**

   输入在通知版主之前必须由成员标记主题或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入主题或评论在隐藏于公共视图之前必须标出的次数。 如果设置为-1，则标记的主题或评论从不隐藏在公共视图中。 否则，此数字必须大于或等于审核阈值。 默认为5。

#### 标记字段选项卡 {#tag-field-tab}

在“标 **[!UICONTROL 记字段]** ”选项卡下，可能应用的标记（如果允许）会根据选择的命名空间 **** 来限制。

* **允许的命名空间**

   如果选中 `Allow Tagging` 了“设置”选项卡下 **[!UICONTROL 的选项]** ，则相关。 可应用的标记仅限于所选命名空间类别内的标记。 命名空间的列表包括“标准标记”(默认命名空间)和“包括所有标记”。 默认值为none checked，表示允许所有命名空间。

* **建议限制**

   输入要作为建议显示给发布到论坛的成员的标记数。 值-1表 **示无** 限制。 默认值为0。

#### “排序设置”选项卡 {#sort-settings-tab}

在“排 **[!UICONTROL 序设置]** ”选项卡下，指定显示已发布注释时的排序方式。

* **排序方式**

   选中所有允许的排序选择： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Default is `Newest, Oldest, Last Updated`.

* **设置为默认**

   下拉以选择一个选中的排序选项作为默认值显示。 Default is `Newest`.

* **选择分析排序的时间选项**

   下拉以选择其中一个 `All, Last 24 Hours, Last 7 Days, Last 30 Days`。 Default is `All`.

## 站点访客体验 {#site-visitor-experience}

### 创建构思 {#creating-idea}

与所有社区功能一样，如果未登录，站点访客只能阅读想法并视图他人的意见（通过评论和投票／喜欢）。

登录后，会员可能会创建新想法。

![chlimage_1-73](assets/chlimage_1-73.png)

在提交构思之前，成员可以保存草稿。

通过选择按 `Save as Draft` 钮，将保存草稿。

![chlimage_1-74](assets/chlimage_1-74.png)

在选项卡中查看保存的草 `My Drafts` 稿时，选择 `Read More` 以重新进入编辑模式：

![chlimage_1-75](assets/chlimage_1-75.png)

#### 提供反馈 {#providing-feedback}

构思发布后，其他成员可以登录，打开构思( `Read More`)并像其他想法一样，从而增加投票数并发表评论。

![chlimage_1-76](assets/chlimage_1-76.png)

### 附加信息 {#additional-information}

有关详细信息，请参阅面向开发 [人员的Idemation Essentials](/help/communities/ideation.md) （构思基本工具）页面。

有关审核已发布的主题和评论，请参阅审核 [用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记已发布的主题和评论，请参阅 [标记用户生成的内容](/help/communities/tag-ugc.md)。
