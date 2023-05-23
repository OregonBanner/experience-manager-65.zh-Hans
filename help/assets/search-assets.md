---
title: 搜尋中的數位資產和影像 [!DNL Adobe Experience Manager]
description: 瞭解如何在中尋找所需資產 [!DNL Adobe Experience Manager] 篩選器面板，以及如何使用搜尋中顯示的資產。
contentOwner: AG
mini-toc-levels: 1
feature: Search, Metadata
role: User
exl-id: 588433b2-564a-430f-9d04-480465ece2ad
hide: true
source-git-commit: eac578f8c8ef3bfc3c94929814398486777094f0
workflow-type: tm+mt
source-wordcount: '5601'
ht-degree: 5%

---

# 搜尋中的數位資產 [!DNL Adobe Experience Manager] {#search-assets-in-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/search-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 提供強大的資產探索方法，協助您實現更高的內容速度。 您的團隊可使用開箱即用的功能和自訂方法，透過順暢的智慧型搜尋體驗縮短上市時間。 搜尋資產是使用數位資產管理系統的核心，無論是供創意人員進一步使用、供業務使用者和行銷人員健全管理資產，還是DAM管理員管理。 您可以透過執行簡單、進階和自訂搜尋 [!DNL Assets] 使用者介面或其他應用程式和介面有助於完成這些使用案例。

[!DNL Experience Manager Assets] 支援下列使用案例，本文介紹這些使用案例的使用方式、概念、設定、限制和疑難排解。

