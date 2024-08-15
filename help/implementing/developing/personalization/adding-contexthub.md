---
title: 将ContextHub添加到页面并访问存储
description: 将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub JavaScript库
exl-id: 8bfe2cff-3944-4e86-a95c-ebf1cb13913c
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# 将ContextHub添加到页面并访问存储 {#adding-contexthub-to-pages-and-accessing-stores}

将ContextHub添加到您的页面以启用ContextHub功能并链接到ContextHub JavaScript库。

ContextHub JavaScript API提供了对ContextHub管理的上下文数据的访问权限。 本页简要描述了用于访问和处理上下文数据的API的主要功能。 单击API参考文档的链接可查看详细信息和代码示例。

## 将ContextHub添加到页面组件 {#adding-contexthub-to-a-page-component}

要启用ContextHub功能并链接到ContextHub JavaScript库，请在页面的`head`部分中包含`contexthub`组件。 页面组件的HTL代码应类似于以下示例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

您还需要配置ContextHub工具栏是否以预览模式显示。 请参阅[显示和隐藏ContextHub UI](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui)。

## 关于ContextHub存储 {#about-contexthub-stores}

使用ContextHub存储来保留上下文数据。 ContextHub提供了以下类型的存储，这些存储构成了所有存储类型的基础：

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [会话存储](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存储类型都是[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)类的扩展。 有关创建商店类型的信息，请参阅[创建自定义商店](extending-contexthub.md#creating-custom-store-candidates)。 有关示例存储类型的信息，请参阅[示例ContextHub存储候选项](sample-stores.md)。

### 持久性模式 {#persistence-modes}

Context Hub存储使用以下持久性模式之一：

* **本地：**&#x200B;使用HTML5 localStorage保留数据。 本地存储跨会话保留在浏览器上。
* **会话：**&#x200B;使用HTML5 sessionStorage保留数据。 会话存储会在浏览器会话期间保留，并可用于所有浏览器窗口。
* **Cookie：**&#x200B;使用浏览器对数据存储的Cookie的本机支持。 Cookie数据会以HTTP请求的形式发送到服务器，或从服务器发出。
* **Window.name：**&#x200B;使用window.name属性保留数据。
* **内存：**&#x200B;使用JavaScript对象保留数据。

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

树结构将存储中的数据项定义为键/值对。 在上例中，键`/number`与值`321`相对应，键`/data/country`与值`Switzerland`相对应。

### 处理对象 {#manipulating-objects}

ContextHub提供了用于处理JavaScript对象的[`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree)类。 在将JavaScript对象添加到存储中或从存储中获取它们之前，使用此类的函数对其进行操作。

另外，[`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json)类提供了将对象序列化为字符串以及将字符串反序列化为对象的函数。 此类用于处理JSON数据，以支持本身不包含`JSON.parse`和`JSON.stringify`函数的浏览器。

## 与ContextHub存储区交互 {#interacting-with-contexthub-stores}

使用[`ContextHub`](contexthub-api.md#ui-event-constants) JavaScript对象获取存储作为JavaScript对象。 获取存储对象后，您可以处理它包含的数据。 使用[`getAllStores`](contexthub-api.md#getallstores)或[`getStore`](contexthub-api.md#getstore-name)函数获取存储。

### 访问存储数据 {#accessing-store-data}

[`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) JavaScript类定义了多个用于与存储数据交互的功能。 以下函数存储和检索对象中包含的多个数据项：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

单个数据项作为一组键/值对进行存储。 要存储和检索值，请指定相应的键：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

自定义商店候选者可以定义其他提供存储数据访问权限的函数。

>[!NOTE]
>
>默认情况下，ContextHub不知道发布服务器上当前使用的已登录，并且ContextHub将此类用户视为“匿名”。
>
>您可以通过加载配置文件存储区，使ContextHub感知已登录的用户。 在GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)上查看示例代码： [aem-sample-we-retail。

### ContextHub事件 {#contexthub-eventing}

ContextHub包括一个事件框架，可用于自动对存储事件做出反应。 每个存储对象都包含一个[`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing)对象，该对象可用作存储的[`eventing`](contexthub-api.md#eventing)属性。 使用[`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents)或[`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents)函数将JavaScript函数绑定到存储事件。

## 使用Context Hub处理Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub JavaScript API为处理浏览器Cookie提供了跨浏览器支持。 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie)命名空间定义了若干用于创建、处理和删除Cookie的功能。

## 确定已解析的ContextHub区段 {#determining-resolved-contexthub-segments}

通过ContextHub区段引擎，可确定在当前上下文中解析的已注册区段。 使用[`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager)类的getResolvedSegments函数检索已解析的段。 然后，使用[`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment)类的`getName`或`getPath`函数来测试区段。

### ContextHub 区段 {#contexthub-segments}

ContextHub区段安装在`/conf/<site>/settings/wcm/segments`节点下。

以下区段随[WKND教程站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md)一起安装。

* 夏天
* 冬季

用于解析这些区段的规则概述如下：

* 首先，使用[地理位置](sample-stores.md#contexthub-geolocation-sample-store-candidate)存储来确定用户的纬度。
* 然后，[surferinfo存储](sample-stores.md#contexthub-surferinfo-sample-store-candidate)的月份数据项将确定它在该纬度中的哪个季节。

>[!WARNING]
>
>提供的已安装区段作为参考配置，可帮助您为项目构建自己的专用配置。 请勿直接使用它们。

## 调试Contexthub {#debugging-contexthub}

调试ContextHub有几个选项，包括生成日志。 有关详细信息，请参阅[配置ContextHub。](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## 请参阅ContextHub框架概述 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供了[诊断页面](contexthub-diagnostics.md)，您可以在其中查看ContextHub框架的概述。
