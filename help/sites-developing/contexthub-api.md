---
title: ContextHub JavaScript API参考
description: 将ContextHub组件添加到页面后，脚本即可使用ContextHub JavaScript API
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub
exl-id: b472d96f-b1a5-40b7-be2a-52f3396f6884
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '5002'
ht-degree: 2%

---

# ContextHub JavaScript API参考{#contexthub-javascript-api-reference}

在以下情况下，您的脚本可以使用ContextHub JavaScript API： [已将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## contexthub常量 {#contexthub-constants}

ContextHub JavaScript API定义的常量值。

### 事件常量 {#event-constants}

下表列出了ContextHub存储区发生的names事件。 另请参阅 [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| 常量 | 描述 | 价值 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub的事件命名空间 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 指示所有必需的存储已注册、初始化并准备使用 | 全店就绪 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 指示在给定的超时时间内并非所有存储都已初始化 | 存储 — 部分就绪 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 在注册存储时触发 | 存储注册 |
| ContextHub.Constants.EVENT_STORE_READY | 指示存储已准备就绪。 它在注册后立即触发，但JSONP存储除外，它在获取数据时触发)。 | 存储就绪 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 在存储更新其持久性时触发 | 存储已更新 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 持久性容器名称 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 存储原始JSON结果的特定持久性键名称 | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | 存储指示何时获取JSON数据的特定时间戳 | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 存储上次调用期间使用的JSON服务的特定URL | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | 指示ContextHub的UI是否展开 | /_/container-expanded |

### UI事件常量 {#ui-event-constants}

下表列出了ContextHub UI中发生的事件名称。

| **常量** | **描述** | **值** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 在注册模式时触发 | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 在模式取消注册时触发 | ui-mode-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 在注册模式渲染器时触发 | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 在取消注册模式渲染器时触发 | ui-mode-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 在添加新模式时触发 | 已添加ui-mode |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 在删除模式时触发 | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 在用户选择模式时触发 | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 注册新模块时触发 | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 在模块取消注册时触发 | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 在注册模块渲染器时触发 | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 在模块渲染器取消注册时触发 | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 在添加新模块时触发 | 已添加ui-module |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 删除模块时触发 | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | 在将UI容器添加到页面时触发 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | 在ContextHub UI打开时触发 | ui-container-open |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | 在ContextHub UI折叠时触发 | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 在修改属性时触发 | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | 每次呈现ContextHub UI时触发（例如，在属性更改后） | ui-rendered |
| ContextHub.Constants.EVENT_UI_INITIALIZED | 在UI容器初始化时触发 | ui已初始化 |
| ContextHub.Constants.ACTIVE_UI_MODE | 指示活动的UI模式 | /_/active-ui-mode |

## ContextHub JavaScript API参考 {#contexthub-javascript-api-reference-2}

ContextHub对象提供对所有存储的访问权限。

### 函数(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

返回所有已注册的ContextHub存储。

此函数没有参数。

**返回**

包含所有ContextHub存储的对象。 每个存储都是一个与存储使用相同名称的对象。

**示例**

以下示例检索所有存储，然后检索地理位置存储：

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

将存储检索为JavaScript对象。

**参数**

* **名称：** 存储所注册的名称。

**返回**

表示存储的对象。

**示例**

以下示例检索地理位置存储：

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

表示ContextHub区段。 使用ContextHub.SegmentEngine.SegmentManager获取区段。

### 函数(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

将区段的名称作为字符串值返回。

#### getPath() {#getpath}

以String值的形式返回区段定义的存储库路径。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供对ContextHub区段的访问权限。

### 函数(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

返回在当前上下文中解析的段。 此函数没有参数。

**返回**

ContextHub.SegmentEngine.Segment对象的数组。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存储的基类。

### 属性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 对象。 使用此对象绑定函数以存储事件。 有关缺省值和初始化的信息，请参见 [init(name，config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

商店的名称。

#### persistence {#persistence}

contexthub.Utils.Persistence对象。 有关缺省值和初始化的信息，请参见 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 函数(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree， options) {#addallitems-tree-options}

将数据对象或数组与存储数据合并。 对象或数组中的每个键/值对都将添加到存储中(通过 `setItem` 函数)：

* **对象：** 键是属性名称。
* **数组：** 键是数组索引。

请注意，值可以是对象。

**参数**

* **树：** （对象或数组）要添加到存储的数据。
* **选项：** （对象）传递给setItem函数的选项的可选对象。 有关信息，请参见 `options` 参数 [setItem(key，value，options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**返回**

A `boolean` 值：

* 值 `true` 指示存储的数据对象。
* 值 `false` 指示数据存储保持不变。

#### addReference(key， anotherKey) {#addreference-key-anotherkey}

创建从一个键到另一个键的引用。 键不能引用自身。

**参数**

* **键：** 引用的键 `anotherKey`.

* **另一键：** 引用的键值 `key`.

**返回**

A `boolean` 值：

* 值 `true` 指示已添加引用。
* 值 `false` 表示未添加引用。

#### announceReadiness() {#announcereadiness}

触发 `ready` 此存储的事件。 此函数没有参数并且不返回任何值。

#### clean() {#clean}

从存储中删除所有数据。 该函数没有参数并且没有返回值。

#### getItem(key) {#getitem-key}

返回与键关联的值。

**参数**

* **键：** （字符串）要返回其值的键。

**返回**

表示键值的对象。

#### getKeys(includeInternals) {#getkeys-includeinternals}

从存储中检索密钥。 （可选）您可以检索ContextHub框架内部使用的键。

**参数**

* **includeInternals：** 值 `true` 在结果中包含内部使用的键。 这些键以下划线(“_”)字符开头。 默认值为 `false`。

**返回**

键名称数组( `string` 值)。

#### getReferences() {#getreferences}

从存储中检索引用。

**返回**

使用引用键作为引用键的索引的数组：

* 引用键与 `key` 的参数 `addReference` 函数。

* 引用的键对应于 `anotherKey` 的参数 `addReference` 函数。

#### getTree(includeInternals) {#gettree-includeinternals}

从存储中检索数据树。 或者，您也可以包含由ContextHub框架在内部使用的键/值对。

**参数**

* `includeInternals:` 值 `true` 在结果中包含内部使用的键/值对。 此数据的键以下划线(“_”)字符开头。 默认值为 `false`。

**返回**

表示数据树的对象。 键是对象的属性名称。

#### init(name， config) {#init-name-config}

初始化存储。

* 将存储数据设置为空对象。
* 设置对空对象的存储引用。
* eventChannel是数据：*name*，其中 *name* 是商店名称。

* storeDataKey为/store/*name*，其中 *name* 是商店名称。

**参数**

* **名称：** 商店的名称。
* **配置：** 包含配置属性的对象：

   * eventDeferring：默认值为32。
   * 事件： [contexthub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 此商店的对象。 默认值是ContextHub.eventing对象使用的值。
   * 持久性：此存储的ContextHub.Utils.Persistence对象。 默认值为ContextHub.persistence对象。

#### isEventingPaused() {#iseventingpaused}

确定是否暂停此存储的事件。

**返回**

布尔值：

* `true`：暂停事件，以便不为此存储触发任何事件。
* `false`：事件不会暂停，因此会为此存储触发事件。

#### pauseEventing() {#pauseeventing}

暂停存储的事件，以便不触发任何事件。 此函数不需要任何参数，也不返回任何值。

#### removeItem(key， options) {#removeitem-key-options}

从存储中删除键/值对。

删除某个键时，函数将触发 `data` 事件。 事件数据包括存储名称、已删除键的名称、已删除的值、键的新值(null)以及“删除”的操作类型。

或者，您可以防止触发 `data` 事件。

**参数**

* **键：** （字符串）要删除的键的名称。
* **选项：** （对象）选项的对象。 以下对象属性有效：

   * 静音：值 `true` 防止触发 `data` 事件。 默认值为 `false`。

**返回**

A `boolean` 值：

* 值 `true` 表示已删除键/值对。
* 值 `false` 表示数据存储未更改，因为未在存储中找到键。

#### removeReference(key) {#removereference-key}

从存储中删除引用。

**参数**

* **键：** 要删除的键引用。 此参数对应于 `key` 的参数 `addReference` 函数。

**返回**

A `boolean` 值：

* 值 `true` 表示引用已删除。
* 值 `false` 指示密钥无效且存储未更改。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重置存储保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的initialValues属性中提供。

**参数**

* **keepRemainingData：** （布尔）值为true会导致保留非初始数据。 如果值为false，则会删除初始值以外的所有数据。

重置存储保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的initialValues属性中提供。

**参数**

* keepRemainingData： （布尔值）如果值为true，则会保留非初始数据。 如果值为false，则会删除初始值以外的所有数据。

#### resolveReference(key， retry) {#resolvereference-key-retry}

检索引用的键。 或者，您可以指定用于解析最佳匹配的迭代次数。

**参数**

* **键：** （字符串）要为其解析引用的键。 此 `key` 参数对应于 `key` 的参数 `addReference` 函数。

* **重试：** （数量）要使用的迭代次数。

**返回**

A `string` 表示引用的键的值。 如果未解析任何引用，则 `key` 返回参数。

#### resumeEventing() {#resumeeventing}

恢复此存储的事件，以便触发事件。 此函数不定义任何参数也不返回任何值。

#### setItem(key， value， options) {#setitem-key-value-options}

向存储中添加键/值对。

触发 `data` 仅当键的值不同于当前为键存储的值时才会发生事件。 您可以选择防止触发 `data` 事件。

事件数据包括存储名称、键、上一个值、新值和操作类型 `set`.

**参数**

* **键：** （字符串）键的名称。
* **选项：** （对象）选项的对象。 以下对象属性有效：

   * 静音：值 `true` 防止触发 `data` 事件。 默认值为 `false`。

* **值：** （对象）要与键关联的值。

**返回**

A `boolean` 值：

* 值 `true` 指示存储的数据对象。
* 值 `false` 指示数据存储保持不变。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON数据的存储。 数据从外部JSONP服务或选择性地从返回JSON数据的服务中检索。 使用指定服务详细信息 [`init`](/help/sites-developing/contexthub-api.md#init-name-config) 函数中。

存储使用内存中持久性（JavaScript变量）。 存储数据仅在页面的生命周期内可用。

ContextHub.Store.JSONPStore扩展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 并继承了该类的功能。

### 函数(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig， override) {#configureservice-serviceconfig-override}

配置用于连接到此对象使用的JSONP服务的详细信息。 您可以更新或替换现有配置。 函数不返回任何值。

**参数**

* **服务配置：** 包含以下属性的对象：

   * host： （字符串）服务器名称或IP地址。
   * jsonp： （布尔值）如果值为true，则表示该服务为JSONP服务；否则为false。 如果为true，则{callback： &quot;ContextHub.Callbacks.*对象名称*}对象已添加到service.params对象。
   * params： （对象）表示为对象属性的URL参数。 参数名是属性名，参数值是属性值。
   * path： （字符串）服务的路径。
   * port： (Number)服务的端口号。
   * secure： （字符串或布尔值）确定用于服务URL的协议：

      * auto: //
      * true： https://
      * false： https://

* **覆盖：** （布尔型）。 值 `true` 导致现有服务配置被替换为 `serviceConfig`. 值 `false` 导致现有服务配置属性与的属性合并 `serviceConfig`.

#### getRawResponse() {#getrawresponse}

返回自上次调用JSONP服务以来缓存的原始响应。 函数不需要参数。

**返回**

表示原始响应的对象。

#### getServiceDetails() {#getservicedetails}

检索此ContextHub.Store.JSONPStore对象的服务对象。 服务对象包含创建服务URL所需的所有信息。

**返回**

具有以下属性的对象：

* **主机：** （字符串）服务器名称或IP地址。
* **jsonp：** （布尔）值为true表示服务是JSONP服务，否则为false。 如果为true，则{callback： &quot;ContextHub.Callbacks.*对象名称*}对象已添加到service.params对象。

* **参数：** （对象）表示为对象属性的URL参数。 参数名是属性名，参数值是属性值。
* **路径：** （字符串）服务的路径。
* **端口：** (Number)服务的端口号。
* **安全：** （字符串或布尔值）确定用于服务URL的协议：

   * auto: //
   * true： https://
   * false： https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

检索JSONP服务的URL。

**参数**

* **解决：** （布尔值）确定是否在URL中包含已解析的参数。 值 `true` 解析参数，以及 `false` 不会。

**返回**

A `string` 表示服务URL的值。

#### init(name， config) {#init-name-config-1}

初始化ContextHub.Store.JSONPStore对象。

**参数**

* **名称：** （字符串）存储的名称。
* **配置：** （对象）包含服务属性的对象。 JSONPStore对象使用 `service` 用于构建JSONP服务的URL的对象：

   * eventDeferring： 32。
   * 事件：此存储的ContextHub.Utils.Eventing对象。 默认值为 `ContextHub.eventing` 对象。
   * 持久性：此存储的ContextHub.Utils.Persistence对象。 默认情况下，使用内存持久性（JavaScript对象）。
   * 服务： （对象）

      * host： （字符串）服务器名称或IP地址。
      * jsonp： （布尔值）如果值为true，则表示该服务为JSONP服务；否则为false。 如果为True，则 `{callback: "ContextHub.Callbacks.*Object.name*}`对象已添加到 `service.params`.
      * params： （对象）表示为对象属性的URL参数。 参数名称和值分别是对象属性名称和值。
      * path： （字符串）服务的路径。
      * port： (Number)服务的端口号。
      * secure： （字符串或布尔值）确定用于服务URL的协议：

         * auto: //
         * true： https://
         * false： https://

      * timeout： (Number)超时前等待JSONP服务响应的时间（以毫秒为单位）。
      * ttl：在两次调用JSONP服务之间经过的最小时间（以毫秒为单位）。 (请参阅 [查询服务](/help/sites-developing/contexthub-api.md#queryservice-reload) 函数)。

#### queryService（重新加载） {#queryservice-reload}

查询远程JSONP服务并缓存响应。 如果自上次调用此函数后经过的时间小于的值 `config.service.ttl`，则不会调用服务，并且不会更改缓存的响应。 或者，您可以强制调用该服务。 此 `config.service.ttl`属性是在调用 [init](/help/sites-developing/contexthub-api.md#init-name-config) 函数以初始化存储。

查询完成后，触发就绪事件。 如果未设置JSONP服务URL，则函数将不执行任何操作。

**参数**

* **重新加载：** （布尔）值为true会删除缓存的响应并强制调用JSONP服务。

#### 重置 {#reset}

重置存储区保留数据的初始值，然后调用JSONP服务。 或者，您也可以从存储中删除所有其他数据。 重置初始值时，将暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的initialValues属性中提供。

**参数**

* **keepRemainingData：** （布尔）值为true会导致保留非初始数据。 如果值为false，则会删除初始值以外的所有数据。

#### resolveParameter(f) {#resolveparameter-f}

解析给定的参数。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore扩展 [contexthub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) 所以它继承了那个类的所有功能。 但是，根据ContextHub持久性的配置，将保留从JSONP服务检索的数据。 (请参阅 [持久性模式](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore扩展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 所以它继承了那个类的所有功能。 此存储中的数据将根据ContextHub持久性的配置进行保留。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore扩展 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 所以它继承了那个类的所有功能。 使用内存中持久性（JavaScript对象）保留此存储中的数据。

## ContextHub.UI {#contexthub-ui}

管理UI模块和UI模块渲染器。

### 函数(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType， renderer， dontRender) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub注册UI模块渲染器。 在注册渲染器后，它可用于 [创建用户界面模块](ch-configuring.md#adding-a-ui-module). 请在以下情况下使用此函数： [扩展ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) 以创建自定义UI模块渲染器。

**参数**

* **模块类型：** （字符串） UI模块渲染器的标识符。 如果已经使用指定的值注册了渲染器，则在注册此渲染器之前将取消注册现有渲染器。
* **呈现器：** （字符串）呈现UI模块的类的名称。
* **不渲染：** （布尔值）设置为 `true` 以防止在注册渲染器后渲染ContextHub UI。 默认值为 `false`。

**示例**

以下示例将渲染器注册为contexthub.browserinfo模块类型。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

用于与Cookie交互的实用程序类。

### 函数(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### 存在（键） {#exists-key}

确定Cookie是否存在。

**参数**

* **键：** A `String` 其中包含您正在测试的Cookie的键。

**返回**

A `boolean` 值为true表示该Cookie存在。

**示例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

返回其键与过滤器匹配的所有Cookie。

**参数**

* （可选） **过滤器：** 匹配Cookie键的条件。 要返回所有Cookie，请不要指定任何值。 支持以下类型：

   * 字符串：将字符串与Cookie键进行比较。
   * 数组：数组中的每一项都是一个过滤器。
   * RegExp对象：对象的测试函数用于匹配Cookie键。
   * 函数：测试Cookie键以查找匹配项的函数。 该函数必须将Cookie密钥作为参数，如果测试确认匹配，则返回true。

**返回**

Cookie的对象。 对象属性是Cookie键，键值是Cookie值。

**示例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

返回Cookie值。

**参数**

* **键：** 您希望获取其值的Cookie的键。

**返回**

Cookie值，或 `null` 如果未找到键的Cookie，则为。

**示例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

返回与过滤器匹配的现有Cookie键的数组。

**参数**

* **过滤器：** 匹配Cookie键的条件。 支持以下类型：

   * 字符串：将字符串与Cookie键进行比较。
   * 数组：数组中的每一项都是一个过滤器。
   * RegExp对象：对象的测试函数用于匹配Cookie键。
   * 函数：测试Cookie键以查找匹配项的函数。 函数必须将Cookie密钥作为参数并返回 `true` 如果测试确认匹配。

**返回**

一个字符串数组，其中每个字符串是与过滤器匹配的Cookie的键。

**示例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key， options) {#removeitem-key-options-1}

删除Cookie。 要删除Cookie，该值将设置为空字符串，并且到期日期将设置为当前日期之前的日期。

**参数**

* **键：** A `String` 表示要删除的Cookie键的值。

* **选项：** 包含用于配置Cookie属性的属性值的对象。 请参阅 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 函数以获取信息。 此 `expires` 属性无效。

**返回**

此函数不返回值。

**示例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key， value， options) {#setitem-key-value-options-1}

创建给定键和值的Cookie，并将Cookie添加到当前文档。 （可选）您可以指定用于配置Cookie属性的选项。

**参数**

* **键：** 包含Cookie键的字符串。
* **值：** 包含Cookie值的字符串。
* **选项：** （可选）一个对象，它包含以下任何可配置Cookie属性的属性：

   * 过期：A `date` 或 `number` 值，指定Cookie的过期时间。 日期值指定绝对到期时间。 一个数字（以天为单位）将过期时间设置为当前时间加上数字。 默认值为 `undefined`。
   * 安全：A `boolean` 值，指定 `Secure` Cookie的属性。 默认值为 `false`。
   * 路径： A `String` 要用作的值 `Path` Cookie的属性。 默认值为 `undefined`。

**返回**

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

删除与给定过滤器匹配的所有Cookie。 Cookie是使用getKeys函数匹配的，并使用removeItem函数删除的。

**参数**

* **过滤器：** 此 `filter` 要在调用中使用的参数 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 函数。

* **选项：** 此 `options` 要在调用中使用的参数 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 函数。

**返回**

此函数不返回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

允许您将函数绑定和取消绑定到ContextHub存储事件。 使用访问存储的ContextHub.Utils.Eventing对象 [事件](/help/sites-developing/contexthub-api.md#eventing) 存储的属性。

### 函数(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name， selector) {#off-name-selector}

从事件中取消绑定函数。

**参数**

* **名称：** 此 [事件的名称](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) ，您将为其取消绑定函数。

* **选择器：** 标识绑定的选择器。 (请参阅 `selector` 的参数 [日期](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 和 [一次](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函数)。

**返回**

此函数不返回任何值。

#### on(name， handler， selector， triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 每次事件发生时都会调用函数。 或者，可以为过去发生的事件（在建立绑定之前）调用函数。

**参数**

* **名称：** （字符串） [事件的名称](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 函数将绑定到的对象。

* **处理程序：** （函数）绑定到事件的函数。
* **选择器：** （字符串）绑定的唯一标识符。 如果要使用 `off` 函数以移除绑定。

* **triggerForPastEvents：** （布尔值）指示是否应为过去发生的事件执行处理程序。 值 `true` 调用过去事件的处理程序。 值 `false` 为将来的活动调用汉堡。 默认值为 `true`。

**返回**

当 `triggerForPastEvents` 参数为 `true`，此函数返回 `boolean` 指示事件是否过去发生的值：

* `true`：该事件发生在过去，并将调用处理程序。
* `false`：该事件在过去未发生过。

如果 `triggerForPastEvents` 是 `false`，此函数不返回任何值。

**示例**

以下示例将函数绑定到地理位置存储的数据事件。 函数会使用存储中的latitude数据项的值填充页面上的元素。

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

#### once(name， handler， selector， triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 函数只调用一次，以首次显示该事件。 或者，可以为过去发生的事件（在建立绑定之前）调用函数。

**参数**

* **名称：** （字符串） [事件的名称](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 函数将绑定到的对象。

* **处理程序：** （函数）绑定到事件的函数。
* **选择器：** （字符串）绑定的唯一标识符。 如果要使用 `off` 函数以移除绑定。

* **triggerForPastEvents：** （布尔值）指示是否应为过去发生的事件执行处理程序。 值 `true` 调用过去事件的处理程序。 值 `false` 为将来的活动调用汉堡。 默认值为 `true`。

**返回**

当 `triggerForPastEvents` 参数为 `true`，此函数返回 `boolean` 指示事件是否过去发生的值：

* `true`：该事件发生在过去，并将调用处理程序。
* `false`：该事件在过去未发生过。

如果 `triggerForPastEvents` 是 `false`，此函数不返回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

一个实用程序类，它允许对象继承另一个对象的属性和方法。

### 函数(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child， parent) {#inherit-child-parent}

使一个对象继承另一个对象的属性和方法。

**参数**

* **子项：** （对象）继承的对象。
* **父项：** （对象）定义继承的属性和方法的对象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供将对象序列化为JSON格式并将JSON字符串反序列化为对象的函数。

### 函数(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

将字符串值解析为JSON并将其转换为Javascript对象。

**参数**

* **数据：** JSON格式的字符串值。

**返回**

javascript对象。

**示例**

代码 `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 返回以下对象：

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### strinify(data) {#stringify-data}

将JavaScript值和对象序列化为JSON格式的字符串值。

**参数**

* **数据：** 要序列化的值或对象。 此函数支持布尔值、数组、数字、字符串和日期值。

**返回**

序列化的字符串值。 时间 `data` 是R `egExp` 值，此函数返回空对象。 时间 `data` 是一个函数，返回 `undefined`.

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

此类便于处理要存储的数据对象或从ContextHub存储中检索的数据对象。

### 函数(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

创建数据对象的副本，并将来自第二个对象的数据树添加到该副本。 该函数将返回副本，并且不会修改任何原始对象。 当两个对象的数据树包含相同的键时，第二对象的值覆盖第一对象的值。

**参数**

* **树：** 复制的对象。
* **secondTree：** 与的副本合并的对象 `tree` 对象。

**返回**

包含合并数据的对象。

#### cleanup() {#cleanup}

创建对象的副本，在数据树中查找和删除不包含值、空值或未定义的值的项，并返回副本。

**参数**

* **树：** 要清理的对象。

**返回**

已清理的树的副本。

#### getItem() {#getitem}

从键的对象中检索值。

**参数**

* **树：** 数据对象。
* **键：** 要检索的值的键。

**返回**

与键对应的值。 当键具有子键时，此函数返回一个复杂的对象。 当键值的类型为 `undefined`， `null` 会返回。

**示例**

请考虑以下JavaScript对象：

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

以下示例代码返回值 `260`：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

以下示例代码检索具有子键的键的值：

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

此函数返回以下对象：

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

从对象的数据树中检索所有键。 或者，您只能检索特定键的子项键。 您还可以选择指定检索到的键的排序顺序。

**参数**

* **树：** 从中检索数据树键的对象。
* **父项：** （可选）数据树中要检索其子项键的项的键。
* **订购：** （可选）确定返回键的排序顺序的函数。 (请参阅 [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) ，位于Mozilla开发人员网络上。)

**返回**

键数组。

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

此 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 脚本返回以下数组：

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

创建给定对象的副本，从数据树中删除指定分支，并返回修改后的副本。

**参数**

* 树：数据对象。
* key：要删除的键。

**返回**

已删除键的原始数据对象的副本。

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

此函数返回以下对象：

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

清理字符串值，使其可用作键。 要整理字符串，此函数将执行以下操作：

* 将多个连续正斜杠减少为单个斜杠。
* 删除字符串开头和结尾的空格。
* 将结果拆分为以斜杠分隔的字符串数组。

使用结果数组创建一个可用的键。  **参数**

* **键：** 此 `string` 去消毒。

**返回**

数组 `string` 值，其中每个字符串是 `key` 用斜线来分隔。 表示经过清理的密钥。 如果经过清理的数组的长度为零，则此函数将返回 `null`.

**示例**

以下代码可清理字符串以生成数组 `["this", "is", "a", "path"]`，然后生成键 `"/this/is/a/path"` 从数组：

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree， key， value) {#setitem-tree-key-value}

将键/值对添加到对象副本的数据树中。 有关数据树的信息，请参阅 [持久性](/help/sites-developing/contexthub.md#persistence).

**参数**

* 树：数据对象。
* key：要与您添加的值关联的键。 键值是数据树中项目的路径。 此函数调用 `ContextHub.Utils.JSON.tree.sanitize` 以在添加密钥之前对其进行整理。
* value：要添加到数据树的值。

**返回**

副本 `tree` 包含 `key`/ `value` 配对。

**示例**

请考虑以下JavaScript代码：

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

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

使您能够注册候选商店和获取已注册的候选商店。

### 函数(ContextHub.Utils.storeCategors) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

返回注册为商店候选商店的存储类型。 检索特定存储类型或所有存储类型的已注册候选文件。

**参数**

* **storeType：** （字符串）存储类型的名称。 请参阅 `storeType` 的参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函数。

**返回**

存储类型的对象。 对象属性是存储类型名称，属性值是已注册的存储候选数组。

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

从已注册的候选中返回存储类型。 如果注册了多个同名存储类型，此函数将返回具有最高优先级的存储类型。

**参数**

* storeType： （字符串）存储候选的名称。 请参阅 `storeType` 的参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函数。

**返回**

一个对象，表示已注册的存储候选。 如果未注册所请求的存储类型，则会引发错误。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回注册为存储候选的存储类型名称。 此函数不需要参数。

**返回**

一个字符串值数组，其中每个字符串是用来注册存储候选的存储类型。 请参阅 `storeType` 的参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 函数。

#### registerStoreCandidate(store， storeType， priority， applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名称和优先级将存储对象注册为存储候选项。

优先级是一个数字，它指示同名存储的重要性。 当使用与已注册的存储候选相同的名称注册存储候选时，使用具有较高优先级的候选。 在注册存储候选时，仅当优先级高于同名已注册的存储候选时才注册存储。

**参数**

* **存储：** （对象）注册为存储候选的存储对象。
* **storeType：** （字符串）商店候选者的名称。 创建存储候选实例时需要此值。
* **优先级：** （编号）商店候选的优先级。
* **应用：** （函数）要调用的函数，用于评估存储在当前环境中的适用性。 函数必须返回 `true` 如果该存储区适用，并且 `false` 否则。 默认值是一个返回true的函数： `function() {return true;}`

**示例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
