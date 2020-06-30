---
title: 日历功能
seo-title: 日历功能
description: 以日历格式提供社区事件信息
seo-description: 以日历格式提供社区事件信息
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 5%

---


# 日历功能 {#calendar-feature}

## 简介 {#introduction}

日历功能支持以日历格式向所有站点事件或仅在站点访客（社区成员）中签名提供社区访客信息，而只有授权成员可以添加事件。

文档的本节介绍

* 将日历功能添加到AEM站点
* 组件的配置 `Calendar` 设置

## Adding a Calendar to a Page {#adding-a-calendar-to-a-page}

要在创作模 `Calendar` 式下将组件添加到页面，请使用组件浏览器来查找

* `Communities / Calendar`

并将其拖动到页面上的位置，如相对于要用户查看的功能的位置。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

当包 [含所需的客户端库](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) ，组件的显示 `Calendar` 方式即为此。

![chlimage_1-112](assets/chlimage_1-112.png)

### 配置日历 {#configuring-calendar}

选择要访问的 `Calendar` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-113](assets/chlimage_1-113.png)![chlimage_1-114](assets/chlimage_1-114.png)

#### “设置”选项卡 {#settings-tab}

在“设 **置** ”选项卡下，指定是否允许将标记应用于日历条目。

* **每页的事件数**

   定义每页显示的事件数。 默认值为10。

* **已审核**

   如果选中此项，则发布日历事件和评论必须获得批准，然后才能在发布站点上显示。 默认为未选中。

* **关闭**

   如果选中，则日历将关闭到新的事件条目和注释。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以输入带有标记的日历事件和注释。 选中默认值。

* **允许标记**

   如果选中此项，则允许成员向他们发布的事件添加标记标签(请参 **阅标记字段** 选项卡)。 选中默认值。

* **允许文件上传**

   如果选中，则允许将文件附件添加到日历事件或注释。 选中默认值。

* **允许关注**

   如果选中，则允许成员遵循已过帐到日历的事件。 选中默认值。

* **最大文件大小**

   仅在选中时 `Allow File Uploads` 相关。 此字段将限制已上载文件的大小（以字节为单位）。 默认值为104857600(10 Mb)。

* **允许的文件类型**

   仅在选中时 `Allow File Uploads` 相关。 以逗号分隔的文件扩展名列表，以“点”分隔。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **附加图像文件最大大小**

   仅当选中“允许文件上传”时相关。 上传的图像文件可能具有的最大字节数。 默认值为2097152** **(2 Mb)。

* **允许的封面图像类型**

   以逗号分隔的图像文件扩展名列表，以“点”分隔。 Default is `.jpg,.jpeg,.png,.gif,.bmp`.

* **允许主题回复**

   如果选中，则允许回复发布到日历事件的注释。 选中默认值。

* **允许用户删除评论和事件**

   如果选中此项，则允许成员删除已发布的评论和日历事件。 默认值为** **checked。

* **允许投票**

   如果选中此项，请在日历事件中包含投票功能。 选中默认值。

* **显示痕迹导航**

   在事件页面上显示痕迹导航. 选中默认值。

* **日期范围筛选器**

   定义添加到当前日期的天数，以计算日历事件列表页面筛选器的“至”值。 默认数为30。

* **允许专题内容**

   如果选中，则可以将该想法标识为特色 [内容](/help/communities/featured.md)。 默认为未选中。

在“用 **户审核** ”选项卡下，指定如何管理已发布的主题和回复（用户生成的内容）。 有关详细信息，请参 [阅调节用户生成的内容](/help/communities/moderate-ugc.md)。

#### “用户审核”选项卡 {#user-moderation-tab}

* **拒绝帖子**

   如果选中，则允许受信任的成员审核者拒绝帖子并阻止帖子显示在公共论坛中。 选中默认值。

* **关闭/重新打开事件**

   如果选中，受信任的成员版主可以关闭事件以进一步编辑和注释，也可以重新打开事件。 选中默认值。

* **旗标帖子**

   如果选中，允许成员将其他人的事件或注释标记为不合适。 选中默认值。

* **标志原因列表**

   如果选中，允许成员从下拉式列表中选择其标记事件或评论为不合适的理由。 默认为未选中。

* **自定义标志原因**

   如果选中，允许成员输入其自己将事件或评论标记为不合适的原因。 默认为未选中。

* **审核阈值**

   输入成员在通知版主之前必须标记事件或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入事件或评论在隐藏之前必须标出的次数，以免公开视图。 如果设置为-1，则标记的主题或评论从不隐藏于公共视图。 否则，此数字必须大于或等于仲裁阈值。 默认值为5。

#### 标记字段选项卡 {#tag-field-tab}

在“标 **记”字段** (Tag field)选项卡下 **，根据所选的命名空间，在“设置”(Settings)选项卡下允许的情况下，** 可以应用的标记会受到限制。

* **允许的命名空间**

   如果在 `Allow Tagging` **设置**选项卡下检查，则相关。 可应用的标记仅限于所选命名空间类别内的标记。 命名空间的列表包括“标准标记”(默认命名空间)和“包括所有标记”。 默认值为“无”(none checked)，这意味着允许所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 默认值为**-**1（无限制）。

>[!NOTE]
>
>访问 [管理标记](/help/sites-administering/tags.md) ，了解如何添加新标记命名空间（分类）。


#### 翻译选项卡 {#translation-tab}

在“翻 **译** ”选项卡下，如果为社区站点启用了翻译，则可以将翻译设置为翻译整个线程(事件和评论)，而不是翻译特定帖子。

* **全部翻译**

   如果选中，则事件和注释将翻译为用户的首选语言。 选中默认值。

## 站点访客体验 {#site-visitor-experience}

在发布环境中，日历功能将显示一个搜索字段，其中包含默认日期范围以及该范围内的任何日历事件。

选择日历事件后，将显示日历事件详细信息、说明和注释。

其他功能取决于站点访客是版主、管理员、社区成员、特权成员还是匿名。

### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审查方或管理员权限时，他们能够对发布到 [事件的所有日历任务](/help/communities/moderate-ugc.md) （在组件配置允许的情况下）执行审核事件。

![chlimage_1-115](assets/chlimage_1-115.png)

#### 成员 {#members}

当登录用户是社区成员或特 [权成员](/help/communities/users.md#privileged-members-group) （取决于配置）时，他们可以选择 `New Event` 创建并发布新的日历事件。

具体而言，他们可以：

* 创建新日历事件
* 将评论发布到日历事件
* 编辑自己的日历事件或注释
* 删除自己的日历事件或注释
* 标记他人的日历事件或注释

![chlimage_1-116](assets/chlimage_1-116.png)

![chlimage_1-117](assets/chlimage_1-117.png)

#### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的日历事件，如果受支持，可翻译这些，但不能添加事件或评论，也不能标记其他人的事件或评论。

![chlimage_1-118](assets/chlimage_1-118.png)

## 附加信息 {#additional-information}

有关开发人员的详细信息，请 [参阅“日历](/help/communities/calendar-basics-for-developers.md) ”“必备工具”页。

有关日历事件和注释的审核，请参 [阅审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记日历事件和注释，请参 [阅标记用户生成的内容](/help/communities/tag-ugc.md)。

有关日历事件和注释的翻译，请参 [阅翻译用户生成的内容](/help/communities/translate-ugc.md)。
