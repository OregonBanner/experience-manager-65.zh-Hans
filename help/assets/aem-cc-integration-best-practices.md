---
title: 與Adobe Creative Cloud最佳實務整合
description: 整合的最佳實務 [!DNL Adobe Experience Manager] 替換為 [!DNL Adobe Creative Cloud] 簡化資產轉移工作流程，並達到高內容速度。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '3268'
ht-degree: 16%

---

# [!DNL Adobe Experience Manager] 和 [!DNL Creative Cloud] 整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 是數位資產管理(DAM)解決方案，可整合至 [!DNL Adobe Creative Cloud] 協助DAM使用者與創意團隊合作，簡化內容建立過程中的共同作業。

[!DNL Adobe Creative Cloud] 為創意團隊提供解決方案和服務的生態系統，以協助他們建立數位資產。 其中包括案頭和行動應用程式、雲端服務（例如具備案頭同步處理或網頁體驗的儲存空間），以及行銷場所，例如 [!DNL Adobe Stock].

請閱讀下文，瞭解根據您的使用案例，在案頭版和企業級DAM之間選擇哪些整合，以及哪些是連線工作流程的相關最佳實務。

>[!NOTE]
>
>[!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用功能已過時，不再涵蓋在本指南中。 Adobe建議使用較新的功能，例如 [Adobe資產連結](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 或 [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) 為創意使用者提供對受管理資產的存取權 [!DNL Experience Manager].

## 創意人員、行銷人員和DAM使用者的共同作業需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化創意人員在桌上型電腦上的體驗 | 簡化從DAM存取資產的程式([!DNL Experience Manager Assets])適用於創意專家，或更廣義地說，適用於在原生資產建立應用程式中工作的案頭使用者。 他們需要一種簡單明瞭的方式，以探索、使用（開啟）、編輯和儲存變更 [!DNL Experience Manager]以及上傳新檔案。 | Win或Mac案頭版； [!DNL Creative Cloud] 應用程式 |
| 提供高品質、現成可用的資產，來自 [!DNL Adobe Stock] | 行銷人員可協助資產來源和探索，以加速內容建立流程。 創意專業人士可從其創意工具內直接使用核准的資產。 | [!DNL Experience Manager Assets]； [!DNL Adobe Stock] 市集；中繼資料欄位 |
| 依組織分送和共用資產 | 內部部門/當地分支和外部合作夥伴、經銷商和代理商會使用上級組織共用的已核准資產。 企業想要安全且順暢地共用建立的資產，以更廣泛地重複使用。 | Brand Portal、Asset Share Commons |

## 支援協同合作需求的Adobe方案 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe方案 | 相關曲面 |
|---|---|---|
| 創意使用者從中發現資產 [!DNL Experience Manager]，開啟並使用它們、編輯和上傳變更至 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager]，不離開 [!DNL Creative Cloud] 應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], 和 [!DNL Adobe InDesign]. |
| 企業使用者可簡化資產的開啟與使用、編輯與上傳變更 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager] 從案頭環境。 他們使用一般整合在原生案頭應用程式中開啟任何資產型別，包括非Adobe的資產型別。 | [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac案頭上的案頭應用程式 |
| 行銷人員和商務使用者可探索、預覽、授權和儲存，以及管理 [!DNL Adobe Stock] 資產來源： [!DNL Experience Manager]. 授權和儲存的資產會提供select [!DNL Adobe Stock] 中繼資料，以提升控管能力。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網頁介面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。替代解決方案，例如 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可建置在 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 元件， [連結共用](/help/assets/link-sharing.md)，使用 [Experience Manager Assets](/help/assets/manage-assets.md) 應根據特定需求審查。

![Creative CloudExperience Manager的連線，決定要使用哪個功能](assets/creative-connections-aem.png)

### 使用案例與Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 用例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面应用程序 | 備註/其他解決方案 |
|---|---|---|---|
| 探索 — 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| 探索 — 存取DAM集合 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| 探索 — 從DAM搜尋資產 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| 使用 — 開啟資產 | 是 | 是 | [從Web介面開啟](manage-assets.md#previewing-assets) 或從Finder |
| 使用 — 將來自DAM的資產放入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | [!DNL Experience Manager] 案頭應用程式可讓您存取本機檔案系統上的資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟動作（在網路共用中） | [在AAL中籤出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 預設會將資產儲存至使用者的creative cloud儲存體帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — DAM外部正在進行中的工作 | 是 — 使用者的Creative Cloud儲存帳戶中可用的資產，已同步至案頭。 | 是 |  |
| 編輯 — 上傳變更 | 是 —  [簽入動作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 含選擇性註解 | 是 |  |
| 上傳 — 單一檔案 | 是 — 上傳目前作用中的檔案 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) 或透過自訂指令碼或工具。 |
| 其他 — 使用者和登入 | 可辨識登入Creative Cloud案頭應用程式的Creative Cloud使用者(SSO) | [!DNL Experience Manager] 使用者和認證 | 這兩種解決方案的使用者都會計入 [!DNL Experience Manager] 使用者配額。 |
| 雜項 — 網路與存取 | 需要從使用者案頭存取以下專案： [!DNL Experience Manager] 透過網路部署 | 需要從使用者案頭存取以下專案： [!DNL Experience Manager] 透過網路部署 | [!DNL Adobe Asset Link] 不共用網路Proxy環境。 |
| 其他 — 移轉大量資產 | 否 | 否 | [資產移轉指南](assets-migration-guide.md) |

若要支援資產散佈使用案例，應考慮其他解決方案：

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 對於可設定的SaaS附加元件 [!DNL Experience Manager Assets] 以發佈資產。
* 自訂解決方案是根據 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 程式碼基底。
* [!DNL Experience Manager] [連結共用](/help/assets/link-sharing.md) 使用連結臨機共用資產。
* [Experience Manager Assets網頁介面](/help/assets/manage-assets.md) 外部合作方的區域由以下專案保護 [!DNL Experience Manager] 存取控制設定，以及必要的IT/網路組態調整，讓這些外部使用者能夠存取 [!DNL Experience Manager].

## 重要概念與使用案例 {#key-concepts-and-use-cases}

### 常用辭彙表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **創意就緒資產：** [!DNL Assets] 已準備好更廣泛地與其他團隊共用，或已獲創意團隊選取或核准，要與行銷或LOB團隊共用的對象。
* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。
* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本檔案中，它是以下內容的同義詞： [!DNL Experience Manager Assets]，除非另有特別說明。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM 用户可以是营销或非营销用户，例如业务线 (LOB) 用户、管理员、销售人员等。

### 使用時的注意事項 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合 {#considerations-when-using-aem-and-creative-cloud-integration}

* 另請參閱 [案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 另請參閱 [Adobe Stock整合](aem-assets-adobe-stock.md)
* 另請參閱 [Adobe資產連結](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)

以下為最佳實務的簡短摘要： [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合。 請閱讀本檔案的其餘部分，以取得這些內容的詳細瞭解。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括清晰處理從取出資產的進行中工作 [!DNL Experience Manager].
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：**[!DNL Experience Manager]请使用 桌面应用程序.
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新.
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 存取 [!DNL Adobe Stock] 資產來源 [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) 提供 [!DNL Experience Manager] 能夠搜尋、預覽、授權和儲存資產的使用者，資產來源 [!DNL Adobe Stock] 到 [!DNL Experience Manager]. 授權並儲存 [!DNL Stock] 已選取資產 [!DNL Stock] 中繼資料，可用來透過額外的篩選條件來搜尋這些資料。

關於這項整合的一些要點：

* 當Adobe庫存中的資產儲存到時 [!DNL Experience Manager]，即成為規則 [!DNL Assets]，並將二進位檔案儲存至 [!DNL Experience Manager] 存放庫。 某些相關中繼資料 [!DNL Adobe Stock] 會為資產儲存在 [!DNL Experience Manager]，否則擷取程式看起來會與任何其他檔案相同。 例如，如果智慧標籤處於作用中狀態，則會在儲存時將標籤新增至這些資產。
* 資產已儲存至 [!DNL Experience Manager] 是復本，而不是要連結回的連結 [!DNL Adobe Stock].

**使用儲存自的資產 [!DNL Adobe Stock] 到 [!DNL Experience Manager] 在[!DNL Creative Cloud]**. 此整合不依賴於 [!DNL Adobe Asset Link]，但 [!DNL Adobe Asset Link] 辨識這些儲存自「 」的資產 [!DNL Stock] ，並顯示其他中繼資料和 [!DNL Adobe Stock] 這些資產上的標誌 [!DNL Adobe Asset Link] 中的擴充功能UI [!DNL Photoshop]， [!DNL Illustrator]，或 [!DNL InDesign]. 檔案可供瀏覽、開啟等操作，因為它們是儲存至時的常規資產 [!DNL Experience Manager].
創作使用者使用 [!DNL Creative Cloud] 應用程式搭配 [!DNL Adobe Asset Link] 除了可從存取已獲得授權的資產外，還顯示擴充功能 [!DNL Adobe Stock] 到 [!DNL Experience Manager]，也可以使用 [!DNL Creative Cloud] 用於搜尋、預覽和授權的程式庫面板 [!DNL Adobe Stock] 資產。
[!DNL Assets] 從 [!DNL Adobe Stock] 已授權並儲存至 [!DNL Experience Manager] 可供更多團隊存取 [!DNL Experience Manager Assets] 部署，而創意人員授權資產來自 [!DNL Adobe Stock] 透過 [!DNL Creative Cloud] 「程式庫」面板僅預設在其中，可供自己使用。 [!DNL Creative Cloud] 帳戶。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

若要在創意和行銷/業務線(LOB)團隊之間設計有效率的工作流程，並選擇最佳支援功能，請務必瞭解資產儲存在DAM的時機和原因。

### 為何資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓您輕鬆存取及找到資產。 它可確保組織或生態系統（包括合作夥伴、客戶等）的眾多使用者都能運用這些資產。

大多陣列織會選擇僅儲存與下遊行銷/LOB程式相關的資產（透過發佈至類似Web頻道的管道） [!DNL Experience Manager Sites] 或Adobe Experience Cloud提供服務的其他管道(Marketing Cloud、Advertising Cloud和Analytics Cloud測量、提供給使用者/合作夥伴等)。 此外，組織會儲存資產，這些資產可能需經過DAM的稽核/核准程式。 如此一來，DAM主要儲存極有可能利用的資產，並避免儲存閒置資產。

儲存資產也受到技術和資源使用率的考量所限制。 DAM提供有關已儲存資產的其他服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考和新增存取控制資訊。 這些服務會消耗額外的時間和基礎建設資源。

通常，儲存所有資產和更新是不合需要的。 例如，如果特定資產的更新品質不佳並消耗過多資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對儲存資產生命週期每個階段的資產不感興趣。 例如，他們會避免在下列情況下儲存資產：

* 尚未完成或有待實驗的資產。
* 未能通過創意/內部團隊稽核週期的資產。
* 相較於相關資產，團隊擁有更好的候選人來代表他們的工作給外部團隊。

通常，以下類別資產會儲存在DAM中：

* 達到特定到期日且被視為可共用的資產。
* 創意團隊預先選取的資產。
* 行銷可用或要求的特定資產格式，視特定合約或協定而定(例如，從RAW檔案轉換的JPG檔案、來自PSD原始檔的TIFF/影像)。

#### 當資產的更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，只有與更廣泛的DAM使用者集相關的資產更新才應儲存在DAM中。 這可確保使用者（行銷和類似功能）只能在DAM資產時間軸中看到相關版本。

通常會與資產生命週期中的主要里程碑相關的變更。 例如，初始行銷就緒資產或根據創意團隊提供的請求/稽核的正式更新應儲存在DAM中並進行版本設定。

在請求變更DAM中的現有資產後，創意團隊的更新以供行銷團隊檢閱，這是相關更新的範例。 它應儲存在DAM中並進行版本設定，以供進一步參考或回覆至先前的版本。

以下是通常無關的更新範例：

* 在資產準備好供行銷稽核之前上傳資產的早期版本
* 創意和行銷團隊決定資產準備好之前，經常在工作階段對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

[!DNL Assets] 根據使用者對「 」的存取權，支援兩種使用者 [!DNL Assets] 部署。 通常企業網路（防火牆）內的使用者可以直接存取DAM。 企業網路以外的其他使用者無法直接存取。 使用者型別會從技術角度決定可使用哪些整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或加入內部網路的代理/創意專業人士有權存取DAM部署，包括 [!DNL Experience Manager] 登入。 [!DNL Experience Manager] 而且網路基礎架構可以設定為允許直接存取外部各方（通常是受信任的組織，例如為客戶工作的機構），以存取 [!DNL Experience Manager] 透過網路，例如透過VPN或IP允許清單。

在這種情況下，請Adobe資產連結或 [!DNL Experience Manager] 案頭應用程式可協助您輕鬆存取最終/核准的資產，並讓您儲存創意就緒的資產至DAM。

#### 沒有DAM存取權的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM部署的外部機構和自由職業者可能會要求存取已核准的資產，或想要將其新設計新增到DAM。

使用下列策略提供最終/核准資產的存取權：

* 如果Asset Link無法運作，請使用案頭應用程式。
* 使用 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於將資產安全地分發給外部合作夥伴
* 根據以下專案使用自訂的發佈和sourcing入口網站實施： [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在中設定的存取控制 [!DNL Experience Manager] 以及必要的網路基礎結構（例如VPN和IP允許清單），以便讓外部各方能夠存取DAM中的專用內容區域。 他們可以使用 [!DNL Experience Manager] Web UI以取得資產並將新內容上傳至您的DAM。

#### 處理中的資產 [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議對資產執行重大更新，有時稱為進行中的工作，而不需將所有編輯內容儲存到本機檔案也不需上傳到 [!DNL Experience Manager] 隨變更。 這可加快案頭使用者的工作速度、限制使用的網路頻寬、保持資產時間表整潔並專注於受控制的重大更新。

Adobe Asset Link對此使用案例提供良好的支援：

* 當使用者在 [!DNL Photoshop]， [!DNL InDesign]，或 [!DNL Illustrator] 他們想要編輯檔案，會對指定的資產執行簽出操作
* 資產會於背景下載，並透過Creative Cloud案頭應用程式放入與磁碟同步的使用者Creative Cloud帳戶，且會切換出庫標幟 [!DNL Experience Manager] 將編輯衝突減到最少
* 從此處，使用者可在檔案中工作，該檔案儲存在同步位置的本機中，並可繼續工作並按需要頻率儲存必要的變更
* 此外，由於資產位於Creative Cloud帳戶中，使用者可能擁有的其他裝置也可使用該資產(例如，可在專用的Creative Cloud行動應用程式中開啟或編輯資產)，並可與其他Creative Cloud使用者共用，以進行共同作業。
* 當創意使用者完成變更時，他們可以在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上可選註釋。 中的對應資產 [!DNL Experience Manager] 會建立版本，並使用新的二進位檔更新為。 [!DNL Experience Manager] 行銷人員或LOB使用者等使用者可以透過存取重大資產變更或里程碑 [!DNL Experience Manager] 資產時間軸UI。

[!DNL Experience Manager] 案頭應用程式為在原生應用程式中開啟的資產提供網路共用。 依預設，所有在本機完成的變更都會上傳至 [!DNL Experience Manager] 在短暫的時間後自動完成。 透過此設定，進行中階段期間經常儲存的內容將會全部上傳到 [!DNL Experience Manager] 和版本化，造成許多網路流量和潛在的可擴充性挑戰 — 更不用說中不必要的版本 [!DNL Experience Manager].

建議在此使用選項 [!DNL Experience Manager] 案頭應用程式關閉自動更新，並將資產變更上傳至 [!DNL Experience Manager] 手動，在應用程式的資產狀態UI中運用上傳變更動作。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能會需要同時將大量檔案上傳到DAM中，例如：

* 上傳拍照或大型專案的結果
* 上傳創意公司提供的資產
* 如果選取是在DAM外部完成，則從較大的集合上傳選取的資產

說明是指以作業方式上傳檔案（例如，每週或每次拍照），作為案頭使用者工作流程的一般部分。 這裡不涵蓋大型資產移轉。

您可以善用下列上傳功能：

* 若要大量上傳大型/階層式資料夾，請使用 [!DNL Experience Manager] 案頭應用程式，提供 [資料夾上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 功能。 您也可以上傳階層資料夾結構。 [!DNL Assets] 會在背景上傳，因此不會繫結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳一些檔案，請直接將檔案拖曳至網頁介面，或使用 [!DNL Assets] 網頁介面。
* 您也可以根據您的業務需求使用自訂上傳程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案共用」來管理數位資產，只需使用對應的網路共用即可 [!DNL Experience Manager] 案頭應用程式可以視為方便的替代品。 從網路檔案共用轉換時， [!DNL Experience Manager] 網頁介面提供豐富的數位資產管理功能，遠遠超越了網路共用的功能（搜尋、收集、中繼資料、共同作業、預覽等），並且 [!DNL Experience Manager] 案頭應用程式提供方便連結，將伺服器端DAM存放庫與案頭上的工作連結。

避免使用 [!DNL Experience Manager] 案頭應用程式，直接管理網路共用中的資產 [!DNL Assets]. 例如，避免使用 [!DNL Experience Manager] 案頭應用程式來移動/複製多個檔案。 請改用 [!DNL Assets] 介面以將資料夾從Finder/Explorer拖曳至網路共用或使用 [!DNL Assets] 資料夾上傳功能。

#### 資產移轉 {#asset-migration}

若要規劃並執行從現有系統到新系統的資產移轉，或移轉儲存在伺服器上的大量資產，請參閱 [移轉指南](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] 案頭應用程式和 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 整合功能不支援這類移轉。 由於要擷取大量資產，以及中繼資料對應、轉換和擷取方面的其他需求，應使用不同的工具和方法處理移轉。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md)

