---
title: 撰寫新社群網站
seo-title: Author a New Community Site
description: 如何撰寫新的AEM Communities網站
seo-description: How to author a new AEM Communities site
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# 撰寫新社群網站{#author-a-new-community-site}

## 建立社群網站 {#create-a-community-site}

使用作者例項建立社群網站。 在AEM作者執行個體上：

1. 以管理員許可權登入。
1. 從全域導覽，前往 **[!UICONTROL Communities]** > **[!UICONTROL 網站]**.

Communities Sites主控台會提供精靈，引導使用者完成建立社群網站的步驟。 您可以前往 `Next` 步驟或 `Back` 到最後一個步驟中認可網站之前的上一個步驟。

若要開始建立新的社群網站：

* 選取 `Create` 按鈕。

![createcommunitysite](assets/createcommunitysite.png)

### 步驟1：網站範本 {#step-site-template}

![建立網站的範本](assets/create-site.png)

於 [網站範本步驟](/help/communities/sites-console.md#step2013asitetemplate)，輸入URL的標題、說明和名稱，然後選取社群網站範本，例如：

* **社区站点标题**: `Getting Started Tutorial`
* **社区站点描述**: `A site for engaging with the community.`
* **社群網站根目錄**：(預設根保留空白 `/content/sites`)
* **雲端設定**：（若未指定雲端設定，則保留空白）提供指定雲端設定的路徑。
* **社群網站基本語言**：（單一語言則保持原樣：英文）使用下拉式清單來選擇一種語言 *或更多* 可用語言提供的基礎語言 — 德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和中文（簡體）。 將會針對新增的每種語言建立一個社群網站，並會遵循中所述的最佳實務存在於相同的網站資料夾中 [翻譯多語言網站的內容](/help/sites-administering/translation.md). 每個網站的根頁面都會包含子頁面，其名稱為所選語言之一的語言代碼，例如「en」代表英文，「fr」代表法文。

* **社群網站名稱**：參與

   * 請仔細檢查名稱，因為網站建立後不易變更
   * 初始URL將顯示在社群網站名稱下方
   * 若要取得有效的URL，請附加基本語言代碼+ &quot;。html&quot;
   * *例如*， https://localhost:4502/content/sites/ `engage/en.html`

* **範本**：下拉以選擇 `Reference Site`

* 选择&#x200B;**下一步**。

### 步驟2：設計 {#step-design}

「設計」步驟分為兩個區段，用於選取主題和品牌橫幅：

#### 社群網站主題 {#community-site-theme}

選取要套用至範本的所需樣式。 選取時，主題將覆蓋一個勾號。

#### 社群網站品牌化 {#community-site-branding}

（選用）上傳橫幅影像以顯示於各網站頁面。 橫幅會釘選至瀏覽器左邊緣、社群網站標題與導覽連結之間。 橫幅高度會裁剪為120畫素。 橫幅的大小不會調整為符合瀏覽器的寬度和120畫素高度。

![社群 — 網站 — 品牌](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

选择&#x200B;**下一步**。

### 步驟3：設定 {#step-settings}

在「設定」步驟中，選取 `Next`，請注意，共有七個區段提供對涉及使用者管理、標籤、協調、群組管理、分析和翻譯的設定的存取權。

#### 用户管理 {#user-management}

勾選所有核取方塊 [User Management](/help/communities/sites-console.md#user-management)

* 允許網站訪客自行註冊
* 允許網站訪客在不登入的情況下檢視網站
* 允許成員傳送和接收來自其他社群成員的訊息
* 允許使用Facebook登入，而不是註冊和建立設定檔
* 允許使用Twitter登入，而不是註冊和建立設定檔

>[!NOTE]
>
>對於生產環境，必須建立自訂Facebook和Twitter應用程式。 另請參閱 [使用Facebook和Twitter進行社交登入](/help/communities/social-login.md).

![社群網站設定](assets/site-settings.png)

#### 標籤 {#tagging}

可套用至社群內容的標籤可藉由選取先前透過定義的AEM名稱空間來控制 [標籤主控台](/help/sites-administering/tags.md#tagging-console) (例如 [教學課程名稱空間](/help/communities/setup.md#create-tutorial-tags))。

使用預先輸入搜尋可輕鬆尋找名稱空間。 例如，

* 类型 `tut`
* 选择 `Tutorial`

![標籤](assets/tagging.png)

#### 角色 {#roles}

[社群成員角色](/help/communities/users.md) 會透過「角色」區段中的設定指派。

若要讓社群成員（或成員群組）以社群管理員的身分體驗網站，請使用預先輸入搜尋，並從下拉式選單中的選項中選取成員或群組名稱。

例如，

* 类型 `q`
* 選取Quinn Harper

>[!NOTE]
>
>[通道服務](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) 允許選擇僅存在於發佈環境中的成員和群組。

![新網站中的使用者角色](assets/site-admin-1.png)

#### 稽核 {#moderation}

接受預設全域設定 [稽核](/help/communities/sites-console.md#moderation) 使用者產生的內容(UGC)。

![稽核](assets/moderation1.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已獲得授權，且已設定Analytics雲端服務和框架，則可啟用Analytics並選取框架。

另請參閱 [Communities功能的Analytics設定](/help/communities/analytics.md).

![分析](assets/analytics.png)

#### 翻譯 {#translation}

此 [翻譯設定](/help/communities/sites-console.md#translation) 指定網站的基本語言，以及是否可將UGC翻譯成以及翻譯成何種語言（如果有的話）。

* Check **允許機器翻譯**
* 保留預設機器翻譯服務選取的預設翻譯語言
* 保留預設翻譯提供者和設定
* 由於沒有語言副本，因此不需要全域存放區
* 選取 **翻譯整個頁面**
* 保留預設持續性選項

![translation-settings](assets/translation-settings.png)

### 步驟4：建立社群網站 {#step-create-communities-site}

選取 **建立。**

![create-site](assets/create-site2.png)

程式完成時，新網站的資料夾會顯示在「社群 — 網站」主控台中。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## 發佈社群網站 {#publish-the-community-site}

建立的網站應從「社群 — 網站」主控台進行管理，該主控台與可能建立新網站的控制檯相同。

選取社群網站的資料夾以開啟後，將滑鼠指標暫留在網站圖示上，四個動作圖示隨即出現：

![siteactionicons-1](assets/siteactionicons-1.png)

選取第四個橢圓圖示（「更多動作」）時，會顯示「匯出網站」和「刪除網站」選項。

![siteactionsnew-1](assets/siteactionsnew-1.png)

從左到右分別是：

* **打开站点**

   選取鉛筆圖示以在作者編輯模式下開啟社群網站，以新增及/或設定頁面元件

* **编辑站点**

   選取屬性圖示以開啟社群網站以修改屬性，例如標題或變更主題

* **发布站点**

   選取世界圖示以發佈社群網站（例如，如果您的發佈伺服器在本機電腦上執行，則預設為localhost：4503）

* **导出站点**

   選取匯出圖示以建立同時儲存在中的社群網站套件 [封裝管理員](/help/sites-administering/package-manager.md) 並下載。
請注意，UGC未包含在網站套件中。

* **删除站点**

   選取刪除圖示，從中刪除社群網站 **[!UICONTROL 社群>網站主控台]**. 此動作會移除與網站相關聯的所有專案，例如UGC、使用者群組、資產和資料庫記錄。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果未使用發佈執行個體的預設連線埠4503，請編輯預設復寫代理程式，以將連線埠號碼設定為正確的值。
>
>在作者執行個體上，從主功能表：
>
>1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 復寫]** 功能表。
>1. 選取 **[!UICONTROL 作者上的代理]**.
>1. 選取 **[!UICONTROL 預設代理程式（發佈）]**.
>1. 旁邊 **[!UICONTROL 設定]**，選取 **[!UICONTROL 編輯]**.
>1. 在「代理程式設定」的彈出式對話方塊中，選取 **[!UICONTROL 傳輸]** 標籤。
>1. 在URI中，將連線埠號碼4503變更為所需的連線埠號碼。 例如，使用連線埠6103： https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 選取 **[!UICONTROL 確定]**.
>1. （選用）選取 **[!UICONTROL 清除]** 或 **[!UICONTROL 強制重試]** 以重設復寫佇列。


### 選取發佈 {#select-publish}

確定發佈伺服器執行之後，請選取世界圖示以發佈社群網站。

![publish-site](assets/publish-site.png)

成功發佈社群網站後，會短暫出現訊息「網站已發佈」。

### 新社群使用者群組 {#new-community-user-groups}

隨著新的社群網站，新的使用者群組也會建立，這些群組擁有針對各種管理功能設定的適當許可權。 如需詳細資訊，請造訪 [社群網站的使用者群組](/help/communities/users.md#usergroupsforcommunitysites).

對於這個新的社群網站，在步驟1中指定網站名稱「engage」，您可能會從以下位置看到四個新的使用者群組： [群組主控台](/help/communities/members.md) （全域導覽：社群、群組）：

* 社群參與社群管理員
* Community Engage群組管理員
* Community Engage會員
* 社群參與版主
* 社群參與有特殊許可權的成員
* 社群參與網站內容管理員

請注意 [艾倫·麥當勞](/help/communities/tutorials.md#demo-users) 是以下專案的成員：

* 社群參與社群管理員
* 社群參與版主
* Community Engage成員（間接身為版主群組的成員）

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![參與](assets/engage.png)

## 設定驗證錯誤 {#configure-for-authentication-error}

設定網站並推送至發佈後， [設定登入對應](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 優點在於，如果未正確輸入登入認證，驗證錯誤將重新顯示社群網站的登入頁面，並顯示錯誤訊息。

新增 `Login Page Mapping` 作為

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 選擇性步驟 {#optional-steps}

### 變更預設首頁 {#change-the-default-home-page}

使用發佈網站進行示範時，將預設首頁變更為新網站可能會有幫助。

若要這麼做，需要使用 [CRXDE](https://localhost:4503/crx/de) 精簡以編輯 [resource-mapping](/help/sites-deploying/resource-mapping.md) 發佈時顯示的表格。

若要開始使用：

1. 在發佈執行個體上，使用管理員許可權登入。
1. 瀏覽至 [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. 在專案瀏覽器中，展開 `/etc/map.`
1. 選取 `http` 節點：

   * 選取 **建立節點：**

      * **名稱** localhost.4503 (do *not* 使用&#39;：&#39;)

      * **型別** [sling：Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 使用新建立的 `localhost.4503` 選取的節點：

   * 添加属性:

   * **名稱** sling：match
      * **型別** 字串
      * **值** localhost.4503/$ （必須以「$」字元結尾）
   * 添加属性:

      * **名稱** sling：internalRedirect
      * **型別** 字串
      * **值** /content/sites/engage/en.html


1. 選取 **全部儲存。**
1. （選用）刪除瀏覽記錄。
1. 瀏覽至https://localhost:4503/。

   * 送達https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>若要停用，只需在 `sling:match` 具有「x」的屬性值 —  `xlocalhost.4503/$`  — 和 **全部儲存**.

![optional-steps](assets/optional-steps.png)

#### 疑難排解：儲存地圖時發生錯誤 {#troubleshooting-error-saving-map}

如果無法儲存變更，請確定節點名稱為 `localhost.4503`，帶有「點」分隔符號，而非 `localhost:4503` 以「冒號」分隔符號，如 `localhost`不是有效的名稱空間前置詞。

![錯誤訊息](assets/error-message.png)

#### 疑難排解：無法重新導向 {#troubleshooting-fail-to-redirect}

「**$**&#39;在規則運算式結尾 `sling:match`字串至關重要，因此僅能精確 `https://localhost:4503/` 會對應，否則重新導向值會加上前置詞，成為URL中server：port之後可能存在的任何路徑。 因此，當AEM嘗試重新導向至登入頁面時，會失敗。

### 修改網站 {#modify-the-site}

網站初次建立後，作者可使用 [開啟網站圖示](/help/communities/sites-console.md#authoring-site-content) 執行標準AEM編寫活動。

此外，管理員可使用 [編輯網站圖示](/help/communities/sites-console.md#modifying-site-properties) 修改網站屬性，例如標題。

進行任何修改後，請記住 **儲存** 並重新&#x200B;**發佈** 網站。

>[!NOTE]
>
>若不熟悉AEM，請檢視以下說明檔案： [基本處理](/help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](/help/sites-authoring/qg-page-authoring.md).
