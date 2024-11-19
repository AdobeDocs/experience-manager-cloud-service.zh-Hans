---
title: 清除 CDN 缓存
description: 了解如何通过配置随后可在API调用中使用的清除API令牌，从AdobeCDN缓存中删除缓存的对象。
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: e5e0606c83f144f92f9ae57e5380a30389e8df1b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# 清除 CDN 缓存 {#cdn-purge-cache}

清除会从AdobeCDN缓存中移除对象，从而导致将来的请求作为缓存缺失继续前往原点，而不是从缓存提供服务。
AEM as a Cloud Service允许您配置清除API令牌，然后将其用于清除API调用。 阅读[配置CDN凭据和身份验证](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)以了解如何使用Cloud Manager配置管道身份验证指令配置此令牌。

有三个受支持的清除变体：

* [单个URL清除](#single-purge) — 一次清除单个资源。
* [按代理项清除](#surrogate-key-purge) — 一次清除多个资源。
* [完全清除](#full-purge) — 清除所有资源。

所有清除变体共享以下内容：

* HTTP方法必须设置为`PURGE`。
* 该URL可以是与清除请求所针对的AEM服务关联的任何域。
* 必须在HTTP标头中提供`X-AEM-Purge-Key`。

>[!CAUTION]
>清除CDN缓存（尤其是使用硬标志）将增加源位置的流量，并且在未正确执行时可能导致中断。

您可以引用[教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)，该教程侧重于配置清除密钥和执行CDN缓存清除。

## 单个URL清除 {#single-purge}

您可以按如下方式一次清除单个资源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

如上面的示例所示，您可以&#x200B;**可选**&#x200B;指定CDN是否应对缓存的对象执行&#x200B;**硬**&#x200B;清除（默认）或&#x200B;**软**&#x200B;清除。

默认硬清除会使得新请求立即无法访问内容，直到从源中检索内容为止。 软清除将内容标记为已过时，但仍会向客户端提供内容，因此客户端不需要等待内容从源中检索出来。

## 代理项清除 {#surrogate-key-purge}

替代键是用于清除一组内容的唯一标识符。 它们通过将`Surrogate-Key`标头添加到响应来应用于内容。 可以在清除API调用中引用一个或多个代理键。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

`Surrogate-Key`用空格分隔。 与单个URL清除类似，您可以配置硬清除或软清除。

## 完全清除 {#full-purge}

您可以按如下方式完全清除所有缓存的资源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

请注意，`X-AEM-Purge`标头必须包含“all”值。

## 与客户管理的CDN交互

如果是[客户管理的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)，还需要提供`X-Forwarded-Host`和`X-AEM-Edge-Key`：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Edge-Key: <my_edge_key>' \
-H 'X-Forwarded-Host: <my_forwarded_domain>'
```


## 与Apache/Dispatcher层的交互 {#apache-layer}

如[内容交付流程](/help/implementing/dispatcher/overview.md)中所述，如果缓存已过期，则CDN将从Apache/Dispatcher层检索内容。 这意味着在CDN上清除资源之前，您应确保在Dispatcher上也提供了内容的新版本。 有关详细信息，另请参阅[Dispatcher缓存无效](/help/implementing/dispatcher/caching.md#disp)。
