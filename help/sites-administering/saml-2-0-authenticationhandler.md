---
title: SAML 2.0 身份验证处理程序
seo-title: SAML 2.0 Authentication Handler
description: 瞭解AEM中的SAML 2.0驗證處理常式。
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6fa3679429527e026313b22d953267503598d1a9
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# SAML 2.0 身份验证处理程序{#saml-authentication-handler}

AEM隨附 [SAML](https://saml.xml.org/saml-specifications) 驗證處理常式。 此處理常式提供 [SAML](https://saml.xml.org/saml-specifications) 2.0驗證要求通訊協定（Web-SSO設定檔）使用 `HTTP POST` 繫結。

它支援：

* 訊息的簽署和加密
* 自動建立使用者
* 將群組同步至AEM中的現有群組
* 服務提供者和身分提供者啟動的驗證

此處理常式會將加密的SAML回應訊息儲存在使用者節點( `usernode/samlResponse`)以促進與協力廠商服務供應商通訊。

>[!NOTE]
>
>另請參閱 [AEM與SAML整合的示範](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## 設定SAML 2.0驗證處理常式 {#configuring-the-saml-authentication-handler}

此 [網頁主控台](/help/sites-deploying/configuring-osgi.md) 提供對的存取 [SAML](https://saml.xml.org/saml-specifications) 2.0已呼叫驗證處理常式設定 **AdobeGranite SAML 2.0驗證處理常式**. 可設定下列屬性。

>[!NOTE]
>
>SAML 2.0 Authentication Handler預設為停用。 您必須至少設定下列其中一個屬性，才能啟用處理常式：
>
>* 身分提供者POSTURL或IDP URL。
>* 服務提供者實體識別碼。
>


>[!NOTE]
>
>SAML宣告已簽署，並可選擇加密。 為了使其運作，您必須至少在TrustStore中提供身分提供者的公開憑證。 另請參閱 [將IdP憑證新增至TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 區段以取得詳細資訊。

**路徑** Sling應使用此驗證處理常式的存放庫路徑。 如果此為空白，則會停用驗證處理常式。

**服務排名** OSGi框架服務排名值，可指出呼叫此服務的順序。 此為整數值，其中較高的值代表較高的優先順序。

**IDP憑證別名** 全域信任存放區中IdP憑證的別名。 如果此屬性為空，則會停用驗證處理常式。 如需如何設定，請參閱下方的「將IdP憑證新增至AEM TrustStore」一章。

**IDP URL** IDP的URL，應將SAML驗證請求傳送至此處。 如果此屬性為空，則會停用驗證處理常式。

>[!CAUTION]
>
>身分提供者主機名稱必須新增至 **Apache Sling查閱者篩選器** OSGi設定。 請參閱 [網頁主控台](/help/sites-deploying/configuring-osgi.md) 區段以取得詳細資訊。

**服務提供者實體ID** 使用身分提供者唯一識別此服務提供者的ID。 如果此屬性為空，則會停用驗證處理常式。

**預設重新導向** 在成功驗證後重新導向到的預設位置。

>[!NOTE]
>
>此位置僅用於 `request-path` 未設定Cookie。 如果您在沒有有效登入權杖的情況下請求已設定路徑下的任何頁面，則請求的路徑會儲存在Cookie中
>而且在成功驗證後，瀏覽器會重新導向至此位置。

**使用者ID屬性** 屬性的名稱，其中包含在CRX存放庫中用於驗證和建立使用者的使用者ID。

>[!NOTE]
>
>系統不會從以下位置取得使用者ID： `saml:Subject` SAML宣告的節點，但來自此 `saml:Attribute`.

**使用加密** 此驗證處理常式是否需要加密的SAML宣告。

**自動建立CRX使用者** 在成功驗證後，是否自動建立存放庫中的非現有使用者。

>[!CAUTION]
>
>如果停用CRX使用者的自動建立，則必須手動建立使用者。

**新增至群組** 在成功驗證後，是否應自動將使用者新增到CRX群組。

**群組成員資格** saml：Attribute的名稱，其中包含此使用者應新增至的CRX群組清單。

## 將IdP憑證新增至AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML宣告已簽署，並可選擇加密。 為了使其運作，您必須至少提供存放庫中IdP的公開憑證。 若要這麼做，您需要：

1. 前往 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按下 **[!UICONTROL 建立TrustStore連結]**
1. 輸入TrustStore的密碼，然後按 **[!UICONTROL 儲存]**.
1. 按一下 **[!UICONTROL 管理信任存放區]**.
1. 上傳IdP憑證。
1. 記下憑證別名。 別名為 **[!UICONTROL admin#1436172864930]** 在以下範例中。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 將服務提供者金鑰和憑證鏈新增至AEM金鑰存放區 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>下列步驟為必要步驟，否則將擲回下列例外狀況： `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 前往： [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 編輯 `authentication-service` 使用者。
1. 按一下以建立KeyStore **建立KeyStore** 在 **帳戶設定**.

>[!NOTE]
>
>只有在處理常式應該能夠簽署或解密訊息時，才需要執行下列步驟。

1. 為AEM建立憑證/金鑰組。 透過openssl產生它的命令應該類似於以下範例：

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. 使用DER編碼將金鑰轉換為PKCS#8格式。 這是AEM金鑰存放區所需的格式。

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. 按一下「 」以上傳私密金鑰檔案 **選取私密金鑰檔案**.
1. 按一下以上傳憑證檔案 **選取憑證鏈結檔案**.
1. 指派別名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 設定SAML的記錄器 {#configure-a-logger-for-saml}

您可以設定記錄器，以偵錯任何可能因錯誤設定SAML而產生的問題。 您可以执行以下操作来实现此目标：

1. 前往網頁主控台，位於 *http://localhost:4502/system/console/configMgr*
1. 搜尋並按一下以下專案： **Apache Sling記錄記錄器設定**
1. 使用下列設定建立記錄器：

   * **記錄層級：** 偵錯
   * **記錄檔：** logs/saml.log
   * **記錄器：** com.adobe.granite.auth.saml
