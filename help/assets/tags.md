---
title: 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成
description: 瞭解適用於Experience Platform標籤和Dynamic Media Viewers 5.13的Dynamic Media Viewers擴充功能。它可讓Adobe Analytics和Experience Platform標籤的客戶在其Experience Platform標籤設定中，使用Dynamic Media檢視器的特定事件和資料。
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: cd797b1a5edd05715761f5914ebc64fdb64745af
workflow-type: tm+mt
source-wordcount: '6631'
ht-degree: 6%

---

# 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## 什麼是Dynamic Media Viewers與Adobe Analytics和Experience Platform標籤的整合？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

*Dynamic Media檢視器* Experience Platform標籤和Dynamic Media檢視器5.13的擴充功能可讓Adobe Analytics和Experience Platform標籤客戶在其Experience Platform標籤設定中，使用Dynamic Media檢視器的特定事件和資料。

此整合表示您可以使用Adobe Analytics追蹤網站上Dynamic Media Viewers的使用情況。 同時，您也可以將檢視器公開的事件和資料，與任何來自Adobe或協力廠商的其他Experience Platform標籤擴充功能搭配使用。

若要深入瞭解Adobe擴充功能或協力廠商擴充功能，請參閱 [Adobe擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) 在Experience Platform標籤使用手冊中。

**本主題適用於下列內容：** 網站管理員、Experience Platform開發人員和營運人員。

### 整合的限制 {#limitations-of-the-integration}

* Dynamic Media檢視器的Experience Platform標籤整合無法在Experience Manager作者節點中運作。 在發佈之前，您無法從WCM頁面看到任何追蹤。
* 「快顯」作業模式不支援Dynamic Media檢視器的Experience Platform標籤整合，此模式會使用「資產詳細資料」頁面上的「URL」按鈕取得檢視器URL。
* 「Experience Platform標籤」整合不能與舊版Viewers Analytics整合約時使用(透過 `config2=` 引數)。
* 視訊追蹤的支援僅限於「核心播放」追蹤，如所述 [追蹤概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en). 特別不支援QoS、廣告、章節/區段或錯誤追蹤。
* 資料元素的儲存持續時間設定不支援使用下列專案的資料元素： *Dynamic Media檢視器* 副檔名。 儲存期間必須設定為 **[!UICONTROL 無]**.

### 整合的使用案例 {#use-cases-for-the-integration}

與Experience Platform標籤整合的主要使用案例是同時使用Adobe Experience Manager Assets和Adobe Experience Manager Sites的客戶。 在這種情況下，您可以設定Experience Manager製作節點和Experience Platform標籤之間的標準整合，然後將您的Sites例項與Experience Platform標籤屬性建立關聯。 之後，新增至Sites頁面的任何Dynamic Media WCM元件都將追蹤檢視器的資料和事件。

