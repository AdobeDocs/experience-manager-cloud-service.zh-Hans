---
title: 扩展ContextHub
description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型
translation-type: tm+mt
source-git-commit: ddfdcf74977adf00bc0ab01b0b1a669781f0d730
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# 扩展ContextHub {#extending-contexthub}

当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型。

## 创建自定义商店候选 {#creating-custom-store-candidates}

ContextHub存储区是从注册的存储候选区创建的。 要创建自定义商店，您需要创建和注册商店候选。

<!--The javascript file that includes the code that creates and registers the store candidate must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

包含创建和注册存储候选项的代码的javascript文件必须包含在客户端库文件夹中。 文件夹的类别必须与以下模式匹配：

```xml
contexthub.store.[storeType]
```

类别 `storeType` 的一部分是注册商 `storeType` 店候选人的部分。 (请参 [阅注册ContextHub存储候选](#registering-a-contexthub-store-candidate))。 例如，对于storeType `contexthub.mystore`，客户端库文件夹的类别必须为 `contexthub.store.contexthub.mystore`。

### 创建ContextHub存储候选项 {#creating-a-contexthub-store-candidate}

要创建商店候选，请使用该 [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) 函数扩展其中一个基本商店：

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

请注意，每个基本存储扩展 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 存储。

以下示例创建存储候选项的最 `ContextHub.Store.PersistedStore` 简单扩展：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义存储候选者将定义其他函数或覆盖存储的初始配置。 以下 [存储库中安装](sample-stores.md) 了几个样本存储候选 `/libs/granite/contexthub/components/stores`项。

### 注册ContextHub存储候选项 {#registering-a-contexthub-store-candidate}

注册一个存储候选项以将其与ContextHub框架集成，并允许从它创建存储。 要注册存储候选项，请 [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 使用类的 `ContextHub.Utils.storeCandidates` 函数。

注册商店候选项时，请提供商店类型的名称。 从候选者创建商店时，您使用商店类型来标识其所基于的候选者。

注册商店候选项时，请指明其优先级。 当使用与已注册的存储候选者相同的存储类型来注册存储候选者时，使用具有较高优先级的候选者。 因此，您可以使用新的实施来覆盖现有的存储候选。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只有一个候选者是必需的，并且优先级可以设置为 `0`，但如果您感兴趣，您可以了解更多 [高级注册](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)`applies`，这允许根据javascript条件()和候选优先级选择少数存储实现之一。

## 创建ContextHub UI模块类型 {#creating-contexthub-ui-module-types}

当随ContextHub安装的模块类型不符合 [您的要求时](sample-modules.md) ，创建自定义UI模块类型。 要创建UI模块类型，请通过扩展类，然后向注册它来 `ContextHub.UI.BaseModuleRenderer` 创建新的UI模块渲染器 `ContextHub.UI`。

要创建UI模块渲染器，请创 `Class` 建一个对象，其中包含渲染UI模块的逻辑。 您的课程至少必须执行以下操作：

* 扩展 `ContextHub.UI.BaseModuleRenderer` 类。 此类是所有UI模块渲染器的基本实现。 对 `Class` 象定义一个名为的 `extend` 属性，该属性用于将此类命名为正在扩展的类。
* 提供默认配置。 创建属 `defaultConfig` 性。 此属性是一个对象，包括为UI模块定义的属 [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) 性以及您需要的任何其他属性。

源位 `ContextHub.UI.BaseModuleRenderer` 于 `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`。  要注册呈示器，请使 [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 用类的方 `ContextHub.UI` 法。 您需要为模块类型提供名称。 管理员根据此呈现器创建UI模块时，会指定此名称。

在自执行匿名函数中创建并注册呈示器类。 以下示例基于UI模块的源 `contexthub.browserinfo` 代码。 此UI模块是类的简单扩 `ContextHub.UI.BaseModuleRenderer` 展。

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

<!--The javascript file that includes the code that creates and registers the renderer must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

包含创建和注册呈现器的代码的javascript文件必须包含在客户端库文件夹中。 文件夹的类别必须与以下模式匹配：

```javascript
contexthub.module.[moduleType]
```

类别 `[moduleType]` 的一部分是模块呈 `moduleType` 示器注册时使用的部分。 例如，对于 `moduleType` , `contexthub.browserinfo`客户端库文件夹的类别必须为 `contexthub.module.contexthub.browserinfo`。
