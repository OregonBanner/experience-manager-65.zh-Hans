---
title: 基本設定概念
seo-title: Basic Configuration Concepts
description: 瞭解如何設定AEM。
seo-description: Learn how to configure AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 1%

---

# 基本設定概念{#basic-configuration-concepts}

Adobe Experience Manager (AEM)已安裝所有引數的預設設定，可讓其「開箱即用」。 不過，您可以根據自己的特定需求設定AEM。

AEM有許多方面可以設定：

* 部分為 [通常為每個專案安裝設定](#primary-configuration-considerations) 而且必須經過稽核，確認其是否適用於您的專案。
* [其他設定](#further-configuration-considerations) 可能是通用的，但不是強制性的；與功能或系統效能和穩定性相關。
* 只有AEM的某些選用功能才需要其他功能（這些功能會與適當的功能一起記錄）。

視特定設定而定，這些變更可使用以下任一項來進行：

* **Adobe CQ Web Console**

   這是設定OSGi套件組合和服務的標準位置。

   另請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得進一步詳細資訊和建議作法。

* **存储库**

   存放庫中提供OSGi設定的子集。 這樣可確保複製或複製存放庫內容會重新建立相同的設定。 您也可以根據執行模式將自己的設定新增到存放庫。

   另請參閱 [存放庫中的OSGi設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 尤其是 [新增設定至存放庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) 以取得更多詳細資料。

* **檔案系統**

   檔案系統內有一些組態檔。

* **AEM WCM**

   您可以在AEM WCM本身中設定各種面向，許多情況下都會使用 [工具](/help/sites-administering/tools-consoles.md) 主控台；例如，復寫代理。

>[!NOTE]
>
>使用Adobe Experience Manager時，有數種方法可管理OSGi服務的組態設定（主控台或存放庫節點）。
>
>另請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

>[!NOTE]
>
>設定AEM很簡單，但您必須注意：
>
>某些變更可能會對應用程式產生重大影響。 因此，在開始設定AEM之前，請確定您具備必要的經驗和知識，並只進行您知道必要的變更。 透過OSGi主控台所做的任何變更包括 **立即** 套用至執行中的系統（不需要重新啟動）。

## 主要設定考量事項 {#primary-configuration-considerations}

此清單詳細說明每個新專案通常設定的主要區域。 並非所有專案都需要，但必須閱讀清單並加以檢閱，以瞭解哪些專案適用於您的專案。

清單提供每個設定方面的簡短概觀，以及提供完整詳細資訊的頁面連結。

### 安全性檢查清單 {#security-checklist}

中列出了幾個主要設定問題 [安全性檢查清單](/help/sites-administering/security-checklist.md). 請確定您已閱讀本文，並採取安裝所需的任何動作。

### 設定預設UI — 觸控最佳化或Classic {#configuring-the-default-ui-touch-optimized-or-classic}

AEM中有兩個可供使用的UI：

* 觸控最佳化的UI
* 傳統UI

您可以使用設定所需的UI [根對應](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>如需有關選取UI的更多資訊，請參閱 [選取您的UI](/help/sites-authoring/select-ui.md).

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如存放庫、Dispatcher等）都可以安裝在IPv4和IPv6網路中。

操作是順暢的，因為不需要特殊設定，需要時您只需使用適合您網路型別的格式來指定IP位址。

這表示當需要指定IP位址時，您可以（視需要）從以下選取：

* ipv6位址

   例如 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* ipv4位址

   例如 `https://123.1.1.4:4502`

* 伺服器名稱

   例如， `https://www.yourserver.com:4502`

* 預設大小寫為 `localhost` 將針對IPv4和IPv6網路安裝進行解譯

   例如， `http://localhost:4502`

### 版本清除 {#version-purging}

在標準安裝中，每當您啟動頁面時（更新內容後），AEM都會建立頁面或節點的新版本。您也可以使用根據請求建立其他版本 **版本設定** 索引標籤。 所有這些版本都儲存在存放庫中，並可在必要時還原。

這些版本永遠不會清除，因此存放庫大小會隨著時間增長，因此需要管理。

另請參閱 [版本清除](/help/sites-deploying/version-purging.md) 以取得完整詳細資訊，特別是 [版本管理員](/help/sites-deploying/version-purging.md#version-manager) 瞭解如何設定AEM在建立新版本時清除舊版本的詳細資訊。

### 日志记录 {#logging}

AEM可讓您設定：

* 中央記錄服務的全域引數
* 請求資料記錄；請求資訊的專用記錄設定
* 個別服務的特定設定；例如，個別記錄檔和記錄訊息的格式

另請參閱 [記錄](/help/sites-deploying/configure-logging.md) 以取得完整詳細資訊。

### 运行模式 {#run-modes}

執行模式可讓您針對特定目的調整AEM執行個體；例如製作或發佈、測試、開發或內部網路等。

這是透過定義每個執行模式的設定引數集合來完成的。 所有執行模式都會套用一組基本組態引數，然後您就可以根據特定環境的目的調整其他組。 然後視需要套用這些引數。

所有組態設定都會儲存在單一存放庫中，並透過設定 **執行模式**.

另請參閱 [執行模式](/help/sites-deploying/configure-runmodes.md) 以取得完整詳細資訊。

### 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供一次驗證認證（例如使用者名稱和密碼）之後存取多個系統。 獨立的系統（稱為受信任的驗證者）會執行驗證並提供Experience Manager使用者認證。 Experience Manager會檢查並強制使用者的存取許可權（即決定允許使用者存取哪些資源）。

另請參閱 [單一登入](/help/sites-deploying/single-sign-on.md) 以取得更多詳細資料。

### 资源映射 {#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些對應來：

* 所有請求的前置詞為 `/content` 以便對網站的訪客隱藏內部結構。
* 定義重新導向，讓所有要求到 `/content/en/gateway` 您的網站頁面會重新導向至 `https://gbiv.com/`.

另請參閱 [資源對應](/help/sites-deploying/resource-mapping.md) 以取得更多詳細資料。

### 復寫、反向復寫和復寫代理程式 {#replication-reverse-replication-and-replication-agents}

復寫代理程式是AEM的核心，因為可用來：

* [發佈（啟動）](/help/sites-authoring/publishing-pages.md) 內容從作者環境移至發佈環境。
* 明確地從Dispatcher快取排清內容。
* 從發佈環境將使用者輸入（例如表單輸入）傳回至作者環境（在作者環境的控制下）。

如需詳細資訊，請參閱 [復寫](/help/sites-deploying/replication.md).

### OSGi組態設定 {#osgi-configuration-settings}

[osgi](https://www.osgi.org/) 是AEM技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

另請參閱 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md) 取得與專案實作相關的各種套件組合清單（根據套件組合列出）。 並非所有列出的設定都需要調整，有些是為了協助您瞭解AEM的運作方式。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

### 設定LDAP {#configuring-ldap}

需要進行LDAP驗證，才能驗證儲存在（中央） LDAP目錄（例如Active Directory）中的使用者。 這有助於減少管理使用者帳戶所需的工作。

LDAP驗證會發生在存放庫層級，因此直接由存放庫處理。 如需詳細資訊，請參閱 [使用AEM設定LDAP](/help/sites-administering/ldap-config.md).

如需AEM內的使用者管理（包括存取許可權的指派），請參閱 [使用者管理與安全性](/help/sites-administering/security.md).

### 設定Dispatcher {#configuring-the-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具，可与企业级 Web 服务器结合使用。

另請參閱 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 以取得完整詳細資訊，特別是 [設定Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 以取得進一步的設定詳細資料。

### 設定AEMLiveCycle聯結器 {#configuring-aem-livecycle-connector}

隨著AEM Doc Services和AEM Doc Security的發行，我們現在能夠叫用LiveCycle檔案服務來轉譯XFA表單、將檔案轉換為PDF以及原則保護檔案。 請閱讀 [AEMLiveCycle聯結器](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) 以取得更多詳細資料。

### 工作解除安裝與拓撲管理 {#job-offloading-and-topology-administration}

[解除安裝](/help/sites-deploying/offloading.md) 將處理工作分散到拓撲中的Experience Manager執行個體。 透過解除安裝，您可以使用特定Experience Manager執行個體來執行特定型別的處理。 專業化的處理可讓您最大限度地使用可用的伺服器資源。

拓撲是參與解除安裝的鬆散耦合Experience Manager叢集。 叢集由一或多個Experience Manager伺服器執行處理（單一執行處理視為叢集）組成。

如需如何檢視或修改拓撲成員資格的詳細資訊，請參閱 [管理拓撲](/help/sites-deploying/offloading.md#administering-topologies) 區段。

### 設定歡迎主控台 {#configuring-the-welcome-console}

傳統UI的「歡迎」主控台提供AEM內各種主控台和功能的連結清單。

您可以設定可見的連結，請參閱 [設定歡迎主控台](/help/sites-developing/customizing-the-welcome-console.md) 以取得更多詳細資料。

### 設定效能 {#configuring-for-performance}

[效能](/help/sites-deploying/configuring-performance.md) 是專案的關鍵。 AEM的某些方面（和/或基礎存放庫）可以設定為最佳化效能。

另請參閱 [設定效能](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 以取得更多詳細資料。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共用資料存放區 {#shared-data-store}

存放庫資料存放區可用來將大型二進位檔的儲存空間從適當的存放庫解除安裝至個別區域，因此存放庫樹狀結構中同一個二進位檔的多個執行個體（例如影像）只會儲存一次。

此「一次儲存、多次參照」功能可擴充為不僅提供單一存放庫樹狀結構，也提供完全不同的存放庫，方法是設定每個存放庫的資料存放區來參照相同的共用檔案系統位置。

這類資料存放區可在相同叢集中的不同節點、相同安裝中的不同發佈和/或製作執行個體或甚至不同安裝中的完全不同執行個體之間共用。

如需詳細資訊，請參閱 [設定資料存放區和節點存放區](/help/sites-deploying/data-store-config.md).

## 其他設定考量事項 {#further-configuration-considerations}

### 啟用HTTP over SSL {#enabling-http-over-ssl}

您可以啟用透過SSL的HTTP，以使用與伺服器的更安全連線。

另請參閱 [啟用HTTP over SSL](/help/sites-administering/ssl-by-default.md) 以取得更多詳細資料。

### AEM入口網站和Portlet {#aem-portals-and-portlets}

入口網站是一種網站應用程式，可提供個人化、單一登入、不同來源的內容整合，並託管資訊系統的展示層。 Portlet元件也可讓您在頁面上內嵌Portlet。 若要存取CQ5 WCM提供的內容，入口網站伺服器可安裝CQ5入口網站Director Portlet。 您可以安裝、設定Portlet並將其新增至入口網站頁面，以執行此操作。

另請參閱 [入口網站和Portlet](/help/sites-administering/aem-as-portal.md) 以取得更多詳細資料。

### 靜態物件的到期日 {#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，系統應設定為不會過期（在合理的時間段內），並減少不必要的流量。

另請參閱 [靜態物件的到期日](/help/sites-deploying/expiration-static-objects.md) 以取得更多詳細資料。

### Java程式中的開啟檔案 {#open-files-in-the-java-process}

每個Java程式都可以存取檔案 — 這需要系統資源。 因此，上限被定義為每個程式可同時存取多少檔案。 如果超過此限制，則可能會發生例外狀況錯誤。

如果AEM處理序超過此上限，則訊息「 `too many open files`「」將顯示在 `error.log`.

若要避免此類例外，您需要：

1. 檢查您的AEM程式正在使用多少個開啟的檔案。

   如何進行這項檢查將取決於執行個體所在的平台。 您可以使用lsof (Unix)或Process Explorer (Windows)等公用程式。

   在開發和測試期間應監控此值，以：

   * 確認檔案已視需要關閉
   * 以決定所需的最大值（在各種情況下）

1. 設定允許的最大值。

   新值應同時符合目前的需求和任何未來的尖峰，因此建議將目前的需求加倍。

   依預設， `serverctl` 設定 `CQ_MAX_OPEN_FILES` 至 `8192`；這應該足以滿足大多數情境。

### 設定RTF編輯器 {#configuring-the-rich-text-editor}

此 **RTF編輯器** (**RTE**)為作者提供各式各樣的 [功能](/help/sites-authoring/rich-text-editor.md) 用於編輯其文字內容；為它們提供用於所見即所得體驗的圖示、選取方塊和選單。

另請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md) 以取得更多詳細資料。

### 設定頁面編輯的復原 {#configuring-undo-for-page-editing}

有數個屬性可控制編輯頁面的還原和重做命令的行為。 這些可設定，請參閱 [設定頁面編輯的復原](/help/sites-administering/config-undo.md) 以取得更多詳細資料。

### 設定視訊元件 {#configuring-the-video-component}

此 [視訊元件](/help/sites-authoring/default-components-foundation.md#video) 可讓您在頁面上放置預先定義的現成視訊元素。

為了進行適當的轉碼，您的管理員必須 [安裝FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) 另外提供。 他們也可以 [設定您的視訊設定檔](/help/sites-administering/config-video.md#configure-video-profiles) 與html5元素搭配使用。

### 設定和自訂報表 {#configuring-and-customizing-reports}

為協助您監控及分析執行個體的狀態，CQ提供一系列預設報表，您可依個別需求加以設定：

請參閱 [報表自訂基本概念](/help/sites-administering/reporting.md#the-basics-of-report-customization) 以取得更多詳細資料。

### 設定電子郵件通知 {#configuring-email-notification}

CQ傳送電子郵件通知給使用者，該使用者：

* 已訂閱頁面事件，例如修改或復寫。
* 已訂閱論壇事件。
* 必須在工作流程中執行步驟。

另請參閱 [設定電子郵件通知](/help/sites-administering/notification.md) 以取得更多詳細資料。

### 啟用頁面印象 {#enabling-page-impressions}

頁面印象會顯示在 **曝光次數** classic UI siteadmin console的欄。 若要啟用頁面印象的擷取，您需要設定：

* 在發佈執行個體上：

   * [Day CQ WCM頁面統計資料](/help/sites-deploying/osgi-configuration-settings.md)

* 在作者執行個體上：

   * [Adobe頁面曝光數追蹤](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>作者環境上Adobe頁面曝光數追蹤器的設定將允許向追蹤服務提出匿名請求。
