---
title: Client Context详解
seo-title: Client Context详解
description: Client Context表示动态组合的用户数据集合
seo-description: Client Context表示动态组合的用户数据集合
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Client Context详解{#client-context-in-detail}

>[!NOTE]
>
>Client Context已被ContextHub取代。 有关详细信息，请 [参阅相关](/help/sites-developing/contexthub.md) 文档。

Client Context表示动态组合的用户数据集合。 您可以使用数据确定在给定情况下要在网页上显示的内容（内容定位）。 该数据还可用于网站分析以及页面上的任何javascript。

Client context主要包括以下方面：

* 包含用户数据的会话存储。
* 显示用户数据并提供模拟用户体验的工具的UI。
* 用于 [与会话商店交互的Javascript API](/help/sites-developing/ccjsapi.md) 。

要创建独立会话存储并将其添加到Client Context，或创建绑定到Context Store组件的会话存储。 AEM会安装多个您可以立即使用的Context store组件。 您可以将这些组件用作组件的基础。

有关打开Client Context、配置其显示的信息以及模拟用户体验的信息，请参阅 [Client Context](/help/sites-administering/client-context.md)。

## 会话商店 {#session-stores}

Client Context包括包含用户数据的各种会话存储。 存储数据来自以下来源：

* 客户端Web浏览器。
* 服务器(有关存储 [来自第三方源的信息](/help/sites-administering/client-context.md#main-pars-variable-8) ，请参阅JSONP商店)

Client Context框架提供了 [javascript API](/help/sites-developing/ccjsapi.md) ，您可以使用它与会话存储进行交互以读取和写入用户数据，以及侦听和响应存储事件。 您还可以为用于内容定位或其他用途的用户数据创建会话存储。

会话存储数据保留在客户端上。 Client Context不会将数据写回服务器。 要向服务器发送数据，请使用表单或开发自定义javascript。

每个会话存储都是属性值对的集合。 会话存储表示（任何类型）的数据集合，其概念含义由设计人员和／或开发人员决定。 以下示例javascript代码定义了一个对象，它表示会话存储可能包含的配置文件数据：

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

会话存储可以跨浏览器会话持续，也只能在创建会话的浏览器会话中持续。

>[!NOTE]
>
>存储持久性使用浏览器存储或cookie( `SessionPersistence` cookie)。 浏览器存储更常见。
>
>当浏览器关闭并重新打开时，会话存储区可以加载来自保留存储区的值。 然后，需要清除浏览器缓存才能删除旧值。

### 上下文存储组件 {#context-store-components}

上下文存储组件是可添加到Client context的CQ组件。 通常，上下文存储组件显示来自与其关联的会话存储的数据。 但是，上下文存储组件显示的信息并不局限于会话存储数据。

上下文存储组件可以包括以下项目：

* 定义Client context中外观的JSP脚本。
* 用于在Sidekick中列出组件的属性。
* 编辑用于配置组件实例的对话框。
* 初始化会话存储的Javascript。

有关可添加到Context store的已安装Context Store组件的说明，请参阅可 [用的Client Context Components](/help/sites-administering/client-context.md#available-client-context-components)。

>[!NOTE]
>
>页面数据不再作为默认组件存在于Client Context中。 如果需要，您可以通过编辑Client Context，添加“通用商店属性”组 **件** ，然后将其配置为将 **Store** 定义为 `pagedata`。

### 目标内容交付 {#targeted-content-delivery}

配置文件信息还用于提供目 [标内容](/help/sites-authoring/content-targeting-touch.md)。

![clientcontext_targetedcontentdeliveryclientcontext](assets/clientcontext_targetedcontentdelivery.png) _ ![targetcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 将Client Context添加到页面 {#adding-client-context-to-a-page}

将Client Context组件包含到网页的正文部分以启用Client Context。 Client Context组件节点的路径为 `/libs/cq/personalization/components/clientcontext`。 要包含该组件，请将以下代码添加到页面组件的JSP文件中，该文件位于页面元 `body` 素的正下方：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext组件使页面加载实现Client context的客户端库。

* Client Context javascript API。
* 支持会话存储、事件管理等的Client Context框架。
* 定义的区段。
* 为已添加到Client Context的每个上下文存储组件生成的init.js脚本。
* （仅限作者实例）Client Context UI。

Client Context UI仅在创作实例上可用。

## 扩展Client Context {#extending-client-context}

要扩展Client Context，请创建会话存储并（可选）显示存储数据：

* 为内容定位和网络分析所需的用户数据创建会话存储。
* 创建一个上下文存储组件，使管理员能够配置关联的会话存储，并在Client context中显示存储数据以用于测试目的。

>[!NOTE]
>
>如果您有（或创建）可 `JSONP` 以提供数据的服务，您只需使用上下文存储组 `JSONP` 件并将其映射到JSONP服务。 这将处理会话存储。

### 创建会话存储 {#creating-a-session-store}

为需要添加到Client Context并从Client context中检索的数据创建会话存储。 通常，可使用以下过程创建会话存储：

1. 创建属性值为的客户端 `categories` 库文件夹 `personalization.stores.kernel`。 Client Context会自动加载此类别的客户端库。

1. 配置客户端库文件夹，使其对客户端库文件夹具 `personalization.core.kernel` 有依赖性。 客 `personalization.core.kernel` 户端库提供Client Context javascript API。

1. 添加创建和初始化会话存储的javascript。

在personalization.stores.kernel客户端库中包含javascript会导致在加载Client Context框架时创建商店。

>[!NOTE]
>
>如果要创建会话存储作为上下文存储组件的一部分，则可以将javascript放置到组件的init.js.jsp文件中。 在这种情况下，仅当将组件添加到Client Context时，才会创建会话存储。

#### 会话存储的类型 {#types-of-session-stores}

会话存储在浏览器会话期间创建并可用，或在浏览器存储或cookie中保留。 Client Context javascript API定义几个类，它们表示两种类型的数据存储：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:这些对象仅驻留在页面DOM中。 数据将在页面的生命周期中创建并保留。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:这些对象驻留在页面DOM中，并保留在浏览器存储或cookie中。 数据可跨页面和用户会话使用。

API还提供了这些类的扩展，这些类专门用于存储JSON数据或JSONP数据：

* 仅会话对象： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore)[和CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore)。

* 保留的对象： [CQ_Analytics.PersitedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore)[和CQ_Analytics.PersitedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore)。

#### 创建会话存储对象 {#creating-the-session-store-object}

客户端库文件夹的javascript将创建并初始化会话存储。 然后，必须使用上下文存储管理器注册会话存储。 以下示例创建并注册 [CQ_Analytics.SessionStore对象](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 。

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

为了存储JSON数据，以下示例创建并注册 [CQ_Analytics.JSONStore对象](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 创建上下文存储组件 {#creating-a-context-store-component}

创建上下文存储组件，以在Client context中呈现会话存储数据。 创建后，您可以将上下文存储组件拖动到Client Context上以从会话存储中呈现数据。 上下文存储组件由以下项目组成：

* 用于呈现数据的JSP脚本。
* 编辑对话框。
* 用于初始化会话存储的JSP脚本。
* （可选）创建会话存储的客户端库文件夹。 如果组件使用现有会话存储，则无需包括客户端库文件夹。

#### 扩展提供的上下文存储组件 {#extending-the-provided-context-store-components}

AEM提供可扩展的常规存储和常规存储属性上下文存储组件。 存储数据的结构决定了您扩展的组件：

* 属性——值对：扩展组 `GenericStoreProperties` 件。 此组件自动呈现属性——值对的存储。 提供了几个交互点：

   * `prolog.jsp` 和 `epilog.jsp`:组件交互，允许您在组件呈现之前或之后添加服务器端逻辑。

* 复杂数据：扩展组 `GenericStore` 件。 然后，您的会话存储将需要一个“渲染器”方法，该方法将在每次需要渲染组件时被调用。 使用两个参数调用呈示器函数：

   * `@param {String} store`
要渲染的商店

   * `@param {String} divId`
必须向其中呈现存储的div的ID。

>[!NOTE]
>
>所有Client Context组件都是Generic Store或Generic Store Properties组件的扩展。 文件夹中安装了几个 `/libs/cq/personalization/components/contextstores` 示例。

#### 配置Sidekick中的外观 {#configuring-the-appearance-in-sidekick}

编辑Client Context时，上下文存储组件显示在Sidekick中。 与所有组件一样，Client Context `componentGroup` 组件 `jcr:title` 的属性和属性决定组件的组和名称。

默认情况下，所有 `componentGroup` 属性值为 `Client Context` 的组件都显示在Sidekick中。 如果对属性使用其他值， `componentGroup` 则必须使用“设计”模式将组件手动添加到Sidekick。

#### 上下文存储组件实例 {#context-store-component-instances}

将上下文存储组件添加到Client Context时，将在下面创建表示组件实例的节点 `/etc/clientcontext/default/content/jcr:content/stores`。 此节点包含使用组件的编辑对话框配置的属性值。

初始化Client Context时，这些节点将被处理。

#### 初始化关联的会话存储 {#initializing-the-associated-session-store}

将init.js.jsp文件添加到组件以生成Javascript代码，该代码初始化上下文存储组件使用的会话存储。 例如，使用初始化脚本检索组件的配置属性，并使用这些属性填充会话存储。

在创作实例和发布实例的页面加载时，当Client Context初始化时，将生成的javascript添加到页面。 在加载和呈现上下文存储组件实例之前执行此JSP。

代码必须将文件的mime类型设置为 `text/javascript`，否则不会执行它。

>[!CAUTION]
>
>init.js.jsp脚本在创作和发布实例上执行，但仅当上下文存储组件添加到Client Context时执行。

以下过程创建init.js.jsp脚本文件并添加设置正确mime类型的代码。 接下来是执行存储初始化的代码。

1. 右键单击上下文存储组件节点，然后单击创建>创建文件。
1. 在“名称”(Name)字段中，键入 `init.js.jsp` 并单击“确定”(OK)。
1. 在页面顶部，添加以下代码，然后单击“全部保存”。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 呈现会话存储数据以用于生成存储属性组件 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式在Client Context中显示会话存储数据。

#### 显示属性数据 {#displaying-property-data}

个性化标签库提 `personalization:storePropertyTag` 供显示会话商店中属性值的标签。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

属 `propertyName` 性是要显示的存储属性的名称。 属 `store` 性是已注册存储的名称。 以下示例标记显示存储 `authorizableId` 区属性的 `profile` 值：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML结构 {#html-structure}

personalization.ui客户端库文件夹(/etc/clientlibs/foundation/personalization/ui/themes/default)提供Client context用于设置HTML代码格式的CSS样式。 以下代码说明了用于显示存储数据的建议结构：

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

上下文 `/libs/cq/personalization/components/contextstores/profiledata` 存储组件使用此结构显示来自配置文件会话存储的数据。 该类 `cq-cc-thumbnail` 放置缩略图图像。 这些 `cq-cc-store-property-level*x*` 类格式化字母数字数据：

* level0、level1和level2垂直分布，并使用白色字体。
* level3和任何其他级别水平分布，并使用背景较暗的白色字体。

![chlimage_1-4](assets/chlimage_1-4.png)

### 为通用存储组件渲染会话存储数据 {#rendering-session-store-data-for-genericstore-components}

要使用常规存储组件渲染存储数据，您需要：

* 将personalization:storeRendererTag标签添加到组件JSP脚本中，以标识会话存储的名称。
* 在会话存储类上实现呈示器方法。

#### 识别Genericstore会话存储 {#identifying-the-genericstore-session-store}

个性化标签库提 `personalization:storePropertyTag` 供显示会话商店中属性值的标签。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 实现会话存储渲染器方法 {#implementing-the-session-store-renderer-method}

然后，您的会话存储将需要一个“渲染器”方法，该方法将在每次需要渲染组件时被调用。 使用两个参数调用呈示器函数：

* @param {String} store要呈现的商店
* @param {String} divId必须呈现到其中的存储的div。

## 与会话存储交互 {#interacting-with-session-stores}

使用javascript与会话商店交互。

### 访问会话存储 {#accessing-session-stores}

获取会话存储对象以读取数据或将数据写入存储。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 根据商店名称提供对商店的访问。 获取后，使用 [CQ_Analytics.SessionStore或](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) CQ_Analytics.PersistedSessionStore [](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) (CQ_Analytics.PersistedSessionStore)的方法与存储数据交互。

以下示例获取存 `profile` 储，然后从存储 `formattedName` 检索属性。

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

### 创建监听器以对会话存储更新做出响应 {#creating-a-listener-to-react-to-a-session-store-update}

会话存储火事件，因此可以添加监听器并基于这些事件触发事件。

会话存储器基于该模式 `Observable` 构建。 它们扩 [ 展了 `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 提供该方法 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 的功能。

以下示例将监听器添加到会 `update` 话存储的事 `profile` 件中。

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

### 检查是否定义和初始化会话存储 {#checking-that-a-session-store-is-defined-and-initialized}

在加载会话存储并使用数据进行初始化之前，会话存储才可用。 以下因素可能会影响会话存储可用性的时间：

* 页面加载
* JavaScript加载
* JavaScript执行时间
* XHR请求的响应时间
* 对会话存储的动态更改

仅当 [会话存储可用时，才使用CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 对象的 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 方法访问会话存储。 这些方法使您能够注册对会话注册和初始化事件做出响应的事件监听器。

>[!CAUTION]
>
>如果您依赖其他商店，则需要满足商店从未注册的情况。

以下示例使用 `onStoreRegistered` 会话存储的 `profile` 事件。 注册存储时，会向会话存储的事 `update` 件添加监听器。 更新商店后，页面上的元素 `<div class="welcome">` 的内容将更新为商店中的名 `profile` 称。

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

### 从会话持久性Cookie中排除属性 {#excluding-a-property-from-the-sessionpersistence-cookie}

要防止某个属性被 `PersistedSessionStore` 保留(即从 `sessionpersistence` cookie中排除它)，请将该属性添加到已保留会话存储的非持续属性列表中。

See ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## 配置设备滑块 {#configuring-the-device-slider}

### 条件 {#conditions}

当前页面必须具有相应的移动页面；这仅在页面配置了LiveCopy并配置了移动转出配置(包含 `rolloutconfig.path.toLowerCase` )时 `mobile`确定。

#### 配置 {#configuration}

从桌面页面切换到其移动对等页面时：

* 移动页面的DOM已加载。
* 将提取 `div` 包含内容的主页（必需）并将其注入到当前桌面页面。

* 需要手动配置需要加载的CSS和正文类。

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

## 示例：创建自定义上下文存储组件 {#example-creating-a-custom-context-store-component}

在此示例中，您创建一个上下文存储组件，该组件从外部服务检索数据并将其存储在会话存储中：

* 扩展了常规存储属性组件。
* 使用CQ_Analytics.JSONPStore javascript对象初始化存储。
* 调用JSONP服务以检索数据并将其添加到存储。
* 在Client Context中呈现数据。

### 添加geoloc组件 {#add-the-geoloc-component}

创建CQ应用程序并添加geoloc组件。

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 右键单击文件夹， `/apps` 然后单击创建>创建文件夹。 指定名称，然 `myapp` 后单击“确定”。
1. 同样，在下面 `myapp`创建一个名为的文件夹 `contextstores`。&quot;
1. 右键单击文件夹， `/apps/myapp/contextstores` 然后单击创建>创建组件。 指定以下属性值，然后单击“下一步”:

   * 标签：geoloc
   * 标题：位置存储
   * 超级类型：cq/personalization/components/contextstores/generaticstoreproperties
   * 组：Client Context

1. 在创建组件对话框中，单击每页上的下一步，直到启用确定按钮，然后单击确定。
1. 单击“全部保存”。

### 创建geoloc编辑对话框 {#create-the-geoloc-edit-dialog}

上下文存储组件需要一个编辑对话框。 geoloc编辑对话框将包含一条静态消息，指示没有要配置的属性。

1. 右键单击该节 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` 点，然后单击复制。
1. 右键单击该节 `/apps/myapp/contextstores/geoloc` 点，然后单击粘贴。
1. 删除/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items节点下的所有子节点：

   * 商店
   * 属性
   * 缩略图

1. 右键单击该节点， `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 然后单击创建>创建节点。 指定以下属性值，然后单击“确定”:

   * 名称：静态
   * 类型：cq：构件

1. 将以下属性添加到节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | cls | 字符串 | x-form-fieldset-description |
   | 文本 | 字符串 | geoloc组件不需要配置。 |
   | xtype | 字符串 | 静态 |

1. 单击“全部保存”。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 创建初始化脚本 {#create-the-initialization-script}

将init.js.jsp文件添加到geoloc组件中，然后使用它创建会话存储、检索位置数据并将其添加到存储。

init.js.jsp文件在页面加载Client context时执行。 此时，Client Context javascript API已加载并可用于您的脚本。

1. 右键单击/apps/myapp/contextstores/geoloc节点，然后单击创建>创建文件。 指定init.js.jsp的名称，然后单击“确定”。
1. 将以下代码添加到页面顶部，然后单击“全部保存”。

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

### 呈现geoloc会话存储数据 {#render-the-geoloc-session-store-data}

将代码添加到geoloc组件的JSP文件，以在Client context中呈现存储数据。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，打开文 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 件。
1. 在存根代码下添加以下HTML代码：

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

1. 单击“全部保存”。

### 将组件添加到Client Context {#add-the-component-to-client-context}

将“位置存储”组件添加到Client Context，以便在加载页面时对其进行初始化。

1. 在创作实例上打开Geometrixx Outdoors主页([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 单击Ctrl-Alt-c(Windows)或control-option-c(Mac)以打开Client Context。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![](do-not-localize/chlimage_1.png)

1. 将位置存储组件拖动到Client Context。

### 请参阅Client context中的位置信息 {#see-the-location-information-in-client-context}

在编辑模式下打开Geometrixx Outdoors主页，然后打开Client Context以查看位置存储组件中的数据。

1. 打开Geometrixx Outdoors站点的“英语”页面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 要打开Client Context，请按Ctrl-Alt-c(Windows)或control-option-c(Mac)。

## 创建自定义的Client Context {#creating-a-customized-client-context}

要创建第二个Client Context，您需要复制分支：

`/etc/clientcontext/default`

* 子文件夹：
   `/content`
将包含自定义客户端上下文的内容。

* 文件夹：
   `/contextstores`
允许您为上下文存储定义不同的配置。

要使用自定义的Client Context，请按页面模`path`板中包含的Client Context组件的设计样式编辑属性。 例如，作为以下项的标准位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
