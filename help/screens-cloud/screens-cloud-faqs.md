---
title: Screens作为Cloud Service常见问题解答
description: 本页介绍Screens作为Cloud Service常见问题解答。
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Screens作为Cloud Service常见问题解答 {#screens-cloud-faqs}

以下部分提供了与Screens as a A Seens项目相关的常见问题解答(FAQ)的解答。

## 如果指向Screens作为Cloud Service的AEM Screens播放器没有选择/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自定义clientlibs，我该怎么做？

AEM as aCloud Service会根据每个部署更改长缓存键值。 AEM Screens会在内容被修改时（而不是Cloud Manager运行部署时）生成离线缓存。 清单中的这些长缓存键无效，因此播放器无法下载这些&#x200B;*clientlibs*。

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
