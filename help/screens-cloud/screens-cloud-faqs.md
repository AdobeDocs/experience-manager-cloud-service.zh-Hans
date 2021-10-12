---
title: Screensas a Cloud Service常见问题解答
description: 本页介绍屏幕as a Cloud Service常见问题解答。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Screensas a Cloud Service常见问题解答 {#screens-cloud-faqs}

以下部分提供了与Screensas a Cloud Service项目相关的常见问题解答(FAQ)的答案。

## 如果指向Screens的AEM Screens播放器没有选取/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自定义clientlib，我该怎么做？

AEM as a Cloud Service会根据每个部署更改长缓存键值。 AEM Screens会在内容被修改时（而不是Cloud Manager运行部署时）生成离线缓存。 清单中的这些长缓存键无效，因此播放器无法下载这些&#x200B;*clientlibs*。

在`clientlib`文件夹中使用`longCacheKey="none"`会完全删除这些&#x200B;*clientlibs*&#x200B;的长缓存键。


## 如果离线清单未包含预期的所有资源，我们应该怎么做？ {#offline-manifest}

离线缓存是使用&#x200B;**bulk-offline-update-screens-service**&#x200B;服务用户生成的。 某些路径（无法`bulk-offline-update-screens-service`访问）会导致离线清单中缺少内容。

在您的代码中，即`ui.config or ui.apps`，在配置文件夹中创建OSGi配置，并包含以下内容，并将文件名称命名为`org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 在AEM Screensas a Cloud Service渠道中，建议使用哪些图像格式来无缝呈现图像？{#screens-cloud-image-format}

建议在AEM Screensas a Cloud Service渠道中使用格式为`.png`和`.jpeg`的图像，以获得最佳的数字标牌体验。
格式为`*.tif`（标记图像文件格式）的图像在AEM Screensas a Cloud Service中不受支持。 如果渠道具有此格式的图像，则在播放器侧，图像将不会呈现。