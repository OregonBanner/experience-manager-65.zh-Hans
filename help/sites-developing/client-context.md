---
title: 客户端上下文详细信息
description: Client Context表示动态组合的用户数据集合。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
feature: Context Hub
exl-id: 38b9a795-1c83-406c-ab13-b4456da938dd
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '3001'
ht-degree: 0%

---

# 客户端上下文详细信息{#client-context-in-detail}

>[!NOTE]
>
>ContextHub已取代客户端上下文。 请参阅 [相关文档](/help/sites-developing/contexthub.md) 了解详细信息。

Client Context表示动态组合的用户数据集合。 您可以使用数据来确定在给定情况下（内容定位）要在网页上显示的内容。 该数据还可用于网站分析以及页面上的任何JavaScript。

Client Context主要包括以下几个方面：

* 包含用户数据的会话存储。
* 显示用户数据并提供用于模拟用户体验的工具的UI。
* A [JavaScript API](/help/sites-developing/ccjsapi.md) 用于与会话存储区交互。

要创建独立会话存储并将其添加到Client Context，或创建绑定到Context Store组件的会话存储。 Adobe Experience Manager (AEM)安装了多个可以立即使用的上下文存储组件。 您可以将这些组件用作组件的基础。

有关打开Client Context、配置它显示的信息和模拟用户体验的信息，请参阅 [客户端上下文](/help/sites-administering/client-context.md).

## 会话存储 {#session-stores}

Client Context包括包含用户数据的各种会话存储。 存储数据来自以下来源：

