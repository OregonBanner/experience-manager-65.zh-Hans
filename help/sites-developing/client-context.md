---
title: 詳細的使用者端內容
seo-title: Client Context in Detail
description: Client Context代表動態組合的使用者資料集合
seo-description: The Client Context represents a dynamically assembled collection of user data
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
feature: Context Hub
exl-id: 38b9a795-1c83-406c-ab13-b4456da938dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3008'
ht-degree: 0%

---

# 詳細的使用者端內容{#client-context-in-detail}

>[!NOTE]
>
>ContextHub已取代Client Context。 請參閱 [相關檔案](/help/sites-developing/contexthub.md) 以取得詳細資訊。

Client Context代表動態組合的使用者資料集合。 您可以使用資料來決定要在指定情境（內容目標定位）的網頁上顯示的內容。 資料也可用於網站分析以及頁面上的任何JavaScript。

Client Context主要包含下列幾個方面：

* 工作階段存放區，包含使用者資料。
* 顯示使用者資料並提供模擬使用者體驗工具的UI。
* A [javascript API](/help/sites-developing/ccjsapi.md) 用於與工作階段存放區互動。

建立獨立工作階段存放區並將其新增至Client Context，或建立繫結至Context Store元件的工作階段存放區。 AEM會安裝數個內容存放區元件，供您立即使用。 您可以使用這些元件作為元件的基礎。

如需有關開啟Client Context、設定其顯示的資訊和模擬使用者體驗的資訊，請參閱 [使用者端內容](/help/sites-administering/client-context.md).

## 工作階段存放區 {#session-stores}

Client Context包含包含使用者資料的各種工作階段存放區。 存放區資料來自下列來源：

