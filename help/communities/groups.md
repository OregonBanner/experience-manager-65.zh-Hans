---
title: 社区组控制台
seo-title: Community Groups Console
description: 群組控制檯可讓您建立社群群組
seo-description: Groups console lets you create Community groups
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# 社区组控制台 {#community-groups-console}

「群組」主控台提供在社群網站上的時建立社群群組的存取權。 [範本結構](/help/communities/sites-console.md#step1) 包含 [群組功能](/help/communities/functions.md#groups-function).

* AEM Communities支援在其他群組內巢狀內嵌群組。 群組巢狀可在以下情況下使用： [新群組的結構](/help/communities/tools-groups.md) 包含群組函式。
* 僅針對作者環境，有一個群組建立精靈，類似於網站建立精靈。
* 成員是否可以在發佈環境中建立群組，可以在將群組功能新增到社群網站結構或社群群組結構時進行設定。

包含的三個群組範本中，只有 `Reference Group` 範本在其結構中包含群組功能。

社群群組的不同面向包括：

* **建立**：新群組可在作者上建立，也可選擇在發佈執行個體上建立。
* **控制**：群組可以是開放或秘密。
* **巢狀**：群組可包含零個或多個群組。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此「群組」主控台只能從「社群網站」主控台存取，切勿與成員混淆 [群組主控台](/help/communities/members.md) 用於管理成員群組。
>
>成員群組是在發佈環境中註冊的使用者群組，並可使用從作者環境存取。 [通道服務](/help/communities/deploy-communities.md#tunnel-service-on-author).

## 组创建 {#group-creation}

若要存取「群組」主控台：

* 在作者上，以管理員許可權登入。
* 從全域導覽： **[!UICONTROL Communities]** > **[!UICONTROL 網站]**.
* 選取現有的社群網站資料夾以開啟。
* 在資料夾中選取社群網站的執行個體。

   * 社群網站的結構必須包含群組功能。
   * 這些熒幕擷取畫面來自下列專案之後的快速入門教學課程： [在發佈時建立群組](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* 選取 **群組資料夾** 以開啟。

   開啟時，所有現有群組（無論是在作者或發佈時建立）都會顯示。

   在此「群組」主控台中，可以編寫新群組。

   ![create-new-group](assets/create-new-group.png)

* 選取 **建立群組** 按鈕。

### 步驟1：社群群組範本 {#step-community-group-template}

![多語言社群群組](assets/multi-lingual-group.png)

* **社区组标题**

   群組的顯示標題。
標題會顯示在群組的已發佈網站上。

* **社区组描述**

   群組的說明。

* **社区组根路径**

   群組的根路徑。
預設根目錄為父網站，但根目錄可移至網站內的任何位置。 不建議進行變更。

* **其他可用的社群群組語言** 功能表

   使用下拉式清單來選取可用的社群群組語言。 功能表會顯示建立上層社群網站的所有語言。 使用者可以選取這些語言之一，以在此單一步驟中建立多個地區設定的群組。 在個別社群網站的「群組」主控台中，會以多種指定語言建立相同的群組。

* **社区组名称**

   顯示在URL中的群組根頁面名稱。 請避免在群組名稱中使用底線字元(_)和關鍵字（例如資源和設定）。

   * 請仔細檢查名稱，因為建立群組後不易變更。
   * 基底URL將顯示在 `Community Group Name`.
   * 對於有效的URL，附加「.html」
      *例如*， `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **社群群組範本** 功能表

   使用下拉式選單來選擇可用的 [社群群組範本](/help/communities/tools.md).

### 步驟2：設計 {#step-design}

### 社群群組主題 {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

框架使用 `Twitter Bootstrap` 為網站帶來回應式靈活設計。 可選擇預先載入的Bootstrap主題之一，以設定所選社群群組範本的樣式，或可上傳Bootstrap主題。

選取時，主題會以不透明的藍色勾號覆蓋。

您可以選取與父網站主題不同的主題。

社群網站發佈後，您可以 [編輯屬性](#modifyinggroupproperties) 並選取不同的主題。

### 社群群組品牌 {#community-group-branding}

![社群 — 群組 — 品牌](assets/community-group-branding.png)

社群網站品牌化是顯示為每個頁面頂端標題的影像。 可以顯示與其他網站頁面不同的群組橫幅。

影像大小應設定為和瀏覽器中頁面的預期顯示一樣寬，且高度為120畫素。

建立或選取影像時，請記住：

* 影像高度將會裁切成從影像上邊緣測量的120畫素
* 影像已釘選至瀏覽器視窗的左邊緣
* 不會調整影像大小，因此當影像寬度為：

   * 小於瀏覽器的寬度，影像將會水準重複。
   * 大於瀏覽器的寬度，影像看起來將會被裁切。

### 步驟3：設定 {#step-settings}

**稽核**

![選取社群群組成員角色](assets/group-admin.png)

**社区组版主**

依預設，會繼承父社群網站的版主清單。

可以新增群組特定的版主。 搜尋成員（從發佈環境）以將他們新增為版主

**组管理员**

依預設，父級社群網站管理員也是群組的管理員。

不過，也可以指派獨立的群組管理員。 群組管理員可以管理群組（例如G1），並在G1下建立巢狀的子群組。 他們可為子群組進一步指派不同的管理員。

因此，使用者U1可以是群組G1的管理員，也可以是巢狀群組G2的一般使用者。

**會籍**

成員資格設定允許從三種方式中選擇一種來保護社群群組。

![社群群組成員資格](assets/community-group-membership.png)

* **可选成员资格**

   如果選取，社群群組為公用群組。 網站成員可以加入群組並張貼，而無需明確加入群組。 預設值已選取。

* **必需成员资格**

   如果選取，則社群群組為開放群組。 社群網站成員可以檢視群組的內容，但需要加入群組才能發佈內容。 成員透過選取 `Join` 按鈕。 未選取預設。

* **受限制的成员资格**

   如果選取，則社群群組為機密群組。 必須明確邀請社群成員。 已邀請的成員會輸入搜尋方塊。 稍後可以使用新增成員 [成員和群組主控台](/help/communities/members.md) 作者環境。 未選取預設。

**缩略图**

![community-group-thumpail](assets/community-group-thumbnail.png)

縮圖是要在製作和發佈時為群組顯示的影像。

群組影像的最佳大小是支援的影像格式(例如JPG或PNG)為170 x 90畫素。

如果未新增任何影像，則會顯示預設影像。

![thumbnail-image](assets/thumbnail-image.png)

### 步驟4：建立群組 {#step-create-group}

![community-create-group](assets/community-create-group.png)

如果需要任何調整，請使用 **返回** 按鈕來進行變更。

一次 **建立** 選取並啟動，建立群組的程式無法中斷。

程式完成時，新子社群網站（群組）的卡片會顯示在「社群網站群組」主控台中，作者可以在其中新增頁面內容，管理員也可以修改網站的屬性。

![建立社群群組](assets/create-community-groups.png)

>[!NOTE]
>
>系統會使用中指定的所有語言建立群組 [步驟1：社群群組範本](/help/communities/groups.md#step-community-group-template) 在其他可用的社群群組語言中，位於個別社群網站的社群群組主控台中。

## 作者群組內容 {#author-group-content}

![open-site](assets/open-site.png)

群組的頁面內容可使用與任何其他AEM頁面相同的工具進行編寫。 若要開啟群組以進行編寫，請選取「開啟網站」圖示，將滑鼠游標停留在群組卡片上時就會顯示這個圖示。

## 修改群組屬性 {#modify-group-properties}

在社群群組建立過程中指定的現有子社群網站屬性，可以透過選取將游標停留在群組卡片上時顯示的「編輯網站」圖示來修改：

![edit-site](assets/edit-site.png)

下列屬性的詳細資訊與「 」中提供的說明相符 [群組建立](#group-creation) 區段。 可以修改任何巢狀群組，無論是在發佈環境或作者環境中建立。

![community-group-basic](assets/community-group-basic.png)

### 修改基本 {#modify-basic}

「基本」面板允許修改

* 社区组标题
* 社区组描述

社群群組名稱不可修改。

選擇不同的社群群組範本不會影響現有的社群群組網站，因為範本和網站之間沒有持續連線。

取而代之的是 [結構](#modify-structure) 可以修改子社群的。

### 修改結構 {#modify-structure}

「結構」面板可讓您修改最初從作者或發佈環境建立子社群網站時選取的社群群組範本建立的結構。 您可以從面板執行下列作業：

* 拖放其他專案 [社群功能](/help/communities/functions.md) 放入網站結構中。
* 在網站結構中的社群功能例項上：

   * **`Gear icon`**
編輯設定，包括顯示標題、URL和 [有特殊許可權的成員群組](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
從網站結構移除（刪除）函式。

   * **`Grid icon`**
修改網站頂層導覽列中顯示的函式順序。

>[!CAUTION]
>
>雖然顯示標題可以變更且沒有副作用，但建議您不要編輯屬於社群網站的社群功能的URL名稱。
>
>例如，重新命名URL不會移動現有UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>群組函式必須 *not* 成為 *第一個或唯一* 網站結構中的函式。
>
>任何其他函式，例如 [頁面函式](/help/communities/functions.md#page-function)，必須先包含並列出。

**範例：新增行事曆功能至子社群（群組）結構**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改設計 {#modify-design}

DESIGN面板允許修改主題：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您新增社群 [版主](#moderation).

### 修改成員資格 {#modify-membership}

此 [會籍](#membership) 面板僅供參考。 無法變更已建立的群組成員資格型別，無論是選擇性、必要或限制。

### 修改縮圖 {#modify-thumbnail}

此 [縮圖](#thumbnail) 面板可讓您上傳影像，以代表發佈環境中的社群群組以及作者環境中的Communities網站的「群組」主控台。

## 發佈群組 {#publish-the-group}

![publish-site](assets/publish-site.png)

建立或修改社群群組後，您可以選取 `Publish Site` 圖示。

成功發佈群組後，畫面會顯示訊息：

![group-published](assets/group-published.png)

>[!CAUTION]
>
>上層社群網站和上層群組應已發佈。
>
>社群網站和巢狀群組應以由上而下的方式發佈。

## 刪除群組 {#delete-the-group}

![刪除圖示](assets/deleteicon.png)

選取「刪除群組」圖示（將滑鼠懸停在群組上時出現），從社群群組主控台中刪除群組。

這會移除與群組相關聯的所有專案，例如，群組的所有內容會永久刪除，且使用者成員資格會從系統中移除。
