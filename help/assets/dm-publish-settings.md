---
title: 設定影像伺服器的Dynamic Media發佈設定
description: 瞭解如何在Dynamic Media中設定發佈。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 25fe5e240fd7404cb07375325e1f7b6a32923bfd
workflow-type: tm+mt
source-wordcount: '3494'
ht-degree: 3%

---

# 設定影像伺服器的Dynamic Media發佈設定

只有符合以下條件時，才可設定Dynamic Media發佈設定：

* 您正在以Scene7模式執行Dynamic Media。 另請參閱 [在Scene7模式下啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 您有 *現有* **[!UICONTROL Dynamic Media設定]** (in **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5.11或更新版本中。 另請參閱 [在Cloud Services中建立Dynamic Media設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* 您是具有管理員許可權的Experience Manager系統管理員。

Dynamic Media發佈設定適用於有經驗的網站開發人員和程式設計人員。 Adobe Dynamic Media建議變更這些發佈設定的使用者熟悉AdobeDynamic Media、HTTP通訊協定標準和慣例，以及基本影像處理技術。

「Dynamic Media發佈設定」頁面會建立預設設定，以判斷如何將資產從Adobe Dynamic Media伺服器傳送至網站或應用程式。 如果未指定任何設定，AdobeDynamic Media伺服器會根據Dynamic Media Publish Setup頁面上設定的預設設定傳送資產。

另請參閱 [可選 — Dynamic Media的設定和配置 — Scene7模式設定](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 以取得更多選擇性設定工作。

>[!NOTE]
>
>在Adobe Experience Manager上從Dynamic Media Classic升級至Dynamic Media？ 此 [一般設定](/help/assets/dm-general-settings.md) Dynamic Media中的頁面和發佈設定頁面已預先填入從您的Dynamic Media Classic帳戶中取得的值。 例外情況是 **[!UICONTROL 預設上傳選項]** 「一般設定」頁面的區域。 這些值已Experience Manager。 因此，您在下列專案底下所做的任何變更 **[!UICONTROL 預設上傳選項]**&#x200B;橫跨五個標籤的任何一個，透過Experience Manager使用者介面，反映在Dynamic Media中，而不是Dynamic Media Classic中。 所有其他設定和值 [一般設定](/help/assets/dm-general-settings.md) 頁面和「發佈設定」頁面會在Dynamic Media Classic和Dynamic Media之間Experience Manager時維護。

**若要設定Dynamic Media Publish設定影像伺服器：**

1. 在Experience Manager作者模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在左側欄中，選取「工具」圖示，然後前往 **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**.
1. 在「影像伺服器」頁面中，設定「影像伺服器 — 發佈」內容，然後使用五個索引標籤來設定預設發佈設定。

   * [图像服务器](#image-server)
   * [安全性](#security-tab) 標籤
   * [目錄管理](#catalog-management-tab) 標籤
   * [請求屬性](#request-attributes-tab) 標籤
   * [通用縮圖屬性](#common-thumbnail-attributes-tab) 標籤
   * [色彩管理屬性](#color-management-attributes-tab) 標籤

   ![Dynamic Media發佈設定頁面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media發佈設定頁面，使用&#x200B;**[!UICONTROL 請求屬性]**標籤已選取。*<br><br>

1. 完成後，在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.

## 图像服务器 {#image-server}

「影像伺服器」頁面會建立從影像伺服器傳送影像的預設設定。 設定分為五個類別

| 发布上下文 | 描述 |
| --- | --- |
| 图像服务 | 指定發佈設定的內容。 |
| 提供测试图像 | 指定測試發佈設定的內容。<br>僅用於新Dynamic Media帳戶，預設值 **[!UICONTROL 使用者端位址]** 欄位已設為 `127.0.0.1` 自動。<br>另請參閱 [在公開資產之前先測試資產](#test-assets-before-making-public). |

### 安全性索引標籤 {#security-tab}

**[!UICONTROL 使用者端位址]**  — 可讓您指定一或多個IP位址或IP位址範圍。 指定後，系統會拒絕從未列出的IP位址之使用者端對此影像目錄提出的要求。 此規則會同時套用至影像傳送和演算後的影像。

![安全性索引標籤&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*顯示IP「允許」欄位的安全性索引標籤。*

### 目錄管理標籤 {#catalog-management-tab}

**[!UICONTROL 規則集定義檔案路徑]**  — 指定包含影像目錄的規則集定義的檔案。

另請參閱 [規則集檔案](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) Dynamic Media檢視器參考指南中的引數。

>[!NOTE]
>
>如果您的Dynamic Media Classic帳戶已有 **[!UICONTROL 規則集定義檔案路徑]** 已選取（如下所設定） **[!UICONTROL 設定]** > **[!UICONTROL 應用]** > **[!UICONTROL 發佈設定]**，下 **[!UICONTROL 目錄管理]** 群組)，則您的Dynamic Media帳戶(在Experience Manager上)會從Dynamic Media Classic擷取檔案。 然後，當您開啟 **[!UICONTROL Dynamic Media發佈設定]** 第一次瀏覽頁面。

### 請求屬性標籤 {#request-attributes-tab}

這些設定與影像的預設外觀有關。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 回复图像大小限制]** | 必填.<br>僅對於新的Dynamic Media帳戶，預設大小限制會自動設定為寬度： `3000` 和高度： `3000` 兩者 **[!UICONTROL 影像伺服]** 和 **[!UICONTROL 測試影像伺服]**.<br>指定傳回給使用者端的回覆影像寬度與高度上限。 如果要求造成回覆影像的寬度或（或）高度大於此設定，則伺服器會傳回錯誤。<br>另請參閱 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 请求混淆模式]** | 若要將base64編碼套用至有效的請求，請啟用。<br>另請參閱 [要求模糊化](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 请求锁定模式]** | 如果您想要在要求中包含簡單的雜湊鎖定，請啟用。<br>另請參閱 [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认请求属性]** |  |
| **[!UICONTROL 默认图像文件后缀]** | 必填.<br>路徑不包含檔案字尾時，附加至目錄Path和MaskPath欄位值的預設資料檔案副檔名。<br>另請參閱 [預設分機](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认字体名称]** | 指定如果文字圖層要求未提供任何字型時，使用哪種字型。 如果已指定，它必須是此影像目錄的字型地圖或預設目錄的字型地圖中的有效字型名稱值。<br>另請參閱 [預設字型](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认图像]** | 提供預設影像，以便在找不到所要求的影像時傳回。<br>另請參閱 [預設影像](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) Dynamic Media檢視器參考指南中的引數。<br>**注意**：如果您的Dynamic Media Classic帳戶已有 **[!UICONTROL 預設影像]** 已選取（如下所設定） **[!UICONTROL 設定]** > **[!UICONTROL 應用]** > **[!UICONTROL 發佈設定]**，下 **[!UICONTROL 預設請求屬性]** 群組)，則您的Dynamic Media帳戶(在Experience Manager上)會從Dynamic Media Classic擷取檔案。 然後檔案會儲存並在您開啟 **[!UICONTROL Dynamic Media發佈設定]** 第一次瀏覽頁面。 |
| **[!UICONTROL 默认图像模式]** | 啟用滑桿方塊（右側的滑桿）時， **[!UICONTROL 預設影像]** 會以預設影像取代來源影像中每個遺失的圖層，並照常傳回複合影像。 停用滑桿方塊（左側滑桿）時，預設影像會取代整個複合影像，即使遺失的影像隻是數個圖層中的一個圖層亦然。<br>另請參閱 [預設影像模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认视图大小]** | 必填.<br>僅對於新的Dynamic Media帳戶，預設檢視大小會自動設定為「寬度」： `1280` 和高度： `1280` 兩者 **[!UICONTROL 影像伺服]** 和 **[!UICONTROL 測試影像伺服]**.<br>如果要求未明確使用指定檢視大小，伺服器會將回覆影像限製為不得大於此寬度與高度。 `wid=`， `hei=`，或 `scl=`.<br>另請參閱 [預設畫素](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认缩略图大小]** | 必填.<br>已使用而非屬性 **[!UICONTROL 預設檢視大小]** 對於縮圖請求(`req=tmb`)。 如果縮圖要求(`req=tmb`)不會明確使用指定大小 `wid=`， `hei=`，或 `scl=`.<br>另請參閱 [DefaultthumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认背景颜色]** | 指定用於填滿不包含實際影像資料之回覆影像的任何區域的RGB值。<br>另請參閱 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL JPEG 编码属性]** |  |
| **[!UICONTROL 质量]** | <br>指定JPEG回覆影像的預設屬性。<br>僅針對新的Dynamic Media帳戶， **[!UICONTROL 品質]** 預設值會自動設定為 `80` 兩者 **[!UICONTROL 影像伺服]** 和 **[!UICONTROL 測試影像伺服]**.<br>此欄位的定義範圍介於1到100之間。<br>另請參閱 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 色度降采样]** | 啟用或停用JPEG編碼器使用的色度縮減取樣。 |
| **[!UICONTROL 默认重新取样模式]** | 指定縮放影像資料所使用的預設重新取樣與內插屬性。 使用時機 `resMode` 請求中未指定。<br>僅對於新的Dynamic Media帳戶，預設重新取樣模式會自動設定為 `Sharp2` 兩者 **[!UICONTROL 影像伺服]** 和 **[!UICONTROL 測試影像伺服]**.<br>另請參閱 [解析模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) Dynamic Media檢視器參考指南中的引數。 |

### 通用縮圖屬性索引標籤 {#common-thumbnail-attributes-tab}

這些設定與縮圖影像的預設外觀和對齊有關。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 缩略图的默认背景颜色]** | 指定用來對不包含實際影像資料的輸出縮圖影像區域進行填色的RGB值。 僅用於縮圖要求(`req=tmb`)和時間 **[!UICONTROL 預設縮圖型別]** 設定已設為 **[!UICONTROL 符合]** 或 **[!UICONTROL 紋理]**.<br>另請參閱 [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 水平对齐方式]** | 指定所指定的回覆影像矩形中縮圖影像的水準對齊方式 `wid=` 和 `hei=` 值。<br>僅用於縮圖要求(`req=tmb`)和時間 **[!UICONTROL 預設縮圖型別]** 設定已設為 **[!UICONTROL 符合]**.<br>有三種水準對齊方式可供選擇： **[!UICONTROL 置中對齊]**， **[!UICONTROL 靠左對齊]**、和 **[!UICONTROL 靠右對齊]**.<br>另請參閱 [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 垂直对齐方式]** | 指定所指定的回覆影像矩形中的縮圖影像垂直對齊方式 `wid=` 和 `hei=` 值。 僅用於縮圖要求(`req=tmb`)和時間 **[!UICONTROL 預設縮圖型別]** 設定已設為 **[!UICONTROL 符合]**.<br>有三個垂直對齊可供選擇： **[!UICONTROL 靠上對齊]**， **[!UICONTROL 置中對齊]**、和 **[!UICONTROL 靠下對齊]**.<br>另請參閱 [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认缓存生存时间]** | 提供預設到期時間間隔（小時），以防止特定目錄記錄未包含有效的目錄Expiration值。 設定為 `-1` 標籤為永不過期。 <br>另請參閱 [有效期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认缩略图类型]** | 提供縮圖型別的預設值，以防止特定目錄記錄未包含有效的目錄ThumbType值。 僅用於縮圖要求(`req=tmb`)。<br>有三種縮圖型別可供選擇： **[!UICONTROL 裁切]**， **[!UICONTROL 符合]**、和 **[!UICONTROL 紋理]**.<br>另請參閱 [縮圖型別](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 默认缩略图分辨率]** | 提供縮圖物件解析度的預設值，以防止特定目錄記錄未包含有效的目錄ThumbRes值。 僅用於縮圖要求(`req=tmb`)以及當 **[!UICONTROL 預設縮圖型別]** 設定已設為 **[!UICONTROL 紋理]**.<br>另請參閱 [縮圖](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) Dynamic Media檢視器參考指南中的引數。 |

### 色彩管理屬性標籤 {#color-management-attributes-tab}

這些設定會決定影像要使用的ICC色彩設定檔。

**色彩轉換演算色彩比對方式**
色彩轉換演算色彩比對方式允許覆寫使用中輪廓的預設演算色彩比對方式，以決定如何調整來源顏色。 使用時機：

1. 其中一個預設ICC設定檔是色彩轉換的目標色域。
1. 輸出裝置（印表機或熒幕）的特點就是此設定檔。
1. 而且，指定的演算色彩比對方式對此設定檔有效。

不同的演算意圖會使用不同的規則來決定如何調整來源顏色。

另請參閱 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) Dynamic Media檢視器參考指南中的引數。

>[!NOTE]
>
>一般而言，最好對選取的顏色設定使用預設的色彩演算比對方式，這些設定已經過Adobe測試以符合業界標準。 例如，如果您選擇北美或歐洲的色彩設定，預設的色彩轉換演算色彩比對方式為 **[!UICONTROL 相對比色]**. 如果您為日本選擇顏色設定，預設的色彩轉換演算色彩比對方式為 **[!UICONTROL 可感知]**.

| 设置 | 特性 |
| --- | --- |
| **[!UICONTROL CMYK 默认颜色空间]** | 指定要用作CMYK資料的使用中設定檔的ICC色彩設定檔名稱。 若 **[!UICONTROL 未指定]** 如果選擇，則在涉及CMYK來源影像時，將停用此影像目錄的色彩管理。 所有CMYK工作空間都依裝置而定，這表示它們是以實際的油墨和紙張組合為基礎。 CMYK工作區Adobe供給是根據標準商業列印條件。<br> 另請參閱 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 灰度默认色彩空间]** | 指定用作灰階資料使用中描述檔的ICC色彩描述檔名稱。 若 **[!UICONTROL 未指定]** 如果選擇，則在涉及灰階來源影像時，將停用此影像目錄的色彩管理。<br>另請參閱 [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL RGB 默认颜色空间]** | 指定要用作RGB資料的使用中設定檔的ICC色彩設定檔名稱。 若 **[!UICONTROL 未指定]** 如果選擇，則在涉及RGB來源影像時停用此影像目錄的色彩管理。 一般來說，最好選擇 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而不是特定裝置的設定檔（例如監視器設定檔）。 **[!UICONTROL sRGB]** 當您準備網頁或行動裝置的影像時，建議使用此選項，因為它會定義在網頁上檢視影像的標準監視器的色域。 **[!UICONTROL sRGB]** 當您使用消費者等級的數位相機影像時，這也是很好的選擇，因為這些相機大多使用sRGB作為預設色彩空間。<br>另請參閱 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) Dynamic Media檢視器參考指南中的引數。 |
| **[!UICONTROL 颜色转换调色]** | **[!UICONTROL 可感知]**  — 旨在保留色彩之間的視覺關係，讓人眼覺得自然，即使色彩值本身可能會變更。 此意圖適用於具有大量超出色域顏色的攝影影像。 此設定是日本印刷業的標準色彩演算方法。 |
|  | **[!UICONTROL 相對比色]**  — 比較來源色域和目的地色域的極端反白顯示，並相應地移動所有顏色。 超出色域的顏色會移到目標色域中最接近的可複製顏色。 相對比色會保留影像中比「感應式」更多的原始顏色。 此設定是北美和歐洲列印的標準色彩演算方式。 |
|  | **[!UICONTROL 飽和度]**  — 嘗試在影像中產生鮮豔的色彩，以犧牲色彩精確度為代價。 此演算色彩比對方式適用於圖形或圖表等商業圖形，其中明亮飽和色彩比色彩之間的確切關係更重要。 |
|  | **[!UICONTROL 絕對比色]**  — 讓落在目的地色域內的顏色保持不變。 超出色域的顏色會被剪裁。 不會執行將顏色縮放到目標白點的動作。 此意圖旨在維持色彩精確度，但犧牲了保留色彩之間的關係，並適合用於校樣以模擬特定裝置的輸出。 此意圖對於預覽紙張顏色如何影響列印顏色非常有用。 |

## 在公開資產之前先測試資產 {#test-assets-before-making-public}

Secure Testing可協助您定義安全的測試環境，並根據一組可設定的IP位址和範圍，建立健全的企業對企業解決方案。 此功能可讓您將AdobeDynamic Media部署與內容管理和業務系統的架構配對。

使用Secure Testing，您可以預覽含有未發佈內容的網站測試版本。

如有需要，請建立中繼環境，而非讓資產公開可用，理由如下：

* 在公開啟動前預覽網站（測試網站）。
* 提供需要限制存取的資產，例如在B2B Web應用程式中顯示價格的eCatalog。
* 使用防火牆後的資產，做為產品資訊管理系統、客戶服務應用程式、訓練網站等的一部分。

>[!NOTE]
>
>安全測試不會影響對Adobe Dynamic Media Classic的存取。 Adobe Dynamic Media Classic安全性會維持一致，且需要一般憑證才能存取Adobe Dynamic Media Classic及相關網路服務。

### 安全測試的運作方式 {#how-test-assets-works}

大多數企業都在防火牆後面執行網際網路。 網際網路存取可透過特定路由進行，通常透過有限的公用IP位址範圍進行。

透過公司網路，您可以使用以下網站找出您的公用IP位址： [https://www.whatismyip.com](https://www.whatismyip.com/) 或向您的企業IT組織索取此資訊。

透過安全測試，Adobe Dynamic Media可為中繼環境或內部應用程式建立專用的影像伺服器。 對此伺服器的任何請求都會檢查原始IP位址。 如果傳入的請求不在核准的IP位址清單中，則會傳回失敗回應。 AdobeDynamic Media公司管理員會為公司的安全測試環境設定經過核准的IP位址清單。

由於原始請求的位置必須確認，因此Secure Testing服務的流量不會透過內容發佈網路(例如公用Dynamic Media Image Server流量)進行路由。 向安全測試服務提出的請求與公開Dynamic Media影像伺服器的延遲相比，稍微高一些。

未發佈的資產可立即從Secure Testing服務取得，而不需要發佈。 透過這種方式，您可以在資產發佈到公開顯示的影像伺服器之前執行預覽。

>[!NOTE]
>
>Secure Testing服務會使用已設定內部發佈內容的目錄伺服器。 因此，如果您的公司設定為發佈至Secure Testing，則AdobeDynamic Media中任何上傳的資產都可立即透過Secure Testing服務使用。 不論資產是否標示為上傳時發佈，此功能皆為true。

Secure Testing服務目前支援下列資產型別和功能：

* 图像.
* 暈映（轉譯器伺服器請求）。
* 轉譯器伺服器請求（受支援，但必須由客戶明確請求）。
* 集，包括影像集、eCatalog、演算集和媒體集。
* 標準AdobeDynamic Media多媒體檢視器。
* AdobeDynamic Media OnDemand JSP頁面。
* 靜態內容，例如PDF檔案和逐步提供的視訊。
* HTTP視訊串流。
* 漸進式視訊串流。

目前不支援下列資產型別和功能：

* Adobe Dynamic Media Classic資訊或eCatalog搜尋
* RTMP視訊串流
* 網頁列印
* UGC （使用者產生的內容）服務

   >[!IMPORTANT]
   >
   >自2023年5月1日起，Dynamic Media中的UGC資產最多可在上傳日期後60天內使用。 60天後，資產將會移除。

   >[!NOTE]
   >
   >Adobe Dynamic Media已於2021年9月30日停止支援新的或現有的UGC向量影像資產。

### 測試Secure Testing service {#test-secure-testing-service}

若要確保Secure Testing服務如預期般運作，請執行以下操作：

#### 準備您的帳戶

1. 請聯絡Adobe客戶服務，要求他們在您的帳戶上啟用安全測試。
1. 在Adobe Experience Manager中選取 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**.
1. 在「影像伺服器」頁面的 **[!UICONTROL 發佈內容]** 下拉式清單，選取 **[!UICONTROL 測試影像伺服]**.
1. 選取 **[!UICONTROL 安全性]** 標籤。
1. 對於 **[!UICONTROL 使用者端位址]** 篩選，選取 **[!UICONTROL 新增]**.
1. 在 **[!UICONTROL ip位址]** 欄位，輸入IP位址。
1. 在 **[!UICONTROL 遮色片]** 欄位，輸入網路遮色片。

   >[!NOTE]
   >
   >如果您新增一個以上的IP位址和網路遮罩，它實際上會允許 *全部* 進行資產呼叫的IP位址，這些位址都會顯示。

1. 执行下列操作之一：

   * 若要新增更多IP位址，請重複前三個步驟。
   * 繼續下一步驟。

1. 在「影像伺服器」頁面的右上角，選取 **[!UICONTROL 儲存]**.
1. 將所需的影像上傳至您的AdobeDynamic Media帳戶。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 請確定部分影像已標示為發佈，其他影像未標示，然後提交發佈工作。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 請前往「 」，判斷Secure Testing服務的名稱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media一般設定]**.
1. 於 **[!UICONTROL 伺服器]** 頁面，在頁面右側尋找伺服器名稱 **[!UICONTROL 已發佈的伺服器名稱]**.

如果伺服器名稱遺失或伺服器的URL無法運作，請聯絡Adobe服務。

#### 準備網站變數

您需要連結已發佈和未發佈資產的兩個網站變體：

* 公開版本 — 使用傳統AdobeDynamic Media URL語法連結資產。
* 測試版本 — 使用相同語法但具有安全測試網站名稱的連結資產。

#### 執行測試

執行下列測試：

1. 檢查資產是否可從公司網路中看見。

   從先前定義的IP位址範圍所識別的公司網路中，網站的測試版本會顯示所有影像，無論是否標籤為發佈。 因此，您可以在測試時避免在預覽核准或產品上市之前意外提供影像。

   確認您的網站公開版本會顯示已發佈的資產，如同先前在AdobeDynamic Media時所體驗的一樣。

1. 從公司網路外部，確認未發佈的資產（即未標籤為發佈）受到保護，不會受到第三方存取。

   從外部存取您的網路（例如從您的家用電腦或透過4G/5G連線），然後確認公用版本的網站是否顯示所有已發佈的資產，但不顯示任何未發佈的內容。

   確認測試版本未顯示任何資產，因為您正從未核准的IP位址存取Secure Testing服務。
