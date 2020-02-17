---
title: ContextHub Javascript API参考
seo-title: ContextHub Javascript API参考
description: 将ContextHub组件添加到页面后，您的脚本可以使用ContextHub Javascript API
seo-description: 将ContextHub组件添加到页面后，您的脚本可以使用ContextHub Javascript API
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ContextHub Javascript API参考{#contexthub-javascript-api-reference}

将ContextHub组件添加到页面后，您的脚 [本可以使用ContextHub Javascript API](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component)。

## ContextHub常量 {#contexthub-constants}

ContextHub Javascript API定义的常数值。

### 事件常量 {#event-constants}

下表列出了ContextHub Stores发生的名称事件。 另请参 [阅ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing)。

| 常数 | 描述 | 值 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub的事件命名空间 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 指示所有必需的存储已注册、初始化并准备使用 | 所有商店就绪 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 指示并非所有存储都在给定超时内初始化 | stores-partially-ready |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 注册商店时触发 | 商店注册 |
| ContextHub.Constants.EVENT_STORE_READY | 指示商店可以使用。 注册后会立即触发它，但JSONP存储区除外，当获取数据时会触发它)。 | 商店就绪 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 当存储更新其持久性时触发 | 商店更新 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 持久性容器名称 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 存储存储原始JSON结果的特定持久性密钥名称 | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | 存储指示何时获取JSON数据的特定时间戳 | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 存储上次调用期间使用的JSON服务的特定URL | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | 指示ContextHub的UI是否已展开 | /_/容器扩展 |

### UI事件常量 {#ui-event-constants}

下表列出了ContextHub UI发生的事件的名称。

| **常数** | **描述** | **值** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 注册模式时触发 | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 未注册模式时触发 | ui-mode-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 注册模式渲染器时触发 | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 当未注册模式渲染器时触发 | ui-mode-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 添加新模式时触发 | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 删除模式时触发 | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 当用户选择模式时触发 | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 注册新模块时触发 | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 未注册模块时触发 | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 注册模块渲染器时触发 | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 未注册模块渲染器时触发 | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 添加新模块时触发 | 添加了UI模块 |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 删除模块时触发 | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | 将UI容器添加到页面时触发 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | 打开ContextHub UI时触发 | ui-container-opened |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | 折叠ContextHub UI时触发 | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 修改属性时触发 | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | 每次呈现ContextHub UI时触发（例如，在属性更改后） | ui-rendered |
| ContextHub.Constants.EVENT_UI_INITIALIZED | UI容器初始化时触发 | ui-initialized |
| ContextHub.Constants.ACTIVE_UI_MODE | 指示活动UI模式 | /_/active-ui-mode |

## ContextHub Javascript API参考 {#contexthub-javascript-api-reference-2}

ContextHub对象提供对所有商店的访问。

### 函数(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

返回所有注册的ContextHub存储。

此函数没有参数。

**退货**

包含所有ContextHub存储的对象。 每个存储都是一个与存储同名的对象。

**示例**

以下示例检索所有存储，然后检索geolocation存储：

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

将存储检索为Javascript对象。

**参数**

* **** name:注册商店时使用的名称。

**退货**

表示存储的对象。

**示例**

以下示例检索geolocation存储：

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

表示ContextHub区段。 使用ContextHub.SegmentEngine.SegmentManager获取区段。

### 函数(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

以字符串值的形式返回区段的名称。

#### getPath() {#getpath}

以字符串值的形式返回区段定义的存储库路径。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供对ContextHub区段的访问。

### 函数(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

返回在当前上下文中解析的区段。 此函数没有参数。

**退货**

ContextHub.SegmentEngine.Segment对象的数组。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存储的基类。

### 属性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 活动 {#eventing}

