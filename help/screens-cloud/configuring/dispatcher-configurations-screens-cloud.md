---
title: Screens中的Dispatcher配置as a Cloud Service
description: 本页介绍了Screensas a Cloud Service中的Dispatcher配置。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Screens中的Dispatcher配置as a Cloud Service {#dispatcher-configurations-screens-cloud}

此部分介绍Screensas a Cloud Service的Dispatcher配置。

## 在Dispatcher for Screensas a Cloud Service部署中添加筛选器和缓存规则 {#deployment}

在Dispatcher中允许在Screensas a Cloud Service中为发布实例使用以下筛选器和缓存规则。

### AEM Screens筛选器 {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### 缓存规则 {#cache-rules}

* 添加 `/statfileslevel "10"` 到 `/cache` 中的部分 `publish_farm.any`/.

  >[!NOTE]
  >此缓存规则支持从缓存docroot中缓存最多10个级别，并且在发布内容时使内容无效，而不是使所有内容无效。 您可以根据内容结构的设置深度更改此级别。

* 将以下内容添加到 `/invalidate` 中的部分 `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* 将以下规则添加到 `/rules` 中的部分 `/cache` 在publish_farm.any中或从包含的文件中 `publish_farm.any`.

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
