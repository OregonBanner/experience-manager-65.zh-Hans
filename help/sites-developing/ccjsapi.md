---
title: Client Context Javascript API
seo-title: Client Context Javascript API
description: 适用于客户端上下文的Javascript API
seo-description: The Javascript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3153'
ht-degree: 2%

---

# Client Context Javascript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr对象是一个单例，它包含一组自注册的会话存储，并提供注册、持久化和管理会话存储的方法。

扩展CQ_Analytics.PersistedSessionStore。

### 方法 {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

返回指定名称的会话存储。 另请参阅 [访问会话存储](/help/sites-developing/client-context.md#accessing-session-stores).

**参数**

* 名称：字符串。 会话存储的名称。

**返回**

CQ_Analytics.SessionStore对象，表示给定名称的会话存储。 返回 `null` 当给定名称的存储不存在时。

#### register(sessionstore) {#register-sessionstore}

向Client Context注册会话存储。 完成时触发storeregister和storeupdate事件。

**参数**

* sessionstore： CQ_Analytics.SessionStore. 要注册的会话存储对象。

**返回**

没有返回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供侦听会话存储激活和注册的方法。 另请参阅 [检查是否已定义和初始化会话存储](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### 方法 {#methods-1}

#### onStoreInitialized（storeName， callback，延迟） {#onstoreinitialized-storename-callback-delay}

注册在初始化会话存储时调用的回调函数。 对于已初始化多次的存储，请指定回调延迟，以便只调用一次回调函数：

* 当存储在上一次初始化的延迟时段被初始化时，取消上一次函数调用，并且为当前初始化再次调用该函数。
* 如果在后续初始化发生之前延迟时段已过，则回调函数将执行两次。

例如，会话存储基于JSON对象，并通过JSON请求进行检索。 可能会出现以下初始化场景：

* 完成请求，检索数据并将其加载到存储中。 在这种情况下，初始化只发生一次。
* 请求失败（超时）。 在这种情况下，不会进行初始化，并且存储中没有数据。
* 存储中预先填充了默认值（init属性），但请求失败（超时）。 只有一个使用默认值的初始化。
* 已预填充存储。

当延迟设置为 `true` 或毫秒数，此方法会先等待，然后再调用回调方法。 如果在传递延迟之前触发了另一个初始化事件，它将等待直到超过延迟时间，而不发生初始化事件。 这允许等待触发第二个初始化事件，并在最佳情况下调用回调函数。

**参数**

* storeName：字符串。 用于添加监听程序的会话存储的名称。
* callback：函数。 在存储初始化时调用的函数。
* delay： Boolean或Number。 延迟回调函数调用的时间（以毫秒为单位）。 布尔值 `true` 使用默认延迟 `200 ms`. 布尔值 `false` 或负数导致使用无延迟。

**返回**

没有返回值。

#### onStoreRegistered(storeName， callback) {#onstoreregistered-storename-callback}

注册在注册会话存储时调用的回调函数。 当存储注册到时，会发生注册事件 [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**参数**

* storeName：字符串。 用于添加监听程序的会话存储的名称。
* callback：函数。 在存储初始化时调用的函数。

**返回**

没有返回值。

## cq_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON数据的非持久会话存储。 数据从外部JSONP服务中检索。 使用 `getInstance` 或 `getRegisteredInstance` 创建此类的实例的方法。

扩展CQ_Analytics.JSONStore。

### 属性 {#properties}

有关继承的属性，请参阅CQ_Analytics.JSONStore和CQ_Analytics.SessionStore 。

### 方法 {#methods-2}

有关继承的方法，另请参阅CQ_Analytics.JSONStore和CQ_Analytics.SessionStore 。

#### getInstance(storeName， serviceURL， dynamicData， deferLoading， loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

创建CQ_Analytics.JSONPStore对象。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。 如果未提供storeName，则方法返回null。
* serviceURL：字符串。 JSONP服务的URL
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* deferLoading： （可选）布尔值。 值为true可防止在创建对象时调用JSONP服务。 值为false会导致调用JSONP服务。
* loadingCallback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

新的CQ_Analytics.JSONPStore对象；如果storeName为null，则为null。

#### getServiceURL() {#getserviceurl}

检索此对象用于检索JSON数据的JSONP服务的URL。

**参数**

无.

**返回**

表示服务URL的字符串，如果未配置服务URL，则为null。

#### load(serviceURL， dynamicData， callback) {#load-serviceurl-dynamicdata-callback}

调用JSONP服务。 JSONP URL是后缀为给定回调函数名的服务URL。

**参数**

* serviceURL： （可选）字符串。 要调用的JSONP服务。 值为null会导致使用已配置的服务URL。 非null值设置JSONP服务以用于此对象。 （请参阅setServiceURL。）
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* callback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

没有返回值。

#### registerNewInstance(storeName， serviceURL， dynamicData， callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

创建CQ_Analytics.JSONPStore对象并在客户端上下文中注册存储。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。 如果未提供storeName，则方法返回null。
* serviceURL： （可选）字符串。 JSONP服务的URL。
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* callback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

注册的CQ_Analytics.JSONPStore对象。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

设置用于检索JSON数据的JSONP服务的URL。

**参数**

* serviceURL：字符串。 提供JSON数据的JSONP服务的URL

**返回**

没有返回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON对象的容器。 创建此类的实例以创建包含JSON数据的非持久化会话存储：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定义在初始化时填充存储的一组数据。

扩展CQ_Analytics.SessionStore。

### 属性 {#properties-1}

#### STOREKEY {#storekey}

标识存储的键。 使用 `getInstance` 方法以检索此值。

#### STORENAME {#storename}

存储的名称。 使用 `getInstance` 方法以检索此值。

### 方法 {#methods-3}

另请参阅CQ_Analytics.SessionStore以了解继承的方法。

#### 清除() {#clear}

删除会话存储区数据并删除所有初始化属性。

**参数**

无.

**返回**

没有返回值。

#### getInstance(storeName， jsonData) {#getinstance-storename-jsondata}

使用给定的名称创建一个CQ_Analytics.JSONStore对象，并使用给定的JSON数据初始化（调用initJSON方法）。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。
* jsonData：对象。 包含JSON数据的对象。

**返回**

cq_Analytics.JSONStore对象。

#### getJSON() {#getjson}

检索会话存储区的JSON格式数据。

**参数**

无.

**返回**

以JSON格式表示存储数据的对象。

#### init() {#init}

清除会话存储并使用初始化属性对其进行初始化。 将初始化标志设置为 `true` 然后触发 `initialize` 和 `update` 事件。

**参数**

无.

**返回**

没有返回的数据。

#### initJSON(jsonData， doNotClear) {#initjson-jsondata-donotclear}

从JSON对象中的数据创建初始化属性。 您可以选择删除所有现有的初始化属性。

属性的名称从JSON对象中数据的层次结构派生。 以下示例代码表示一个JSON对象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

对于此示例，将在存储中创建以下属性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**参数**

* jsonData： JSON对象，包含要存储的数据。
* doNotClear：值为true时会保留现有的初始化属性，并添加从JSON对象派生的属性。 值为false会先删除现有的初始化属性，然后再添加从JSON对象派生的属性。

**返回**

没有返回值。

#### registerNewInstance(storeName， jsonData) {#registernewinstance-storename-jsondata}

使用给定的名称创建一个CQ_Analytics.JSONStore对象，并使用给定的JSON数据初始化（调用initJSON方法）。 新对象会自动向Clickstream Cloud Manager注册。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。
* jsonData：对象。 包含JSON数据的对象。

**返回**

cq_Analytics.JSONStore对象。

## CQ_Analytics.Observable {#cq-analytics-observable}

触发事件并允许其他对象侦听这些事件并做出反应。 扩展此类的类可以触发导致调用侦听器的事件。

### 方法 {#methods-4}

#### addListener(event， fct， scope) {#addlistener-event-fct-scope}

注册事件的侦听器。 另请参阅 [创建侦听器以响应会话存储更新](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**参数**

* 事件：字符串。 要侦听的事件的名称。
* fct：函数。 发生事件时调用的函数。
* 范围： （可选）对象。 执行处理程序函数的范围。 处理程序函数的“this”上下文。

**返回**

没有返回值。

#### removeListener(event， fct) {#removelistener-event-fct}

删除事件的给定事件处理程序。

**参数**

* 事件：字符串。 事件的名称。
* fct：函数。 事件处理程序。

**返回**

没有返回值。

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

从远程JSONP服务检索的JSON对象的持久容器。

扩展CQ_Analytics.PersistedJSONStore。

### 方法 {#methods-5}

另请参阅CQ_Analytics.PersistedJSONStore以了解继承的方法。

#### getInstance(storeName， serviceURL， dynamicData， deferLoading， loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

创建CQ_Analytics.PersistedJSONPStore对象。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。 如果未提供storeName，则方法返回null。
* serviceURL：字符串。 JSONP服务的URL
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* deferLoading： （可选）布尔值。 值为true可防止在创建对象时调用JSONP服务。 值为false会导致调用JSONP服务。
* loadingCallback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

新的CQ_Analytics.PersistedJSONPStore对象；如果storeName为null，则为null。

#### getServiceURL() {#getserviceurl-1}

检索此对象用于检索JSON数据的JSONP服务的URL。

**参数**

无.

**返回**

表示服务URL的字符串，如果未配置服务URL，则为null。

#### load(serviceURL， dynamicData， callback) {#load-serviceurl-dynamicdata-callback-1}

调用JSONP服务。 JSONP URL是后缀为给定回调函数名的服务URL。

**参数**

* serviceURL： （可选）字符串。 要调用的JSONP服务。 值为null会导致使用已配置的服务URL。 非null值设置JSONP服务以用于此对象。 （请参阅setServiceURL。）
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* callback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

没有返回值。

#### registerNewInstance(storeName， serviceURL， dynamicData， callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

创建CQ_Analytics.PersistedJSONPStore对象并在客户端上下文中注册存储。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。 如果未提供storeName，则方法返回null。
* serviceURL： （可选）字符串。 JSONP服务的URL。
* dynamicData： （可选）对象。 在调用回调函数之前附加到存储区初始化数据的JSON数据。
* callback： （可选）字符串。 为处理JSONP服务返回的JSONP对象而调用的函数的名称。 回调函数必须定义一个参数，该参数是一个CQ_Analytics.JSONPStore对象。

**返回**

注册的CQ_Analytics.PersistedJSONPStore对象。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

设置用于检索JSON数据的JSONP服务的URL。

**参数**

* serviceURL：字符串。 提供JSON数据的JSONP服务的URL

**返回**

没有返回值。

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

JSON对象的持久容器。

扩展 `CQ_Analytics.PersistedSessionStore`.

### 属性 {#properties-2}

#### STOREKEY {#storekey-1}

标识存储的键。 使用 `getInstance` 方法以检索此值。

#### STORENAME {#storename-1}

存储的名称。 使用 `getInstance` 方法以检索此值。

### 方法 {#methods-6}

另请参阅CQ_Analytics.PersistedSessionStore以了解继承的方法。

#### getInstance(storeName， jsonData) {#getinstance-storename-jsondata-1}

创建具有给定名称的CQ_Analytics.PersistedJSONStore对象，并使用给定的JSON数据初始化（调用initJSON方法）。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。
* jsonData：对象。 包含JSON数据的对象。

**返回**

cq_Analytics.PersistedJSONStore对象。

#### getJSON() {#getjson-1}

检索会话存储区的JSON格式数据。

**参数**

无.

**返回**

以JSON格式表示存储数据的对象。

#### initJSON(jsonData， doNotClear) {#initjson-jsondata-donotclear-1}

从JSON对象中的数据创建初始化属性。 您可以选择删除所有现有的初始化属性。

属性的名称从JSON对象中数据的层次结构派生。 以下示例代码表示一个JSON对象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

对于此示例，将在存储中创建以下属性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**参数**

* jsonData： JSON对象，包含要存储的数据。
* doNotClear：值为true时会保留现有的初始化属性，并添加从JSON对象派生的属性。 值为false会先删除现有的初始化属性，然后再添加从JSON对象派生的属性。

**返回**

没有返回值。

#### registerNewInstance(storeName， jsonData) {#registernewinstance-storename-jsondata-1}

创建具有给定名称的CQ_Analytics.PersistedJSONStore对象，并使用给定的JSON数据初始化（调用initJSON方法）。 新对象将自动向Client Context Manager注册。

**参数**

* storeName：字符串。 要用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，且包含所有大写字符。
* jsonData：对象。 包含JSON数据的对象。

**返回**

cq_Analytics.PersistedJSONStore对象。

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

属性和值的容器。 使用CQ_Analytics.SessionPersistence持久保留数据。 创建此类的实例以创建持久会话存储：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

扩展CQ_Analytics.SessionStore。

### 属性 {#properties-3}

#### STOREKEY {#storekey-2}

默认值为 `key`.

### 方法 {#methods-7}

有关继承的方法，请参阅CQ_Analytics.SessionStore 。

当继承的方法 `clear`， `setProperty`， `setProperties`， `removeProperty` 用于更改存储区数据，除非已更改的属性被标记为notPersisted，否则更改会自动保留。

#### getStoreKey() {#getstorekey}

检索 `STOREKEY` 属性。

**参数**

无

**返回**

的值 `STOREKEY` 属性。

#### isPersisted(name) {#ispersisted-name}

确定是否保留数据属性。

**参数**

* 名称：字符串。 属性的名称。

**返回**

布尔值 `true` 如果属性持续存在，并且值为 `false` 如果值不是持久属性。

#### persist() {#persist}

保留会话存储。 默认持久性模式使用浏览器 `localStorage` 使用 `ClientSidePersistence` 作为名称( `window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage不可用或不可写，则该存储将作为窗口的属性保留。

触发 `persist` 完成时的事件。

**参数**

无

**返回**

没有返回值。

#### reset(deferEvent) {#reset-deferevent}

从存储中删除所有数据属性并保留存储。 （可选）不触发 `udpate` 完成时的事件。

**参数**

* deferevent：如果值为true，则会阻止 `update` 事件被触发。 值 `false` 导致触发更新事件。

**返回**

没有返回值。

#### setNonPersisted(name) {#setnonpersisted-name}

将数据属性标记为未保留。

**参数**

* 名称：字符串。 不保留的属性的名称。

**返回**

无返回值。

## cq_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore表示会话存储。 创建此类的实例以创建会话存储：

`mystore = new CQ_Analytics.SessionStore`

扩展CQ_Analytics.Observable。

### 属性 {#properties-4}

#### STORENAME {#storename-2}

会话存储的名称。 使用getName检索此属性的值。

### 方法 {#methods-8}

#### addInitProperty(name， value) {#addinitproperty-name-value}

向会话存储初始化数据添加属性和值。

使用loadInitProperties使用初始化值填充会话存储数据。

**参数**

* 名称：字符串。 要添加属性的名称。
* 值：字符串。 要添加属性的值。

**返回**

没有返回值。

#### 清除() {#clear-1}

从存储中删除所有数据属性。

**参数**

无.

**返回**

无返回值。

#### getData(excluded) {#getdata-excluded}

返回存储数据。 （可选）从数据中排除名称属性。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

excluded： （可选）要从返回的数据中排除的属性名称数组。

**返回**

属性及其值的对象。

#### getInitProperty(name) {#getinitproperty-name}

检索数据属性的值。

**参数**

* 名称：字符串。 要检索的数据属性的名称。

**返回**

数据属性的值。 返回 `null` 如果会话存储不包含给定名称的属性。

#### getName() {#getname}

返回会话存储的名称。

**参数**

无.

**返回**

表示存储名称的字符串值。

#### getProperty(name， raw) {#getproperty-name-raw}

返回属性的值。 该值作为原始属性或XSS筛选值返回。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

* 名称：字符串。 要检索的数据属性的名称。
* raw：布尔值。 值为true会导致返回原始属性值。 值为false会导致返回的值被XSS过滤。

**返回**

数据属性的值。

#### getPropertyNames(excluded) {#getpropertynames-excluded}

返回会话存储所包含属性的名称。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

excluded： （可选）要从结果中忽略的属性名称数组。

**返回**

表示会话属性名称的字符串值数组。

#### getSessionStore() {#getsessionstore}

返回附加到当前对象的会话存储。

**参数**

无.

**返回**

此

#### init() {#init-1}

将存储标记为已初始化，并触发 `initialize` 事件。

**参数**

无.

**返回**

没有返回值。

#### isInitialized() {#isinitialized}

指示会话存储是否已初始化。

**参数**

无.

**返回**

值 `true` 如果存储已初始化，并且值为 `false` 如果存储未初始化。

#### loadInitProperties(obj， setValues) {#loadinitproperties-obj-setvalues}

将给定对象的属性添加到会话存储的初始化数据中。 （可选）对象数据也添加到存储数据中。

**参数**

* obj：包含可枚举属性的对象。
* setValues：为true时，如果存储数据尚未包含同名属性，则对象属性会添加到会话存储数据中。 为false时，不会向会话存储数据添加任何数据。

**返回**

没有返回值。

#### removeProperty(name) {#removeproperty-name}

从会话存储中删除属性。 触发 `update` 完成时的事件。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

* 名称：字符串。 要删除的属性的名称。

**返回**

没有返回值。

#### 重置() {#reset}

恢复数据存储区的初始值。 默认实施只是删除所有数据。 触发 `update` 完成时的事件。

**参数**

无.

**返回**

没有返回值。

#### setProperties(properties) {#setproperties-properties}

设置多个属性的值。 触发 `update` 完成时的事件。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

* 属性：对象。 包含可枚举属性的对象。 每个属性名称和值都会添加到存储中。

**返回**

没有返回值。

#### setProperty(name， value) {#setproperty-name-value}

设置属性的值。 触发 `update` 完成时的事件。 调用 `init` 方法（如果存储的数据属性不存在）。

**参数**

* 名称：字符串。 属性的名称。
* 值：字符串。 属性值。

**返回**

没有返回值。
