---
title: 使用評等
seo-title: Using Ratings
description: 將Rating元件新增至頁面
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 使用評等 {#using-ratings}

此 `Rating` 元件可獨立使用或搭配其他Communities功能使用。 此元件可讓登入的社群成員透過對內容進行評分來表達意見。

## 新增評等至頁面 {#adding-a-rating-to-a-page}

若要新增 `Rating` 元件至作者模式下的頁面，找到元件 `Communities / Rating` 並將其拖曳至頁面上某個位置，例如成員相對於該特徵進行評等。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](rating-basics.md#essentials-for-client-side) 包含，這就是 `Rating` 元件隨即出現。

![评级](assets/rating.png)

## 設定評等 {#configuring-rating}

選取已放置的 `Rating` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 標籤：您指定「評等」的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL 標簽名稱]**
(*必填*)的簡單名稱 `Rating` 會唯一識別此執行個體。 必須為存放庫的有效節點名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成员 {#members}

每個成員只允許一個評等。 會員可隨時變更其評等。

### 匿名 {#anonymous}

不支援評級的匿名發佈。 網站訪客必須註冊（成為會員）並登入才能參與。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [Rating Essentials](rating-basics.md) 適用於開發人員的頁面。
