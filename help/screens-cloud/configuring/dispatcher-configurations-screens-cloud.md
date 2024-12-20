---
title: Screens中的Dispatcher配置as a Cloud Service
description: 本页介绍了Screensas a Cloud Service中的Dispatcher配置。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Screens中的Dispatcher配置as a Cloud Service {#dispatcher-configurations-screens-cloud}

此部分介绍Screensas a Cloud Service的Dispatcher配置。

## 在Dispatcher中添加筛选器和缓存规则以用于Screensas a Cloud Service部署 {#deployment}

在Dispatcher中允许对Screensas a Cloud Service中的发布实例使用以下过滤器和缓存规则。

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

* 将`/statfileslevel "10"`添加到`publish_farm.any`/中的`/cache`分区。

  >[!NOTE]
  >此缓存规则支持从缓存docroot中缓存最多10个级别，并在发布内容时使无效，而不是使所有内容无效。 您可以根据内容结构的设置深度更改此级别。

* 将以下内容添加到`publish_farm.any`中的`/invalidate`分区。

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* 将以下规则添加到publish_farm.any中`/cache`的`/rules`部分或从`publish_farm.any`包含的文件中。

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
