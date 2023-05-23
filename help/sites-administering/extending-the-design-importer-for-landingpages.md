---
title: 擴充和設定登入頁面的Design Importer
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: 瞭解如何設定登入頁面的Design Importer。
seo-description: Learn how to configure the Design Importer for landing pages.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3503'
ht-degree: 0%

---

# 擴充和設定登入頁面的Design Importer{#extending-and-configuring-the-design-importer-for-landing-pages}

本節說明如何設定，並視需要擴充登入頁面的設計匯入工具。 有關匯入後使用登入頁面的資訊，請參閱 [登陸頁面。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**讓設計匯入工具提取您的自訂元件**

以下是讓設計匯入工具識別自訂元件的邏輯步驟

1. 建立TagHandler

   * 標籤處理常式是處理特定型別HTML標籤的POJO。 您的TagHandler可以處理的HTML標籤「種類」是透過TagHandlerFactory的OSGi屬性&quot;tagpattern.name&quot;來定義。 此OSGi屬性基本上是規則運算式，應該符合您要處理的輸入html標籤。 所有巢狀標籤都會擲回標籤處理常式進行處理。 例如，如果您註冊的div包含巢狀 &lt;p> 標籤， &lt;p> 標籤也會擲回至您的TagHandler，而由您自行決定如何處理它。
   * 標籤處理常式介面類似於SAX內容處理常式介面。 它會接收每個html標籤的SAX事件。 作為標籤處理常式提供者，您需要實作由設計匯入工具架構自動呼叫的特定生命週期方法。

1. 建立其對應的TagHandlerFactory。

   * 標籤處理常式工廠是OSGi元件(singleton)，負責產生標籤處理常式的例項。
   * 您的標籤處理常式處理常式工廠必須公開名為「tagpattern.name」的OSGi屬性，該屬性的值與輸入html標籤相符。
   * 如果有多個標籤處理常式符合輸入html標籤，則會挑選排名較高的處理常式。 排名本身會顯示為OSGi屬性 **service.ranking**.
   * TagHandlerFactory是OSGi元件。 您要提供給TagHandler的任何參考都必須透過此工廠提供。

1. 如果您想要覆寫預設值，請確定TagHandlerFactory有更好的排名。

>[!CAUTION]
>
>Design Importer，用於匯入登入頁面， [已由AEM 6.5取代](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## 準備匯入的HTML {#preparing-the-html-for-import}

建立匯入工具頁面後，您可以匯入完整的HTML登陸頁面。 若要匯入HTML登入頁面，您必須先將其內容壓縮至設計封裝。 設計套件包含您的HTML登陸頁面以及參考的資產（影像、css、圖示、指令碼等）。

下列速查表提供如何準備匯入HTML的範例：

登陸頁面速查表

[获取文件](assets/cheatsheet.zip)

### Zip檔案版面配置與需求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>此時，ZIP檔案只能包含一個HTML頁面或頁面的一部分。

zip的範例版面配置如下：

* /index.html ->登陸頁面HTML檔案
* /css ->以新增至CSS clientlib
* /img ->所有影像和資產
* /js ->以新增至JS clientlib

配置以HTML5樣板最佳實務配置為基礎。 如需詳細資訊，請參閱 [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>至少，設計封裝 **必須** 包含 **index.html** 根層級的檔案。 如果要匯入的登入頁面也有行動版本，則zip檔案必須包含 **mobile.index.html** 以及 **index.html** 在根層級。

### 準備登入頁面HTML {#preparing-the-landing-page-html}

若要匯入HTML，您必須將畫布div新增至登入頁面HTML。

畫布div是html **div** 替換為 `id="cqcanvas"` 必須插入至HTML中 `<body>` 標籤包住，且必須包含要進行轉換的內容。

新增畫布div後，登入頁面HTML的範常式式碼片段如下：

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### 準備HTML以包含可編輯的AEM元件 {#preparing-the-html-to-include-editable-aem-components}

匯入登入頁面時，您可以選擇按原樣匯入頁面，這表示在登入頁面匯入後，您無法在AEM中編輯任何匯入的專案(您仍然可以在頁面上新增其他AEM元件)。

在匯入登入頁面之前，您可能想要轉換登入頁面的某些部分，以使其成為可編輯的AEM元件。 這可讓您快速編輯登陸頁面的部分，即使在已匯入登陸頁面設計之後也是如此。

您可以透過新增 `data-cq-component` 至您匯入之HTML檔案中的適當元件。

下節將說明如何編輯HTML檔案，以便將登入頁面的某些部分轉換為不同的可編輯AEM元件。 如需元件的詳細說明，請參閱 [登陸頁面元件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>將部分登入頁面轉換為AEM元件的HTML標籤同時具有長格式和速記標籤宣告。 針對每個元件會說明這兩者。

### 限制 {#limitations}

匯入之前，請注意下列限制：

### 不會保留套用在&amp;lt；body>標籤上的任何屬性，例如類別或ID {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果有任何屬性（例如id或類別）套用在body標籤上 `<body id="container">` 則在匯入後不會保留。 因此，匯入的設計不應與套用至的屬性有任何相依性 `<body>` 標籤之間。

### 拖放zip {#drag-and-drop-zip}

Internet Explorer和Firefox 3.6版及舊版不支援拖放zip上傳。 若要在使用這些瀏覽器時上傳設計，請按一下拖放檔案區域以開啟檔案上傳對話方塊，然後使用該對話方塊上傳您的設計。

支援「拖放」設計zip的瀏覽器為Chrome、Safari5.x、Firefox 4及更高版本。

### 不支援Modernizer {#modernizr-is-not-supported}

`Modernizr.js` 是以javascript為基礎的工具，可偵測瀏覽器的原生功能，並偵測這些功能是否適用於html5元素。 設計若使用Modernizer來增強舊版不同瀏覽器的支援，可能會導致登陸頁面解決方案中出現匯入問題。 `Modernizr.js` Design Importer不支援指令碼。

### 匯入設計封裝時未保留頁面屬性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

任何頁面屬性（例如自訂網域、強制執行HTTPS等） 在設計匯入後，在匯入設計套件之前為頁面（使用空白登陸頁面範本）設定的將會遺失。 因此，建議您在匯入設計套件後設定頁面屬性。

### 假設僅HTML標籤 {#html-only-markup-assumed}

匯入時，標籤會因為安全性原因而經過消毒，以避免匯入和發佈無效的標籤。 這假設僅限HTML的標籤和所有其他形式的元素(例如內嵌SVG或Web元件)將被篩選掉。

### 文本 {#text}

插入文字元件的HTML標示( `foundation/components/text`)在design package的HTML中：

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

在HTML中加入上述標籤，會執行下列動作：

* 建立可編輯的AEM文字元件( `sling:resourceType=foundation/components/text`)，此頁面位於匯入設計套件後建立的登陸頁面中。
* 設定 `text` 內含之HTML的已建立文字元件的屬性 `div`.

**速記元件標籤宣告**：

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**含清單的文字**

若要新增包含清單的文字：

* 1st
* 2nd

可以在RTE編輯器中編輯的專案：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**含顏色的文字**

若要新增可在RTE編輯器中編輯的顏色（粉紅色）文字：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 标题 {#title}

HTML標籤可插入標題元件( `wcm/landingpage/components/title`)在design package的HTML中：

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

在HTML中加入上述標籤，會執行下列動作：

* 建立可編輯的AEM標題元件( `sling:resourceType=wcm/landingpage/components/title`)，此頁面位於匯入設計套件後建立的登陸頁面中。
* 設定 `jcr:title` 將建立的標題元件屬性改成包在div中的標題標籤內的文字。
* 設定 `type` 屬性至標題標籤，在此案例中為 `h1`.

標題元件支援7種型別 —  `h1, h2, h3, h4, h5, h6` 和 `default`.

**速記元件標籤宣告**：

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 图像 {#image}

在design package內的HTML中插入影像元件(foundation/components/image)的HTML標籤：

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

在HTML中加入上述標籤，會執行下列動作：

* 建立可編輯的AEM影像元件( `sling:resourceType=foundation/components/image`)，此頁面位於匯入設計套件後建立的登陸頁面中。
* 設定 `fileReference` 建立之影像元件的屬性，可匯入src屬性中指定的影像的路徑。
* 設定 `alt` 屬性變更為img標籤中alt屬性的值。
* 設定 `title` 屬性前往img標籤中title屬性的值。
* 設定 `width` 屬性變更為img標籤中width屬性的值。
* 設定 `height` 屬性前往img標籤中height屬性的值。

**速記元件標籤宣告：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 影像元件Div中不支援絕對URL img src {#absolute-url-img-src-not-supported-within-image-component-div}

如果 `<img>` 已嘗試使用絕對url src的標籤進行元件轉換，適當的 **UnsupportedTagContentException** 會引發。 例如，不支援下列專案：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

否則，不屬於影像元件div的img標籤會支援絕對URL影像。

### 行動號召元件 {#call-to-action-components}

您可以將部分登入頁面標籤為匯入為「可編輯的呼叫動作元件」 — 在匯入登入頁面後，可以編輯這類匯入的呼叫動作元件。 AEM包含下列CTA元件：

* 點進連結 — 可讓您新增文字連結，當按一下連結時，會將訪客導向至目標URL。
* 圖形連結 — 可讓您新增影像，在按一下時讓訪客前往目標URL。

#### 點進連結 {#click-through-link}

此CTA元件可用來在登入頁面上新增文字連結。

支援的屬性

* 標籤，包含粗體、斜體和底線選項
* 目標URL，支援第三方和AEM URL
* 頁面呈現選項（相同視窗、新視窗等）

HTML標籤，以在匯入的zip檔案中包含點進元件。 此處href對應至目標URL，「檢視產品詳細資料」對應至標籤，以此類推。

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

此元件可用於任何獨立應用程式，或可從zip匯入。

**速記元件標籤宣告**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 图形链接 {#graphical-link}

此CTA元件可用來新增登陸頁面上具有連結的任何圖形影像。 影像可以是簡單的按鈕，也可以是任何圖形影像作為背景。 按一下影像時，使用者將被帶往元件屬性中指定的目標URL。 它是「號召性用語」群組的一部分。

支援的屬性

* 影像裁切、旋轉
* 暫留文字、說明、大小（以畫素為單位）
* 目標URL，支援第三方和AEM URL
* 頁面呈現選項（相同視窗、新視窗等）

HTML標籤，在匯入的zip檔案中包含圖形連結元件。 這裡href將對應到目標url，img src將是轉譯影像，「title」將被視為暫留文字等。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**速記元件標籤宣告**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>若要建立點進圖形連結，您必須使用將錨點標籤和影像標籤包裹在div中 `data-cq-component="clickthroughgraphicallink"` 屬性。
>
>例如： `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>不支援使用CSS將影像與錨點標籤建立關聯的其他方法，例如，下列標籤將無法運作：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>與相關聯的 `css .hasbackground { background-image: pathtoimage }`

### 潜在客户表单 {#lead-form}

潛在客戶表單是用於收集訪客/潛在客戶設定檔資訊的表單。 此資訊可以儲存並稍後使用，以根據資訊進行有效的行銷。 這些資訊通常包括標題、名稱、電子郵件、出生日期、地址、興趣等。 它是「CTA銷售機會表單」群組的一部分。

**支援的功能**

* 預先定義的銷售機會欄位 — 名字、姓氏、地址、dob、性別、關於、userId、emailId、提交按鈕可在sidekick中使用。 只需在潛在客戶表單中拖放所需的元件即可。
* 在這些元件的協助下，作者可以設計獨立的銷售機會表單，這些欄位對應到銷售機會表單欄位。 在獨立或匯入的zip應用程式中，使用者可以使用cq：form或cta潛在客戶表單欄位來新增額外欄位，並根據要求命名和設計。
* 使用CTA潛在客戶表單的特定預先定義名稱對應潛在客戶表單欄位，例如 — 潛在客戶表單中名字的firstName等。
* 未對應到潛在客戶表單的欄位將對應到cq：form元件 — 文字、單選按鈕、核取方塊、下拉選單、隱藏、密碼。
* 使用者可以使用「label」標籤提供標題，也可以使用樣式屬性「class」提供樣式（僅適用於CTA銷售機會表單元件）。
* 感謝頁面和訂閱清單可作為表單的隱藏引數提供（出現在index.htm中），或從「潛在客戶表單開始」的編輯列新增/編輯

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 可透過每個元件的編輯設定提供如下的限制：必要。

HTML標籤，在匯入的zip檔案中包含圖形連結元件。 這裡「firstName」對應至銷售機會表單firstName等，但核取方塊除外 — 這兩個核取方塊對應至cq：form下拉式清單元件。

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

AEM parsys元件是可包含其他AEM元件的容器元件。 可以在匯入的HTML中新增parsys元件。 這可讓使用者在登入頁面匯入後，也能新增/刪除可編輯的AEM元件。

段落系統可讓使用者使用Sidekick新增元件。

插入parsys元件的HTML標示( `foundation/components/parsys`)在design package的HTML中：

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

在HTML中包含上述標籤會執行下列動作：

* 在匯入設計套件後建立的登入頁面中插入AEM parsys元件(foundation/components/parsys)。
* 使用預設元件初始化Sidekick。 新元件可透過將元件從sidekick拖曳至parsys元件來新增至登入頁面。
* 兩個標題元件也是parsys的一部分。

### 目标 {#target}

目標元件會顯示頁面上的體驗內容。 您可以在行銷活動中建立許多體驗，且目標元件可動態地向造訪頁面的不同使用者顯示不同體驗的內容。

用於插入目標元件以及在行銷活動中建立不同體驗的html標籤：

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## 其他匯入選項 {#additional-importing-options}

除了指定匯入的元件是否為可編輯的AEM元件外，您也可以在匯入設計封裝之前設定下列專案：

* 擷取匯入HTML中定義的中繼資料，以設定頁面屬性。
* 在HTML中指定charset編碼。
* 覆蓋匯入工具頁面範本。

### 透過擷取匯入HTML中定義的中繼資料來設定頁面屬性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

下列在匯入HTML標頭中宣告的中繼資料應由設計匯入工具擷取並保留為屬性&quot;jcr：description&quot;：

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

在HTML標籤中設定的Lang屬性應由設計匯入工具擷取並保留為屬性&quot;jcr：language&quot;

* &lt;html lang=&quot;en&quot;>

### 指定html中的charset編碼 {#specifying-the-charset-encoding-in-the-html}

設計匯入工具會讀取匯入HTML中指定的編碼。 編碼可依照以下方式指定：

`<meta charset="UTF-8">`

*或*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果在匯入的HTML中未指定編碼，則設計匯入工具設定的預設編碼為UTF-8。

### 覆蓋範本 {#overlaying-template}

您可以在下列位置建立新範本，以覆蓋「空白登陸頁面」範本： `/apps/<appName>/designimporter/templates/<templateName>`

說明在AEM中建立新範本的步驟 [此處](/help/sites-developing/templates.md).

### 從登入頁面反向連結元件 {#referring-a-component-from-landing-page}

假設您有想要在HTML中使用data-cq-component屬性參照的元件，這樣設計匯入工具就會在此呈現元件。 例如，您想要參照表元件( `resourceType = /libs/foundation/components/table`)。 需要在HTML中新增下列內容：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component中的路徑應為元件的resourceType。

### 最佳实践 {#best-practices}

對於在匯入時標籤為進行元件轉換的元素，不建議使用類似於以下專案的CSS選取器。

| E > F | E元素的F元素子項 | [子組合子](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | 緊接在E元素前面的F元素 | [相鄰同層級組合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | 前面有E元素的F元素 | [一般同層級組合器](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E：root | E元素，檔案的根目錄 | [結構化的虛擬類別](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-child(n) | E元素，其父項的第n個子項 | [結構化的虛擬類別](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-last-child(n) | E元素，其父項的第n個子項，從最後一個專案開始計數 | [結構化的虛擬類別](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-of-type(n) | E元素，其型別的第n個同層級 | [結構化的虛擬類別](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-last-of-type(n) | E元素，其型別的第n個同層級，從最後一個同層級開始計數 | [結構化的虛擬類別](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

這是因為其他html元素，例如 &lt;div> 標籤會新增至匯入後產生的Html。

* 此外，不建議將依賴上述類似結構的指令碼與標示為要轉換至AEM元件的元素搭配使用。
* 在標籤標籤上使用樣式以進行元件轉換，例如 &lt;div data-cq-component=&quot;&amp;ast;&quot;> 不建議使用。
* 設計版面配置應遵循HTML5 Boilerplate的最佳實務。 深入瞭解： [https://html5boilerplate.com/](https://html5boilerplate.com/).

## 設定OSGI模組 {#configuring-osgi-modules}

公開可透過OSGI主控台設定的屬性的元件如下：

* 登陸頁面設計匯入工具
* 登陸頁面產生器
* 行動登陸頁面產生器
* 登陸頁面登入前置處理器

下表簡要說明屬性：

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>属性名称</strong></td>
   <td><strong>屬性說明 </strong></td>
  </tr>
  <tr>
   <td>登陸頁面設計匯入工具</td>
   <td>擷取篩選器</td>
   <td>用於篩選擷取檔案的規則運算式清單。 <br /> 符合任何指定模式的壓縮專案會從擷取中排除</td>
  </tr>
  <tr>
   <td>登陸頁面產生器</td>
   <td>檔案模式</td>
   <td>登入頁面產生器可設定為處理符合檔案模式所定義之規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td>行動登陸頁面產生器</td>
   <td>檔案模式</td>
   <td>登入頁面產生器可設定為處理符合檔案模式所定義之規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td> </td>
   <td>设备组</td>
   <td>要支援的裝置群組清單。</td>
  </tr>
  <tr>
   <td>登陸頁面登入前置處理器</td>
   <td>搜尋模式 </td>
   <td>要在封存專案內容中搜尋的模式。 此規則運算式與專案內容逐行比對。 相符時，相符的文字會以指定的取代模式取代。<br /> <br /> 請參閱下方關於登陸頁面登入前置處理器目前限制的附註。</td>
  </tr>
  <tr>
   <td> </td>
   <td>取代圖樣</td>
   <td>用來取代找到之相符的模式。 您可以使用$1、$2等規則運算式群組參考。 此外，此模式支援在匯入期間以實際值解析的{designPath}等關鍵字。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**登陸頁面登入前置處理器目前的限制：**
>如果您需要對搜尋模式進行任何變更，在開啟felix屬性編輯器時，您需要手動新增反斜線字元以逸出規則運算式中繼字元。 如果您未手動新增反斜線字元，則規則運算式會被視為無效，且不會取代舊的。
>
>例如，如果預設設定為
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>而且您需要更換 >`CQ_DESIGN_PATH` 替換為 `VIPURL` 在搜尋模式中，您的搜尋模式應如下所示：
`/\* *VIPURL *\*/ *(['"])`

## 疑难解答 {#troubleshooting}

匯入設計封裝時，您可能會遇到數個錯誤，如本節所述。

### 使用登陸頁面相關元件初始化Sidekick {#initialization-of-sidekick-with-landing-page-relevant-components}

如果設計套件包含parsys元件標籤，則在匯入後，sidekick會開始顯示登入頁面相關的元件。 您可以將新元件拖放至登陸頁面內的parsys元件上。 您也可以前往設計模式並將新元件新增到Sidekick。

### 匯入期間顯示的錯誤訊息 {#error-messages-displayed-during-import}

萬一發生任何錯誤（例如匯入的封裝不是有效的zip檔），設計匯入將不會匯入封裝，而是會在頁面上方拖放方塊上方顯示錯誤訊息。 此處提供錯誤情況的範例。 更正錯誤後，您可以將更新後的zip重新匯入至相同的空白登陸頁面。 擲回錯誤的不同情況如下：

* 匯入的設計封裝不是有效的zip封存。
* 匯入的設計封裝在頂層不包含index.html。

### 匯入後顯示警告 {#warnings-displayed-after-import}

萬一出現任何警告(例如HTML是指封裝內不存在的影像)，設計匯入工具會匯入zip，但同時在結果窗格中顯示問題/警告清單，按一下問題連結會顯示警告清單，指出設計封裝內的任何問題。 設計匯入工具攔截到警告並顯示警告的不同情況如下：

* HTML是指封裝內不存在的影像。
* HTML是指套件中不存在的指令碼。
* HTML是指封裝內不存在的樣式。

### ZIP檔案的檔案儲存在AEM中的何處？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

匯入登入頁面後，檔案（影像、css、js等） 在設計封裝內，儲存在AEM的以下位置：

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假設登入頁面是在We.Retail促銷活動下建立，且登入頁面的名稱為 **myBlankLandingPage** 則Zip檔案的儲存位置如下：

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 未保留格式設定 {#formatting-not-preserved}

建立CSS時，請注意下列限制：

如果文字和（可編輯的）影像如下所示：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

在類別上套用CSS `box` 如下所示：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

則 `box img` 用於design importer，因此產生的登陸頁面似乎並未保留格式。 若要解決此問題，請注意AEM會在CSS中新增div標籤，並據此重寫程式碼。 否則，某些CSS規則將無效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
此外，設計人員應注意，只有內部的程式碼 **id=cqcanvas** 標籤會由匯入工具識別，否則不會保留設計。