* 使用者端網頁瀏覽器。
* 伺服器(請參閱 [JSONP存放區](/help/sites-administering/client-context.md#main-pars-variable-8) 儲存來自協力廠商的資訊)

Client Context架構提供 [javascript API](/help/sites-developing/ccjsapi.md) 可用來與工作階段存放區互動，以讀取和寫入使用者資料，以及接聽和回應存放區事件。 您也可以針對用於內容目標定位或其他用途的使用者資料建立工作階段存放區。

工作階段存放區資料會保留在使用者端上。 Client Context不會將資料寫回伺服器。 若要將資料傳送至伺服器，請使用表單或開發自訂javascript。

每個工作階段存放區都是屬性值配對的集合。 工作階段存放區代表（任何型別的）資料集合，其概念含義可由設計人員和/或開發人員決定。 以下範例javascript程式碼定義物件，該物件代表工作階段存放區可能包含的設定檔資料：

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

工作階段存放區可在多個瀏覽器工作階段之間持續存在，或僅可針對建立該存放區的瀏覽器工作階段持續。

>[!NOTE]
>
>存放區持續性使用瀏覽器存放區或Cookie (以 `SessionPersistence` Cookie)。 瀏覽器儲存空間較為常見。
>
>當瀏覽器關閉並重新開啟時，工作階段存放區可以載入來自持續存放區的值。 然後需要清除瀏覽器快取來移除舊值。

### 內容存放區元件 {#context-store-components}

內容存放區元件是可新增至Client Context的CQ元件。 通常，內容存放區元件會顯示與其相關聯之工作階段存放區的資料。 不過，前後關聯存放區元件顯示的資訊並不限於工作階段存放區資料。

前後關聯存放區元件可包含下列專案：

* 在Client Context中定義外觀的JSP指令碼。
* 在Sidekick中列出元件的屬性。
* 用於設定元件例證的「編輯」對話方塊。
* 初始化工作階段存放區的Javascript。

如需可新增至前後關聯存放區的已安裝前後關聯存放區元件的說明，請參閱 [可用的使用者端內容元件](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>頁面資料不再在使用者端內容中作為預設元件。 如有需要，您可以編輯使用者端內容、新增 **一般存放區屬性** 元件，然後設定以定義 **儲存** 作為 `pagedata`.

### 目標內容傳送 {#targeted-content-delivery}

設定檔資訊也用於傳遞 [目標內容](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_targetedcontentdelivery](assets/clientcontext_targetedcontentdelivery.png) ![clientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 新增使用者端內容至頁面 {#adding-client-context-to-a-page}

將Client Context元件加入網頁的正文區段，以啟用Client Context。 Client Context元件節點的路徑是 `/libs/cq/personalization/components/clientcontext`. 若要包含元件，請將下列程式碼新增至頁面元件的JSP檔案中 `body` 頁面元素：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext元件會使頁面載入實作Client Context的使用者端資料庫。

* Client Context JavaScript API。
* 支援工作階段儲存、事件管理等的Client Context架構。
* 已定義的區段。
* 為每個已新增至Client Context的內容存放區元件產生的init.js指令碼。
* （僅限作者執行個體） Client Context UI。

Client Context UI僅適用於作者執行個體。

## 延伸使用者端內容 {#extending-client-context}

若要擴充Client Context，請建立工作階段存放區，並選擇顯示存放區資料：

* 針對內容鎖定目標和網頁分析所需的使用者資料建立工作階段存放區。
* 建立內容存放區元件，讓管理員能夠設定關聯的工作階段存放區，並在Client Context中顯示存放區資料以供測試之用。

>[!NOTE]
>
>如果您有（或建立） `JSONP` 可提供資料的服務，只要使用 `JSONP` 內容存放區元件，並將其對應至JSONP服務。 這將處理工作階段存放區。

### 建立工作階段存放區 {#creating-a-session-store}

為需要新增到Client Context和從中擷取的資料建立工作階段存放區。 通常，您會使用以下程式來建立工作階段存放區：

1. 建立具有「 」的使用者端資料庫資料夾 `categories` 屬性值 `personalization.stores.kernel`. Client Context會自動載入此類別的使用者端程式庫。

1. 設定使用者端程式庫資料夾，使其相依於 `personalization.core.kernel` 使用者端資料庫資料夾。 此 `personalization.core.kernel` client library提供Client Context javascript API。

1. 新增建立和初始化工作階段存放區的javascript。

在personalization.stores.kernel使用者端資料庫中加入javascript會在載入Client Context架構時建立存放區。

>[!NOTE]
>
>如果您要建立工作階段存放區作為前後關聯存放區元件的一部分，您可以將javascript放在元件的init.js.jsp檔案中。 在此情況下，只有在將元件新增到Client Context時，才會建立工作階段存放區。

#### 工作階段存放區型別 {#types-of-session-stores}

工作階段存放區會在瀏覽器工作階段期間建立並可供使用，或保留在瀏覽器存放區或Cookie中。 Client Context JavaScript API定義了代表兩種資料儲存型別的幾個類別：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`：這些物件僅存在於頁面DOM中。 資料會在頁面存留期內建立並持續存在。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`：這些物件位於頁面DOM中，並持續存在於瀏覽器儲存空間或Cookie中。 資料可跨頁面和使用者工作階段使用。

此API還提供專門用於儲存JSON資料或JSONP資料的這些類別的擴充功能：

* 僅工作階段物件： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) 和 [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* 持續物件： [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) 和 [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### 建立工作階段存放區物件 {#creating-the-session-store-object}

使用者端程式庫資料夾的javascript會建立並初始化工作階段存放區。 然後必須使用內容存放區管理員註冊工作階段存放區。 以下範例會建立並註冊 [cq_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 物件。

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

為了儲存JSON資料，以下範例會建立並註冊 [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 物件。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 建立內容存放區元件 {#creating-a-context-store-component}

建立內容存放區元件，以在Client Context中呈現工作階段存放區資料。 建立後，您可以將內容存放區元件拖曳到Client Context上，以從工作階段存放區轉譯資料。 前後關聯存放區元件包含下列專案：

* 呈現資料的JSP指令碼。
* 編輯對話方塊。
* 用於初始化工作階段存放區的JSP指令碼。
* （選用）建立工作階段存放區的使用者端資料庫資料夾。 如果元件使用現有工作階段存放區，則不需要包含使用者端程式庫資料夾。

#### 擴充提供的內容存放區元件 {#extending-the-provided-context-store-components}

AEM提供您可以擴充的genericstore和genericstoreproperties內容存放區元件。 存放區資料的結構會決定您要擴展的元件：

* 屬性值組：擴充 `GenericStoreProperties` 元件。 此元件會自動轉譯屬性值組的存放區。 提供幾個互動點：

   * `prolog.jsp` 和 `epilog.jsp`：元件互動可讓您在元件呈現之前或之後新增伺服器端邏輯。

* 複雜資料：擴充 `GenericStore` 元件。 接著，您的工作階段存放區將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 使用兩個引數呼叫轉譯器函式：

   * `@param {String} store`
要呈現的存放區

   * `@param {String} divId`
必須轉譯存放區的div識別碼。

>[!NOTE]
>
>所有Client Context元件都是Generic Store或Generic Store Properties元件的延伸。 中安裝了幾個範例 `/libs/cq/personalization/components/contextstores` 資料夾。

#### 在Sidekick中設定外觀 {#configuring-the-appearance-in-sidekick}

編輯Client Context時，內容存放區元件會出現在Sidekick中。 與所有元件一樣， `componentGroup` 和 `jcr:title` 使用者端內容元件的屬性會決定元件的群組和名稱。

所有元件具有 `componentGroup` 屬性值 `Client Context` 預設會顯示在Sidekick中。 如果您對「 」使用不同的值 `componentGroup` 屬性，您必須使用設計模式手動將元件新增到Sidekick。

#### 內容存放區元件執行個體 {#context-store-component-instances}

將前後關聯存放區元件新增至Client Context時，會在下方建立代表元件例項的節點 `/etc/clientcontext/default/content/jcr:content/stores`. 此節點包含使用元件的編輯對話方塊設定的屬性值。

初始化Client Context時，會處理這些節點。

#### 初始化關聯的工作階段存放區 {#initializing-the-associated-session-store}

將init.js.jsp檔案新增至您的元件，以產生JavaScript程式碼，此程式碼會初始化您的內容存放區元件所使用的工作階段存放區。 例如，使用初始化指令碼來擷取元件的設定屬性，並使用它們來填入工作階段存放區。

當在製作和發佈執行個體的頁面載入上初始化使用者端內容時，產生的javascript會新增到頁面中。 此JSP會在載入及轉譯內容存放區元件執行個體之前執行。

程式碼必須將檔案的mime型別設定為 `text/javascript`，否則不會執行。

>[!CAUTION]
>
>init.js.jsp指令碼會在作者和發佈執行個體上執行，但前提是內容存放區元件已新增到Client Context。

下列程式會建立init.js.jsp指令碼檔案，並新增設定正確mime型別的程式碼。 執行存放區初始化的程式碼將會隨之執行。

1. 以滑鼠右鍵按一下前後關聯存放區元件節點，然後按一下「建立>建立檔案」。
1. 在「名稱」欄位中，輸入 `init.js.jsp` 然後按一下「確定」。
1. 在頁面頂端，新增下列程式碼，然後按一下「儲存全部」。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 轉譯genericstoreproperties元件的工作階段存放區資料 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式在Client Context中顯示工作階段存放區資料。

#### 顯示屬性資料 {#displaying-property-data}

個人化Taglib提供 `personalization:storePropertyTag` 標籤會顯示工作階段存放區中屬性的值。 若要使用標籤，請在JSP檔案中加入下列程式碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有以下格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

此 `propertyName` attribute是要顯示的存放區屬性名稱。 此 `store` attribute是註冊存放區的名稱。 以下範例標籤顯示 `authorizableId` 的屬性 `profile` 儲存：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML結構 {#html-structure}

personalization.ui使用者端程式庫資料夾(/etc/clientlibs/foundation/personalization/ui/themes/default)提供Client Context用來格式化HTML程式碼的CSS樣式。 下列程式碼說明用於顯示存放區資料的建議結構：

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

此 `/libs/cq/personalization/components/contextstores/profiledata` 內容存放區元件使用此結構來顯示設定檔工作階段存放區的資料。 此 `cq-cc-thumbnail` class會放置縮圖影像。 此 `cq-cc-store-property-level*x*` 類別會格式化英數字元資料：

* level0、level1和level2會垂直分佈，並使用白色字型。
* level3和任何其他層級會水準分佈，並使用具有較暗背景的白色字型。

![chlimage_1-4](assets/chlimage_1-4.png)

### 呈現一般存放區元件的工作階段存放區資料 {#rendering-session-store-data-for-genericstore-components}

若要使用一般存放區元件呈現存放區資料，您需要：

* 將personalization：storeRendererTag標籤新增至元件JSP指令碼，以識別工作階段存放區的名稱。
* 在工作階段存放區類別上實作轉譯器方法。

#### 識別一般存放區工作階段存放區 {#identifying-the-genericstore-session-store}

個人化Taglib提供 `personalization:storePropertyTag` 標籤會顯示工作階段存放區中屬性的值。 若要使用標籤，請在JSP檔案中加入下列程式碼行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

標籤具有以下格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 實作工作階段存放區轉譯器方法 {#implementing-the-session-store-renderer-method}

接著，您的工作階段存放區將需要「轉譯器」方法，每次需要轉譯元件時都會呼叫此方法。 使用兩個引數呼叫轉譯器函式：

* @param{String}存放區要轉譯的存放區
* @param要轉譯存放區之div的{String} divId ID。

## 與工作階段存放區互動 {#interacting-with-session-stores}

使用javascript與工作階段存放區互動。

### 存取工作階段存放區 {#accessing-session-stores}

取得工作階段存放區物件，以讀取或寫入存放區的資料。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 根據商店名稱提供對商店的存取。 取得後，請使用 [cq_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 或 [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) 以與存放區資料互動。

下列範例會取得 `profile` 儲存，然後擷取 `formattedName` 屬性。

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### 建立監聽器以回應工作階段存放區更新 {#creating-a-listener-to-react-to-a-session-store-update}

工作階段會儲存引發事件，因此可以根據這些事件新增接聽程式和觸發事件。

工作階段存放區建立在 `Observable` 模式。 它們會擴展 [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 可提供 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 方法。

下列範例會將監聽器新增至 `update` 以下專案的事件： `profile` 工作階段存放區。

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### 正在檢查工作階段存放區是否已定義及初始化 {#checking-that-a-session-store-is-defined-and-initialized}

工作階段存放區必須透過資料載入及初始化，才能使用。 下列因素可能會影響工作階段存放區可用性的時間：

* 頁面載入中
* JavaScript載入
* JavaScript執行時間
* XHR要求的回應時間
* 工作階段存放區的動態變更

使用 [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 物件的 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 只有在工作階段存放區可用的情況下才能存取這些方法。 這些方法可讓您註冊事件接聽程式，這些接聽程式會對工作階段註冊和初始化事件做出反應。

>[!CAUTION]
>
>如果您依賴其他商店，則需要滿足從未註冊商店的情況。

以下範例使用 `onStoreRegistered` 以下專案的事件： `profile` 工作階段存放區。 註冊存放區後，監聽器會新增至 `update` 工作階段存放區的事件。 更新存放區時， `<div class="welcome">` 頁面上的元素會以來自以下專案的名稱更新： `profile` 商店。

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### 從sessionpersistence Cookie排除屬性 {#excluding-a-property-from-the-sessionpersistence-cookie}

防止的屬性 `PersistedSessionStore` 永久(即將其從 `sessionpersistence` cookie)，將屬性新增至持續工作階段存放區的非持續屬性清單。

请参阅 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## 設定裝置滑桿 {#configuring-the-device-slider}

### 条件 {#conditions}

目前頁面必須有對應的行動頁面；這只有在頁面有設定了行動轉出設定( `rolloutconfig.path.toLowerCase` 包含 `mobile`)。

#### 配置 {#configuration}

從案頭頁面切換至行動裝置頁面時：

* 已載入行動頁面的DOM。
* 主要 `div` （必要）會擷取並插入目前的案頭頁面。

* 需要載入的CSS和body類別需要手動設定。

例如：

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## 範例：建立自訂內容存放區元件 {#example-creating-a-custom-context-store-component}

在此範例中，您會建立一個內容存放區元件，該元件會從外部服務擷取資料，並將其儲存在工作階段存放區中：

* 延伸genericstoreproperties元件。
* 使用CQ_Analytics.JSONPStore javascript物件初始化存放區。
* 呼叫JSONP服務以擷取資料並將其新增至存放區。
* 在Client Context中呈現資料。

### 新增地理位置元件 {#add-the-geoloc-component}

建立CQ應用程式並新增地理位置元件。

1. 在網頁瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 以滑鼠右鍵按一下 `/apps` 資料夾，然後按一下「建立>建立資料夾」。 指定名稱 `myapp` 然後按一下「確定」。
1. 同樣地，在下方 `myapp`，建立名為的資料夾 `contextstores`.&quot;
1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores` 資料夾，然後按一下「建立>建立元件」。 指定下列屬性值，然後按下一步：

   * 標籤： geoloc
   * 標題：位置存放區
   * 超級型別：cq/personalization/components/contextstores/genericstoreproperties
   * 群組：使用者端內容

1. 在「建立元件」對話方塊中，按一下每個頁面上的「下一步」，直到啟用「確定」按鈕為止，然後按一下「確定」。
1. 按一下「儲存全部」。

### 建立地理位置編輯對話方塊 {#create-the-geoloc-edit-dialog}

內容存放區元件需要編輯對話方塊。 地理位置編輯對話方塊將包含靜態訊息，指出沒有可設定的屬性。

1. 以滑鼠右鍵按一下 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` 節點，然後按一下「複製」。
1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores/geoloc` 節點，然後按一下「貼上」。
1. 刪除/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items節點下的所有子節點：

   * 儲存
   * 属性
   * 縮圖

1. 以滑鼠右鍵按一下 `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 節點，然後按一下「建立>建立節點」。 指定下列屬性值，然後按一下「確定」：

   * 名稱：靜態
   * 型別：cq：Widget

1. 將下列屬性新增至節點：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | cls | 字符串 | x-form-fieldset-description |
   | text | 字符串 | geoloc元件不需要設定。 |
   | xtype | 字符串 | 静态 |

1. 按一下「儲存全部」。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 建立初始化指令碼 {#create-the-initialization-script}

將init.js.jsp檔案新增至geoloc元件，並使用它來建立工作階段存放區、擷取位置資料，然後將其新增至存放區。

頁面載入Client Context時，會執行init.js.jsp檔案。 此時，Client Context JavaScript API已載入並可供您的指令碼使用。

1. 以滑鼠右鍵按一下/apps/myapp/contextstores/geoloc節點，然後按一下「建立>建立檔案」。 指定「名稱」init.js.jsp，然後按一下「確定」。
1. 將下列程式碼新增至頁面頂端，然後按一下「全部儲存」。

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### 轉譯Geoloc工作階段存放區資料 {#render-the-geoloc-session-store-data}

將程式碼新增至Geoloc元件的JSP檔案，以在Client Context中呈現存放區資料。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，開啟 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 檔案。
1. 在存根程式碼下方新增以下HTML程式碼：

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. 按一下「儲存全部」。

### 將元件新增至使用者端內容 {#add-the-component-to-client-context}

將「位置存放區」元件新增至「使用者端內容」，以便在頁面載入時將其初始化。

1. 開啟作者執行個體上的Geometrixx Outdoors首頁([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 按一下Ctrl-Alt-c (windows)或control-option-c (Mac)開啟「使用者端內容」。
1. 按一下「使用者端內容」頂端的編輯圖示，開啟「使用者端內容設計工具」。

   ![](do-not-localize/chlimage_1.png)

1. 將「位置存放區」元件拖曳至「使用者端內容」。

### 請參閱使用者端內容中的位置資訊 {#see-the-location-information-in-client-context}

以編輯模式開啟Geometrixx Outdoors首頁，然後開啟「使用者端內容」以檢視「位置存放區」元件的資料。

1. 開啟Geometrixx Outdoors網站的英文頁面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 若要開啟「使用者端內容」，請按Ctrl-Alt-c (windows)或control-option-c (Mac)。

## 建立自訂使用者端內容 {#creating-a-customized-client-context}

若要建立第二個使用者端內容，您需要複製分支：

`/etc/clientcontext/default`

* 子資料夾：
   `/content`
將包含自訂使用者端內容的內容。

* 資料夾：
   `/contextstores`
可讓您為內容存放區定義不同的設定。

若要使用自訂的使用者端內容，請編輯屬性
`path`
使用者端前後關聯元件的設計樣式中（如頁面範本中所包含）。 例如，作為的標準位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