* 客户端Web浏览器。
* 服务器(请参见 [JSONP存储](/help/sites-administering/client-context.md#main-pars-variable-8) 用于存储来自第三方源的信息)

Client Context框架提供 [JavaScript API](/help/sites-developing/ccjsapi.md) 用于与会话存储区交互以读取和写入用户数据，以及侦听和响应存储事件。 您还可以为用于内容定位或其他目的的用户数据创建会话存储。

会话存储数据将保留在客户端上。 Client Context不会将数据写回服务器。 要将数据发送到服务器，请使用表单或开发自定义JavaScript。

每个会话存储区都是属性值对的集合。 会话存储表示（任何类型的）数据的集合，其概念含义可由设计人员、开发人员或两者决定。 以下示例JavaScript代码定义了一个对象，该对象表示会话存储可能包含的配置文件数据：

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

会话存储可以在多个浏览器会话中持久保留，也可以仅针对在其中创建会话的浏览器会话持续保留。

>[!NOTE]
>
>存储持久性使用浏览器存储或Cookie( `SessionPersistence` Cookie)。 浏览器存储更常见。
>
>当浏览器关闭并重新打开时，可以使用来自持久存储的值加载会话存储。 需要清除浏览器缓存才能删除旧值。

### 上下文存储组件 {#context-store-components}

上下文存储组件是可以添加到客户端上下文的CQ组件。 通常，上下文存储组件显示与其关联的会话存储中的数据。 但是，上下文存储组件显示的信息不限于会话存储数据。

上下文存储组件可以包括以下项目：

* 在客户端上下文中定义外观的JSP脚本。
* 用于列出Sidekick中组件的属性。
* 用于配置组件实例的编辑对话框。
* 初始化会话存储的JavaScript。

有关可以添加到上下文存储的已安装上下文存储组件的说明，请参见 [可用的客户端上下文组件](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>页面数据不再作为默认组件存在于客户端上下文中。 如果需要，可以通过编辑客户端上下文、添加 **通用存储属性** 组件，然后配置此项以定义 **存储** 作为 `pagedata`.

### 目标内容交付 {#targeted-content-delivery}

用户档案信息还用于投放 [目标内容](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_targetedcontentdelivery](assets/clientcontext_targetedcontentdelivery.png) ![clientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## 向页面添加客户端上下文 {#adding-client-context-to-a-page}

将Client Context组件包含在网页的正文部分以启用Client Context。 客户端上下文组件节点的路径为 `/libs/cq/personalization/components/clientcontext`. 要包含该组件，请将以下代码添加到页面组件的JSP文件中，该文件位于 `body` 页面元素：

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext组件使页面加载实现Client Context的客户端库。

* 客户端上下文JavaScript API。
* Client Context框架支持会话存储、事件管理等。
* 已定义的区段。
* 为已添加到客户端上下文的每个上下文存储组件生成的init.js脚本。
* （仅限创作实例）客户端上下文UI。

客户端上下文UI仅在创作实例上可用。

## 扩展客户端上下文 {#extending-client-context}

要扩展Client Context，请创建一个会话存储区，并可以选择显示存储区数据：

* 为内容定位和网站分析所需的用户数据创建会话存储。
* 创建上下文存储组件，使管理员能够配置关联的会话存储，并在Client Context中显示存储数据以进行测试。

>[!NOTE]
>
>如果您拥有（或创建） `JSONP` 提供数据的服务，您只需使用 `JSONP` 上下文存储组件并将其映射到JSONP服务。 这将处理会话存储。

### 创建会话存储 {#creating-a-session-store}

为必须添加并从Client Context检索的数据创建会话存储。 通常，使用以下过程创建会话存储：

1. 创建具有 `categories` 属性值 `personalization.stores.kernel`. Client Context会自动加载此类别的客户端库。

1. 配置客户端库文件夹，使其依赖于 `personalization.core.kernel` 客户端库文件夹。 此 `personalization.core.kernel` 客户端库提供客户端上下文JavaScript API。

1. 添加用于创建和初始化会话存储的JavaScript。

在personalization.stores.kernel客户端库中包含JavaScript会导致在加载Client Context框架时创建存储。

>[!NOTE]
>
>如果要创建作为上下文存储组件一部分的会话存储，则可以将JavaScript放在组件的init.js.jsp文件中。 在这种情况下，仅当将组件添加到Client Context时，才会创建会话存储。

#### 会话存储的类型 {#types-of-session-stores}

会话存储是在浏览器会话期间创建并可用的，或者保留在浏览器存储或Cookie中。 Client Context JavaScript API定义了表示两种数据存储类型的几个类：

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`：这些对象仅驻留在页面DOM中。 数据在页面的生命周期内创建和保留。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`：这些对象驻留在页面DOM中，并保留在浏览器存储或Cookie中。 数据可在页面和用户会话间使用。

API还提供了专门用于存储JSON数据或JSONP数据的类的扩展：

* 仅用于会话的对象： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) 和 [cq_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* 持久化对象： [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) 和 [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### 创建会话存储对象 {#creating-the-session-store-object}

客户端库文件夹的JavaScript将创建和初始化会话存储。 必须使用上下文存储管理器注册会话存储。 以下示例创建并注册 [cq_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 对象。

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

为了存储JSON数据，以下示例创建并注册 [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 对象。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### 创建上下文存储组件 {#creating-a-context-store-component}

创建上下文存储组件以在Client Context中呈现会话存储数据。 创建后，您可以将上下文存储组件拖动到Client Context上以呈现来自会话存储的数据。 上下文存储组件由以下项目组成：

* 用于呈现数据的JSP脚本。
* 编辑对话框。
* 用于初始化会话存储区的JSP脚本。
* （可选）创建会话存储的客户端库文件夹。 如果组件使用现有会话存储，则无需包含客户端库文件夹。

#### 扩展提供的上下文存储组件 {#extending-the-provided-context-store-components}

AEM提供可以扩展的genericstore和genericstoreproperties上下文存储组件。 存储数据的结构决定了要扩展的组件：

* 属性值对：扩展 `GenericStoreProperties` 组件。 此组件自动呈现属性值对的存储。 提供了几个交互点：

   * `prolog.jsp` 和 `epilog.jsp`：组件交互，可让您在组件渲染之前或之后添加服务器端逻辑。

* 复杂数据：扩展 `GenericStore` 组件。 您的会话存储需要每当必须呈现组件时都调用的“renderer”方法。 使用两个参数调用renderer函数：

   * `@param {String} store`
要呈现的存储

   * `@param {String} divId`
必须将存储呈现到的div的ID。

>[!NOTE]
>
>所有客户端上下文组件都是通用存储或通用存储属性组件的扩展。 中安装了多个示例 `/libs/cq/personalization/components/contextstores` 文件夹。

#### 在Sidekick中配置外观 {#configuring-the-appearance-in-sidekick}

编辑Client Context时，上下文存储组件以Sidekick显示。 与所有组件一样， `componentGroup` 和 `jcr:title` 客户端上下文组件的属性确定组件的组和名称。

所有具有 `componentGroup` 属性值 `Client Context` 默认显示在Sidekick中。 如果您为 `componentGroup` 属性，您必须使用设计模式手动将组件添加到Sidekick。

#### 上下文存储组件实例 {#context-store-component-instances}

将上下文存储组件添加到Client Context时，将在下面创建一个表示该组件实例的节点 `/etc/clientcontext/default/content/jcr:content/stores`. 此节点包含使用组件的“编辑”对话框配置的属性值。

初始化客户端上下文时，将处理这些节点。

#### 初始化关联的会话存储 {#initializing-the-associated-session-store}

将init.js.jsp文件添加到组件中以生成JavaScript代码，该代码初始化上下文存储组件使用的会话存储。 例如，使用初始化脚本检索组件的配置属性，并使用这些属性填充会话存储区。

当创作实例和发布实例上的页面加载时初始化客户端上下文时，生成的JavaScript将添加到页面中。 此JSP在上下文存储组件实例加载和渲染之前执行。

代码必须将文件的mime类型设置为 `text/javascript`，或者它不执行。

>[!CAUTION]
>
>init.js.jsp脚本在创作和发布实例上运行，但前提是已将上下文存储组件添加到客户端上下文中。

以下过程将创建init.js.jsp脚本文件并添加用于设置正确mime类型的代码。 随后是执行存储初始化的代码。

1. 右键单击上下文存储组件节点，然后单击“创建”>“创建文件”。
1. 在“名称”字段中，键入 `init.js.jsp` 然后单击“确定”。
1. 在页面顶部，添加以下代码，然后单击全部保存。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### 呈现用于genericstoreproperties组件的会话存储数据 {#rendering-session-store-data-for-genericstoreproperties-components}

使用一致的格式在Client Context中显示会话存储数据。

#### 显示属性数据 {#displaying-property-data}

个性化taglib提供 `personalization:storePropertyTag` 标记，用于显示会话存储中的属性值。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

此 `propertyName` attribute是要显示的存储属性的名称。 此 `store` attribute是已注册的存储的名称。 以下示例标记显示 `authorizableId` 的属性 `profile` 存储：

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML结构 {#html-structure}

Personalization.ui客户端库文件夹(/etc/clientlibs/foundation/personalization/ui/themes/default)提供Client Context用于设置HTML代码格式的CSS样式。 以下代码说明了用于显示存储数据的建议结构：

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

此 `/libs/cq/personalization/components/contextstores/profiledata` 上下文存储组件使用此结构来显示配置文件会话存储中的数据。 此 `cq-cc-thumbnail` 类放置缩略图图像。 此 `cq-cc-store-property-level*x*` 类设置字母数字数据的格式：

* level0、level1和level2垂直分布，使用白色字体。
* 级别3和任何其他级别水平分布，并使用背景较暗的白色字体。

![chlimage_1-4](assets/chlimage_1-4.png)

### 渲染泛型存储组件的会话存储数据 {#rendering-session-store-data-for-genericstore-components}

要使用genericstore组件呈现存储数据，您必须执行以下操作：

* 将personalization：storeRendererTag标记添加到组件JSP脚本以标识会话存储的名称。
* 对会话存储类实施渲染器方法。

#### 标识泛型存储会话存储 {#identifying-the-genericstore-session-store}

个性化taglib提供 `personalization:storePropertyTag` 标记，用于显示会话存储中的属性值。 要使用标记，请在JSP文件中包含以下代码行：

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

标记具有以下格式：

```java
<personalization:storeRendererTag store="store_name"/>
```

#### 实现会话存储渲染方法 {#implementing-the-session-store-renderer-method}

您的会话存储需要每当必须呈现组件时都调用的“renderer”方法。 使用两个参数调用renderer函数：

* @param {String} 存储要呈现的存储
* @param {String} 必须将存储呈现到的div的divId ID。

## 与会话存储区交互 {#interacting-with-session-stores}

使用JavaScript与会话存储区交互。

### 访问会话存储 {#accessing-session-stores}

获取会话存储对象以将数据读取或写入存储。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) 根据商店名称提供对商店的访问权限。 获取后，请使用 [cq_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) 或 [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) 以与存储数据交互。

以下示例获得 `profile` 存储，然后检索 `formattedName` 属性。

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

### 创建监听程序以响应会话存储区更新 {#creating-a-listener-to-react-to-a-session-store-update}

会话会存储触发事件，因此可以根据这些事件添加侦听器并触发事件。

会话存储构建于 `Observable` 模式。 它们可以扩展 [`CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) 可提供 ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)` 方法。

以下示例将一个监听程序添加到 `update` 的事件 `profile` 会话存储。

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

### 检查是否已定义和初始化会话存储 {#checking-that-a-session-store-is-defined-and-initialized}

会话存储区在加载并使用数据初始化之前不可用。 以下因素可能会影响会话存储可用性的时间：

* 页面正在加载
* JavaScript加载
* JavaScript执行时间
* XHR请求的响应时间
* 对会话存储区的动态更改

使用 [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) 对象的 [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) 和 [onStoreInitialled](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 方法仅在会话存储可用时用于访问。 这些方法使您能够注册对会话注册和初始化事件作出反应的事件侦听器。

>[!CAUTION]
>
>如果您依赖于其他商店，则必须满足从未注册该商店的情况。

以下示例使用 `onStoreRegistered` 的事件 `profile` 会话存储。 注册存储后，监听程序将添加到 `update` 会话存储的事件。 更新存储时， `<div class="welcome">` 页面上的元素将更新为来自 `profile` 商店。

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

### 从sessionpersistence Cookie排除属性 {#excluding-a-property-from-the-sessionpersistence-cookie}

要阻止的属性，请执行以下操作 `PersistedSessionStore` 从persistent(即从 `sessionpersistence` cookie)，将属性添加到持久会话存储的非持久属性列表。

请参阅 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

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

当前页面必须具有对应的移动设备页面；仅当页面具有配置了移动设备转出配置( `rolloutconfig.path.toLowerCase` 包含 `mobile`)。

#### 配置 {#configuration}

从桌面页面切换到移动设备等效页面时：

* 加载移动设备页面的DOM。
* 主要 `div` （必需）将提取并插入到当前桌面页面中。

* 必须手动配置加载的CSS和正文类。

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

在此示例中，您将创建一个上下文存储组件，该组件从外部服务检索数据并将其存储在会话存储中：

* 扩展genericstoreproperties组件。
* 使用CQ_Analytics.JSONPStore JavaScript对象初始化存储。
* 调用JSONP服务以检索数据并将其添加到存储中。
* 在Client Context中渲染数据。

### 添加地理位置组件 {#add-the-geoloc-component}

创建CQ应用程序并添加geoloc组件。

1. 在Web浏览器中打开CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 右键单击 `/apps` 文件夹，然后单击创建>创建文件夹。 指定名称 `myapp` 然后单击“确定”。
1. 同样，在下方 `myapp`，创建一个名为的文件夹 `contextstores`.”
1. 右键单击 `/apps/myapp/contextstores` 文件夹，然后单击“创建”>“创建组件”。 指定以下属性值，然后单击“下一步”：

   * 标签： geoloc
   * 标题：位置存储
   * 超级类型：cq/personalization/components/contextstores/genericstoreproperties
   * 组：客户端上下文

1. 在“创建组件”对话框中，单击每个页面上的“下一步”，直到启用“确定”按钮，然后单击“确定”。
1. 单击全部保存。

### 创建地理位置的“编辑”对话框 {#create-the-geoloc-edit-dialog}

上下文存储组件需要“编辑”对话框。 地理位置编辑对话框包含一个静态消息，指示没有要配置的属性。

1. 右键单击 `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` 节点，然后单击复制。
1. 右键单击 `/apps/myapp/contextstores/geoloc` 节点，然后单击粘贴。
1. 删除/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items节点下的所有子节点：

   * 存储
   * 属性
   * 缩略图

1. 右键单击 `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` 节点，然后单击创建>创建节点。 指定以下属性值，然后单击“确定”：

   * 名称：静态
   * 类型：cq：Widget

1. 将以下属性添加到节点：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | cls | 字符串 | x-form-fieldset-description |
   | text | 字符串 | Geoloc组件无需配置。 |
   | xtype | 字符串 | 静态 |

1. 单击全部保存。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 创建初始化脚本 {#create-the-initialization-script}

将init.js.jsp文件添加到geoloc组件中，并使用它来创建会话存储、检索位置数据并将其添加到存储中。

init.js.jsp文件在页面加载Client Context时执行。 届时，将加载客户端上下文JavaScript API以供您的脚本使用。

1. 右键单击/apps/myapp/contextstores/geoloc节点，然后单击“创建”>“创建文件”。 指定“名称”init.js.jsp ，然后单击“确定”。
1. 将以下代码添加到页面顶部，然后单击全部保存。

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

### 渲染geoloc会话存储数据 {#render-the-geoloc-session-store-data}

将代码添加到geoloc组件的JSP文件中，以在Client Context中呈现存储数据。

![chlimage_1-6](assets/chlimage_1-6.png)

1. 在CRXDE Lite中，打开 `/apps/myapp/contextstores/geoloc/geoloc.jsp` 文件。
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

1. 单击全部保存。

### 将组件添加到客户端上下文 {#add-the-component-to-client-context}

将位置存储组件添加到客户端上下文，以便在页面加载时进行初始化。

1. 在创作实例上打开Geometrixx Outdoors主页([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 单击Ctrl-Alt-c (windows)或control-option-c (Mac)以打开“客户端上下文”。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![方形内由铅笔指示的编辑图标。](do-not-localize/chlimage_1.png)

1. 将位置存储组件拖动到客户端上下文。

### 请参阅客户端上下文中的位置信息 {#see-the-location-information-in-client-context}

在编辑模式下打开Geometrixx Outdoors主页，然后打开Client Context以查看位置存储组件中的数据。

1. 打开Geometrixx Outdoors网站的英语页面。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. 要打开“客户端上下文”，请按Ctrl-Alt-c (windows)或control-option-c (Mac)。

## 创建自定义的客户端上下文 {#creating-a-customized-client-context}

要创建第二个客户端上下文，请复制分支：

`/etc/clientcontext/default`

* 子文件夹：
  `/content`
包含自定义客户端上下文的内容。

* 文件夹：
  `/contextstores`
允许您为上下文存储定义不同的配置。

要使用自定义的客户端上下文，请编辑属性
`path`
客户端上下文组件的设计样式中（如页面模板中所示）。 例如，作为标准位置：
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
