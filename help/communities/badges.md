---
title: 标记控制台
seo-title: 标记控制台
description: 社区徽章控制台允许您添加自定义徽章，当会员获得（奖励）或在社区中承担特定角色（分配）时，这些徽章可显示给会员
seo-description: 社区徽章控制台允许您添加自定义徽章，当会员获得（奖励）或在社区中承担特定角色（分配）时，这些徽章可显示给会员
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---


# 标记控制台{#badges-console}

## 关于标记{#about-badges}

社区徽章控制台提供添加自定义徽章的功能，这些徽章可在会员获得（奖励）或在社区中承担特定角色（分配）时为其显示。

### 徽章可见性{#badge-visibility}

目前，社区会员获得或分配的徽章将与其姓名和头像一起出现在以下位置：

* 个人资料
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在创作环境中，导航到标记控制台：

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 标记]**

此控制台显示当前可用的标记，以及可从中添加新标记。

![徽章主页](assets/badges-homepage.png)

## 创建徽章 {#create-badge}

通过上传合适的小图像（72dpi，高度在26-32像素之间）并提供名称来创建标记。 徽章图像存储在`/libs/settings/community/badging/images`的存储库中，并自动复制到发布环境。

如果发布环境是发布者的场，则必须配置[用户同步](/help/communities/sync.md)。

![create-badge](assets/create-badge.png)

* **上传图像**

   （*必需*）建议大小为32 x 32像素、72dpi的徽章图像，采用JPEG或PNG格式。

* **名称**

   （*必需*）徽章名称。 它是默认`Display Name`以及存储库节点名称。 如果`Name`不是有效的存储库节点名称，则将修改它。

* **显示名称**

   （*可选*）要在UI中显示徽章的名称。 默认值是为`Name`输入的未更改文本。

* **描述**

   （*可选*）徽章的说明。

## 附加信息 {#additional-information}

有关设置得分和徽章规则的详细信息，请参阅[得分和徽章](/help/communities/implementing-scoring.md)。

有关管理成员的标记，请参阅[成员控制台](/help/communities/members.md)。
