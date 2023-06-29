---
title: 配置 ContextHub
description: 了解如何配置上下文中心。
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 1%

---

# 配置 ContextHub {#configuring-contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 有关ContextHub的详细信息，请参阅 [ContextHub开发人员概述](contexthub.md).

您可以配置ContextHub工具栏以控制它是否显示在预览模式下、创建ContextHub存储区以及添加UI模块。

## 显示和隐藏ContextHub用户界面 {#showing-and-hiding-the-contexthub-ui}

配置AdobeGranite ContextHub OSGi服务以显示或隐藏 [ContextHub UI](/help/sites-cloud/authoring/personalization/targeted-content.md) 页面上。 此服务的PID为 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服务，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) 或使用存储库中的JCR节点：

* **Web控制台：** 要显示UI，请选择显示UI属性。 要隐藏UI，请清除隐藏UI属性。
* **JCR节点：** 要显示UI，请设置布尔值 `com.adobe.granite.contexthub.show_ui` 属性至 `true`. 要隐藏UI，请将属性设置为 `false`.

显示ContextHub UI时，它仅显示在AEM创作实例上的页面上。 UI未出现在发布实例的页面上。

## 添加ContextHub UI模式和模块 {#adding-contexthub-ui-modes-and-modules}

配置在“预览”模式下显示在ContextHub工具栏中的UI模式和模块：

* UI模式：相关模块组
* 模块：从存储区公开上下文数据并允许作者处理上下文的小部件

UI模式在工具栏左侧显示为一系列图标。 选中后，UI模式的模块将显示在右侧。

![ContextHub 工具栏](assets/contexthub-toolbar.png)

