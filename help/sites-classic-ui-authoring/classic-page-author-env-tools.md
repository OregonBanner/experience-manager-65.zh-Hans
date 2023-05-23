---
title: 製作 — 環境與工具
description: 「網站」主控台可讓您管理和導覽您的網站。 使用兩個窗格，可以展開網站的結構並對所需元素採取動作。
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 5%

---

# 製作 — 環境與工具 {#authoring-the-environment-and-tools}

AEM 的创作环境提供了各种可用于组织和编辑内容的机制. 可以从各种控制台和页面编辑器访问提供的工具。

## 網站管理 {#site-administration}

此 **網站** 主控台可讓您管理和導覽您的網站。 使用這兩個窗格，可以展開您網站的結構並對所需元素採取的動作：

![chlimage_1-108](assets/chlimage_1-108.png)

## 編輯您的頁面內容 {#editing-your-page-content}

有一個單獨的頁面編輯器搭配傳統UI，使用內容尋找器和Sidekick：

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## 访问帮助 {#accessing-help}

各種 **說明** 資源可從AEM內直接存取：

以及存取 [主控台工具列的說明](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)，您也可以存取sidekick的協助(使用？ 圖示)編輯頁面時：

![](do-not-localize/sidekick-collapsed-2.png)

或透過使用 **說明** 按鈕；這將顯示上下文相關說明。

## Sidekick {#sidekick}

此 **元件** sidekick的索引標籤可讓您瀏覽可新增到目前頁面的元件。 您可以展開所需群組，然後將元件拖曳至頁面上的所需位置。

![chlimage_1-110](assets/chlimage_1-110.png)

## 內容尋找器 {#the-content-finder}

內容尋找器是在編輯頁面時，在存放庫中快速輕鬆地尋找資產和/或內容。

您可以使用內容尋找器來尋找一系列資源。 您可以視情況將專案拖放至頁面上的段落中：

* [图像](#finding-images)
* [文档](#finding-documents)
* [电影](#finding-movies)
* [Dynamic Media瀏覽器](/help/sites-administering/scene7.md#scene7contentbrowser)
* [页面](#finding-pages)

* [段落](#referencing-paragraphs-from-other-pages)
* [产品](#products)
* 或至 [依存放庫結構瀏覽網站](#the-content-finder)

使用所有選項，您可以 [搜尋特定專案](#the-content-finder).

### 尋找影像 {#finding-images}

此索引標籤會列出存放庫中的所有影像。

在頁面上建立「影像」段落後，您可以將專案拖放到段落中。

![chlimage_1-111](assets/chlimage_1-111.png)

### 尋找檔案 {#finding-documents}

此索引標籤會列出存放庫中的所有檔案。

在頁面上建立「下載」段落後，您可以將專案拖放到段落中。

![chlimage_1-112](assets/chlimage_1-112.png)

### 尋找影片 {#finding-movies}

此索引標籤會列出存放庫中的所有影片(例如Flash專案)。

在頁面上建立適當的段落(例如Flash)後，您可以將專案拖放到段落中。

![chlimage_1-113](assets/chlimage_1-113.png)

### 产品 {#products}

此索引標籤會列出所有產品。 在頁面上建立適當的段落（例如「產品」）後，您可以將專案拖放到段落中。

![chlimage_1-114](assets/chlimage_1-114.png)

### 尋找頁面 {#finding-pages}

此索引標籤會顯示所有頁面。 連按兩下任何頁面以開啟它進行編輯。

![chlimage_1-115](assets/chlimage_1-115.png)

### 引用其他頁面的段落 {#referencing-paragraphs-from-other-pages}

此索引標籤可讓您搜尋其他頁面。 將會列出該頁面中的所有段落。 然後您可以將段落拖曳到目前頁面，這樣會建立原始段落的參照。

![chlimage_1-116](assets/chlimage_1-116.png)

### 使用完整存放庫檢視 {#using-the-full-repository-view}

此索引標籤會顯示存放庫中的所有資源。

![chlimage_1-117](assets/chlimage_1-117.png)

### 搭配內容瀏覽器使用搜尋 {#using-search-with-the-content-browser}

在所有選項上，您可以搜尋特定專案。 以下列出符合搜尋模式的任何標籤和所有資源：

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

您也可以使用萬用字元進行搜尋。 支援的萬用字元包括：

* `*`
符合零或更多字元的順序。

* `?`
符合單一字元。

>[!NOTE]
>
>虛擬屬性「name」必須用來執行萬用字元搜尋。

例如，如果存在名稱為的可用影像：

`ad-nmvtis.jpg`

下列搜尋模式會找到它（以及符合該模式的任何其他影像）：

* `name:*nmv*`
* `name:AD*`
字元比對為 *not* 區分大小寫。

* `name:ad?nm??is.*`
您可以在查詢中使用任意數量的萬用字元。

>[!NOTE]
>
>您也可以使用 [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) 搜尋。

## 顯示引用 {#showing-references}

AEM可讓您檢視哪些頁面連結至您目前正在處理的頁面。

若要顯示直接頁面參照：

1. 在sidekick中，選取 **頁面** 標籤圖示。

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. 選取 **顯示參考……** AEM會開啟「參照」視窗，並顯示參照所選頁面的頁面，包括其路徑。

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

在某些情況下，可以從Sidekick執行進一步動作，包括：

* [启动项](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copy](/help/sites-administering/msm.md)

* [Blueprint](/help/sites-administering/msm-best-practices.md)

其他 [可以在網站主控台中檢視頁面間關係](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## 审查日志 {#audit-log}

此 **稽核記錄** 可從以下位置存取： **資訊** 索引標籤。 它列出在目前頁面上採取的最近動作；例如：

![chlimage_1-118](assets/chlimage_1-118.png)

## 页面信息 {#page-information}

網站主控台也 [提供有關頁面目前狀態的資訊](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) 例如發佈、修改、鎖定、即時副本等。

## 頁面模式 {#page-modes}

使用傳統UI編輯頁面時，可使用Sidekick底部的圖示來存取各種模式：

![](do-not-localize/chlimage_1-12.png)

Sidekick底部的圖示列可用來切換使用頁面的模式：

* [編輯](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
這是預設模式，可讓您編輯頁面、新增或刪除元件並進行其他變更。

* [預覽](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
此模式可讓您預覽頁面，就像頁面以最終形式出現在您的網站上。

* [設計](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
在此模式中，您可以設定可存取的元件，以編輯頁面的設計。

>[!NOTE]
>
>也可使用其他選項：
>
>* [基架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* 網站 — 將開啟網站主控台。
>* 重新載入 — 將重新整理頁面。


## 键盘快捷键 {#keyboard-shortcuts}

可以使用各种[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。
