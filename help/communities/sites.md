---
title: 站点模板
seo-title: Site Templates
description: 如何存取網站範本主控台
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 4%

---

# 站点模板 {#site-templates}

「網站範本」主控台與 [群組範本](tools-groups.md) 主控台，著重於社群群組感興趣的功能。

>[!NOTE]
>
>用於建立的控制檯 [社群網站](sites-console.md)， [社群網站範本](sites.md)， [社群群組範本](tools-groups.md) 和 [社群功能](functions.md) 僅供作者環境使用。

## 網站範本主控台 {#site-templates-console}

在作者環境中，若要存取社群網站主控台：

* 從全域導覽： **[!UICONTROL 工具>社群>網站範本]**

此主控台會顯示 [社群網站](sites-console.md) 可建立並允許建立新的網站範本。

![site-template](assets/site-template.png)

## 创建站点模板 {#create-site-template}

若要開始建立新網站範本，請選取「 」 `Create`.

這會顯示包含3個子面板的網站編輯器面板：

### 基本資訊 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

在「基本資訊」面板上，會設定名稱、說明以及範本是啟用還是停用：

* **[!UICONTROL 社区站点模板名称]**

   範本名稱id。

* **[!UICONTROL 社区站点模板描述]**

   範本說明。

* **[!UICONTROL 已停用/已啟用]**

   控制範本是否可參照的切換開關。

### 缩略图 {#thumbnail}

![網站縮圖](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示，以顯示縮圖以及社群網站建立者的名稱和說明。

### 结构 {#structure}

![site-structure](assets/site-structure.png)

若要新增社群功能，請從右側拖曳至左側，順序為網站功能表連結的顯示順序。 在建立網站期間，樣式將套用至範本。

例如，如果您想要首頁，請從資料庫拖曳Page函式，放置於範本產生器下方。 這會導致頁面設定對話方塊開啟。 請參閱 [函式主控台](functions.md) 以取得有關設定對話方塊的資訊。

根據此範本，繼續拖放社群網站所需的任何其他社群功能。

頁面函式會提供一個空白頁面。 群組功能提供在社群網站內建立群組網站（子社群）的功能。

>[!CAUTION]
>
>群組函式必須 *not* 成為 *第一個或唯一* 網站結構中的函式。
>
>任何其他函式，例如 [頁面函式](functions.md#page-function)，必須先包含並列出。

![網站編輯器](assets/site-editor.png)

### 群組功能的群組範本 {#group-templates-for-groups-function}

在場地範本中加入群組功能時，設定需要當在發佈環境中建立新群組時允許群組範本選擇的規格。

>[!CAUTION]
>
>群組功能必須 *not* 成為 *第一個或唯一* 網站結構中的函式。

![網站函式](assets/site-functions.png)

選取兩個或多個社群群組範本，可在社群中實際建立新群組時，為群組管理員提供選項。

![網站功能](assets/site-functions1.png)

## 编辑站点模板 {#edit-site-template}

在主要內容中檢視網站範本時 [網站範本主控台](#site-templates-console)，即可選取現有網站範本進行編輯。

此程式提供的面板與 [建立網站範本](#create-site-template).
