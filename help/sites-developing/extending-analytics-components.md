---
title: 將Adobe Analytics追蹤新增至元件
seo-title: Adding Adobe Analytics Tracking to Components
description: 將Adobe Analytics追蹤新增至元件
seo-description: null
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# 將Adobe Analytics追蹤新增至元件{#adding-adobe-analytics-tracking-to-components}

## 在頁面元件中包含Adobe Analytics模組 {#including-the-adobe-analytics-module-in-a-page-component}

頁面範本元件(例如 `head.jsp, body.jsp`)需要JSP包含才能載入ContextHub和Adobe Analytics整合(這是Cloud Services的一部分)。 全部包括載入JavaScript檔案。

ContextHub專案應直接包含在 `<head>` 標籤中，而Cloud Services應包含在 `<head>` 而且早於 `</body>` 區段；例如：

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

此 `contexthub` 您插入在後的指令碼 `<head>` 元素會將ContextHub功能新增至頁面。

此 `cloudservices` 您在中新增的指令碼 `<head>` 和 `<body>` 區段會套用至新增至頁面的雲端服務設定。 (如果頁面使用多個Cloud Services組態，您只需包含一次ContextHub jsp和Cloud Servicesjsp。)

將Adobe Analytics架構新增至頁面時， `cloudservices` 指令碼會產生與Adobe Analytics相關的javascript和對使用者端資料庫的參考，類似於以下範例：

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

所有AEM範例網站(例如Geometrixx Outdoors)皆包含此程式碼。

### sitecatalystAfterCollect事件 {#the-sitecatalystaftercollect-event}

此 `cloudservices` 指令碼觸發 `sitecatalystAfterCollect` 事件：

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

觸發此事件即表示頁面追蹤已完成。 如果您正在此頁面上執行其他追蹤操作，您應該接聽此事件，而不是檔案載入或檔案就緒事件。 使用 `sitecatalystAfterCollect` 事件可避免衝突或其他無法預測的行為。

