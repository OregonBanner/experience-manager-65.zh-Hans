---
title: Client Context详细信息
seo-title: Client Context详细信息
description: Client Context表示动态组合的用户数据集合
seo-description: Client Context表示动态组合的用户数据集合
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
source-wordcount: '3025'
ht-degree: 0%

---

# Client Context详细信息{#client-context-in-detail}

>[!NOTE]
>
>Client Context已被ContextHub取代。 有关详细信息，请参阅[相关文档](/help/sites-developing/contexthub.md)。

Client Context表示动态组合的用户数据集合。 您可以使用数据确定在给定情况下要在网页上显示的内容（内容定位）。 该数据也可用于网站分析以及页面上的任何javascript。

Client Context主要包括以下方面：

* 包含用户数据的会话存储。
* 用于显示用户数据并提供模拟用户体验的工具的UI。
* 用于与会话存储交互的[javascript API](/help/sites-developing/ccjsapi.md)。

要创建独立会话存储并将其添加到Client Context，或创建与Context Store组件绑定的会话存储。 AEM会安装多个可立即使用的上下文存储组件。 您可以将这些组件用作组件的基础。

有关打开Client Context、配置其显示的信息以及模拟用户体验的信息，请参阅[Client Context](/help/sites-administering/client-context.md)。

## 会话存储{#session-stores}

Client Context包括包含用户数据的各种会话存储。 存储数据来自以下来源：

