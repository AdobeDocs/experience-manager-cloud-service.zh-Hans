---
title: ContextHub Javascript API参考
description: 将ContextHub组件添加到页面后，您的脚本可以使用ContextHub Javascript API
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '4622'
ht-degree: 2%

---

# ContextHub Javascript API参考 {#contexthub-javascript-api-reference}

当 [ContextHub组件已添加到页面](adding-contexthub.md).

## ContextHub常量 {#contexthub-constants}

ContextHub Javascript API定义的常量值。

### 事件常量 {#event-constants}

下表列出了ContextHub存储发生的名称事件。 另请参阅 [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| 常量 | 描述 | 值 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub的事件命名空间 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 指示所有必需的存储都已注册、初始化并准备使用 | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 表示并非所有存储都在给定的超时内初始化 | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | 注册商店时触发 | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | 表示存储已准备就绪，可以工作。 注册后会立即触发该事件，但JSONP存储除外，在那里获取数据时会触发该事件)。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | 存储更新其持久性时触发 | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 持久性容器名称 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 存储存储原始JSON结果的特定持久性键名称 | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | 存储指示何时获取JSON数据的特定时间戳 | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 存储上次调用期间使用的JSON服务的特定URL | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | 指示ContextHub的UI是否已展开 | `/_/container-expanded` |

### UI事件常量 {#ui-event-constants}

下表列出了ContextHub UI中发生的事件的名称。

| **常量** | **描述** | **值** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | 注册模式时触发 | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | 取消注册模式时触发 | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | 注册模式渲染器时触发 | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | 未注册模式渲染器时触发 | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 添加新模式时触发 | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | 删除模式时触发 | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | 用户选择模式时触发 | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 注册新模块时触发 | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | 取消注册模块时触发 | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | 注册模块渲染器时触发 | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | 未注册模块渲染器时触发 | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 添加新模块时触发 | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | 删除模块时触发 | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | 将UI容器添加到页面时触发 | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | 打开ContextHub UI时触发 | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | 折叠ContextHub UI时触发 | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | 修改属性时触发 | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | 每次呈现ContextHub UI时（例如，在属性更改后）均触发 | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | 初始化UI容器时触发 | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | 指示活动UI模式 | `/_/active-ui-mode` |

## ContextHub Javascript API参考 {#contexthub-javascript-api-reference-2}

ContextHub对象提供对所有存储的访问。

### 函数(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

返回所有注册的ContextHub存储。

此函数没有参数。

##### 返回结果 {#returns-}

包含所有ContextHub存储的对象。 每个存储都是一个使用与存储相同名称的对象。

##### 示例 {#example-}

以下示例检索所有存储区，然后检索地理位置存储区：

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

检索存储作为Javascript对象。

##### 参数 {#parameters-}

* **`name`:** 用于注册商店的名称。

##### 返回结果 {#returns-getstore-name}

表示存储的对象。

##### 示例 {#example-getstore-name}

以下示例检索地理位置存储：

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

表示ContextHub区段。 使用 `ContextHub.SegmentEngine.SegmentManager` 以获取区段。

### 函数(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

将区段的名称作为字符串值返回。

#### getPath() {#getpath}

将区段定义的存储库路径作为字符串值返回。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供对ContextHub区段的访问。

### 函数(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

返回在当前上下文中解析的区段。 此函数没有参数。

##### 返回结果 {#returns-getresolvedsegments}

数组 `ContextHub.SegmentEngine.Segment` 对象。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存储的基类。

### 属性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) 对象。 使用此对象绑定函数以存储事件。 有关默认值和初始化的信息，请参阅 [`init(name,config)`](#init-name-config).

#### name {#name}

商店的名称。

#### 持久性 {#persistence}

