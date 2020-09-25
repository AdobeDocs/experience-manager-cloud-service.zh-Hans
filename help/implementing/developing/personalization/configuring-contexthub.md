---
title: 配置ContextHub
description: 了解如何配置Context Hub。
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 1%

---


# 配置ContextHub {#configuring-contexthub}

ContextHub是存储、处理和呈现上下文数据的框架。 有关ContextHub的详细信息，请参阅ContextHub [开发人员概述](contexthub.md)。

您可以配置ContextHub工具栏以控制它是否显示在预览模式中、创建ContextHub存储区以及添加UI模块。

## 显示和隐藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

将AdobeGranite ContextHub OSGi服务配置为在页 [面上显示](/help/sites-cloud/authoring/personalization/targeted-content.md) 或隐藏ContextHub UI。 此服务的PID是 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服务，您可以使用Web [控制台](/help/implementing/deploying/configuring-osgi.md) ，或在存储库中使用JCR节点：

* **Web控制台：** 要显示UI，请选择显示UI属性。 要隐藏UI，请清除隐藏UI属性。
* **JCR节点：** 要显示UI，请将布尔属 `com.adobe.granite.contexthub.show_ui` 性设置为 `true`。 要隐藏UI，请将属性设置为 `false`。

显示ContextHub UI时，它仅显示在AEM作者实例的页面上。 UI不显示在发布实例的页面上。

## 添加ContextHub UI模式和模块 {#adding-contexthub-ui-modes-and-modules}

配置在预览模式下ContextHub工具栏中显示的UI模式和模块：

* UI模式：相关模块组
* 模块：用于显示存储中的上下文数据并允许作者操作上下文的构件

UI模式在工具栏左侧显示为一系列图标。 选择后，UI模式的模块将显示在右侧。

![ContextHub工具栏](assets/contexthub-toolbar.png)

