---
title: 将ContextHub添加到页面并访问存储
description: 将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub JavaScript库
exl-id: 8bfe2cff-3944-4e86-a95c-ebf1cb13913c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 将ContextHub添加到页面并访问存储 {#adding-contexthub-to-pages-and-accessing-stores}

将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub JavaScript库。

ContextHub JavaScript API提供了对ContextHub管理的上下文数据的访问权限。 本页简要描述了用于访问和处理上下文数据的API的主要功能。 单击API参考文档的链接可查看详细信息和代码示例。

## 将ContextHub添加到页面组件 {#adding-contexthub-to-a-page-component}

要启用ContextHub功能并链接到ContextHub JavaScript库，请包含 `contexthub` 中的组件 `head` 部分。 页面组件的HTL代码应类似于以下示例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

请注意，您还需要配置ContextHub工具栏是否以预览模式显示。 请参阅 [显示和隐藏ContextHub UI](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui).

## 关于ContextHub存储 {#about-contexthub-stores}

使用ContextHub存储来保留上下文数据。 ContextHub提供了以下类型的存储，这些存储构成了所有存储类型的基础：

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [会话存储](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存储类型都是 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 类。 有关创建存储类型的信息，请参见 [创建自定义存储](extending-contexthub.md#creating-custom-store-candidates). 有关示例存储类型的信息，请参见 [示例ContextHub存储候选项](sample-stores.md).

### 持久性模式 {#persistence-modes}

Context Hub存储使用以下持久性模式之一：

* **本地：** 使用HTML5 localStorage保留数据。 本地存储跨会话保留在浏览器上。
* **会话：** 使用HTML5 sessionStorage保留数据。 会话存储会在浏览器会话期间保留，并可用于所有浏览器窗口。
* **Cookie：** 使用浏览器对数据存储的Cookie的本机支持。 Cookie数据会以HTTP请求的形式发送到服务器，或从服务器发出。
* **Window.name：** 使用window.name属性保留数据。
* **内存：** 使用JavaScript对象来保留数据。

默认情况下，Context Hub使用本地持久性模式。 如果浏览器不支持或不允许使用HTML5 localStorage，则使用会话持久性。 如果浏览器不支持或不允许使用HTML5 sessionStorage，则使用Window.name持久性。

### 存储数据 {#store-data}

在内部，存储数据形成树结构，从而能够将值添加为主要类型或复杂对象。 将复杂对象添加到存储区时，对象属性将形成数据树中的分支。 例如，将以下复杂对象添加到名为location的空存储中：

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

存储数据的树结构可以概念化，如下所示：

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

树结构将存储中的数据项定义为键/值对。 在上例中，键 `/number` 与值对应 `321`和键 `/data/country` 与值对应 `Switzerland`.

### 处理对象 {#manipulating-objects}

ContextHub提供 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) 用于处理JavaScript对象的类。 在将JavaScript对象添加到存储中或从存储中获取它们之前，使用此类的函数对其进行处理。

此外， [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) 类提供了将对象序列化为字符串以及将字符串反序列化为对象的函数。 此类用于处理JSON数据，以支持本身不包含 `JSON.parse` 和 `JSON.stringify` 函数。

## 与ContextHub存储区交互 {#interacting-with-contexthub-stores}

使用 [`ContextHub`](contexthub-api.md#ui-event-constants) 用于作为JavaScript对象获取存储的JavaScript对象。 获取存储对象后，您可以处理它包含的数据。 使用 [`getAllStores`](contexthub-api.md#getallstores) 或 [`getStore`](contexthub-api.md#getstore-name) 函数以获取存储。

### 访问存储数据 {#accessing-store-data}

此 [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) JavaScript类定义了几个用于与存储数据交互的函数。 以下函数存储和检索对象中包含的多个数据项：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

单个数据项作为一组键/值对进行存储。 要存储和检索值，请指定相应的键：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

请注意，自定义候选存储区可以定义其他提供存储数据访问权限的函数。

>[!NOTE]
>
>默认情况下，ContextHub不知道发布服务器上当前使用的已登录，并且ContextHub将此类用户视为“匿名”。
>
>您可以通过加载配置文件存储区，使ContextHub感知已登录的用户。 请参阅 [此处为GitHub上的示例代码](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### ContextHub事件 {#contexthub-eventing}

ContextHub包括一个事件框架，可用于自动对存储事件做出反应。 每个存储对象包含 [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) 可用作商店的对象 [`eventing`](contexthub-api.md#eventing) 属性。 使用 [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 或 [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 函数，用于将JavaScript函数绑定到存储事件。

## 使用Context Hub处理Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub JavaScript API为处理浏览器Cookie提供了跨浏览器支持。 此 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace定义了用于创建、处理和删除Cookie的多个函数。

## 确定已解析的ContextHub区段 {#determining-resolved-contexthub-segments}

通过ContextHub区段引擎，可确定在当前上下文中解析的已注册区段。 使用的getResolvedSegments函数 [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) 类以检索已解析的区段。 然后，使用 `getName` 或 `getPath` 的功能 [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 用于测试区段的类。

### ContextHub 区段 {#contexthub-segments}

ContextHub区段安装在 `/conf/<site>/settings/wcm/segments` 节点。

以下区段随 [WKND教程网站](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* 夏天
* 冬季

用于解析这些区段的规则概述如下：

* 首先 [地理位置](sample-stores.md#contexthub-geolocation-sample-store-candidate) 存储用于确定用户的纬度。
* 然后，的月份数据项 [surferinfo store](sample-stores.md#contexthub-surferinfo-sample-store-candidate) 确定该纬度中的哪个季节。

>[!WARNING]
>
>安装的区段作为参考配置提供，以帮助您为项目构建自己的专用配置，因此不应直接使用。

## 调试Contexthub {#debugging-contexthub}

调试ContextHub有几个选项，包括生成日志。 请参阅 [配置ContextHub以了解更多信息。](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## 请参阅ContextHub框架概述 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供 [诊断页面](contexthub-diagnostics.md) 其中，您可以查看ContextHub框架的概述。
