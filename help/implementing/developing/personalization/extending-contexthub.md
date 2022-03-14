---
title: 扩展 ContextHub
description: 定义新类型的ContextHub存储和模块（如果提供的存储和模块不符合您的解决方案要求）
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# 扩展 ContextHub {#extending-contexthub}

定义新类型的ContextHub存储和模块（如果提供的存储和模块不符合您的解决方案要求）。

## 创建自定义商店候选项 {#creating-custom-store-candidates}

ContextHub存储区是根据注册的存储候选区创建的。 要创建自定义存储，您需要创建并注册存储候选项。

包含用于创建和注册存储候选项的代码的javascript文件必须包含在 [客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md). 文件夹的类别必须匹配以下模式：

```xml
contexthub.store.[storeType]
```

的 `storeType` 类别的一部分是 `storeType` 其中注册了商店候选项。 (请参阅 [注册ContextHub存储候选项](#registering-a-contexthub-store-candidate))。 例如，对于 `contexthub.mystore`，客户端库文件夹的类别必须 `contexthub.store.contexthub.mystore`.

### 创建ContextHub存储候选项 {#creating-a-contexthub-store-candidate}

要创建商店候选项，请使用 [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) 函数来扩展一个基库：

* [&#39;ContextHub.Store.PersiredStore&#39;](contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersiredJSONPStore&#39;](contexthub-api.md#contexthub-store-persistedjsonpstore)

请注意，每个基本存储库都会 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 存储。

以下示例创建 `ContextHub.Store.PersistedStore` 存储候选项：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义商店候选者将定义其他函数或覆盖商店的初始配置。 几个 [示例存储候选项](sample-stores.md) 安装在下面的存储库中 `/libs/granite/contexthub/components/stores`.

### 注册ContextHub存储候选项 {#registering-a-contexthub-store-candidate}

注册存储候选项以将其与ContextHub框架集成，并允许从中创建存储。 要注册商店候选商，请使用 [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函数 `ContextHub.Utils.storeCandidates` 类。

注册存储候选项时，将提供存储类型的名称。 从候选项创建存储时，使用存储类型来标识其所基于的候选项。

注册商店候选项时，需指明其优先级。 当使用与已注册的存储候选者相同的存储类型注册存储候选者时，使用具有较高优先级的候选者。 因此，您可以使用新实施来覆盖现有的存储候选项。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只需要一个候选者，并且优先级可以设置为 `0`，但如果您感兴趣，您可以了解 [更高级的注册，](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 这允许根据javascript条件(`applies`)和候选优先级。

## 创建ContextHub UI模块类型 {#creating-contexthub-ui-module-types}

在 [随ContextHub一起安装](sample-modules.md) 不要满足您的要求。 要创建UI模块类型，请通过扩展 `ContextHub.UI.BaseModuleRenderer` 然后在 `ContextHub.UI`.

要创建UI模块渲染器，请创建 `Class` 包含呈现UI模块的逻辑的对象。 类必须至少执行以下操作：

* 扩展 `ContextHub.UI.BaseModuleRenderer` 类。 此类是所有UI模块渲染器的基本实现。 的 `Class` 对象定义名为 `extend` 用于将此类命名为正在扩展的类。
* 提供默认配置。 创建 `defaultConfig` 属性。 此属性是一个对象，其中包含为 [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI模块以及您需要的任何其他属性。

的来源 `ContextHub.UI.BaseModuleRenderer` 位于 `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  要注册渲染器，请使用 [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 方法 `ContextHub.UI` 类。 您需要提供模块类型的名称。 当管理员基于此呈现器创建UI模块时，他们会指定此名称。

在自执行的匿名函数中创建并注册渲染器类。 以下示例基于 `contexthub.browserinfo` UI模块。 此UI模块是 `ContextHub.UI.BaseModuleRenderer` 类。

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

包含用于创建和注册渲染器的代码的javascript文件必须包含在 [客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md). 文件夹的类别必须匹配以下模式：

```javascript
contexthub.module.[moduleType]
```

的 `[moduleType]` 类别的一部分是 `moduleType` 其中注册了模块渲染器。 例如，对于 `moduleType` of `contexthub.browserinfo`，客户端库文件夹的类别必须 `contexthub.module.contexthub.browserinfo`.