ContextHub. [Utils.Eventing对象](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 。 使用此对象绑定函数以存储事件。 有关默认值和初始化的信息，请 [参阅init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config)。

#### 名称 {#name}

商店的名称。

#### 持久性 {#persistence}

ContextHub.Utils.Persistence对象。 有关默认值和初始化的信息，请参阅 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 函数(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

将数据对象或数组与存储数据合并。 对象或数组中的每个键／值对都添加到存储中(通过函 `setItem` 数):

* **** 对象：键是属性名称。
* **** 阵列：键是数组索引。

请注意，值可以是对象。

**参数**

* **** 树：（对象或数组）要添加到存储的数据。
* **** 选项：（对象）传递给setItem函数的选项的可选对象。 有关信息，请参 `options` 阅 [setItem(key,value,options)的参数](/help/sites-developing/contexthub-api.md#setitem-key-value-options)。

**退货**

值 `boolean` :

* 值表示 `true` 已存储数据对象。
* 值表示数 `false` 据存储未更改。

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

创建从一个键到另一个键的引用。 键不能引用自身。

**参数**

* **** 键：引用的键 `anotherKey`。

* **** 其他密钥：它们由引用的键 `key`。

**退货**

值 `boolean` :

* 值表示 `true` 已添加引用。
* 值表示 `false` 未添加引用。

#### announceReadiness() {#announcereadiness}

触发此 `ready` 商店的事件。 此函数没有参数，并且不返回值。

#### clean() {#clean}

从存储中删除所有数据。 该函数没有参数，也没有返回值。

#### getItem(key) {#getitem-key}

返回与键关联的值。

**参数**

* **** 键：（字符串）要返回值的键。

**退货**

表示键值的Object。

#### getKeys(includeInternals) {#getkeys-includeinternals}

从商店检索密钥。 或者，您也可以检索ContextHub框架内部使用的键。

**参数**

* **** includeInternals:值包括 `true` 结果中内部使用的键。 这些键以下划线(&quot;_&quot;)字符开头。 默认值为 `false`.

**退货**

键名（值） `string` 的数组。

#### getReferences() {#getreferences}

从商店检索引用。

**退货**

使用引用键作为引用键索引的数组：

* 引用键与函 `key` 数的参数相 `addReference` 对应。

* 引用的键与函 `anotherKey` 数的参数相 `addReference` 对应。

#### getTree(includeInternals) {#gettree-includeinternals}

从存储检索数据树。 或者，您也可以包括ContextHub框架内部使用的键／值对。

**参数**

* `includeInternals:` 值包括 `true` 结果中内部使用的键／值对。 此数据的键以下划线(&quot;_&quot;)字符开头。 默认值为 `false`.

**退货**

表示数据树的对象。 键是对象的属性名称。

#### init(name, config) {#init-name-config}

初始化存储。

* 将存储数据设置为空对象。
* 设置对空对象的存储引用。
* eventChannel是data:*name*，其 *中name* 是存储名称。

* storeDataKey是/store/*name*，其 *中name是* store name。

**参数**

* **** name:商店的名称。
* **** config:包含配置属性的对象：

   * eventDeferring:默认值为32。
   * 活动：此 [存储的ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 对象。 默认值是ContextHub.eventing对象使用的值。
   * 持久性：此存储的ContextHub.Utils.Persistence对象。 默认值是ContextHub.persistence对象。

#### isEventingPaused() {#iseventingpaused}

确定此存储是否暂停了事件。

**退货**

布尔值：

* `true`:暂停事件，以便不会触发此存储的事件。
* `false`:事件不会暂停，因此会为此存储触发事件。

#### pauseEventing() {#pauseeventing}

暂停存储事件，以便不触发任何事件。 此函数不需要任何参数，也不返回任何值。

#### removeItem(key, options) {#removeitem-key-options}

从存储中删除键／值对。

删除键后，该函数将触发该事 `data` 件。 事件数据包括存储名称、已删除的键的名称、已删除的值、键的新值(null)和“remove”的操作类型。

（可选）您可以防止触发事 `data` 件。

**参数**

* **** 键：（字符串）要删除的键的名称。
* **** 选项：（对象）选项对象。 以下对象属性有效：

   * silent:值可防止 `true` 事件的触发 `data` 。 默认值为 `false`.

**退货**

值 `boolean` :

* 值表示 `true` 已删除键／值对。
* 值表示数 `false` 据存储区未更改，因为在存储区中找不到密钥。

#### removeReference(key) {#removereference-key}

从商店中删除引用。

**参数**

* **** 键：要删除的键引用。 此参数与函数 `key` 的参数相 `addReference` 对应。

**退货**

值 `boolean` :

* 值表示 `true` 引用已删除。
* 值表示 `false` 密钥无效且存储未更改。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重置存储的保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时，此存储的事件暂停。 此函数不返回任何值。

初始值提供在用于实例化存储对象的config对象的initialValues属性中。

**参数**

* **** keepRemainingData:(Boolean)如果值为true，则非初始数据会被保留。 如果值为false，则除初始值外，所有数据都会被删除。

重置存储的保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时，此存储的事件暂停。 此函数不返回任何值。

初始值提供在用于实例化存储对象的config对象的initialValues属性中。

**参数**

* keepRemainingData:(Boolean)如果值为true，则非初始数据会被保留。 如果值为false，则除初始值外，所有数据都会被删除。

#### resolveReference(key, retry) {#resolvereference-key-retry}

检索引用的键。 或者，您也可以指定用于解析最佳匹配的迭代数。

**参数**

* **** 键：（字符串）用于解析引用的键。 此参 `key` 数与函数 `key` 的参数相 `addReference` 对应。

* **** 重试：（数量）要使用的迭代数。

**退货**

表 `string` 示引用键的值。 如果未解析引用，则返回该参 `key` 数的值。

#### resumeEventing() {#resumeeventing}

恢复此商店的事件，以触发事件。 此函数不定义任何参数，也不返回任何值。

#### setItem(key, value, options) {#setitem-key-value-options}

向存储添加键／值对。

仅当键 `data` 的值与当前存储的键值不同时，才触发事件。 您可以选择防止触发事 `data` 件。

事件数据包括存储名称、键、上一个值、新值和操作类型 `set`。

**参数**

* **** 键：（字符串）键的名称。
* **** 选项：（对象）选项对象。 以下对象属性有效：

   * silent:值可防止 `true` 事件的触发 `data` 。 默认值为 `false`.

* **** value:（对象）要与键关联的值。

**退货**

值 `boolean` :

* 值表示 `true` 已存储数据对象。
* 值表示数 `false` 据存储未更改。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON数据的商店。 从外部JSONP服务检索数据，或从返回JSON数据的服务（可选）检索数据。 在创建此类的实例时， [ 使用函数指 `init`](/help/sites-developing/contexthub-api.md#init-name-config) 定服务详细信息。

存储使用内存中的永久性（Javascript变量）。 存储数据仅在页面的生命周期内可用。

ContextHub.Store.JSONPStore扩展 [了ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) ，并继承了该类的函数。

### 函数(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

配置用于连接到此对象使用的JSONP服务的详细信息。 您可以更新或替换现有配置。 该函数不返回任何值。

**参数**

* **** serviceConfig:包含以下属性的对象：

   * 主机：（字符串）服务器名或IP地址。
   * jsonp:(Boolean)值为true表示服务是JSONP服务，否则为false。 如果为true，则{callback:“ContextHub.Callbacks。*Object.name*}对象添加到service.params对象。
   * params:（对象）表示为对象属性的URL参数。 参数名称是属性名称，参数值是属性值。
   * 路径：（字符串）服务的路径。
   * 端口：(Number)服务的端口号。
   * 安全：（字符串或布尔值）确定用于服务URL的协议：

      * auto: //
      * true:https://
      * false:https://

* **** 覆盖：（布尔值）。 如果值 `true` 为，则现有服务配置将被其属性替换 `serviceConfig`。 如果值为 `false` ，则会将现有服务配置属性与的属性合并 `serviceConfig`。

#### getRawResponse() {#getrawresponse}

返回自上次调用JSONP服务以来缓存的原始响应。 该函数不需要任何参数。

**退货**

表示原始响应的对象。

#### getServiceDetails() {#getservicedetails}

检索此ContextHub.Store.JSONPStore对象的服务对象。 服务对象包含创建服务URL所需的所有信息。

**退货**

具有以下属性的对象：

* **** 主机：（字符串）服务器名或IP地址。
* **** jsonp:(Boolean)值为true表示服务是JSONP服务，否则为false。 如果为true，则{callback:“ContextHub.Callbacks。*Object.name*}对象添加到service.params对象。

* **** params:（对象）表示为对象属性的URL参数。 参数名称是属性名称，参数值是属性值。
* **** 路径：（字符串）服务的路径。
* **** 端口：(Number)服务的端口号。
* **** 安全：（字符串或布尔值）确定用于服务URL的协议：

   * auto: //
   * true:https://
   * false:https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

检索JSONP服务的URL。

**参数**

* **** resolve:（布尔值）确定是否在URL中包含已解析的参数。 解析参 `true` 数的值， `false` 但不。

**退货**

表 `string` 示服务URL的值。

#### init(name, config) {#init-name-config-1}

初始化ContextHub.Store.JSONPStore对象。

**参数**

* **** name:（字符串）商店的名称。
* **** config:（对象）包含服务属性的对象。 JSONPStore对象使用对象的 `service` 属性来构建JSONP服务的URL:

   * eventDeferring:32.
   * 活动：此存储的ContextHub.Utils.Eventing对象。 默认值是对 `ContextHub.eventing` 象。
   * 持久性：此存储的ContextHub.Utils.Persistence对象。 默认情况下，使用内存持久性（Javascript对象）。
   * 服务：（对象）

      * 主机：（字符串）服务器名或IP地址。
      * jsonp:(Boolean)值为true表示服务是JSONP服务，否则为false。 如果为true，则 `{callback: "ContextHub.Callbacks.*Object.name*}`将对象添加到 `service.params`。
      * params:（对象）表示为对象属性的URL参数。 参数名和值分别是对象属性名和值。
      * 路径：（字符串）服务的路径。
      * 端口：(Number)服务的端口号。
      * 安全：（字符串或布尔值）确定用于服务URL的协议：

         * auto: //
         * true:https://
         * false:https://
      * 超时：（数字）在超时之前等待JSONP服务响应的时间（以毫秒为单位）。
      * ttl:JSONP服务调用之间传递的最小时间（以毫秒为单位）。 (请参阅 [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) 函数)。


#### queryService(reload) {#queryservice-reload}

查询远程JSONP服务并缓存响应。 如果自上次调用此函数以来的时间小于的值 `config.service.ttl`，则不调用服务，且不更改缓存的响应。 或者，您也可以强制调用服务。 调 `config.service.ttl`用init函数初始化存储 [时](/help/sites-developing/contexthub-api.md#init-name-config) ，将设置该属性。

查询完成时触发ready事件。 如果未设置JSONP服务URL，则函数不执行任何操作。

**参数**

* **** 重新加载：(Boolean)值true将删除缓存的响应并强制调用JSONP服务。

#### 重置 {#reset}

重置存储的保留数据的初始值，然后调用JSONP服务。 或者，您也可以从存储中删除所有其他数据。 重置初始值时，会暂停此存储的事件。 此函数不返回任何值。

初始值提供在用于实例化存储对象的config对象的initialValues属性中。

**参数**

* **** keepRemainingData:(Boolean)如果值为true，则非初始数据会被保留。 如果值为false，则除初始值外，所有数据都会被删除。

#### resolveParameter(f) {#resolveparameter-f}

解析给定参数。

## ContextHub.Store.PersitedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersitedJSONPStore扩展了 [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) ，因此它继承了该类的所有功能。 但是，从JSONP服务检索的数据会根据ContextHub持久性的配置进行保留。 (请参阅 [持久性模式](/help/sites-developing/ch-adding.md#persistence-modes)。)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersitedStore扩展 [了ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) ，因此它继承了该类的所有功能。 根据ContextHub持久性的配置，将保留此存储中的数据。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore扩展 [了ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) ，因此它继承了该类的所有功能。 此存储中的数据会使用内存中的永久性（Javascript对象）进行保留。

## ContextHub.UI {#contexthub-ui}

管理UI模块和UI模块渲染器。

### 函数(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRenderer) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub注册UI模块渲染器。 在注册呈示器后，可以使用它创建 [UI模块](/help/sites-administering/contexthub-config.md#adding-a-ui-module)。 当您扩展ContextHub.UI.BaseModuleRenderer以 [创建自定义UI模块呈示器时](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) ，请使用此函数。

**参数**

* **** moduleType:（字符串）UI模块渲染器的标识符。 如果渲染器已使用指定的值进行注册，则在注册此渲染器之前，将取消注册现有渲染器。
* **** renderer:（字符串）呈现UI模块的类的名称。
* **** dontRender:（布尔值）设置为 `true` 在注册呈示器后阻止呈现ContextHub UI。 默认值为 `false`.

**示例**

以下示例将呈示器注册为contexthub.browserinfo模块类型。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

用于与Cookie交互的实用程序类。

### 函数(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

确定Cookie是否存在。

**参数**

* **** 键：包 `String` 含要测试的Cookie的键的A。

**退货**

如果 `boolean` 值为true，则表示Cookie存在。

**示例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

返回所有具有与过滤器匹配的密钥的Cookie。

**参数**

* **（可选）过**&#x200B;滤器：匹配Cookie键的条件。 要返回所有Cookie，请不指定任何值。 支持以下类型：

   * 字符串：该字符串与cookie键进行比较。
   * 阵列：数组中的每个项都是一个滤镜。
   * RegExp对象：对象的测试函数用于匹配cookie键。
   * 函数：用于测试Cookie键是否匹配的函数。 如果测试确认匹配，该函数必须将cookie键作为参数并返回true。

**退货**

Cookie对象。 对象属性是cookie键，键值是cookie值。

**示例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

返回Cookie值。

**参数**

* **** 键：您希望其值的Cookie的键。

**退货**

Cookie值，或 `null` 者如果找不到该键的Cookie。

**示例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

返回与筛选器匹配的现有Cookie的密钥数组。

**参数**

* **** 过滤器：匹配Cookie键的条件。 支持以下类型：

   * 字符串：该字符串与cookie键进行比较。
   * 阵列：数组中的每个项都是一个滤镜。
   * RegExp对象：对象的测试函数用于匹配cookie键。
   * 函数：用于测试Cookie键是否匹配的函数。 如果测试确认匹配，该函数必须将cookie键作为参 `true` 数并返回。

**退货**

一个字符串数组，其中每个字符串是与过滤器匹配的cookie的键。

**示例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

删除Cookie。 要删除Cookie，该值将设置为一个电子邮件字符串，到期日期将设置为当前日期前一天。

**参数**

* **** 键：表 `String` 示要删除的Cookie的键的值。

* **** 选项：包含用于配置Cookie属性的属性值的对象。 有关信 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 息，请参阅函数。 该 `expires` 属性无效。

**退货**

此函数不返回值。

**示例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

创建给定密钥和值的Cookie，并将Cookie添加到当前文档。 或者，您也可以指定配置Cookie属性的选项。

**参数**

* **** 键：包含Cookie密钥的字符串。
* **** value:包含Cookie值的字符串。
* **** 选项：（可选）包含以下任意属性的对象，这些属性配置了cookie属性：

   * 过期：一个 `date` 或 `number` 一个值，它指定Cookie何时过期。 日期值指定到期的绝对时间。 数字（以天为单位）将到期时间设置为当前时间加上数字。 默认值为 `undefined`.
   * 安全：一 `boolean` 个值，它指定 `Secure` cookie的属性。 默认值为 `false`.
   * 路径：用 `String` 作Cookie属性 `Path` 的值。 默认值为 `undefined`.

**退货**

具有设置值的Cookie。

**示例**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 消失（过滤器，选项） {#vanish-filter-options}

删除与给定过滤器匹配的所有Cookie。 使用getKeys函数匹配Cookie，并使用removeItem函数删除Cookie。

**参数**

* **** 过滤器：在 `filter` 函数调用中使用的参 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 数。

* **** 选项：在 `options` 函数调用中使用的参 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 数。

**退货**

此函数不返回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

允许您将函数绑定到ContextHub存储事件并将其解除绑定。 访问ContextHub.Utils.使用存储的事件属性 [处理存储](/help/sites-developing/contexthub-api.md#eventing) 的事件对象。

### 函数(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

从事件中解除函数绑定。

**参数**

* **** name:要 [为其解除函数绑定的事件](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 的名称。

* **** 选择器：标识绑定的选择器。 (请参阅 `selector` on和once函 [数](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 的参数 [](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) )。

**退货**

此函数不返回任何值。

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 每次发生事件时都会调用该函数。 或者，可以为过去在建立绑定之前发生的事件调用该函数。

**参数**

* **** name:（字符串） [要将函数绑定到](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 的事件的名称。

* **** 处理函数：（函数）要绑定到事件的函数。
* **** 选择器：（字符串）绑定的唯一标识符。 如果要使用函数删除绑定，则需要选择器来标 `off` 识绑定。

* **** triggerForPastEvents:（布尔值）指示是否应为过去发生的事件执行该处理函数。 调用过去 `true` 事件的处理函数的值。 值调用了 `false` 未来事件的处理器。 默认值为 `true`.

**退货**

当参 `triggerForPastEvents` 数为 `true`时，此函数返回一个值，指 `boolean` 示事件是否发生在过去：

* `true`:该事件发生在过去，将调用该处理函数。
* `false`:以前没有发生过此事件。

如果 `triggerForPastEvents` 是 `false`，则此函数不返回值。

**示例**

以下示例将一个函数绑定到geolocation存储的data事件。 该函数使用商店中纬度数据项的值填充页面上的元素。

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 对于事件的第一次出现，只调用一次函数。 或者，可以为过去在建立绑定之前发生的事件调用函数。

**参数**

* **** name:（字符串） [要将函数绑定到](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 的事件的名称。

* **** 处理函数：（函数）要绑定到事件的函数。
* **** 选择器：（字符串）绑定的唯一标识符。 如果要使用函数删除绑定，则需要选择器来标 `off` 识绑定。

* **** triggerForPastEvents:（布尔值）指示是否应为过去发生的事件执行该处理函数。 调用过去 `true` 事件的处理函数的值。 值调用了 `false` 未来事件的处理器。 默认值为 `true`.

**退货**

当参 `triggerForPastEvents` 数为 `true`时，此函数返回一个值，指 `boolean` 示事件是否发生在过去：

* `true`:该事件发生在过去，将调用该处理函数。
* `false`:以前没有发生过此事件。

如果 `triggerForPastEvents` 是 `false`，则此函数不返回值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

允许对象继承另一个对象的属性和方法的实用程序类。

### 函数(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

使对象继承另一个对象的属性和方法。

**参数**

* **** child:（对象）继承的对象。
* **** 父项：（对象）定义继承的属性和方法的对象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供将对象序列化为JSON格式并将JSON字符串反序列化为对象的函数。

### 函数(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

将字符串值解析为JSON，并将其转换为javascript对象。

**参数**

* **** 数据：JSON格式的字符串值。

**退货**

Javascript对象。

**示例**

代码返 `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 回以下对象：

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

将Javascript值和对象序列化为JSON格式的字符串值。

**参数**

* **** 数据：要序列化的值或对象。 此函数支持布尔值、数组值、数字值、字符串值和日期值。

**退货**

序列化字符串值。 当 `data` 是R值 `egExp` 时，此函数返回空对象。 当 `data` 是函数时，返回 `undefined`。

**示例**

以下代码返回 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

该类便于处理要存储或从ContextHub存储中检索的数据对象。

### 函数(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

创建数据对象的副本，并从第二个对象添加到数据树中。 该函数返回副本，但不修改任何原始对象。 当两个对象的数据树包含相同的键时，第二对象的值将覆盖第一对象的值。

**参数**

* **** 树：所复制的对象。
* **** secondTree:与对象副本合并的对 `tree` 象。

**退货**

包含合并数据的对象。

#### cleanup() {#cleanup}

创建对象的副本，查找并删除数据树中不包含值、空值或未定义值的项，并返回该副本。

**参数**

* **** 树：要清理的对象。

**退货**

已清除的树的副本。

#### getItem() {#getitem}

从键的对象中检索值。

**参数**

* **** 树：数据对象。
* **** 键：要检索的值的键。

**退货**

与键相关的值。 当键具有子键时，此函数返回一个复杂对象。 当键的值类型为时 `undefined`, `null` 将返回。

**示例**

请考虑以下Javascript对象：

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

以下示例代码返回值 `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

以下示例代码检索具有子项的键的值：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

该函数返回以下对象：

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

从对象的数据树中检索所有键。 或者，您也可以仅检索特定键子项的键。 您还可以选择指定检索到的键的排序顺序。

**参数**

* **** 树：要从中检索数据树密钥的对象。
* **** 父项：（可选）要检索子项的键的数据树中项的键。
* **** 订单：（可选）确定返回键的排序顺序的函数。 (请参 [阅Mozilla Developer network上的Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 。)

**退货**

一组键。

**示例**

请考虑以下对象：

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

该脚 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 本返回以下数组：

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

创建给定对象的副本，从数据树中删除指定的分支，并返回修改后的副本。

**参数**

* 树：数据对象。
* 键：要删除的键。

**退货**

删除了键的原始数据对象的副本。

**示例**

请考虑以下对象：

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

以下示例脚本从数据树中删除/one/two/three/four分支：

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

该函数返回以下对象：

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

清理字符串值，使其可用作键。 要清理字符串，此函数将执行以下操作：

* 将多个连续正斜杠减少为一个斜杠。
* 从字符串的开头和结尾删除空格。
* 将结果拆分为一组用斜杠划分的字符串。

使用生成的数组创建可用键。  **参数**

* **** 键：要进 `string` 行清理。

**退货**

一组值， `string` 其中每个字符串是由斜杠划分 `key` 的部分。 表示已清理的密钥。 如果经过清理的数组的长度为零，则此函数返回 `null`。

**示例**

以下代码清理字符串以生成数组 `["this", "is", "a", "path"]`，然后从数组 `"/this/is/a/path"` 生成键：

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

将键／值对添加到对象副本的数据树中。 有关数据树的信息，请参阅 [持久性](/help/sites-developing/contexthub.md#persistence)。

**参数**

* 树：数据对象。
* 键：要与要添加的值关联的键。 关键是数据树中项的路径。 此函数调 `ContextHub.Utils.JSON.tree.sanitize` 用以在添加密钥之前对其进行清理。
* value:要添加到数据树的值。

**退货**

包含该／对 `tree` 的对象的 `key`副 `value` 本。

**示例**

请考虑以下Javascript代码：

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

myObject对象具有以下值：

## ContextHub.Utils.storeConapits {#contexthub-utils-storecandidates}

允许您注册商店候选人，并获取注册的商店候选人。

### 函数(ContextHub.Utils.storeCandiates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCanapites(storeType) {#getregisteredcandidates-storetype}

返回注册为存储候选项的存储类型。 检索特定存储类型或所有存储类型的已注册证书。

**参数**

* **** storeType:（字符串）存储类型的名称。 请参阅 `storeType` 函数的参 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 数。

**退货**

存储类型的对象。 对象属性是存储类型名称，属性值是一组已注册的存储候选项。

#### getStoreFromCanapites(storeType) {#getstorefromcandidates-storetype}

从注册候选者返回存储类型。 如果注册了多个同名的存储类型，则函数将返回具有最高优先级的存储类型。

**参数**

* storeType:（字符串）商店候选者的名称。 请参阅 `storeType` 函数的参 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 数。

**退货**

表示已注册存储候选项的对象。 如果未注册所请求的存储类型，则会引发错误。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回注册为商店候选者的商店类型的名称。 此函数不需要任何参数。

**退货**

字符串值的数组，其中每个字符串是注册存储候选项的存储类型。 请参阅 `storeType` 函数的参 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 数。

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名称和优先级将存储对象注册为存储候选对象。

优先级是指示同名商店重要性的数字。 当使用与已注册的存储候选者相同的名称注册存储候选者时，使用具有较高优先级的候选者。 当注册存储候选者时，仅当优先级高于同名注册存储候选者时，才注册存储。

**参数**

* **** 商店：（对象）要注册为存储候选的存储对象。
* **** storeType:（字符串）商店候选者的名称。 创建商店候选的实例时需要此值。
* **** 优先级：（数字）商店候选者的优先级。
* **** 应用：（函数）用于评估当前环境中存储的可应用性的函数。 如果存储适 `true` 用，则该函数必须返回，否则 `false` 返回。 默认值是返回true的函数： `function() {return true;}`

**示例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

