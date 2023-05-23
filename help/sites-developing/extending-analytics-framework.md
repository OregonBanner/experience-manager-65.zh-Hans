---
title: 自訂Adobe Analytics架構
seo-title: Customizing the Adobe Analytics Framework
description: 自訂Adobe Analytics架構
seo-description: null
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 0%

---

# 自訂Adobe Analytics架構{#customizing-the-adobe-analytics-framework}

Adobe Analytics架構會決定使用Adobe Analytics追蹤的資訊。 若要自訂預設架構，您可以使用JavaScript新增自訂追蹤、整合Adobe Analytics外掛程式，以及變更用於追蹤的架構內的一般設定。

## 關於為框架產生的JavaScript {#about-the-generated-javascript-for-frameworks}

當頁面與Adobe Analytics框架相關聯時，且該頁面包含 [Analytics模組的參考](/help/sites-administering/adobeanalytics.md)，系統會自動為頁面產生analytics.sitecatalyst.js檔案。

頁面中的JavaScript會建立 `s_gi`物件( s_code.js Adobe Analytics程式庫所定義)並指派值給其屬性。 物件例項的名稱為 `s`. 本節中提供的程式碼範例對此有數個參考 `s` 變數。

以下範常式式碼類似於analytics.sitecatalyst.js檔案中的程式碼：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

當您使用自訂JavaScript程式碼來自訂架構時，就會變更此檔案的內容。

## 設定Adobe Analytics屬性 {#configuring-adobe-analytics-properties}

Adobe Analytics中有許多預先定義的變數，可在架構上設定。 此 **charset**， **cookieLifetime**， **currencyCode** 和 **trackInlineStats** 變數包含在 **一般Analytics設定** 預設為清單。

![aa-22](assets/aa-22.png)

您可以將變數名稱和值新增至清單。 這些預先定義的變數以及您新增的任何變數，可用來設定 `s` analytics.sitecatalyst.js檔案中的物件。 以下範例說明如何新增 `prop10` 值的屬性 `CONSTANT` 以javascript程式碼表示：

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

使用以下程式將變數新增至清單：

1. 在您的Adobe Analytics架構頁面上，展開 **一般Analytics設定** 區域。
1. 在變數清單下方，按一下「新增專案」以新增變數至清單。
1. 在左側儲存格中輸入變數的名稱，例如 `prop10`.

1. 在右欄中輸入變數的值，例如 `CONSTANT`.

1. 若要移除變數，請按一下變數旁的(-)按鈕。

>[!NOTE]
>
>輸入變數和值時，請確定它們的格式和拼字正確，或者 **將不會傳送呼叫** 具有正確的值/變陣列。 拼錯的變數和值甚至可以防止呼叫發生。
>
>請洽詢您的Adobe Analytics代表，確認這些變數已正確設定。

>[!CAUTION]
>
>此清單中的部分變數為 **強制** 為了讓Adobe Analytics呼叫正確運作， **currencyCode**， **charSet**)
>
>因此，即使將它們從框架本身移除，在進行Adobe Analytics呼叫時仍會附加預設值。

### 將自訂JavaScript新增至Adobe Analytics架構 {#adding-custom-javascript-to-an-adobe-analytics-framework}

中的免費javascript方塊 **一般Analytics設定** 區域可讓您將自訂程式碼新增到Adobe Analytics架構。

![aa-21](assets/aa-21.png)

您新增的程式碼會附加至analytics.sitecatalyst.js檔案。 因此，您可以存取 `s` 變數，此變數是 `s_gi` 在中定義的javascript物件 `s_code.js`. 例如，新增下列程式碼等同於新增變數： `prop10` 值 `CONSTANT`，即上一節中的範例：

`s.prop10= 'CONSTANT';`

中的程式碼 [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) 檔案(包含Adobe Analytics的內容) `s-code.js` file)包含以下程式碼：

`if (s.usePlugins) s.doPlugins(s)`

下列程式示範如何使用javascript方塊來自訂Adobe Analytics追蹤。 如果您的javascript需要使用Adobe Analytics外掛程式， [整合它們](/help/sites-administering/adobeanalytics.md) 進入AEM。

