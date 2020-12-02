---
title: 扩展ContextHub
description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# 扩展ContextHub {#extending-contexthub}

当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型。

## 创建自定义存储候选项{#creating-custom-store-candidates}

ContextHub存储区是从注册的存储候选区创建的。 要创建自定义商店，您需要创建和注册商店候选。

包含创建和注册存储候选项的代码的javascript文件必须包含在[客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md)中。 文件夹的类别必须与以下模式匹配：

```xml
contexthub.store.[storeType]
```

类别的`storeType`部分是注册存储候选项的`storeType`。 （请参阅[注册ContextHub存储候选项](#registering-a-contexthub-store-candidate)）。 例如，对于`contexthub.mystore`的storeType，客户端库文件夹的类别必须为`contexthub.store.contexthub.mystore`。

### 创建ContextHub存储候选{#creating-a-contexthub-store-candidate}

要创建存储候选项，请使用[`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent)函数扩展其中一个基本存储：

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

请注意，每个基本存储扩展[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)存储。

以下示例创建`ContextHub.Store.PersistedStore`存储候选项的最简单扩展：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义存储候选者将定义其他函数或覆盖存储的初始配置。 在`/libs/granite/contexthub/components/stores`下的存储库中安装了多个[示例存储候选](sample-stores.md)。

### 注册ContextHub存储候选项{#registering-a-contexthub-store-candidate}

注册一个存储候选项以将其与ContextHub框架集成，并允许从它创建存储。 要注册存储候选项，请使用`ContextHub.Utils.storeCandidates`类的[`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)函数。

注册商店候选项时，请提供商店类型的名称。 从候选者创建商店时，您使用商店类型来标识其所基于的候选者。

注册商店候选项时，请指明其优先级。 当使用与已注册的存储候选者相同的存储类型来注册存储候选者时，使用具有较高优先级的候选者。 因此，您可以使用新的实施来覆盖现有的存储候选。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只有一个候选者是必需的，并且优先级可以设置为`0`，但如果您感兴趣，您可以了解关于[更多高级注册的信息，](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)允许根据javascript条件(`applies`)和候选优先级选择少数存储实现之一。

## 创建ContextHub UI模块类型{#creating-contexthub-ui-module-types}

当与ContextHub](sample-modules.md)一起安装的[模块类型不符合您的要求时，创建自定义UI模块类型。 要创建UI模块类型，请通过扩展`ContextHub.UI.BaseModuleRenderer`类，然后向`ContextHub.UI`注册它来创建新的UI模块渲染器。

要创建UI模块渲染器，请创建一个`Class`对象，其中包含渲染UI模块的逻辑。 您的课程至少必须执行以下操作：

* 扩展`ContextHub.UI.BaseModuleRenderer`类。 此类是所有UI模块渲染器的基本实现。 `Class`对象定义一个名为`extend`的属性，该属性用于将此类命名为正在扩展的类。
* 提供默认配置。 创建`defaultConfig`属性。 此属性是一个对象，其中包括为[`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI模块定义的属性以及您需要的任何其他属性。

`ContextHub.UI.BaseModuleRenderer`的源位于`/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`。  要注册呈示器，请使用`ContextHub.UI`类的[`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)方法。 您需要为模块类型提供名称。 管理员根据此呈现器创建UI模块时，会指定此名称。

在自执行匿名函数中创建并注册呈示器类。 以下示例基于`contexthub.browserinfo` UI模块的源代码。 此UI模块是`ContextHub.UI.BaseModuleRenderer`类的简单扩展。

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

包含创建和注册呈示器的代码的javascript文件必须包含在[客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md)中。 文件夹的类别必须与以下模式匹配：

```javascript
contexthub.module.[moduleType]
```

类别的`[moduleType]`部分是模块渲染器注册时使用的`moduleType`。 例如，对于`contexthub.browserinfo`的`moduleType`，客户端库文件夹的类别必须为`contexthub.module.contexthub.browserinfo`。
