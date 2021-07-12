---
title: 徽章控制台
seo-title: 徽章控制台
description: 社区徽章控制台允许您添加自定义徽章，这些徽章可在成员获得（授予）或在社区中承担特定角色（已分配）时为其显示
seo-description: 社区徽章控制台允许您添加自定义徽章，这些徽章可在成员获得（授予）或在社区中承担特定角色（已分配）时为其显示
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# 徽章控制台 {#badges-console}

## 关于徽章 {#about-badges}

社区徽章控制台提供了添加自定义徽章的功能，当会员获得（授予）或在社区中承担特定角色（分配）时，可向其显示自定义徽章。

### 徽章可见性 {#badge-visibility}

目前，社区成员获得或分配的徽章将与其姓名和头像一起显示在以下位置：

* 个人资料
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在创作环境中，导航到徽章控制台：

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 徽章]**

此控制台会显示当前可用的徽章，以及可从中添加新徽章的徽章。

![徽章主页](assets/badges-homepage.png)

## 创建徽章 {#create-badge}

通过上传合适的小图像（72dpi，高度在26-32像素之间）并提供名称来创建标记。 标记图像存储在位于`/libs/settings/community/badging/images`的存储库中，并会自动复制到发布环境。

如果发布环境是发布者的场，则需要配置[用户同步](/help/communities/sync.md)。

![create-badge](assets/create-badge.png)

* **上传图像**

   （*必需*）JPEG或PNG格式的72dpi建议大小为32 x 32像素的标记图像。

* **名称**

   （*必需*）标记名称。 它是默认的`Display Name`以及存储库节点名称。 如果`Name`不是有效的存储库节点名称，则会对其进行修改。

* **显示名称**

   （*可选*）要在UI中显示标记的名称。 默认为为`Name`输入的未更改文本。

* **描述**

   （*可选*）标记的描述。

## 附加信息 {#additional-information}

有关设置评分和标记规则的详细信息，请参阅[评分和徽章](/help/communities/implementing-scoring.md)。

有关管理成员的徽章，请参阅[成员控制台](/help/communities/members.md)。