1. 將下列javascript程式碼新增至方塊，以便 `s.doPlugins` 已執行：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >如果您想要在Adobe Analytics呼叫中傳送已自訂的變數，而這些變數無法透過基本拖放介面或透過Adobe Analytics檢視中的內嵌JavaScript完成，則必須使用此程式碼。
   >
   >如果自訂變數在s_doPlugins函式之外，則會在Adobe Analytics呼叫中以*undefined *的形式傳送

1. 將您的JavaScript程式碼新增至 **s_doPlugins** 函式。

下列範例會使用常見的分隔符號「|」，以階層順序串連頁面上擷取的資料。

Adobe Analytics架構有下列設定：

* 此 `prop2` Adobe Analytics變數已對應至 `pagedata.sitesection` 網站屬性。

* 此 `prop3` Adobe Analytics變數已對應至 `pagedata.subsection` 網站屬性。

* 下列程式碼已新增至免費javascript方塊：

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 瀏覽使用框架的網頁時（或在編輯模式中重新載入或預覽頁面），會執行對Adobe Analytics的呼叫。

例如，Adobe Analytics會產生下列值：

![aa-20](assets/aa-20.png)

### 新增所有Adobe Analytics架構的全域自訂程式碼 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

提供整合至所有Adobe Analytics架構的自訂javascript程式碼。 當頁面的Adobe Analytics框架不包含自訂專案時 [自由格式javascript](/help/sites-administering/adobeanalytics.md)，則/libs/cq/analytics/components/sitecatalyst/config.js.jsp指令碼產生的javascript會附加至 [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) 檔案。 根據預設，指令碼沒有作用，因為它已被註解。 程式碼也會設定 `s.usePlugins` 至 `false`：

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

analytics.sitecatalyst.js檔案中的程式碼(包含Adobe Analytics s_code.js檔案的內容)包含下列程式碼：

若為(s.usePlugins) s.doPlugins(s)

因此，您的javascript應將 `s.usePlugins` 至 `true` 如此一來， `s_doPlugins` 函式執行。 若要自訂程式碼，請以使用您自己javascript的檔案覆蓋config.js.jsp檔案。 如果您的javascript需要使用Adobe Analytics外掛程式， [整合它們](/help/sites-administering/adobeanalytics.md) 進入AEM。

>[!NOTE]
>
>請勿編輯/libs/cq/analytics/components/sitecatalyst/config.js.jsp檔案。 某些AEM升級或維護工作可以重新安裝原始檔案，並移除您的變更。

1. 在CRXDE Lite中，建立/apps/cq/analytics/components資料夾結構：

   1. 以滑鼠右鍵按一下/apps資料夾，然後按一下「建立>建立資料夾」。
   1. 指定 `cq` 作為資料夾名稱，然後按一下確定。
   1. 同樣地，建立 `analytics` 和 `components` 資料夾。

1. 以滑鼠右鍵按一下 `components` 資料夾，然後按一下「建立>建立元件」。 指定下列屬性值：

   * 标签: `sitecatalyst`
   * 标题: `sitecatalyst`
   * 超级类型: `/libs/cq/analytics/components/sitecatalyst`
   * 组: `hidden`

1. 重複按一下「下一步」，直到啟用「確定」按鈕，然後按一下「確定」。

   sitecatalyst元件包含自動建立的sitecatalyst.jsp檔案。

1. 以滑鼠右鍵按一下sitecatalyst.jsp檔案，然後按一下刪除。

1. 以滑鼠右鍵按一下sitecatalyst元件，然後按一下「建立>建立檔案」。 指定名稱 `config.js.jsp` 然後按一下「確定」。

   config.js.jsp檔案會自動開啟以進行編輯。

1. 將下列文字新增至檔案，然後按一下「儲存全部」：

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   對於使用Adobe Analytics架構的所有頁面，/apps/cq/analytics/components/sitecatalyst/config.js.jsp指令碼產生的javascript程式碼現在會插入analytics.sitecatalyst.js檔案中。

1. 新增您要在中執行的javascript程式碼 `s_doPlugins` 函式，然後按一下「儲存全部」。

