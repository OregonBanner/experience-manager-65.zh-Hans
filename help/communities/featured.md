---
title: 精選內容功能
seo-title: Featured Content Feature
description: 「精選內容」功能可讓登入的網站訪客強調顯示內容
seo-description: The Featured Content feature lets signed-in site visitors highlight content
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 5%

---

# 精選內容功能 {#featured-content-feature}

## 简介 {#introduction}

精選內容功能為發佈環境中的登入網站訪客（社群成員）提供一個區域，以反白顯示以下內容：

* [部落格](blog-feature.md)
* [行事曆](calendar.md)
* [論壇](forum.md)
* [构思](ideation-feature.md)
* [问题与解答](working-with-qna.md)

將內容標示為精選內容後，即會在此元件中列出，可放置在特定的登陸頁面或容易吸引社群成員注意的區域。

每個元件可允許或不允許具備功能內容的功能。

本檔案的這一節將說明：

* 新增精選內容至社群網站。
* 的組態設定 `Featured Content` 元件。

## 新增精選內容至頁面 {#adding-featured-content-to-a-page}

若要新增 `Featured Content` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Featured Content`

並將其拖曳至應顯示精選內容的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-featured.md#essentials-for-client-side) 包含，這就是 `Featured Content` 元件將會出現：

![功能內容](assets/featuredcontent.png)

## 設定精選內容 {#configuring-featured-content}

選取已放置的 `Featured Content` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 設定索引標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤中，識別要功能的內容：

* **[!UICONTROL 显示名称]**

   精選內容清單的標題。 例如 `Featured Questions` 或 `Featured Ideas`. 預設為 `Featured Content` 若留空。

* **[!UICONTROL 专题内容的位置]**

   *（必要）* 瀏覽至包含可能特色內容的頁面（該頁面的元件必須設定為允許特色內容）。 例如：`/content/sites/engage/en/forum`。

* **[!UICONTROL 显示限制]**

   要顯示的最大精選內容數量。 預設值為5。

## 網站訪客體驗 {#site-visitor-experience}

將內容標幟為精選內容的功能需要版主許可權。

版主檢視張貼的內容時，可以存取內容內文版主旗標，包括新的 `Feature` 標幟。

![site-visitor-experience](assets/site-visitor-experience.png)

一旦標籤為功能，模組旗標就會變成 `Unfeature`.

包含 `Featured Content` 元件，現在將包含此文章。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 是實際貼文的連結。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [主要內容](essentials-featured.md) 適用於開發人員的頁面。

若要將內容標幟為精選，請參閱 [稽核使用者產生的內容](moderate-ugc.md).
