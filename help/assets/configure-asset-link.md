---
title: 設定Experience Manager Assets以進行Adobe資產連結
description: 設定Experience Manager Assets以搭配Creative Cloud應用程式的Adobe Asset Link擴充功能使用。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 1%

---

# 設定Experience Manager Assets以進行Adobe資產連結 {#adobe-asset-link}

[Adobe資產連結(AAL)](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html) 簡化創意人員與行銷人員在內容建立過程中的合作。 它會將Adobe Experience Manager資產與Creative Cloud案頭應用程式Adobe InDesign、Adobe Photoshop和Adobe Illustrator連線。 「Adobe資產連結」面板可讓創意人員存取及修改儲存在AEM Assets中的內容，而不需離開他們最熟悉的創意應用程式。

若要設定Experience Manager Assets以搭配Asset Link使用，請實作下列工作。 使用Experience Manager管理員帳戶進行設定：

1. 視需要安裝套件。 詳情請參閱 [必備條件](#prerequisites).

1. 設定Experience Manager [手動](#manual-configuration) 或使用 [封裝](#configure-using-package).

1. 若要將Creative Cloud授權使用者與Experience Manager使用者對應，請管理 [使用者存取控制](#user-access).

1. 建立 [自訂查詢索引](#create-custom-index)，設定 [FPO轉譯](/help/assets/configure-fpo-renditions.md) 若為InDesign，請設定 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)，並設定 [視覺或相似性搜尋](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 各種功能的先決條件和支援 {#prerequisites}

請務必視需要安裝適當的Service Pack和套件。 請參閱每個Experience Manager版本和特定功能的下列需求。

| Assets功能 | Experience Manager版本和支援需求 |
|--- |--- |
| 資產連結預設有效 | Experience Manager6.5和6.5.2或更新版本。 </br> Experience Manager6.4.4和6.4.6或更高版本。 </br> Adobe建議安裝最新的 [Experience ManagerService Pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) 使用AAL之前。 |
| Asset Link在安裝套件後即可運作 | 若是Experience Manager6.4.0 - 6.4.3，請安裝 [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 封裝。 |
| Adobe Stock整合 | Experience Manager6.4.2或更新版本 |
| 視覺或相似性搜尋 | Experience Manager 6.5.0或更新版本 |


## 使用設定套件設定Experience Manager {#configure-using-package}

Adobe建議您安裝 [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) 設定套件可自動化大部分的設定工作，之後是一些手動工作。 或者，您可以 [手動設定](#manual-configuration).

>[!CAUTION]
>
>如果您的Experience Manager執行個體設定為使用Adobe IMS帳戶登入的使用者，請勿使用設定套件。 而是 [手動設定](#manual-configuration) 您的Experience Manager執行個體。

1. 若要開啟「封裝管理程式」，請在Experience ManagerWeb介面中存取 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 封裝共用]**. 安裝 `adobe-asset-link-config` 封裝。

1. 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 运营]** > **[!UICONTROL Web 控制台]**。尋找 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定，然後按一下以編輯它。

   設定下列屬性並儲存變更。

   * [!UICONTROL 群組對應]：除非有需要，否則留空。 如需詳細資訊，請參閱 [群組對應](#group-mapping).
   * [!UICONTROL 組織]：輸入您在Adobe Admin Console中使用的組織ID。 如需組織ID的詳細資訊，請參閱 [建立使用者群組](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. 尋找 **[!UICONTROL AdobeGranite Bearer驗證處理常式]** 設定，然後按一下以編輯它。

   新增 **[!UICONTROL InDesignAem2]** 使用者端ID至 **[!UICONTROL 允許的OAuth使用者端ID]** 設定屬性。


## 手動設定Experience Manager {#manual-configuration}

如果您選擇不使用設定套件，或您的Experience Manager部署設定為支援使用者使用Adobe IMS帳戶登入，請手動設定Experience Manager。

若要手動設定Experience Manager：

1. 若要存取設定管理員，請存取 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**. 選取 **[!UICONTROL osgi]** > **[!UICONTROL 設定]** 從頂端的功能表。

1. 找到 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定，然後按一下以編輯它。

   設定下列設定，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 授權端點]： ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 權杖端點]： ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 設定檔端點]： ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 驗證URL]： ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 組織]：在中設為組織ID [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL 群組對應]：除非您有特殊情況，否則留空。 如需詳細資訊，請參閱 [群組對應](#group-mapping).

1. 尋找 **[!UICONTROL AdobeGranite Bearer驗證處理常式]** 設定，然後按一下以編輯它。

   將下列使用者端ID新增至 **[!UICONTROL 允許的OAuth使用者端ID]** 設定屬性： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   若要新增每個 `Client ID`，按一下 `+`. 按一下 **[!UICONTROL 儲存]** 新增所有ID後。

1. 在 **[!UICONTROL AdobeGranite OAuth應用程式和提供者]** 設定，檢查現有 **[!UICONTROL AdobeGranite OAuth驗證處理常式]** 執行個體。 如果您使用找到執行個體， `Config ID` 值 `ims`，請將其用於此程式中的指示。 否則，請按一下 `+` 以建立組態執行個體。 設定下列屬性值，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 使用者端ID]：請勿變更
   * [!UICONTROL 使用者端密碼]：請勿變更
   * [!UICONTROL 設定ID]： ` ims`
   * [!UICONTROL 範圍]： `AdobeID, OpenID, read_organizations` （其他值也可能在設定中）
   * [!UICONTROL 提供者ID]： ` ims`
   * [!UICONTROL 建立使用者]： ` Checked`
   * [!UICONTROL 使用者識別碼屬性]： `Email` 用於新建立的設定。 否則，請勿變更。

1. 找到 **[!UICONTROL Apache Jackrabbit Oak預設同步處理常式]** 設定 **[!UICONTROL 同步處理常式名稱]** `ims` 並按一下以進行編輯。

   設定下列組態屬性，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 使用者到期時間和使用者成員資格到期]：以「m」後面所跟的時間（分鐘），沒有空格。 例如， `15m` 15分鐘。 如需詳細資訊，請參閱 [群組對應](#group-mapping).
   * [!UICONTROL 使用者自動成員資格]：請勿變更
   * [!UICONTROL 使用者動態成員資格]： ` Deslect`

1. 找到 **[!UICONTROL AdobeGranite OAuth驗證處理常式]** 設定，然後按一下以編輯它。 不做任何變更，按一下 **[!UICONTROL 儲存]**.

1. 若要調整承載驗證處理常式的相對優先順序，請在CRXDE中導覽至 `/apps/system/config`. 尋找 `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` 並開啟其設定。 最後，新增 `service.ranking=I"-10"`. 保存更改。

   >[!NOTE]
   >
   >以持有人權杖驗證的每個請求都會產生對Adobe IMS三次呼叫的開銷、使用者同步以及Experience Manager中登入權杖的建立。 為了克服這項額外負荷，Adobe Asset Link會擷取在Experience Manager回應中傳回的登入權杖，並隨後續請求傳送。 若要讓此程式運作，必須調整承載驗證處理常式的相對優先順序。

1. （選用）如果Experience Manager使用者的電子郵件ID中有大寫或混合大小寫的網域名稱，請選取「 」 **[!UICONTROL 將鎖定使用者變更為小寫]** 在 **[!UICONTROL AdobeGranite ACP平台設定]** 在Experience ManagerWeb主控台中。

## 移轉至企業設定檔後的其他設定 {#configure-migration-activity}

Adobe Asset Link使用者可以連線到Experience Manager，以允許從企業(CCE)組織的主要Creative CloudIMS登入。 Experience Manager會使用使用者端ID來識別允許的IMS組織。 在移轉至企業設定檔後，需要為IMS組織設定使用者端ID和秘密金鑰，以Experience Manager表示持有者驗證處理常式。 如需企業個人資料的詳細資訊，請參閱 [Adobe設定檔簡介](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

只有在您使用不同的Adobe IMS組織進行企業(CCE)的Experience Manager和Creative Cloud，且在這兩個組織之間建立網域信任關係時，才需要額外設定。

>[!NOTE]
>
>* Experience Manager6.5.11.0提供企業設定檔的修正。
>* 如果您透過Experience Manager和CCE使用相同的Adobe IMS組織，現有設定仍會繼續運作。



**前提条件**

1. 為AAL設定了持有者驗證且正在執行的Experience Manager執行個體。
1. 在您的Experience Manager6.5執行個體上安裝以下套件(Service Pack 11)。

   [下載Experience Manager6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 連絡人 [!UICONTROL 客戶支援] 以取得IMS組織之持有者驗證的使用者端ID和秘密金鑰。

以下是移轉至企業設定檔後所需的其他設定：

1. 在 **[!UICONTROL AdobeGranite OAuth IMS設定提供者]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)，設定：

   * OAuth設定ID (`oauth.configmanager.ims.configid`)： `ims` （驗證一次，您可能已經設定好）

   * IMS擁有實體(`ims.owningEntity`)：您的IMS組織ID

   ![IMS設定ID](assets/bearer-authentication1.png)

1. 開啟 **[!UICONTROL 持有者驗證處理常式]** 設定並新增從取得的使用者端ID [!UICONTROL 客戶支援] 至清單 **[!UICONTROL 允許的OAuth使用者端ID]**.

   ![新增使用者端ID](assets/add-clientid-bearer-auth.png)

1. 開啟 **[!UICONTROL AdobeGranite OAuth應用程式和提供者]** 設定並新增 **[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]** （秘密金鑰）取得自客戶支援。

   確保 **[!UICONTROL 設定ID]** 欄位(`oauth.config.id`)包含與中提供的相同值 **[!UICONTROL OAuth設定ID]** 欄位(`oauth.configmanager.ims.configid`)。

   ![驗證使用者端ID](assets/clientid-secretkey.png)

1. 開啟 **[!UICONTROL AdobeGranite IMS叢集Exchange Token前置處理器]** 設定並設為 `enable`.

## 管理使用者存取控制 {#user-access}

本節說明如何管理使用者及其對Experience Manager存放庫的存取權。

### 群組對應 {#group-mapping}

群組對應會決定Experience Manager中的群組如何對應至Adobe IMS中的群組。 在授予AdobeAsset Link使用者存取Experience Manager Assets的許可權方面，此功能扮演重要角色。

與Adobe Asset Link搭配使用時，Experience Manager會將使用者管理功能委派給Adobe IMS。 它會自動建立與Adobe IMS中的使用者和群組相對應的使用者和群組。 此外，它會同步Experience Manager中的使用者、群組和群組成員資格，以符合Adobe IMS中的使用者、群組和群組成員資格。

例如，假設AdobeAsset Link使用者是Adobe IMS群組assetlink使用者成員。 在此情況下，當該Adobe IMS群組中的使用者首次連線到Experience Manager Asset Link時，會在Adobe中建立名為assetlink-users的同步群組。 Adobe IMS群組中的每位新使用者在首次透過Experience Manager Asset Link連線到Experience Manager時，都會新增到Adobe中的對應群組。

與Adobe IMS中群組相對應並與之同步的Experience Manager群組，可直接被授予存取權，或透過使其成為其他群組的成員。 以下是如何管理許可權的範例。

![群組範例](assets/group-examples.png)

下列規則適用於Experience Manager中的群組對應：

* 確保 **[!UICONTROL 群組對應]** 中的屬性 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定為空白。
* Adobe資產連結使用者群組成員資格會在使用者驗證時評估，並會評估以下時間段： **[!UICONTROL 使用者到期時間]** 中的屬性 **[!UICONTROL Apache Jackrabbit Oak預設同步處理常式]** 設定已過期。 目前，您可以在Experience Manager中新增和移除使用者，以便與Adobe IMS中的專案同步。
* 避免群組名稱衝突。 確保在Adobe IMS中建立的群組（用於管理使用者）所用名稱與所有Experience Manager系統群組名稱不同。

   例如，請確定它們與 `dam-users` 群組和Experience Manager管理員建立的群組。

   名稱與Experience Manager系統群組名稱或手動建立群組名稱衝突的Adobe IMS群組不會用來控制使用者許可權。
* 如果Adobe IMS使用者連線到Experience Manager執行個體，而該執行個體上的使用者名稱與先前建立的Experience Manager使用者衝突，則會為Adobe IMS使用者指定另一個名稱，並新增編號使其唯一。

**設定首次存取控制**

透過Adobe Asset Link連線的使用者只有在獲得必要許可權後，才能檢視資產並與資產互動。 此 [群組對應](#group-mapping) 上節討論如何在Experience Manager中建立使用者群組，其對應於Adobe IMS中您組織中的使用者群組並與之同步。 建議Experience Manager管理員使用這些群組來管理Adobe Asset Link使用者的存取控制。

對於與Adobe IMS群組（用於管理使用者存取控制）同步的每個Experience Manager群組：

1. 確保群組內有一個成員可用來從Adobe Asset Link建立初始連線。
1. 使用該使用者登入Adobe Asset Link，並連線至Experience Manager。 此連線預期會失敗。
1. 在Experience Manager中，找出與Adobe IMS中群組對應的群組，並授予其所需的存取控制。 例如，新群組成為dam-users群組的成員。
1. 關閉Adobe資產連結並重新啟動Creative Cloud應用程式。
1. 若要確認使用者是否具有預期的存取權，請重新開啟Adobe資產連結。

執行這些步驟後，同一群組中的其他使用者可在第一次嘗試時透過Adobe資產連結連線到Experience Manager。 他們會自動擁有與群組中其他使用者相同的許可權。

## 管理Experience Manager資產連結的Adobe使用者 {#manage-users}

Adobe Asset Link使用者在登入Experience Manager應用程式後，就能與Creative Cloud連線。 此驗證使用Adobe IMS技術，並在Experience Manager中建立使用者資訊（如果沒有）。 Experience Manager企業客戶通常可使用與Experience Manager整合的外部身分提供者來管理其使用者。 身分提供者包括Adobe IMS和其他使用SAML和LDAP通訊協定的產品。 或者，您也可以在Experience Manager中在本機建立和管理使用者。

從Adobe Asset Link連線至Experience Manager的使用者，與先前直接登入儲存於Experience Manager中的現有使用者資訊沒有衝突，如果：

* 用於直接登入Experience Manager的所有使用者名稱，與Adobe IMS中用於Creative Cloud登入的使用者名稱不同。
* Adobe IMS會作為直接Experience Manager登入的身分提供者。
* 使用者先從Adobe資產連結連線到Experience Manager，然後直接Experience Manager使用相同帳戶登入。


另一方面，在下列情況下，必須更新由於直接Experience Manager登入而建立的使用者資訊，才能使用Adobe資產連結：

* 相同的使用者名稱（例如使用者的電子郵件地址）會用於兩者：使用Adobe IMS的Creative Cloud中的帳戶，以及Adobe IMS以外的外部身分提供者中的帳戶。
* 相同的使用者名稱會同時用於兩者 — Creative Cloud中的帳戶和本機Experience Manager帳戶。
* Adobe IMS中的Creative Cloud帳戶是Federated ID，由與Experience Manager整合以供直接登入的相同外部身分提供者服務。

透過這些案例建立的使用者沒有使用者所需的屬性，而是與Adobe IMS同步。

若要在Experience Manager中更新這類使用者，以使用Adobe Asset Link：

1. 在Experience ManagerWeb主控台中，找出 **[!UICONTROL Apache Jackrabbit Oak外部PrincipalConfiguration]** 設定，然後按一下以編輯它。 取消選取 **[!UICONTROL 外部身分保護]** 核取方塊，然後按一下 **[!UICONTROL 儲存]**.
1. 若要在Experience Manager中存取「使用者管理」介面，請瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**. 選取您要更新的使用者，然後記下該使用者的瀏覽器URL路徑結尾，開頭為 `/home/users`. 或者，您也可以在CRXDE中搜尋使用者名稱。 範例使用者路徑： `/home/users/x/xTac082TDh-guJzzG7WM`.
1. 在CRXDE中，導覽至使用者路徑、選取使用者節點，並透過選取 **[!UICONTROL 屬性]** 定位鍵。 此節點具有 `jcr:primaryType` 屬性值 `rep:User`.
1. 在底部 **[!UICONTROL 屬性]** 標籤區域，輸入 `Name` 值 `rep:externalId`， `Type` 值 `String`，和 `Value` 值 `rep:authorizableId`；`ims`，其中 `rep:authorizableId` 是 `rep:authorizableId` 節點的屬性。 (分號可用來分隔 `rep:authorizableId` 值自 `ims`.)
1. 按一下 **[!UICONTROL 新增]** 按鈕，然後按一下 **[!UICONTROL 全部儲存]**.
1. 對您要升級的任何其他使用者重複步驟2到5，以搭配AdobeAsset Link使用。
1. 在Experience ManagerWeb主控台中，找出 **[!UICONTROL Apache Jackrabbit Oak外部PrincipalConfiguration]** 設定，然後按一下以編輯它。 取消選取 **[!UICONTROL 外部身分保護]** 核取方塊，然後按一下 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>如果服務在幾分鐘內未還原，請重新啟動Experience Manager以允許成功驗證。

進行此變更後，更新的Experience Manager使用者可以連線Adobe資產連結，並繼續使用直接登入方法來登入更新前使用的Experience Manager。 成功使用Adobe IMS驗證後，Experience Manager使用者設定檔資訊會與Adobe IMS中的使用者設定檔同步。

有一個方法可以執行多個Experience Manager使用者的大量移轉，好讓他們能夠使用Adobe資產連結。 如需啟用此選項的詳細資訊和協助，請聯絡Adobe服務。

作為這些步驟的替代方法，在某些情況下，Adobe Asset Link使用者可能會獲得快速存取Experience Manager的許可權。 在這種情況下，在與Adobe Asset Link連線之前，可以透過Experience Manager使用者管理或Experience ManagerCRXDE找到並刪除預先存在的使用者資訊。 新的使用者資訊會在連線後以Experience Manager建立。 只有在您確定沒有重要資料新增為使用者節點的子項時，才使用此方法。 這類額外資料是使用者節點之子節點的任何節點，而非節點 `tokens`， `preferences`， `profile`， `profiles`， `profiles/public`、和 `rep:policy/*` 節點。

## 自動啟動工作流程以有條件地處理資產 {#auto-start-workflow}

在Experience Manager6.4和Experience Manager6.5中，管理員可設定工作流程，以根據預先定義的條件自動執行及處理資產。

例如，業務線使用者和行銷人員在幾個特定資料夾上建立自訂工作流程時，此設定就十分實用。 假設機構拍照的所有資產都可以加上水印，或者自由譯者上傳的所有資產都可以經過處理，以建立特定的轉譯。

如需詳細資訊和Experience Manager設定，請參閱 [在資產上自動執行工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## 在Experience Manager6.4.x版本中建立自訂索引 {#create-custom-index}

Experience Manager包含用於查詢的索引。 為指定版本建立下列自訂索引。 Experience Manager6.5.0預設包含此索引。 Adobe資產連結需要此索引來判斷使用者已簽出哪些資產。

1. 在CRXDE中，找出 `/oak:index` 節點。 建立名為的節點 `cqDrivelock` 並設定其 `Type` 至 `oak:QueryIndexDefinition`.

1. 將下列屬性新增至新節點並儲存變更：

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 設定視覺或相似性搜尋 {#configure-visual-similarity-search}

「視覺搜尋」功能可讓您使用「Adobe資產連結」面板，在AEM Assets存放庫中搜尋視覺上類似的資產。 6.5.0或更新版本中提供此功能，而且只會搜尋索引資產。 如需詳細資訊，請參閱 [如何設定視覺搜尋](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 為Adobe InDesign產生僅供放置的轉譯 {#fpo-renditions}

Experience Manager提供僅用於放置的轉譯(FPO)。 這些FPO轉譯檔案大小雖小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程順利進行，而不會出現任何中斷情形。 如需詳細資訊，請參閱 [產生FPO轉譯](/help/assets/configure-fpo-renditions.md).


## 整合Adobe Stock {#adobe-stock-integration}

組織可將其Adobe Stock帳戶與Experience Manager Assets整合。 它可協助行銷人員為其創意和行銷專案提供授權的高品質、免版稅像片、向量、插圖、影片、範本和3D資產。 創意專業人士可以使用Asset Link面板來使用這些資產。

若要整合Adobe Stock，請參閱 [Experience Manager Assets中的Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md). 與Adobe Stock整合需要Experience Manager6.4.2或更新版本。


## 疑難排解Experience Manager相關問題 {#troubleshoot}


如果您在設定或使用Adobe Asset Link時遇到問題，請嘗試下列操作：

* 確保您的部署符合先決條件。 具體來說，請確定已安裝適當的Feature Pack或套件。
* 請聯絡貴組織的合作夥伴或系統整合商。
* 如果您的Creative Cloud使用者無法在已取出資產中進行驗證，請檢查電子郵件ID中網域名稱的大小寫。 若要修正，請參閱 [手動設定](#manual-configuration).
* 如需詳細資訊，請參閱 [疑難排解Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [关于 Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [在Creative Cloud案頭應用程式中使用資產連結並管理資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [as a Cloud Service設定Adobe Experience Manager資產](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html).

