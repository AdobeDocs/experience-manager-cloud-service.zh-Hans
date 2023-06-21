---
title: 内容交付流程概述
description: 内容交付流程概述
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 48%

---

# 内容交付流程 {#content-delivery}

当前页面详述了将 AEM as a Cloud Service 中的发布服务内容交付。发布服务内容交付包括：

* CDN
* AEM调度程序
* AEM发布者

数据流如下所示：

1. 在浏览器中添加 URL
1. 向 CDN 发出的请求已在 DNS 中映射到该域
1. 如果内容已在 CDN 上完全缓存，则 CDN 会将内容提供给浏览器
1. 如果内容未完全缓存，则CDN会向Dispatcher发出调用（反向代理）
1. 如果在Dispatcher上完全缓存了内容，则Dispatcher会将其提供给CDN
1. 如果内容未完全缓存，则Dispatcher会调用（反向代理）AEM发布
1. 内容由浏览器呈现，同时浏览器也可以缓存内容，具体取决于标头

默认情况下，内容类型HTML/文本设置为在Dispatcher层的300秒（5分钟）后过期，Dispatcher缓存和CDN都遵守此阈值。 在重新部署发布服务期间，先清除Dispatcher缓存，然后在新发布节点接受流量之前预热缓存。

以下部分提供了有关内容交付的更多详细信息：
* [CDN 配置](/help/implementing/dispatcher/cdn.md)
* [缓存](/help/implementing/dispatcher/caching.md)


[此处](/help/operations/replication.md)提供了有关从创作服务到发布服务的复制的信息。
