---
title: 将ContextHub添加到页面和访问商店
description: 将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub Javascript库
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# 将ContextHub添加到页面和访问存储{#adding-contexthub-to-pages-and-accessing-stores}

将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub Javascript库。

ContextHub Javascript API提供对ContextHub管理的上下文数据的访问。 本页简要介绍了用于访问和操作上下文数据的API的主要功能。 按照指向API参考文档的链接查看详细信息和代码示例。

## 将ContextHub添加到页面组件{#adding-contexthub-to-a-page-component}

要启用ContextHub功能并链接到ContextHub Javascript库，请在页面的`head`部分包含`contexthub`组件。 页面组件的HTL代码应类似于以下示例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

请注意，您还需要配置ContextHub工具栏是否以预览模式显示。 请参阅[显示和隐藏ContextHub UI](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui)。

## 关于ContextHub存储{#about-contexthub-stores}

使用ContextHub存储保留上下文数据。 ContextHub提供以下类型的存储，这些存储构成了所有存储类型的基础：

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersitedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存储类型都是[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)类的扩展。 有关创建新存储类型的信息，请参阅[创建自定义存储](extending-contexthub.md#creating-custom-store-candidates)。 有关示例存储类型的信息，请参阅[示例ContextHub存储候选项](sample-stores.md)。

### 持久性模式{#persistence-modes}

Context Hub存储区使用以下持久性模式之一：

* **本地：** 使用HTML5 localStorage保留数据。本地存储会跨会话在浏览器上保留。
* **会话：** 使用HTML5会话存储保留数据。会话存储在浏览器会话的持续时间内持续存在，并且可用于所有浏览器窗口。
* **Cookie:** 使用浏览器对Cookie的本机支持进行数据存储。在HTTP请求中，Cookie数据会发送到服务器或从服务器发送。
* **Window.name：使** 用window.name属性保留数据。
* **内存：** 使用Javascript对象保留数据。

默认情况下，Context Hub使用本地持久性模式。 如果浏览器不支持或允许HTML5 localStorage，则使用会话持久性。 如果浏览器不支持或允许HTML5 sessionStorage，则使用Window.name持久性。

### 存储数据 {#store-data}

在内部，存储数据以树形结构的形式，使值能够添加为主类型或复杂对象。 在向存储添加复杂对象时，对象属性在数据树中形成分支。 例如，以下复杂对象将添加到名为location的空存储区：

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

存储数据的树结构可以概念化为：

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

树结构将存储中的数据项定义为键／值对。 在上例中，键`/number`与值`321`对应，键`/data/country`与值`Switzerland`对应。

### 处理对象{#manipulating-objects}

ContextHub提供[`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree)类以处理Javascript对象。 在将Javascript对象添加到商店或从商店获取它们之前，使用此类的函数来处理这些对象。

此外，[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json)类还提供一些函数，用于对对象进行序列化，以及将字符串反序列化为对象。 使用此类处理JSON数据以支持本机不包含`JSON.parse`和`JSON.stringify`函数的浏览器。

## 与ContextHub存储区交互{#interacting-with-contexthub-stores}

使用[`ContextHub`](contexthub-api.md#ui-event-constants) Javascript对象将存储作为Javascript对象获取。 获得存储对象后，您可以处理它包含的数据。 使用[`getAllStores`](contexthub-api.md#getallstores)或[`getStore`](contexthub-api.md#getstore-name)函数获取存储。

### 访问存储数据{#accessing-store-data}

[`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript类定义与存储数据交互的多个函数。 以下函数存储和检索对象中包含的多个数据项：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

单个数据项作为一组键／值对进行存储。 要存储和检索值，请指定相应的键：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

请注意，自定义存储候选者可以定义提供存储数据访问权限的其他函数。

>[!NOTE]
>
>默认情况下，ContextHub不知道当前在发布服务器上使用的登录名，ContextHub将这些用户视为“匿名”。
>
>您可以通过加载用户档案存储来使ContextHub了解已登录的用户。 请在此处参阅GitHub上的[示例代码](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)。

### ContextHub事件{#contexthub-eventing}

ContextHub包含一个事件框架，它允许您对存储事件做出自动响应。 每个存储对象都包含一个[`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing)对象，该对象可用作存储的[`eventing`](contexthub-api.md#eventing)属性。 使用[`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents)或[`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents)函数将Javascript函数绑定到存储事件。

## 使用Context Hub操纵Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub Javascript API提供跨浏览器支持以处理浏览器cookie。 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie)命名空间定义用于创建、操作和删除Cookie的多个函数。

## 确定已解析的ContextHub区段{#determining-resolved-contexthub-segments}

ContextHub区段引擎允许您确定在当前上下文中解析的已注册区段。 使用[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager)类的getResolvedSegments函数检索已解析的段。 然后，使用[`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment)类的`getName`或`getPath`函数测试段。

### ContextHub 区段 {#contexthub-segments}

ContextHub区段安装在`/conf/<site>/settings/wcm/segments`节点下。

以下区段随[WKND教程站点一起安装。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 夏
* 冬

用于解析这些区段的规则概述如下：

* 首先，使用[地理位置](sample-stores.md#contexthub-geolocation-sample-store-candidate)存储确定用户的纬度。
* 然后，[surferinfo store](sample-stores.md#contexthub-surferinfo-sample-store-candidate)的月份数据项决定该纬度所在的季节。

>[!WARNING]
>
>安装的区段会作为参考配置提供，以帮助您为项目构建自己的专用配置，因此不应直接使用。

## 调试ContextHub {#debugging-contexthub}

有许多用于调试ContextHub的选项，包括生成日志。 有关详细信息，请参阅[配置ContextHub。](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## 请参阅ContextHub Framework {#see-an-overview-of-the-contexthub-framework}概述

ContextHub提供[诊断页面](contexthub-diagnostics.md)，您可在其中看到ContextHub框架的概述。
