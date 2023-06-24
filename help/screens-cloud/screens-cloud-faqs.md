---
title: Screens as a Cloud Service 常见问题解答
description: 本页介绍Screensas a Cloud Service常见问题解答。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# Screens as a Cloud Service 常见问题解答 {#screens-cloud-faqs}

以下部分提供了与Screensas a Cloud Service项目相关的常见问题解答(FAQ)。

## 如果AEM Screens Player指向Screensas a Cloud Service时没有选择采用/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自定义clientlibs，我应该怎么做？

AEMas a Cloud Service会在每次部署时更改长缓存密钥。 修改内容时，AEM Screens会生成离线缓存，而不是在Cloud Manager运行部署时生成。 清单中的这些长缓存键无效，因此播放器无法下载 *clientlibs*.

使用 `longCacheKey="none"` 在您的 `clientlib` 文件夹会同时删除以下项的长缓存键： *clientlibs*.


## 如果离线清单未按预期包含所有资源，我应该怎么做？ {#offline-manifest}

使用以下方式生成脱机缓存 **bulk-offline-update-screens-service** 服务用户。 某些路径，不可由访问 `bulk-offline-update-screens-service`，导致离线清单中缺少内容。

在你的密码里， `ui.config or ui.apps`，在配置文件夹中创建包含以下内容的OSGi配置，并将文件名标题为 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 推荐哪些图像格式以在AEM Screensas a Cloud Service渠道中无缝呈现图像？{#screens-cloud-image-format}

建议在格式中使用图像 `.png` 和 `.jpeg` 在AEM Screensas a Cloud Service渠道中，获得最佳的数字标牌体验。
格式的图像 `*.tif` （标记图像文件格式）在AEM Screensas a Cloud Service中不受支持。 如果某个渠道具有此格式的图像，则在播放器端，不会渲染图像。

## 如果处于开发人员模式（在线）的渠道未在AEM Screens Player中呈现，我应该怎么做？{#screens-cloud-online-channel-blank-iframe}

Adobe建议您使用AEM Screens缓存功能。 但是，如果您必须在开发人员模式下运行渠道，并且AEM Screens Player显示一个空白屏幕，请检查播放器的开发人员工具并查找 `X-Frame-Options` 或 `frame-ancestors` 错误。 解决方法是将Dispatcher配置为允许内容在iFrame中运行。 通常，以下配置有效：

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## 注册码限制的用法是什么？

作为最佳实践，您可以限制注册码的使用。 如果注册码被盗用，但限制为100个注册，则攻击者最多只能注册该数字，但不能注册更多。 在创建注册代码并注册一些客户播放器后，您始终可以更新使用限制。 如果客户观察到特定注册码的异常注册活动，他们可以在调查时实时降低限制。 如果出现误报，他们可以增加该数量，而不会影响已注册的播放器。
