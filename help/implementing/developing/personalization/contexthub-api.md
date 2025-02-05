---
title: ContextHub JavaScript API参考
description: 将ContextHub组件添加到页面后，脚本即可使用ContextHub JavaScript API
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '4602'
ht-degree: 2%

---

# ContextHub JavaScript API参考 {#contexthub-javascript-api-reference}

将[ContextHub组件添加到页面](adding-contexthub.md)后，您的脚本即可使用ContextHub JavaScript API。

## contexthub常量 {#contexthub-constants}

ContextHub JavaScript API定义的常量值。

### 事件常量 {#event-constants}

下表列出了ContextHub存储区发生的names事件。 另请参阅[ContextHub.Utils.Eventing](#contexthub-utils-eventing)。

| 常量 | 描述 | 价值 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub的事件命名空间 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 指示所有必需的存储已注册、初始化并准备使用 | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 指示在给定的超时时间内并非所有存储都已初始化 | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | 在注册存储时触发 | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | 指示存储已准备就绪。 它在注册后立即触发，但JSONP存储除外，它在获取数据时触发)。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | 在存储更新其持久性时触发 | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 持久性容器名称 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 存储原始JSON结果的特定持久性键名称 | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | 存储指示何时获取JSON数据的特定时间戳 | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 存储上次调用期间使用的JSON服务的特定URL | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | 指示ContextHub的UI是否展开 | `/_/container-expanded` |

### UI事件常量 {#ui-event-constants}

下表列出了ContextHub UI中发生的事件名称。

| **常量** | **描述** | **值** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | 在注册模式时触发 | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | 在模式取消注册时触发 | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | 在注册模式渲染器时触发 | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | 在取消注册模式渲染器时触发 | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 在添加新模式时触发 | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | 在删除模式时触发 | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | 在用户选择模式时触发 | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 注册新模块时触发 | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | 在模块取消注册时触发 | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | 在注册模块渲染器时触发 | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | 在模块渲染器取消注册时触发 | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 在添加新模块时触发 | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | 删除模块时触发 | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | 在将UI容器添加到页面时触发 | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | 在ContextHub UI打开时触发 | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | 在ContextHub UI折叠时触发 | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | 在修改属性时触发 | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | 每次呈现ContextHub UI时触发（例如，在属性更改后） | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | 在UI容器初始化时触发 | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | 指示活动的UI模式 | `/_/active-ui-mode` |

## ContextHub JavaScript API参考 {#contexthub-javascript-api-reference-2}

ContextHub对象提供对所有存储的访问权限。

### 函数(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

返回所有已注册的ContextHub存储。

此函数没有参数。

##### 返回 {#returns-}

包含所有ContextHub存储的对象。 每个存储都是一个使用与该存储相同的名称的对象。

##### 示例 {#example-}

以下示例检索所有存储，然后检索地理位置存储：

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

将存储检索为JavaScript对象。

##### 参数 {#parameters-}

* **`name`：**&#x200B;存储所注册的名称。

##### 返回 {#returns-getstore-name}

表示存储的对象。

##### 示例 {#example-getstore-name}

以下示例检索地理位置存储：

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

表示ContextHub区段。 使用`ContextHub.SegmentEngine.SegmentManager`获取区段。

### 函数(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

将区段的名称作为字符串值返回。

#### getPath() {#getpath}

以字符串值的形式返回区段定义的存储库路径。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供对ContextHub区段的访问权限。

### 函数(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

返回在当前上下文中解析的段。 此函数没有参数。

##### 返回 {#returns-getresolvedsegments}

`ContextHub.SegmentEngine.Segment`对象的数组。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存储的基类。

### 属性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

