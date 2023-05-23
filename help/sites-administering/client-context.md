---
title: ClientContext
seo-title: Client Context
description: 瞭解如何在AEM中使用Client Context。
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: 02afc4eb78acaacc40d3ba1830ccb1e9c3907d0f
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 0%

---

# ClientContext{#client-context}

>[!NOTE]
>
>ContextHub已取代Client Context。 如需詳細資訊，請參閱相關 [設定](/help/sites-developing/ch-configuring.md) 和 [開發人員](/help/sites-developing/contexthub.md) 檔案。

Client Context是一種機制，可向您提供有關目前頁面和訪客的特定資訊。 可使用下列方式開啟它： **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)：

![](assets/clientcontext_alisonparker.png)

在 [它會顯示資訊的發佈和作者環境](#propertiesavailableintheclientcontext) 關於：

* 訪客；根據您的執行個體，會要求或衍生某些資訊。
* 頁面標籤以及目前訪客存取這些標籤的次數（這會在您將滑鼠移到特定標籤上時顯示） 。
* 頁面資訊。
* 技術環境的相關資訊；例如IP位址、瀏覽器和熒幕解析度。
* 目前解析的任何區段。

圖示（僅適用於作者環境）可讓您設定使用者端內容的詳細資訊：

![](do-not-localize/clientcontext_icons.png)

* **編輯**
將會開啟一個新頁面，讓您可以 [編輯、新增或移除設定檔屬性](#editingprofiledetails).

* **載入**
您可以 [從設定檔清單中選取並載入設定檔](#loading-a-new-user-profile) 您想要測試。

* **重設**
您可以 [重設設定檔](#resetting-the-profile-to-the-current-user) 與目前使用者的相同。

## 可用的使用者端內容元件 {#available-client-context-components}

Client Context可顯示下列屬性([根據使用「編輯」選取的內容](#adding-a-property-component))：

**瀏覽者資訊** 顯示下列使用者端資訊：

* 此 **ip位址**
* **關鍵字** 用於搜尋引擎轉介
* 此 **瀏覽器** 正在使用
* 此 **作業系統** （作業系統）使用中
* 畫面 **解析度**
* 此 **滑鼠X** position
* 此 **滑鼠Y** position

**活動資料流** 這可提供使用者在各種平台(例如AEM論壇、部落格、評分等)上的社交活動相關資訊。

**Campaign** 可讓作者模擬行銷活動的特定體驗。 此元件會覆寫一般的促銷活動解析度和體驗選擇，以啟用各種置換的測試。

行銷活動的解析度通常以行銷活動的優先順序屬性為基礎。 通常會根據細分來選取體驗。

**購物車** 顯示購物車資訊，包括產品專案（標題、數量、價格格式等）、已解決的促銷活動（標題、訊息等） 和憑單（代碼、說明等）。

購物車工作階段存放區也會使用ClientContextCartServlet將已解決的促銷活動變更（根據分段變更）通知伺服器。

**通用存放區** 是顯示存放區內容的一般元件。 這是一般存放區屬性元件的較低層級版本。

Generic Store必須設定有JS轉譯器，以自訂方式顯示資料。

**一般存放區屬性** 是顯示存放區內容的一般元件。 這是一般存放區元件的較高層級版本。

「一般存放區屬性」元件包含預設轉譯器，其列出已設定的屬性（連同縮圖）。

**地理位置** 顯示使用者端的經緯度。 它會使用HTML5地理位置API在瀏覽器中查詢目前位置。 這會向訪客顯示快顯視窗，瀏覽器會詢問訪客是否同意共用其位置。

在Context Cloud中顯示時，元件會使用Google API將地圖顯示為縮圖。 元件受Google API限制 [使用量限制](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>在AEM 6.1中，地理位置存放區不再提供反向地理編碼功能。 因此，地理位置存放區不會再擷取有關目前位置的詳細資訊，例如城市名稱或國家/地區代碼。 使用此存放區資料的區段將無法正常運作。 地理位置存放區僅包含位置的經緯度。

**JSONP存放區** 顯示與安裝相依之內容的元件。

JSONP標準是JSON的補充功能，可讓您規避相同原始原則（使網頁應用程式無法與其他網域上的伺服器通訊）。 它包含於包裝JSON物件於函式呼叫中，以便能夠將其載入為 `<script>` 來自其他網域（這是相同來源原則的允許例外）。

JSONP存放區與其他存放區類似，但會載入來自其他網域的資訊，而不需要在目前網域上為該資訊擁有Proxy。 請參閱中的範例 [透過JSONP在Client Context中儲存資料](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>JSONP存放區不會快取Cookie中的資訊，但會在每次頁面載入時擷取該資料。

**設定檔資料** 顯示使用者設定檔中收集的資訊。 例如，性別、年齡、電子郵件地址等。

**已解析的區段** 顯示目前解析的區段（通常取決於使用者端內容中顯示的其他資訊）。 這在設定行銷活動時是有意義的。

例如，滑鼠目前是在視窗的左手或右手部分上方。 此區段主要用於測試，因為可以立即看到變更。

**社交圖** 顯示使用者的朋友和關注者的社交圖。

>[!NOTE]
>
>目前這是示範功能，需要仰賴示範使用者設定檔節點上預先設定的資料集。 例如，請參閱：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => friends屬性

**標籤雲** 顯示在目前頁面上設定的標籤以及瀏覽網站時收集的標籤。 將滑鼠移到標籤上會顯示目前使用者存取包含該特定標籤的頁面的次數。

>[!NOTE]
在造訪的頁面上顯示的DAM資產上設定的標籤不會計算在內。

**Technographics商店** 此元件取決於您的安裝。

**已檢視的產品** 追蹤購物者已檢視的產品。 可查詢最近檢視的產品或未在購物車中的最近檢視的產品。

此工作階段存放區沒有預設的使用者端內容元件。

如需詳細資訊，請參閱 [詳細的使用者端內容](/help/sites-developing/client-context.md).

>[!NOTE]
頁面資料不再在使用者端內容中作為預設元件。 如有需要，您可以編輯使用者端內容、新增 **一般存放區屬性** 元件，然後設定以定義 **儲存** 作為 `pagedata`.

## 變更使用者端內容設定檔 {#changing-the-client-context-profile}

「使用者端內容」可讓您以互動方式變更詳細資訊：

* 變更Client Context中使用的設定檔，可讓您檢視不同使用者在目前頁面上會看到的不同體驗。
* 除了變更使用者設定檔之外，您還可以變更一些設定檔詳細資料，以檢視頁面體驗在各種條件下的差異。

### 正在載入新的使用者設定檔 {#loading-a-new-user-profile}

您可以透過以下任一方式變更設定檔：

* [使用載入圖示](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用選取範圍滑桿](#loadinganewvisitorprofilewiththeselectionslider)

完成後，您可以 [重設設定檔](#resetting-the-profile-to-the-current-user).

#### 使用載入設定檔圖示載入新訪客設定檔 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 按一下「載入設定檔」圖示：

   ![](do-not-localize/clientcontext_loadprofile.png)

1. 這將開啟對話方塊，您可以在此處選取要載入的設定檔：

   ![](assets/clientcontext_profileloader.png)

1. 按一下 **確定** 以載入。

#### 使用選取範圍滑桿載入新的使用者設定檔 {#loading-a-new-user-profile-with-the-selection-slider}

您也可以使用選取範圍滑桿來選取設定檔：

1. 連按兩下代表目前使用者的圖示。 選取器將會開啟，使用箭頭來導覽並檢視可用的設定檔：

   ![](assets/clientcontext_profileselector.png)

1. 按一下要載入的設定檔。 載入詳細資料後，按一下選取器外部以關閉。

#### 將設定檔重設為目前使用者 {#resetting-the-profile-to-the-current-user}

1. 使用重設圖示將Client Context中的設定檔傳回至目前使用者的設定檔：

   ![](do-not-localize/clientcontext_resetprofile.png)

### 變更瀏覽器平台 {#changing-the-browser-platform}

1. 連按兩下代表瀏覽器平台的圖示。 選擇器將會開啟、使用箭頭來導覽並檢視可用的平台/瀏覽器：

   ![](assets/clientcontext_browserplatform.png)

1. 按一下您要載入的平台瀏覽器。 載入詳細資料後，按一下選取器外部以關閉。

### 變更地理位置 {#changing-the-geolocation}

1. 連按兩下地理位置圖示。 展開的地圖將會開啟，您可以在此處將標籤拖曳到新位置：

   ![](assets/clientcontext_geomocationrelocate.png)

1. 按一下地圖外部以關閉。

### 變更標籤選取範圍 {#changing-the-tag-selection}

1. 連按兩下Client Context的「標籤雲」區段。 隨即會開啟對話方塊，您可在此處選取標籤：

   ![](assets/clientcontext_tagselection.png)

1. 按一下「確定」以載入使用者端內容。

## 編輯使用者端內容 {#editing-the-client-context}

編輯使用者端內容可用於設定（或重設）特定屬性的值、新增屬性或移除不再需要的屬性。

### 編輯屬性詳細資料 {#editing-property-details}

編輯使用者端內容可用於設定（或重設）某些屬性的值。 這可讓您測試特定情境(對以下專案尤其有用： [細分](/help/sites-administering/campaign-segmentation.md) 和 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md))。

![](assets/clientcontext_alisonparker_edit.png)

### 新增屬性元件 {#adding-a-property-component}

在您開啟 **ClientContext設計頁面**，您也可以 **新增** 使用可用元件的全新屬性（元件會列在sidekick上或清單中）。 **插入新元件** 連按兩下後開啟的對話方塊 **將元件或資產拖曳到這裡** box)：

![](assets/clientcontext_alisonparker_new.png)

### 移除屬性元件 {#removing-a-property-component}

在您開啟 **ClientContext設計頁面**，您也可以 **移除** 屬性（若不再需要）。 這包括現成可用的屬性； **重設** 如果這些專案已移除，則會恢復這些專案。

## 透過JSONP在Client Context中儲存資料 {#storing-data-in-client-context-via-jsonp}

請依照此範例使用JSONP存放區內容存放區元件，將外部資料新增至使用者端內容。 然後，根據該資料中的資訊建立區段。 此範例使用WIPmania.com提供的JSONP服務。 此服務會根據Web使用者端的IP位址傳回地理位置資訊。

此範例使用Geometrixx Outdoors範例網站來存取Client Context並測試建立的區段。 只要頁面已啟用「使用者端內容」，您就可以使用不同的網站。 (請參閱 [新增使用者端內容至頁面](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### 新增JSONP存放區元件 {#add-the-jsonp-store-component}

將JSONP Store元件新增至Client Context，並使用它來擷取和儲存Web使用者端的地理位置資訊。

1. 開啟AEM編寫執行個體上Geometrixx Outdoors網站的英文首頁。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 若要開啟「使用者端內容」，請按Ctrl-Alt-c (windows)或control-option-c (Mac)。
1. 按一下「使用者端內容」頂端的編輯圖示，開啟「使用者端內容設計工具」。

   ![](do-not-localize/chlimage_1.png)

1. 將JSONP存放區元件拖曳至Client Context。

   ![](assets/chlimage_1-4.jpeg)

1. 連按兩下元件以開啟「編輯」對話方塊。
1. 在「JSONP服務URL」方塊中，輸入以下URL，然後按一下「擷取存放區」：

   `https://api.wipmania.com/jsonp?callback=${callback}`

   元件會呼叫JSONP服務並列出傳回資料包含的所有屬性。 清單中的屬性是可在Client Context中使用的屬性。

   ![](assets/chlimage_1-40.png)

1. 单击确定。
1. 返回Geometrixx Outdoors首頁並重新整理頁面。 Client Context現在包含來自JSONP存放區元件的資訊。

   ![](assets/chlimage_1-41.png)

### 建立區段 {#create-the-segment}

使用您使用JSONP存放區元件建立的工作階段存放區中的資料。 區段會使用工作階段存放區的緯度和目前日期，來判斷這是否為使用者端位置的冬季時間。

1. 在網頁瀏覽器中開啟「工具」主控台(`https://localhost:4502/miscadmin#/etc`)。
1. 在資料夾樹狀結構中，按一下「工具/分段」資料夾，然後按一下「新增>新增資料夾」。 指定下列屬性值，然後按一下「建立」：

   * 名稱： mysegments
   * 標題：我的區段

1. 選取「我的區段」資料夾，然後按一下「新增>新增頁面」：

   1. 在「標題」中輸入Winter。
   1. 選取區段範本。
   1. 单击创建。

1. 以滑鼠右鍵按一下Winter區段，然後按一下「開啟」。
1. 將Generic Store屬性拖曳至預設的AND容器。

   ![](assets/chlimage_1-5.jpeg)

1. 連按兩下元件以開啟「編輯」對話方塊，指定下列屬性值，然後按一下「確定」：

   * 商店： wipmania
   * 屬性名稱： latitude
   * 運運算元：大於
   * 屬性值： 30

1. 將Script元件拖曳至相同的AND容器，並開啟其編輯對話方塊。 新增下列指令碼，然後按一下「確定」：

   `3 < new Date().getMonth() < 12`
