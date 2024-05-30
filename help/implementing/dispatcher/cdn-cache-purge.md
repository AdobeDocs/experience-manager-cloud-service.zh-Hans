---
title: 清除CDN缓存
description: 了解如何通过配置随后可在API调用中使用的清除API令牌，从AdobeCDN缓存中删除缓存的对象。
feature: Dispatcher
source-git-commit: 7224db99c29c90fb5e93ac07d7d501e2e9aaf74e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# 清除CDN缓存 {#cdn-purge-cache}

>[!NOTE]
>此功能尚未普遍可用。要加入率先采用者计划，请发送电子邮件至 `aemcs-cdn-config-adopter@adobe.com`.

清除会从AdobeCDN缓存中移除对象，从而导致将来的请求作为缓存缺失继续前往原点，而不是从缓存提供服务。
AEMas a Cloud Service允许您配置清除API令牌，然后可以在API调用中使用它。 阅读 <!--[Configuring CDN Credentials and Authentication article](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)--> 了解如何使用Cloud Manager配置管道身份验证指令配置此令牌。

有三个受支持的清除变体：

* [单个URL清除](#single-purge)  — 一次清除单个资源。
* [通过替代键清除](#surrogate-key-purge)  — 一次清除多个资源。
* [完全清除](#full-purge)  — 清除所有资源。

所有清除变体共享以下内容：

* 必须将HTTP方法设置为 `PURGE`.
* 该URL可以是与清除请求所针对的AEM服务关联的任何域。
* 此 `X-AEM-Purge-Key` 必须在HTTP标头中提供。

>[!CAUTION]
>清除CDN缓存（尤其是使用硬标志）将增加源位置的流量，并且在未正确执行时可能导致中断。

## 单个URL清除 {#single-purge}

您可以按如下方式一次清除单个资源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

如上面的示例所示，您可以 **（可选）** 指定CDN是否应执行 **硬** 清除（默认）或 **柔光** 清除缓存的对象。

默认硬清除会使得新请求立即无法访问内容，直到从源中检索内容为止。 软清除将内容标记为已过时，但仍会向客户端提供内容，因此客户端不需要等待内容从源中检索出来。

## 代理项清除 {#surrogate-key-purge}

替代键是用于清除一组内容的唯一标识符。 它们通过添加 `Surrogate-Key` 标头到响应。 可以在清除API调用中引用一个或多个代理键。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

此 `Surrogate-Key`(s)用空格分隔。 与单个URL清除类似，您可以配置硬清除或软清除。

## 完全清除 {#full-purge}

您可以按如下方式完全清除所有缓存的资源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

请注意 `X-AEM-Purge` 标头必须包含“all”值。

## 与Apache/Dispatcher层的交互 {#apache-layer}

如 [内容投放流程文章](/help/implementing/dispatcher/overview.md)时，如果缓存已过期，则CDN将从Apache/Dispatcher层检索内容。 这意味着在CDN上清除资源之前，您应确保在Dispatcher上也提供了内容的新版本。 有关更多详细信息，另请参阅 [Dispatcher缓存失效](/help/implementing/dispatcher/caching.md#disp).
