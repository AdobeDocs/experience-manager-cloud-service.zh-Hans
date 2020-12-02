---
title: 内容投放流概述
description: 内容投放流概述
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# 内容交付流程 {#content-delivery}

当前页详细信息以Cloud Service形式发布AEM中的服务内容投放。 发布服务内容投放包括：

* CDN
* AEM dispatcher
* AEM发布

数据流如下：

1. URL将添加到浏览器中
1. 向DNS中映射到该域的CDN发出请求
1. 如果内容已在CDN上完全缓存，CDN会将其提供给浏览器
1. 如果内容未完全缓存，CDN将向调度程序发出（反向代理）调用
1. 如果内容已完全缓存在调度程序上，调度程序会将其提供给CDN
1. 如果内容未完全缓存，调度程序将调用（反向代理）AEM发布
1. 内容由浏览器呈现，浏览器也可缓存它，具体取决于标题

默认情况下，内容类型HTML/文本设置为在调度程序层300秒（5分钟）后过期，该阈值是调度程序缓存和CDN所遵循的阈值。 在发布服务的重新部署期间，将清除调度程序缓存，然后在新发布节点接受通信之前预热。

以下各节提供有关内容投放（包括CDN配置和缓存）的更详细信息。

有关从作者服务复制到发布服务的信息，请在[此处](/help/operations/replication.md)获取。