另請參閱 [在Experience Manager Sites中追蹤Dynamic Media檢視器](#tracking-dynamic-media-viewers-in-aem-sites).

整合支援的次要使用案例為僅使用Experience Manager Assets或Dynamic Media Classic的客戶。 在這種情況下，您需要取得檢視器的內嵌程式碼，並將其新增至網站頁面。 然後，從Experience Platform標籤中取得Experience Platform標籤程式庫生產URL，並手動將其新增至網頁程式碼。

另請參閱 [使用內嵌程式碼追蹤Dynamic Media檢視器](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## 資料和事件追蹤在整合中的運作方式 {#how-data-and-event-tracking-works-in-the-integration}

此整合採用兩種獨立的Dynamic Media檢視器追蹤型別： *Adobe Analytics* 和 *適用於音訊和視訊的Adobe Analytics*.

### 關於使用Adobe Analytics進行追蹤  {#about-tracking-using-adobe-analytics}

Adobe Analytics可讓您追蹤一般使用者在您網站上與Dynamic Media Viewers互動時所執行的動作。 Adobe Analytics也可讓您追蹤檢視器特定資料。 例如，您可以追蹤並記錄檢視載入事件以及資產名稱、任何已發生的縮放動作和視訊播放動作。

在Experience Platform標籤中， *資料元素* 和 *規則* 共同啟用Adobe Analytics追蹤。

#### 關於Experience Platform標籤中的資料元素 {#about-data-elements-in-adobe-launch}

Experience Platform標籤中的資料元素是已命名屬性，其值會以靜態方式定義，或根據網頁或Dynamic Media檢視器資料的狀態進行動態計算。

資料元素定義可用的選項取決於Experience Platform標籤屬性中安裝的擴充功能清單。 「核心」擴充功能已預先安裝，且在任何設定中均可立即使用。 此「核心」擴充功能可定義資料元素，其值來自Cookie、JavaScript程式碼、查詢字串和許多其他來源。

如所述，針對Adobe Analytics追蹤，必須安裝其他多個擴充功能 [擴充功能的安裝及設定](#installing-and-setup-of-extensions). Dynamic Media Viewers擴充功能新增定義「資料元素」的功能，而「資料元素」值是「動態檢視器」事件的引數。 例如，可參照檢視器型別，或檢視器載入時報告的資產名稱，以及一般使用者縮放時報告的縮放等級等等。

Dynamic Media Viewer擴充功能會自動將其資料元素的值維持在最新狀態。

定義資料元素後，您可使用資料元素選擇器Widget，將其用於Experience Platform標籤UI的其他位置。 尤其是，為追蹤Dynamic Media檢視器而定義的資料元素，會由「規則」中Adobe Analytics擴充功能的「設定變數」動作參照（請參閱下文）。

另請參閱 [資料元素](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html).

#### 關於Experience Platform標籤中的規則 {#about-rules-in-adobe-launch}

Experience Platform標籤中的規則是一種不可知的設定，它定義了構成規則的三個區域： *事件*， *條件*、和 *動作*：

* *事件* (if)告知Experience Platform標籤何時觸發規則。
* *條件* （如果）告知Experience Platform標籤在觸發規則時允許或禁止哪些其他限制。
* *動作* (then)指示Experience Platform標籤觸發規則時該做什麼。

「事件」、「條件」和「動作」區段中可用的選項取決於Experience Platform標籤屬性中安裝的擴充功能。 此 *核心* 擴充功能已預先安裝，並可隨時用於任何設定。 擴充功能提供數個事件選項，例如基本瀏覽器層級的動作。 這些動作包括焦點變更、按鍵和表單提交。 此外也包含「條件」選項，例如Cookie值、瀏覽器型別等。 對於「動作」，只有「自訂程式碼」選項可用。

針對Adobe Analytics追蹤，必須安裝數個其他擴充功能，如所述 [擴充功能的安裝及設定](#installing-and-setup-of-extensions). 具體來說：

* Dynamic Media Viewers擴充功能可擴充支援的事件清單，以擴充至Dynamic Media檢視器專屬的事件，例如檢視器載入、資產交換、放大和視訊播放。
* Adobe Analytics擴充功能擴充了支援的動作清單，提供傳送資料至追蹤伺服器所需的兩個動作： *設定變數* 和 *傳送信標*.

若要追蹤Dynamic Media檢視器，您可以使用下列任何型別：

* 來自Dynamic Media Viewers擴充功能、核心擴充功能或任何其他擴充功能的事件。
* 規則定義中的條件。 或者，您也可以將條件區域留空。

在「動作」區段中，您必須擁有 *設定變數* 動作。 此動作可告知Adobe Analytics如何使用資料填入追蹤變數。 同時， *設定變數* 動作不會傳送任何內容至追蹤伺服器。

此 *設定變數* 動作後面必須跟有 *傳送信標* 動作。 此 *傳送信標* 動作實際上會將資料傳送至analytics追蹤伺服器。 這兩個動作， *設定變數* 和 *傳送信標*，來自Adobe Analytics擴充功能。

另請參閱 [規則](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html).

#### 範例設定 {#sample-configuration}

Experience Platform標籤內的下列設定範例示範如何在檢視器載入時追蹤資產名稱。

1. 從 **[!UICONTROL 資料元素]** 標籤，定義資料元素 `AssetName` 該參考 `asset` 的引數 `LOAD` Dynamic Media Viewers擴充功能中的事件。

   ![image2019-11](assets/image2019-11.png)

1. 從 **[!UICONTROL 規則]** 標籤，定義規則 *TrackAssetOnLoad*.

   在此規則中， **[!UICONTROL 事件]** 欄位使用 **[!UICONTROL 載入]** Dynamic Media Viewers擴充功能中的事件。

   ![image2019-22](assets/image2019-22.png)

1. 動作設定有兩種Adobe Analytics擴充功能的動作型別：

   *設定變數*，將您選擇的analytics變數對應至 `AssetName` 資料元素。

   *傳送信標*，會將追蹤資訊傳送至Adobe Analytics。

   ![image2019-3](assets/image2019-3.png)

1. 產生的規則設定如下所示：

   ![image2019-4](assets/image2019-4.png)

### 關於適用於音訊和視訊的Adobe Analytics {#about-adobe-analytics-for-audio-and-video}

當Experience Cloud帳戶訂閱使用Adobe Analytics for Audio and Video時，即足以在中啟用視訊追蹤 *Dynamic Media檢視器* 擴充功能設定。 視訊量度可在Adobe Analytics中使用。 視訊追蹤取決於Adobe Medium Analytics for Audio and Video擴充功能的存在。

另請參閱 [擴充功能的安裝及設定](#installing-and-setup-of-extensions).

目前，視訊追蹤支援僅限「核心播放」追蹤，如所述 [追蹤概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en). 特別不支援QoS、廣告、章節/區段或錯誤追蹤。

## 使用Dynamic Media Viewers擴充功能 {#using-the-dynamic-media-viewers-extension}

如中所述 [整合的使用案例](#use-cases-for-the-integration)，即可透過Experience Manager Sites中的新Experience Platform標籤整合及使用內嵌程式碼來追蹤Dynamic Media檢視器。

### 在Experience Manager Sites中追蹤Dynamic Media檢視器 {#tracking-dynamic-media-viewers-in-aem-sites}

若要在Experience Manager Sites中追蹤Dynamic Media檢視器， [設定所有整合專案](#configuring-all-the-integration-pieces) 區段必須執行。 具體來說，您必須建立IMS設定和Experience Platform標籤雲端設定。

正確設定後，您使用Dynamic Media支援的WCM元件新增至網站頁面的任何Dynamic Media檢視器，都會自動追蹤資料到Adobe Analytics或Adobe Analytics for Video，或兩者皆追蹤。

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### 使用內嵌程式碼追蹤Dynamic Media檢視器 {#tracking-dynamic-media-viewers-using-embed-code}

未使用Experience Manager Sites或（或）未將Dynamic Media檢視器內嵌至Experience Manager Sites外部網頁的客戶，仍可使用Experience Platform標籤整合。

完成設定步驟，從 [設定Adobe Analytics](#configuring-adobe-analytics-for-the-integration) 和 [設定Experience Platform標籤](#configuring-adobe-launch-for-the-integration) 區段。 不過，不需要Experience Manager相關的設定步驟。

在正確設定後，您可以使用Dynamic Media檢視器將Experience Platform標籤支援新增至網頁。

另請參閱 [新增Experience Platform標籤內嵌程式碼](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) 以進一步瞭解如何使用Experience Platform標籤程式庫內嵌程式碼。

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**使用內嵌程式碼追蹤Dynamic Media檢視器：**

1. 建立可內嵌Dynamic Media檢視器的網頁。
1. 請先登入Experience Platform標籤，取得Experience Platform標籤程式庫的內嵌程式碼(請參閱 [設定Experience Platform標籤](#configuring-adobe-launch-for-the-integration))。
1. 選取 **[!UICONTROL 屬性]**，然後選取 **[!UICONTROL 環境]** 標籤。
1. 選擇與網頁環境相關的環境層級。 然後，在 **[!UICONTROL 安裝]** 欄中，選取方塊圖示。
1. **[!UICONTROL 在Web安裝指示中]** 對話方塊中，複製完整的Experience Platform標籤程式庫內嵌程式碼，以及周圍的程式碼 `<script/>` 標籤之間。

## Dynamic Media Viewers擴充功能的參考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 關於Dynamic Media檢視器設定 {#about-the-dynamic-media-viewers-configuration}

如果符合以下條件，Dynamic Media Viewer擴充功能會自動與Experience Platform標籤程式庫整合：

* Experience Platform標籤程式庫全域物件( `_satellite`)會顯示在頁面上。
* Dynamic Media檢視器擴充功能函式 `_dmviewers_v001()` 定義於 `_satellite`.

* `config2=` 未指定檢視器引數，這表示檢視器不會使用舊版Analytics整合。

此外，還有一個選項，可透過指定以下專案來明確停用檢視器中的Experience Platform標籤整合 `launch=0` 檢視器設定中的引數。 此引數的預設值為 `1`.

### 設定Dynamic Media Viewers擴充功能 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media Viewers擴充功能的唯一設定選項是 **[!UICONTROL 啟用音訊和視訊的Adobe Medium Analytics]**.

勾選（啟用）此選項，且已安裝並設定Adobe Medium Analytics for Audio and Video擴充功能時，視訊播放量度會傳送至Adobe Analytics for Audio and Video解決方案。 停用此選項會關閉視訊追蹤。

如果您啟用此選項 *不含* 安裝Adobe Medium Analytics for Audio and Video擴充功能後，選項沒有作用。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 關於Dynamic Media檢視器擴充功能中的資料元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media Viewers 扩展提供的唯一数据元素类型是&#x200B;**[!UICONTROL 数据元素类型]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 查看器事件]**。

選取後，資料元素編輯器會呈現包含兩個欄位的表單：

* **[!UICONTROL DM 查看器事件数据类型]** - 一个下拉列表，标识了 Dynamic Media 查看器扩展支持的所有查看器事件（具有参数）以及特殊的 **[!UICONTROL COMMON]** 项目。**[!UICONTROL COMMON]** 项目表示事件参数列表，这些事件参数对查看器发送的所有类型事件都是通用的。
* **[!UICONTROL 追蹤引數]**  — 所選Dynamic Media檢視器事件的引數。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

請參閱 [Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 如需各種檢視器型別的支援事件清單，請前往特定檢視器區段，然後選取「支援Adobe Analytics追蹤」子區段。 目前，Dynamic Media檢視器參考指南不會記錄事件引數。

現在請考慮Dynamic Media檢視器的生命週期 *資料元素*. 此資料元素的值會在頁面上發生對應的Dynamic Media檢視器事件後填入。 例如，假設資料元素指向 **[!UICONTROL 載入]** 事件及其「asset」引數。 在此情況下，檢視器執行「 」後，此資料元素的值就會收到有效資料。 **[!UICONTROL 載入]** 第一次的事件。 如果資料元素指向 **[!UICONTROL 縮放]** 事件及其「縮放」引數，在檢視器傳送 **[!UICONTROL 縮放]** 第一次的事件。

同样，当查看器在页面上发送相应事件时，数据元素的值也会自动更新。即使在规则配置中未指定特定事件，也会发生值更新。例如，假設資料元素 **[!UICONTROL 縮放比例]** 是為ZOOM事件的「縮放」引數定義的。 不過，規則設定中唯一存在的規則是由 **[!UICONTROL 載入]** 事件。 的值 **[!UICONTROL 縮放比例]** 仍會在每次使用者在檢視器內執行縮放時更新。

任何Dynamic media查看器在网页上都有唯一标识符。 資料元素會追蹤值本身，以及填入值的檢視器。 例如，假設同一頁面上有數個檢視器，且 **[!UICONTROL 資產名稱]** 資料元素指向 **[!UICONTROL 載入]** 事件及其「asset」引數。 此 **[!UICONTROL 資產名稱]** 「資料元素」會維護與頁面上載入的每個檢視器相關聯的資產名稱集合。

資料元素傳回的確切值取決於上下文。 若資料元素是在由Dynamic Media檢視器事件觸發的規則中要求，則會傳回起始規則的檢視器資料元素值。 而且，資料元素是在某個其他Experience Platform標籤擴充功能的「事件」所觸發的規則中要求。 此時，資料元素的值來自上次更新此資料元素的檢視器。

**考量下列範例設定：**

* 具有兩個Dynamic Media縮放檢視器的網頁： *檢視者1* 和 *檢視器2*.

* **[!UICONTROL 縮放比例]** 資料元素指向 **[!UICONTROL 縮放]** 事件及其「縮放」引數。
* **[!UICONTROL Trackpan]** 規則與下列專案：

   * 使用Dynamic Media檢視器 **[!UICONTROL 平移]** 事件作為觸發條件。
   * 傳送值 **[!UICONTROL 縮放比例]** 資料元素重新命名為Adobe Analytics。

* **[!UICONTROL TrackKey]** 規則與下列專案：

   * 使用核心Experience Platform標籤擴充功能的按鍵事件作為觸發器。
   * 傳送值 **[!UICONTROL 縮放比例]** 資料元素重新命名為Adobe Analytics。

現在，假設使用者載入網頁時具有兩個檢視器。 在 *檢視者1*，然後放大至50%的縮放比例；接著放大 *檢視器2*，則會放大至25%的縮放比例。 在 *檢視者1*，然後移動影像，最後在鍵盤上選取按鍵。

一般使用者的活動會導致對Adobe Analytics進行以下兩個追蹤呼叫：

* 發生第一次呼叫是因為 **[!UICONTROL Trackpan]** 當使用者進入時觸發規則 *檢視者1*. 該呼叫傳送50%作為的值 **[!UICONTROL 縮放比例]** 資料元素，因為資料元素知道規則觸發自 *檢視者1* 和會擷取對應的比例值；
* 第二個呼叫的發生是因為 **[!UICONTROL TrackKey]** 當使用者按下鍵盤上的按鍵時觸發規則。 該呼叫傳送25%作為值 **[!UICONTROL 縮放比例]** 資料元素，因為檢視器未觸發規則。 因此，資料元素會傳回最新的值。

上述設定的範例也會影響資料元素值的生命週期。 即使檢視器本身已放置在網頁上，Dynamic Media檢視器所管理的資料元素值仍會儲存在Experience Platform標籤程式庫程式碼中。 此功能表示，如果非Dynamic Media Viewer擴充功能觸發規則，並參照此類資料元素，資料元素會傳回最後一個已知值。 即使檢視器不再出現在網頁上。

無論如何，Dynamic Media檢視器所驅動的資料元素值不會儲存在本機儲存空間或伺服器上，而是只會儲存在使用者端Experience Platform標籤資料庫上。 網頁重新載入時，此資料元素的值會消失。

一般而言，資料元素編輯器支援 [儲存期間選擇](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). 不過，使用Dynamic Media檢視器擴充功能的資料元素僅支援的儲存持續時間選項： **[!UICONTROL 無]**. 您可以在使用者介面中設定任何其他值，但在此情況下不會定義資料元素行為。 擴充功能會自行管理「資料元素」的值：「資料元素」，會在整個檢視器生命週期中維護檢視器事件引數的值。

### 關於Dynamic Media檢視器擴充功能中的規則 {#about-rules-in-the-dynamic-media-viewers-extension}

在規則編輯器中，擴充功能會為事件編輯器新增設定選項。 此外，編輯器也提供在動作編輯器中手動參考事件引數的選項，作為簡短選項，而不使用預先設定的資料元素。

#### 關於事件編輯器 {#about-the-events-editor}

在「事件」編輯器中，「Dynamic Media檢視器」擴充功能會新增 **[!UICONTROL 事件型別]** 已呼叫 **[!UICONTROL 檢視器事件]**.

選取後，事件編輯器會呈現下拉式清單 **[!UICONTROL Dynamic Media Viewer事件]**，列出Dynamic Media檢視器支援的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 關於動作編輯器 {#about-the-actions-editor}

Dynamic Media檢視器擴充功能可讓您使用Dynamic Media檢視器的事件引數，以對應至Adobe Analytics擴充功能之「設定變數」編輯器中的分析變數。

最簡單的方法是完成以下兩個步驟的流程：

* 首先，定義一或多個資料元素，其中每個資料元素代表Dynamic Media Viewer事件的引數。
* 最後，在Adobe Analytics擴充功能的「設定變數」編輯器中，選取 **[!UICONTROL 資料元素]** 選擇器圖示（三個棧疊的磁碟）以開啟「選取資料元素」對話方塊，然後從其中選取資料元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

但是，可以使用替代方法并绕过数据元素创建。您可以直接參照Dynamic Media Viewer事件的引數。 在中輸入事件引數的完整名稱 **[!UICONTROL 值]** Analytics變數指派的輸入欄位。 請務必加上百分比(%)符號。 例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

使用資料元素與直接事件引數參考之間有重大差異。 對於資料元素，哪個事件會觸發「設定變數」動作並不重要。 觸發規則的事件可能與動態檢視器無關。 例如，從核心擴充功能選取網頁。 但是，使用直接引數參考時，請務必確保觸發規則的事件對應到它參考的事件引數。

例如，如果规 `%event.detail.dm.LOAD.asset%` 则是由Dynamic Media Viewer扩展的 **[!UICONTROL LOAD]** 事件触发的，则引用将返回正确的资产名称。 但是，对于任何其他事件，它都会返回一个空值。

下表列出Dynamic Media Viewer事件及其支援的引數：

<table>
 <tbody>
  <tr>
   <td>檢視器事件名稱</td>
   <td>引數參考</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## 設定所有整合專案 {#configuring-all-the-integration-pieces}

**開始之前**

Adobe建議您仔細檢閱本節之前的所有檔案，以瞭解完整的整合。

本節說明將Dynamic Media檢視器與Adobe Analytics和用於音訊與視訊的Adobe Analytics整合所需的設定步驟。 雖然Dynamic Media檢視器擴充功能可用於Experience Platform標籤中的其他用途，但本檔案未涵蓋這類案例。

您即將使用下列Adobe產品來設定整合：

* Adobe Analytics — 用於設定追蹤變數和報表。
* Experience Platform標籤 — 用來定義屬性、一個或多個規則以及一個或多個資料元素，以啟用檢視器追蹤。

此外，如果此整合解決方案搭配Experience Manager Sites使用，則還必須完成以下設定：

* [!DNL Adobe Developer Console]  — 會為Experience Platform標籤建立整合。
* Experience Manager作者節點 — IMS設定和Experience Platform標籤雲端設定。

在設定中，請確定您有權存取Adobe Experience Cloud中已啟用Adobe Analytics和Experience Platform標籤的公司。

## 設定Adobe Analytics以進行整合 {#configuring-adobe-analytics-for-the-integration}

設定Adobe Analytics後，系統會針對整合進行下列設定：

* 報告套裝已就位並選取。
* Analytics變數可用來接收追蹤資料。
* 報表可用來檢視Adobe Analytics內收集的資料。

另請參閱 [Analytics實作指南](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**若要設定Adobe Analytics以進行整合：**

1. 從Experience Cloud存取Adobe Analytics開始 [首頁](https://experience.adobe.com/#/home). 在功能表列上，選取 **[!UICONTROL 解決方案]** 圖示（一個三乘三的點表），然後選取 **[!UICONTROL 分析]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   現在選取報表套裝。

### 選取報表套裝 {#selecting-a-report-suite}

1. 在 Adobe Analytics 页面的右上角附近，在&#x200B;**[!UICONTROL 搜索报告]**&#x200B;字段的右侧，从下拉列表中选择正确的报表包。如果有多个可用报表包，并且您不确定要使用哪个报表包，请与 Adobe Analytics 管理员联系，帮助您选择要使用的报表包。

   在下方熒幕擷圖中，使用者已建立報表套裝，並命名為 *DynamicMediaViewersExtensionDoc* 並從下拉式清單中選取。 報表套裝名稱僅為範例名稱。 您最終選取的報表套裝名稱由您決定。

   如果沒有可用的報表套裝，您或您的Adobe Analytics管理員必須先建立一個報表套裝，然後才能繼續進行設定。

   另請參閱 [報表與報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) 和 [建立報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   在Adobe Analytics中，報表套裝由 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   現在設定Adobe Analytics變數。

### 設定Adobe Analytics變數 {#setting-up-adobe-analytics-variables}

1. 指定一或多個Adobe Analytics變數，以用來追蹤網頁上的Dynamic Media檢視器行為。

   您可以使用Adobe Analytics支援的任何變數型別。 關於變數型別的決定（如自訂流量） [prop]，轉換 [eVar])取決於Analytics實作的特定需求。

   另請參閱 [Prop和eVar概觀](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   就本檔案而言，僅會使用自訂流量(prop)變數，因為自訂流量在網頁上發生動作後，幾分鐘內便可在Analytics報表中使用。

   若要啟用新的自訂流量變數，請在Adobe Analytics的工具列中，前往 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**.

1. 於 **[!UICONTROL 報表套裝管理員]** 頁面上，選取正確的報表，然後在工具列中導覽至 **[!UICONTROL 編輯設定]** > **[!UICONTROL 流量]** > **[!UICONTROL 流量變數]**.
1. 選取未使用的變數，為其提供描述性名稱(**[!UICONTROL 檢視器資產(prop 30)]**)，並在「已啟用」欄中將下拉式方塊變更為「已啟用」。

   以下熒幕擷圖為自訂流量變數( **[!UICONTROL prop30]**)以追蹤檢視器使用的資產名稱：

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. 在變數清單底部，選取 **[!UICONTROL 儲存]**.

### 設定報表 {#setting-up-a-report}

1. 一般而言，在Adobe Analytics中設定報表是由特定專案需求所驅動。 因此，詳細報表設定不在本次整合的涵蓋範圍內。

   不過，只要您在中設定自訂流量變數後， 「自訂流量」報表就能在Adobe Analytics中自動使用 [設定Adobe Analytics變數](#setting-up-adobe-analytics-variables).

   例如，以下專案的報表： **[!UICONTROL 檢視器資產(prop 30)]** 變數可從下方的「報表」功能表取得 **[!UICONTROL 自訂流量]** > **[!UICONTROL 自訂流量21-30]** > **[!UICONTROL 檢視器資產(prop 30)]**.

   在查看器资产(prop 30)创 **[!UICONTROL 建后直接访问此报告]** ，不显示任何数据；在整合的这一阶段，人们就会期待它。

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## 設定整合的Experience Platform標籤 {#configuring-adobe-launch-for-the-integration}

設定Experience Platform標籤後，系統會針對整合設定下列專案：

* 建立新屬性以將您的所有設定放在一起。
* 擴充功能的安裝和設定。 屬性中安裝的所有擴充功能的使用者端程式碼會一起編譯至程式庫中。 此程式庫稍後會由網頁使用。
* 資料元素和規則的設定。 此設定會定義從Dynamic Media檢視器擷取哪些資料、何時觸發追蹤邏輯，以及在Adobe Analytics中將檢視器資料傳送至何處。
* 程式庫的發佈。

**若要設定整合的Experience Platform標籤：**

1. 首先，從Experience Cloud存取Experience Platform標籤 [首頁](https://experience.adobe.com/#/home). 在功能表列上，選取 **[!UICONTROL 解決方案]** 圖示（三乘三點表）並選取右上角，接著選取「 」 **[!UICONTROL 標籤]**.

   您也可以 [直接開啟Experience Platform標籤](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Experience Platform標籤中建立屬性 {#creating-a-property-in-adobe-launch}

Experience Platform標籤中的屬性是具名設定，可讓您的所有設定維持在一起。 系統會產生組態設定程式庫，並發佈至不同的環境層級（開發、測試和生產）。

另請參閱 [建立Tags屬性](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

1. 在Experience Platform標籤中，選取 **[!UICONTROL 新增屬性]**.
1. 在&#x200B;**[!UICONTROL 创建属性]**&#x200B;对话框的&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入描述性名称，如网站的标题。例如，`DynamicMediaViewersProp.`
1. 在 **[!UICONTROL 網域]** 欄位中，輸入您網站的網域。
1. 在 **[!UICONTROL 進階選項]** 下拉式清單，啟用 **[!UICONTROL 設定擴充功能開發（之後無法修改）]** 如果您想使用的擴充功能，在本例中， *Dynamic Media檢視器* — 尚未發行。

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

   選取新建立的屬性，然後繼續前往 *擴充功能的安裝及設定*.

### 安裝及設定擴充功能 {#installing-and-setup-of-extensions}

「Experience Platform標籤」中所有可用的擴充功能都會列於 **[!UICONTROL 擴充功能]** > **[!UICONTROL 目錄]**.

若要安裝擴充功能，請選取 **[!UICONTROL 安裝]**. 如有需要，請執行一次性擴充功能設定，然後選取「 」 **[!UICONTROL 儲存]**.

必要時，必須安裝並設定下列擴充功能：

* （必要） *Experience CloudID服務* 副檔名。

無需額外設定，接受任何建議值。 完成後，請務必選取 **[!UICONTROL 儲存]**.

另請參閱 [Adobe Experience Cloud Identity Service擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* （必要） *Adobe Analytics* 擴充功能

若要設定此擴充功能，您需要Adobe Analytics中下方的「報表套裝ID」 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**，位於 **[!UICONTROL 報表套裝ID]** 欄標題。

(僅供示範之用， **[!UICONTROL DynamicMediaViewersExtensionDoc]** 報表套裝用於下列熒幕擷取畫面。 此ID已建立並用於 [選取報表套裝](#selecting-a-report-suite) 較早。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在“安装扩展”页面的&#x200B;**[!UICONTROL 开发报表包]**&#x200B;字段、**[!UICONTROL 测试报表包]**&#x200B;字段和&#x200B;**[!UICONTROL 生产报表包]**&#x200B;字段中输入报表包 ID。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*只有在您打算使用視訊追蹤時，才設定下列專案：*

於 **[!UICONTROL 安裝擴充功能]** 頁面，展開 **[!UICONTROL 一般]**，然後指定追蹤伺服器。 追蹤伺服器會遵循範本 `<trackingNamespace>.sc.omtrdc.net`，其中 `<trackingNamespace>` 是在布建電子郵件中取得的資訊。

选择&#x200B;**[!UICONTROL 保存]**。

另請參閱 [Adobe Analytics擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* （選用；只有在需要視訊追蹤時才需要） *適用於音訊和視訊的Adobe Medium Analytics* 擴充功能

填寫追蹤伺服器欄位。 的追蹤伺服器 *適用於音訊和視訊的Adobe Medium Analytics* 擴充功能與Adobe Analytics使用的追蹤伺服器不同。 它會依循範本 `<trackingNamespace>.hb.omtrdc.net`，其中 `<trackingNamespace>` 是來自布建電子郵件的資訊。

所有其他欄位都是選用欄位。

另請參閱 [Adobe Medium Analytics for Audio and Video擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* （必要） *Dynamic Media檢視器* 擴充功能

选择&#x200B;**[!UICONTROL 启用 Adobe Analytics for Video]** 以启用（打开）视频检测信号跟踪。

截至本文撰寫， *Dynamic Media檢視器* 擴充功能僅適用於為開發建立Experience Platform標籤屬性時。

另請參閱 [在Experience Platform標籤中建立屬性](#creating-a-property-in-adobe-launch).

在安裝及設定擴充功能後，擴充功能>已安裝區域將至少列出下列五個擴充功能（四個，如果您未追蹤視訊）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 設定資料元素和規則 {#setting-up-data-elements-and-rules}

在Experience Platform標籤中，建立追蹤Dynamic Media檢視器所需的資料元素和規則。

另請參閱 [資料和事件追蹤在整合中的運作方式](#how-data-and-event-tracking-works-in-the-integration) 以取得使用Experience Platform標籤追蹤的概觀。

另請參閱 [範例設定](#sample-configuration) ，取得Experience Platform標籤中的範例設定，示範如何在檢視器載入時追蹤資產名稱。

另請參閱 [設定Dynamic Media Viewers擴充功能](#configuring-the-dynamic-media-viewers-extension) 以取得有關擴充功能功能的深入資訊。

### 發佈程式庫 {#publishing-a-library}

若要變更Experience Platform標籤設定（包括屬性、擴充功能、規則和資料元素設定），您必須 *發佈* 這類變更。 從「屬性」設定下的「發佈」標籤執行「Experience Platform標籤」中的發佈。

Experience Platform標籤可能具有多個開發環境、一個中繼環境及一個生產環境。 根據預設，Experience Manager中的Experience Platform標籤雲端設定會將Experience Manager作者節點指向Experience Platform標籤的舞台環境。 Experience Manager發佈節點指向Experience Platform標籤的生產環境。 此安排表示使用預設Experience Manager設定時，必須將Experience Platform標籤程式庫發佈至測試環境。 如此可讓您在Experience Manager作者中使用它。 然後，您可以將其發佈到生產環境，以便用於Experience Manager發佈。

另請參閱 [環境](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) 以取得有關Experience Platform標籤環境的詳細資訊。

發佈程式庫需執行下列兩個步驟：

* 將所有必要的變更（新變更和更新）納入程式庫，以新增和建立新程式庫。
* 在不同環境層級（從開發到測試及生產）中向上移動程式庫。

#### 新增及建置新程式庫 {#adding-and-building-a-new-library}

1. 第一次在Experience Platform標籤中開啟「發佈」標籤時，資料庫清單是空的。

   在左欄中，選取 **[!UICONTROL 新增程式庫]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在「建立新程式庫」頁面的 **[!UICONTROL 名稱]** 欄位，輸入新程式庫的描述性名稱。 例如，

   *DynamicMediaViewersLib*

   從「環境」下拉式清單中選擇「環境」層級。 最初，只有開發層級可供選取。 在頁面的左下角附近，選取 **[!UICONTROL 新增所有變更的資源]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存並為開發環境建置]**.

   幾分鐘後，程式庫就會建立並準備使用。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次變更Experience Platform標籤設定時，請前往 **[!UICONTROL 發佈]** 標籤下的 **[!UICONTROL 屬性]** 設定，然後選取您先前建立的程式庫。
   >
   >
   >在程式庫發佈畫面中，選取 **[!UICONTROL 新增所有變更的資源]**，然後選取 **[!UICONTROL 儲存並為開發環境建置]**.

#### 在環境層級中向上移動程式庫 {#moving-a-library-up-through-environment-levels}

1. 新增程式庫後，即可在開發環境中找到該程式庫。 若要將其移至測試環境層級（對應至「已提交」欄），請從程式庫的下拉式功能表中選取 **[!UICONTROL 提交以進行核准]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在確認對話方塊中選取 **[!UICONTROL 提交]**.

   程式庫移至「已提交」欄後，從程式庫的下拉式功能表中選取 **[!UICONTROL 為測試環境建置]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 若要將程式庫從測試環境移至生產環境（亦即「已發佈」欄），請遵循類似程式。

   首先，從下拉式功能表中選取 **[!UICONTROL 核准以發佈]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 從下拉式選單中選取 **[!UICONTROL 建置並發佈至生產環境]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   另請參閱 [發佈](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) 以取得Experience Platform標籤中發佈程式的詳細資訊。

## 設定Adobe Experience Manager以進行整合 {#configuring-adobe-experience-manager-for-the-integration}

前提条件:

* Experience Manager會執行Author和Publish例項。
* Experience Manager作者節點設定於Dynamic Media - Scene7執行模式(dynamicmedia_s7)
* Dynamic Media WCM元件會在Experience Manager Sites中啟用。

Experience Manager設定包含下列兩個主要步驟：

* Experience ManagerIMS的設定。
* Experience Platform標籤雲端的設定。

### 設定Experience ManagerIMS {#configuring-aem-ims}

1. 在Experience Manager作者中，選取 **[!UICONTROL 工具]** 圖示（槌子），然後前往 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在「AdobeIMC設定」頁面的左上角附近，選取 **[!UICONTROL 建立]**.
1. 於 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面，在 **[!UICONTROL 雲端解決方案]** 下拉式清單，選取 **[!UICONTROL Experience Platform標籤]**.
1. 啟用 **[!UICONTROL 建立新憑證]**，然後在文字欄位中，為您的憑證輸入任何有意義的值。 例如， *AdobeLaunchIMSCert*. 選取 **[!UICONTROL 建立憑證]**.

   會顯示下列資訊訊息：

   *若要擷取有效的存取Token，新憑證的公開金鑰會新增至Adobe Developer Console上的技術帳戶！*

   若要關閉「資訊」對話方塊，請選取 **[!UICONTROL 確定]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 若要下載公開金鑰檔案(&#42;.crt)，選取 **[!UICONTROL 下載公開金鑰]**.

   >[!NOTE]
   >
   >此時， ***保持開啟*** 此 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面； ***不要*** 關閉頁面並 ***不要*** 選取「下一步」。 您稍後將在步驟中返回此頁面。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的瀏覽器標籤中，瀏覽至 [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/integrations).

1. 從 **[!UICONTROL Adobe Developer主控台整合]** 頁面，右上角附近，選取 **[!UICONTROL 新整合]**.
1. 在 **[!UICONTROL 建立新的整合]** 對話方塊，確認 **[!UICONTROL 存取API]** 已選取選項按鈕，然後選取 **[!UICONTROL 繼續]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 於第二個 **[!UICONTROL 建立新的整合]** 頁面，啟用（開啟） **[!UICONTROL Experience Platform標籤API]** 選項按鈕。 在頁面的右下角，選取 **[!UICONTROL 繼續]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 於第三個 **[!UICONTROL 建立新的整合]** 頁面，請執行下列動作：

   * 在 **[!UICONTROL 名稱]** 欄位，輸入描述性名稱。 例如， *DynamicMediaViewersIO*.

   * 在 **[!UICONTROL 說明]** 欄位中，輸入整合的說明。

   * 在 **[!UICONTROL 公開金鑰憑證]** 區域，上傳您的公開金鑰檔案(&#42;.crt)之前在這些步驟中下載的檔案。

   * 在 **[!UICONTROL 選取Experience Platform標籤API的角色]** 標題，選取 **[!UICONTROL 管理員]**.

   * 在 **[!UICONTROL 為Experience Platform標籤API選取一或多個產品設定檔]** 標題，選取名為的產品設定檔 **[!UICONTROL 標籤 —  &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 選取 **[!UICONTROL 建立整合]**.
1. 於 **[!UICONTROL 已建立整合]** 頁面，選取 **[!UICONTROL 繼續前往整合詳細資訊]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 整合詳細資訊頁面隨即顯示， **** 類似於以下內容：

   >[!NOTE]
   >
   >***保持打开此集成详细信息页面***。您將會需要 **[!UICONTROL 概觀]** 和 **[!UICONTROL JWT]** 快速建立標籤。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   整合詳細資訊頁面。

1. 返回之前打开的 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。在頁面的右上角，選取 **[!UICONTROL 下一個]** 以開啟 **[!UICONTROL 帳戶]** 中的頁面 **[!UICONTROL Adobe IMS技術帳戶設定]** 視窗。

   (如果您先前關閉頁面，請返回Experience Manager作者，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**. 选择&#x200B;**[!UICONTROL 创建]**。在 **[!UICONTROL 雲端解決方案]** 下拉式清單，選取 **[!UICONTROL Experience Platform標籤]**. 在 **[!UICONTROL 憑證]** 下拉式清單，選取先前建立之憑證的名稱。)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Adobe IMS技術帳戶設定 — 憑證頁面。

1. 此 **[!UICONTROL 帳戶]** 頁面有五個欄位，您必須使用上一步驟之整合詳細資訊頁面的資訊來填寫。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Adobe IMS技術帳戶設定 — 帳戶頁面。

1. 於 **[!UICONTROL 帳戶]** 頁面，填寫下列欄位：

   * **[!UICONTROL 標題]**  — 輸入描述性科目標題。
   * **[!UICONTROL 授權伺服器]**  — 返回您先前開啟的整合詳細資訊頁面。 選取 **[!UICONTROL JWT]** 標籤。 複製伺服器名稱（不含路徑），如下方反白所示。

（伺服器名稱僅供範例說明）   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将名称粘贴到相应的字段中。例如， `https://ims-na1.adobelogin.com/`
（伺服器名稱僅供範例說明）

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   整合詳細資訊頁面 — JWT索引標籤

1. **[!UICONTROL API 密钥]** - 返回到“集成详细信息”页面。選取 **[!UICONTROL 概觀]** 標籤，然後前往右側 **[!UICONTROL API金鑰（使用者端ID）]** 欄位，選取 **[!UICONTROL 複製]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   整合詳細資訊頁面。

1. **[!UICONTROL 客户端密钥]** - 返回到“集成详细信息”页面。從 **[!UICONTROL 概觀]** 索引標籤，選取 **[!UICONTROL 擷取使用者端密碼]**. 右側 **[!UICONTROL 使用者端密碼]** 欄位，選取 **[!UICONTROL 複製]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

1. **[!UICONTROL 裝載]**  — 返回「整合詳細資訊」頁面。 從 **[!UICONTROL JWT]** 索引標籤中的「JWT裝載」欄位，複製整個JSON物件程式碼。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将代码粘贴到相应的字段中。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   整合詳細資訊頁面 — JWT索引標籤

   「帳戶」頁面（已填寫所有欄位）看起來類似以下內容：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. 在右上角附近 **[!UICONTROL 帳戶]** 頁面，選取 **[!UICONTROL 建立]**.

   設定Experience Manager IMS後，您現在有新的IMSAccount列在下 **[!UICONTROL Adobe IMS設定]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 設定Experience Platform標籤雲端以進行整合 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在Experience Manager author的左上角附近，選取 **[!UICONTROL 工具]** 圖示（槌子），然後前往 **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform標籤設定]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 於 **[!UICONTROL Experience Platform標籤設定]** 頁面，在左側面板中，選取您要套用Experience Manager標籤設定的Experience Platform網站。

   僅供範例使用， **`We.Retail`** 已選取以下熒幕擷圖中的網站。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在頁面的左上角附近，選取 **[!UICONTROL 建立]**.
1. 於 **[!UICONTROL 一般]** 第頁（1/3頁），共 **[!UICONTROL 建立Experience Platform標籤設定]** 視窗中，填寫下列欄位：

   * **[!UICONTROL 標題]**  — 輸入描述性設定標題。 例如：`We.Retail Tags cloud configuration`。

   * **[!UICONTROL 關聯的Adobe IMS設定]**  — 選取您先前在中建立的IMS設定 [設定Experience ManagerIMS](#configuring-aem-ims).

   * **[!UICONTROL 公司]**  — 從 **[!UICONTROL 公司]** 從下拉式清單中，選取您的Experience Cloud公司。 清單會自動填入。

   * **[!UICONTROL 屬性]**  — 從「屬性」下拉式清單中，選取您先前建立的Experience Platform標籤屬性。 清單會自動填入。
   完成所有欄位後，您的 **[!UICONTROL 一般]** 頁面外觀如下：

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，選取 **[!UICONTROL 下一個]**.
1. 於 **[!UICONTROL 分段]** 頁面（2/3頁）/ **[!UICONTROL 建立Experience Platform標籤設定]** 視窗中，填寫下列欄位：

   在 **[!UICONTROL 資料庫URI]** （統一資源識別碼）欄位，檢查Experience Platform標籤程式庫的測試版本位置。 Experience Manager會自動填入此欄位。

   此步驟使用部署至Experience PlatformCDN的Adobe標籤程式庫（僅供範例用途）。

   >[!NOTE]
   >
   >檢查以確定自動填入的資料庫URI （統一資源識別碼）的格式不正確。 如有必要，請修正此錯誤，使URI代表通訊協定相對URI。 也就是說，它從雙正斜線開始。
   >
   >
   >例如：`//assets.adobetm.com/launch-xxxx`。

   您的 **[!UICONTROL 分段]** 頁面可能會顯示類似下列內容。 此 **[!UICONTROL 封存]** 和 **[!UICONTROL 非同步載入程式庫]** 選項包括 ***not*** 設定：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，選取 **[!UICONTROL 下一個]**.
1. 於 **[!UICONTROL 生產]** 頁面（3/3頁）/ **[!UICONTROL 建立Experience Platform標籤設定]** 視窗，視需要修正自動填入的生產URI，就像先前操作一樣 **[!UICONTROL 分段]** 頁面。
1. 在右上角附近，選取 **[!UICONTROL 建立]**.

   您的新Experience Platform標籤雲端設定現已建立，並列於您的網站旁邊，類似於以下範例：

1. 選取您的新Experience Platform標籤雲端設定（選取時，設定標題左側會出現核取標籤）。 在工具列上，選取 **[!UICONTROL 發佈]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，Experience Manager作者不支援將Dynamic Media檢視器與Experience Platform標籤整合。

但是，Experience Manager發佈節點支援此功能。 使用Experience Platform標籤雲端設定的預設設定，Experience Manager發佈節點會使用Experience Platform標籤的生產環境。 因此，每次測試期間，都必須將Experience Platform標籤程式庫更新從開發推送至生產環境。

您可以繞過此限制。 在上述Experience Manager發佈節點的Experience Platform標籤雲端設定中，指定Platform標籤程式庫的開發或預備URL。 這麼做會使Experience Manager發佈節點使用Experience Platform標籤程式庫的開發或測試版本。

另請參閱 [透過以下方式將Experience Manager與Experience Platform標籤整合 [!DNL Adobe Developer Console]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html) 有關設定Experience Platform標籤雲端設定的詳細資訊。