图标是Coral UI图 [标库中的引用](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 添加UI模式 {#adding-a-ui-mode}

添加UI模式以组相关的ContextHub模块。 在创建UI模式时，您提供标题和图标，它们显示在ContextHub工具栏中。

1. 在Experience Manager边栏上，单击或点按工具>站点> Context Hub。
1. 单击或点按默认的配置容器。
1. 单击或点按Context Hub配置。
1. 单击或点按创建按钮，然后单击或点按Context Hub UI模式。

   ![添加UI模式](assets/contexthub-ui-mode.png)

1. 提供以下属性的值：

   * UI模式标题：标识UI模式的标题
   * 模式图标：要使用的 [Coral UI图标](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) (例如， `coral-Icon--user`
   * 已启用：选择此项可在ContextHub工具栏中显示UI模式

1. 单击或点按保存。

### 添加UI模块 {#adding-a-ui-module}

将ContextHub UI模块添加到UI模式，以便它显示在ContextHub工具栏中以预览页面内容。 添加UI模块时，您将创建向ContextHub注册的模块类型实例。 要添加UI模块，您必须知道关联模块类型的名称。

AEM提供基本UI模块类型以及几种示例UI模块类型，您可以在这些类型上对UI模块进行基础设置。 下表对每种方法进行了简要说明。 有关开发自定义UI模块的信息，请参 [阅创建ContextHub UI模块](extending-contexthub.md#creating-contexthub-ui-module-types)。

UI模块属性包括详细信息配置，您可以在其中提供模块特定属性的值。 您以JSON格式提供详细配置。 表中的“模块类型”列提供了指向每个UI模块类型所需JSON代码的相关信息的链接。

| 模块类型 | 描述 | 存储 |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 通用UI模块类型 | 在UI模块属性中配置 |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | 显示有关浏览器的信息 | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 显示日期和时间信息 | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | 显示客户端的经度和纬度，以及地图上的位置。 允许您更改位置。 | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | 显示设备的屏幕方向（横向或纵向） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | 显示有关页面标记的统计信息 | `tagcloud` |
| [granite.用户档案](sample-modules.md#granite-profile-ui-module-type) | 显示当前用户的用户档案信息， `authorizableID`包括 `displayName` 和 `familyName`。 您可以更改和 `displayName` 的值 `familyName`。 | `profile` |

1. 在Experience Manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按要向其添加UI模块的配置容器。
1. 单击或键入要向其添加UI模块的ContextHub配置。
1. 单击或点按要添加UI模块的UI模式。
1. 单击或点按创建按钮，然后单击或点按ContextHub UI模块（通用）。

   ![ContextHub UI模块](assets/contexthub-ui-module.png)

1. 提供以下属性的值：

   * UI模块标题：标识UI模块的标题
   * 模块类型：模块类型
   * 已启用：选择此项可在ContextHub工具栏中显示UI模块

1. （可选）要覆盖默认的存储配置，请输入JSON对象以配置UI模块。
1. 单击或点按保存。

## 创建ContextHub存储 {#creating-a-contexthub-store}

创建Context Hub存储库以保留用户数据并根据需要访问数据。 ContextHub存储基于注册的存储候选。 创建商店时，需要注册商店候选者的storeType值。 (请参 [阅创建自定义商店候选](extending-contexthub.md#creating-custom-store-candidates)。)

### 详细的存储配置 {#detailed-store-configuration}

配置存储时，Detail Configuration属性允许您为存储特定属性提供值。 该值基于存储 `config` 器函数的参数 `init` 。 因此，是否需要提供此值以及值的格式取决于存储。

Detail Configuration属性的值是JSON格 `config` 式的对象。

### 样例存储候选项 {#sample-store-candidates}

AEM提供以下可作为商店基础的样本商店候选。

| 存储类型 | 描述 |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | 存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager检索区段 |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | 存储浏览器位置的经度和纬度。 |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | 定义多个设备的属性和功能，并检测当前客户端设备 |
| [granite.用户档案](sample-stores.md#granite-profile-sample-store-candidate) | 存储当前用户的用户档案数据 |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | 存储有关客户端的信息，如设备信息、浏览器类型和窗口方向 |

1. 在Experience Manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按默认配置容器。
1. 单击或点按Contexthub配置
1. 要添加商店，请单击或点按创建图标，然后单击或点按ContextHub商店配置。

   ![ContextHub存储配置](assets/contexthub-store-configuration.png)

1. 提供基本配置属性的值，然后单击或点按下一步：

   * **配置标题：** 标识商店的标题
   * **存储类型：** 存储候选项的storeType属性值，该属性作为存储的基础
   * **必需：** 选择
   * **已启用：** 选择以启用商店

1. （可选）要覆盖默认的存储配置，请在“详细配置(JSON)”框中输入JSON对象。
1. 单击或点按保存。

## 示例：使用JSONP服务  {#example-using-a-jsonp-service}

此示例说明如何在UI模块中配置存储和显示数据。 在此示例中，jsontest.com站点的MD5服务用作存储的数据源。 服务以JSON格式返回给定字符串的MD5哈希代码。

配置contexthub.generic-jsonp存储，以便它存储服务调用的数据 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服务返回UI模块中显示的以下数据：

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 创建contexthub.generic-jsonp商店 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp示例存储候选项允许您从JSONP服务或返回JSON数据的Web服务检索数据。 对于此存储候选项，请使用存储配置提供有关要使用的JSONP服务的详细信息。

Javascript [类的](contexthub-api.md#init-name-config) init函数定义一个对 `ContextHub.Store.JSONPStore``config` 象，该对象初始化此存储候选项。 该 `config` 对象包含 `service` 一个包含JSONP服务详细信息的对象。 要配置商店，您需要 `service` 以JSON格式提供该对象作为“详细配置”属性的值。

要保存jsontest.com站点的MD5服务中的数据，请使用以下属 [性创建ContextHub](#creating-a-contexthub-store) Store中的步骤：

* **配置标题：** md5
* **存储类型：** contexthub.generic-jsonp
* **必需：** 选择
* **已启用：** 选择
* **详细配置 (JSON):**

   ```javascript
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### 为md5数据添加UI模块 {#adding-a-ui-module-for-the-md-data}

将UI模块添加到ContextHub工具栏以显示存储在示例md5商店中的数据。 在此示例中，contexthub.base模块用于生成以下UI模块：

![ContextHub MD5商店](assets/contexthub-md5-store.png)

使用添加UI [模块中的过程](#adding-a-ui-module) ，将UI模块添加到现有UI模式，如示例人物UI模式。 对于UI模块，请使用以下属性值：

* **UI模块标题：** MD5
* **模块类型：** contexthub.base
* **详细配置 (JSON):**

   ```javascript
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Conversion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## 调试ContextHub {#debugging-contexthub}

可以启用ContextHub的调试模式以允许进行疑难解答。 调试模式可以通过ContextHub配置或通过CRXDE启用。

### 通过配置 {#via-the-configuration}

编辑ContextHub的配置并选中“调试”选 **项**

1. 在边栏中，单击或点 **按工具>站点> ContextHub**
1. 单击或点按默认的配 **置容器**
1. 选择ContextHub **配置** ，然后单击或点按编 **辑选定元素**
1. 单击或点按调 **试** ，然后单击或点按保 **存**

### 通过CRXDE {#via-crxde}

使用CRXDE Lite将属性 `debug` 设置 **为** true:

* `/conf/global/settings/cloudsettings` 或
* `/conf/<site>/settings/cloudsettings`

### 记录ContextHub的调试消息 {#logging-debug-messages-for-contexthub}

配置AdobeGranite ContextHub OSGi服务(PID =) `com.adobe.granite.contexthub.impl.ContextHubImpl`以记录详细的调试消息，这些消息在开发时很有用。

要配置服务，您可以使用Web [控制台](/help/implementing/deploying/configuring-osgi.md) ，或在存储库中使用JCR节点：

* Web控制台：要记录调试消息，请选择调试属性。
* JCR节点：要记录调试消息，请将布尔 `com.adobe.granite.contexthub.debug` 属性设 `true`置为。

### 静默模式 {#silent-mode}

“静默”模式抑制所有调试信息。 与常规调试选项不同，静默模式是全局设置，优先于ContextHub配置级别上的任何调试设置。

这对于您的发布实例非常有用，因为您根本不需要任何调试信息。 由于它是全局设置，因此它通过OSGi启用。

1. 打开 **Adobe Experience ManagerWeb控制台配置** : `http://<host>:<port>/system/console/configMgr`
1. 搜索 **AdobeGranite ContextHub**
1. 单击配置 **AdobeGranite ContextHub** ，编辑其属性
1. 选中“静默模 **式”选项** ，然后单击“ **保存”**

## 禁用ContextHub {#disabling-contexthub}

可以禁用ContextHub以阻止它加载js/css和初始化。 禁用ContextHub有两种选项：

* 编辑ContextHub的配置并选中“禁用ContextHub” **选项**

   1. 在边栏中，单击或点 **按工具>站点> ContextHub**
   1. 单击或点按默认的配 **置容器**
   1. 选择ContextHub **配置** ，然后单击或点按编 **辑选定元素**
   1. 单击或点按 **禁用ContextHub** ，然后单击或点按 **保存**

或

* 使用CRXDE Lite将属性 `disabled` 设置 **为** true `/conf/global/settings/cloudsettings/<configName>/contexthub`
