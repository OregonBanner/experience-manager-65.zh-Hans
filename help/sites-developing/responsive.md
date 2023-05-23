---
title: 網頁的回應式設計
seo-title: Responsive design for web pages
description: 透過回應式設計，能以多種方向在多種裝置上有效顯示相同頁面
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '5336'
ht-degree: 0%

---

# 網頁的回應式設計{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe建議對需要以單頁應用程式框架為基礎的使用者端轉譯的專案使用SPA編輯器(例如 _React_)。 [了解详情](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>各種範例是根據AEM (Adobe Experience Manager)不再隨附的Geometrixx範例內容，已由We.Retail取代。 檢視檔案 [We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx) 瞭解如何下載和安裝Geometrixx。

設計您的網頁，使其適應顯示它們的使用者端檢視區。 透過回應式設計，相同的頁面可雙向有效顯示在多個裝置上。 下圖示範頁面可回應檢視區大小變更的一些方式：

* 版面：對較小的檢視區使用單欄版面，對較大的檢視區使用多欄版面。
* 文字大小：在較大的檢視區中使用較大的文字大小（如標題）。
* 內容：在較小裝置上顯示時，僅包含最重要的內容。
* 導覽：提供裝置特定工具來存取其他頁面。
* 影像：提供適合使用者端檢視區的影像轉譯。 視窗尺寸而定。

![chlimage_1-4](assets/chlimage_1-4a.png)

開發Adobe Experience Manager (AEM)應用程式，產生可適應多種視窗大小和方向的HTML5頁面。 例如，下列檢視區寬度範圍會與各種裝置型別和方向相對應

* 最大寬度480畫素（手機、縱向）
* 最大寬度767畫素（手機、橫向）
* 介於768畫素和979畫素之間的寬度（平板電腦，縱向）
* 寬度介於980畫素和1199畫素之間（平板電腦、橫向）
* 寬度1200畫素或更高（案頭）

如需實作回應式設計行為的相關資訊，請參閱下列主題：