A `ContextHub.Utils.Persistence` 对象。 有关默认值和初始化的信息，请参阅 [`init(name,config)`](#init-name-config).

### 函数(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree， options) {#addallitems-tree-options}

将数据对象或数组与存储数据合并。 对象或数组中的每个键/值对都会添加到存储中(通过 `setItem` 函数):

* **对象：** 键是属性名称。
* **阵列：** 键是数组索引。

请注意，值可以是对象。

##### 参数 {#parameters-addallitems}

* **`tree`:** （对象或数组）要添加到存储中的数据。
* **`options`:** （对象）传递到setItem函数的选项的可选对象。 有关信息，请参阅 `options` 参数 [`setItem(key,value,options)`](#setitem-key-value-options).

##### 返回结果 {#returns-addallitems}

A `boolean` 值：

* 值 `true` 指示存储了数据对象。
* 值 `false` 表示数据存储未更改。

#### addReference(key， anotherKey) {#addreference-key-anotherkey}

创建从一个键到另一个键的引用。 键不能引用自身。

##### 参数 {#parameters-addreference}

* **`key`:** 引用的键 `anotherKey`.

* **`anotherkey`:** 引用的键 `key`.

##### 返回结果 {#returns-addreference}

A `boolean` 值：

* 值 `true` 表示已添加引用。
* 值 `false` 表示未添加引用。

#### announceReadiness() {#announcereadiness}

触发 `ready` 事件。 此函数没有参数，且不返回任何值。

#### clean() {#clean}

从存储中删除所有数据。 函数没有参数，也没有返回值。

#### getItem(key) {#getitem-key}

返回与键值关联的值。

##### 参数 {#parameters-getitem}

* **`key`:** （字符串）要返回值的键。

##### 返回结果 {#returns-getitem}

表示键值的对象。

#### getKeys(includeInternals) {#getkeys-includeinternals}

从存储中检索键。 或者，您也可以检索ContextHub框架内部使用的键。

##### 参数 {#parameters-getkeys}

* **`includeInternals`:** 值 `true` 结果中包含内部使用的键。 这些键以下划线(`_`)字符。 默认值为 `false`。

##### 返回结果 {#returns-getkeys}

键名称数组( `string` 值)。

#### getReferences() {#getreferences}

从存储中检索引用。

##### 返回结果 {#returns-getreferences}

使用引用键作为引用键的索引的数组：

* 引用键值与 `key` 参数 `addReference` 函数。
* 引用的键与 `anotherKey` 参数 `addReference` 函数。

#### getTree(includeInternals) {#gettree-includeinternals}

从存储中检索数据树。 或者，您也可以包含ContextHub框架在内部使用的键/值对。

##### 参数 {#parameters-gettree}

* `includeInternals:` 值 `true` 结果中包含内部使用的键/值对。 此数据的键以下划线(`_`)字符。 默认值为 `false`。

##### 返回结果 {#returns-gettree}

表示数据树的对象。 键是对象的属性名称。

#### init(name， config) {#init-name-config}

初始化存储。

* 将存储数据设置为空对象。
* 设置对空对象的存储引用。
* 的 `eventChannel` is `data:<name>`，其中 `<name>` 是商店名称。
* 的 `storeDataKey` is `/store/<name>`，其中 `<name>` 是商店名称。

##### 参数 {#parameters-init}

* **`name`:** 商店的名称。
* **`config`:** 包含配置属性的对象：
   * `eventDeferring`:默认值为32。
   * `eventing`:的 [ContextHub.Utils.Eventing](#contexthub-utils-eventing) 对象。 默认值为 `ContextHub.eventing` 对象使用。
   * `persistence`:的 `ContextHub.Utils.Persistence` 对象。 默认值为 `ContextHub.persistence` 对象。

#### isEventingPaused() {#iseventingpaused}

确定是否暂停此存储的事件。

##### 返回结果 {#returns-iseventingpaused}

布尔值：

* `true`:事件暂停，因此不会为此存储触发任何事件。
* `false`:事件不会暂停，因此会为此存储触发事件。

#### pauseEventing() {#pauseeventing}

会暂停存储的事件，以便不触发任何事件。 此函数不需要任何参数，也不返回任何值。

#### removeItem(key， options) {#removeitem-key-options}

从存储中删除键/值对。

删除键后，函数将触发 `data` 事件。 事件数据包括存储名称、已删除键的名称、已删除的值、键的新值(null)以及“remove”操作类型。

或者，您也可以选择阻止触发 `data` 事件。

##### 参数 {#parameters-removeitem}

* **`key`:** （字符串）要删除的键的名称。
* **`options`:** （对象）选项的对象。 以下对象属性有效：
   * 沉默：值 `true` 阻止触发 `data` 事件。 默认值为 `false`。

##### 返回结果 {#returns-removeitem}

A `boolean` 值：

* 值 `true` 表示已删除键/值对。
* 值 `false` 表示数据存储未更改，因为在存储中未找到密钥。

#### removeReference(key) {#removereference-key}

从存储中删除引用。

##### 参数 {#parameters-removereference}

* **`key`:** 要删除的键引用。 此参数与 `key` 参数 `addReference` 函数。

##### 返回结果 {#returns-removereference}

A `boolean` 值：

* 值 `true` 表示已删除引用。
* 值 `false` 表示键无效，且存储未更改。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重置存储保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时，会暂停此存储的事件。 此函数不返回任何值。

初始值在 `initialValues` 用于实例化存储对象的配置对象的属性。

##### 参数 {#parameters-reset}

* **`keepRemainingData`**:（布尔值）如果值为true，则会保留非初始数据。 如果值为false，则会删除除初始值之外的所有数据。

#### resolveReference(key， retry) {#resolvereference-key-retry}

检索引用的键值。 或者，您可以指定用于解析最佳匹配的迭代次数。

##### 参数 {#parameters-resolvereference}

* **`key`:** （字符串）要解析引用的键。 此 `key` 参数与 `key` 参数 `addReference` 函数。
* **`retry`:** （数字）要使用的小版本数。

##### 返回结果 {#returns-resolvereference}

A `string` 表示引用键值的值。 如果未解析引用，则 `key` 参数。

#### resumeEventing() {#resumeeventing}

恢复此存储的事件，以便触发事件。 此函数未定义任何参数，且不返回任何值。

#### setItem(key， value， options) {#setitem-key-value-options}

向存储添加键/值对。

触发 `data` 事件。 您可以选择阻止触发 `data` 事件。

事件数据包括存储名称、键、上一个值、新值和操作类型 `set`.

##### 参数 {#parameters-setitem}

* **`key`:** （字符串）键的名称。
* **`options`:** （对象）选项的对象。 以下对象属性有效：
   * `silent`:值 `true` 阻止触发 `data` 事件。 默认值为 `false`。
* **`value`:** （对象）要与键关联的值。

##### 返回结果 {#returns-setitem}

A `boolean` 值：

* 值 `true` 指示存储了数据对象。
* 值 `false` 表示数据存储未更改。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON数据的商店。 数据是从外部JSONP服务中检索，或者（可选）从返回JSON数据的服务中检索。 使用指定服务详细信息 [`init`](#init-name-config) 函数。

存储使用内存中的永久性（Javascript变量）。 存储数据仅在页面的生命周期内可用。

ContextHub.Store.JSONPStore扩展 [ContextHub.Store.Core](#contexthub-store-core) 并继承该类的函数。

### 函数(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig， override) {#configureservice-serviceconfig-override}

配置用于连接到此对象所使用的JSONP服务的详细信息。 您可以更新或替换现有配置。 该函数不返回任何值。

##### 参数 {#parameters-configureservice}

* **`serviceConfig`:** 包含以下属性的对象：
   * `host`:（字符串）服务器名称或IP地址。
   * `jsonp`:（布尔值）值为true表示该服务是JSONP服务，否则为false。 如果为true，则为{callback:&quot;ContextHub.回调。*Object.name*}对象已添加到service.params对象。
   * `params`:（对象）表示为对象属性的URL参数。 参数名称是属性名称，参数值是属性值。
   * `path`:（字符串）服务的路径。
   * `port`:（数字）服务的端口号。
   * `secure`:（字符串或布尔值）确定用于服务URL的协议：
      * `auto`: //
      * `true`:https://
      * `false`: http://
* **覆盖：** （布尔值）。 值 `true` 导致现有服务配置被 `serviceConfig`. 值 `false` 导致现有服务配置属性与 `serviceConfig`.

#### getRawResponse() {#getrawresponse}

返回自上次调用JSONP服务后缓存的原始响应。 函数不需要任何参数。

##### 返回结果 {#returns-getrawresponse}

表示原始响应的对象。

#### getServiceDetails() {#getservicedetails}

检索此ContextHub.Store.JSONPStore对象的服务对象。 服务对象包含创建服务URL所需的所有信息。

##### 返回结果 {#returns-getservicedetails}

具有以下属性的对象：

* **`host`:** （字符串）服务器名称或IP地址。
* **`jsonp`:** （布尔值）值为true表示该服务是JSONP服务，否则为false。 如果为true，则为{callback:&quot;ContextHub.回调。*Object.name*}对象已添加到service.params对象。
* **`params`:** （对象）表示为对象属性的URL参数。 参数名称是属性名称，参数值是属性值。
* **`path`:** （字符串）服务的路径。
* **`port`:** （数字）服务的端口号。
* **`secure`:** （字符串或布尔值）确定用于服务URL的协议：
   * `auto`://
   * `true`:https://
   * `false`:http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

检索JSONP服务的URL。

##### 参数 {#parameters-getserviceurl}

* **`resolve`:** （布尔）确定是否在URL中包含已解析的参数。 值 `true` 解析参数和 `false` 不会。

##### 返回结果 {#returns-getserviceurl}

A `string` 表示服务URL的值。

#### init(name， config) {#init-name-config-1}

初始化 `ContextHub.Store.JSONPStore` 对象。

##### 参数 {#parameters-init-1}

* **`name`:** （字符串）存储的名称。
* **`config`:** （对象）包含服务属性的对象。 JSONPStore对象使用 `service` 用于构建JSONP服务URL的对象：
   * `eventDeferring`:32.
   * `eventing`:此存储的ContextHub.Utils.Eventing对象。 默认值为 `ContextHub.eventing` 对象。
   * `persistence`:此存储的ContextHub.Utils.Persistence对象。 默认情况下，会使用内存持久性（Javascript对象）。
   * `service`: (对象)
      * `host`:（字符串）服务器名称或IP地址。
      * `jsonp`:（布尔值）值为true表示该服务是JSONP服务，否则为false。 如果为true，则 `{callback: "ContextHub.Callbacks.*Object.name*}`对象添加到 `service.params`.
      * `params`:（对象）表示为对象属性的URL参数。 参数名称和值分别是对象属性名称和值。
      * `path`:（字符串）服务的路径。
      * `port`:（数字）服务的端口号。
      * `secure`:（字符串或布尔值）确定用于服务URL的协议：
         * `auto`://
         * `true`:https://
         * `false`:http://
      * `timeout`:（数字）等待JSONP服务在超时前做出响应的时间（以毫秒为单位）。
         * `ttl`:在对JSONP服务的调用之间传递的最小时间（以毫秒为单位）。 (请参阅 [queryService](#queryservice-reload) 函数)。

#### queryService(reload) {#queryservice-reload}

查询远程JSONP服务并缓存响应。 如果自上次调用此函数以来经过的时间小于的值 `config.service.ttl`，则不会调用服务并且不会更改缓存的响应。 或者，您也可以强制调用服务。 的 `config.service.ttl`属性 [init](#init-name-config) 函数来初始化存储。

查询完成后会触发就绪事件。 如果未设置JSONP服务URL，则函数不执行任何操作。

##### 参数 {#parameters-queryservice}

* **`reload`:** （布尔值）值为true将删除缓存响应并强制调用JSONP服务。

#### 重置 {#reset}

重置存储保留数据的初始值，然后调用JSONP服务。 或者，您也可以从存储中删除所有其他数据。 重置初始值时，会暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的initialValues属性中提供。

##### 参数 {#parameters-reset-1}

* **`keepRemainingData`:** （布尔值）如果值为true，则会保留非初始数据。 如果值为false，则会删除除初始值之外的所有数据。

#### resolveParameter(f) {#resolveparameter-f}

解析给定参数。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` 扩展 [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) 所以它继承了该类的所有功能。 但是，从JSONP服务检索的数据将根据ContextHub持久性的配置进行保留。 (请参阅 [持久性模式：](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` 扩展 [ContextHub.Store.Core](#contexthub-store-core) 所以它继承了该类的所有功能。 此存储中的数据将根据ContextHub持久性的配置进行保留。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` 扩展 [ContextHub.Store.Core](#contexthub-store-core) 所以它继承了该类的所有功能。 此存储中的数据将使用内存中持久性（Javascript对象）进行保留。

## ContextHub.UI {#contexthub-ui}

管理UI模块和UI模块渲染器。

### 函数(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType， renderer， dontRender) {#registerrenderer-moduletype-renderer-dontrender}

使用ContextHub注册UI模块渲染器。 注册渲染器后，可以使用 [创建UI模块](configuring-contexthub.md#adding-a-ui-module). 当您 [扩展 `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) 创建自定义UI模块渲染器。

##### 参数 {#parameters-registerrenderer}

* **`moduleType`:** （字符串）UI模块渲染器的标识符。 如果已使用指定的值注册了渲染器，则在注册此渲染器之前会取消注册现有渲染器。
* **`renderer`:** （字符串）呈现UI模块的类的名称。
* **`dontRender`:** （布尔值）设置为 `true` ，以防止在注册渲染器后渲染ContextHub UI。 默认值为 `false`。

##### 示例 {#example-registerrenderer}

以下示例将一个渲染器注册为 `contexthub.browserinfo` 模块类型。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

用于与Cookie交互的实用程序类。

### 函数(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

确定是否存在Cookie。

##### 参数 {#parameters-exists}

* **`key`:** A `String` ，其中包含要测试的Cookie的键。

##### 返回结果 {#returns-exists}

A `boolean` 值为true表示Cookie存在。

##### 示例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

返回具有与过滤器匹配的键的所有Cookie。

##### 参数 {#parameters-getallitems}

* **`filter`:** （可选）匹配Cookie键的条件。 要返回所有Cookie，请指定无值。 支持以下类型：
   * 字符串：字符串会与Cookie键值进行比较。
   * 阵列：数组中的每个项目都是一个过滤器。
   * 正则表达式对象：对象的测试函数用于匹配Cookie键。
   * 函数：用于测试Cookie键是否匹配的函数。 如果测试确认匹配，则函数必须将Cookie键作为参数并返回true。

##### 返回结果 {#returns-getallitems}

Cookie的对象。 对象属性是Cookie键，键值是Cookie值。

##### 示例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

返回Cookie值。

##### 参数 {#parameters-getitem-1}

* **`key`:** 您想要其值的Cookie的键。

##### 返回结果 {#returns-getitem-1}

Cookie值，或 `null` 如果找不到密钥的cookie。

##### 示例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

返回与过滤器匹配的现有Cookie的键数组。

##### 参数 {#parameters-getkeys-1}

* **`filter`:** 匹配Cookie键的条件。 支持以下类型：
   * 字符串：字符串会与Cookie键值进行比较。
   * 阵列：数组中的每个项目都是一个过滤器。
   * 正则表达式对象：对象的测试函数用于匹配Cookie键。
   * 函数：用于测试Cookie键是否匹配的函数。 函数必须将Cookie键作为参数并返回 `true` 测试是否确认匹配。

##### 返回结果 {#returns-getkeys-1}

一个字符串数组，其中每个字符串是与过滤器匹配的Cookie的键。

##### 示例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key， options) {#removeitem-key-options-1}

删除Cookie。 要删除Cookie，该值将设置为空字符串，到期日期将设置为当前日期前一天。

##### 参数 {#parameters-removeitem-1}

* **`key`:** A `String` 表示要删除的Cookie键的值。
* **`options`:** 一个对象，其中包含用于配置Cookie属性的属性值。 请参阅 [`setItem`](#setitem-key-value-options) 函数。 的 `expires` 属性不起作用。

##### 返回结果 {#returns-removeitem-1}

此函数不返回值。

##### 示例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key， value， options) {#setitem-key-value-options-1}

创建给定键值的Cookie，并将该Cookie添加到当前文档。 或者，您也可以指定用于配置Cookie属性的选项。

##### 参数 {#parameters-setitem-1}

* **`key`:** 包含Cookie键的字符串。
* **`value`:** 包含Cookie值的字符串。
* **`options`:** （可选）一个对象，其中包含配置Cookie属性的以下任意属性：
   * `expires`:A `date` 或 `number` 指定Cookie何时过期的值。 日期值指定到期的绝对时间。 数字（以天为单位）会将到期时间设置为当前时间加上数字。 默认值为 `undefined`。
   * `secure`:A `boolean` 指定 `Secure` 属性。 默认值为 `false`。
   * `path`:A `String` 值 `Path` 属性。 默认值为 `undefined`。

##### 返回结果 {#returns-setitem-1}

具有设置值的Cookie。

##### 示例 {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 消失（过滤器，选项） {#vanish-filter-options}

删除与给定过滤器匹配的所有Cookie。 Cookie与 `getKeys` 函数并使用 `removeItem` 函数。

##### 参数 {#parameters-vanish}

* **`filter`:** 的 `filter` 要在对的调用中使用的参数 [`getKeys`](#getkeys-filter) 函数。
* **`options`:** 的 `options` 要在对的调用中使用的参数 [`removeItem`](#removeitem-key-options) 函数。

##### 返回结果 {#returns-vanish}

此函数不返回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

允许您将函数绑定和取消绑定到ContextHub存储事件。 访问 `ContextHub.Utils.Eventing` 使用 [事件](#eventing) 存储的属性。

### 函数(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name， selector) {#off-name-selector}

从事件中取消绑定函数。

##### 参数 {#parameters-off}

* **`name`:** 的 [事件的名称](#contexthub-utils-eventing) 解除函数绑定。
* **`selector`:** 标识绑定的选择器。 (请参阅 `selector` 参数 [`on`](#on-name-handler-selector-triggerforpastevents) 和 [`once`](#once-name-handler-selector-triggerforpastevents) 函数)。

##### 返回结果 {#returns-off}

此函数不返回任何值。

#### on(name， handler， selector， triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 每次发生事件时都会调用函数。 或者，也可以在建立绑定之前，为过去发生的事件调用函数。

##### 参数 {#parameters-on}

* **`name`:** （字符串） [事件的名称](#contexthub-utils-eventing) 将函数绑定到的。
* **`handler`:** （函数）要绑定到事件的函数。
* **`selector`:** （字符串）绑定的唯一标识符。 如果要使用 `off` 函数来删除绑定。
* **`triggerForPastEvents`:** （布尔值）指示是否应为过去发生的事件执行处理程序。 值 `true` 为过去的事件调用处理程序。 值 `false` 为将来的事件调用处理程序。 默认值为 `true`。

##### 返回结果 {#returns-on}

当 `triggerForPastEvents` 参数 `true`，此函数返回 `boolean` 用于指示事件是否发生在过去的值：

* `true`:事件在过去发生，将调用处理程序。
* `false`:以前未发生过该事件。

如果 `triggerForPastEvents` is `false`，则此函数不返回任何值。

##### 示例 {#example-on}

以下示例将函数绑定到地理位置存储的数据事件。 函数会使用商店中纬度数据项的值填充页面上的元素。

```html
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

将函数绑定到事件。 对于事件的首次出现，函数只调用一次。 或者，也可以在建立绑定之前，为过去发生的事件调用函数。

##### 参数 {#parameters-once}

* **`name`:** （字符串） [事件的名称](#contexthub-utils-eventing) 将函数绑定到的。
* **`handler`:** （函数）要绑定到事件的函数。
* **`selector`:** （字符串）绑定的唯一标识符。 如果要使用 `off` 函数来删除绑定。
* **`triggerForPastEvents`:** （布尔值）指示是否应为过去发生的事件执行处理程序。 值 `true` 为过去的事件调用处理程序。 值 `false` 为将来的事件调用处理程序。 默认值为 `true`。

##### 返回结果 {#returns-once}

当 `triggerForPastEvents` 参数 `true`，此函数返回 `boolean` 用于指示事件是否发生在过去的值：

* `true`:事件在过去发生，将调用处理程序。
* `false`:以前未发生过该事件。

如果 `triggerForPastEvents` is `false`，则此函数不返回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

允许对象继承另一个对象的属性和方法的实用程序类。

### 函数(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child， parent) {#inherit-child-parent}

导致对象继承另一个对象的属性和方法。

##### 参数 {#parameters-inherit}

* **`child`:** （对象）继承的对象。
* **`parent`:** （对象）用于定义继承的属性和方法的对象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供了用于将对象序列化为JSON格式并将JSON字符串反序列化为对象的函数。

### 函数(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

将字符串值解析为JSON，并将其转换为Javascript对象。

##### 参数 {#parameters-parse}

* **`data`:** JSON格式的字符串值。

##### 返回结果 {#returns-parse}

Javascript对象。

##### 示例 {#example-parse}

代码：

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

返回以下对象：

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

将Javascript值和对象序列化为JSON格式的字符串值。

##### 参数 {#parameters-stringify}

* **`data`:** 要序列化的值或对象。 此函数支持布尔值、数组值、数字值、字符串值和日期值。

##### 返回结果 {#returns-stringify}

序列化的字符串值。 When `data` 是R `egExp` 值时，此函数返回空对象。 When `data` 是函数，返回 `undefined`.

##### 示例 {#example-stringify}

以下代码：

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

返回：

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此类便于处理要存储或从ContextHub存储中检索的数据对象。

### 函数(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

创建数据对象的副本，并从第二个对象向其添加数据树。 该函数返回副本，且不会修改任何原始对象。 当两个对象的数据树包含相同的键时，第二对象的值将覆盖第一对象的值。

##### 参数 {#parameters-addallitems-1}

* **`tree`:** 复制的对象。
* **`secondTree`:** 与 `tree` 对象。

##### 返回结果 {#returns-addallitems-1}

包含合并数据的对象。

#### cleanup() {#cleanup}

创建对象的副本，查找并删除数据树中不包含值、空值或未定义值的项，然后返回该副本。

##### 参数 {#parameters-cleanup}

* **`tree`:** 要清理的对象。

##### 返回结果 {#returns-cleanup}

已清理的树副本。

#### getItem() {#getitem}

从键的对象中检索值。

##### 参数 {#parameters-getitem-2}

* **`tree`:** 数据对象。
* **`key`:** 要检索的值的键。

##### 返回结果 {#returns-getitem-2}

与键对应的值。 当键具有子键时，此函数将返回一个复杂的对象。 当键值的类型为 `undefined`, `null` 的次数。

##### 示例 {#example-getitem-2}

请考虑以下Javascript对象：

```javascript
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

以下示例代码会返回值 `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

以下示例代码可检索具有子项的键的值：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

该函数返回以下对象：

```javascript
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

从对象的数据树中检索所有键。 或者，您只能检索特定键子项的键。 您还可以选择指定检索到键值的排序顺序。

##### 参数 {#parameters-getkeys-2}

* **`tree`:** 要从中检索数据树键的对象。
* **`parent`:** （可选）要检索子项目键的数据树中项目的键。
* **`order`:** （可选）确定返回键的排序顺序的函数。 (请参阅 [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 在Mozilla开发人员网络上)。

##### 返回结果 {#returns-getkeys-2}

一组键。

##### 示例 {#example-getkeys-2}

请考虑以下对象：

```javascript
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

的 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 脚本返回以下数组：

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

创建给定对象的副本，从数据树中删除指定的分支，并返回修改后的副本。

##### 参数 {#parameters-removeitem-2}

* **`tree`:** 数据对象。
* **`key`:** 要删除的键。

##### 返回结果 {#returns-removeitem-2}

删除了键的原始数据对象的副本。

##### 示例 {#example-removeitem-2}

请考虑以下对象：

```javascript
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

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

该函数返回以下对象：

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitingKey(key) {#sanitizekey-key}

整理字符串值以使其可用作键。 要整理字符串，此函数将执行以下操作：

* 将多个连续正斜杠减少为一个斜杠。
* 从字符串的开头和结尾删除空格。
* 将结果拆分为用斜杠标定的字符串数组。

使用生成的数组创建可用键。

##### 参数 {#parameters-sanitizekey}

* **`key`:** 的 `string` 整理。

##### 返回结果 {#returns-sanitizekey}

数组 `string` 其中，每个字符串是 `key` 是用斜杠划定的。 表示已清理的键值。 如果清理后的数组的长度为零，则此函数将返回 `null`.

##### 示例 {#example-sanitizekey}

以下代码会清理字符串以生成数组 `["this", "is", "a", "path"]`，然后生成键值 `"/this/is/a/path"` 从数组：

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree， key， value) {#setitem-tree-key-value}

将键/值对添加到对象副本的数据树中。 有关数据树的信息，请参阅 [持久性。](contexthub.md#persistence)

##### 参数 {#parameters-setitem-2}

* **`tree`:** 数据对象。
* **`key`:** 要与您添加的值关联的键。 键值是数据树中项目的路径。 此函数调用 `ContextHub.Utils.JSON.tree.sanitize` 以在添加密钥之前对其进行整理。
* **`value`:** 要添加到数据树中的值。

##### 返回结果 {#returns-setitem-2}

副本 `tree` 包含的对象 `key`/ `value` 配对。

##### 示例 {#example-setitem-2}

请考虑以下Javascript代码：

```javascript
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

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

允许您注册存储候选项并获取注册的存储候选项。

### 函数(ContextHub.Utils.storeCapoints) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCanapits(storeType) {#getregisteredcandidates-storetype}

返回注册为商店候选项的商店类型。 检索特定存储类型或所有存储类型的注册候选项。

##### 参数 {#parameters-getregisteredcandidates}

* **`storeType`:** （字符串）存储类型的名称。 请参阅 `storeType` 参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 函数。

##### 返回结果 {#returns-getregisteredcandidates}

存储类型的对象。 对象属性是存储类型名称，属性值是已注册的存储候选项数组。

#### getStoreFromCapinates(storeType) {#getstorefromcandidates-storetype}

从已注册的候选项返回存储类型。 如果注册了多个同名的存储类型，则函数将返回具有最高优先级的存储类型。

##### 参数 {#parameters-getstorefromcandidates}

* `storeType`:（字符串）存储候选项的名称。 请参阅 `storeType` 参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) 函数。

##### 返回结果 {#returns-getstorefromcandidates}

表示注册的存储候选项的对象。 如果未注册请求的存储类型，则会引发错误。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回注册为存储候选项的存储类型的名称。 此函数不需要任何参数。

##### 返回结果 {#returns-getsupportedstoretypes}

字符串值的数组，其中每个字符串是在其中注册存储候选项的存储类型。 请参阅 `storeType` 参数 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 函数。

#### registerStoreCandidate(store， storeType， priority， applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名称和优先级将存储对象注册为存储候选项。

优先级是指示同名商店重要性的数字。 当使用与已注册的存储候选者相同的名称注册存储候选者时，使用具有较高优先级的候选者。 当注册存储候选时，仅当优先级高于同一命名的注册存储候选时，才注册存储。

##### 参数 {#parameters-registerstorecandidate}

* **`store`:** （对象）要注册为存储候选项的存储对象。
* **`storeType`:** （字符串）存储候选项的名称。 创建存储候选项的实例时需要此值。
* **`priority`:** （数字）商店候选项的优先级。
* **`applies`:** （函数）用于调用的函数，该函数可评估存储在当前环境中的适用性。 函数必须返回 `true` 如果商店适用， `false` 否则。 默认值为返回true的函数： `function() {return true;}`

##### 示例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
