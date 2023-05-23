---
title: 组模板
seo-title: Group Templates
description: 如何存取群組範本主控台
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 组模板 {#group-templates}

「群組範本」控制檯類似於 [網站範本](/help/communities/sites.md) 主控台。 兩者都是組成社群網站的一組預佈線頁面和功能的藍圖。 不同之處在於網站範本適用於主要社群，而群組範本適用於社群群組，即巢狀內建於主要社群的子社群。

社群群組是透過包含 [群組功能](/help/communities/functions.md#groups-function) （這並非範本中的第一個或唯一函式）。

截至社群 [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack)，可在群組範本中加入「群組」功能以巢狀內嵌群組。

執行動作建立新社群群組時，即會選取該群組的範本（結構）。 選取範圍取決於群組新增至網站或群組範本時的設定方式。

>[!NOTE]
>
>用於建立的控制檯 [社群網站](/help/communities/sites-console.md)， [社群網站範本](/help/communities/sites.md)， [社群群組範本](/help/communities/tools-groups.md) 和 [社群功能](/help/communities/functions.md) 僅供作者環境使用。

## 群組範本主控台 {#group-templates-console}

若要存取AEM作者環境中的「群組範本」主控台：

* 選取 **工具 |社群 |群組範本，** 從全域導覽。

此主控台會顯示 [社群網站](/help/communities/sites-console.md) 可建立並允許建立新的群組範本。

![社群群組範本](assets/groups-template.png)

## 创建组模板 {#create-group-template}

若要開始建立新的群組範本，請選取 `Create`.

這會顯示包含3個子面板的網站編輯器面板：

### 基本信息 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在「基本資訊」面板上，會設定名稱、說明以及範本是啟用還是停用：

* **新组模板名称**

   範本名稱id。

* **描述**

   範本說明。

* **已停用/已啟用**

   控制範本是否可參照的切換開關。

#### 缩略图 {#thumbnail}

![網站縮圖](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示以顯示縮圖，以及社群網站建立者的名稱和說明。

#### 结构 {#structure}

>[!CAUTION]
>
>如果使用AEM 6.1 Communities FP4或更舊版本，請勿將群組函式新增至群組範本。
>
>巢狀群組功能自Communities起即可使用 [FP1](/help/communities/communities.md#latestfeaturepack).
>
>仍不允許將「群組」函式新增為範本中的第一個或唯一函式。

![群組範本編輯器](assets/template-editor.png)

若要新增社群功能，請從右側拖曳至左側，順序為網站功能表連結的顯示順序。 在建立網站期間，樣式將套用至範本。

例如，如果您想要論壇，請從資料庫拖曳論壇功能，然後放置於範本產生器下。 這會導致論壇設定對話方塊開啟。 請參閱 [函式主控台](/help/communities/functions.md) 以取得有關設定對話方塊的資訊。

根據此範本，繼續拖放子社群網站（群組）所需的任何其他社群功能。

![拖曳函式](assets/dragfunctions.png)

將所有需要的函式放入範本產生器區域並設定後，選取 **儲存** 右上角。

## 编辑组模板 {#edit-group-template}

在主要內容中檢視社群群組時 [群組範本主控台](#group-templates-console)，即可選取要編輯的現有群組範本。

編輯群組範本不會影響已從範本建立的社群網站。 您可以直接 [編輯社群網站](/help/communities/sites-console.md#modify-structure)的結。

此程式提供的面板與 [建立群組範本](#create-group-template).
