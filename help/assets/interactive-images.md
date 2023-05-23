---
title: 互動式影像
description: 瞭解如何在Dynamic Media中使用互動式影像
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: Interactive Images
role: User, Admin
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4275'
ht-degree: 1%

---

# 互動式影像{#interactive-images}

您可以將「可購物」熱點拖放至影像上，輕鬆讓靜態影像豐富，吸引客戶體驗。 可購物熱點結合有關產品或服務的其他資訊與直接的銷售點「加入購物車」或「購買」功能。 客戶可以選取這些熱點並直接連結至產品或服務、將其新增至購物車，或連結至網頁。 這類直接體驗會增加客戶參與度和您網站上的轉換率。

以下是具有「快速檢視」快顯視窗的可購物橫幅。 使用者可透過選取模型上的圓形或「熱點」來啟動快速檢視。

![chlimage_1-152](assets/chlimage_1-368.png)

請前往下列網址，檢視互動式影像在上述網頁上的運作中：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 觀看互動式影像橫幅的建立方式 {#watch-how-interactive-image-banners-are-created}

在上播放逐步解說 [如何建立互動式影像橫幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) （10分33秒）。 您也會瞭解如何預覽、編輯及傳遞互動式影像橫幅。

## 快速入門：互動式影像 {#quick-start-interactive-images}

下列逐步工作流程說明可協助您在Adobe Experience Manager Assets中快速啟動並執行互動式影像。

尋找 **範例** 部分快速入門任務中的標題。 此教學課程內容簡短，以下列尚未新增互動影像的網頁範例為基礎：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

本教學課程有助於說明在您的網站上整合互動式影像的步驟。

互動式影像步驟：

1. **（可選）識別熱點變數**  — 如果您單獨使用Experience Manager Assets和Dynamic Media，請先識別現有Quickview實作中使用的動態變數。 之後，您就可以在建立互動式影像時輸入熱點資料。 另請參閱 [（可選）識別熱點變數](#optional-identifying-hotspot-variables).
不過，如果您使用Adobe Experience Manager Sites或Adobe Experience Manager電子商務，或兩者都使用，則不需要執行此步驟。
另請參閱 [Experience Manager Assets中的電子商務概念](/help/commerce/cif-classic/administering/concepts.md).

1. **（可選）建立互動式影像檢視器預設集**  — 自訂用來表示熱點的圖形影像。 如果您打算使用現成的互動影像檢視器預設集，則不需要建立自己的互動影像檢視器預設集，該預設集名為 `Shoppable_Banner` 而非。
另請參閱 [（可選）建立互動式影像檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **上傳影像橫幅**  — 上傳您想要互動的影像橫幅。
另請參閱 [上傳影像橫幅](#uploading-an-image-banner).

1. **將熱點新增至影像橫幅**  — 新增一或多個熱點至影像橫幅，並將每個熱點與超連結、快速檢視或體驗片段等動作建立關聯。 新增熱點後，您就可以發佈互動式影像來完成這項工作。

   * 另請參閱 [將熱點新增至影像橫幅](#adding-hotspots-to-an-image-banner).
   * 另請參閱 [預覽互動式影像](#optional-previewing-interactive-images)  — 選擇性。 如有需要，您可以檢視可購物橫幅的呈現方式，並測試其互動性。
   * 另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md) 以取得如何發佈互動式影像資產的詳細資訊。

1. **新增互動式影像至您的網站**  — 如果您使用Experience Manager Sites或eCommerce （或兩者），可以將互動式影像以Experience Manager新增至網頁。 將互動式媒體元件拖曳至頁面上。 另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

   如果您使用Experience Manager Assets和Dynamic Media獨立版，您必須複製網站上的內嵌程式碼，然後將其與現有的快速檢視整合。 另請參閱 [將互動式影像與您的網站整合](#integrating-an-interactive-image-with-your-website).

   如果您使用協力廠商WCM （Web內容管理員），您必須將新的互動式視訊與網站上使用的現有Quickview實作整合。 另請參閱 [將互動式影像與現有的快速檢視整合](#integrating-an-interactive-image-with-an-existing-quickview).

## （可選）識別熱點變數 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>只有符合下列條件時，才需要執行此工作：
>
>* 您想要藉由觸發至「快速檢視」，將互動性新增至影像。
>* 您實作的Experience Manager可以 *not* 使用電子商務整合架構，將產品資料從任何電子商務解決方案(例如IBM®WebSphere®Commerce、Elastic Path、hybris或Intershop)提取至Experience Manager。 另請參閱 [Experience Manager Assets中的電子商務概念](/help/commerce/cif-classic/administering/concepts.md).
>
>如果您的Experience Manager實作使用電子商務，您可以略過此任務並繼續下一項任務。

首先，請識別您現有Quickview實作所使用的動態變數，以便您可以輸入熱點資料來建立互動式影像。

在Experience Manager Assets中將熱點新增至橫幅影像時，您必須將SKU （庫存單位）和選用的其他變數指派至每個熱點。 這類熱點變數稍後會用於比對熱點與Quickview內容。

請務必正確識別要與熱點資料產生關聯的變數數量和型別。 新增至橫幅影像的每個熱點都必須攜帶足夠的資訊，以明確識別現有後端系統中的產品。

有不同的方法可識別一組變數，以用於熱點資料。

有時只要諮詢負責現有Quickview實作的IT專家就足夠了。 IT專家可能會知道在系統中識別Quickview所需的最小資料集為何。 但是，也可以只分析前端計畫碼的現有行為。

大部分的「快速檢視」實作都使用下列範例：

* 用户在网站上激活用户界面元素。例如，選取「快速檢視」按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入Quickview資料或內容。
* 快速檢視資料會轉譯成內容，以準備在網頁上呈現。
* 最後，前端程式碼會在畫面上以視覺化方式呈現此類內容。

接著，方法就是造訪已實作「快速檢視」功能的現有網站的不同區域。 然後您觸發Quickview，並擷取網頁傳送的Ajax URL以載入Quickview資料或內容。

通常您不需要使用任何專門的偵錯工具。 現代的網頁瀏覽器提供可完成適當工作的網頁檢查工具。 以下是一些包含網頁檢查器的網頁瀏覽器範例：

* 若要在Google Chrome中檢視所有傳出的HTTP請求，請按F12開啟「開發人員工具」面板，然後選取「網路」索引標籤。
在Mac上，按Command+Option+I開啟「開發人員工具」面板，然後選取「網路」標籤。

* 在Firefox中，您可以按下F12並使用其「網路」標籤來啟動Firebug外掛程式，或使用內建的「偵測器」工具及其「網路」標籤。
在Mac上，按Command+Option+I開啟「開發人員工具」面板，然後選取「檢測器」索引標籤。

在瀏覽器中開啟網路監視時，會觸發頁面上的快速檢視。

現在，請在網路記錄檔中找到Quickview Ajax URL，並複製記錄的URL以供日後分析。 通常，當您觸發「快速檢視」時，會有許多要求傳送至伺服器。 通常，快速檢視Ajax URL是清單中的第一個專案。 它具有複雜的查詢字串部分或路徑，並且其回應MIME型別是 `text/html`， `text/xml`，或 `text/javascript`.

在此過程中，請務必使用不同的產品類別和型別，造訪您網站的不同區域。 原因在於「快速檢視」URL可以包含指定網站類別的共同部分，但只有在您造訪網站的其他區域時才會變更。

最簡單的情況是，快速檢視URL中的唯一變數部分是產品SKU。 在此情況下，SKU值是您將熱點新增至橫幅影像時唯一需要的資料片段。

不過，在複雜的情況下，除了SKU之外，「快速檢視URL」還有不同的變數元素，例如類別ID、顏色代碼和大小代碼。 在這種情況下，在Experience Manager Assets的可購物互動影像功能中，每個元素在熱點資料定義中都是一個單獨的變數。

請考量下列快速檢視URL範例及其產生的熱點變數：

<table>
  <tbody>
  <tr>
    <td><p>單一SKU，可在查詢字串中找到。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中的唯一變數部分是productId=查詢字串引數的值，這顯然是SKU值。 因此，您的熱點只需要填入如下值的SKU欄位 <strong><code>866558</code></strong>， <strong><code>1196184</code></strong>， <strong><code>1081492</code></strong>， <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>在URL路徑中找到單一SKU。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，並成為熱點的SKU值： <strong><code>6422350843</code></strong>， <strong><code>1607745002</code></strong>， <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別識別碼。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU會儲存在 <code>prodId</code> 引數和類別ID<code></code> 儲存在 <code>category=</code> 引數。</p> <p>因此，熱點定義是配對。 即SKU值和名為的額外變數 <code>categoryId</code>. 產生的配對如下：</p>
    <ul>
      <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>.</p> </li>
      <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

您可以將上述三個範例中所使用的方法套用至示範網頁：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

示範網頁具有多個產品縮圖，每個縮圖都有一個標示為「檢視更多」的「快速檢視」按鈕。 當您仍啟動網頁瀏覽器的偵錯工具時，請選取每個按鈕並記下錄製的「快速檢視」URL。 啟用頁面上可用的所有四個產品快速檢視後，您會看到向後端發出的快速檢視請求清單，如下所示：

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

檢視伺服器呼叫，您會發現要求路徑中只會出現產品特定資訊。 您也注意到根本不會使用查詢字串，而且其中涉及兩種不同型別的資料片段：

* 第一個型別是「男性」或「女性」。 您可以將此區段稱為「產品類別」。
* 第二個型別是產品名稱，例如CamoPullover。 您可以假設此資訊是產品SKU。

根據此資訊，整個快速檢視URL的模式如下：

`/datafeed/$categoryId$-$SKU$.json`

根據此類分析，您應使用 `categoryId` 和 `SKU` 用於熱點。

您現在可以使用Experience Manager Assets中的可購物互動影像功能，上傳影像橫幅及新增熱點。

## （可選）建立互動式影像檢視器預設集 {#optional-creating-an-interactive-image-viewer-preset}

您可以選擇使用預設的現成互動式影像檢視器預設集，稱為 `Shoppable_Banner` Experience Manager Assets隨附的其他功能。 或者，您也可以建立自己的自訂檢視器預設集，以用於互動式影像。

建立自訂互動式影像檢視器預設集時，您可以決定影像橫幅上的熱點外觀。 在建立檢視器預設集時，您可以選擇使用來自預先定義影像庫的熱點圖形。

儲存檢視器預設集後，它就會在Experience Manager Assets的「檢視器預設集」清單頁面上自動啟動（開啟）。 這項功能表示只要您檢視資產，互動媒體元件中都能看到這項功能。 但是，到 *deliver* 此檢視器預設集的互動式橫幅，您必須 *發佈* 您的檢視器預設集也是。 此規則適用於自訂或現成可用的檢視器預設集。

**若要建立互動式影像檢視器預設集：**

1. 在左側邊欄中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 在頁面的右上角附近，選取 **[!UICONTROL 建立]**.
1. 在「新增檢視器預設集」對話方塊中，輸入描述互動式橫幅檢視器預設集的名稱。

   儲存後，標題會顯示在「檢視器預設集」清單頁面中。

1. 在“富媒体类型”下拉菜单中，选择&#x200B;**[!UICONTROL 交互式图像]**。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在「編輯檢視器預設集」頁面上，選取 **[!UICONTROL 外觀]** 標籤。
1. 执行下列操作之一：

   * 若要上傳您想要用於影像的熱點影像，請選取「資產選取器」圖示。 在「選取內容」頁面中，導覽至您要使用的熱點影像，選取熱點影像，然後選取右上角的「勾號」圖示。
   * 若要選取預先定義的熱點影像，請選取「熱點庫」圖示。 在熱點相簿調色盤上，選取您要使用的熱點影像。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.

   請確定您發佈新的檢視器預設集。

   另請參閱 [發佈您已新增的檢視器預設集](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   您現在已準備好上傳影像橫幅。

## 上傳影像橫幅 {#uploading-an-image-banner}

如果您已上傳要使用的影像，請繼續進行下一個步驟， [新增熱點至影像橫幅](#adding-hotspots-to-an-image-banner).

**若要上傳影像橫幅：**

1. 上傳您想要互動的影像橫幅。

   另請參閱 [正在上傳資產](/help/assets/manage-assets.md#uploading-assets).

   您現在已準備好將熱點新增至影像橫幅；請參閱下方的下一個工作。

## 將熱點新增至影像橫幅 {#adding-hotspots-to-an-image-banner}

您可以使用「熱點管理」頁面上的編輯器，將熱點新增至影像橫幅。

新增熱點時，可將熱點定義為「快速檢視」彈出式顯示、超連結或體驗片段。

另請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>將檢視器嵌入體驗片段時，不支援互動式影像中的社群媒體分享工具。 若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。

在您目前的建立/編輯工作階段期間，支援頁面右上角附近的「還原」和「重做」選項。

當您完成互動式影像的建立時，可以使用「預覽」來檢視向客戶呈現互動式影像的方式。

另請參閱 [（可選）預覽互動式影像](#optional-previewing-interactive-images).

>[!NOTE]
>
>當您將熱點新增至互動式影像或轉盤橫幅中的影像時，熱點資訊會儲存在相同的中繼資料位置。 該位置是相對於影像的位置，無論該影像是互動式影像還是輪播橫幅。 這項功能表示您可以在任一檢視器中輕鬆重複使用相同的影像，及其定義的熱點資料。
轉盤橫幅支援影像上也可能包含熱點的影像地圖，互動式影像則否。 如果您打算建立使用相同影像的互動式影像或輪播橫幅，請記住此規則。 您可以使用相同影像的個別復本，建立互動式影像和輪播橫幅。
另請參閱 [輪播橫幅](/help/assets/carousel-banners.md).

>[!NOTE]
如果您使用熱點編輯互動式影像並裁切影像，則會移除熱點。

**若要新增熱點至影像橫幅：**

1. 在「資產」檢視中，導覽至您要產生互動式效果的影像橫幅。
1. 执行下列操作之一：

   * 暫留在影像上，然後選取 **[!UICONTROL 選取]** （勾選圖示）。 在工具列上，選取 **[!UICONTROL 編輯]**.

   * 暫留在影像上，然後選取 **[!UICONTROL 更多動作]** （三點圖示） **[!UICONTROL 編輯]**.

   * 選取影像，以便在「詳細資料檢視」頁面中將其開啟。 在工具列上，選取 **[!UICONTROL 編輯]**.

1. 在頁面的左上角附近，選取 **[!UICONTROL 新增熱點]** （手指點選圖示）以開啟「熱點」管理頁面。
1. 在頁面的左上角附近，選取 **[!UICONTROL 熱點]**.

   1. 在「熱點管理」頁面的左上角附近，選取「 」 **[!UICONTROL 熱點]**.
   1. 在影像上，選取您要熱點出現的位置。 如有必要，可拖动热点以调整其位置。
   1. 重複步驟a和b，視需要新增其他熱點。
   1. （可選）若要刪除熱點，請在影像上選取它，然後選取 **[!UICONTROL 刪除]** （垃圾桶圖示），在 **[!UICONTROL 熱點]** 標題。

1. 在「名稱」文字欄位中，輸入連結區的名稱。 此名稱也會顯示在選取的熱點下拉式清單中。
1. 执行下列操作之一：

   * 選取 **[!UICONTROL 快速檢視]**.

      * 如果您是Experience Manager Sites或電子商務客戶，請選取「產品選擇器」圖示（放大鏡）以開啟「選取產品」頁面。 選取您要使用的產品，然後選取 **[!UICONTROL 選取]** ，以便返回「熱點」管理頁面。
      * 如果您是 *not* Experience Manager Sites或電子商務客戶

         * 另請參閱 [識別熱點變數](#optional-identifying-hotspot-variables)；您必須定義這些變數。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU （庫存單位），這是您提供的每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入快速檢視範本的變數部分，讓系統知道將選取的熱點與特定SKU的快速檢視建立關聯。
         * （選擇性）如果快速檢視中有其他變數您必須用來進一步識別產品，請選取 **[!UICONTROL 新增一般變數]**. 在文字欄位中，指定額外的變數。 例如， `category=Males` 是新增的變數。
   * 選取 **[!UICONTROL 超連結]**.

      * 如果您是Experience Manager Sites客戶，請選取「網站選擇器」圖示（資料夾）以導覽至URL。 如果您的互動式內容具有具有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
      * 如果您是獨立客戶，請在HREF文字欄位中指定連結網頁的完整URL路徑。

   請務必指定要在新的瀏覽器分頁（建議的預設值）或相同的分頁中開啟連結。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md) 以取得詳細資訊。

   * 選取 **[!UICONTROL 體驗片段]**.

      * 如果您是Experience Manager Sites客戶，請選取「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 選取您要使用的體驗片段，然後選取 **[!UICONTROL 選取]** ，以便返回「熱點」管理頁面。
另請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md).

      * 指定您希望體驗片段在橫幅上顯示的寬度和高度。

         >[!NOTE]
         將檢視器嵌入體驗片段時，不支援互動式影像中的社群媒體分享工具。 若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。



1. 選取 **[!UICONTROL 儲存]** 以儲存您的工作並返回「瀏覽」頁面。
1. 發佈互動式影像。 發佈可讓您透過雲端傳遞橫幅，也可在您需要與協力廠商網站整合時產生內嵌程式碼。

   另請參閱 [發佈資產](/help/assets/manage-assets.md#publishing-assets).

   新增熱點並發佈互動式影像後，您現在就可以將其新增至現有網站了。

   另請參閱 [將互動式影像與您的網站整合](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   如果您使用熱點編輯互動式影像並裁切影像，則會刪除您的熱點。

### （可選）預覽互動式影像 {#optional-previewing-interactive-images}

您可以使用「預覽」來檢視向客戶呈現互動式影像的方式，以及測試影像的熱點以確保其如預期般運作。

當您對互動式影像感到滿意時，可以發佈該影像。
另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
另請參閱 [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容具有具有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

**若要預覽互動式影像：**

1. 在「資產」檢視中，導覽至您已建立的現有互動式影像，並選取以在「預覽」中開啟。
1. 在「預覽」頁面的左上角附近，從「內容」下拉式清單中選取 **[!UICONTROL 檢視者]**.
1. 在「檢視器」清單中，選取 **[!UICONTROL Shoppable_Banner]** 或您已建立的互動式影像檢視器預設集名稱。
1. 如果您要測試其相關動作，請選取影像上的熱點。

## 發佈互動式影像資產 {#publishing-interactive-image-assets}

另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md) 以取得如何發佈互動式影像資產的詳細資訊。

## 將互動式影像與您的網站整合 {#integrating-an-interactive-image-with-your-website}

上傳橫幅影像、將熱點新增至影像，並發佈互動式影像後，您就可以將其新增至網站頁面了。

如果您是Experience Manager Sites客戶，您可以將互動式媒體元件拖曳至頁面上，以新增互動式影像。 另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

如果您是獨立Experience Manager Assets客戶，您可以依照本節所述，手動將互動式影像新增至您的網站。

1. 複製已發佈的互動式影像的內嵌程式碼。
另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).

1. 將複製的內嵌程式碼新增至網頁內所需的位置。
複製的內嵌程式碼是為回應式環境所設定，因此會自動符合指派的區域。

**示例**

以示範網站為例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

請注意，這三名男性的圖片是靜態的 `IMG` 標籤：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

整合就像移除 `IMG` 標籤並將其取代為從Experience Manager Assets複製的內嵌程式碼。 您可在下列URL中看到結果，該URL會在具有三個圓形熱點的頁面上顯示可購物互動影像：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
此時，示範網站可購物互動影像上的熱點僅供顯示；尚未與現有的Quickview整合。

若要針對回應式環境將「裁切」套用至可購物互動影像，您可以包含互動影像設定屬性 `ZoomView.iscommand` 至路徑。 元件 `ZoomView` 稱為和 `iscommand` 是您套用的「裁切」影像伺服命令。

另請參閱 [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 設定屬性。

另請參閱 [裁切](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) 影像伺服命令。

您現在已準備好將互動式影像與網站上現有的快速檢視整合。

## 將互動式影像與現有的快速檢視整合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
此工作僅適用於獨立Experience Manager Assets客戶。

此程式的最後一步是將互動式影像與網站上現有的快速檢視實作整合。 整合沒有適用於所有情況的解決方案。 每個Quickview實作都是獨一無二的，而且需要特定方法。 這可能需要前端IT人員的協助。

現有的「快速檢視」實作通常代表一連串在網頁上發生的相互關聯動作，順序如下：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1所觸發的使用者介面元素來取得快速檢視URL。
1. 前端計畫碼會使用步驟2中取得的URL傳送Ajax請求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入Quickview資料或內容。
1. 前端程式碼可選擇性將載入的快速檢視資料轉換為HTML表示法。
1. 前端程式碼會顯示強制回應對話方塊或面板，並在畫面上為一般使用者呈現HTML內容。

這些呼叫不代表網頁邏輯可從任意步驟呼叫的獨立公用API呼叫。 而是鏈結式呼叫，每個下一個步驟都隱藏在上一個步驟的最後一個階段（回呼）中。

同時，可購物互動影像正在取代步驟1和部分步驟2，當使用者選擇可購物影像內的熱點時，此類使用者互動由檢視器處理。 檢視器會將事件傳回至包含先前新增至Experience Manager Assets之所有熱點資料的網頁。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 聆聽可購物互動影像所發出的事件。
* 根據熱點資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在畫面上呈現以供顯示的程式。

Experience Manager Assets傳回的內嵌程式碼已有備註的現成可用事件處理常式，如下列醒目提示的程式碼片段所示：

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

因此，只需取消註解程式碼，並將虛擬處理常式主體取代為特定網頁專用的程式碼。

建構快速檢視URL的程式與用來識別先前涵蓋之熱點變數的程式相反。

另請參閱 [識別熱點變數](#optional-identifying-hotspot-variables).

使用先前的快速檢視URL範例，您可以檢視下列範例，瞭解快速檢視URL在各種情況下的建構方式：

<table>
 <tbody>
  <tr>
   <td><p>單一SKU，可在查詢字串中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>單一SKU，可在URL路徑中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>查詢字串中的SKU和類別ID</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

觸發「快速檢視」URL和啟動「快速檢視」面板的最後一個步驟，很可能需要您IT部門的前端IT人員的協助。 他們深知如何透過適當的步驟正確觸發快速檢視實施，並擁有現成的快速檢視URL。

您可以檢視這些步驟如何套用至示範網站，以將可購互動影像與快速檢視程式碼完全整合。 之前，快速檢視URL的結構識別如下：

```xml
/datafeed/$categoryId$-$SKU$.json
```

若要在內部重新建構此URL `quickViewActivate` 處理常式，您可以使用 `categoryId` 和 `SKU` 中的可用欄位 `inData` 檢視器程式碼傳遞至處理常式的物件：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站正在使用簡單的「 」觸發「快速檢視」對話方塊 `loadQuickView()` 函式呼叫。 此函式僅接受一個引數，即快速檢視資料URL。 因此，整合可購物互動影像的最後一步是將下列程式碼行新增至 `quickViewActivate` 處理常式：

```xml
loadQuickView(quickViewUrl);
```

以下是完整的原始程式碼：

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

具備完全整合互動式影像的最終示範網站看起來如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)

## 使用快速檢視建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

另請參閱 [使用Quickview建立自訂快顯視窗](/help/assets/custom-pop-ups.md).
