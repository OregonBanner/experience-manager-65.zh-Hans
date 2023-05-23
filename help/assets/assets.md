---
title: 简介 [!DNL Adobe Experience Manager Assets]
description: 瞭解什麼是數位資產管理、其使用案例和 [!DNL Adobe Experience Manager Asset] 方案。
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# 關於 [!DNL Adobe Experience Manager Assets] 作為DAM解決方案 {#administering-assets}

[!DNL Assets] 是數位資產管理(DAM)工具，是 [!DNL Experience Manager] 平台，讓您的企業能夠管理和散佈數位資產。 組織的使用者可以管理、儲存和存取許多型別的數位資產，例如影像、影片、檔案、音訊片段、3D檔案和豐富多彩的媒體，以便在網路、印刷品和數位發行中使用。

## 什麼是數位資產管理？ {#what-is-digital-asset-management}

[!DNL Assets] 提供企業範圍內共用和發佈組織關鍵數位資產的功能。 組織的使用者可以透過Web介面（或CIFS或WebDAV資料夾）儲存、管理和存取數位資產，例如影像、圖形、音訊、視訊和檔案。

[!DNL Assets] 功能 [!DNL Experience Manager] 可讓您進行下列作業：

* 以各種檔案格式新增和共用影像、檔案、音訊檔案和視訊檔案。
* 透過按標籤、燈箱或星星（您的最愛）分組來管理資產。 新增註解至資產。
* 透過搜尋檔案名稱、檔案全文以及搜尋日期、檔案型別和標籤來尋找資產。
* 新增或編輯資產的中繼資料資訊。 中繼資料會自動與對應的資產一起建立版本。 您可以匯入或匯出資產中繼資料。
* 執行影像編輯功能，例如縮放和新增影像濾鏡。 使用WebDAV或CIFS資料夾同時匯入和匯出多個數位資產。
* 使用工作流程與通知允許共同處理和下載任何資產集，並管理資產的存取許可權。

### [!DNL Experience Manager Assets] 與整合 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 完全整合 [!DNL Sites] 和適用於所有使用案例。 例如，編寫網頁時， [!DNL Sites] 作者可透過「內容尋找器」尋找及使用數位資產。 的使用者介面 [!DNL Assets] 與的相同 [!DNL Sites]. 另請參閱 [網站概觀](/help/sites-authoring/page-authoring.md) 以取得完整詳細資訊。

基本使用者介面與相同， [!DNL Sites]. 另請參閱 [Sites概述](/help/sites-authoring/page-authoring.md) 以取得完整詳細資訊。

### 數位資產管理與影像元件 {#digital-asset-management-versus-image-component}

在決定要將影像放入DAM存放庫或使用影像元件時，請考慮影像生命週期：

* 如果影像的生命週期與頁面相同，請使用影像元件。
* 如果影像有單獨的生命週期，例如，如果您使用影像兩次或在WCM外部，請使用 [!DNL Assets].

## 什麼是數位資產？ {#what-are-digital-assets}

資產是數位檔案、影像、視訊或音訊（或其中一部分），可以多次轉譯也可以有子資產（例如Photoshop檔案中的圖層、PowerPoint檔案中的投影片、pdf中的頁面、ZIP中的檔案）。

資產本質上是二進位加中繼資料、轉譯加子資產。 請參閱 [DAM效能指南](/help/sites-deploying/assets-performance-sizing.md) 詳細資訊。

>[!CAUTION]
>
>上傳和/或編輯大量資產（尤其是影像）可能會影響您的效能 [!DNL Experience Manager] 部署。

### [!DNL Experience Manager Assets] 術語 {#aem-assets-terminology}

在中使用數位資產時 [!DNL Experience Manager]，您必須瞭解下列術語：

* **集合**：資產集合，根據實體位置（資料夾）、一般屬性（儲存的搜尋資料夾）或使用者選擇（燈箱資料夾）。

* **中繼資料** [!DNL Assets] 具有中繼資料；例如，作者、到期日、DRM資訊(Digital Rights Management)等。 中繼資料受存取控制。 [!DNL Assets] 支援下列各種立即可用的常見中繼資料結構：

   * Dublin Core：包括作者、說明、日期、主旨等。
   * IPTC：包括事件、模型、位置等。
   * WCM：包含頁面屬性、 [!UICONTROL 準時] 和 [!UICONTROL 關閉時間]、等等。

* **標籤**： [!DNL Assets] 可以進行標籤和分類。 另請參閱 [組織資產](/help/assets/organize-assets.md).

* **轉譯**：轉譯是資產的二進位表示法。 [!DNL Assets] 一律具有主要表示法 — 上傳檔案的主要表示法。 他們可以建立任何數量的其他表示法，例如透過自訂工作流程步驟或資產上傳時建立。 轉譯可能大小不同、解析度不同、加上了浮水印，或是其他特徵有所變更。

* **版本**：版本設定會在特定時間點建立數位資產的快照。 您可以將資產還原至舊版。 另請參閱 [版本設定 [!DNL Assets]](manage-assets.md#asset-versioning).

* **子資產**：子資產是組成資產的資產，例如 [!DNL Adobe Photoshop] PDF檔案中的一或多個頁面。 在 [!DNL Assets]，您可以像管理資產一樣管理子資產。

### 如何使用數位資產 {#how-to-work-with-assets}

您對資產或集合執行動作。 動作可以建立或修改資產、收藏集和轉譯。 您在資產上執行的許多基本動作（上傳、刪除、更新、儲存子資產）都會觸發預先設定的工作流程。 這些會自動開啟 [!DNL Assets] 和的詳細說明，請參閱 [!DNL Assets] 媒體處理常式。

您可以透過這些預先設定的工作流程執行的任務：

* 將資產儲存在存放庫中，或從存放庫中刪除資產。
* 擷取並儲存資產的中繼資料；個別中繼資料專案會儲存為XMP。
* 為資產產生轉譯和縮圖，包括視需要自動調整大小和裁切。
* 視需要轉碼資產。 例如，行動和Web使用的視訊會以每秒24個影格進行轉碼，而下載的視訊則為每秒30個影格。 行動裝置和網頁使用的音訊會以128 Kbps轉碼，下載時則以192 Kbps轉碼。

當然，您也可以手動套用工作流程。 另請參閱 [Assets媒體處理常式](media-handlers.md)以取得預設工作流程清單。

## [!DNL Experience Manager Assets] 和 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

另請參閱 [Assets與Media Library](medialibrary.md) 以取得差異的相關資訊。

>[!MORELIKETHIS]
>
>* [影片簡介 — Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [瞭解中繼資料概念](/help/assets/metadata-concepts.md)

