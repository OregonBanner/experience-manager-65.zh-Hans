---
title: 徽章控制台
seo-title: Badges Console
description: “社区徽章”控制台允许您添加自定义徽章，当成员获得（奖励）或在社区中承担特定角色（已分配）时，可以显示这些徽章
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
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
source-wordcount: '287'
ht-degree: 4%

---

# 徽章控制台 {#badges-console}

## 关于徽章 {#about-badges}

“社区徽章”控制台提供添加自定义徽章的功能，当成员获得（奖励）或在社区中承担特定角色（已分配）时，可以显示这些徽章。

### 徽章可见性 {#badge-visibility}

目前，社区成员获得的徽章或已分配的徽章将与其名称和头像一起显示在以下位置：

* 配置文件
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在创作环境中，导航到徽章控制台：

* 从全局导航： **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 徽章]**

此控制台显示当前可用的徽章，并可从中添加新徽章。

![徽章 — 主页](assets/badges-homepage.png)

## 创建徽章 {#create-badge}

通过上载适当小图像（高度在26-32像素范围内的72dpi）并提供名称来产生徽章。 徽章图像存储在存储库中的 `/libs/settings/community/badging/images` 和会自动复制到发布环境。

如果发布环境是发布者的场，则需要配置 [用户同步](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **上传图像**

   (*必需*)以JPEG或PNG格式表示的徽章图像，建议大小为32 x 32像素(72dpi)。

* **名称**

   (*必需*)徽章名称。 这是默认设置 `Display Name` 以及存储库节点名称。 如果 `Name` 不是有效的存储库节点名称，将被修改。

* **显示名称**

   (*可选*)为UI中的徽章显示的名称。 默认值为为为输入的未更改文本 `Name`.

* **描述**

   (*可选*)徽章的描述。

## 附加信息 {#additional-information}

有关设置评分和徽章规则的详细信息，请参阅 [评分和徽章](/help/communities/implementing-scoring.md).

有关管理成员的徽章，请参阅 [成员控制台](/help/communities/members.md).
