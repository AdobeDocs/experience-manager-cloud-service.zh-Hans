---
title: CDN 性能仪表板
description: 了解Cloud Manager如何评估Content Delivery Network (CDN)性能以及您可以从功能板中学到什么。
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# CDN性能仪表板 {#cdn-performance}

了解Cloud Manager如何评估Content Delivery Network (CDN)性能以及您可以从功能板中学到什么。

## 概述 {#overview}

每个Cloud Manager项目都有一个CDN性能功能板。 此仪表板显示CDN性能的总体分数，以及趋势、警报和必要的改进建议。

![CDN性能仪表板](assets/cdn-performance-dashboard.png)

## 访问仪表板 {#accessing}

CDN功能板可在每个项目的概述页面上找到。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，单击要查看其CDN仪表板的程序。

   ![我的项目页面](assets/my-programs.png)

1. 在项目的&#x200B;**项目概述**&#x200B;页面上，向下滚动到&#x200B;**环境**&#x200B;和&#x200B;**管道**&#x200B;信息卡的下方以查看&#x200B;**性能**&#x200B;信息卡。

   ![性能](assets/cdn-performance-overview.png)

## 使用仪表板 {#using}

仪表板显示CDN性能的整体分数，以及趋势、警报和必要的改进建议。

![CDN性能仪表板](assets/cdn-performance-dashboard.png)

有关您的CDN性能的详细信息以及如何改进它的建议，请点按或单击&#x200B;**查看趋势**。

![性能趋势](assets/cdn-performance-trend.png)

点按或单击图表下方的&#x200B;**查看**&#x200B;以更改图表的时间范围。

有关如何提高CDN性能的建议，请选择&#x200B;**Recommendations**&#x200B;选项卡。

![CDN推荐](assets/cdn-performance-recommendations.png)

点按或单击列表中任何推荐旁边的V形符号，可查看有关要采取的改进步骤和问题原因的详细信息。

## 缓存命中定义 {#cache-hit}

缓存命中率是衡量缓存可成功填充的内容请求数，以及缓存接收的内容请求数的一个指标。 缓存命中率越高，CDN的执行效果就越好。

>[!TIP]
>
>Adobe建议用户以99%的缓存命中率为目标。

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **点击** — 从缓存中请求了数据，但找到了该数据。
* **未命中** — 正在从缓存中请求数据，但未找到该数据。
* **传递** — 从缓存中请求数据，无论如何，它都设置为不缓存此数据。
* **Other** — 来自缓存的与任何其他大小写不匹配的所有数据请求。

缓存量度每24小时更新一次。

>[!TIP]
>
>有关Cloud Manager和CDN如何与Dispatcher交互的更多详细信息，请参阅[AEM as a Cloud Service中的缓存](/help/implementing/dispatcher/caching.md)。