>[!NOTE]
>
>此 `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 程式庫中包含來自Adobe Analytics的程式碼 `s_code.js` 檔案。

## 對自訂元件實作Adobe Analytics追蹤 {#implementing-adobe-analytics-tracking-for-custom-components}

啟用您的AEM元件，以與Adobe Analytics架構互動。 然後，設定您的架構，讓Adobe Analytics追蹤元件資料。

當您編輯框架時，與Adobe Analytics框架互動的元件會顯示在SideKick中。 將元件拖曳至框架後，元件屬性隨即顯示，然後您就可以使用Adobe Analytics屬性加以對應。 (請參閱 [設定基本追蹤的框架](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

當元件具有名為的子節點時，元件可以與Adobe Analytics架構互動 `analytics`. 此 `analytics` 節點具有下列屬性：

* `cq:trackevents`：識別元件公開的CQ事件。 （請參閱自訂事件）。
* `cq:trackvars`：為與Adobe Analytics屬性對應的CQ變數命名。
* `cq:componentName`：顯示在Sidekick中的元件名稱。
* `cq:componentGroup`：Sidekick中包含元件的群組。

元件JSP中的程式碼會將JavaScript新增至觸發追蹤的頁面，並定義要追蹤的資料。 Javascript中使用的事件名稱和資料名稱必須與 `analytics` 節點屬性。

* 在頁面載入時，使用data-tracking屬性追蹤事件資料。 (請參閱 [追蹤頁面載入時的自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* 使用CQ_Analytics.record函式來追蹤使用者與頁面功能互動時的事件資料。 (請參閱 [頁面載入後追蹤自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

當您使用這些資料追蹤方法時，Adobe Analytics整合模組會自動執行對Adobe Analytics的呼叫，以記錄事件和資料。

### 範例：追蹤topnav點按 {#example-tracking-topnav-clicks}

擴充Foundation Topnav元件，讓Adobe Analytics能夠追蹤頁面頂端導覽連結的點按次數。 當導覽連結被點按時，Adobe Analytics會記錄被點按的連結以及被點按的頁面。

下列程式要求您已執行下列工作：

* 已建立CQ應用程式。
* 已建立Adobe Analytics設定和Adobe Analytics架構。

#### 複製topnav元件 {#copy-the-topnav-component}

將topnav元件複製到CQ應用程式。 此程式要求您的應用程式必須以CRXDE Lite設定。

1. 以滑鼠右鍵按一下 `/libs/foundation/components/topnav` 節點，然後按一下「複製」。
1. 以滑鼠右鍵按一下應用程式資料夾下方的「元件」資料夾，然後按一下「貼上」。
1. 按一下「儲存全部」。

#### 將topnav與Adobe Analytics框架整合 {#integrating-topnav-with-the-adobe-analytics-framework}

設定topnav元件並編輯JSP檔案，以定義追蹤事件和資料。

1. 以滑鼠右鍵按一下topnav節點，然後按一下「建立>建立節點」。 指定下列屬性值，然後按一下「確定」：

   * 名称: `analytics`
   * 类型: `nt:unstructured`

1. 將下列屬性新增至Analytics節點，為追蹤事件命名：

   * 名稱： cq：trackevents
   * 型別：字串
   * 值： topnavClick

1. 將下列屬性新增至Analytics節點，為資料變數命名：

   * 名稱：cq：trackvars
   * 型別：字串
   * 值： topnavTarget，topnavLocation

1. 將下列屬性新增至Analytics節點，為Sidekick的元件命名：

   * 名稱：cq：componentName
   * 型別：字串
   * 值： topnav (tracking)

1. 將下列屬性新增至Analytics節點，為Sidekick的元件群組命名：

   * 名稱：cq：componentGroup
   * 型別：字串
   * 值：一般

1. 按一下「儲存全部」。
1. 開啟 `topnav.jsp` 檔案。
1. 在元素中，新增下列屬性：

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. 在頁面底部，新增下列javascript程式碼：

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. 按一下「儲存全部」。

的內容 `topnav.jsp` 檔案應如下所示：

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>通常需要從ContextHub追蹤資料。 如需使用javascript取得此資訊的詳細資訊，請參閱 [存取ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### 將追蹤元件新增至Sidekick {#adding-the-tracking-component-to-sidekick}

將啟用Adobe Analytics追蹤的元件新增至Sidekick，以便將其新增至您的架構。

1. 從Adobe Analytics設定開啟您的Adobe Analytics架構。 ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 在Sidekick上，按一下「設計」按鈕。

   ![](assets/chlimage_1a.png)

1. 在連結追蹤設定區域中，按一下設定繼承。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 在「允許的元件」清單中，選取「一般」區段中的topnav （追蹤），然後按一下「確定」。
1. 展開Sidekick以進入編輯模式。 元件現在可在「一般」群組中使用。

#### 將topnav元件新增至您的架構 {#adding-the-topnav-component-to-your-framework}

將topnav元件拖曳至您的Adobe Analytics架構，並將元件變數和事件對應至Adobe Analytics變數和事件。 (請參閱 [設定基本追蹤的框架](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

topnav元件現在已與Adobe Analytics框架整合。 將元件新增至頁面時，按一下頂端導覽列中的專案會導致將追蹤資料傳送至Adobe Analytics。

### 將s.products資料傳送至Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

元件可產生傳送至Adobe Analytics之s.products變數的資料。 設計您的元件以貢獻至s.products變數：

* 記錄名為的值 `product` 特定結構的URL。
* 公開以下專案的資料成員： `product` 值，以便能在Adobe Analytics架構中以Adobe Analytics變數對應。

Adobe Analytics s.products變數會使用以下語法：

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics整合模組會建構 `s.products` 變數，使用 `product` AEM元件產生的值。 此 `product` AEM元件所產生javascript中的值是具有以下結構的值陣列：

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

當省略了資料專案時 `product` 值，則會以s.products中的空字串形式傳送。

>[!NOTE]
>
>當沒有任何事件與產品值相關聯時，Adobe Analytics會使用 `prodView` 事件（預設）。

此 `analytics` 元件的節點必須使用下列專案公開變數名稱： `cq:trackvars` 屬性：

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

電子商務模組提供數個會產生s.products變數資料的元件。 例如，submitorder元件([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))會產生與下列範例類似的javascript：

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### 限制追蹤呼叫的大小 {#limiting-the-size-of-tracking-calls}

一般而言，網頁瀏覽器會限制GET要求的大小。 由於CQ產品和SKU值是存放庫路徑，因此包含多個值的產品陣列可能會超過請求大小限制。 因此，您的元件應限制 `product` 每個的陣列 `CQ_Analytics.record function`. 如果您需要追蹤的專案數量可能超過限制，請建立多個函式。

例如，電子商務提交訂單元件會限制 `product` 呼叫中的專案4個。 當購物車包含超過四個產品時，會產生多個產品 `CQ_Analytics.record` 函式。