* [媒體查詢](/help/sites-developing/responsive.md#using-media-queries)
* [流動格線](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [最適化影像](/help/sites-developing/responsive.md#using-adaptive-images)

當您設計時，請使用 **[!UICONTROL Sidekick]** 以預覽各種熒幕大小的頁面。

## 開發之前 {#before-you-develop}

在開發支援網頁的AEM應用程式之前，您應該先做出數個設計決定。 例如，您必須具備下列資訊：

* 您定位的裝置。
* 目標檢視區大小。
* 每個目標檢視區大小的頁面配置。

### 應用程式結構 {#application-structure}

典型的AEM應用程式結構支援所有回應式設計實作：

* 頁面元件位於/apps/下方&#x200B;*application_name*/components
* 範本位於/apps/下方&#x200B;*application_name*/templates
* 設計位於/etc/designs之下

## 使用媒體查詢 {#using-media-queries}

媒體查詢可選擇性使用CSS樣式來轉譯頁面。 AEM開發工具和功能可讓您在應用程式中有效率地實作媒體查詢。

W3C群組提供 [媒體查詢](https://www.w3.org/TR/mediaqueries-3/) 說明此CSS3功能和語法的建議。

### 建立CSS檔案 {#creating-the-css-file}

在CSS檔案中，根據您鎖定目標的裝置屬性定義媒體查詢。 下列實作策略可有效管理每個媒體查詢的樣式：

* 使用ClientLibraryFolder定義在轉譯頁面時組裝的CSS。
* 在不同的CSS檔案中定義每個媒體查詢和相關聯的樣式。 使用代表媒體查詢之裝置功能的檔案名稱會很有用。
* 定義個別CSS檔案中所有裝置通用的樣式。
* 在ClientLibraryFolder的css.txt檔案中，依照組合的CSS檔案中的要求，對CSS檔案清單進行排序。

此 `We.Retail` 媒體範例使用此策略來定義網站設計中的樣式。 使用的CSS檔案 `We.Retail` 位於 `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

下表列出css子資料夾中的檔案。

<table>
 <tbody>
  <tr>
   <th>檔案名稱</th>
   <th>描述</th>
   <th>媒體查詢</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>通用樣式。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>通用樣式，由TwitterBootstrap定義。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>所有寬度或寬度為1200畫素之媒體的樣式。</td>
   <td><p>@media （最小寬度： 1200畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>寬度介於980畫素和1199畫素之間的媒體樣式。</td>
   <td><p>@media （最小寬度：980畫素）和（最大寬度：1199畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>寬度介於768畫素和979畫素之間的媒體樣式。 </td>
   <td><p>@media （最小寬度：768畫素）和（最大寬度：979畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>寬度小於768畫素的所有媒體樣式。</td>
   <td><p>@media （最大寬度：767畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>寬度小於481畫素的所有媒體樣式。</td>
   <td>@media （最大寬度：480畫素） {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

中的css.txt檔案 `/etc/designs/weretail/clientlibs` 資料夾會列出使用者端資料庫資料夾中包含的CSS檔案。 檔案的順序會實作樣式優先順序。 裝置大小減少時，樣式會更加具體。

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**秘訣**：描述性檔案名稱可讓您輕鬆識別目標檢視區大小。

### 搭配AEM頁面使用媒體查詢 {#using-media-queries-with-aem-pages}

在頁面元件的JSP指令碼中包含使用者端程式庫資料夾。 這麼做有助於產生包含媒體查詢的CSS檔案，並參考該檔案。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>此 `apps.weretail.all` client library資料夾內嵌clientlibs資料庫。

JSP指令碼會產生下列參考樣式表的HTML程式碼：

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 預覽特定裝置 {#previewing-for-specific-devices}

檢視不同檢視區大小的頁面預覽，以便測試回應式設計的行為。 在 **[!UICONTROL 預覽]** 模式， **[!UICONTROL Sidekick]** 包含 **[!UICONTROL 裝置]** 您用來選取裝置的下拉式功能表。 當您選取裝置時，頁面會隨著檢視區大小而改變。

![chlimage_1-5](assets/chlimage_1-5a.png)

若要在中啟用裝置預覽 **[!UICONTROL Sidekick]**，您必須設定頁面和 **[!UICONTROL MobileEmulatorProvider]** 服務。 另一個頁面設定會控制出現在「 」中的 **[!UICONTROL 裝置]** 清單。

### 新增裝置清單 {#adding-the-devices-list}

此 **[!UICONTROL 裝置]** 清單出現於 **[!UICONTROL Sidekick]** 當頁面包含轉譯的JSP指令碼時 **[!UICONTROL 裝置]** 清單。 若要新增 **[!UICONTROL 裝置]** 清單至 **[!UICONTROL Sidekick]**，包含 `/libs/wcm/mobile/components/simulator/simulator.jsp` 中的指令碼 `head` 區段。

將下列程式碼加入定義 `head` 區段：

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

若要檢視範例，請開啟 `/apps/weretail/components/page/head.jsp` 檔案CRXDE Lite。

### 註冊用於模擬的頁面元件 {#registering-page-components-for-simulation}

若要讓裝置模擬器支援您的頁面，請使用MobileEmulatorProvider Factory服務註冊您的頁面元件，並定義 `mobile.resourceTypes` 屬性。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

例如，若要建立 ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` 節點的位置：

* 父資料夾： `/apps/application_name/config`
* 名称: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   此 —  `*alias*` 需要字尾，因為MobileEmulatorProvider服務是工廠服務。 使用這個工廠唯一的任何別名。

* jcr:primaryType: `sling:OsgiConfig`

新增下列節點屬性：

* 名称: `mobile.resourceTypes`
* 类型: `String[]`
* 值：轉譯您網頁的頁面元件路徑。 例如， geometrixx-media應用程式會使用以下值：

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### 指定裝置群組 {#specifying-the-device-groups}

若要指定出現在「裝置」清單中的裝置群組，請新增 `cq:deviceGroups` 屬性至 `jcr:content` 網站根頁面的節點。 屬性的值是裝置群組節點的路徑陣列。

裝置群組節點位於 `/etc/mobile/groups` 資料夾。

例如，Geometrixx Media網站的根頁面為 `/content/geometrixx-media`. 此 `/content/geometrixx-media/jcr:content` 節點包含下列屬性：

* 名称: `cq:deviceGroups`
* 类型: `String[]`
* 价值: `/etc/mobile/groups/responsive`

使用「工具」主控台： [建立和編輯裝置群組](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>對於您用於回應式設計的裝置群組，請編輯裝置群組，然後在「一般」標籤上選取「停用模擬器」。 此選項可防止出現與回應式設計無關的模擬器輪播。

## 使用自適應影像 {#using-adaptive-images}

您可以使用媒體查詢來選取要在頁面中顯示的影像資源。 但是，使用媒體查詢來條件化其使用的每個資源都會下載到使用者端。 媒體查詢只會判斷是否顯示下載的資源。

對於大型資源（例如影像），下載所有資源並非有效使用使用者端的資料管道。 若要有選擇地下載資源，請在媒體查詢執行選擇後，使用JavaScript起始資源要求。

以下策略會載入使用媒體查詢選擇的單一資源：

1. 為資源的每個版本新增DIV元素。 將資源的URI加入為屬性值的值。 瀏覽器不會將屬性解譯為資源。
1. 將媒體查詢新增至適用於資源的每個DIV元素。
1. 當檔案載入或視窗調整大小時，JavaScript程式碼會測試每個DIV元素的媒體查詢。
1. 根據查詢的結果，決定要包括的資源。
1. 在參照資源的DOM中插入HTML元素。

### 使用JavaScript評估媒體查詢 {#evaluating-media-queries-using-javascript}

的實作 [MediaQueryList介面](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) W3C所定義的專案，可讓您使用JavaScript評估媒體查詢。 您可以將邏輯套用至媒體查詢結果，並執行目前視窗的目標指令碼：

* 實作MediaQueryList介面的瀏覽器支援 `window.matchMedia()` 函式。 此函式針對給定的字串測試媒體查詢。 此函式傳回 `MediaQueryList` 提供查詢結果存取權的物件。

* 對於未實作介面的瀏覽器，您可以使用 `matchMedia()` 多邊形填色，例如 [matchmedia.js](https://github.com/paulirish/matchMedia.js)，免費提供的JavaScript程式庫。

#### 選取媒體專用資源 {#selecting-media-specific-resources}

W3C [圖片元素](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) 使用媒體查詢來決定影像元素要使用的來源。 圖片元素會使用元素屬性，將媒體查詢與影像路徑建立關聯。

免費提供 [picturefill.js資料庫](https://github.com/scottjehl/picturefill) 提供與建議類似的功能 `picture` 元素，並使用類似的策略。 picturefill.js程式庫呼叫 `window.matchMedia` 以評估為一組定義的媒體查詢 `div` 元素。 每個 `div` element也會指定影像來源。 來源的媒體查詢會使用 `div` 元素傳回 `true`.

此 `picturefill.js` 程式庫需要類似於以下範例的HTML程式碼：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

轉譯頁面時，picturefull.js會插入 `img` 元素做為的最後一個子項 `<div data-picture>` 元素：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

在AEM頁面中， `data-src` attribute是存放庫中資源的路徑。

### 在AEM中實作最適化影像 {#implementing-adaptive-images-in-aem}

若要在AEM應用程式中實作最適化影像，您必須新增必要的JavaScript程式庫，並在頁面中包含必要的HTML標籤。

**库**

取得下列JavaScript程式庫，並將其包含在使用者端程式庫資料夾中：

* [matchmedia.js](https://github.com/paulirish/matchMedia.js) （適用於未實作MediaQueryList介面的瀏覽器）
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (可透過 `/etc/clientlibs/granite/jquery` 使用者端資料庫資料夾（類別= jquery）
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) （重新調整視窗大小後發生一次的jquery事件）

**秘訣：** 您可以透過以下方式自動串連多個使用者端資料庫資料夾： [內嵌](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

建立一個元件，該元件會產生picturefill.js程式碼預期的必要div元素。 在AEM頁面中，data-src屬性的值是儲存庫中資源的路徑。 例如，頁面元件可以硬式編碼媒體查詢和DAM中影像轉譯的相關路徑。 或者，建立自訂影像元件，讓作者選取影像轉譯或指定執行階段轉譯選項。

以下範例HTML會從相同影像的兩個DAM轉譯中選取。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>最適化影像基礎元件實作最適化影像：
>
>* 使用者端資料庫資料夾： `/libs/foundation/components/adaptiveimage/clientlibs`
>* 產生HTML的指令碼： `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>後續章節會提供此元件的詳細資訊。

### 瞭解AEM中的影像演算 {#understanding-image-rendering-in-aem}

若要自訂影像演算，您應瞭解預設的AEM靜態影像演算實作。 AEM提供影像元件和影像轉譯servlet，可搭配使用以轉譯網頁的影像。 將影像元件納入頁面的段落系統時，會發生下列事件順序：

1. 製作：作者可編輯「影像」元件，以指定要包含在HTML頁面中的影像檔案。 檔案路徑會儲存為影像元件節點的屬性值。
1. 頁面請求：頁面元件的JSP會產生HTML代碼。 Image元件的JSP會產生一個img元素並將其新增到頁面中。
1. 影像要求：網頁瀏覽器載入頁面，並根據img元素的src屬性要求影像。
1. 影像演算：影像演算servlet會將影像傳回至網頁瀏覽器。

![chlimage_1-6](assets/chlimage_1-6a.png)

例如，影像元件的JSP會產生下列HTML元素：

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

瀏覽器載入頁面時，會使用src屬性的值作為URL來要求影像。 Sling會解壓縮URL：

* 资源: `/content/mywebsite/en/_jcr_content/par/image_0`
* 副檔名： `.jpg`
* 选择器: `img`
* 后缀: `1358372073597.jpg`

此 `image_0` 節點具有 `jcr:resourceType` 值 `foundation/components/image`，具有 `sling:resourceSuperType` 值 `foundation/components/parbase`. parbase元件包含的img.java.GET指令碼會符合選取器和要求URL的副檔名。 CQ會使用此指令碼(servlet)來轉譯影像。

若要檢視指令碼的原始碼，請使用CRXDE Lite開啟 `/libs/foundation/components/parbase/img.GET.java`
檔案。

## 根據目前檢視區大小縮放影像 {#scaling-images-for-the-current-viewport-size}

在執行階段根據使用者端檢視區的特性縮放影像，以提供符合回應式設計原則的影像。 使用servlet和編寫元件，使用與靜態影像演算相同的設計模式。

元件必須執行下列工作：

* 將影像資源的路徑和所需尺寸儲存為屬性值。
* 產生 `div` 包含媒體選擇器的元素以及轉譯影像的服務呼叫。

>[!NOTE]
>
>Web使用者端使用matchMedia和Picturefill JavaScript程式庫（或類似的程式庫）來評估媒體選擇器。

處理影像要求的servlet必須執行下列工作：

* 從元件屬性中擷取影像的路徑和尺寸。
* 根據屬性縮放影像並傳回影像。

**可用的解決方案**

AEM會安裝下列實作，供您使用或擴充。

* 產生媒體查詢的最適化影像基礎元件，以及對可縮放影像的最適化影像元件Servlet的HTTP請求。
* GeometrixxCommons套件會安裝會改變影像解析度的影像參考修改Servlet範例servlet。

### 瞭解自我調整影像元件 {#understanding-the-adaptive-image-component}

最適化影像元件會產生對最適化影像元件Servlet的呼叫，以演算根據裝置熒幕調整大小的影像。 此元件包含下列資源：

* JSP：新增將媒體查詢與對最適化影像元件Servlet的呼叫相關聯的div元素。
* 使用者端資料庫： clientlibs資料夾是 `cq:ClientLibraryFolder` 會組合matchMedia polyfill JavaScript程式庫和修改過的Picturefill JavaScript程式庫。
* 編輯對話方塊： `cq:editConfig` 節點會覆寫CQ foundation影像元件，以便放置目標建立最適化影像元件，而不是基礎影像元件。

#### 新增DIV元素 {#adding-the-div-elements}

adaptive-image.jsp指令碼包含以下產生div元素和媒體查詢的程式碼：

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

此 `path` 變數包含目前資源的路徑（最適化影像元件節點）。 程式碼會產生一系列 `div` 元素具有下列結構：

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

的值 `data-scr` attribute是Sling解析至轉譯影像之最適化影像元件Servlet的URL。 data-media屬性包含根據使用者端屬性評估的媒體查詢。

以下HTML程式碼為 `div` JSP產生的元素：

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 變更影像大小選取器 {#changing-the-image-size-selectors}

如果您自訂最適化影像元件並變更寬度選擇器，您也必須設定最適化影像元件Servlet以支援寬度。

### 瞭解自我調整影像元件Servlet {#understanding-the-adaptive-image-component-servlet}

最適化影像元件Servlet會根據指定的寬度調整JPEG影像的大小，並設定JPEG品質。

#### 最適化影像元件Servlet的介面 {#the-interface-of-the-adaptive-image-component-servlet}

最適化影像元件Servlet繫結至預設的Sling servlet，並支援.jpg、.jpeg、.gif和.png副檔名。 Servlet選擇器為img。

>[!CAUTION]
>
>AEM不支援動畫.gif檔案以進行最適化轉譯。

因此，Sling會將以下格式的HTTP請求URL解析為此servlet：

`*path-to-node*.img.*extension*`

例如，Sling使用URL轉送HTTP請求 `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` 至最適化影像元件Servlet。

另外兩個選取器會指定要求的影像寬度和JPEG品質。 下列範例會要求寬度480畫素和中等品質的影像：

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**支援的影像屬性**

此servlet接受有限數量的影像寬度和品質。 預設支援下列寬度（畫素）：

* 全部
* 320
* 480
* 476
* 620

完整值表示沒有縮放。

支援下列JPEG品質值：

* 低
* 中
* 高

數值分別為0.4、0.82和1.0。

**變更預設支援的寬度**

使用Web控制檯([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))或sling：OsgiConfig節點，以設定Adobe CQ最適化影像元件Servlet的支援寬度。

如需如何設定AEM服務的詳細資訊，請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>網頁主控台</th>
   <th>sling：OsgiConfig</th>
  </tr>
  <tr>
   <th>服務或節點名稱</th>
   <td>「設定」標籤上的服務名稱為Adobe CQ最適化影像元件Servlet</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>属性</th>
   <td><p>支援的寬度</p>
    <ul>
     <li>若要新增支援的寬度，請按一下+按鈕並輸入正整數。</li>
     <li>若要移除支援的寬度，請按一下相關聯的 — 按鈕。</li>
     <li>若要修改支援的寬度，請編輯欄位值。</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>屬性是多值字串值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 實作詳細資料 {#implementation-details}

此 `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` 類別擴充 [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 類別。 AdaptiveImageComponentServlet原始程式碼位於 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` 資料夾。

類別會使用Felix SCR註解來設定與servlet關聯的資源型別和檔案副檔名，以及第一個選取器的名稱。

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

此servlet使用「屬性SCR」註解來設定預設支援的影像品質和尺寸。

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

此 `AbstractImageServlet` 類別提供 `doGet` 處理HTTP要求的方法。 此方法會判斷與要求相關聯的資源、從存放庫擷取資源屬性，並將它們傳回 [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 物件。

>[!NOTE]
>
>此 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 類別提供 `getFileReference method`，會擷取資源的 `fileReference` 屬性。

此 `AdaptiveImageComponentServlet` 類別會覆寫 `createLayer` 方法。 方法會從「 」取得影像資源的路徑及要求的影像寬度 `ImageContext` 物件。 然後它會呼叫 `info.geometrixx.commons.impl.AdaptiveImageHelper` 類別，執行實際的影像縮放。

AdaptiveImageComponentServlet類別也會覆寫writeLayer方法。 此方法會將JPEG品質套用至影像。

### 影像參考修改Servlet (常見Geometrixx) {#image-reference-modification-servlet-geometrixx-common}

範例影像參考修改Servlet會產生影像元素的大小屬性，以縮放網頁上的影像。

#### 呼叫servlet {#calling-the-servlet}

此servlet繫結到 `cq:page` 資源並支援.jpg副檔名。 此servlet選擇器為 `image`. 因此，Sling會將以下格式的HTTP請求URL解析為此servlet：

`path-to-page-node.image.jpg`

例如，Sling使用URL轉送HTTP請求 `http://localhost:4502/content/geometrixx/en.image.jpg` 至影像參照修改Servlet。

三個額外的選取器可指定要求的影像寬度、高度和（選擇性）品質。 下列範例會要求寬度770畫素、高度360畫素和中等品質的影像。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**支援的影像屬性**

此servlet接受有限數量的影像尺寸和品質值。

預設支援下列值(widthxheight)：

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

支援下列影像品質值：

* 低
* 中
* 高

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

#### 指定影像資源 {#specifying-the-image-resource}

影像路徑、尺寸和品質值必須儲存為存放庫中節點的屬性：

* 節點名稱為 `image`.
* 父節點為 `jcr:content` 節點屬於 `cq:page` 資源。

* 影像路徑會儲存為名為之屬性的值 `fileReference`.

編寫頁面時，請使用 **Sidekick** 以指定影像並新增 `image` 節點至頁面屬性：

1. 在 **Sidekick**，按一下 **頁面** 標籤，然後按一下 **頁面屬性**.
1. 按一下 **影像** 標籤並指定影像。
1. 单击&#x200B;**确定**。

#### 實作詳細資料 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet類別可擴充 [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 類別。 如果您已安裝cq-geometrixx-commons-pkg套件，則ImageReferenceModificationServlet原始程式碼位於 `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` 資料夾。

類別會使用Felix SCR註解來設定與servlet關聯的資源型別和檔案副檔名，以及第一個選取器的名稱。

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

此servlet使用「屬性SCR」註解來設定預設支援的影像品質和尺寸。

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

此 `AbstractImageServlet` 類別提供 `doGet` 處理HTTP要求的方法。 此方法會判斷與呼叫相關聯的資源、從存放庫擷取資源屬性，並將它們儲存在 [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 物件。

此 `ImageReferenceModificationServlet` 類別會覆寫 `createLayer` 方法和實作決定要呈現之影像資源的邏輯。 方法會擷取頁面的子節點 `jcr:content` 節點已命名 `image`. 一個 [影像](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) 物件是從這裡建立的 `image` 節點，以及 `getFileReference` 方法會傳回影像檔案的路徑，從 `fileReference` 影像節點的屬性。

>[!NOTE]
>此 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 類別提供getFileReferencemethod。

## 開發流動格線 {#developing-a-fluid-grid}

AEM可讓您有效率且有效地實作流動格線。 此頁面說明如何整合流動網格或現有的網格實作(例如 [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css))至您的AEM應用程式。

如果您不熟悉流動格點，請參閱 [Fluid Grid簡介](/help/sites-developing/responsive.md#developing-a-fluid-grid) 區段。 此簡介提供流動格點的概觀以及設計流動格點的指引。

### 使用「頁面」元件定義網格 {#defining-the-grid-using-a-page-component}

使用頁面元件來產生定義頁面內容區塊的HTML元素。 頁面參照的ClientLibraryFolder提供可控制內容區塊版面的CSS：

* 頁面元件：新增代表內容區塊列的div元素。 代表內容區塊的div元素包含作者新增內容的parsys元件。
* 使用者端程式庫資料夾：提供CSS檔案，其中包含媒體查詢和div元素的樣式。

例如，範例geometrixx-media應用程式包含media-home元件。 此頁面元件插入兩個指令碼，產生兩個 `div` 類別元素 `row-fluid`：

* 第一列包含 `div` 類別元素 `span12` （內容跨越12欄）。 此 `div` 元素包含parsys元件。

* 第二列包含兩個 `div` 元素，類別之一 `span8` 和類別中的另一個 `span4`. 每個 `div` 元素包含parsys元件。

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>當元件包含多個時 `cq:include` 參照parsys元件的元素，每個 `path` 屬性必須有不同的值。

#### 縮放頁面元件格線 {#scaling-the-page-component-grid}

與geometrixx-media頁面元件關聯的設計(`/etc/designs/geometrixx-media`)包含 `clientlibs` ClientLibraryFolder。 此ClientLibraryFolder定義CSS樣式 `row-fluid` 類別， `span*` 類別，以及 `span*` 為子系的類別 `row-fluid` 類別。 媒體查詢可讓您針對不同的檢視區大小重新定義樣式。

以下範例CSS是這些樣式的子集。 此子集專注於 `span12`， `span8`、和 `span4` 類別以及兩種檢視區大小的媒體查詢。 請注意CSS的下列特性：

* 此 `.span` 樣式會使用絕對數字來定義元素寬度。
* 此 `.row-fluid .span*` 樣式會將元素寬度定義為父項的百分比。 百分比是以絕對寬度計算。
* 較大檢視區的媒體查詢會指派較大的絕對寬度。

>[!NOTE]
>
>Geometrixx Media範例整合了 [Bootstrap](https://getbootstrap.com/2.0.2/) 將JavaScript框架匯入其Fluid Grid實作。 Bootstrap架構提供bootstrap.css檔案。

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### 重新定位頁面元件格線中的內容 {#repositioning-content-in-the-page-component-grid}

範例Geometrixx Media應用程式的頁面會在寬檢視區中水準分佈內容區塊列。 在較小的檢視區中，相同的區塊會垂直分佈。 以下範例CSS顯示為media-home頁面元件產生的HTML程式碼實施此行為的樣式：

* media-welcome頁面的預設CSS會指派 `float:left` 樣式 `span*` 位於內部的類別 `row-fluid` 類別。

* 較小檢視區的媒體查詢會指派 `float:none` 相同類別的樣式。

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### 將頁面元件模組化 {#tip-modularize-your-page-components}

將元件模組化，以便有效使用程式碼。 您的網站可能會使用數種不同型別的頁面，例如歡迎頁面、文章頁面或產品頁面。 每種型別的頁面包含不同型別的內容，且可能使用不同的版面。 不過，當每個版面的某些元素在多個頁面中很通用時，您可以重複使用實作該版面部分的程式碼。

**使用頁面元件覆蓋圖**

建立主要頁面元件，提供產生頁面各個部分的指令碼，例如 `head` 和 `body` 區段，和 `header`， `content`、和 `footer` 區段。

建立使用主要頁面元件作為的其他頁面元件 `cq:resourceSuperType`. 這些元件包括視需要覆寫首頁面指令碼的指令碼。

例如，goemetrixx-media應用程式包含頁面元件( `sling:resourceSuperType` 基礎頁面元件)。 數個子元件（例如article、category和media-home）會使用此頁面元件作為 `sling:resourceSuperType`. 每個子元件都包含content.jsp檔案，此檔案會覆寫頁面元件的content.jsp檔案。

**重複使用指令碼**

建立多個JSP指令碼，以產生多個頁面元件通用的列和欄組合。 例如， `content.jsp` 文章的指令碼和media-home元件都參考 `8x4col.jsp` 指令碼。

**依目標檢視區大小組織CSS樣式**

在不同檔案中包含不同檢視區大小的CSS樣式和媒體查詢。 使用使用者端程式庫資料夾來串連它們。

### 將元件插入頁面格線 {#inserting-components-into-the-page-grid}

當元件產生單一內容區塊時，通常頁面元件建立的格點會控制內容的放置。

身為作者，內容區塊可以各種大小和相對位置轉譯。 內容文字不應使用相對方向來參照其他內容區塊。

如有必要，元件應提供其產生的HTML程式碼所需的任何CSS或JavaScript程式庫。 在元件內使用使用者端程式庫資料夾，以產生CSS和JS檔案。 若要公開檔案， [建立相依性或內嵌程式庫](/help/sites-developing/clientlibs.md#creating-client-library-folders) /etc資料夾下方的另一個使用者端資料庫資料夾中。

**子格點**

如果元件包含多個內容區塊，請在列內新增內容區塊，以在頁面上建立子網格：

* 使用與容納頁面元件相同的類別名稱，以便您可以將div元素表示為列和內容區塊。
* 若要覆寫頁面設計之CSS實作的行為，請對row div元素使用第二個類別名稱，並在使用者端程式庫資料夾中提供關聯的CSS。

例如， `/apps/geometrixx-media/components/2-col-article-summary` 元件會產生兩欄內容。 它產生的HTML具有以下結構：

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

此 `.row-fluid .span6` 頁面CSS的選取器會套用至 `div` 此HTML中相同類別和結構的元素。 不過，元件也包含/apps/geometrixx-media/components/2-col-article-summary/clientlibs使用者端程式庫資料夾：

* CSS使用與頁面元件相同的媒體查詢，以相同的離散頁面寬度在版面中建立變更。
* 選擇器使用 `multi-col-article-summary` 列的類別 `div` 元素來覆寫頁面的 `row-fluid` 類別。

例如，下列樣式包含在 `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` 檔案：

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## 流動格線簡介 {#introduction-to-fluid-grids}

流動格點可讓頁面版面配置適應使用者端檢視區的尺寸。 格點由邏輯欄和列組成，這些邏輯欄和列會定位頁面上的內容區塊。

* 欄決定內容區塊的水平位置和寬度。
* 列決定內容區塊的相對垂直位置。

使用HTML5技術，您可以實作格線並操控它，使頁面版面適應不同的檢視區大小：

* HTML `div` 元素包含橫跨部分欄的內容區塊。
* 當這些div元素中的一個或多個共用共同的父項div元素時，它們會組成一列。

### 使用獨立寬度 {#using-discrete-widths}

對於您定位的每個檢視區寬度範圍，請使用靜態頁面寬度和固定寬度的內容區塊。 手動調整瀏覽器視窗大小時，內容大小的變更會在分散的視窗寬度（也稱為中斷點）發生。 因此，頁面設計會更密切地粘著，最大化使用者體驗。

#### 縮放格線 {#scaling-the-grid}

使用格點來縮放內容區塊，以適應不同的檢視區大小。 內容區塊跨越特定數量的欄。 當欄寬增加或減少以符合不同的檢視區大小時，內容區塊的寬度也會相應地增加或減少。 縮放可支援寬到足以容納並排放置內容區塊的大中型檢視區。

![](do-not-localize/chlimage_1-1a.png)

#### 在格線中重新定位內容 {#repositioning-content-in-the-grid}

內容區塊的大小可由最小寬度限制，超出此寬度縮放不再有效。 對於較小的檢視區，格點可用於垂直分配內容區塊，而非水準分配。

![](do-not-localize/chlimage_1-2a.png)

### 設計格線 {#designing-the-grid}

決定必須在頁面上放置內容區塊的欄和列。 您的頁面版面配置會決定跨越網格的欄和列數。

**欄數**

包含足夠的欄以水平定位所有版面中的內容區塊（針對所有檢視區大小）。 使用的欄數超過目前所需的數目，因此您可以因應未來的頁面設計。

**列內容**

使用列來控制內容區塊的垂直位置。 決定共用相同列的內容區塊：

* 在任何版面中，彼此水準相鄰的內容區塊位於同一列。
* 水準（較寬的檢視區）和垂直（較小的檢視區）彼此相鄰的內容區塊位於同一列。

### 格線實作 {#grid-implementations}

建立CSS類別和樣式，以便您可以控制頁面上內容區塊的版面。 頁面設計通常以檢視區內內容區塊的相對大小和位置為基礎。 檢視區決定內容區塊的實際大小。 您的CSS必須說明相對和絕對大小。 您可以使用三種型別的CSS類別來實作流動格線：

* 的類別 `div` 作為所有列容器的元素。 此類別會設定格線的絕對寬度。
* 類別 `div` 代表列的元素。 此類別會控制其包含的內容區塊的水平或垂直位置。
* 類別 `div` 代表不同寬度內容區塊的元素。 寬度以父項（列）的百分比表示。

目標檢視區寬度（及其相關媒體查詢）可區分用於頁面配置的離散寬度。

#### 內容區塊寬度 {#widths-of-content-blocks}

一般而言， `width` 內容區塊類別的樣式是根據頁面和格線的下列特性：

* 您對每個目標檢視區大小使用的絕對頁面寬度。 已知值。
* 每個頁面寬度的格點欄的絕對寬度。 您可以決定這些值。
* 每欄的相對寬度，以總頁面寬度的百分比表示。 您會計算這些值。

CSS包含一系列使用下列結構的媒體查詢：

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

使用以下演演算法作為開發頁面的元素類別和CSS樣式的起點。

1. 為包含所有列的div元素定義類別名稱，例如 `content.`
1. 為代表列的div元素定義CSS類別，例如 `row-fluid`.
1. 定義內容區塊元素的類別名稱。 所有可能的寬度（以欄跨度而言）都需要類別。 例如，使用 `span3` 類別 `div` 橫跨三欄的元素，請使用 `span4` 橫跨四欄的類別。 定義格線中欄的類別數。

1. 針對您定位的每個檢視區大小，將對應的媒體查詢新增至您的CSS檔案。 在每個媒體查詢中新增下列專案：

   * 的選擇器 `content` 類別，例如 `.content{}`.
   * 每個範圍類別的選取器，例如 `.span3{ }`.
   * 的選擇器 `row-fluid` 類別，例如 `.row-fluid{ }`
   * 位於資料列流動類別內部的跨度類別選取器，例如 `.row-fluid span3 { }`.

1. 為每個選取器新增寬度樣式：

   1. 設定寬度 `content` 頁面絕對大小的選取器，例如 `width:480px`.
   1. 將所有資料列流體選擇器的寬度設定為100%。
   1. 將所有範圍選取器的寬度設定為內容區塊的絕對寬度。 簡單格點會使用相同寬度的均勻分佈欄： `(absolute width of page)/(number of columns)`.
   1. 設定 `.row-fluid .span` 選取器以總寬度的百分比表示。 使用計算此寬度 `(absolute span width)/(absolute page width)*100` 公式。

#### 將內容區塊定位在列中 {#positioning-content-blocks-in-rows}

使用浮點樣式 `.row-fluid` 類別，讓您能夠控制列中的內容區塊是水準還是垂直排列。

* 此 `float:left` 或 `float:right` style會導致子元素（內容區塊）的水準分佈。

* 此 `float:none` style會造成子元素的垂直分佈。

將樣式新增至 `.row-fluid` 每個媒體查詢內的選擇器。 根據您用於該媒體查詢的頁面版面配置設定值。 例如，下圖說明為寬檢視區水準分送內容，為窄檢視區垂直分送內容的列。

![](do-not-localize/chlimage_1-3a.png)

下列CSS可實作此行為：

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### 將類別指派給內容區塊 {#assigning-classes-to-content-blocks}

針對您定位的每個檢視區大小的頁面配置，決定每個內容區塊所跨越的欄數。 然後，決定要將哪個類別用於這些內容區塊的div元素。

建立div類別後，您可以使用AEM應用程式實作網格。
