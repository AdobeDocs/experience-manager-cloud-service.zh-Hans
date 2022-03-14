---
title: Screens as a Cloud Service 常见问题解答
description: 本页介绍Screensas a Cloud Service常见问题解答。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Screens as a Cloud Service 常见问题解答 {#screens-cloud-faqs}

以下部分提供了与Screensas a Cloud Service项目相关的常见问题解答(FAQ)的答案。

## 如果指向Screens的AEM Screens播放器没有选取/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自定义客户端，我应该怎么做？

AEM as a Cloud Service会根据每个部署更改长缓存键值。 AEM Screens会在内容被修改时（而不是Cloud Manager运行部署时）生成离线缓存。 清单中的这些长缓存键无效，因此播放器无法下载这些键 *clientlibs*.

使用 `longCacheKey="none"` 在 `clientlib` 文件夹会完全删除这些长缓存键 *clientlibs*.


## 如果离线清单未包含预期的所有资源，我们应该怎么做？ {#offline-manifest}

脱机缓存是使用 **bulk-offline-update-screens-service** 服务用户。 某些路径，无法访问 `bulk-offline-update-screens-service`，导致离线清单中缺少内容。

在你的代码中， `ui.config or ui.apps`，请在配置文件夹中创建OSGi配置（包含以下内容），并将文件名称命名为 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

建议使用格式的图像 `.png` 和 `.jpeg` 在AEM Screensas a Cloud Service渠道中，提供最佳的数字标牌体验。
格式的图像 `*.tif` （标记图像文件格式）在AEM Screensas a Cloud Service中不受支持。 如果渠道具有此格式的图像，则在播放器侧，图像将不会呈现。

## 如果开发人员模式下的渠道（在线）未在AEM Screens播放器上呈现，我应该怎么做？{#screens-cloud-online-channel-blank-iframe}

建议使用AEM Screens缓存功能，但如果您需要在开发人员模式下运行渠道，并且AEM Screens播放器显示空白屏幕，请检查播放器的开发人员工具并查找 `X-Frame-Options` 或 `frame-ancestors` 错误。 解决方案是将调度程序配置为允许在iFrame中运行内容。 通常，以下配置可正常工作：

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 注册代码限制的用途是什么？

作为最佳实践，您可以限制注册代码的使用。 如果注册代码被攻破，但注册数量限制为100个，则攻击者只能注册到该号码，但注册数量不能超过该号码。 您始终可以在创建注册代码并且已注册客户的某些播放器后更新使用限制。 如果客户发现特定注册代码存在异常注册活动，则他们可以在调查时实时降低该限制，如果是虚警，则可以增加返回数量，而不会影响已注册的播放器。
