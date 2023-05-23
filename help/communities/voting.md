---
title: 使用投票
seo-title: Using Voting
description: 新增投票元件至頁面
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# 使用投票 {#using-voting}

此 `Voting` 元件是實用的工具，可讓社群成員為特定內容片段（例如QnA元件中的答案）評分。 使用 `Voting` 元件時，成員會選取向上或向下箭頭來表示其意見。

## 新增投票至頁面 {#adding-voting-to-a-page}

若要新增 `Voting` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Voting` 並將其拖曳至頁面上適當的位置，例如與功能相對的位置以供使用者投票。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-voting.md#essentials-for-client-side) 包含，這就是 `Voting` 元件隨即出現。

![voting-component](assets/voting-component.png)

## 設定投票 {#configuring-voting}

選取已放置的 `Voting` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 索引標籤中，指定用來記錄投票的屬性。

![voting-label](assets/voting-label.png)

* **[!UICONTROL 正面响应标签]**

   (*必填*)正面回應的內部屬性名稱。

* **[!UICONTROL 负面响应标签]**

   (*必填*)負面回應的內部屬性名稱。

* **[!UICONTROL 标签名称]**

   (*必填*)此投票元件例項的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成员 {#members}

成員只能投票一次，但可隨時變更投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入才能參與投票一次。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [Voting Essentials](essentials-voting.md) 適用於開發人員的頁面。
