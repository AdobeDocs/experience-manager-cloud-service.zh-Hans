---
title: CDN性能功能板
description: 了解Cloud Manager如何评估内容交付网络(CDN)性能，以及您可以从功能板中学到什么。
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---


# CDN性能功能板 {#cdn-performance}

了解Cloud Manager如何评估内容交付网络(CDN)性能，以及您可以从功能板中学到什么。

## 概述 {#overview}

每个Cloud Manager项目都有一个CDN性能仪表板。 此仪表板显示CDN性能的总体分数，以及趋势、警报和必要的改进建议。

![CDN性能仪表板](assets/cdn-performance-dashboard.png)

## 访问功能板 {#accessing}

CDN功能板可在每个项目的概述页面上找到。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 页面，点按或单击要查看其CDN功能板的项目。

   ![我的项目群页面](assets/my-programs.png)

1. 在 **项目概述** 页面，向下滚动到 **环境** 和 **管道** 卡片以查看 **性能** 卡片。

   ![性能](assets/cdn-performance-overview.png)

## 使用功能板 {#using}

仪表板显示CDN性能的整体分数，以及趋势、警报和必要的改进建议。

![CDN性能仪表板](assets/cdn-performance-dashboard.png)

有关您的CDN性能以及如何改进它的建议的详细信息，请点按或单击 **查看趋势**.

![性能趋势](assets/cdn-performance-trend.png)

点击或单击 **视图** 更改图表的时间范围。

有关如何提高CDN性能的建议，请选择 **Recommendations** 选项卡。

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

* **点击**  — 数据是从缓存中请求的，并且已找到。
* **小姐**  — 数据是从缓存中请求的，但是找不到。
* **通过**  — 数据是从缓存中请求的，无论如何，它都设置为不缓存此数据。
* **其他**  — 缓存中不符合任何其他大小写的所有数据请求。

缓存量度每24小时更新一次。

>[!TIP]
>
>有关Cloud Manager和CDN如何与Dispatcher交互的更多详细信息，请参阅文档 [AEMas a Cloud Service中的缓存。](/help/implementing/dispatcher/caching.md)
