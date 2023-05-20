---
title: Screens中的Dispatcher設定as a Cloud Service
description: 本頁面說明Screensas a Cloud Service中的Dispatcher設定。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Screens中的Dispatcher設定as a Cloud Service {#dispatcher-configurations-screens-cloud}

本節說明Screensas a Cloud Service的Dispatcher設定。

## 在Dispatcher for Screensas a Cloud Service部署中新增篩選器和快取規則 {#deployment}

在Dispatcher中允許針對Screensas a Cloud Service中的發佈執行個體有下列篩選器和快取規則。

### AEM Screens篩選器 {#filters}

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

### 快取規則 {#cache-rules}

* 新增 `/statfileslevel "10"` 至 `/cache` 中的區段 `publish_farm.any`/.

   >[!NOTE]
   >此快取規則支援從快取docroot快取最多10個層級，並在內容發佈時讓內容失效而不是讓所有內容失效。 您可以根據內容結構的設定深度來變更此層級。

* 將下列專案新增至 `/invalidate` 中的區段 `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 將下列規則新增至 `/rules` 中的區段 `/cache` (在publish_farm.any中或包含在 `publish_farm.any`.

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
