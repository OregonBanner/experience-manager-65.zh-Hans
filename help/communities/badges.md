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
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 4%

---


# 标记控制台 {#badges-console}

## 关于标记 {#about-badges}

社区徽章控制台提供添加自定义徽章的功能，这些徽章可在会员获得（授予）或在社区中承担特定角色（分配）时显示。

### 徽章可见性 {#badge-visibility}

目前，社区会员获得或分配的徽章将与其姓名和头像一起出现在以下位置：

* 个人资料
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在创作环境中，要访问标记控制台

* 在全局导航中，导航到工 **[!UICONTROL 具>社区>标记]**

此控制台显示当前可用的标记，以及可从中添加新标记。

![chlimage_1-123](assets/chlimage_1-123.png)

## 创建徽章 {#create-badge}

通过上传合适的小图像（72dpi，高度在26-32像素之间）并提供名称来创建标记。 徽章图像存储在位于的存储库 `/libs/settings/community/badging/images` 中，并自动复制到发布环境。

如果发布环境是发布者的场，则必须配置用 [户同步](/help/communities/sync.md)。

![chlimage_1-124](assets/chlimage_1-124.png)

* **上传图像**

   (*必需*)建议大小为32 x 32像素、72dpi的徽章图像，采用JPEG或PNG格式。

* **名称**

   (必&#x200B;*需*)徽章名称。 它是默认的 `Display Name` 和存储库节点名称。 如果该 `Name` 节点不是有效的存储库节点名称，则会对其进行修改。

* **显示名称**

   (*可选*)在UI中为徽章显示的名称。 默认值是为输入的未更改文本 `Name`。

* **描述**

   (*可选*)徽章的说明。

## 附加信息 {#additional-information}

有关设置得分和徽章规则的详细信息，请参 [阅评分和徽章](/help/communities/implementing-scoring.md)。

有关管理会员的标记，请参阅 [会员控制台](/help/communities/members.md)。
