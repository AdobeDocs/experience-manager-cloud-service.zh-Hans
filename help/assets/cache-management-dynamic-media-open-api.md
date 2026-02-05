---
title: 使用Open API的Dynamic Media中的缓存管理
description: 使用Open API的Dynamic Media中的缓存管理
role: User
source-git-commit: 89f21f96a741acbd6458c3777227548fbc89e525
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# 使用Open API的Dynamic Media中的缓存管理 {#cache-management-dynamic-media-open-apis}

高效的缓存管理对于提供高性能、可扩展且最新的数字资产至关重要。 在具有Open API的Dynamic Media中，缓存管理定义如何在交付管道的各个层存储、刷新和交付内容。 资产投放响应将缓存在多个层，以确保最佳性能和快速内容投放。

Dynamic Media中带有Open API的长时间缓存包括[CDN层缓存](#cdn-layer-caching)和[外部缓存控制（BYOCDN和浏览器缓存）](#byocdn-browser-caching)。

## CDN层缓存 {#cdn-layer-caching}

资源投放响应会在[Adobe Managed CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn)中缓存较长时间，以最大化性能并最大限度地减少源上的负载。 此缓存完全由Adobe管理，以确保为最终用户提供始终如一的高质量体验。 缓存持续时间专门针对性能进行优化，用户无法对其进行自定义以在所有客户中保持可靠性和高效的内容交付。

所有投放URL都会在边缘(Fastly)缓存较长时间，以确保最佳性能。 缓存的投放对象包括静态演绎版、视频、原始图像二进制文件和动态转换的图像，例如通过URL参数生成的调整大小或重新格式化的资产。<!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## 外部缓存控制（BYOCDN和浏览器缓存） {#byocdn-browser-caching}

对于下游缓存层，资源投放响应包含具有默认值`Cache-Control` `max-age`10分钟&#x200B;**的**&#x200B;标头。 这适用于自定义&#x200B;*自带CDN (BYOCDN)配置*、*最终用户浏览器*&#x200B;和任何&#x200B;*中间缓存代理*，从而确保在整个投放路径中实现一致的缓存控制。

### 自定义缓存控制标头 {#customizing-cache-control-headers}

增加缓存时间，使值的存留时间超过默认配置会增加提供过时内容的可能性，这可能会延迟内容更新在最终用户体验中的可见性。 如果需要修改特定用例的缓存控制行为，可以配置自定义CDN规则以调整响应标头。 这允许您根据自己的要求设置不同的缓存持续时间。 请参阅响应标头的[AEM自定义CDN规则](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic)。

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

有关缓存管理的其他帮助或问题，请联系[Adobe支持](https://helpx.adobe.com/in/contact.html)。

## 活动缓存失效 {#active-cache-invalidation}

每当更新、删除或修改资源（任何元数据更改）时，带Open API的Dynamic Media都会自动使Adobe Managed CDN上每个关联的投放URL失效。 这适用于使用虚ID或别名的URL，以及包含转换参数（如宽度、格式或质量）的任何URL。 这种事件驱动型失效机制可确保您的用户始终都能收到最新版本的资产，而无需手动干预。

### 手动清除缓存 {#manual-cache-purging}

当需要手动清除缓存的内容时，您可以使用AEM的缓存失效功能来执行该操作。 有关如何清除特定缓存URL的详细说明，请参阅[AEM CDN缓存无效](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge)。

## 常见问题解答{#faq-cache-management}

+++**缓存管理如何影响现有集成？**

资源URL保持不变，并且通过[`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean)从Adobe Managed CDN发送到浏览器（和其他下游中介）的缓存控制标头将持续10分钟，从而确保下游系统继续以最佳方式利用其缓存。

+++

+++**什么触发了缓存清除？**

更新、修改、存档或删除资产时，会自动触发缓存清除。

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **长时间缓存支持哪些所有资产类型？**

带事件驱动活动缓存失效的较长缓存适用于带Open API的Dynamic Media中的所有资产类型，而不管资产类型或格式如何。

+++

+++ **我是否可以为存储库选择退出长期缓存？**

您可以联系[Adobe支持](https://helpx.adobe.com/in/contact.html)，解释原因，Adobe将与您联系以进行讨论。

+++


>[!MORELIKETHIS]
>
>- [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>- [虚URL](/help/assets/vanity-urls.md)
