---
title: Screens中的调度程序配置作为Cloud Service
description: 本页介绍Screens中的调度程序配置作为Cloud Service。
source-git-commit: b00856e1be8842c4e9fa6ed4ada9129926c73ef5
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Screens中的调度程序配置作为Cloud Service{#dispatcher-configurations-screens-cloud}

本节将介绍Screens的调度程序配置作为Cloud Service。

## Screens作为Cloud Service部署的调度程序配置 {#deployment}

在Screens中，为发布实例允许以下过滤器和缓存规则作为Cloud Service。

### 过滤器 {#filters}

## AEM Screens过滤器

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

## 缓存规则 {#cache-rules}

* 将`/statfileslevel "10"`添加到`publish_farm.any`/中的`/cache`部分。

   >[!NOTE]
   >这支持从缓存缓存中缓存多达10个级别，并在内容发布时使其失效，而不是使所有内容失效。 您可以根据内容结构的深度更改此级别。

* 在`publish_farm.any`的`/invalidate`部分添加以下内容。

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 将以下规则添加到publish_farm.any中`/cache`部分或`publish_farm.any`所包含文件中的`/rules`部分。

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