| 搜尋資產 | 設定及管理搜尋功能 | 使用搜尋結果 |
|---|---|---|
| [基本搜尋](#searchbasics) | [搜尋索引](#searchindex) | [排序結果](#sort) |
| [瞭解搜尋UI](#searchui) | [視覺或相似性搜尋](#configvisualsearch) | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必要中繼資料](#mandatorymetadata) | [下载](#download) |
| [瞭解搜尋結果和行為](#searchbehavior) | [修改搜尋多面向](#searchfacets) | [大量中繼資料更新](#metadataupdates) |
| [搜尋排名和升冪](#searchrank) | [文字擷取](#extracttextupload) | [智慧型集合](#collections) |
| [進階搜尋：篩選和搜尋範圍](#scope) | [自訂述詞](#custompredicates) | [瞭解並疑難排解非預期的結果](#unexpected-results) |
| [從其他解決方案和應用程式搜尋](#search-assets-other-surfaces)：<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager案頭應用程式](#desktop-app)</li><li>[Adobe Stock影像](#adobe-stock)</li><li>[Dynamic Media資產](#dynamic-media)</li></ul> |  |  |
| [資產選擇器](#asset-picker) |  |  |
| [限制](#limitations) 和 [提示](#tips) |  |  |
| [插圖範例](#samples) |  |  |

使用Omnisearch欄位(在頂部的 [!DNL Experience Manager] 網頁介面。 前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** 在 [!DNL Experience Manager]，按一下 ![search_icon](assets/do-not-localize/search_icon.png) 在頂端列中，輸入搜尋關鍵字，然後選取 `Return`. 或者，使用關鍵字捷徑 `/` （正斜線）以開啟「全能搜尋」欄位。 `Location:Assets` 已預先選取，以將搜尋限制在DAM資產。 [!DNL Experience Manager] 會在您開始輸入搜尋關鍵字時提供建議。

使用 **[!UICONTROL 篩選器]** 面板以搜尋資產、資料夾、標籤和中繼資料。 您可以根據各種選項（述詞）來篩選搜尋結果，例如檔案型別、檔案大小、上次修改日期、資產狀態、見解資料和Adobe Stock授權。 您可以自訂「篩選器」面板，並使用新增或移除搜尋述詞 [搜尋Facet](/help/assets/search-facets.md). 此 [!UICONTROL 檔案型別] 在中篩選 [!UICONTROL 篩選器] 面板中有混合狀態核取方塊。 因此，除非您選取所有巢狀述詞（或格式），否則會部分勾選第一層核取方塊。

[!DNL Experience Manager] 搜尋功能支援搜尋集合和搜尋集合內的資產。 另請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 瞭解搜尋介面 {#searchui}

熟悉搜尋介面和可用的動作。

![瞭解Experience Manager Assets搜尋結果介面](assets/aem_search_results.png)

*圖：瞭解 [!DNL Experience Manager Assets] 搜尋結果介面。*

**答：** 將搜尋儲存為智慧型集合。 **B.** 篩選或述詞以縮小搜尋結果的範圍。 **C.** 顯示檔案、資料夾或兩者。 **D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F.** 具有使用者提供搜尋關鍵字的Omnisearch欄位。 **G.** 選取載入的搜尋結果。 **高** 搜尋結果總數中顯示的搜尋結果數目。 **I.** 關閉搜尋。 **J.** 在卡片檢視和清單檢視之間切換。

### 動態搜尋多面向 {#dynamicfacets}

您可以使用搜尋Facet中預期搜尋結果數量的動態更新，更快速地從搜尋結果頁面探索所需資產。 資產預期數量會在套用搜尋篩選之前更新。 檢視篩選的預期計數，有助於您快速有效地瀏覽搜尋結果。

![檢視搜尋Facet中未篩選搜尋結果的大約資產數量。](assets/asset_search_results_in_facets_filters.png)

*圖：檢視搜尋Facet中未篩選搜尋結果的大約資產數量。*

## 瞭解搜尋結果和行為 {#searchbehavior}

### 基本搜尋字詞和結果 {#searchbasics}

您可以從「全域搜尋」欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，且是全文搜尋（涵蓋熱門中繼資料欄位）。 如果使用多個關鍵字， `AND` 是關鍵字之間的預設運運算元。

結果會依相關性排序，從最接近的相符專案開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含這兩個字詞的資產。 在中繼資料中，顯示為智慧標籤的關鍵字的排名高於出現在其他中繼資料欄位中的關鍵字。 [!DNL Experience Manager] 允許給予特定搜尋詞較高的權重。 此外，您也可以 [提升排名](#searchrank) 特定搜尋字詞的幾個目標資產中。

為了快速找到相關資產，豐富的介面提供了篩選、排序和選擇機制。 您可以根據多個條件篩選結果，並檢視各種篩選的已搜尋資產數量。 或者，您可以透過變更Omnisearch欄位中的查詢來重新執行搜尋。 當您變更搜尋字詞或篩選器時，其他篩選器仍會套用，以保留您的搜尋內容。

當結果為許多資產時， [!DNL Experience Manager] 在卡片檢視中顯示前100個，在清單檢視中顯示200個。 當使用者捲動時，會載入更多資產。 這是為了改善效能。 觀看的影片示範 [顯示的資產數量](https://www.youtube.com/watch?v=LcrGPDLDf4o).

有時，您可能會在搜尋結果中看到一些未預期的資產。 如需詳細資訊，請參閱 [未預期的結果](#unexpected-results).

[!DNL Experience Manager] 可搜尋多種檔案格式，也可自訂搜尋篩選器以符合您的業務需求。 請聯絡您的管理員，瞭解您的DAM存放庫有哪些搜尋選項可用，以及您的帳戶有哪些限制。

### 包含和不包含增強型智慧標籤的結果 {#withsmarttags}

依預設， [!DNL Experience Manager] 搜尋會將搜尋字詞與AND子句結合。 例如，考慮搜尋關鍵字woman正在執行。 依預設，搜尋結果中只會顯示中繼資料中同時包含女性和執行中關鍵字的資產。 關鍵字使用特殊字元（句號、底線或破折號）時，會保留相同的行為。 下列搜尋查詢會傳回相同的結果：

* `woman running`
* `woman.running`
* `woman-running`

但是，查詢 `woman -running` 傳回資產，但不包含 `running` 在其中繼資料中。
使用智慧標籤會額外新增 `OR` 子句可尋找任何搜尋詞作為套用的智慧標籤。 以任一專案標籤的資產 `woman` 或 `running` 使用智慧標籤也會出現在這類搜尋查詢中。 因此搜尋結果是

* 資產，具有 `woman` 和 `running` 中繼資料中的關鍵字（預設行為）。

* 使用任一關鍵字進行智慧標籤的資產（智慧標籤行為）。

### 在您輸入時搜尋建議 {#searchsuggestions}

當您開始輸入關鍵字時， [!DNL Experience Manager] 建議可能的搜尋關鍵字或片語。 這些建議是根據現有資產的中繼資料。 [!DNL Experience Manager] 會對所有中繼資料欄位編制索引，以協助進行搜尋。 為了提供搜尋建議，系統使用下列幾個中繼資料欄位的值。 若要提供搜尋建議，請考慮將適當的關鍵字填入下列欄位：

* 資產標籤。 (將對應至 `jcr:content/metadata/cq:tags`)
* 資產標題。 (將對應至 `jcr:content/metadata/dc:title`)
* 資產說明。 (將對應至 `jcr:content/metadata/dc:description`)
* JCR存放庫中的標題。 值可能會對應至資產標題。 (將對應至 `jcr:content/jcr:title`)
* JCR存放庫中的說明。 此值可能會對應到資產說明。 (將對應至 `jcr:content/jcr:description`)

若要接收多個搜尋關鍵字的建議，請繼續輸入所有關鍵字，而不選取單一關鍵字的任何建議。

![輸入多個關鍵字以檢視符合所有關鍵字的建議](assets/search_suggestionsmanykeywords.gif)

*圖：輸入多個關鍵字以檢視符合所有關鍵字的建議。*

### 搜尋排名和提升 {#searchrank}

符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 在上述範例中，顯示搜尋結果的大約順序為：

1. 符合 `woman running` 於各種中繼資料欄位中。
1. 符合 `woman running` 在智慧標籤中。
1. 符合 `woman` 或 `running` 在智慧標籤中。

您可以改善特定資產的關鍵字關聯性，以協助根據關鍵字提升搜尋次數。 換言之，當您根據這些關鍵字進行搜尋時，您為其促銷特定關鍵字的影像會顯示在搜尋結果的最上方。

1. 從 [!DNL Assets] 使用者介面，開啟資產的屬性頁面。 按一下 **[!UICONTROL 進階]** 並按一下 **[!UICONTROL 新增]** 在 **[!UICONTROL 提升搜尋關鍵字]**.
1. 在 **[!UICONTROL 搜尋提升]** 方塊中，指定您要增加影像搜尋的關鍵字，然後按一下 **[!UICONTROL 新增]**. 您可以用相同方式指定多個關鍵字。
1. 单击“**[!UICONTROL 保存并关闭]**”。您針對此關鍵字促銷的資產會出現在熱門搜尋結果中。

您可以藉由提升目標關鍵字搜尋結果中某些資產的排名，來使用此功能。 請觀看下方的範例影片。 如需詳細資訊，請參閱 [搜尋 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*影片：瞭解搜尋結果的排名方式，以及排名會受到哪些影響。*

## 進階搜尋 {#scope}

[!DNL Experience Manager] 提供多種方法（例如套用至搜尋資產的篩選器），以協助您更快找到所需資產。 以下說明一些常用方法。 部分 [圖解範例](#samples) 以下共用。

**搜尋檔案或資料夾**：在搜尋結果中，檢視檔案、資料夾或兩者。 從 **[!UICONTROL 篩選器]** 面板上，您可以選取適當的選項。 另請參閱 [搜尋介面](#searchui).

**搜尋資料夾中的資產**：您可以將搜尋限制在特定資料夾中。 在 **[!UICONTROL 篩選器]** 面板，新增資料夾的路徑。 您一次只能選取一個資料夾。

![在「篩選器」面板中新增資料夾路徑，將搜尋結果限製為資料夾](assets/search_folder_select.gif)

*圖：在「篩選器」面板中新增資料夾路徑，將搜尋結果限製為資料夾。*

### 尋找類似影像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡片檢視中的選項尋找類似影像](assets/search_find_similar.png)

*圖：使用卡片檢視中的選項尋找類似影像。*

### Adobe Stock影像 {#adobe-stock}

從 [!DNL Experience Manager] 使用者介面，使用者可搜尋 [Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) 並授權必要的資產。 新增 `Location: Adobe Stock` 在Omnisearch列中。 您也可以使用「篩選器」面板來尋找所有授權或未經授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。

### Dynamic Media資產 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用中繼資料欄位中的特定值的GQL搜尋 {#gql-search}

您可以根據中繼資料欄位的確切值搜尋數位資產，例如，標題、說明和建立者。 GQL全文檢索搜尋功能只會擷取中繼資料值與搜尋查詢完全相符的資產。 屬性的名稱（建立者、標題等）和值區分大小寫。

| 中繼資料欄位 | Facet值和使用狀況 |
|---|---|
| 标题 | title：John |
| 创建者 | 建立者：John |
| 位置 | location：NA |
| 描述 | description：&quot;Sample Image&quot; |
| 建立者工具 | creatortool：&quot;Adobe Photoshop&quot; |
| 版权所有者 | 版權擁有者：「Adobe Systems」 |
| 参与者 | 投稿人：John |
| 使用条款 | usageterms：&quot;CopyRights Reserved&quot; |
| 创建时间 | created：YYYY-MM-DDTHH |
| 到期日期 | expires：YYYY-MM-DDTHH |
| 準時 | ontime：YYYY-MM-DDTHH |
| 關閉時間 | offtime：YYYY-MM-DDTHH |
| 時間範圍(expires dateontime，offtime) | Facet欄位：下限……上界 |
| 路径 | /content/dam/&lt;folder name=&quot;&quot;> |
| PDF 标题 | pdftitle：&quot;Adobe檔案&quot; |
| 主题 | 主旨：「培訓」 |
| 标记 | 標籤：「地點與旅行」 |
| 类型 | 型別：&quot;image\png&quot; |
| 影像寬度 | width：lowerbound..上界 |
| 影像高度 | height：lowerbound..上界 |
| 人员 | person：John |

屬性 `path`， `limit`， `size`、和 `orderby` 無法使用合併 `OR` 運運算元與任何其他屬性。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

使用者產生的屬性的關鍵字是屬性編輯器中的欄位標籤（小寫），並移除空格。

以下是一些複雜查詢的搜尋格式範例：

* 若要顯示具有多個Facet欄位的所有資產(例如： title=John Doe和建立者工具= Adobe Photoshop)： `title:"John Doe" creatortool:Adobe*`
* 當Facet值不是單一字詞而是句子時（例如：title=Scott Reynolds）顯示所有資產： `title:"Scott Reynolds"`
* 若要顯示具有單一屬性的多個值的資產（例如：title=Scott Reynolds或John Doe）： `title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產（例如：title是Scott Reynolds）： `title:Scott*`
* 若要顯示屬性值以特定字串結尾的資產（例如：title是Scott Reynolds）： `title:*Reynolds`
* 若要以包含特定字串的屬性值來顯示資產（例如：title = Basel Meeting Room）： `title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如：在title=John Doe的資產中搜尋字串Adobe)： `*Adobe* title:"John Doe"`

## 從其他來源搜尋數位資產 [!DNL Experience Manager] 方案或介面 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] 將DAM存放庫連線到各種其他 [!DNL Experience Manager] 解決方案，提供更快速存取數位資產並簡化創意工作流程。 任何資產探索都會從瀏覽或搜尋開始。 在各種表面和解決方案中，搜尋行為大致維持不變。 有些搜尋方法會隨著目標對象、使用案例和使用者介面的不同而有所變更。 [!DNL Experience Manager] 解決方案。 以下連結提供各個解決方案的特定方法。 本文記錄通用提示和行為。

### 從Adobe Asset Link面板搜尋數位資產 {#aal}

創意專業人士現在可以使用Adobe Asset Link存取中儲存的內容 [!DNL Experience Manager Assets]，無需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用 [!DNL Adobe Creative Cloud] 應用程式： [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign]. Asset Link也可讓使用者搜尋視覺上類似的結果。 視覺化搜尋顯示結果由Adobe Sensei的機器學習演演算法提供支援，並幫助使用者尋找在美學上相似的影像。 另請參閱 [搜尋和瀏覽資產](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 使用Adobe資產連結。

### 搜尋中的數位資產 [!DNL Experience Manager] 案頭應用程式 {#desktop-app}

創意專業人士使用案頭應用程式製作 [!DNL Experience Manager Assets] 可輕鬆搜尋並在其本機案頭(Win或Mac)上使用。 創意人員可以輕鬆地在Mac Finder或Windows檔案總管中顯示所需的資產、在案頭應用程式中開啟並在本機變更 — 變更會儲存回 [!DNL Experience Manager] 在存放庫中建立新版本。 應用程式支援使用一或多個關鍵字進行基本搜尋。 `*` 和 `?` 萬用字元，和 `AND` 運運算元。 另請參閱 [瀏覽、搜尋和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 在案頭應用程式中。

### 搜尋中的數位資產 [!DNL Brand Portal] {#brand-portal}

業務線使用者和行銷人員可使用Brand Portal，有效率且安全地與其擴充的內部團隊、合作夥伴和經銷商共用核准的數位資產。 另請參閱 [在Brand Portal上搜尋資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜尋 [!DNL Adobe Stock] 影像 {#adobe-stock1}

從 [!DNL Experience Manager] 使用者介面，使用者可以搜尋Adobe Stock資產並授權必要的資產。 新增 `Location: Adobe Stock` 在Omnisearch欄位中。 您也可以使用 **[!UICONTROL 篩選器]** 面板以尋找所有授權或未經授權的資產，或使用Adobe Stock檔案編號搜尋特定資產。 另請參閱 [管理 [!DNL Adobe Stock] 中的影像 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### 搜尋 [!DNL Dynamic Media] 資產 {#dynamic-media}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 製作網頁時在Content Finder中搜尋數位資產 {#content-finder}

作者可以使用內容尋找器來搜尋DAM存放庫中的相關資產，並在他們建立的網頁中使用資產。 作者也可以使用連線資產功能來搜尋遠端可用的資產 [!DNL Experience Manager] 部署。 然後，作者便可以在本機的網頁中使用這些資產 [!DNL Experience Manager] 部署。 另請參閱 [使用遠端資產](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜尋集合 {#collections}

[!DNL Experience Manager] 搜尋功能支援搜尋集合和搜尋集合內的資產。 另請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 資產選擇器 {#asset-picker}

>[!NOTE]
>
>已呼叫資產選擇器 [資產選取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在舊版中 [!DNL Adobe Experience Manager].

資產選擇器可讓您以特殊方式搜尋、篩選和瀏覽DAM資產。 資產選擇器位於 `https://[aem_server]:[port]/aem/assetpicker.html`. 您可以使用資產選擇器擷取所選資產的中繼資料。 您可以使用支援的請求引數來啟動它，例如資產型別（影像、視訊、文字）和選取模式（單一或多個選取範圍）。 這些引數會為特定搜尋執行個體設定資產選擇器的內容，並在整個選取範圍中維持不變。

資產選擇器使用HTML5 `Window.postMessage` 傳送所選資產的資料給收件者的訊息。 它僅適用於瀏覽模式和Omnisearch結果頁面。

在URL中傳遞以下請求引數，以啟動特定內容中的資產選擇器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 資源字尾(B) | 在URL中作為資源尾碼的資料夾路徑： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 在選取特定資料夾的情況下（例如使用資料夾）啟動資產選擇器 `/content/dam/we-retail/en/activities` 選取時，URL的格式應為： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果您在啟動資產選擇器時要求選擇特定資料夾，請將其傳遞為資源尾碼。 |
| `mode` | 單一，多個 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多重模式中，您可以使用資產選擇器同時選取多個資產。 |
| `dialog` | true， false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些引數開啟資產選擇器作為Granite對話方塊。 只有當您透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時，此選項才適用。 |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在此情況下，資產選擇器可讓您僅選取根資料夾下的子資產（直接/間接）。 |
| `viewmode` | 搜索 |  | 若要在搜尋模式中啟動資產選擇器，請使用 `assettype` 和 `mimetype` 引數。 |
| `assettype` | 影像、檔案、多媒體、封存。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用選項可依據提供的值篩選資產型別。 |
| `mimetype` | MIME型別(`/jcr:content/metadata/dc:format`)（也支援萬用字元）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根據MIME型別篩選資產。 |

若要存取資產選擇器介面，請前往 `https://[aem_server]:[port]/aem/assetpicker`. 導覽至所需的資料夾，然後選取一或多個資產。 或者，從Omnisearch方塊搜尋所需的資產，視需要套用篩選器，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/assetpicker.png)

*圖：瀏覽並選取資產選擇器中的資產。*

## 限制 {#limitations}

中的搜尋功能 [!DNL Experience Manager Assets] 有以下限制：

* 請勿在搜尋查詢中輸入前導空格，否則搜尋無法運作。
* [!DNL Experience Manager] 在您從搜尋結果中選取資產的屬性，然後取消搜尋之後，可以繼續顯示搜尋字詞。 <!-- (CQ-4273540) -->
* 搜尋資料夾或檔案和資料夾時，搜尋結果無法依任何引數排序。
* 如果您選取 `Return` 無需輸入Omnisearch列， [!DNL Experience Manager] 只傳回檔案清單，不傳回資料夾清單。 如果您在不使用關鍵字的情況下專門搜尋資料夾， [!DNL Experience Manager] 未傳回任何結果。
* 您可以對資料夾執行全文檢索搜尋。 指定要讓搜尋運作的搜尋字詞。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋最適合用於大型存放庫。 雖然沒有達到良好結果所需的最低影像數量，但少數影像的相符品質不如大型存放庫的相符專案。
* 您無法變更模型或訓練 [!DNL Experience Manager] 以尋找類似的影像。 例如，在少數資產中新增或移除智慧標籤不會變更模型。 這些資產確實會從視覺上相似的搜尋結果中排除。

搜尋功能在下列情況下可能有效能限制：

* 與清單檢視相比，卡片檢視的載入時間更快，可顯示搜尋結果。

## 搜尋提示 {#tips}

* 監控資產的稽核狀態時，請使用適當的選項來尋找已核准的資產或待核准的資產。
* 使用見解述詞，根據從各種創意應用程式獲得的使用情況統計資料，搜尋支援的資產。 使用情況資料會依使用情況分數、曝光數、點按數和資產顯示所在的媒體管道分類分組。
* 使用 **[!UICONTROL 全選]** 核取方塊以選取搜尋的資產。 [!DNL Experience Manager] 最初在卡片檢視中顯示100個資產，在清單檢視中顯示200個資產。 捲動搜尋結果時會載入更多資產。 您可以選取比已載入資產更多的資產。 所選資產的計數會顯示在搜尋結果頁面的右上角。 您可以對選項執行操作，例如，下載所選資產、大量更新所選資產的中繼資料屬性，或將所選資產新增到收藏集。 當選取的資產多於顯示時，動作會套用於所有選取的資產，或對話方塊會顯示套用於的資產數量。 若要將動作套用至未載入的資產，請確定已明確選取所有資產。
* 若要搜尋不包含必要中繼資料的資產，請參閱 [必要中繼資料](#mandatorymetadata).
* 搜尋會使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為了獲得更好的結果，請使用雙引號（而非單引號）或確保數字與沒有特殊字元的字詞相鄰(例如 `shoe12`)。
* 全文檢索搜尋支援下列運運算元 `-` 和 `^`. 若要將這些字母搜尋為字串常值，請以雙引號括住搜尋運算式。 例如，使用 `"Notebook - Beauty"` 而非 `Notebook - Beauty`.
* 如果搜尋結果太多，請限制 [搜尋範圍](#scope) 以零進位所需資產。 當您瞭解如何更妥善尋找所需資產（例如，特定檔案型別、特定位置、特定中繼資料等）時，此工具將最有效果。

* **標籤**：標籤可協助您更有效率地將可瀏覽和搜尋的資產分類。 標籤有助於將適當的分類法傳播給其他使用者和工作流程。 [!DNL Experience Manager] 提供使用Adobe Sensei的人為智慧型服務自動標籤資產的方法，以便透過使用和培訓來更有效地標籤您的資產。 搜尋資產時，如果您的帳戶已啟用此功能，則會將智慧標籤列入考量。 它可與內建搜尋功能搭配使用。 另請參閱 [搜尋行為](#searchbehavior). 若要最佳化搜尋結果的顯示順序，您可以 [提升搜尋排名](#searchrank) 中的幾個選取資產。

* **索引**：搜尋結果中只會傳回已索引的中繼資料和資產。 為獲得更好的涵蓋範圍和效能，請確保建立適當的索引並遵循最佳實務。 另請參閱 [索引](#searchindex).

* 若要從搜尋結果中排除特定資產，請使用 `excludedPath` Lucene索引的屬性。

## 說明搜尋的一些範例 {#samples}

在關鍵字周圍使用雙引號來尋找包含精確片語的資產，其順序與使用者指定的完全一致。

![有引號和無引號的搜尋行為](assets/search_with_quotes.gif)

*圖：使用和不使用引號的搜尋行為。*

**使用星號萬用字元搜尋**：若要擴大搜尋範圍，請在搜尋字詞前後加上星號，以比對任意數量的字元。 例如，搜尋沒有星號的執行不會傳回包含任何字詞變數的資產（包括中繼資料中的）。 星號可取代任意數目的字元。 例如，

* `run` 以exactly run關鍵字傳回資產
* `run*` 傳回資產的方式 `running`， `run`， `runaway`、等等。
* `*run` 傳回資產的方式 `outrun`， `rerun`、等等。
* `*run*` 傳回所有可能的組合。

![舉例說明在資產搜尋中使用星號萬用字元](assets/search_with_asterisk_run.gif)

*圖：以範例說明在資產搜尋中使用星號萬用字元的情形。*

**使用問號萬用字元搜尋**：若要擴大搜尋範圍，請使用一或多個「？」 個字元，以符合確切的字元數。 例如，在下圖中，

* `run???` 查詢不符合任何資產。

* `run????` 查詢符合單字 `running` 後面有四個字元 `run`.

* `??run` 查詢符合單字 `rerun` 之前有兩個字元 `run`.

![舉例說明在資產搜尋中使用問號萬用字元](assets/search_with_questionmark_run.gif)

*圖：說明在資產搜尋中使用問號萬用字元的範例。*

**排除關鍵字**：使用破折號來搜尋不包含關鍵字的資產。 例如， `running -shoe` 查詢傳回的資產包含 `running`，但不是 `shoe`. 同樣地， `camp -night` 查詢傳回的資產包含 `camp` 但不是 `night`. 查詢 `camp-night` 傳回同時包含兩者的資產 `camp` 和 `night`.

![使用破折號來搜尋不包含排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)

*圖：使用破折號來搜尋不包含排除關鍵字的資產。*

## 與搜尋功能相關的設定和管理工作 {#configadmin}

### 搜尋索引設定 {#searchindex}

資產探索有賴於DAM內容的索引，包括中繼資料。 更快、更精確的資產探索有賴於最佳化的索引和適當的設定。 另請參閱 [搜尋索引](/help/assets/performance-tuning-guidelines.md#search-indexes)， [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)、和 [最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

若要從搜尋結果中排除特定資產，請使用 `excludedPath` Lucene索引的屬性。

### 視覺或相似性搜尋 {#configvisualsearch}

視覺化搜尋使用智慧標籤。 設定智慧標籤功能後，請依照下列步驟操作。

1. 在 [!DNL Experience Manager] CRXDE，在 `/oak:index/lucene` 節點，新增以下屬性和值並儲存變更。

   * `costPerEntry` 型別的屬性 `Double` 包含值 `10`.
   * `costPerExecution` 型別的屬性 `Double` 包含值 `2`.
   * `refresh` 型別的屬性 `Boolean` 包含值 `true`.

   此設定允許從適當的索引進行搜尋。

1. 若要建立Lucene索引，請在CRXDE中的 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`，建立名為的節點 `imageFeatures` 型別 `nt-unstructured`. 在 `imageFeatures` 節點，

   * 新增 `name` 型別的屬性 `String` 包含值 `jcr:content/metadata/imageFeatures/haystack0`.
   * 新增 `nodeScopeIndex` 型別的屬性 `Boolean` ，其值為 `true`.
   * 新增 `propertyIndex` 型別的屬性 `Boolean` ，其值為 `true`.
   * 新增 `useInSimilarity` 型別的屬性 `Boolean` 包含值 `true`.

   保存更改。

1. 存取 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 並新增 `similarityTags` 型別的屬性 `Boolean` ，其值為 `true`.
1. 將智慧標籤套用至中的資產 [!DNL Experience Manager] 存放庫。 另請參閱 [如何設定智慧標籤](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. 在CRXDE中，在 `/oak-index/damAssetLucene` 節點，設定 `reindex` 屬性至 `true`. 保存更改。
1. （選擇性）如果您有自訂的搜尋表單，請複製 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 節點至 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. 保存更改。

如需相關資訊，請參閱 [瞭解Experience Manager中的智慧標籤](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) 和 [如何管理智慧標籤](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>如果Lucene索引完成於 [!DNL Adobe Experience Manager]，則根據智慧標籤進行的搜尋無法如預期運作。

### 必要中繼資料 {#mandatorymetadata}

業務使用者、管理員或DAM程式庫管理員可以將一些中繼資料定義為必要中繼資料，這是業務流程運作的必要條件。 由於各種原因，某些資產可能遺漏此中繼資料，例如舊版資產或大量移轉的資產。 系統會根據已索引的中繼資料屬性，偵測及報告含有遺失或無效中繼資料的資產。 若要進行設定，請參閱 [必要中繼資料](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### 修改搜尋多面向 {#searchfacets}

若要提高探索速度， [!DNL Experience Manager Assets] 提供可讓您篩選搜尋結果的搜尋Facet。 依預設，「篩選器」面板包含幾個標準面向。 管理員可以自訂「篩選器」面板，以使用內建述詞修改預設面向。 [!DNL Experience Manager] 提供良好的內建述詞集合，以及自訂Facet的編輯器。 另請參閱 [搜尋Facet](/help/assets/search-facets.md).

### 上傳資產時擷取文字 {#extracttextupload}

您可以設定 [!DNL Experience Manager] 以在使用者上傳資產(例如PSD或PDF檔案)時，從資產中擷取文字。 [!DNL Experience Manager] 會為擷取的文字建立索引，並協助使用者根據擷取的文字搜尋這些資產。 另請參閱 [上傳資產](/help/assets/manage-assets.md#uploading-assets).

如果文字擷取對於您的部署而言變得過於耗費資源，請考慮 [停用文字擷取](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### 用於篩選搜尋結果的自訂述詞 {#custompredicates}

述詞用於建立Facet。 管理員可以使用預先設定的述詞來自訂「篩選器」面板中的搜尋Facet。 可使用覆蓋圖自訂這些述詞。 另請參閱 [建立自訂述詞](/help/assets/searchx.md).

您可以根據下列一或多個屬性來搜尋數位資產。 依預設，套用至其中一些屬性的篩選器可供使用，而其他某些篩選器則可自訂建立，以套用至其他屬性。

| 搜索字段 | 搜尋屬性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 类型 | 影像、檔案、多媒體、封存或其他。 |
| 上次修改时间 | 小時、日、周、月或年。 |
| 檔案大小 | 小、中、大。 |
| 發佈狀態 | 已發佈或已取消發佈。 |
| 已核准狀態 | 已核准或已拒絕。 |
| 方向 | 水準、垂直或正方形。 |
| 样式 | 彩色或黑白。 |
| 视屏高度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 视频宽度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值會儲存在來源視訊的中繼資料和任何轉譯中。 |
| 視訊轉碼器 | x264。 值只會儲存在視訊轉譯的中繼資料中。 |
| 视频比特率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC編碼。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音频比特率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |

## 使用資產搜尋結果 {#aftersearch}

您可以使用搜尋過的資產執行下列動作 [!DNL Experience Manager]：

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用「案頭動作」在案頭應用程式中開啟這些資產。
* 建立智慧型集合。

### 排序搜尋結果 {#sort}

排序搜尋結果以更快找到所需資產。 您可以在清單檢視中排序搜尋結果，而且只有在選取 **[[!UICONTROL 檔案]](#searchui)** 從 **[!UICONTROL 篩選器]** 面板。 [!DNL Assets] 使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產（無論數量多少）。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在清單檢視中，您可以排序搜尋結果，就像排序任何資料夾中的資產一樣。 排序功能適用於這些欄 — 名稱、標題、狀態、Dimension、大小、評等、使用狀況、（日期）建立時間、（日期）修改時間、（日期）發佈時間、工作流程和出庫。

如需排序功能的限制，請參閱 [限制](#limitations).

### 檢查資產的詳細資訊 {#checkinfo}

您可以從搜尋結果頁面檢查搜尋資產的詳細資訊。

若要檢視資產的所有中繼資料，請選取資產並按一下 **[!UICONTROL 屬性]** （從工具列）。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![排序搜尋資產的時間軸專案](assets/sort_timeline_search_results.gif)

*圖：排序搜尋資產的時間軸專案。*

### 下載搜尋的資產 {#download}

您可以下載搜尋的資產及其轉譯，就像從資料夾下載一般資產一樣。 從搜尋結果中選取一或多個資產，然後按一下 **[!UICONTROL 下載]** （從工具列）。

### 大量更新中繼資料屬性 {#metadataupdates}

您可以對多個資產的常見中繼資料欄位進行大量更新。 從搜尋結果中選取一或多個資產。 按一下 **[!UICONTROL 屬性]** 並視需要更新中繼資料。 按一下 **[!UICONTROL 儲存並關閉]** 完成時。 更新欄位中先前存在的中繼資料會被覆寫。

對於可在單一資料夾或集合中取得的資產，更容易 [大量更新中繼資料](/help/assets/metadata.md) 而不使用搜尋功能。 對於跨資料夾可用的資產或符合共同條件的資產，透過搜尋大量更新中繼資料會更快一些。

### 智慧型集合 {#smart-collections}

收藏集是一組經過排序的資產，可以包含來自不同位置的資產，因為收藏集僅包含對這些資產的引用。 集合有兩種型別：

* 資產、資料夾和其他集合的靜態參考清單。
* 根據搜尋條件填入集合中資產的動態清單（智慧型集合）。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/manage-collections.md)。

## 未預期的搜尋結果和問題 {#unexpected-results}

| 錯誤、問題、症狀 | 可能的原因 | 對問題的可能修正或瞭解 |
|---|---|---|
| 搜尋缺少中繼資料的資產時結果不正確。 | 搜尋缺少必要中繼資料的資產時， [!DNL Experience Manager] 可能會顯示一些具有有效中繼資料的資產。 結果是根據已編制索引的中繼資料屬性。 | 更新中繼資料後，需要重新索引以反映資產中繼資料的正確狀態。 另請參閱 [必要中繼資料](metadata-schemas.md#define-mandatory-metadata). |
| 搜尋結果太多。 | 廣泛搜尋引數。 | 請考慮限制 [搜尋範圍](#scope). 使用智慧標籤可能會提供比您預期更多的搜尋結果。 另請參閱 [使用智慧標籤搜尋行為](#withsmarttags). |
| 不相關或部分相關的搜尋結果。 | 使用智慧標籤來變更搜尋行為。 | 瞭解 [智慧型標籤後搜尋的變更](#withsmarttags). |
| 沒有資產的自動完成建議。 | 新上傳的資產尚未編列索引。 當您開始在Omnisearch列中輸入搜尋關鍵字時，中繼資料無法立即作為建議使用。 | [!DNL Experience Manager] 會等到逾時期間（預設為一小時）過後，才執行背景工作，為所有新上傳或更新資產的中繼資料建立索引，然後將中繼資料新增到建議清單中。 |
| 无搜索结果. | <ul><li>符合您查詢的資產不存在。 </li><li> 在搜尋查詢前新增空格。 </li><li> 不支援的中繼資料欄位包含您搜尋的關鍵字。</li><li> 在資產關閉期間進行搜尋。 </li></ul> | <ul><li>使用不同的關鍵字進行搜尋。 或者，使用智慧標籤或相似性搜尋來改善搜尋結果。 </li><li>[已知限制](#limitations).</li><li>搜尋時不考慮所有中繼資料欄位。 另請參閱 [範圍](#scope).</li><li>稍後搜尋或修改所需資產的開啟時間和關閉時間。</li></ul> |
| 搜尋篩選或述詞無法使用。 | <ul><li>搜尋篩選器尚未設定。</li><li>無法供您的登入使用。</li><li>（可能性較低）搜尋選項不會根據您使用的部署自訂。</li></ul> | <ul><li>請聯絡管理員以檢查搜尋自訂功能是否可用。</li><li>請聯絡管理員，檢查您的帳戶是否有使用自訂的許可權。</li><li>請聯絡管理員，並檢查以下專案的可用自訂專案： [!DNL Assets] 您正在使用的部署。</li></ul> |
| 搜尋視覺上相似的影像時，缺少預期的影像。 | <ul><li>影像無法用於 [!DNL Experience Manager].</li><li>影像未編列索引。 通常是在最近上傳時。</li><li>影像未使用智慧標籤。</li></ul> | <ul><li>將影像新增至 [!DNL Assets].</li><li>請聯絡您的管理員以重新索引存放庫。 此外，請確定您使用適當的索引。</li><li>請聯絡您的管理員，以智慧標籤相關資產。</li></ul> |
| 搜尋視覺上相似的影像時，會顯示不相關的影像。 | 視覺搜尋行為。 | [!DNL Experience Manager] 顯示儘可能多的潛在相關資產。 將相關性較低的影像（如果有的話）新增到結果中，但搜尋排名較低。 向下捲動搜尋結果時，相符專案的品質和搜尋資產的相關性會降低。 |
| 選取並操作搜尋結果時，不會操作所有搜尋的資產。 | 此 [!UICONTROL 全選] 選項只會選取卡片檢視中的前100個搜尋結果，以及清單檢視中的前200個搜尋結果。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜尋實作指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [提升搜尋結果的進階設定](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [設定智慧型翻譯搜尋](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

