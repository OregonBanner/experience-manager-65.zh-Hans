---
title: 使用 Quickview 创建自定义弹出窗口
description: 預設Quickview用於電子商務體驗，顯示快顯視窗和產品資訊，以推動購買。 您可以觸發自訂內容以顯示於快顯視窗中。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Viewers
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: 05af34f8be6a4e32c3488ec05bc0133154caff7f
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 1%

---

# 使用 Quickview 创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

預設Quickview用於電子商務體驗，顯示快顯視窗和產品資訊，以推動購買。 不過，您可以觸發自訂內容以顯示於快顯視窗中。 根據檢視器的不同，此功能可讓使用者在熱點、縮圖影像或影像地圖上選取以檢視資訊或相關內容。

Dynamic Media中的下列檢視器支援快速檢視：

* 互動式影像（可點按的熱點）
* 互動式影片（影片播放期間可點按的縮圖影像）
* 傳送橫幅（可點按的熱點或影像地圖）

雖然每個檢視器的功能不同，但建立快速檢視的程式在所有三個支援的檢視器中都相同。

**若要使用Quickview建立自訂快顯視窗：**

1. 為上傳的資產建立快速檢視。

   您通常會在編輯資產的同時建立快速檢視，以搭配您使用的檢視器使用。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的檢視器</strong></td>
    <td><strong>如果您想要建立快速檢視，請完成這些步驟</strong></td>
    </tr>
    <tr>
    <td>交互式图像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">新增熱點至影像橫幅</a>.</td>
    </tr>
    <tr>
    <td>交互式视频</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">新增互動功能至您的影片</a>.</td>
    </tr>
    <tr>
    <td>传送横幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">新增熱點或影像地圖至橫幅</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 取得檢視器內嵌程式碼，以便在您的網站中整合檢視器。

   <table>
    <tbody>
    <tr>
    <td><strong>您正在使用的檢視器</strong><br /> </td>
    <td><strong>如果您想要將檢視器與您的網站整合，請完成這些步驟</strong></td>
    </tr>
    <tr>
    <td>互動式影像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">將互動式影像與您的網站整合</a>.<br /> </td>
    </tr>
    <tr>
    <td>互動視訊<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">將互動式視訊與您的網站整合</a>.<br /> </td>
    </tr>
    <tr>
    <td>傳送橫幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">新增輪播橫幅至您的網站頁面</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您現在使用的檢視器必須知道如何使用快速檢視。

   檢視器使用名為的處理常式 `QuickViewActive`.

   **範例**
假設您在網頁上將下列範例內嵌程式碼用於互動式影像：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   處理常式會使用載入檢視器 `setHandlers`：

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **以上文的內嵌程式碼範例為例，提供下列程式碼：**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   進一步瞭解 `setHandlers()` 方法：

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 您現在必須設定 `quickViewActivate` 處理常式。

   此 `quickViewActivate` 處理常式會控制檢視器中的快速檢視。 處理常式包含要與Quickview一起使用的變數清單和函式呼叫。 內嵌程式碼提供快速檢視中設定的SKU變數與範例的對應 `loadQuickView` 函式呼叫。

   **變數對應**
將網頁中使用的變數對應至Quickview中包含的SKU值和一般變數：

   `var *variable1*= inData.*quickviewVariable*`

   提供的內嵌程式碼具有SKU變數的範例對應：

   `var sku=inData.sku`

   也從「快速檢視」對應其他變數，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函式呼叫**
處理常式也需要Quickview的函式呼叫才能運作。 假設主機頁面可存取函式。 內嵌程式碼提供範例函式呼叫：

   `loadQuickView(sku)`

   範例函式呼叫會假設函式 `loadQuickView()` 存在且可存取。

   進一步瞭解 `quickViewActivate` 方法：

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 互動式視訊檢視器中的互動式資料支援： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 执行以下操作：

   * 取消註解內嵌程式碼的setHandlers區段。
   * 對應快速檢視中包含的任何其他變數。

      * 更新 `loadQuickView(sku,*var1*,*var2*)` 如果您要新增其他變數，請呼叫。
   * 建立簡單 `loadQuickView` ()在頁面上的功能，在檢視器外。

      例如，下列將SKU的值寫入瀏覽器主控台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 將測試HTML頁面上傳至網頁伺服器並開啟。

      在快速檢視中的變數已對應且函式呼叫已就緒的情況下，瀏覽器主控台會使用提供的範例函式將變數值寫入瀏覽器主控台。



1. 您現在可以使用函式在快速檢視中叫用簡單的快顯視窗。 以下範例使用 `DIV` 用於快顯視窗。
1. 設定快顯視窗的樣式 `DIV` 以下列方式進行。 視需要新增您自己的其他樣式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 放置快顯視窗 `DIV` 在HTML頁面內文中。

   其中一個元素會以ID設定，當使用者叫用快速檢視時，ID會以SKU值更新。 此範例也包含簡單按鈕，可在快顯視窗顯示後再次隱藏快顯視窗。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 新增函式，以便您可以在快顯視窗中更新SKU值；取代步驟5中建立的簡單函式，讓快顯視窗可見。 ，其功能如下：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 將測試HTML頁面上傳至您的網頁伺服器並開啟。 檢視器會顯示快顯視窗 `DIV` 使用者叫用快速檢視時。
1. **如何以全熒幕模式顯示自訂快顯視窗**

   有些檢視器（例如互動式視訊檢視器）支援以全熒幕模式顯示。 不過，如先前步驟所述使用快顯視窗，會在全熒幕模式下顯示在檢視器後面。

   若要讓快顯視窗同時以標準與全熒幕模式顯示，請將快顯視窗附加至檢視器容器。 使用第二個處理常式方法， `initComplete`.

   此 `initComplete` 在檢視器初始化後，會叫用處理常式。

   ```xml
   "initComplete":function() { code block }
   ```

   進一步瞭解 `init()` 方法：

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 若要將前述步驟中所述的快顯視窗附加至檢視器，請使用下列程式碼：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上述程式碼中，已進行下列操作：

   * 已識別自訂快顯視窗。
   * 已將其從DOM移除。
   * 已識別檢視器容器。
   * 已將快顯視窗附加至檢視器容器。

1. 您的整個setHandlers程式碼看起來類似於以下內容（使用了互動式視訊檢視器）：

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 載入處理常式後，您可以初始化檢視器：

   `*viewerInstance.*init()`

   **範例**
此範例使用互動式影像檢視器。

   `s7interactiveimageviewer.init()`

   將檢視器內嵌至主機頁面後，請確定已建立檢視器例項，而且處理常式已在使用叫用檢視器之前載入 `init()`.
