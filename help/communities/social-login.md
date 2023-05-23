---
title: 使用Facebook和Twitter進行社交登入
seo-title: Social Login with Facebook and Twitter
description: 社交登入可讓網站訪客使用其Facebook或Twitter帳戶登入。
seo-description: Social login lets site visitors to sign in with their Facebook or Twitter account.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 1%

---

# 使用Facebook和Twitter進行社交登入 {#social-login-with-facebook-and-twitter}

社交登入是向網站訪客呈現使用其Facebook或Twitter帳戶登入的選項。 因此，請將允許的Facebook或Twitter資料納入其AEM成員設定檔中。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登入概觀 {#social-login-overview}

若要納入社交登入，則是 *必填* 以建立自訂Facebook和Twitter應用程式。

雖然We-Retail範例提供範例Facebook和Twitter應用程式及雲端服務，但無法用於 [生產網站](../../help/sites-administering/production-ready.md).

必要的步驟包括：

1. [啟用OAuth驗證](#adobe-granite-oauth-authentication-handler) 在所有AEM發佈執行個體上。

   若未啟用OAuth，登入嘗試會失敗。

1. **建立** 社交應用程式和雲端服務。

   * 若要支援使用Facebook登入：

      * 建立 [facebook應用程式](#create-a-facebook-app).
      * 建立並發佈 [facebook Connect雲端服務](#create-a-facebook-connect-cloud-service).
   * 若要支援使用Twitter登入：

      * 建立 [twitter應用程式](#create-a-twitter-app).
      * 建立並發佈 [twitter Connect雲端服務](#create-a-twitter-connect-cloud-service).


1. [**啟用** 社交登入](#enable-social-login) 適用於社群網站。

有兩個基本概念：

1. **範圍** （許可權）指定允許應用程式要求的資料。

   * facebook和Twitter [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider) 依預設，執行個體會在其範圍內包含基本應用程式許可權。

1. **欄位** (params)會指定使用URL引數請求的實際資料。

   * 這些欄位指定於 [AEM Communities Facebook OAuth提供者](#aem-communities-facebook-oauth-provider) 和 [AEM Communities Twitter OAuth提供者](#aem-communities-twitter-oauth-provider).
   * 預設欄位對於大多數使用案例來說已經足夠，但是可以修改。

## facebook登入 {#facebook-login}

### facebook API版本 {#facebook-api-version}

社交登入和We-Retail Facebook範例是在Facebook Graph API 1.0版時開發。AEM 6.4 GA和AEM 6.3 SP1的社交登入已更新，可與更新的Facebook Graph API 2.5版本搭配使用。

>[!NOTE]
>
>對於舊版AEM，如果您在記錄中遇到例外狀況 **無法從此擷取權杖**，請升級至該AEM版本適用的最新CFP。

如需Facebook Graph API版本資訊，請參閱 [facebook API變更記錄檔](https://developers.facebook.com/docs/apps/changelog).

### 建立Facebook應用程式 {#create-a-facebook-app}

必須正確設定的Facebook應用程式才能啟用Facebook社交登入。

若要建立Facebook應用程式，請依照Facebook的指示操作，網址為 [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 對指示所做的變更不會反映在以下資訊中。

一般而言，截至Facebook API v2.7：

* *新增新的Facebook應用程式*
   * 對象 *Platform*，選擇網站：
      * 對象 *網站URL*，輸入 `  https://<server>:<port>.`
      * 對象 *顯示名稱*，輸入標題以用作Facebook連線服務的標題。
      * 對象 *類別*，建議選擇 *適用於頁面的應用程式*，但可以是任何專案。
      * *新增產品： Facebook登入*
      * 對象 *有效的OAuth重新導向URI*，輸入 `  https://<server>:<port>.`

>[!NOTE]
>
>http://localhost:4503將適用於開發。

建立應用程式後，找到 **[!UICONTROL 應用程式ID]** 和 **[!UICONTROL 應用程式密碼]** 設定。 此資訊是設定 [facebook雲端服務](#createafacebookcloudservice).

### 建立Facebook ConnectCloud Service {#create-a-facebook-connect-cloud-service}

此 [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider) 執行個體（透過建立雲端服務設定而具現化）可識別Facebook應用程式和新增使用者的成員群組。

1. 在AEM編寫執行個體上，使用管理員許可權登入。
1. 在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL facebook社交登入設定]**.
1. 選取設定 **[!UICONTROL 內容路徑]**.

   **[!UICONTROL 內容路徑]** 應與您建立/編輯社群網站時選取的雲端設定路徑相同。

1. 檢查您的內容路徑是否已啟用，以便在其下方建立雲端服務。
1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**. 選取您的內容並編輯屬性。 啟用雲端設定（如果尚未啟用）。

   ![config-propertiesping](assets/config-propertiespng.png)

   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。

1. **建立/編輯** facebook雲端服務設定。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 標題]** (*必填*)輸入可識別Facebook應用程式的顯示標題。 建議使用與輸入的名稱相同的名稱 *顯示名稱* 適用於Facebook應用程式。
   * **[!UICONTROL 應用程式ID/API金鑰]** (*必填*)輸入 ***應用程式ID*** 適用於Facebook應用程式。 這可識別 [AdobeGranite OAuth應用程式和提供者](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 從對話方塊建立的例項。
   * **[!UICONTROL 應用程式密碼]** (*必填*)輸入 ***應用程式密碼*** 適用於Facebook應用程式。
   * **[!UICONTROL 建立使用者]** 如果勾選，使用Facebook帳戶登入將會建立AEM使用者專案，並將他們新增為所選使用者群組的成員。  已勾選預設值（強烈建議）。
   * **[!UICONTROL 隱藏使用者ID]**：保留為取消選取。
   * **[!UICONTROL 設定電子郵件範圍]**：使用者的電子郵件id應從Facebook擷取。
   * **[!UICONTROL 新增到使用者群組]** 選取「新增使用者群組」以選擇一或多個 [成員群組](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 使用者將新增至的社群網站。

   >[!NOTE]
   >
   >群組可隨時新增或移除。 但現有使用者的成員資格不會受到影響。 自動成員資格僅適用於此欄位更新後建立的新使用者。 針對停用匿名使用者的網站，選擇將使用者新增至適用於該已關閉社群網站的對應社群成員群組。

   * 選取 **[!UICONTROL 儲存]**.
   * **[!UICONTROL 发布]**.


結果為 [AdobeGranite OAuth應用程式和提供者](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 例項，除非新增其他範圍（許可權），否則不需要進一步修改。 預設範圍是Facebook登入的標準許可權。 如果需要其他範圍，則需要直接編輯OSGI設定。 如果直接透過系統/主控台完成修改，請避免從觸控式UI編輯雲端服務設定，以避免覆寫。

### AEM Communities Facebook OAuth提供者 {#aem-communities-facebook-oauth-provider}

AEM Communities提供者擴充 [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider) 執行個體。

此提供者需要編輯以：

* 允許使用者更新
* 新增其他欄位 [在範圍內](#adobe-granite-oauth-application-and-provider)

   * 預設不會包含預設允許的所有欄位。

如果需要進行編輯，請在每個AEM發佈執行個體上：

1. 以管理員許可權登入。
1. 導覽至 [網頁主控台](../../help/sites-deploying/configuring-osgi.md). 例如，http://localhost:4503/system/console/configMgr。
1. 找到AEM Communities Facebook OAuth提供者。
1. 選取鉛筆圖示以開啟以進行編輯。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供者ID]**

      (*必填*)預設值為 *soco -facebook*. 請勿編輯。

   * **[!UICONTROL Cloud Service設定]**

      默认值为 `/etc/  cloudservices /  facebookconnect`. 請勿編輯。

   * **[!UICONTROL OAuth提供者服務設定]**

      默认值为 `/apps/social/facebookprovider/config/`. 請勿編輯。

   * **[!UICONTROL 啟用標籤]**

      請勿編輯。

   * **[!UICONTROL 使用者路徑]**

      存放庫中儲存使用者資料的位置。 對於社群網站，為確保成員擁有檢視彼此設定檔的許可權，路徑應為預設值 */home/users/community*.

   * **[!UICONTROL 啟用欄位]**

      如果勾選，列出的欄位會在向Facebook發出的請求中指定，以取得使用者驗證和資訊。 預設為取消選取。

   * **[!UICONTROL 字段]**

      啟用欄位後，在呼叫Facebook Graph API時會包含下列欄位。 這些欄位必須允許在雲端服務設定中定義的範圍內。 其他欄位可能需要Facebook核准。 請參考Facebook檔案的Facebook登入許可權一節。 新增為引數的預設欄位包括：

      * id
      * name
      * 名字
      * last_name
      * 連結
      * 区域设置
      * 圖片
      * 時區
      * update_time
      * 已驗證
      * 电子邮件

   如果新增或變更了任何欄位，請更新對應的Default Sync處理常式設定以更正對應。

   * **[!UICONTROL 更新使用者]**

      如果勾選，會在每次登入時重新整理存放庫中的使用者資料，以反映設定檔變更或請求的其他資料。 「預設」已取消選取。


#### 后续步骤 {#next-steps}

facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社群網站啟用](#enable-social-login)

## twitter登入 {#twitter-login}

### 建立Twitter應用程式 {#create-a-twitter-app}

需要設定的Twitter應用程式才能啟用Twitter社交登入。

請依照最新指示，在下列位置建立新的Twitter應用程式： [https://apps.twitter.com](https://apps.twitter.com/).

一般而言：

1. 輸入 *名稱* 會向網站使用者識別您的Twitter應用程式。
1. 輸入 *說明*.
1. 對象 *網站*  — 輸入 `https://<server>`.
1. 對象 *回撥URL*  — 輸入 `https://server`.

   >[!NOTE]
   >
   >不需要指定連線埠。
   >
   >https://127.0.0.1/將適用於開發。

1. 建立應用程式後，找到 **[!UICONTROL 消費者(API)金鑰]** 和 **[!UICONTROL 消費者(API)密碼]**. 設定時需要此資訊 [twitter雲端服務](#createatwittercloudservice).

#### 权限 {#permissions}

在Twitter應用程式管理的許可權區段中：

* **[!UICONTROL 存取]**：選取 `Read only`.

   * 不支援其他選項

* **[!UICONTROL 其他許可權]**：選擇性地選擇 `Request email addresses from users`.

   * 如果未選取，AEM中的使用者設定檔將不會包含其電子郵件地址。
   * twitter的指示會註明其他要採取的步驟。

對社交登入提出的唯一REST請求是 *[GET帳戶/驗證認證](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### 建立Twitter ConnectCloud Service {#create-a-twitter-connect-cloud-service}

此 [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider) 執行個體（透過建立雲端服務設定而具現化）可識別Twitter應用程式和新增使用者的成員群組。

1. 在作者執行個體上，使用管理員許可權登入。
1. 在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL twitter社交登入設定]**.
1. 選擇 **[!UICONTROL 內容路徑]** 設定。

   內容路徑應與您在建立/編輯社群網站時選取的雲端設定路徑相同。

1. 檢查您的內容路徑是否已啟用，以便在其下方建立雲端服務。
1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**. 選取您的內容並編輯屬性。 啟用雲端設定（如果尚未啟用）。

   ![twitterconfigpropng](assets/twitterconfigproppng.png)

   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。

1. 建立/編輯Twitter雲端服務設定。

   ![twittersocialloginping](assets/twittersocialloginpng.png)

   * **[!UICONTROL 标题]**

      (*必填*)輸入可識別Twitter應用程式的顯示標題。 建議使用與輸入的名稱相同的名稱 *顯示名稱* 適用於Twitter應用程式。

   * **[!UICONTROL 使用者密钥]**

      (*必填*)輸入 **消費者(API)金鑰** 適用於Twitter應用程式。 這可識別 [AdobeGranite OAuth應用程式和提供者](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 從對話方塊建立的例項。

   * **[!UICONTROL 使用者密钥]**

      (*必填*)輸入 ***Consumer(API)密碼*** 適用於Twitter應用程式。

   * **[!UICONTROL 创建用户]**

      如果勾選，使用Twitter帳戶登入將會建立AEM使用者專案，並將他們新增為所選使用者群組的成員。 已勾選預設值（強烈建議）。

   * **[!UICONTROL 隐藏用户 ID]**

      保留為取消選取。

   * **[!UICONTROL 添加到用户组]**

      選取「新增使用者群組」以選擇一或多個 [成員群組](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 使用者將新增至的社群網站。
   >[!NOTE]
   >
   >群組可隨時新增或移除。 但現有使用者的成員資格不會受到影響。 自動成員資格僅適用於此欄位更新後建立的新使用者。 若為停用匿名使用者的網站，請將使用者新增至適用於該已關閉社群網站的對應社群成員群組。

1. 選取 **[!UICONTROL 儲存]** 和 **[!UICONTROL 發佈]**.

結果為 [AdobeGranite OAuth應用程式和提供者](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 不需要進一步修改的例項。 預設範圍是Twitter登入的標準許可權。

### AEM Communities Twitter OAuth提供者 {#aem-communities-twitter-oauth-provider}

AEM Communities設定可擴充 [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider) 執行個體。 此提供者需要編輯才能允許使用者更新。

如果需要進行編輯，請在每個AEM發佈執行個體上：

1. 以管理員許可權登入。
1. 導覽至 [網頁主控台](../../help/sites-deploying/configuring-osgi.md).

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AEM Communities Twitter OAuth提供者。
1. 選取鉛筆圖示以開啟以進行編輯。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供者ID]**

   (*必填*)預設值為 *soco -twitter*. 請勿編輯。

   * **[!UICONTROL Cloud Service設定]**

      預設值為 *會議* 請勿編輯。

   * **[!UICONTROL OAuth提供者服務設定]**

      默认值为 `/apps/social/twitterprovider/config/`。請勿編輯。

   * **[!UICONTROL 使用者路徑]**

      存放庫中儲存使用者資料的位置。 對於社群網站，為確保成員擁有檢視彼此設定檔的許可權，路徑應為預設值 `/home/users/community`.

   * **[!UICONTROL 啟用引數]** 不要編輯
   * **[!UICONTROL URL引數]** 不要編輯
   * **[!UICONTROL 更新使用者]**

      如果勾選，會在每次登入時重新整理存放庫中的使用者資料，以反映設定檔變更或請求的其他資料。 預設為取消選取。


#### 后续步骤 {#next-steps-1}

facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社群網站啟用](#enable-social-login)

## 啟用社交登入 {#enable-social-login}

### AEM Communities Sites主控台 {#aem-communities-sites-console}

設定雲端服務後，可使用針對社群網站的相關社交登入設定啟用它 [User Management](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 社群網站期間的設定子面板 [建立](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) 或 [管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. 選擇您儲存社交登入設定的網站設定內容。

1. 在一般索引標籤上，設定雲端設定。

   ![managesites_png](assets/managesites_png.png)

1. 在設定索引標籤上，啟用 **[!UICONTROL 社交登入]** 和儲存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 測試社交登入 {#test-social-login}

* 確定 [AdobeGranite OAuth驗證處理常式](#adobe-granite-oauth-authentication-handler) 已在所有發佈執行個體上啟用。
* 確保雲端服務已發佈。
* 確認社群網站已發佈。
* 在瀏覽器中啟動已發佈的網站。
例如， http://localhost:4503/content/sites/engage/en.html
* 選取 **[!UICONTROL 登入]**.
* 選取 **[!UICONTROL 使用Facebook登入]** 或 **[!UICONTROL 使用Twitter登入]**.
* 如果尚未登入Facebook或Twitter，請使用適當的憑證登入。
* 視Facebook或Twitter應用程式顯示的對話方塊而定，可能需要授與許可權。
* 請注意，頁面頂端的工具列已更新，以反映成功的登入。
* 選取 **[!UICONTROL 設定檔]**：設定檔頁面會顯示使用者的頭像影像、名字和姓氏。 也會根據允許的欄位/引數顯示Facebook或Twitter設定檔的資訊。

## AEM平台OAuth設定 {#aem-platform-oauth-configurations}

### AdobeGranite OAuth驗證處理常式 {#adobe-granite-oauth-authentication-handler}

此 `Adobe Granite OAuth Authentication Handler` 未預設啟用，並且 ***必須在所有AEM發佈執行個體上啟用。***

若要在發佈時啟用驗證處理常式，只需開啟OSGi設定並儲存即可：

* 以管理員許可權登入。
* 導覽至 [網頁主控台](../../help/sites-deploying/configuring-osgi.md).
例如， http://localhost:4503/system/console/configMgr
* 尋找 `Adobe Granite OAuth Authentication Handler`.
* 選取「 」以開啟設定進行編輯。
* 选择&#x200B;**[!UICONTROL 保存]**。

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>請留意勿將驗證處理常式與的Facebook或Twitter執行個體混淆 *AdobeGranite OAuth應用程式和提供者*.

![graniteoauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth應用程式和提供者 {#adobe-granite-oauth-application-and-provider}

建立Facebook或Twitter的雲端服務時， `Adobe Granite OAuth Authentication Handler` 「 」已建立。

若要找到Facebook或Twitter應用程式已建立的例項：

1. 以管理員許可權登入。
1. 導覽至 [網頁主控台](../../help/sites-deploying/configuring-osgi.md).

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AdobeGranite OAuth應用程式和提供者。

   * 找到執行個體，其中 **[!UICONTROL 使用者端ID]** 符合 **[!UICONTROL 應用程式ID]**.

      ![graniteoauth2](assets/graniteoauth2.png)

      除了下列屬性外，設定的其他屬性保持不變：

   * **[!UICONTROL 設定ID]**

      (*必填*) OAuth設定ID必須是唯一的。 建立雲端服務時自動產生。

   * **[!UICONTROL 客户端 ID]**

      (*必填*)建立雲端服務時提供的應用程式ID。

   * **[!UICONTROL 客户端密钥]**

      (*必填*)建立Cloud Service時提供的應用程式密碼。

   * **[!UICONTROL 范围]**

      (*可選*)可向提供者要求其他允許範圍。 預設範圍涵蓋提供社交驗證和設定檔資料所需的許可權。

   * **[!UICONTROL 提供者ID]**

      (*必填*)AEM Communities的提供者ID是在建立雲端服務時設定。 請勿編輯。 facebook Connect的值為 *soco -facebook*. twitter Connect的值為 *soco -twitter*.

   * **[!UICONTROL 组]**

      (*建議*)建立的使用者新增至一或多個成員群組。 若為AEM Communities，建議列出社群網站的成員群組。

   * **[!UICONTROL 回调 URL]**

      (*可選*)以OAuth提供者設定的URL，用於將使用者端重新導向。 使用相對URL來使用原始請求的主機。 留空將使用最初請求的URL。 字尾&quot;/callback/j_security_check&quot;會自動附加至此url 。
   >[!NOTE]
   >
   >回呼的網域必須向提供者(Facebook或Twitter)註冊。

對於每個OAuth驗證處理常式設定，執行個體中會建立兩個額外的設定：

* Apache Jackrabbit Oak Default Sync Handler (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — 此處不需要編輯，但您可以檢視Facebook欄位對應到CQ使用者設定檔節點的使用者欄位對應。 另請注意，「同步處理常式名稱」符合OAuth提供者設定的設定ID。
* Apache Jackrabbit Oak外部登入模組(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — 此處不需要編輯，但您可能會注意到「身分提供者名稱」和「同步處理常式名稱」相同，分別指向對應的OAuth和同步處理常式設定。

如需詳細資訊，請參閱 [使用Apache Oak外部登入模組進行驗證](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth使用者周遊效能 {#oauth-user-traversal-performance}

若是社群網站，有數十萬使用者使用其Facebook或Twitter登入進行註冊，則新增下列Oak索引可改善網站訪客使用其社交登入時所執行查詢的周遊效能。

如果記錄中出現周遊警告，建議新增此索引。

在作者執行個體上，以管理許可權登入：

1. 從全域導覽：選取 **工具， [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. 從ntBaseLucene復本建立名為ntBaseLucene-oauth的索引：

   * 在節點下 `/oak:index`
   * 選取節點 `ntBaseLucene`
   * 選取 **[!UICONTROL 複製]**
   * 选择 `/oak:index`
   * 選取 **[!UICONTROL 貼上]**
   * 將ntBaseLucene的復本重新命名為 `ntBaseLucene-oauth`

1. 修改節點ntBaseLucene-oauth的屬性：

   * **[!UICONTROL indexPath]**： `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名稱]**： `oauthid-123****`
   * **[!UICONTROL 重新索引]**： `true`
   * **[!UICONTROL reindexCount]**： `1`

1. 在節點/oak：index/ntBaseLucene-oauth/indexRules/nt：base/properties底下：

   * 刪除除cqTags以外的所有子節點。
   * 將cqTags重新命名為 `oauthid-123****`
   * 修改節點的屬性 `oauthid-123****`

      * **[!UICONTROL 名稱]**： `oauthid-123****`
   * 選取 **[!UICONTROL 全部儲存]**.


* 對於 **名稱** `oauthid-123`，取代 *123* 使用Facebook ***應用程式ID*** 或Twitter ***消費者(API)金鑰*** 這是 **使用者端ID** 在 [AdobeGranite OAuth應用程式和提供者](social-login.md#adobe-granite-oauth-application-and-provider) 設定。

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

如需其他資訊和工具，請參閱 [Oak查詢和索引](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher設定 {#dispatcher-configuration}

另請參閱 [為社群設定Dispatcher](dispatcher.md).