图标是来自的引用 [Coral UI图标库](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### 添加UI模式 {#adding-a-ui-mode}

添加UI模式以分组相关的ContextHub模块。 创建UI模式时，需提供显示在ContextHub工具栏中的标题和图标。

1. 在Experience Manager边栏上，单击或点按工具>站点> Context Hub。
1. 单击或点按默认配置容器。
1. 单击或点按Context Hub配置。
1. 单击或点按创建按钮，然后单击或点按Context Hub UI模式。

   ![添加UI模式](assets/contexthub-ui-mode.png)

1. 提供以下属性的值：

   * UI模式标题：标识UI模式的标题
   * 模式图标：的选择器 [Coral UI图标](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 以使用，例如 `coral-Icon--user`
   * 启用：选择此项可在ContextHub工具栏中显示UI模式

1. 单击或点按保存。

### 添加UI模块 {#adding-a-ui-module}

将ContextHub UI模块添加到UI模式，以便该模块显示在ContextHub工具栏中，用于预览页面内容。 添加UI模块时，您将创建一个已在ContextHub中注册的模块类型实例。 要添加UI模块，您必须知道关联模块类型的名称。

AEM提供了一个基本UI模块类型以及多个示例UI模块类型，您可以基于这些类型建立UI模块。 下表简要说明了每个报表包。 有关开发自定义UI模块的信息，请参阅 [创建ContextHub UI模块](extending-contexthub.md#creating-contexthub-ui-module-types).

UI模块属性包括详细配置，您可以在其中提供特定于模块的属性的值。 您以JSON格式提供详细配置。 表中的模块类型列提供指向每个UI模块类型所需JSON代码信息的链接。

| 模块类型 | 描述 | 存储 |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 通用UI模块类型 | 在UI模块属性中配置 |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | 显示有关浏览器的信息 | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 显示日期和时间信息 | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | 显示客户端的纬度和经度，以及地图上的位置。 允许您更改位置。 | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | 显示设备的屏幕方向（横向或纵向） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | 显示有关页面标记的统计信息 | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | 显示当前用户的配置文件信息，包括 `authorizableID`， `displayName` 和 `familyName`. 您可以更改 `displayName` 和 `familyName`. | `profile` |

1. 在Experience Manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按要向其中添加UI模块的配置容器。
1. 单击或键入要向其中添加UI模块的ContextHub配置。
1. 单击或点按要向其中添加UI模块的UI模式。
1. 单击或点按创建按钮，然后单击或点按ContextHub UI模块（常规）。

   ![ContextHub UI模块](assets/contexthub-ui-module.png)

1. 提供以下属性的值：

   * UI模块标题：标识用户界面模块的标题
   * 模块类型：模块类型
   * 已启用：选择以在ContextHub工具栏中显示UI模块

1. （可选）要覆盖默认存储配置，请输入要配置UI模块的JSON对象。
1. 单击或点按保存。

## 创建ContextHub存储 {#creating-a-contexthub-store}

创建Context Hub存储区以保留用户数据并根据需要访问数据。 ContextHub存储基于已注册的存储候选项。 创建存储时，需要存储候选注册到的storeType的值。 (请参阅 [创建自定义商店候选者](extending-contexthub.md#creating-custom-store-candidates).)

### 详细存储配置 {#detailed-store-configuration}

在配置存储时，“详细配置”属性允许您为特定于存储的属性提供值。 该值基于 `config` 商店的参数 `init` 函数。 因此，是否需要提供此值和值的格式取决于存储。

Detail Configuration属性的值为 `config` JSON格式的对象。

### 示例存储候选 {#sample-store-candidates}

AEM提供了以下存储候选项示例，您可以根据它们建立存储。

| 存储类型 | 描述 |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | 存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager检索区段 |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | 存储浏览器位置的纬度和经度。 |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | 为许多设备定义属性和功能，并检测当前客户端设备 |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | 存储当前用户的配置文件数据 |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | 存储有关客户端的信息，如设备信息、浏览器类型和窗口方向 |

1. 在Experience Manager边栏上，单击或点按工具>站点> ContextHub。
1. 单击或点按默认配置容器。
1. 单击或点按Contexthub配置
1. 要添加商店，请单击或点按“创建”图标，然后单击或点按ContextHub商店配置。

   ![ContextHub存储配置](assets/contexthub-store-configuration.png)

1. 提供基本配置属性的值，然后单击或点按下一步：

   * **配置标题：** 标识存储的标题
   * **存储类型：** 作为存储基础的存储候选项的storeType属性的值
   * **必需：** 选择
   * **已启用：** 选择以启用存储

1. （可选）要覆盖默认存储配置，请在Detail Configuration (JSON)框中输入JSON对象。
1. 单击或点按保存。

## 示例：使用JSONP服务  {#example-using-a-jsonp-service}

此示例说明如何在UI模块中配置存储区并显示数据。 在此示例中，jsontest.com站点的MD5服务用作存储的数据源。 该服务以JSON格式返回给定字符串的MD5哈希代码。

contexthub.generic-jsonp存储已配置为存储服务调用的数据 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. 该服务返回以下数据，这些数据显示在UI模块中：

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 创建contexthub.generic-jsonp存储 {#creating-a-contexthub-generic-jsonp-store}

Contexthub.generic-jsonp示例存储候选项允许您从返回JSON数据的JSONP服务或Web服务检索数据。 对于此存储候选项，请使用存储配置提供要使用的JSONP服务的详细信息。

此 [init](contexthub-api.md#init-name-config) 的功能 `ContextHub.Store.JSONPStore` JavaScript类定义 `config` 初始化此存储候选项的对象。 此 `config` 对象包含 `service` 包含有关JSONP服务的详细信息的对象。 要配置存储，您需要提供 `service` JSON格式的对象，作为详细信息配置属性的值。

要从jsontest.com站点的MD5服务中保存数据，请按照以下步骤操作： [创建ContextHub存储](#creating-a-contexthub-store) 使用以下属性：

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

将UI模块添加到ContextHub工具栏，以显示存储在示例md5存储中的数据。 在此示例中，contexthub.base模块用于生成以下UI模块：

![ContextHub MD5存储](assets/contexthub-md5-store.png)

请按照以下步骤进行操作： [添加UI模块](#adding-a-ui-module) 将UI模块添加到现有UI模式，例如示例角色UI模式。 对于UI模块，请使用以下属性值：

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

可以启用ContextHub的调试模式以进行故障排除。 调试模式可通过ContextHub配置或CRXDE启用。

### 通过配置 {#via-the-configuration}

编辑ContextHub的配置并选中选项 **调试**

1. 在边栏中，单击或点按 **工具>站点> ContextHub**
1. 单击或点按默认 **配置容器**
1. 选择 **ContextHub配置** ，然后单击或点按 **编辑选定的元素**
1. 单击或点按 **调试** ，然后单击或点按 **保存**

### 通过CRXDE {#via-crxde}

使用CRXDE Lite设置属性 `debug` 到 **true** 在：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<site>/settings/cloudsettings`

### 记录ContextHub的调试消息 {#logging-debug-messages-for-contexthub}

配置AdobeGranite ContextHub OSGi服务(PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`)来记录详细的调试消息，这些消息在开发时很有用。

要配置服务，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) 或使用存储库中的JCR节点：

* Web控制台：要记录调试消息，请选择Debug属性。
* JCR节点：要记录调试消息，请设置布尔值 `com.adobe.granite.contexthub.debug` 属性至 `true`.

### 静默模式 {#silent-mode}

静默模式会隐藏所有调试信息。 与可为每个ContextHub配置单独设置的普通调试选项不同，静默模式是一种全局设置，它优先于ContextHub配置级别上的任何调试设置。

这对于您根本不需要任何调试信息的发布实例非常有用。 由于它是全局设置，因此可通过OSGi启用。

1. 打开 **Adobe Experience Manager Web控制台配置** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **AdobeGranite ContextHub**
1. 单击配置 **AdobeGranite ContextHub** 编辑其属性
1. 选中选项 **静默模式** 并单击 **保存**

## 禁用ContextHub {#disabling-contexthub}

可以禁用ContextHub以阻止加载js/css和初始化。 可通过以下两个选项禁用ContextHub：

* 编辑ContextHub的配置并选中选项 **禁用Contexthub**

   1. 在边栏中，单击或点按 **工具>站点> ContextHub**
   1. 单击或点按默认 **配置容器**
   1. 选择 **ContextHub配置** ，然后单击或点按 **编辑选定的元素**
   1. 单击或点按 **禁用Contexthub** ，然后单击或点按 **保存**

或

* 使用CRXDE Lite设置属性 `disabled` 到 **true** 下 `/conf/global/settings/cloudsettings/<configName>/contexthub`
