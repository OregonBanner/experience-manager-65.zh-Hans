---
title: 使用社交圖
seo-title: Using Social Graph
description: 將下列元件新增至頁面
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# 使用社交圖 {#using-social-graph}

## 简介 {#introduction}

社群成員可遵循的功能 [活動](activities.md) 以及所遵循的規範是透過兩個元件建立的： `Follow` 和 `Following`.

此 `Follow` 元件必須與另一個資源相關聯，而且已為社群成員和功能建立此關聯。

此 `Following` component只會列出目前成員之後或目前成員之後的成員。 此成員之間關係的社交圖表包含在為建立的使用者個人資料中 [社群網站](overview.md#communitiessites).

## 新增關注專案至頁面 {#adding-following-to-a-page}

如果需要新增 `Following` 元件至作者模式下的頁面，找到元件 `Communities / Following` 並將其拖曳至社交圖表應出現的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-socialgraph.md#essentials-for-client-side) 包含，這就是 `Following` 元件將會出現：

![關注](assets/following.png)

## 設定下列專案 {#configuring-following}

目前，需要設定屬性以判斷元件是否顯示 `follows` 關聯性，或 `following` 關係。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [Social Graph Essential](essentials-socialgraph.md) 適用於開發人員的頁面。
