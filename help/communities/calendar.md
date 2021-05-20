---
title: 日历功能
seo-title: 日历功能
description: 以日历格式提供社区活动信息
seo-description: 以日历格式提供社区活动信息
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 5%

---

# 日历功能{#calendar-feature}

## 简介 {#introduction}

日历功能支持以日历格式向所有站点访客或仅登录站点访客（社区成员）提供社区活动信息，而只有授权成员才能添加活动。

此文档部分描述

* 向AEM网站添加日历功能
* `Calendar`组件的配置设置

## 向页面{#adding-a-calendar-to-a-page}添加日历

要在创作模式下向页面添加`Calendar`组件，请使用组件浏览器找到

* `Communities / Calendar`

并将其拖动到页面上的适当位置，如相对于要供用户查看的功能的位置。

有关必要信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side)时，将显示`Calendar`组件。

![日历 — 组件](assets/calendar-component.png)

### 配置日历{#configuring-calendar}

选择要访问的已放置的`Calendar`组件，然后选择`Configure`图标以打开编辑对话框。

![配置](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### “设置”选项卡{#settings-tab}

在&#x200B;**设置**&#x200B;选项卡下，指定是否允许将标记应用于日历条目。

* **每页的事件数**

   定义每页显示的事件数。 默认值为10。

* **已审核**

   如果选中此项，则必须批准发布日历事件和评论，然后才能在发布网站上显示这些事件和评论。 默认为未选中。

* **关闭**

   如果选中，则日历将关闭为新事件条目和注释。 默认为未选中。

* **富文本编辑器**

   如果选中，则可以输入带有标记的日历事件和注释。 默认选中。

* **允许标记**

   如果选中此选项，则允许成员向他们发布的事件中添加标签（请参阅&#x200B;**标签字段**&#x200B;选项卡）。 默认选中。

* **允许文件上传**

   如果选中此项，则允许将文件附件添加到日历事件或评论。 默认选中。

* **允许关注**

   如果选中，则允许成员关注发布到日历的事件。 默认选中。

* **最大文件大小**

   仅当选中`Allow File Uploads`时相关。 此字段将限制已上传文件的大小（以字节为单位）。 默认为104857600(10 Mb)。

* **允许的文件类型**

   仅当选中`Allow File Uploads`时相关。 以逗号分隔的文件扩展名列表，其中带有“圆点”分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则将不允许上载未指定的文件类型。 默认值未指定，以便允许使用所有文件类型。

* **附加图像文件最大大小**

   仅当选中允许文件上传时相关。 上传的图像文件可能具有的最大字节数。 默认为2097152** **(2 Mb)。

* **允许的封面图像类型**

   以逗号分隔的图像文件扩展名列表，其中带有“点”分隔符。 默认值为`.jpg,.jpeg,.png,.gif,.bmp`。

* **允许主题回复**

   如果选中此项，则允许对发布到日历事件的评论做出回复。 默认选中。

* **允许用户删除评论和事件**

   如果选中此项，则允许成员删除他们发布的评论和日历事件。 默认选中** **。

* **允许投票**

   如果选中此项，则包含包含日历事件的投票功能。 默认选中。

* **显示痕迹导航**

   在事件页面上显示痕迹导航. 默认选中。

* **日期范围筛选器**

   定义添加到当前日期的天数，以计算日历事件列表页面过滤器的“至”值。 默认数字为30。

* **允许专题内容**

   如果选中，则该构思能够被标识为[特色内容](/help/communities/featured.md)。 默认为未选中。

在&#x200B;**用户审核**&#x200B;选项卡下，指定如何管理已发布的主题和回复（用户生成的内容）。 有关更多信息，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

#### “用户审核”选项卡{#user-moderation-tab}

* **拒绝帖子**

   如果选中，则允许受信任的成员审核者拒绝帖子并阻止帖子出现在公共论坛中。 默认选中。

* **关闭/重新打开事件**

   如果选中，受信任的成员审核者可以关闭事件以进一步进行编辑和评论，也可以重新打开事件。 默认选中。

* **标记帖子**

   如果选中此选项，则允许成员将他人的事件或评论标记为不适当。 默认选中。

* **标记原因列表**

   如果选中，允许成员从下拉列表中选择其标记事件或评论为不适当的原因。 默认为未选中。

* **自定义标记原因**

   如果选中，则允许成员输入自己将事件或评论标记为不适当的原因。 默认为未选中。

* **审核阈值**

   输入在通知审核者之前，必须由成员标记事件或评论的次数。 默认值为1（一次）。

* **标记限制**

   输入在事件或评论在公共视图中隐藏之前必须进行标记的次数。 如果设置为–1，则标记的主题或评论永远不会在公共视图中隐藏。 否则，此数字必须大于或等于审核阈值。 默认值为5。

#### 标记字段选项卡{#tag-field-tab}

在&#x200B;**标记字段**&#x200B;选项卡下，可能应用的标记（如果允许）位于&#x200B;**设置**&#x200B;选项卡下，将根据所选的命名空间而受到限制。

* **允许的命名空间**

   如果在&#x200B;**设置**&#x200B;选项卡下选中`Allow Tagging`，则相关。 可应用的标记仅限于所选命名空间类别中的标记。 命名空间列表包括“标准标记”（默认命名空间）以及“包括所有标记”。 默认为“未选中”，这表示允许使用所有命名空间。

* **建议限制**

   输入要作为建议显示给论坛成员的标记数。 默认值为**-**1（无限制）。

>[!NOTE]
>
>访问[管理标记](/help/sites-administering/tags.md)以了解如何添加新的标记命名空间（分类）。

#### 翻译选项卡{#translation-tab}

在&#x200B;**翻译**&#x200B;选项卡下，如果为社区站点启用了翻译，则可以设置翻译来翻译整个线程（事件和评论），而不是特定帖子。

* **全部翻译**

   如果选中此选项，则事件和注释将翻译为用户的首选语言。 默认选中。

## 网站访客体验{#site-visitor-experience}

在发布环境中，日历功能将显示具有默认日期范围的搜索字段以及该范围内的任何日历事件。

选择日历事件后，将显示日历事件详细信息、说明和注释。

其他功能取决于网站访客是审核者、管理员、社区成员、特权成员还是匿名。

### 审核者和管理员{#moderators-and-administrators}

当登录用户具有审核者或管理员权限时，他们能够对发布到某个事件的所有日历事件和评论执行[审核任务](/help/communities/moderate-ugc.md)（组件配置允许）。

![审核者 — 视图](assets/moderators-view.png)

#### 成员 {#members}

当登录用户是社区成员或[特权成员](/help/communities/users.md#privileged-members-group)（取决于配置）时，他们能够选择`New Event`以创建和发布新的日历事件。

具体而言，他们可以：

* 创建新日历事件
* 将评论发布到日历事件
* 编辑自己的日历事件或评论
* 删除自己的日历事件或评论
* 标记他人的日历事件或评论

![create-event](assets/configure-calendar2.png)

![事件 — 帖子](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登录的网站访客只能阅读发布的日历事件，翻译这些事件（如果受支持），但不得添加事件或评论，也不得标记他人的事件或评论。

![anonymous-user-view](assets/anonymous-user-view1.png)

## 附加信息 {#additional-information}

有关更多信息，请参阅[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)页面，供开发人员使用。

有关日历事件和评论的审核，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记日历事件和注释，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。

有关日历事件和注释的翻译，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。
