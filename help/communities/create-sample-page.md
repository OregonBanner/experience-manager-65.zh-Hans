---
title: 建立範例頁面
seo-title: Create a Sample Page
description: 建立範例社群網站
seo-description: Create a Sample community site
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 建立範例頁面 {#create-a-sample-page}

自AEM 6.1 Communities起，建立範例頁面的最簡單方式是建立簡單的社群網站，由Page函陣列成。

這將包括parsys元件，以便您可以 [啟用元件以供編寫](basics.md#accessing-communities-components).

使用範例元件進行探索的另一個選項是使用 [社群元件指南](components-guide.md).

## 建立社群網站 {#create-a-community-site}

這非常類似於建立中所述的新網站 [AEM Communities快速入門](getting-started.md).

主要差異在於此教學課程將建立新的社群網站範本，其中僅包含 [Page函式](functions.md#page-function) 以建立不含其他功能的簡單社群網站（除了所有社群網站的基本預先有線功能）。

### 建立新網站範本 {#create-new-site-template}

若要開始使用，請建立 [社群網站範本](sites.md).

從作者執行個體的全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 網站範本]**.

![create-site-template](assets/create-site-template1.png)

* 选择 `Create button`
* 基本資訊

   * `Name`：單頁範本
   * `Description`：由單頁函陣列成的範本。
   * 选择 `Enabled`

![site-template-editor](assets/site-template-editor.png)

* 結構

   * 拖曳 `Page` 範本產生器的函式
   * 如需組態功能詳細資訊，請輸入

      * `Title`：單頁
      * `URL`: 页

![site-template-editor-structure](assets/site-template-editor1.png)

* 選取 **`Save`** 用於設定
* 選取 **`Save`** 適用於網站範本

### 建立新社群網站 {#create-new-community-site}

現在根據簡單的網站範本建立新的社群網站。

建立網站範本後，從全域導覽選取 **[!UICONTROL 社群>網站]**.

![create-community-site](assets/create-community-site1.png)

* 選取 **`Create`** 圖示

* 步骤 `1 - Site Template`

   * `Title`：簡單社群網站
   * `Description`：包含實驗所需單一頁面的社群網站。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`：範例

      * url = http://localhost:4502/content/sites/sample

      * `Template`：選擇 `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* 选择 `Next`
* 步骤 `2 - Design`

   * 選取任何設計

* 选择 `Next`
* 选择 `Next`

   （接受所有預設設定）

* 选择 `Create`

   ![create-community-site](assets/create-community-site.png)

## 發佈網站 {#publish-the-site}

![publish-site](assets/publish-site.png)

從 [社群網站主控台](sites-console.md)，選取發佈圖示以發佈網站，預設為http://localhost:4503。

## 在編輯模式下開啟作者網站 {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

選取開啟網站圖示以在編輯模式下檢視網站。

URL將會是 [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

在簡單首頁上，您可以透過社群功能和範本檢視預先佈線的內容，並嘗試新增和設定社群元件。

## 在發佈時檢視網站 {#view-site-on-publish}

發佈頁面後，請開啟 [發佈執行個體](http://localhost:4503/content/sites/sample/en.html) 以匿名網站訪客、登入會員或管理員身分來實驗功能。 除非管理員登入，否則作者環境中可見的管理連結不會出現在發佈環境中。
