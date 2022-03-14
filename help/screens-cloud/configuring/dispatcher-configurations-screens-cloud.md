---
title: Screens中的调度程序配置as a Cloud Service
description: 本页介绍Screens中的调度程序配置as a Cloud Service。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Screens中的调度程序配置as a Cloud Service {#dispatcher-configurations-screens-cloud}

本节介绍Screens的调度程序配置as a Cloud Service。

## 在Dispatcher for Screensas a Cloud Service部署中添加过滤器和缓存规则 {#deployment}

在Screensas a Cloud Service中，为发布实例在调度程序中允许以下过滤器和缓存规则。

### AEM Screens过滤器 {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### 缓存规则 {#cache-rules}

* 添加 `/statfileslevel "10"` to `/cache` 部分 `publish_farm.any`/.

   >[!NOTE]
   >此缓存规则支持从缓存域缓存多达10个级别，并在内容发布时使其失效，而不是使所有内容失效。 您可以根据内容结构的设置深度更改此级别。

* 将以下内容添加到 `/invalidate` 部分 `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 将以下规则添加到 `/rules` 部分 `/cache` 在publish_farm.any或 `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
        }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
