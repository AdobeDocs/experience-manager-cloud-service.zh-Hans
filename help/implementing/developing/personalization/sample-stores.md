---
title: 示例ContextHub存储候选项
description: ContextHub提供了几个可在解决方案中使用的示例商店候选项
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 示例ContextHub存储候选项 {#sample-contexthub-store-candidates}

ContextHub提供了几个可在解决方案中使用的示例商店候选项。 为每个示例提供了以下信息：

* 在何处查找源代码，以便打开它进行学习。
* 如何配置您从候选商店创建的商店。
* 存储数据的结构方式，以便您能够访问它。

>[!WARNING]
>
>示例存储候选项作为参考配置提供，可帮助您为项目构建自己的专用配置。 请勿直接使用它们。

## aem.segmentation示例存储候选项 {#aem-segmentation-sample-store-candidate}

存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager检索区段。

### 源位置 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基本实施 {#base-implementation-segmentation}

aem.segmentation存储候选扩展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 配置 {#configuration-segmentation}

当您创建 `aem.segmentation` 存储，您无需提供详细配置。 默认配置指定ContextHub区段定义的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation示例存储候选项 {#contexthub-geolocation-sample-store-candidate}

此 `contexthub.geolocation` 示例存储候选项使用Google映射获取和存储有关客户端位置的信息。

### 源位置 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基本实施 {#base-implementation-geolocation}

此 `contexthub.geolocation` 存储候选扩展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 配置 {#configuration-geolocation}

默认配置指定有关Google服务以及初始纬度和经度坐标的信息。

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### 数据项 {#data-items-geolocation}

该存储使用与以下示例类似的数据树：

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中引入的安全策略要求所有与地理位置相关的调用都通过安全连接进行。 因此，如果AEM也通过https运行，则AEM强制对地理位置API调用使用https。 否则，会使用http来遵守相同来源的策略。
>
>请参阅 [此Google博客帖子](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) 以了解有关Chrome中更改的更多详细信息。

## contexthub.surferinfo示例存储候选项 {#contexthub-surferinfo-sample-store-candidate}

存储有关当前客户端环境的信息，如设备、窗口、浏览器、日期和时间。

### 源位置 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基本实施 {#base-implementation-surferinfo}

此 `contexthub.surferinfo` 存储候选扩展 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### 配置 {#configuration-surferinfo}

默认配置继承自 `ContextHub.Store.PersistedStore`.

### 数据项 {#data-items-surferinfo}

使用此候选商店的存储区具有类似于以下示例的数据树：

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators示例存储候选项 {#granite-emulators-sample-store-candidate}

此 `granite.emulators` 示例存储候选项存储有关客户端设备的信息。

### 源位置 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基本实施 {#base-implementation-emulators}

此 `granite.emulators` 存储候选扩展 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### 配置 {#configuration-emulators}

默认配置包括一个名为的数组 `defaultEmulators` 其中包含有关不同设备的信息。 在创建存储时，根据需要在详细配置属性中提供不同的设备配置文件，使用的格式如下例所示：

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### 数据项 {#data-items-emulators}

存储数据树类似于以下示例：

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile示例存储候选项 {#granite-profile-sample-store-candidate}

存储有关当前用户的信息。

### 源位置 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基本实施 {#base-implementation-profile}

此 `granite.profile` 存储候选扩展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 配置 {#configuration-profile}

使用以下默认配置。 您不应更改此配置。

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### 数据项 {#data-items-profile}

使用此候选商店的存储区具有类似于以下示例的数据树：

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
