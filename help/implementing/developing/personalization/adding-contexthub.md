---
title: 将ContextHub添加到页面和访问存储
description: 将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub Javascript库
exl-id: 8bfe2cff-3944-4e86-a95c-ebf1cb13913c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 将ContextHub添加到页面和访问存储 {#adding-contexthub-to-pages-and-accessing-stores}

将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub Javascript库。

ContextHub Javascript API提供对ContextHub管理的上下文数据的访问权限。 本页简要介绍了API用于访问和处理上下文数据的主要功能。 请查看API参考文档的链接，以查看详细信息和代码示例。

## 将ContextHub添加到页面组件 {#adding-contexthub-to-a-page-component}

要启用ContextHub功能并链接到ContextHub Javascript库，请包括 `contexthub` 组件 `head` 的子代码。 页面组件的HTL代码应类似于以下示例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

请注意，您还需要配置ContextHub工具栏是否显示在“预览”模式下。 请参阅 [显示和隐藏ContextHub UI](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui).

## 关于ContextHub存储 {#about-contexthub-stores}

使用ContextHub存储保留上下文数据。 ContextHub提供以下类型的存储，这些存储构成了所有存储类型的基础：

* [持久存储](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersiredJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存储类型都是 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 类。 有关创建新商店类型的信息，请参阅 [创建自定义商店](extending-contexthub.md#creating-custom-store-candidates). 有关示例存储类型的信息，请参阅 [ContextHub存储候选示例](sample-stores.md).

### 持久性模式 {#persistence-modes}

ContextHub存储使用以下持久模式之一：

* **本地：** 使用HTML5 localStorage保留数据。 本地存储会在各会话期间在浏览器上持久保留。
* **会话：** 使用HTML5 sessionStorage保留数据。 会话存储在浏览器会话期间会持续保留，并可用于所有浏览器窗口。
* **Cookie:** 使用浏览器对Cookie的本机支持进行数据存储。 在HTTP请求中，Cookie数据会从服务器发送到服务器。
* **Window.name:** 使用window.name属性保留数据。
* **内存：** 使用Javascript对象保留数据。

默认情况下，ContextHub使用本地持久性模式。 如果浏览器不支持或允许HTML5 localStorage，则使用会话持久性。 如果浏览器不支持或允许HTML5sessionStorage，则使用Window.name持久性。

### 存储数据 {#store-data}

在内部，将数据存储为树结构，从而可以将值添加为主要类型或复杂对象。 添加要存储的复杂对象时，对象属性会在数据树中形成分支。 例如，将以下复杂对象添加到名为location的空存储区：

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

存储数据的树结构可概念化如下：

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

树结构将存储中的数据项定义为键/值对。 在上例中，键 `/number` 与值对应 `321`，和键 `/data/country` 与值对应 `Switzerland`.

### 处理对象 {#manipulating-objects}

ContextHub提供 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) 类。 在将Javascript对象添加到存储区之前，或从存储区获取Javascript对象后，使用此类的函数处理这些对象。

此外， [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) 类提供了将对象序列化为字符串，并将字符串反序列化为对象的函数。 使用此类处理JSON数据，以支持本机不包含的浏览器 `JSON.parse` 和 `JSON.stringify` 函数。

## 与ContextHub存储交互 {#interacting-with-contexthub-stores}

使用 [`ContextHub`](contexthub-api.md#ui-event-constants) 用于将存储作为Javascript对象获取的Javascript对象。 获取存储对象后，即可处理该存储对象包含的数据。 使用 [`getAllStores`](contexthub-api.md#getallstores) 或 [`getStore`](contexthub-api.md#getstore-name) 函数来获取存储。

### 访问存储数据 {#accessing-store-data}

的 [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript类定义了与存储数据交互的多个函数。 以下函数存储并检索对象中包含的多个数据项：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

单个数据项将存储为一组键/值对。 要存储和检索值，请指定相应的键：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

请注意，自定义存储候选者可以定义其他函数，以提供对存储数据的访问。

>[!NOTE]
>
>默认情况下， ContextHub不会感知发布服务器上当前已登录的用户，并且ContextHub会将此类用户视为“匿名”。
>
>您可以通过加载用户档案存储，使ContextHub了解已登录的用户。 请参阅 [GitHub上的示例代码，此处为](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### ContextHub事件 {#contexthub-eventing}

ContextHub包含一个事件框架，通过该框架，您可以自动对存储事件做出反应。 每个存储对象都包含 [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) 可用作存储 [`eventing`](contexthub-api.md#eventing) 属性。 使用 [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 或 [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函数将Javascript函数绑定到存储事件。

## 使用ContextHub处理Cookie {#using-context-hub-to-manipulate-cookies}

ContextHub Javascript API提供跨浏览器支持来处理浏览器Cookie。 的 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 命名空间定义了用于创建、处理和删除cookie的多个函数。

## 确定已解析的ContextHub区段 {#determining-resolved-contexthub-segments}

ContextHub区段引擎允许您确定在当前上下文中解析的已注册区段。 使用 [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) 类来检索已解析的区段。 然后，使用 `getName` 或 `getPath` 函数 [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 用于测试区段的类。

### ContextHub 区段 {#contexthub-segments}

ContextHub区段安装在 `/conf/<site>/settings/wcm/segments` 节点。

以下区段随 [WKND教程网站。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 夏季
* 冬

用于解析这些区段的规则概述如下：

* 首先 [地理位置](sample-stores.md#contexthub-geolocation-sample-store-candidate) 存储区用于确定用户的纬度。
* 然后， [surferinfo存储](sample-stores.md#contexthub-surferinfo-sample-store-candidate) 确定该纬度的季节。

>[!WARNING]
>
>已安装的区段作为参考配置提供，以帮助您为项目构建自己的专用配置，因此不应直接使用。

## 调试ContextHub {#debugging-contexthub}

有许多用于调试ContextHub的选项，包括生成日志。 请参阅 [配置ContextHub ，以了解更多信息。](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## 请参阅ContextHub框架概述 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供 [诊断页面](contexthub-diagnostics.md) 您可以在此处查看ContextHub框架的概述。