* 客户端Web浏览器。
* 服务器（请参阅[JSONP存储](/help/sites-administering/client-context.md#main-pars-variable-8)以存储来自第三方源的信息）

Client Context框架提供了[javascript API](/help/sites-developing/ccjsapi.md)，您可以使用该API与会话存储进行交互以读取和写入用户数据，以及侦听和响应存储事件。 您还可以为用于内容定位或其他目的的用户数据创建会话存储。

会话存储数据会保留在客户端上。 Client Context不会将数据写回服务器。 要将数据发送到服务器，请使用表单或开发自定义Javascript。

每个会话存储都是属性值对的集合。 会话存储表示（任何类型）的数据集合，其概念含义可由设计人员和/或开发人员决定。 以下示例Javascript代码定义了一个对象，该对象表示会话存储可能包含的配置文件数据：

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

会话存储可以在浏览器会话中持久保留，或者只能在创建会话的浏览器会话中持续。

>[!NOTE]
>
>存储持久性使用浏览器存储或Cookie(`SessionPersistence` Cookie)。 浏览器存储更为常见。
>
>关闭并重新打开浏览器后，可以使用持久存储中的值加载会话存储。 然后需要清除浏览器缓存才能删除旧值。

### 上下文存储组件{#context-store-components}

上下文存储组件是可添加到Client Context的CQ组件。 通常，上下文存储组件显示来自与其关联的会话存储的数据。 但是，上下文存储组件显示的信息并不限于会话存储数据。

上下文存储组件可以包含以下项目：

* 在Client Context中定义外观的JSP脚本。
* 用于在Sidekick中列出组件的属性。
* 编辑用于配置组件实例的对话框。
* 初始化会话存储的Javascript。

有关可添加到上下文存储的已安装上下文存储组件的说明，请参阅[可用的客户端上下文组件](/help/sites-administering/client-context.md#available-client-context-components)。

>[!NOTE]
>
>页面数据不再作为默认组件显示在客户端上下文中。 如果需要，您可以添加此组件，方法是编辑客户端上下文，添加&#x200B;**通用存储属性**&#x200B;组件，然后将其配置为将&#x200B;**存储**&#x200B;定义为`pagedata`。

### 目标内容交付{#targeted-content-delivery}

用户档案信息还用于传送[目标内容](/help/sites-authoring/content-targeting-touch.md)。

![clientcontext_](assets/clientcontext_targetedcontentdelivery.png) ![targetedcontentdeliveryclientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 向页面{#adding-client-context-to-a-page}添加Client Context

将Client Context组件包含到网页的正文部分以启用Client Context。 Client Context组件节点的路径为`/libs/cq/personalization/components/clientcontext`。 要包含该组件，请将以下代码添加到页面组件的JSP文件中，该文件位于页面`body`元素的正下方：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext组件会导致页面加载实施Client Context的客户端库。

* Client Context Javascript API。
* 支持会话存储、事件管理等的Client Context框架。
* 定义的区段。
* 为已添加到Client Context的每个上下文存储组件生成的init.js脚本。
* （仅限创作实例）Client Context UI。

Client Context UI仅在创作实例上可用。

## 扩展Client Context {#extending-client-context}

要扩展Client Context，请创建会话存储并（可选）显示存储数据：

* 为内容定位和Web分析所需的用户数据创建会话存储。
* 创建上下文存储组件，使管理员能够配置关联的会话存储，并在Client Context中显示存储数据以进行测试。

>[!NOTE]
>
>如果您有（或创建）可以提供数据的`JSONP`服务，则只需使用`JSONP`上下文存储组件并将其映射到JSONP服务即可。 这将处理会话存储。

### 创建会话存储{#creating-a-session-store}

为需要添加到Client Context并从中检索的数据创建会话存储。 通常，可使用以下过程创建会话存储：

1. 创建属性值为`personalization.stores.kernel`的客户端库文件夹。 `categories`Client Context会自动加载此类别的客户端库。

1. 配置客户端库文件夹，使其与`personalization.core.kernel`客户端库文件夹存在依赖关系。 `personalization.core.kernel`客户端库提供Client Context Javascript API。

1. 添加用于创建和初始化会话存储的javascript。

在personalization.stores.kernel客户端库中包含javascript会导致在加载Client Context框架时创建存储。

>[!NOTE]
>
>如果要创建作为上下文存储组件一部分的会话存储，则也可以将javascript放置在组件的init.js.jsp文件中。 在这种情况下，仅当将组件添加到Client Context时，才会创建会话存储。

#### 会话存储的类型{#types-of-session-stores}

会话存储在浏览器会话期间创建并可用，或者在浏览器存储或Cookie中持久保留。 Client Context Javascript API定义了几个类，这些类表示两种类型的数据存储：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`:这些对象仅位于页面DOM中。将在页面的生命周期中创建并保留数据。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`:这些对象位于页面DOM中，并会保留在浏览器存储或Cookie中。数据可在页面之间和用户会话之间使用。

API还提供了以下类的扩展，这些类专门用于存储JSON数据或JSONP数据：

* 仅会话对象：[CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore)和[CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore)。

* 保留的对象：[CQ_Analytics.PeristedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore)和[CQ_Analytics.PersiredJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore)。

#### 创建会话存储对象{#creating-the-session-store-object}

客户端库文件夹的javascript将创建并初始化会话存储。 然后，必须使用上下文存储管理器注册会话存储。 以下示例创建并注册一个[CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)对象。

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

为了存储JSON数据，以下示例创建并注册一个[CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)对象。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 创建上下文存储组件{#creating-a-context-store-component}

创建上下文存储组件以在Client Context中呈现会话存储数据。 创建后，您可以将上下文存储组件拖动到Client Context上以渲染会话存储中的数据。 上下文存储组件包含以下项目：

* 用于呈现数据的JSP脚本。
* 编辑对话框。
* 用于初始化会话存储的JSP脚本。
* （可选）用于创建会话存储的客户端库文件夹。 如果组件使用的是现有会话存储，则无需包含客户端库文件夹。

#### 扩展提供的上下文存储组件{#extending-the-provided-context-store-components}

AEM提供可扩展的常规存储和常规存储属性上下文存储组件。 存储数据的结构决定了扩展的组件：

* 属性 — 值对：扩展`GenericStoreProperties`组件。 此组件会自动渲染属性值对的存储。 提供了以下几个交互点：

   * `prolog.jsp` 和 `epilog.jsp`:组件交互，允许您在组件渲染之前或之后添加服务器端逻辑。

* 复杂数据：扩展`GenericStore`组件。 然后，会话存储将需要一个“渲染器”方法，每次需要渲染组件时都将调用该方法。 使用两个参数调用渲染器函数：

   * `@param {String} store`
要渲染的存储

   * `@param {String} divId`
必须呈现存储的div的ID。

>[!NOTE]
>
>所有Client Context组件都是通用存储或通用存储属性组件的扩展。 `/libs/cq/personalization/components/contextstores`文件夹中安装了几个示例。

#### 在Sidekick中配置外观{#configuring-the-appearance-in-sidekick}

编辑Client Context时，上下文存储组件显示在Sidekick中。 与所有组件一样，客户端上下文组件的`componentGroup`和`jcr:title`属性确定组件的组和名称。

默认情况下，所有属性值为`componentGroup`的组件都会显示在Sidekick中。 `Client Context`如果对`componentGroup`属性使用其他值，则必须使用设计模式手动将组件添加到Sidekick。

#### 上下文存储组件实例{#context-store-component-instances}

将上下文存储组件添加到Client Context时，会在`/etc/clientcontext/default/content/jcr:content/stores`下创建表示组件实例的节点。 此节点包含使用组件的编辑对话框配置的属性值。

初始化Client Context后，将处理这些节点。

#### 初始化关联的会话存储{#initializing-the-associated-session-store}

将init.js.jsp文件添加到组件以生成Javascript代码，该代码将初始化上下文存储组件所使用的会话存储。 例如，使用初始化脚本检索组件的配置属性，然后使用这些属性填充会话存储。

在创作实例和发布实例的页面加载中初始化Client Context时，将生成的Javascript添加到页面。 此JSP在加载和渲染上下文存储组件实例之前执行。

该代码必须将文件的mime类型设置为`text/javascript`，否则不会执行该类型。

>[!CAUTION]
>
>init.js.jsp脚本在创作和发布实例上执行，但前提是上下文存储组件已添加到Client Context。

以下过程将创建init.js.jsp脚本文件并添加用于设置正确mime类型的代码。 执行存储初始化的代码将随后显示。

1. 右键单击上下文存储组件节点，然后单击创建>创建文件。
1. 在“Name（名称）”字段中，键入`init.js.jsp`，然后单击“OK（确定）”。
1. 在页面顶部，添加以下代码，然后单击“全部保存”。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 呈现常规存储属性组件的会话存储数据{#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式在Client Context中显示会话存储数据。

#### 显示属性数据{#displaying-property-data}

个性化标签提供了`personalization:storePropertyTag`标记，用于显示会话存储中属性的值。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

`propertyName`属性是要显示的存储属性的名称。 `store`属性是已注册存储的名称。 以下示例标记显示`profile`存储的`authorizableId`属性的值：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML结构{#html-structure}

personalization.ui客户端库文件夹(/etc/clientlibs/foundation/personalization/ui/themes/default)提供Client Context用于设置HTML代码格式的CSS样式。 以下代码说明了用于显示存储数据的建议结构：

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

`/libs/cq/personalization/components/contextstores/profiledata`上下文存储组件使用此结构显示配置文件会话存储中的数据。 `cq-cc-thumbnail`类放置缩略图图像。 `cq-cc-store-property-level*x*`类格式化字母数字数据：

* level0、level1和level2垂直分布，并使用白色字体。
* 水平分布级别3和任何其他级别，并使用背景较深的白色字体。

![chlimage_1-4](assets/chlimage_1-4.png)

### 呈现常规存储组件的会话存储数据{#rendering-session-store-data-for-genericstore-components}

要使用常规存储组件渲染存储数据，您需要：

* 将personalization:storeRendererTag标记添加到组件JSP脚本中，以标识会话存储的名称。
* 在会话存储类上实现渲染器方法。

#### 标识Genericstore会话存储{#identifying-the-genericstore-session-store}

个性化标签提供了`personalization:storePropertyTag`标记，用于显示会话存储中属性的值。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 实施会话存储渲染器方法{#implementing-the-session-store-renderer-method}

然后，会话存储将需要一个“渲染器”方法，每次需要渲染组件时都将调用该方法。 使用两个参数调用渲染器函数：

* @param {String}存储
要渲染的存储
* @param {String} divId
必须呈现存储的div的ID。

## 与会话存储交互{#interacting-with-session-stores}

使用javascript与会话存储进行交互。

### 访问会话存储{#accessing-session-stores}

获取会话存储对象以读取或写入存储数据。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 提供基于存储名称的存储访问。获取后，使用[CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)或[CQ_Analytics.PersiredSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)的方法与存储数据交互。

以下示例获取`profile`存储区，然后从存储区中检索`formattedName`属性。

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

### 创建侦听器以对会话存储更新{#creating-a-listener-to-react-to-a-session-store-update}做出响应

会话会存储触发事件，因此可以添加侦听器并根据这些事件触发事件。

会话存储基于`Observable`模式构建。 它们扩展了[ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable)，用于提供` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`方法。

以下示例将侦听器添加到`profile`会话存储的`update`事件。

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

### 检查会话存储是否已定义并初始化{#checking-that-a-session-store-is-defined-and-initialized}

会话存储在加载并初始化为数据后才可用。 以下因素可能会影响会话存储可用性的时间：

* 页面加载
* JavaScript加载
* JavaScript执行时间
* XHR请求的响应时间
* 会话存储的动态更改

使用[CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils)对象的[onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback)和[onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay)方法仅在会话存储可用时才访问会话存储。 这些方法允许您注册对会话注册和初始化事件做出响应的事件侦听器。

>[!CAUTION]
>
>如果您依赖其他商店，则需要满足从未注册商店的情况。

以下示例使用`profile`会话存储的`onStoreRegistered`事件。 注册存储后，会向会话存储的`update`事件添加侦听器。 更新存储时，页面上`<div class="welcome">`元素的内容将更新为`profile`存储中的名称。

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

### 从会话持久性Cookie {#excluding-a-property-from-the-sessionpersistence-cookie}中排除属性

要阻止保留`PersistedSessionStore`的属性（即将其从`sessionpersistence` Cookie中排除），请将该属性添加到持久会话存储的非持久属性列表中。

请参阅 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## 配置设备滑块{#configuring-the-device-slider}

### 条件 {#conditions}

当前页面必须具有相应的移动页面；仅当页面具有配置了移动转出配置的LiveCopy时（`rolloutconfig.path.toLowerCase`包含`mobile`），才会确定此值。

#### 配置 {#configuration}

从桌面页面切换到其移动设备等效页面时：

* 将加载移动页面的DOM。
* 将提取包含内容的主`div`（必需）并将其插入到当前桌面页面。

* 需要手动配置需要加载的CSS和body类。

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

## 示例：创建自定义上下文存储组件{#example-creating-a-custom-context-store-component}

在此示例中，您创建一个上下文存储组件，用于从外部服务中检索数据并将其存储在会话存储中：

* 扩展了“常规”存储属性组件。
* 使用CQ_Analytics.JSONPStore Javascript对象初始化存储。
* 调用JSONP服务以检索数据并将其添加到存储中。
* 在Client Context中呈现数据。

### 添加地理位置组件{#add-the-geoloc-component}

创建CQ应用程序并添加地理位置组件。

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 右键单击`/apps`文件夹，然后单击创建>创建文件夹。 指定名称`myapp`，然后单击“确定”。
1. 同样，在`myapp`下方创建一个名为`contextstores`的文件夹。 &quot;
1. 右键单击`/apps/myapp/contextstores`文件夹，然后单击创建>创建组件。 指定以下属性值，然后单击下一步：

   * 标签：geoloc
   * 标题：位置存储
   * 超级类型：cq/personalization/components/contextstores/generistoreproperties
   * 群组：Client Context

1. 在创建组件对话框中，单击每个页面上的下一步，直到启用确定按钮，然后单击确定。
1. 单击“全部保存”。

### 创建地理位置编辑对话框{#create-the-geoloc-edit-dialog}

上下文存储组件需要一个编辑对话框。 geoloc编辑对话框将包含一条静态消息，指示没有要配置的属性。

1. 右键单击`/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog`节点，然后单击复制。
1. 右键单击`/apps/myapp/contextstores/geoloc`节点，然后单击粘贴。
1. 删除/apps/myapp/contextstores/geoloc/dialog/items/tab1/items节点下的所有子节点：

   * 商店
   * 属性
   * 缩略图

1. 右键单击`/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items`节点，然后单击创建>创建节点。 指定以下属性值，然后单击确定：

   * 名称：静态
   * 类型：cq:Widget

1. 将以下属性添加到节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | cls | 字符串 | x-form-fieldset-description |
   | 文本 | 字符串 | geoloc组件不需要任何配置。 |
   | xtype | 字符串 | 静态 |

1. 单击“全部保存”。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 创建初始化脚本{#create-the-initialization-script}

将init.js.jsp文件添加到geoloc组件，然后使用它创建会话存储、检索位置数据，并将其添加到存储。

init.js.jsp文件在页面加载Client Context时执行。 此时，Client Context Javascript API已加载，可供您的脚本使用。

1. 右键单击/apps/myapp/contextstores/geoloc节点，然后单击创建>创建文件。 指定名称init.js.jsp ，然后单击“确定”。
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

### 呈现地理位置会话存储数据{#render-the-geoloc-session-store-data}

将代码添加到地理位置组件的JSP文件中，以在Client Context中呈现存储数据。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，打开`/apps/myapp/contextstores/geoloc/geoloc.jsp`文件。
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

将位置存储组件添加到Client Context，以便在页面加载时对其进行初始化。

1. 在创作实例上打开Geometrixx Outdoors主页([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 单击Ctrl-Alt-c（窗口）或control-option-c(Mac)以打开Client Context。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![](do-not-localize/chlimage_1.png)

1. 将位置存储组件拖到Client Context。

### 请参阅Client Context中的位置信息{#see-the-location-information-in-client-context}

在编辑模式下打开Geometrixx Outdoors主页，然后打开Client Context ，以查看位置存储组件中的数据。

1. 打开Geometrixx Outdoors网站的英文页面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 要打开Client Context，请按Ctrl-Alt-c（窗口）或control-option-c(Mac)。

## 创建自定义客户端上下文{#creating-a-customized-client-context}

要创建第二个客户端上下文，您需要复制分支：

`/etc/clientcontext/default`

* 子文件夹：
   `/content`
将包含自定义客户端上下文的内容。

* 文件夹：
   `/contextstores`
允许您为上下文存储定义不同的配置。

要使用自定义的Client Context，请编辑属性
`path`
，如页面模板中所包含。 例如，作为的标准位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
