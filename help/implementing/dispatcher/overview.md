---
title: 内容交付流程概述
description: 详细了解内容交付数据流以及如何发布内容
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: d58055cd0ed2451b5e8063fbb4e7269885d0787c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 93%

---

# 内容交付流程 {#content-delivery}

当前页面详述了将 AEM as a Cloud Service 中的发布服务内容交付。发布服务内容交付包括：

* CDN
* AEM Dispatcher
* AEM 发布者

数据流如下所示：

1. 在浏览器中添加 URL
1. 向 CDN 发出的请求已在 DNS 中映射到该域
1. 如果内容已在 CDN 上完全缓存，则 CDN 会将内容提供给浏览器
1. 如果内容未完全缓存，则 CDN 会调用（反向代理）Dispatcher
1. 如果内容已在 Dispatcher 上完全缓存，则 Dispatcher 会将内容提供给 CDN
1. 如果内容未完全缓存，则 Dispatcher 会调用（反向代理）AEM 发布功能
1. 内容由浏览器呈现，同时浏览器也可以缓存内容，具体取决于标头

默认情况下，内容类型 HTML/文本在 Dispatcher 层上设置为 300 秒（5 分钟）后过期，这是 Dispatcher 缓存和 CDN 都遵守的阈值。在重新部署发布服务期间，Dispatcher 缓存将被清除，并且随后会在新的发布节点接受流量之前进行预热。

以下部分提供了有关内容交付的更多详细信息：
* [CDN 配置](/help/implementing/dispatcher/cdn.md)
* [缓存](/help/implementing/dispatcher/caching.md)

有关从创作服务复制到发布服务的信息，请参阅[复制](/help/operations/replication.md)。
