---
title: 徽章主控台
seo-title: Badges Console
description: Communities Badges主控台可讓您新增自訂徽章，當成員贏取（授予）或在社群中擔任特定角色（已指派）時，徽章可顯示給成員
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

# 徽章主控台 {#badges-console}

## 關於徽章 {#about-badges}

Communities Badges主控台可新增自訂徽章，當成員贏取（授予）或在社群中擔任特定角色（已指派）時，徽章可以針對該成員顯示。

### 徽章可見性 {#badge-visibility}

目前，社群成員獲得或指派的徽章將與其名稱和頭像一起顯示在以下位置：

* 配置文件
* [論壇](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在作者環境中，導覽至「徽章」主控台：

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 徽章]**

此主控台會顯示目前可用的徽章，以及可以從中新增新徽章的徽章。

![徽章 — 首頁](assets/badges-homepage.png)

## 创建徽章 {#create-badge}

徽章是藉由上傳適當小影像（72dpi，高度範圍介於26到32畫素之間）並提供名稱來建立。 徽章影像儲存在存放庫中，位置為 `/libs/settings/community/badging/images` 和會自動復寫至發佈環境。

如果發佈環境是發佈者的陣列，則必須設定 [使用者同步](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **上传图像**

   (*必填*)以JPEG或PNG格式呈現建議大小32 x 32畫素(72dpi)的徽章影像。

* **名称**

   (*必填*)徽章名稱。 這是預設值 `Display Name` 以及存放庫節點名稱。 如果 `Name` 不是有效的存放庫節點名稱，將修改它。

* **显示名称**

   (*可選*)為UI中的徽章顯示的名稱。 預設值是為「 」輸入的未變更文字 `Name`.

* **描述**

   (*可選*)徽章的說明。

## 附加信息 {#additional-information}

如需設定評分和徽章規則的詳細資訊，請參閱 [評分和預算](/help/communities/implementing-scoring.md).

如需管理成員的徽章，請參閱 [成員主控台](/help/communities/members.md).
