---
title: 扩展 ContextHub
description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义这些存储和模块的新类型
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 扩展 ContextHub {#extending-contexthub}

在提供的ContextHub存储和模块不符合您的解决方案要求时，定义新类型的ContextHub存储和模块。

## 创建自定义商店候选 {#creating-custom-store-candidates}

ContextHub存储是从已注册的存储候选区创建的。 要创建自定义商店，您需要创建和注册商店候选。

包含创建和注册商店候选的代码的javascript文件必须包含在 [客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md). 文件夹的类别必须符合以下模式：

```xml
contexthub.store.[storeType]
```

此 `storeType` 类别的一部分是 `storeType` 存储候选的注册位置。 (请参阅 [注册ContextHub存储候选](#registering-a-contexthub-store-candidate))。 例如，对于storeType `contexthub.mystore`，客户端库文件夹的类别必须为 `contexthub.store.contexthub.mystore`.

### 创建ContextHub存储候选 {#creating-a-contexthub-store-candidate}

要创建商店候选者，您可以使用 [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) 函数以扩展其中一个基础存储：

* [&#39;ContextHub.Store.PersistedStore&#39;](contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPStore&#39;](contexthub-api.md#contexthub-store-persistedjsonpstore)

每个基础存储区会扩展 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 商店。

以下示例创建 `ContextHub.Store.PersistedStore` 存储候选：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义商店候选者将定义其他功能或覆盖商店的初始配置。 多个 [示例存储候选](sample-stores.md) 安装在以下存储库中 `/libs/granite/contexthub/components/stores`.

### 注册ContextHub存储候选 {#registering-a-contexthub-store-candidate}

注册存储候选项，以将其与ContextHub框架集成并允许从中创建存储。 要注册候选商店，请使用 [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 的功能 `ContextHub.Utils.storeCandidates` 类。

注册候选商店时，需提供商店类型的名称。 从候选项创建存储时，可以使用存储类型标识存储所基于的候选项。

注册候选商店时，需指定其优先级。 当使用与已注册的存储候选相同的存储类型来注册存储候选时，使用具有较高优先级的候选。 因此，您可以使用新实施覆盖现有商店候选。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只需一个候选，并且优先级可以设置为 `0`，但如果您感兴趣，可以了解 [更高级的注册，](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 这允许根据javascript条件选择少数存储实现之一(`applies`)和候选优先级。

## 创建ContextHub UI模块类型 {#creating-contexthub-ui-module-types}

创建自定义UI模块类型，如果 [随ContextHub一起安装](sample-modules.md) 不符合您的要求。 要创建UI模块类型，请通过扩展 `ContextHub.UI.BaseModuleRenderer` 类，然后将其注册到 `ContextHub.UI`.

要创建UI模块渲染器，请创建 `Class` 包含呈现UI模块的逻辑的对象。 类至少必须执行以下操作：

* 扩展 `ContextHub.UI.BaseModuleRenderer` 类。 此类是所有UI模块渲染器的基本实现。 此 `Class` 对象定义一个名为的属性 `extend` 用于将此类命名为正在扩展的类。
* 提供默认配置。 创建 `defaultConfig` 属性。 此属性是一个对象，其中包含为定义的属性 [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI模块以及您需要的任何其他属性。

的源 `ContextHub.UI.BaseModuleRenderer` 位于 `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  要注册渲染器，请使用 [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 方法 `ContextHub.UI` 类。 您需要提供模块类型的名称。 当管理员基于此渲染器创建UI模块时，他们会指定此名称。

在自动执行的匿名函数中创建并注册renderer类。 以下示例基于 `contexthub.browserinfo` 用户界面模块。 此UI模块是 `ContextHub.UI.BaseModuleRenderer` 类。

```javascript
;(function() {

    var SurferinfoRenderer = new Class ({
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

包含用于创建和注册渲染器的代码的javascript文件必须包含在 [客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md). 文件夹的类别必须符合以下模式：

```javascript
contexthub.module.[moduleType]
```

此 `[moduleType]` 类别的一部分是 `moduleType` 注册了模块渲染器的位置。 例如，对于 `moduleType` 之 `contexthub.browserinfo`，客户端库文件夹的类别必须为 `contexthub.module.contexthub.browserinfo`.