>[!CAUTION]
>
>如果頁面框架的自由格式javascript中出現任何文字（甚至只有空白），則會忽略config.js.jsp。

### 在AEM中使用Adobe Analytics外掛程式 {#using-adobe-analytics-plugins-in-aem}

取得Adobe Analytics外掛程式的JavaScript程式碼，並將它們整合到AEM的Adobe Analytics架構中。 將程式碼新增至類別的使用者端程式庫資料夾 `sitecatalyst.plugins` 以便用於自訂javascript程式碼。

例如，如果您整合 `getQueryParams` 外掛程式，您可從以下位置呼叫外掛程式： `s_doPlugins` 自訂javascript的函式。 以下範常式式碼傳送查詢字串於 **&quot;pid&quot;** 從反向連結URL做為 **EVAR1**，觸發Adobe Analytics呼叫時。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM會安裝下列Adobe Analytics外掛程式，以便在預設情況下可以使用：

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins使用者端程式庫資料夾的sitecatalyst.plugins類別中包含這些外掛程式。

>[!NOTE]
>
>為外掛程式建立新的使用者端程式庫資料夾。 請勿將外掛程式新增至 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 資料夾。 此做法可確保您對 `sitecatalyst.plugins` 在AEM重新安裝或升級工作期間，不會覆寫類別。

使用以下程式，為您的外掛程式建立使用者端程式庫資料夾。 您只需要執行此程式一次。 若要將外掛程式新增至使用者端程式庫資料夾，請使用後續程式。

1. 在網頁瀏覽器中，開啟「CRXDE Lite」。 ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. 以滑鼠右鍵按一下/apps/my-app/clientlibs資料夾，然後按一下「建立>建立節點」。 輸入下列屬性值，然後按一下「確定」：

   * 名稱：使用者端程式庫資料夾的名稱，例如my-plugins

   * 型別： cq：ClientLibraryFolder

1. 選取您剛建立的使用者端程式庫資料夾，並使用右下方的屬性列來新增下列屬性：

   * 名稱：類別
   * 型別：字串
   * 值： sitecatalyst.plugins
   * 多個：已選取

   在「編輯」視窗中按一下「確定」以確認屬性值。

1. 以滑鼠右鍵按一下您剛建立的使用者端資料庫資料夾，然後按一下「建立>建立檔案」。 檔案名稱請鍵入js.txt，然後按一下「確定」。

1. 按一下「儲存全部」。

使用以下程式來取得外掛程式程式碼、將程式碼儲存在AEM存放庫中，並將程式碼新增至您的使用者端程式庫資料夾。

1. 登入 [sc.omniture.com](https://sc.omniture.com) 使用您的Adobe Analytics帳戶。
1. 在登陸頁面上，前往「說明>說明首頁」。
1. 在左側的目錄下，按一下「實作外掛程式」。
1. 按一下您要新增外掛程式的連結，然後在頁面開啟時，找到外掛程式的javascript原始程式碼，然後選取程式碼並加以複製。

1. 以滑鼠右鍵按一下使用者端程式庫資料夾，然後按一下「建立>建立檔案」。 在檔案名稱中，輸入您要整合的外掛程式名稱，後面接著.js，然後按一下「確定」。 例如，如果您整合getQueryParam外掛程式，請將檔案命名為getQueryParam.js。

   當您建立檔案時，它會開啟以進行編輯。

1. 將外掛程式JavaScript程式碼貼入檔案中，按一下「全部儲存」，然後關閉檔案。

1. 從使用者端程式庫資料夾開啟js.txt檔案。

1. 在新的一行中，新增包含外掛程式的檔案名稱，例如getQueryParam.js。 然後，按一下「儲存全部」並關閉檔案。

>[!NOTE]
>
>使用外掛程式時，請務必整合任何支援的外掛程式，否則外掛程式javascript將無法辨識它對支援外掛程式中的函式進行的呼叫。 例如，getPreviousValue()外掛程式需要split()外掛程式才能正常運作。
>
>需要新增支援外掛程式的名稱 **js.txt** 以及。
