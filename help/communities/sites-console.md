---
title: 社群網站主控台
seo-title: Communities Sites Console
description: 如何存取社群網站主控台
seo-description: How to access the Communities Sites console
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 4%

---

# 社群網站主控台 {#communities-sites-console}

社群網站主控台提供下列專案的存取權：

* 網站建立
* 網站編輯
* 網站管理
* [建立和編輯巢狀群組](/help/communities/groups.md) （子社群）

另請參閱 [AEM Communities快速入門](/help/communities/getting-started.md) 體驗在製作環境中建立社群網站的速度有多快，以及如何從製作和發佈環境建立社群群組。

>[!NOTE]
>
>用於建立的主要Communities功能表 [社群網站](/help/communities/sites-console.md)， [社群網站範本](/help/communities/sites.md)， [社群群組範本](/help/communities/tools-groups.md) 和 [社群功能](/help/communities/functions.md) 僅供作者環境使用。

## 前提条件 {#prerequisites}

在建立社群網站之前，請先 *必填* 至：

* 請確定一個或多個發佈執行個體正在執行。
* 啟用 [通道服務](/help/communities/deploy-communities.md#tunnel-service-on-author) 以管理成員和成員群組。
* 識別 [主要發行者](/help/communities/deploy-communities.md#primary-publisher).
* [設定復寫](/help/communities/deploy-communities.md#replication-agents-on-author) 主要發行者連線埠不是預設值(4503)時。

為確保網站準備好支援許多功能，最佳實務是採取下列步驟：

* 安裝 [最新feature pack](/help/communities/deploy-communities.md#latestfeaturepack).
* 啟用 [Adobe Analytics](/help/communities/analytics.md) 適用於AEM Communities。
* 設定 [電子郵件](/help/communities/email.md)
* 識別 [社群管理員](/help/communities/users.md#creating-community-members).
* [啟用OAuth處理常式](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 用於社交登入。

## 存取社群網站主控台 {#accessing-communities-sites-console}

在製作環境中，若要存取Communities Sites主控台：

* 從全域導覽： **[!UICONTROL Communities]** > **[!UICONTROL 網站]**

社群網站主控台會顯示任何現有的社群網站。 您可以在此主控台建立、編輯、管理及刪除社群網站。

若要建立新的社群網站，請選取 **建立** 圖示。

若要存取現有的社群網站，以便編寫、修改、發佈、匯出或新增巢狀群組，請選取網站的資料夾圖示。

## 站点创建 {#site-creation}

網站建立主控台提供根據所選物件來組裝網站特徵的逐步方法 [社群網站範本](/help/communities/sites.md) 和設定。

每個建立的網站都包含登入功能，因為網站訪客必須先登入，才能發佈內容、傳送訊息或參與群組。 其他包含的功能包括使用者設定檔、傳訊、通知、網站功能表、搜尋、主題設定和品牌化。

透過選取 `Create` 按鈕的位置。

建立過程是作為面板顯示的一系列步驟，其中包含要配置的一組特徵（顯示為子面板）。 您可以前往 **下一個** 步驟或 **返回** 到最後一個步驟中認可網站之前的上一個步驟。

### 步驟1 ：網站範本 {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

在「網站範本」面板上，指定標題、說明、網站根目錄、基本語言、名稱和網站範本：

* **社区站点标题**

   網站的顯示標題。

   標題會顯示在已發佈的網站以及網站管理員UI中。

* **社区站点描述**

   網站說明。

   說明未出現在已發佈的網站上。

* **社群網站根目錄**

   網站的根路徑。

   預設根目錄為 `/content/sites`，但根可移至網站內的任何位置。

* **社区站点基本语言**

   （單一語言則保持原樣：英文）使用下拉式功能表選擇一個語言 *或更多* 可用語言提供的基礎語言 — 德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和中文（簡體）。 將會針對新增的每種語言建立一個社群網站，並會遵循中所述的最佳實務存在於相同的網站資料夾中 [翻譯多語言網站的內容](/help/sites-administering/translation.md). 每個網站的根頁面都會包含子頁面，其名稱為所選語言之一的語言代碼，例如「en」代表英文，「fr」代表法文。

* **社区站点名称**:

   顯示在URL中的網站根頁面名稱。

   * 請仔細檢查名稱，因為網站建立後不易變更。
   * 基底URL ( `https://server:port/site root/site name)` 將會顯示在 `Community Site Name`.

   * 若要取得有效的URL，請附加基本語言代碼+ &quot;。html&quot;

      *例如*， `https://localhost:4502/content/sites/mysight/en.html`

* **社群網站範本** 功能表

   使用下拉式功能表選擇可用的 [社群網站範本](/help/communities/tools.md).

* 选择&#x200B;**下一步**。

### 步驟2 ：設計 {#step-design}

「設計」面板包含2個子面板，用於選取主題和品牌橫幅：

#### 社群網站主題 {#community-site-theme}

![sitetheme](assets/sitetheme.png)

框架使用 `Twitter Bootstrap` 為網站帶來回應式靈活設計。 可選擇許多預先載入的Bootstrap主題之一來設定所選社群網站範本的樣式，或可上傳Bootstrap主題。

選取時，主題會以不透明的藍色核取記號覆蓋。

社群網站發佈後，您可以 [編輯屬性](#modifying-site-properties) 並選取不同的主題。

#### 社群網站品牌化 {#community-site-branding}

![網站品牌](assets/site-branding.png)

社群網站品牌化是顯示為每個頁面頂端標題的影像。

影像大小應設定為和瀏覽器中頁面的預期顯示一樣寬，且高度為120畫素。

建立或選取影像時，請記住：

* 影像高度將會裁切成從影像頂端邊緣測量的120畫素。
* 影像已釘選至瀏覽器視窗的左邊緣。
* 不會調整影像大小，因此當影像寬度為……

   * 小於瀏覽器的寬度，影像將會水準重複。
   * 大於瀏覽器的寬度，影像看起來將會被裁切。

* 选择&#x200B;**下一步**。

### 步驟3：設定 {#step-settings}

「設定」面板包含數個子面板，顯示了在移至建立網站的最後一步之前要設定的功能。

* [USER MANAGEMENT](#user-management)
* [標籤](#tagging)
* [角色](#roles)
* [稽核](#moderation)
* [ANALYTICS](#analytics)
* [翻譯](#translation)

>[!NOTE]
>
>**啟用通道服務**
>
>有幾個「設定」子面板允許指派受信任的成員來稽核UGC、管理群組或成為發佈環境中啟用資源的聯絡人。
>
>慣例適用於發佈端 [使用者與使用者群組](/help/communities/users.md) （成員和成員群組）。
>
>因此，在製作環境中建立社群網站，並將受信任的成員指派給各種角色時，必須從發佈環境中擷取成員資料。
>
>這是透過啟用 ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` 用於製作環境。

#### USER MANAGEMENT {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **允许用户注册**

   若勾選，網站訪客可透過自助註冊成為社群成員。
如果未勾選，社群網站會是 *受限制* 和網站訪客必須指派給社群網站的成員群組、提出請求或透過電子郵件傳送邀請。 如果未勾選，則不應允許匿名存取。
取消勾選 *私人* 社群網站。 預設為已核取。

* **允许匿名访问**

   如果勾選，社群網站為*open *且任何網站訪客都可以存取該網站。
如果未勾選，則只有已登入的成員才能存取該網站。
取消勾選*private *community網站。 預設為已核取。

* **允许发送消息**

   如果勾選，成員可以相互傳送訊息給群組，也可以傳送訊息給社群網站內的群組。
如果未勾選，則不會為社群設定傳訊。
預設為未勾選。

* **允许社交登录: Facebook**

   如果勾選，則允許網站訪客使用其Facebook帳戶憑證登入。 選取的 [facebook雲端設定](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) 建立社群網站後，應設定為將使用者新增至社群網站的成員群組。
如果未勾選，則不會顯示任何Facebook登入。
取消勾選 *私人* 社群網站。 預設為未勾選。

* **允许社交登录: Twitter**

   如果勾選，則允許網站訪客使用其Twitter帳戶憑證登入。 選取的 [twitter雲端設定](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) 建立社群網站後，應設定為將使用者新增至社群網站的成員群組。
如果未勾選，則不會顯示任何Twitter登入。
取消勾選 *私人* 社群網站。 預設為未勾選。

>[!NOTE]
>
>**允許社交登入**
>
>雖然範例Facebook和Twitter設定可能存在且可供選取，但對於 [生產環境](/help/sites-administering/production-ready.md)，您必須建立自訂Facebook和Twitter應用程式。 另請參閱 [使用Facebook和Twitter進行社交登入](/help/communities/social-login.md).

#### 標籤 {#tagging}

![網站標籤](assets/site-tagging.png)

可套用至社群內容的標籤是透過選取先前透過定義的標籤名稱空間來控制的 [標籤主控台](/help/sites-administering/tags.md#tagging-console).

此外，為社群網站選取標籤名稱空間會限制定義目錄和資源時顯示的選取範圍。

* 文字搜尋方塊：開始輸入以識別允許用於網站上的標籤。

#### 角色 {#roles}

![社群角色](assets/site-admin-2.png)

此 [社群成員的角色](/help/communities/users.md) 會指派這些設定。

使用預先輸入搜尋可輕鬆尋找社群成員。

* **社区管理员**

   開始輸入以選取一個或多個可管理社群成員和成員群組的社群成員或成員群組。

* **社区审查方**

   開始輸入以選取一或多個社群成員或成員群組，這些成員或成員群組將被信任為使用者產生內容的版主。

* **拥有权限的社区成员**

   開始輸入以選取一個或多個社群成員或成員群組，以便在下列情況下建立新內容 `Allow Privileged Member` 已為「 」選取 [社群功能](/help/communities/functions.md).

* **社区管理员**

   開始輸入以選取一個或多個可以獨立於其他網站管理員和預設社群管理員來處理網站結構的網站管理員。 他們可以在階層架構的任何層級建立群組，並成為巢狀群組的預設管理員（但他們稍後可以從巢狀群組的管理員角色中移除）。

#### 稽核 {#moderation}

![網站稽核](assets/site-moderation.png)

用於仲裁使用者產生內容(UGC)的全域設定是由這些設定所控制。 個別元件具有控制稽核的其他設定。

* **内容已通过预审**

   如果勾選，張貼的社群內容必須等到版主核准後才會顯示。 預設為未勾選。 如需詳細資訊，請參閱 [仲裁社群內容](/help/communities/moderate-ugc.md#premoderation).

* **标记阈值，达到此值后隐藏内容**

   如果大於0，則在從公開檢視隱藏主題或貼文之前，必須將其標籤的次數。 如果設為–1，則已標幟的主題或貼文絕不會從公開檢視中隱藏。 預設值為5。

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **启用 Analytics**

   僅當Adobe Analytics已 [已設定](/help/communities/analytics.md) 用於Communities功能。
預設為未勾選。 勾選後，會出現其他選取功能表：

![site-analytics-enable](assets/site-analytics-enable.png)

* **云配置框架引用**

   從下拉式選單中，選取為此社群網站設定的Analytics雲端服務架構。
   `Communities` 是來自的架構範例 [Communities功能的Analytics設定](/help/communities/analytics.md#aem-analytics-framework-configuration) 說明檔案。

#### 翻譯 {#translation}

![網站翻譯](assets/site-translation.png)

* **允许机器翻译**

   核取後（預設為未核取），網站內的UGC會啟用機器翻譯。 這不會影響任何其他內容，例如頁面內容，即使網站設定為多語言網站亦然。 另請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md) 以取得為AEM Communities設定授權翻譯服務的相關資訊。 另請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 以取得完整的總覽。

![allow-machine-translation](assets/allow-machine-translation.png)

* **为选定的语言启用机器翻译**

   為機器翻譯啟用的語言預設為指定的系統設定 [翻譯整合設定](/help/communities/translate-ugc.md#translation-integration-configuration). 您可透過刪除預設值和/或從下拉式選單中選取其他語言來覆寫此網站的這些預設設定。

* **选择翻译提供商**

   依預設，服務提供者為試用服務，使用 `microsoft` 僅供示範。 如果沒有授權翻譯服務提供者， **允許機器翻譯** 應取消勾選。

* **选择全球共享商店**

   對於擁有多個語言副本的網站，全域共用商店會提供單一對話對話對話對話串，從每個語言副本中可見。 這是透過選取語言副本中包含的語言之一來達成。 預設為 *無全域共用存放區*.

* **选择翻译提供商配置**

   選擇 [翻譯整合框架](/help/sites-administering/tc-tic.md) 已為授權的翻譯提供者建立。

* **为您的社区站点选择翻译选项**

   * **翻译整个页面**

      如果選取，頁面上的所有UGC都會轉譯為頁面的基本語言。

      預設為 *未選取*.

   * **仅翻译选定内容**

      如果選取，每個貼文旁都會顯示翻譯選項，可將個別貼文翻譯成頁面的基本語言。
預設為 *已選取*.

* **选择持久性选项**

   * **翻譯使用者要求的貢獻並於之後持續**
如果選取，則在提出請求之前不會翻譯內容。 翻譯完成後，翻譯會儲存在存放庫中。

      預設為 *未選取*.

   * **不持續翻譯**

      如果選取，翻譯將不會儲存在存放庫中。

      如果未選取，則會持續翻譯。

      預設為 *未選取*.

* **智能渲染**

   選取下列其中一項：

   * `Always show contributions in the original language`（默认）
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### 步驟4 ：建立社群網站 {#step-create-communities-site}

如果需要任何調整，請使用 **返回** 按鈕來進行變更。

一次 **建立** 選取並啟動，建立網站的程式無法中斷。

建立網站後：

* 不支援變更url （節點名稱）。
* 社群網站範本的未來變更不會影響已建立的社群網站。
* 停用社群網站範本不會影響已建立的社群網站。
* 您可以編輯 [結構](#modify-structure) 修改其屬性以建立社群網站。

![create-site](assets/create-site1.png)

程式完成時，新網站的資料夾會顯示在Communities Sites主控台中，作者可在其中新增頁面內容，管理員則可修改網站的屬性。

![modify-site-property](assets/modify-site-property.png)

若要修改社群網站，請選取其專案資料夾以開啟它：

![site-project](assets/site-project.png)

使用滑鼠將滑鼠游標停留在網站上或接觸網站卡片時，會出現圖示，允許 [在作者模式下編輯網站](#authoring-site-content)， [開啟網站屬性以進行修改](#modifying-site-properties)， [發佈網站](#publishing-the-site)， [匯出網站](#exporting-the-site)、和 [刪除網站](#deleting-the-site).

## 製作網站內容 {#authoring-site-content}

可以使用與任何其他AEM網站相同的工具來編寫網站內容。 若要開啟網站進行編寫，請選取 `Open Site` 圖示顯示在滑鼠懸停網站上。 網站將在新標籤中開啟，以便Communities Sites主控台保持可存取狀態。

![site-content](assets/site-content.png)

>[!NOTE]
>
>若不熟悉AEM，請檢視以下說明檔案： [基本處理](/help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](/help/sites-authoring/qg-page-authoring.md).

## 修改場地屬性 {#modifying-site-properties}

![edit-site](assets/edit-site.png)

在場地建立過程中指定的現有場地屬性，可以透過選取 `Edit Site`圖示顯示在滑鼠懸停網站上。

`Details of the following properties match the descriptions provided in the` [網站建立](#site-creation) 區段。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本 {#modify-basic}

「基本」面板允許修改：

* 社区站点标题
* 社区站点描述

社群網站名稱不可修改。

選擇不同的社群網站範本不會影響現有的社群網站，因為範本和網站之間沒有連線。

取而代之的是 [結構](#modify-structure) 可修改社群網站的「 」。

### 修改結構 {#modify-structure}

「結構」面板允許修改最初從所選社群網站範本建立的結構。 您可以從面板執行下列作業：

* 拖放其他專案 [社群功能](/help/communities/functions.md) 放入網站結構中。
* 在網站結構中的社群功能例項上：

   * **`gear icon`**

      編輯設定，包括顯示標題和URL名稱*以及 [有特殊許可權的成員群組](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

      從網站結構移除（刪除）函式。

   * **`grid icon`**

      修改網站最上層導覽列中顯示的函式順序。

>[!NOTE]
>
>您可以變更「場地結構」中所有函式的順序，但頂端的函式除外。 因此，無法變更Communities網站首頁。

>[!CAUTION]
>
>* 雖然顯示標題可能會變更且沒有副作用，但建議您不要編輯屬於社群網站的社群功能的URL名稱。
>
>例如，重新命名URL不會移動現有UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>群組函式必須 *not* 成為 *第一個或唯一* 網站結構中的函式。
>
>任何其他函式，例如 [頁面函式](/help/communities/functions.md#page-function)，必須先包含並列出。

#### 範例：新增目錄函式至社群網站結構 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改設計 {#modify-design}

「設計」面板可套用新主題：

* [社区站点主题](#community-site-theme)
* [社区站点品牌化](#community-site-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您存取子面板下的大部分設定，這些子面板用於建立社群網站的步驟3：

* [用户管理](#user-management)
* [标记](#tagging)
* [审核](#moderation)
* [成员角色](#roles)
* [分析](#analytics)
* [翻译](#translation)

### 修改縮圖 {#modify-thumbnail}

「縮圖」面板可讓您上傳影像，以在Communities Sites主控台中代表網站。

## 發佈網站 {#publishing-the-site}

建立或修改社群網站後，可以透過選取 `Publish Site` 圖示，此圖示會出現在滑鼠停留在場地上。

![publish-site](assets/publish-site.png)

網站成功發佈後，將會顯示提示。

![site-published](assets/site-published.png)

### 使用巢狀群組發佈 {#publishing-with-nested-groups}

發佈社群網站後，有必要個別發佈使用建立的每個子社群（巢狀群組）。 [群組主控台](/help/communities/groups.md).

## 匯出網站 {#exporting-the-site}

![export-site](assets/export-site.png)

將滑鼠停留在網站上，選取匯出圖示，以建立同時儲存在中的社群網站套件 [封裝管理員](/help/sites-administering/package-manager.md) 並下載。

請注意，UGC未包含在網站套件中。

## 刪除網站 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

若要刪除社群網站，請選取將滑鼠游標停留在Communities網站主控台的網站上方時顯示的刪除網站圖示。 此動作會移除與網站相關聯的所有專案，例如UGC、使用者群組、資產和資料庫記錄。

## 已建立的社群使用者群組 {#created-community-user-groups}

發佈新社群網站後，新成員群組（在發佈環境中建立使用者群組）將擁有針對各種管理和成員角色設定的適當許可權。

為成員群組建立的名稱包括 *site-name* 指定網站於 [步驟1](#step13asitetemplate) （出現在URL中的名稱）以及唯一ID，以避免與不同社群網站根目錄具有相同網站名稱的社群網站和群組發生衝突。

例如，如果名稱為「Getting Started Tutorial」的網站為「engage」，則版主的使用者群組將是：

* title：社群參與版主
* 名稱： community-*engage-uid* — 版主

請注意，在建立場地時，任何指派為版主或群組管理員角色的成員，都會指派給適當的群組，也會指派給成員群組。 發佈新網站時，會在發佈時建立這些群組和成員指派。

如需詳細資訊，請參閱 [管理使用者和使用者群組](/help/communities/users.md).

>[!NOTE]
>
>若 [允許社交登入： Facebook](#user-management) 已啟用，一旦使用者群組
>
>* `community-<site-name>-<uid>-members`
>
>已建立，已套用 [facebook雲端服務](/help/communities/social-login.md#createafacebookcloudservice) 應設定為新增使用者至此群組。

## 設定驗證錯誤 {#configure-for-authentication-error}

依預設，當使用者輸入錯誤的憑證且無法登入時，社群網站將重新導向至範例登入頁面。 此範例登入將不會出現在 [生產伺服器](/help/sites-administering/production-ready.md).

若要正確重新導向，在設定網站並推送至發佈後，請完成以下步驟以取得驗證失敗，重新導向至社群網站：

* 在每個AEM發佈執行個體上。
* 以管理員許可權登入。
* 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md).

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* 尋找 `Adobe Granite Login Selector Authentication Handler`.
* 選取 `pencil` 圖示以開啟設定進行編輯。
* 輸入 **登入頁面對應** 如下所示：

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 选择&#x200B;**保存**。

![auth-error](assets/auth-error.png)

### 測試驗證重新導向 {#test-authentication-redirection}

在設定了社群網站登入頁面對應的相同AEM發佈執行個體上：

* 瀏覽至社群網站首頁。

   * 例如， [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 選取「登出」。
* 選取「登入」。
* 輸入明顯不正確的認證，例如使用者名稱&quot;x&quot;和密碼&quot;x&quot;。
* 登入頁面應顯示「無效登入」錯誤。

![測試驗證](assets/test-authentication.png)

## 從主要網站主控台存取社群網站 {#accessing-community-sites-from-main-sites-console}

從全域導覽Sites主控台，社群網站位於 `Community Sites` 資料夾。

雖然可以這種方式存取社群網站，但針對管理任務，社群網站應從「社群網站」主控台存取。

![access-site](assets/access-site.png)
