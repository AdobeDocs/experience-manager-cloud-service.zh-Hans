---
title: 内容交付流程概述
description: 内容交付流程概述
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# 内容交付流程 {#content-delivery}

当前页面详细信息在AEMas a Cloud Service中发布服务内容交付。 发布服务内容交付包括：

* CDN
* AEM dispatcher
* AEM发布

数据流如下所示：

1. 该URL将添加到浏览器中
1. 向DNS中映射到该域的CDN发出的请求
1. 如果内容已完全缓存在CDN上，则CDN会将其提供给浏览器
1. 如果内容未完全缓存，CDN会向调度程序发出调用（反向代理）请求
1. 如果内容已完全缓存在Dispatcher上，则Dispatcher会将其提供给CDN
1. 如果内容未完全缓存，则调度程序将调用out（反向代理）到AEM发布
1. 内容由浏览器呈现，浏览器也可能会缓存该内容，具体取决于标头

默认情况下，内容类型HTML/文本设置为在调度程序层的300秒（5分钟）后过期，调度程序缓存和CDN均遵循该阈值。 在重新部署发布服务期间，将清除调度程序缓存，然后在新发布节点接受流量之前对其进行热化。

以下各节提供了有关内容交付（包括CDN配置和缓存）的更多详细信息。

有关从创作服务复制到发布服务的信息可用 [此处](/help/operations/replication.md).
