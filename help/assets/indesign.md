---
title: 整合 [!DNL Assets] 替換為 [!DNL InDesign Server]
description: 瞭解如何整合 [!DNL Adobe Experience Manager Assets] 替換為 [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# 整合 [!DNL Adobe Experience Manager Assets] 替換為 [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用：

* 用於分配特定處理任務負載的Proxy。 Proxy是 [!DNL Experience Manager] 與Proxy Worker通訊以完成特定任務和其他任務的例項 [!DNL Experience Manager] 執行個體以傳遞結果。
* 定義和管理特定任務的Proxy Worker。
這些功能可涵蓋各種作業；例如，使用 [!DNL InDesign Server] 以處理檔案。

若要將檔案完全上傳至 [!DNL Experience Manager Assets] 您已使用建立的 [!DNL Adobe InDesign] 已使用Proxy。 這會使用Proxy Worker與 [!DNL Adobe InDesign Server]，其中 [指令碼](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 執行以擷取中繼資料並產生各種轉譯 [!DNL Experience Manager Assets]. Proxy Worker會啟用 [!DNL InDesign Server] 和 [!DNL Experience Manager] 雲端設定中的例項。

>[!NOTE]
>
>[!DNL Adobe InDesign] 以兩種不同的方案提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 用於為列印和數位發佈設計頁面佈局的案頭應用程式。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 可讓您根據已建立的檔案，以程式設計方式建立自動化檔案 [!DNL InDesign]. 它是作為一項服務提供介面給其 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Script是以 [!DNL ExtendScript]，類似於 [!DNL JavaScript]. 如需有關的資訊 [!DNL InDesign] 指令碼請參閱 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## 擷取的運作方式 {#how-the-extraction-works}

此 [!DNL Adobe InDesign Server] 可以與整合 [!DNL Experience Manager Assets] 這樣建立的INDD檔案 [!DNL InDesign] 可以上傳、產生轉譯、擷取所有媒體（例如視訊）並儲存為資產：

>[!NOTE]
>
>舊版 [!DNL Experience Manager] 能夠擷取XMP和縮圖，現在可以擷取所有媒體。

1. 將您的INDD檔案上傳到 [!DNL Experience Manager Assets].
1. 框架會將命令指令碼傳送至 [!DNL InDesign Server] 透過SOAP （簡單物件存取通訊協定）。
這個命令指令碼會：

   * 擷取INDD檔案。
   * 執行 [!DNL InDesign Server] 命令：

      * 會擷取結構、文字及任何媒體檔案。
      * 會產生PDF和JPG轉譯。
      * 會產生HTML和IDML轉譯。
   * 將產生的檔案發佈回 [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML是以XML為基礎的格式，可轉譯所有內容 [!DNL InDesign] 檔案。 它會以壓縮封裝形式儲存，使用 [ZIP](https://www.techterms.com/definition/zip) 壓縮。 如需詳細資訊，請參閱 [InDesign交換格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 尚未安裝或未設定，則您仍可上傳INDD檔案至 [!DNL Experience Manager]. 不過，產生的轉譯將限製為PNG和JPEG。 您將無法產生HTML、.idml或頁面轉譯。

1. 產生擷取和轉譯後：

   * 此結構會復寫至 `cq:Page` （轉譯型別）。
   * 擷取的文字和檔案會儲存在 [!DNL Experience Manager Assets].
   * 所有轉譯都儲存在 [!DNL Experience Manager Assets]，在資產本身中。

## 整合 [!DNL InDesign Server] 具有Experience Manager {#integrating-the-indesign-server-with-aem}

若要整合 [!DNL InDesign Server] 搭配使用 [!DNL Experience Manager Assets] 設定Proxy後，您需要：

1. [安裝InDesign Server](#installing-the-indesign-server).
1. 如有需要， [設定Experience Manager Assets工作流程](#configuring-the-aem-assets-workflow).
只有在預設值不適合您的執行個體時，才需要執行此操作。
1. 設定 [InDesign Server的Proxy背景工作](#configuring-the-proxy-worker-for-indesign-server).

### 安裝 [!DNL InDesign Server] {#installing-the-indesign-server}

若要安裝並啟動 [!DNL InDesign Server] 搭配使用 [!DNL Experience Manager]：

1. 下載並安裝 [!DNL InDesign Server].

1. 如有需要，您可以自訂 [!DNL InDesign Server] 執行個體。

1. 從命令列啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這將啟動伺服器，並在連線埠8080上接聽SOAP外掛程式。 所有日誌訊息和輸出都直接寫入命令視窗。

   >[!NOTE]
   >
   >如果您要將輸出訊息儲存至檔案，則使用重新導向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 設定 [!DNL Experience Manager Assets] 工作流程 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 有預先設定的工作流程 **[!UICONTROL DAM更新資產]**，其中包含數項專門用於下列用途的處理步驟 [!DNL InDesign]：

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

此工作流程設定了預設值，這些值可以適應您在各種作者執行個體上的設定(這是標準工作流程，因此如需詳細資訊，請參閱 [編輯工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果您使用預設值（包括SOAP連線埠），則不需要進行設定。

設定完成後，上傳 [!DNL InDesign] 檔案到 [!DNL Experience Manager Assets] （透過任何一般方法）觸發工作流程來處理資產並準備各種轉譯。 透過上傳INDD檔案到測試您的設定 [!DNL Experience Manager Assets] 確認您看見底下由ID建立的不同轉譯 `<*your_asset*>.indd/Renditions`

#### 媒體擷取 {#media-extraction}

此步驟會控制從INDD檔案擷取媒體。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 媒体提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript資料庫**：這是簡單的http get/post方法程式庫，其他指令碼會需要此程式庫。

* **擴充指令碼**：您可以在此處指定不同的指令碼組合。 如果您希望自己的指令碼在 [!DNL InDesign Server]，將指令碼儲存在 `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>请勿更改 ExtendScript 库。此程式庫提供與Sling通訊所需的HTTP功能。 此設定會指定要傳送至的程式庫 [!DNL InDesign Server] 以便在該處使用。

此 `ThumbnailExport.jsx` 媒體提取工作流程步驟執行的指令碼會產生JPG格式的縮圖轉譯。 「處理縮圖」工作流程步驟使用此轉譯來產生所需的靜態轉譯 [!DNL Experience Manager].

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確定您並未移除預設值，因為 [!DNL Experience Manager Assets] 介面。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為不再需要它。

#### 頁面擷取 {#page-extraction}

這會建立 [!DNL Experience Manager] 頁面擷取元素。 擷取處理常式用於從轉譯(目前為HTML或IDML)中擷取資料。 然後會使用此資料來使用PageBuilder建立頁面。

要进行自定义，可以编辑&#x200B;**[!UICONTROL 页面提取]**&#x200B;步骤的&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**：從快顯清單中選取您要使用的處理常式。 提取处理程序对相关 `RenditionPicker` 选择的特定演绎版发挥作用（请参阅 `ExtractionHandler` API）。在標準 [!DNL Experience Manager] 安裝下列專案可供使用：
   * IDML匯出擷取控制代碼：對下列專案操作： `IDML` MediaExtract步驟中產生的轉譯。

* **頁面名稱**：指定您要指派給產生頁面的名稱。 如果保留為空白，則名稱是「page」（如果已存在「page」，則為衍生物）。

* **頁面標題**：指定您要指派給產生頁面的標題。

* **頁面根路徑**：結果頁面的根位置的路徑。 如果保留為空白，則會使用儲存資產轉譯的節點。

* **頁面範本**：產生結果頁面時要使用的範本。

* **頁面設計**：產生結果頁面時要使用的頁面設計。

### 設定Proxy背景工作 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Worker位在Proxy執行個體上。

1. 在「工具」控制檯中，展開 **[!UICONTROL Cloud Services設定]** 在左窗格中。 然後展開 **[!UICONTROL 雲端Proxy設定]**.

1. 双击 **[!UICONTROL IDS worker]** 以打开进行配置。

1. 按一下 **[!UICONTROL 編輯]** 若要開啟組態對話方塊並定義必要的設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS集區**
用來與通訊的SOAP端點 [!DNL InDesign Server]. 您可以新增、移除及訂購必要專案。

1. 按一下「確定」以儲存。

### 設定Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果 [!DNL InDesign Server] 和 [!DNL Experience Manager] 位於不同主機上，或其中一個或兩個應用程式在預設連線埠上無法運作，然後設定 [!UICONTROL Day CQ連結外部化器] 設定主機名稱、連線埠和內容路徑 [!DNL InDesign Server].

1. 存取Web主控台，網址為 `https://[aem_server]:[port]/system/console/configMgr`.
1. 找到設定 **[!UICONTROL Day CQ連結外部化器]**. 按一下 **[!UICONTROL 編輯]** 以開啟。
1. 連結外部化程式設定有助於為建立絕對URL [!DNL Experience Manager] 的部署和 [!DNL InDesign Server]. 使用 **[!UICONTROL 網域]** 欄位來指定主機名稱 [!DNL Adobe InDesign Server]. 单击“**保存**”。

   在絕對URL中，使用 `localhost` 作為本機（作者）執行個體的主機名稱，以及發佈執行個體的主機名稱或IP位址，如下圖所示。

   ![連結外部化程式設定](assets/link-externalizer-config.png)

### 啟用並行工作處理 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

您現在可以啟用ID的平行作業處理。 決定平行作業的最大數量(`x`)和 [!DNL InDesign Server] 可以處理：

* 在單一多處理器電腦上，平行作業的最大數量(`x`)表示 [!DNL InDesign Server] 可以處理比執行ID的處理器數目少一個。
* 當您在多部機器上執行ID時，您需要計算可用的處理器總數（即所有機器上的處理器總數），然後減去機器總數。

若要設定平行ID作業的數目：

1. 開啟 **[!UICONTROL 設定]** 標籤進行識別，例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 選取IDS處理佇列於 `Apache Sling Job Queue Configuration`.

1. 套:

   * **类型** - `Parallel`
   * **最大平行作業數** - `<*x*>` （如上計算）

1. 儲存這些變更。
1. 若要啟用AdobeCS6和更新版本的多工作階段支援，請核取 `enable.multisession.name` 核取方塊，下 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定。
1. 建立 [集區： `x` 將SOAP端點新增至IDS Worker設定來建立IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   如果有多台電腦在執行 [!DNL InDesign Server]，為每部機器新增SOAP端點（每部機器的處理器數目–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用背景工作集區時，您可以啟用IDS背景工作區的封鎖清單。
>
>若要這麼做，請啟用 **[!UICONTROL enable.retry.name]** 核取方塊，位於 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定，可啟用IDS工作重試。
>
>此外，在 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 設定，設定正值 `max.errors.to.blacklist` 引數可決定從工作處理常式清單中禁止ID之前的工作重試次數。
>
>依預設，在可設定的(`retry.interval.to.whitelist.name`)重新驗證IDS工作者所需的時間（以分鐘為單位）。 如果工作程式線上上找到，則會從封鎖清單中將其移除。

## 啟用支援 [!DNL InDesign Server] 10.0或更新版本 {#enabling-support-for-indesign-server-or-later}

對象 [!DNL InDesign Server] 10.0或更新版本，執行以下步驟以啟用多工作階段支援。

1. 從您的開啟設定管理員 [!DNL Experience Manager Assets] 例項 `https://[aem_server]:[port]/system/console/configMgr`.
1. 編輯設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. 選取 **[!UICONTROL ids.cc.enable]** 選項，然後按一下 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>對象 [!DNL InDesign Server] 與整合 [!DNL Experience Manager Assets]，請使用多核心處理器，因為單核心系統不支援整合所需的作業階段支援功能。

## 設定 [!DNL Experience Manager] 認證 {#configure-aem-credentials}

您可以變更用來存取的預設管理員認證（使用者名稱和密碼）。 [!DNL InDesign Server] 從您的 [!DNL Experience Manager] 部署，而不中斷與的整合 [!DNL InDesign Server].

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存認證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