[`ContextHub.Utils.Eventing`](#contexthub-utils-eventing)对象。 使用此对象绑定函数以存储事件。 有关默认值和初始化的信息，请参阅[`init(name,config)`](#init-name-config)。

#### name {#name}

商店的名称。

#### persistence {#persistence}

`ContextHub.Utils.Persistence`对象。 有关默认值和初始化的信息，请参阅[`init(name,config)`](#init-name-config)。

### 函数(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree， options) {#addallitems-tree-options}

将数据对象或数组与存储数据合并。 对象或数组中的每个键/值对都将添加到存储中（通过`setItem`函数）：

* **对象：**&#x200B;键是属性名称。
* **数组：**&#x200B;键是数组索引。

值可以是对象。

##### 参数 {#parameters-addallitems}

* **`tree`：** （对象或数组）要添加到存储的数据。
* **`options`：** （对象）传递给setItem函数的选项的可选对象。 有关信息，请参阅[`setItem(key,value,options)`](#setitem-key-value-options)的`options`参数。

##### 返回 {#returns-addallitems}

`boolean`值：

* 值为`true`表示存储了数据对象。
* 值为`false`表示数据存储未更改。

#### addReference(key， anotherKey) {#addreference-key-anotherkey}

创建从一个键到另一个键的引用。 键不能引用自身。

##### 参数 {#parameters-addreference}

* **`key`：**&#x200B;引用`anotherKey`的键。

* **`anotherkey`：**&#x200B;它们由`key`引用的键。

##### 返回 {#returns-addreference}

`boolean`值：

* 值为`true`表示已添加引用。
* 值为`false`表示未添加引用。

#### announceReadiness() {#announcereadiness}

触发此存储的`ready`事件。 此函数没有参数并且不返回任何值。

#### clean() {#clean}

从存储中删除所有数据。 该函数没有参数并且没有返回值。

#### getItem(key) {#getitem-key}

返回与键关联的值。

##### 参数 {#parameters-getitem}

* **`key`：** （字符串）要返回值的键。

##### 返回 {#returns-getitem}

表示键值的对象。

#### getKeys(includeInternals) {#getkeys-includeinternals}

从存储中检索密钥。 （可选）您可以检索ContextHub框架内部使用的键。

##### 参数 {#parameters-getkeys}

* **`includeInternals`：**&#x200B;值`true`在结果中包含内部使用的键。 这些键以下划线(`_`)字符开头。 默认值为 `false`。

##### 返回 {#returns-getkeys}

键名称的数组（`string`值）。

#### getReferences() {#getreferences}

从存储中检索引用。

##### 返回 {#returns-getreferences}

一个数组，使用引用键作为引用键的索引：

* 引用键与`addReference`函数的`key`参数相对应。
* 引用的键对应于`addReference`函数的`anotherKey`参数。

#### getTree(includeInternals) {#gettree-includeinternals}

从存储中检索数据树。 或者，您也可以包含由ContextHub框架在内部使用的键/值对。

##### 参数 {#parameters-gettree}

* `includeInternals:`值`true`在结果中包含内部使用的键/值对。 此数据的键以下划线(`_`)字符开头。 默认值为 `false`。

##### 返回 {#returns-gettree}

表示数据树的对象。 键是对象的属性名称。

#### init(name， config) {#init-name-config}

初始化存储。

* 将存储数据设置为空对象。
* 设置对空对象的存储引用。
* `eventChannel`是`data:<name>`，其中`<name>`是存储名称。
* `storeDataKey`是`/store/<name>`，其中`<name>`是存储名称。

##### 参数 {#parameters-init}

* **`name`：**&#x200B;存储的名称。
* **`config`：**&#x200B;包含配置属性的对象：
   * `eventDeferring`：默认值为32。
   * `eventing`：此存储的[ContextHub.Utils.Eventing](#contexthub-utils-eventing)对象。 默认值是`ContextHub.eventing`对象使用的值。
   * `persistence`：此存储的`ContextHub.Utils.Persistence`对象。 默认值是`ContextHub.persistence`对象。

#### isEventingPaused() {#iseventingpaused}

确定是否暂停此存储的事件。

##### 返回 {#returns-iseventingpaused}

布尔值：

* `true`：事件已暂停，因此不会为此存储触发任何事件。
* `false`：事件未暂停，因此触发了此存储的事件。

#### pauseEventing() {#pauseeventing}

暂停存储的事件，以便不触发任何事件。 此函数不需要任何参数，也不返回任何值。

#### removeItem(key， options) {#removeitem-key-options}

从存储中删除键/值对。

删除键时，函数将触发`data`事件。 事件数据包括存储名称、已删除键的名称、已删除的值、键的新值(null)以及“删除”的操作类型。

或者，您可以阻止触发`data`事件。

##### 参数 {#parameters-removeitem}

* **`key`：** （字符串）要删除的键的名称。
* **`options`：** （对象）选项的对象。 以下对象属性有效：
   * 静默：值`true`阻止触发`data`事件。 默认值为 `false`。

##### 返回 {#returns-removeitem}

`boolean`值：

* 值`true`表示已删除键/值对。
* 值为`false`表示数据存储未更改，因为在存储中未找到键。

#### removeReference(key) {#removereference-key}

从存储中删除引用。

##### 参数 {#parameters-removereference}

* **`key`：**&#x200B;要删除的键引用。 此参数对应于`addReference`函数的`key`参数。

##### 返回 {#returns-removereference}

`boolean`值：

* 值为`true`表示引用已删除。
* 值为`false`表示密钥无效，存储未更改。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重置存储保留数据的初始值。 或者，您也可以从存储中删除所有其他数据。 重置存储时暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的`initialValues`属性中提供。

##### 参数 {#parameters-reset}

* **`keepRemainingData`**： （布尔值）值为true会导致保留非初始数据。 如果值为false，则会删除初始值以外的所有数据。

#### resolveReference(key， retry) {#resolvereference-key-retry}

检索引用的键。 或者，您可以指定用于解析最佳匹配的迭代次数。

##### 参数 {#parameters-resolvereference}

* **`key`：** （字符串）要为其解析引用的键。 此`key`参数对应于`addReference`函数的`key`参数。
* **`retry`：** （数字）要使用的迭代次数。

##### 返回 {#returns-resolvereference}

表示引用的键的`string`值。 如果未解析任何引用，则返回`key`参数的值。

#### resumeEventing() {#resumeeventing}

恢复此存储的事件，以便触发事件。 此函数不定义任何参数也不返回任何值。

#### setItem(key， value， options) {#setitem-key-value-options}

向存储中添加键/值对。

仅当键的值不同于当前为键存储的值时，才会触发`data`事件。 您可以选择阻止触发`data`事件。

事件数据包括`set`的存储名称、键、上一个值、新值和操作类型。

##### 参数 {#parameters-setitem}

* **`key`：** （字符串）键的名称。
* **`options`：** （对象）选项的对象。 以下对象属性有效：
   * `silent`： `true`值阻止触发`data`事件。 默认值为 `false`。
* **`value`：** （对象）要与键关联的值。

##### 返回 {#returns-setitem}

`boolean`值：

* 值为`true`表示存储了数据对象。
* 值为`false`表示数据存储未更改。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON数据的存储。 数据从外部JSONP服务或选择性地从返回JSON数据的服务中检索。 创建此类的实例时，使用[`init`](#init-name-config)函数指定服务详细信息。

存储使用内存中持久性(JavaScript变量)。 存储数据仅在页面的生命周期内可用。

ContextHub.Store.JSONPStore扩展[ContextHub.Store.Core](#contexthub-store-core)并继承该类的函数。

### 函数(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig， override) {#configureservice-serviceconfig-override}

配置用于连接到此对象使用的JSONP服务的详细信息。 您可以更新或替换现有配置。 函数不返回任何值。

##### 参数 {#parameters-configureservice}

* **`serviceConfig`：**&#x200B;包含以下属性的对象：
   * `host`： （字符串）服务器名称或IP地址。
   * `jsonp`： （布尔值）值为true表示服务是JSONP服务，否则为false。 如果为true，则{callback： &quot;ContextHub.Callbacks.*Object.name*}对象已添加到service.params对象。
   * `params`： （对象） URL参数表示为对象属性。 参数名是属性名，参数值是属性值。
   * `path`： （字符串）服务的路径。
   * `port`： (Number)服务的端口号。
   * `secure`： （字符串或布尔值）确定用于服务URL的协议：
      * `auto`： //
      * `true`： https://
      * `false`： http://
* **覆盖：** （布尔值）。 值为`true`会导致现有服务配置被替换为`serviceConfig`的属性。 值为`false`会导致现有服务配置属性与`serviceConfig`的属性合并。

#### getRawResponse() {#getrawresponse}

返回自上次调用JSONP服务以来缓存的原始响应。 函数不需要参数。

##### 返回 {#returns-getrawresponse}

表示原始响应的对象。

#### getServiceDetails() {#getservicedetails}

检索此ContextHub.Store.JSONPStore对象的服务对象。 服务对象包含创建服务URL所需的信息。

##### 返回 {#returns-getservicedetails}

具有以下属性的对象：

* **`host`：** （字符串）服务器名称或IP地址。
* **`jsonp`：** （布尔值）值为true表示该服务是JSONP服务，否则为false。 如果为true，则{callback： &quot;ContextHub.Callbacks.*Object.name*}对象已添加到service.params对象。
* **`params`：** （对象）URL参数表示为对象属性。 参数名是属性名，参数值是属性值。
* **`path`：** （字符串）服务的路径。
* **`port`：** （编号）服务的端口号。
* **`secure`：** （字符串或布尔值）确定用于服务URL的协议：
   * `auto`： //
   * `true`： https://
   * `false`： http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

检索JSONP服务的URL。

##### 参数 {#parameters-getserviceurl}

* **`resolve`：** （布尔值）确定是否在URL中包含已解析的参数。 值为`true`可解析参数，而`false`则不解析。

##### 返回 {#returns-getserviceurl}

表示服务URL的`string`值。

#### init(name， config) {#init-name-config-1}

初始化`ContextHub.Store.JSONPStore`对象。

##### 参数 {#parameters-init-1}

* **`name`：** （字符串）存储的名称。
* **`config`：** （对象）包含服务属性的对象。 JSONPStore对象使用`service`对象的属性来构建JSONP服务的URL：
   * `eventDeferring`： 32。
   * `eventing`：此存储的ContextHub.Utils.Eventing对象。 默认值是`ContextHub.eventing`对象。
   * `persistence`：此存储的ContextHub.Utils.Persistence对象。 默认情况下，使用内存持久性(JavaScript对象)。
   * `service`： （对象）
      * `host`： （字符串）服务器名称或IP地址。
      * `jsonp`： （布尔值）值为true表示服务是JSONP服务，否则为false。 为true时，`{callback: "ContextHub.Callbacks.*Object.name*}`对象将添加到`service.params`。
      * `params`： （对象） URL参数表示为对象属性。 参数名称和值分别是对象属性名称和值。
      * `path`： （字符串）服务的路径。
      * `port`： (Number)服务的端口号。
      * `secure`： （字符串或布尔值）确定用于服务URL的协议：
         * `auto`： //
         * `true`： https://
         * `false`： http://
      * `timeout`： （数字）超时前等待JSONP服务响应的时间（以毫秒为单位）。
         * `ttl`：调用JSONP服务之间的最小时间量（以毫秒为单位）。 （请参阅[queryService](#queryservice-reload)函数）。

#### queryService（重新加载） {#queryservice-reload}

查询远程JSONP服务并缓存响应。 如果自上次调用此函数以来的时间小于`config.service.ttl`的值，则不会调用服务，也不会更改缓存的响应。 或者，您可以强制调用该服务。 在调用[init](#init-name-config)函数初始化存储区时设置了`config.service.ttl`属性。

查询完成后，触发就绪事件。 如果未设置JSONP服务URL，则函数将不执行任何操作。

##### 参数 {#parameters-queryservice}

* **`reload`：** （布尔值）值为true会删除缓存的响应并强制调用JSONP服务。

#### 重置 {#reset}

重置存储区保留数据的初始值，然后调用JSONP服务。 或者，您也可以从存储中删除所有其他数据。 重置初始值时，将暂停此存储的事件。 此函数不返回任何值。

初始值在用于实例化存储对象的配置对象的initialValues属性中提供。

##### 参数 {#parameters-reset-1}

* **`keepRemainingData`：** （布尔值）值为true会导致保留非初始数据。 如果值为false，则会删除初始值以外的所有数据。

#### resolveParameter(f) {#resolveparameter-f}

解析给定的参数。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore`扩展[ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore)，以便继承该类的所有函数。 但是，根据ContextHub持久性的配置，将保留从JSONP服务检索的数据。 （请参阅[持久性模式](adding-contexthub.md#persistence-modes)）

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore`扩展[ContextHub.Store.Core](#contexthub-store-core)，以便继承该类的所有函数。 此存储中的数据将根据ContextHub持久性的配置进行保留。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore`扩展[ContextHub.Store.Core](#contexthub-store-core)，以便继承该类的所有函数。 使用内存中持久性(JavaScript对象)保留此存储中的数据。

## ContextHub.UI {#contexthub-ui}

管理UI模块和UI模块渲染器。

### 函数(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType， renderer， dontRender) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub注册UI模块渲染器。 在注册渲染器后，它可用于[创建UI模块](configuring-contexthub.md#adding-a-ui-module)。 当您[扩展`ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types)以创建自定义UI模块渲染器时，使用此函数。

##### 参数 {#parameters-registerrenderer}

* **`moduleType`：** （字符串） UI模块渲染器的标识符。 如果已经使用指定的值注册了渲染器，则在注册此渲染器之前将取消注册现有渲染器。
* **`renderer`：** （字符串）呈现UI模块的类的名称。
* **`dontRender`：**（布尔值）设置为`true`以防止在注册渲染器后渲染ContextHub UI。 默认值为 `false`。

##### 示例 {#example-registerrenderer}

以下示例将渲染器注册为`contexthub.browserinfo`模块类型。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

用于与Cookie交互的实用程序类。

### 函数(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### 存在（键） {#exists-key}

确定Cookie是否存在。

##### 参数 {#parameters-exists}

* **`key`：**&#x200B;包含要测试的Cookie键的`String`。

##### 返回 {#returns-exists}

值为true的`boolean`表示Cookie存在。

##### 示例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

返回其键与过滤器匹配的所有Cookie。

##### 参数 {#parameters-getallitems}

* **`filter`：**（可选）匹配Cookie密钥的条件。 要返回所有Cookie，请不要指定任何值。 支持以下类型：
   * 字符串：将字符串与Cookie键进行比较。
   * 数组：数组中的每一项都是一个过滤器。
   * RegExp对象：对象的测试函数用于匹配Cookie键。
   * 函数：测试Cookie键以查找匹配项的函数。 该函数必须将Cookie密钥作为参数，如果测试确认匹配，则返回true。

##### 返回 {#returns-getallitems}

Cookie的对象。 对象属性是Cookie键，键值是Cookie值。

##### 示例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

返回Cookie值。

##### 参数 {#parameters-getitem-1}

* **`key`：**&#x200B;您希望求值的Cookie的键。

##### 返回 {#returns-getitem-1}

Cookie值，或未找到键的Cookie时的`null`。

##### 示例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

返回与过滤器匹配的现有Cookie键的数组。

##### 参数 {#parameters-getkeys-1}

* **`filter`：**&#x200B;匹配Cookie密钥的条件。 支持以下类型：
   * 字符串：将字符串与Cookie键进行比较。
   * 数组：数组中的每一项都是一个过滤器。
   * RegExp对象：对象的测试函数用于匹配Cookie键。
   * 函数：测试Cookie键以查找匹配项的函数。 函数必须将Cookie密钥作为参数，如果测试确认匹配，则返回`true`。

##### 返回 {#returns-getkeys-1}

一个字符串数组，其中每个字符串是与过滤器匹配的Cookie的键。

##### 示例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key， options) {#removeitem-key-options-1}

删除Cookie。 要删除Cookie，该值将设置为空字符串，并且到期日期将设置为当前日期之前的日期。

##### 参数 {#parameters-removeitem-1}

* **`key`：**&#x200B;表示要删除的Cookie键的`String`值。
* **`options`：**&#x200B;包含用于配置Cookie属性的属性值的对象。 有关信息，请参阅[`setItem`](#setitem-key-value-options)函数。 `expires`属性无效。

##### 返回 {#returns-removeitem-1}

此函数不返回值。

##### 示例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key， value， options) {#setitem-key-value-options-1}

创建给定键和值的Cookie，并将Cookie添加到当前文档。 （可选）您可以指定用于配置Cookie属性的选项。

##### 参数 {#parameters-setitem-1}

* **`key`：**&#x200B;包含Cookie键的字符串。
* **`value`：**&#x200B;包含Cookie值的字符串。
* **`options`：**（可选）一个对象，它包含以下任何配置Cookie属性的属性：
   * `expires`：指定Cookie过期时间的`date`或`number`值。 日期值指定绝对到期时间。 一个数字（以天为单位）将过期时间设置为当前时间加上数字。 默认值为 `undefined`。
   * `secure`：指定Cookie的`Secure`特性的`boolean`值。 默认值为 `false`。
   * `path`：要用作Cookie的`Path`特性的`String`值。 默认值为 `undefined`。

##### 返回 {#returns-setitem-1}

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

删除与给定过滤器匹配的所有Cookie。 Cookie使用`getKeys`函数匹配，并使用`removeItem`函数删除。

##### 参数 {#parameters-vanish}

* **`filter`：**&#x200B;要用于调用[`getKeys`](#getkeys-filter)函数的`filter`参数。
* **`options`：**&#x200B;要用于调用[`removeItem`](#removeitem-key-options)函数的`options`参数。

##### 返回 {#returns-vanish}

此函数不返回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

允许您将函数绑定和取消绑定到ContextHub存储事件。 使用存储的[eventing](#eventing)属性访问存储的`ContextHub.Utils.Eventing`对象。

### 函数(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name， selector) {#off-name-selector}

从事件中取消绑定函数。

##### 参数 {#parameters-off}

* **`name`：**&#x200B;要取消绑定函数的事件](#contexthub-utils-eventing)的[名称。
* **`selector`：**&#x200B;标识绑定的选择器。 （请参阅[`on`](#on-name-handler-selector-triggerforpastevents)和[`once`](#once-name-handler-selector-triggerforpastevents)函数的`selector`参数）。

##### 返回 {#returns-off}

此函数不返回任何值。

#### on(name， handler， selector， triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

将函数绑定到事件。 每次事件发生时都会调用函数。 或者，可以为过去发生的事件（在建立绑定之前）调用函数。

##### 参数 {#parameters-on}

* **`name`：** （字符串）要绑定函数的事件](#contexthub-utils-eventing)的[名称。
* **`handler`：** （函数）要绑定到事件的函数。
* **`selector`：** （字符串）绑定的唯一标识符。 如果要使用`off`函数移除绑定，则需要选择器识别绑定。
* **`triggerForPastEvents`：** （布尔值）指示是否应为过去发生的事件执行处理程序。 值为`true`会调用过去事件的处理程序。 值为`false`会调用未来事件的处理程序。 默认值为 `true`。

##### 返回 {#returns-on}

当`triggerForPastEvents`参数为`true`时，此函数返回一个`boolean`值，指示该事件是否在过去发生：

* `true`：该事件在过去发生过，因此调用了处理程序。
* `false`：该事件在过去未发生。

如果`triggerForPastEvents`为`false`，则此函数不返回任何值。

##### 示例 {#example-on}

以下示例将函数绑定到地理位置存储的数据事件。 函数会使用存储中的latitude数据项的值填充页面上的元素。

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

将函数绑定到事件。 函数只调用一次，以首次显示该事件。 或者，可以为过去发生的事件（在建立绑定之前）调用函数。

##### 参数 {#parameters-once}

* **`name`：** （字符串）要绑定函数的事件](#contexthub-utils-eventing)的[名称。
* **`handler`：** （函数）要绑定到事件的函数。
* **`selector`：** （字符串）绑定的唯一标识符。 如果要使用`off`函数移除绑定，则需要选择器识别绑定。
* **`triggerForPastEvents`：** （布尔值）指示是否应为过去发生的事件执行处理程序。 值为`true`会调用过去事件的处理程序。 值为`false`会调用未来事件的处理程序。 默认值为 `true`。

##### 返回 {#returns-once}

当`triggerForPastEvents`参数为`true`时，此函数返回一个`boolean`值，指示该事件是否在过去发生：

* `true`：该事件在过去发生过，因此调用了处理程序。
* `false`：该事件在过去未发生。

如果`triggerForPastEvents`为`false`，则此函数不返回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

一个实用程序类，它允许对象继承另一个对象的属性和方法。

### 函数(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child， parent) {#inherit-child-parent}

使一个对象继承另一个对象的属性和方法。

##### 参数 {#parameters-inherit}

* **`child`：** （对象）继承的对象。
* **`parent`：** （对象）定义继承的属性和方法的对象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供将对象序列化为JSON格式并将JSON字符串反序列化为对象的函数。

### 函数(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

将字符串值解析为JSON并将其转换为Javascript对象。

##### 参数 {#parameters-parse}

* **`data`：** JSON格式的字符串值。

##### 返回 {#returns-parse}

JavaScript对象。

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

#### strinify(data) {#stringify-data}

将JavaScript值和对象序列化为JSON格式的字符串值。

##### 参数 {#parameters-stringify}

* **`data`：**&#x200B;要序列化的值或对象。 此函数支持布尔值、数组、数字、字符串和日期值。

##### 返回 {#returns-stringify}

序列化的字符串值。 当`data`是R `egExp`值时，此函数返回空对象。 当`data`为函数时，返回`undefined`。

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

此类便于处理要存储的数据对象或从ContextHub存储中检索的数据对象。

### 函数(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

创建数据对象的副本，并将来自第二个对象的数据树添加到该副本。 该函数将返回副本，并且不会修改任何原始对象。 当两个对象的数据树包含相同的键时，第二对象的值覆盖第一对象的值。

##### 参数 {#parameters-addallitems-1}

* **`tree`：**&#x200B;复制的对象。
* **`secondTree`：**&#x200B;与`tree`对象的副本合并的对象。

##### 返回 {#returns-addallitems-1}

包含合并数据的对象。

#### cleanup() {#cleanup}

创建对象的副本，在数据树中查找和删除不包含值、空值或未定义的值的项，并返回副本。

##### 参数 {#parameters-cleanup}

* **`tree`：**&#x200B;要清理的对象。

##### 返回 {#returns-cleanup}

已清理的树的副本。

#### getItem() {#getitem}

从键的对象中检索值。

##### 参数 {#parameters-getitem-2}

* **`tree`：**&#x200B;数据对象。
* **`key`：**&#x200B;要检索的值的键。

##### 返回 {#returns-getitem-2}

与键对应的值。 当键具有子键时，此函数返回一个复杂的对象。 当键值的类型为`undefined`时，返回`null`。

##### 示例 {#example-getitem-2}

请考虑以下JavaScript对象：

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

以下示例代码返回值`260`：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

以下示例代码检索具有子键的键的值：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

此函数返回以下对象：

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

从对象的数据树中检索所有键。 或者，您只能检索特定键的子项键。 您还可以选择指定检索到的键的排序顺序。

##### 参数 {#parameters-getkeys-2}

* **`tree`：**&#x200B;从中检索数据树键的对象。
* **`parent`：**（可选）数据树中要检索其子项键的项的键。
* **`order`：**（可选）确定返回键的排序顺序的函数。 （请参阅Mozilla开发人员网络上的[`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)。）

##### 返回 {#returns-getkeys-2}

键数组。

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

`ContextHub.Utils.JSON.tree.getKeys(myObject);`脚本返回以下数组：

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

创建给定对象的副本，从数据树中删除指定分支，并返回修改后的副本。

##### 参数 {#parameters-removeitem-2}

* **`tree`：**&#x200B;数据对象。
* **`key`：**&#x200B;要删除的键。

##### 返回 {#returns-removeitem-2}

已删除键的原始数据对象的副本。

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

此函数返回以下对象：

```javascript
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

使用结果数组创建一个可用的键。

##### 参数 {#parameters-sanitizekey}

* **`key`：**&#x200B;要清理的`string`。

##### 返回 {#returns-sanitizekey}

`string`值的数组，其中每个字符串是`key`中用斜杠分隔的部分。 表示经过清理的密钥。 如果经过清理的数组的长度为零，则此函数返回`null`。

##### 示例 {#example-sanitizekey}

以下代码清理字符串以生成数组`["this", "is", "a", "path"]`，然后从数组生成键`"/this/is/a/path"`：

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree， key， value) {#setitem-tree-key-value}

将键/值对添加到对象副本的数据树中。 有关数据树的信息，请参阅[持久性](contexthub.md#persistence)。

##### 参数 {#parameters-setitem-2}

* **`tree`：**&#x200B;数据对象。
* **`key`：**&#x200B;要与您添加的值关联的键。 键值是数据树中项目的路径。 此函数调用`ContextHub.Utils.JSON.tree.sanitize`以在添加键之前对其进行清理。
* **`value`：**&#x200B;要添加到数据树的值。

##### 返回 {#returns-setitem-2}

包含`key`/`value`对的`tree`对象的副本。

##### 示例 {#example-setitem-2}

请考虑以下JavaScript代码：

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

使您能够注册候选商店和获取已注册的候选商店。

### 函数(ContextHub.Utils.storeCategors) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

返回注册为商店候选商店的存储类型。 检索特定存储类型或所有存储类型的已注册候选项。

##### 参数 {#parameters-getregisteredcandidates}

* **`storeType`：** （字符串）存储类型的名称。 查看[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)函数的`storeType`参数。

##### 返回 {#returns-getregisteredcandidates}

存储类型的对象。 对象属性是存储类型名称，属性值是已注册的存储候选数组。

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

从已注册的候选中返回存储类型。 如果注册了多个同名存储类型，此函数将返回具有最高优先级的存储类型。

##### 参数 {#parameters-getstorefromcandidates}

* `storeType`： （字符串）商店候选者的名称。 查看[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies)函数的`storeType`参数。

##### 返回 {#returns-getstorefromcandidates}

一个对象，表示已注册的存储候选。 如果未注册所请求的存储类型，则会引发错误。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回注册为存储候选的存储类型名称。 此函数不需要参数。

##### 返回 {#returns-getsupportedstoretypes}

一个字符串值数组，其中每个字符串是用来注册存储候选的存储类型。 查看[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)函数的`storeType`参数。

#### registerStoreCandidate(store， storeType， priority， applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名称和优先级将存储对象注册为存储候选项。

优先级是一个数字，它指示同名存储的重要性。 当使用与已注册的存储候选相同的名称注册存储候选时，使用具有较高优先级的候选。 在注册存储候选时，仅当优先级高于同名已注册的存储候选时才注册存储。

##### 参数 {#parameters-registerstorecandidate}

* **`store`：** （对象）要注册为存储候选的存储对象。
* **`storeType`：** （字符串）商店候选者的名称。 创建存储候选实例时需要此值。
* **`priority`：** （数字）商店候选的优先级。
* **`applies`：** （函数）要调用的函数，它评估存储在当前环境中的适用性。 如果存储适用，该函数必须返回`true`，否则必须返回`false`。 默认值是一个返回true的函数： `function() {return true;}`

##### 示例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
