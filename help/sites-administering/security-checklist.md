---
title: 安全性檢查清單
seo-title: Security Checklist
description: 瞭解設定和部署AEM時的各種安全性考量事項。
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: 41752e40f2bceae98d4a9ff8bf130476339fe324
workflow-type: tm+mt
source-wordcount: '3025'
ht-degree: 1%

---

# 安全性檢查清單 {#security-checklist}

本節說明您應採取的各種步驟，以確保在部署時AEM安裝的安全。 檢查清單旨在從上到下套用。

>[!NOTE]
>
>如需最危險的安全性威脅的詳細資訊，請參閱以下文章所發表的資訊： [開啟Web應用程式安全性專案(OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>此外，我們提供 [安全性考量](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 適用於開發階段。

## 主要安全性措施 {#main-security-measures}

### 在生產就緒模式下執行AEM {#run-aem-in-production-ready-mode}

如需詳細資訊，請參閱 [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md).

### 为传输层安全性启用 HTTPS {#enable-https-for-transport-layer-security}

必須有安全執行個體，才能在製作和發佈執行個體上啟用HTTPS傳輸層。

>[!NOTE]
>
>請參閱 [啟用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 區段以取得詳細資訊。

### 安裝安全性Hotfix {#install-security-hotfixes}

確定您已安裝最新的 [Adobe提供的安全性Hotfix](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans).

### 變更AEM和OSGi Console管理帳戶的預設密碼 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe建議您在安裝後變更有特殊許可權者的密碼 [**AEM** `admin` 帳戶](#changing-the-aem-admin-password) （在所有執行個體上）。

這些帳戶包括：

* AEM `admin` 帳戶

   在您變更AEM管理員帳戶的密碼後，請在存取CRX時使用新密碼。

* 此 `admin` OSGi Web主控台的密碼

   此變更也會套用至用於存取Web主控台的管理員帳戶，因此在存取該帳戶時使用相同的密碼。

這兩個帳戶使用不同的認證，而且每個帳戶都有獨特的強式密碼，這對於安全部署至關重要。

#### 變更AEM管理密碼 {#changing-the-aem-admin-password}

AEM管理員帳戶的密碼可透過以下方式變更： [Granite作業 — 使用者](/help/sites-administering/granite-user-group-admin.md) 主控台。

您可以在此處編輯 `admin` 帳戶和 [變更密碼](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>變更管理員帳戶也會變更OSGi Web主控台帳戶。 變更管理員帳戶後，您應將OSGi帳戶變更為其他帳戶。

#### 變更OSGi Web主控台密碼的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帳戶，若未變更OSGi Web主控台密碼的預設密碼，可能會導致：

* 在啟動和關閉期間使用預設密碼公開伺服器（大型伺服器可能需要幾分鐘的時間）；
* 當存放庫關閉/重新啟動套件組合時 — 且OSGI正在執行時，伺服器的曝光。

如需有關變更Web主控台密碼的詳細資訊，請參閱 [變更OSGi Web主控台管理密碼](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下方的。

#### 變更OSGi Web主控台管理密碼 {#changing-the-osgi-web-console-admin-password}

變更用於存取Web主控台的密碼。 使用 [OSGI設定](/help/sites-deploying/configuring-osgi.md) 更新下列屬性 **Apache Felix OSGi管理主控台**：

* **使用者名稱** 和 **密碼**，此憑證用於存取Apache Felix Web管理主控台本身。
必須變更密碼 *晚於* 初始安裝以確保執行個體的安全性。

>[!NOTE]
>
>另請參閱 [OSGI設定](/help/sites-deploying/configuring-osgi.md) 以取得設定OSGi設定的完整詳細資訊。

**若要變更OSGi Web主控台管理密碼**：

1. 使用 **工具**， **作業** 功能表，開啟 **網頁主控台** 並導覽至 **設定** 區段。
例如，在 `<server>:<port>/system/console/configMgr`.
1. 導覽至並開啟專案 **Apache Felix OSGi管理主控台**.
1. 變更 **使用者名稱** 和 **密碼**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 选择&#x200B;**保存**。

### 實作自訂錯誤處理常式 {#implement-custom-error-handler}

Adobe建議定義自訂錯誤處理常式頁面，尤其是針對404和500 HTTP回應代碼，以防止資訊洩漏。

>[!NOTE]
>
>另請參閱 [如何建立自訂指令碼或錯誤處理常式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) 以取得更多詳細資料。

### 完成Dispatcher安全性檢查清單 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您基礎架構的關鍵部分。 Adobe建議您完成 [Dispatcher安全性檢查清單](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>使用Dispatcher時，您必須停用「.form」選擇器。

## 驗證步驟 {#verification-steps}

### 設定復寫和傳輸使用者 {#configure-replication-and-transport-users}

AEM的標準安裝會指定 `admin` 預設為傳輸憑證的使用者 [復寫代理](/help/sites-deploying/replication.md). 此外，管理員使用者也可在作者系統上為復寫設定來源。

基於安全性考量，兩者都應該變更以反映手頭的特定使用案例，並牢記以下兩個方面：

* 此 **傳輸使用者** 不得為管理員使用者。 而是要在發佈系統上設定只具備發佈系統相關部分存取許可權的使用者，並使用該使用者的憑證進行傳輸。

   您可以從隨附的復寫接收者使用者開始，並設定此使用者的存取許可權以符合您的情況

* 此 **復寫使用者** 或 **代理使用者ID** 也不得為管理員使用者，而必須是只能看見已復寫內容的使用者。 復寫使用者是用來收集要在製作系統上復寫的內容，然後再傳送給發行者。

### 檢查操作儀表板安全性健康情況檢查 {#check-the-operations-dashboard-security-health-checks}

AEM 6推出新的操作控制面板，旨在協助系統操作員疑難排解問題，並監控執行個體的健康狀況。

儀表板也隨附一組安全性健康情況檢查。 建議您在使用生產執行個體上線之前，先檢查所有安全性健康情況檢查的狀態。 如需詳細資訊，請參閱 [操作儀表板檔案](/help/sites-administering/operations-dashboard.md).

### 檢查是否存在範例內容 {#check-if-example-content-is-present}

所有範例內容和使用者(例如Geometrixx專案及其元件)應在生產系統中完全解除安裝並刪除，然後再開放存取。

>[!NOTE]
>
>範例 `We.Retail` 如果此執行個體是在中執行，則會移除應用程式 [生產就緒模式](/help/sites-administering/production-ready.md). 如果不是這種情況，您可以前往「封裝管理員」，搜尋並解除安裝範例內容 `We.Retail` 封裝。

另請參閱 [使用封裝](package-manager.md).

### 檢查CRX開發套件組合是否存在 {#check-if-the-crx-development-bundles-are-present}

這些開發OSGi套件組合應先在製作和發佈生產力系統上解除安裝，然後才能存取。

* Adobe CRXDE支援(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer (com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 檢查Sling開發套件組合是否存在 {#check-if-the-sling-development-bundle-is-present}

此 [AEM Developer Tools](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支援安裝(org.apache.sling.tooling.support.install)。

此OSGi套件組合應先在製作和發佈生產力系統上解除安裝，然後才能存取。

### Protect防止跨網站請求偽造 {#protect-against-cross-site-request-forgery}

#### CSRF保護架構 {#the-csrf-protection-framework}

AEM 6.1隨附有助於抵禦跨網站請求偽造攻擊的機制，稱為 **CSRF保護架構**. 如需其使用方式的詳細資訊，請參閱 [檔案](/help/sites-developing/csrf-protection.md).

#### Sling查閱者篩選器 {#the-sling-referrer-filter}

若要解決CRX WebDAV和Apache Sling中跨網站請求偽造(CSRF)的已知安全性問題，請新增反向連結篩選器的設定以使用它。

反向連結篩選服務是OSGi服務，可讓您設定下列專案：

* 應該篩選哪些http方法
* 是否允許空的反向連結標頭
* 以及除了伺服器主機之外還允許使用的伺服器清單。

   依預設，伺服器所繫結之localhost和目前主機名稱的所有變數都列在清單中。

若要設定反向連結篩選服務：

1. 開啟Apache Felix主控台(**設定**)於：

   `https://<server>:<port_number>/system/console/configMgr`

1. 登入身份 `admin`.
1. 在 **設定** 功能表，選取：

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 欄位，輸入允許作為反向連結的所有主機。 每個專案都必須採用格式

   &lt;protocol>：//&lt;server>：&lt;port>

   例如：

   * `https://allowed.server:80` 允許來自此伺服器的所有要求使用指定的連線埠。
   * 如果您也想要允許https請求，則必須輸入第二行。
   * 如果您允許來自該伺服器的所有連線埠，則可以使用 `0` 作為連線埠號碼。

1. 檢查 `Allow Empty` 欄位（如果要允許空白/缺少反向連結標題）。

   >[!CAUTION]
   >
   >Adobe建議您在使用命令列工具(例如 `cURL` 而不是允許空值，因為它可能會讓您的系統遭到CSRF攻擊。

1. 編輯此篩選器用於檢查的方法，使用 `Filter Methods` 欄位。

1. 按一下 **儲存** 以儲存變更。

### OSGI設定 {#osgi-settings}

部分OSGI設定預設為更輕鬆偵錯應用程式。 在發佈和編寫高生產力的執行個體上變更這類設定，以避免內部資訊洩露給公眾。

>[!NOTE]
>
>以下所有設定，但不包括 **Day CQ WCM偵錯篩選器**，會自動涵蓋 [生產就緒模式](/help/sites-administering/production-ready.md). 因此，Adobe建議您先檢閱所有設定，然後再將執行個體部署至高生產力的環境。

對於下列各項服務，必須變更指定的設定：

* [AdobeGraniteHTML程式庫管理員](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager)：

   * 啟用 **最小化** （移除CRLF和空白字元）。
   * 啟用 **Gzip** （允許透過一個請求來壓縮及存取檔案）。
   * disable **偵錯**
   * disable **計時**

* [Day CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 取消勾選 **啟用**

* [Day CQ WCM篩選器](/help/sites-deploying/osgi-configuration-settings.md)：

   * 僅發佈時，設定 **WCM模式** 變成「已停用」

* [Apache Sling JavaScript處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler)：

   * disable **產生偵錯資訊**

* [Apache Sling JSP指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * disable **產生偵錯資訊**
   * disable **對應的內容**

另請參閱 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md).

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

## 進一步閱讀 {#further-readings}

### 減輕拒絕服務(DoS)攻擊 {#mitigate-denial-of-service-dos-attacks}

拒绝服务 (DoS) 攻击是一种试图让计算机资源对其目标用户不可用的攻击。此攻擊通常是透過使資源過載來完成，例如：

* 來自外部來源的大量請求。
* 系統無法成功傳遞的更多資訊請求。

   例如，整個存放庫的JSON表示法。

* 藉由請求包含不限數量URL的內容頁面，URL可以包含控制代碼、某些選取器、副檔名和尾碼 — 任何都可以修改。

   例如， `.../en.html` 也可以以下列身分要求：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效的變數(例如，傳回 `200` 回應且已設定為快取)會由Dispatcher快取，最終導致完整的檔案系統，而且沒有服務可進一步要求。

有許多設定點可防止此類攻擊，但此處僅討論與AEM相關的那些點。

**設定Sling以避免DoS**

Sling是 *以內容為中心*. 處理著重於內容，因為每個(HTTP)請求都會對應到JCR資源（存放庫節點）形式的內容：

* 第一個目標是儲存內容的資源（JCR節點）。
* 其次，轉譯器或指令碼會位於資源屬性中，且包含請求的某些部分（例如選取器和/或擴充功能）。

另請參閱 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing) 以取得詳細資訊。

這種方法讓Sling功能強大且有彈性，但一如既往，彈性必須謹慎管理。

為協助防止DoS誤用，您可以執行下列動作：

1. 在應用程式層級納入控制項。 由於可能的變異數，預設設定不可行。

   在您的應用程式中，您應該：

   * 控制應用程式中的選取器，讓您 *僅限* 提供所需的明確選取器並傳回 `404` 適用於其他所有使用者。
   * 防止輸出無限數量的內容節點。

1. 檢查預設轉譯器的設定，這可能是一個問題區域。

   * 尤其是JSON轉譯器會跨多個層級轉換樹狀結構。

      例如，請求：

      `http://localhost:4502/.json`

      可能會以JSON表示法傾印整個存放庫，這可能會導致嚴重的伺服器問題。 因此，Sling會設定結果數量上限。 若要限制JSON演算的深度，請設定下列專案的值：

      **JSON最大結果** ( `json.maximumresults`)

      在的設定中 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). 超過此限制時，演算會收合。 AEM中Sling的預設值為 `1000`.

   * 作為預防性測量，您應該停用其他預設轉譯器(HTML、純文字、XML)。 同樣地，透過設定 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >請勿停用JSON轉譯器，因為AEM的正常操作需要它。

1. 使用防火牆來篩選執行個體的存取權。

   * 若要篩選存取執行個體的點，若未加以保護，可能會導致拒絕服務攻擊，則必須使用作業系統層級防火牆。

**針對使用表單選取器所導致的DoS減輕影響**

>[!NOTE]
>
>這項緩解作業只應在未使用Forms的AEM環境中執行。

因為AEM不會為 `FormChooserServlet`，在查詢中使用表單選擇器可能會觸發代價高昂的存放庫周遊作業，通常會讓AEM執行個體陷入停頓。 表單選取器可透過以下專案來偵測： **&amp;ast；.form.&amp;ast；** 字串。

若要緩解此問題，您可以執行下列步驟：

1. 將瀏覽器指向，即可前往Web主控台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*

1. 搜尋 **Day CQ WCM表單選擇器Servlet**
1. 按一下專案後，請停用 **進階搜尋需求** 於下列視窗中。

1. 单击“**保存**”。

**減輕資產下載Servlet所導致DoS的影響**

預設的資產下載servlet可讓已驗證身分的使用者發出任意大型的並行下載請求，以建立資產的ZIP檔案。 建立大型ZIP封存可能會使伺服器和網路過載。 若要降低此行為所導致的潛在拒絕服務(DoS)風險， `AssetDownloadServlet` OSGi元件預設為停用於 [!DNL Experience Manager] 發佈執行個體。 啟用日期 [!DNL Experience Manager] 依預設，編寫執行個體。

如果您不需要下載功能，請在作者和發佈部署上停用servlet。 如果您的設定需要啟用資產下載功能，請參閱 [本文](/help/assets/download-assets-from-aem.md) 以取得詳細資訊。 此外，您也可以定義部署可支援的最大下載限制。

### 停用WebDAV {#disable-webdav}

停止適當的OSGi套件組合，以在製作和發佈環境中停用WebDAV。

1. 連線至 **Felix管理主控台** 執行於：

   `https://<*host*>:<*port*>/system/console`

   例如：`http://localhost:4503/system/console/bundles`。

1. 在套件組合清單中，找到名為的套件：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 若要停止此組合，請在「動作」欄中按一下停止按鈕。

1. 再次在套件組合清單中，找到名為的套件：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 若要停止此組合，請按一下停止按鈕。

   >[!NOTE]
   >
   >不需要重新啟動AEM。

### 確認您未在使用者首頁路徑中公開個人識別資訊 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

請務必確保不會公開存放庫使用者首頁路徑中的任何個人識別資訊，以保護您的使用者。

自AEM 6.1起，使用者（也稱為可授權） ID節點名稱的儲存方式會隨著新的實施而改變 `AuthorizableNodeName` 介面。 新介面不再公開節點名稱中的使用者ID，而是產生隨機名稱。

啟用時不必執行任何設定，因為現在這是在AEM中產生可授權ID的預設方式。

雖然不建議使用，但您可以將其停用，以防您需要舊實作以便與現有應用程式回溯相容。 若要這麼做，您必須執行下列動作：

1. 前往Web主控台，並從屬性中移除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**專案 **requiredServicePids** 在 **Apache Jackrabbit Oak SecurityProvider**.

   您也可以尋找Oak安全性提供者 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** OSGi設定中的PID。

1. 刪除 **Apache Jackrabbit Oak隨機可授權節點名稱** Web主控台的OSGi設定。

   為了更方便查閱，此設定的PID為 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>如需詳細資訊，請參閱Oak檔案，網址為 [可授權節點名稱產生](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 匿名許可權強化套件 {#anonymous-permission-hardening-package}

依預設，AEM會儲存系統中繼資料，例如 `jcr:createdBy` 或 `jcr:lastModifiedBy` 作為節點屬性，位於存放庫中的一般內容旁。 視設定和存取控制設定而定，在某些情況下，這可能會導致個人識別資訊(PII)外洩，例如當這類節點呈現為原始JSON或XML時。

如同所有存放庫資料，這些屬性是由Oak授權棧疊所中介。 應根據最低許可權原則限制存取這些許可權。

為了支援此功能，Adobe提供許可權強化套件，作為客戶進行建置的基礎。 其運作方式是在存放庫根目錄安裝「拒絕」存取控制專案，限制對常用系統屬性的匿名存取。 套件可供下載 [此處](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) 和可以安裝在所有支援的AEM版本上。

為了說明變更，我們可以在安裝套件之前比較可匿名檢視的節點屬性：

![安裝套件之前](/help/sites-administering/assets/before_resized.png)

以及安裝套件後可檢視的專案，其中 `jcr:createdBy` 和 `jcr:lastModifiedBy` 不可見：

![安裝套件後](/help/sites-administering/assets/after_resized.png)

如需詳細資訊，請參閱套件發行說明。

### 防御点击劫持攻击 {#prevent-clickjacking}

為防止點選劫持，Adobe建議您設定網頁伺服器，以提供 `X-FRAME-OPTIONS` HTTP標頭設定為 `SAMEORIGIN`.

如需點選劫持的詳細資訊，請參閱 [OWASP網站](https://www.owasp.org/index.php/Clickjacking).

### 請務必視需要正確復寫加密金鑰 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和驗證配置需要您在所有AEM執行個體上復寫加密金鑰。

在執行此操作之前，不同版本之間的金鑰復寫會有所不同，因為6.3版與舊版之間的金鑰儲存方式不同。

如需詳細資訊，請參閱下文。

#### 複製AEM 6.3的金鑰 {#replicating-keys-for-aem}

而在舊版本中，複製金鑰會儲存在存放庫中，從AEM 6.3開始，會儲存在檔案系統上。

因此，若要跨執行個體複製金鑰，請將金鑰從來源執行個體複製到檔案系統上的目標執行個體位置。

更具體地說，您必須執行下列動作：

1. 存取包含要複製之重要素材的AEM例項（通常是作者例項）；
1. 在本機檔案系統中找到com.adobe.granite.crypto.file套件組合。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   此 `bundle.info` 每個資料夾內的檔案會識別該套件組合名稱。

1. 導覽至資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 複製HMAC和主檔案。
1. 然後，前往您要將HMAC金鑰複製到的目標執行個體，並導覽至資料資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 貼上您先前複製的兩個檔案。
1. [重新整理加密套件組合](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目標執行個體已在執行中。
1. 對您要複製金鑰的所有執行個體重複上述步驟。

>[!NOTE]
>
>第一次安裝AEM時，您可以新增下列引數，回覆成6.3版之前儲存金鑰的方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 複製AEM 6.2和更舊版本的金鑰 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2和更早版本中，金鑰會儲存在存放庫中的 `/etc/key` 節點。

跨執行個體安全複製金鑰的建議方法是僅複製此節點。 您可以透過CRXDE Lite選擇性地復寫節點：

1. 開啟CRXDE Lite，方法是前往 *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. 選取 `/etc/key` 節點。
1. 前往 **復寫** 標籤。
1. 按下 **復寫** 按鈕。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe建議您在進入生產階段之前，先對AEM基礎架構執行滲透測試。

### 開發最佳實務 {#development-best-practices}

新開發必須遵循 [安全性最佳實務](/help/sites-developing/security.md) 以確保您的AEM環境保持安全。
