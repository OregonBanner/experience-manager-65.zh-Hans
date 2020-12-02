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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 5%

---


# 日历功能{#calendar-feature}

## 简介 {#introduction}

日历功能支持以日历格式向所有站点事件或仅在站点访客（社区成员）中签名提供社区访客信息，而只有授权成员可以添加事件。

文档的本节介绍

* 将日历功能添加到AEM站点
* `Calendar`组件的配置设置

## 将日历添加到页面{#adding-a-calendar-to-a-page}

要在创作模式下将`Calendar`组件添加到页面，请使用组件浏览器查找

* `Communities / Calendar`

并将其拖动到页面上的位置，如相对于要用户查看的功能的位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[必需的客户端库](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side)时，将显示`Calendar`组件。

![calendar-component](assets/calendar-component.png)

### 配置日历{#configuring-calendar}

选择要访问的已放置`Calendar`组件，然后选择打开编辑对话框的`Configure`图标。

![配置](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### 设置选项卡{#settings-tab}

在&#x200B;**设置**&#x200B;选项卡下，指定是否允许将标记应用于日历条目。

* **每页的事件数**

   定义每页显示的事件数。 默认值为10。

* **已审核**

   如果选中此项，则发布日历事件和评论必须获得批准，然后才能在发布站点上显示。 默认为未选中。

* **关闭**

   如果选中，则日历将关闭到新的事件条目和注释。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以输入带有标记的日历事件和注释。 选中默认值。

* **允许标记**

   如果选中此项，则允许成员向他们发布的事件添加标记标签（请参阅&#x200B;**标记字段**&#x200B;选项卡）。 选中默认值。

* **允许文件上传**

   如果选中，则允许将文件附件添加到日历事件或注释。 选中默认值。

* **允许关注**

   如果选中，则允许成员遵循已过帐到日历的事件。 选中默认值。

* **最大文件大小**

   仅当选中`Allow File Uploads`时相关。 此字段将限制已上载文件的大小（以字节为单位）。 默认值为104857600(10 Mb)。

* **允许的文件类型**

   仅当选中`Allow File Uploads`时相关。 以逗号分隔的文件扩展名列表，以“点”分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许上传那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **附加图像文件最大大小**

   仅当选中“允许文件上传”时相关。 上传的图像文件可能具有的最大字节数。 默认值为2097152** **(2 Mb)。

* **允许的封面图像类型**

   以逗号分隔的图像文件扩展名列表，以“点”分隔。 默认值为`.jpg,.jpeg,.png,.gif,.bmp`。

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

   如果选中，则该想法可标识为[特色内容](/help/communities/featured.md)。 默认为未选中。

在&#x200B;**用户协调**&#x200B;选项卡下，指定如何管理已发布的主题和回复（用户生成的内容）。 有关详细信息，请参阅[协调用户生成的内容](/help/communities/moderate-ugc.md)。

#### “用户协调”选项卡{#user-moderation-tab}

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

#### 标记字段选项卡{#tag-field-tab}

在&#x200B;**标记字段**&#x200B;选项卡下，如果允许在&#x200B;**设置**&#x200B;选项卡下应用的标记会根据所选命名空间进行限制。

* **允许的命名空间**

   如果在&#x200B;**设置**&#x200B;选项卡下检查了`Allow Tagging`，则相关。 可应用的标记仅限于所选命名空间类别内的标记。 命名空间的列表包括“标准标记”(默认命名空间)和“包括所有标记”。 默认值为“无”(none checked)，这意味着允许所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 默认值为**-**1（无限制）。

>[!NOTE]
>
>访问[管理标记](/help/sites-administering/tags.md)，了解如何添加新标记命名空间（分类）。

#### 转换选项卡{#translation-tab}

在&#x200B;**Translation**&#x200B;选项卡下，如果为社区站点启用了翻译，则可以设置翻译来翻译整个线程(事件和评论)，而不是翻译特定帖子。

* **全部翻译**

   如果选中，则事件和注释将翻译为用户的首选语言。 选中默认值。

## 站点访客体验{#site-visitor-experience}

在发布环境中，日历功能将显示一个搜索字段，其中包含默认日期范围以及该范围内的任何日历事件。

选择日历事件后，将显示日历事件详细信息、说明和注释。

其他功能取决于站点访客是版主、管理员、社区成员、特权成员还是匿名。

### 版主和管理员{#moderators-and-administrators}

当登录用户具有审查方或管理员权限时，他们可以对所有日历事件和发布到事件的评论执行[审核任务](/help/communities/moderate-ugc.md)（组件配置允许）。

![版主-视图](assets/moderators-view.png)

#### 成员 {#members}

当登录用户是社区成员或[特权成员](/help/communities/users.md#privileged-members-group)（取决于配置）时，他们可以选择`New Event`创建并发布新的日历事件。

具体而言，他们可以：

* 创建新日历事件
* 将评论发布到日历事件
* 编辑自己的日历事件或注释
* 删除自己的日历事件或注释
* 标记他人的日历事件或注释

![创建事件](assets/configure-calendar2.png)

![事件后](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的日历事件，如果受支持，可翻译这些，但不能添加事件或评论，也不能标记其他人的事件或评论。

![匿名用户视图](assets/anonymous-user-view1.png)

## 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)页面。

有关日历事件和注释的协调，请参阅[协调用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记日历事件和注释，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。

有关日历事件和注释的转换，请参阅[转换用户生成的内容](/help/communities/translate-ugc.md)。
