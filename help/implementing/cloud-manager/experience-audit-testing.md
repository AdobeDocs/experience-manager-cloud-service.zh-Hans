---
title: 体验审核测试 — Cloud Services
description: 体验审核测试 — Cloud Services
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 体验审核测试{#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="体验审核测试"
>abstract="体验审核是Cloud Manager Sites Production Pipelines中提供的一项功能，由Google Lighthouse（Google的开源工具）提供支持。 此功能在所有Cloud Manager Production管道中都已启用。"

体验审核是Cloud Manager Sites Production Pipelines中提供的一项功能，由Google Lighthouse（Google的开源工具）提供支持。 此功能在所有Cloud Manager Production管道中都已启用。

它将验证部署流程并帮助确保部署了以下更改：

1. 符合性能、辅助功能、最佳实践、SEO（搜索引擎优化）和PWA（渐进式Web应用程序）的基准标准。

1. 请勿在这些维度中包含回归。

Cloud Manager中的体验审核可确保最终用户在网站上的数字体验可以按照最高标准进行维护。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否引入回归参数非常有价值。

## 了解体验审核结果{#understanding-experience-audit-results}

体验审核通过生产管道执行页面提供汇总的详细页面级测试结果。

* 汇总级别量度测量经过审核的页面中的平均分数，这些分数旨在获取性能、辅助功能、最佳实践、SEO（搜索引擎优化）。
   >[!NOTE]
   >渐进式Web应用程序(PWA)分数未包含在摘要分数中，并且只会显示在页面级别的报表详细信息屏幕中。
* 单个页面级别的得分也可通过向下钻取获得。
* 可以使用得分的详细信息来查看各个测试的结果，以及有关如何修正在体验审核期间发现的任何问题的指导。
* 测试结果的历史记录将保留在Cloud Manager中，以便客户能够查看在管道运行中引入的更改是否包含来自上次运行的任何回归。

### 总分{#aggregate-scores}

每种测试类型（如性能、辅助功能、SEO和最佳实践）都有一个汇总级别得分。
>[!NOTE]
>渐进式Web应用程序(PWA)分数未包含在摘要分数中，并且只会显示在页面级别的报表详细信息屏幕中。

聚合级别分数采用运行中包含的页面的平均分数。 聚合级别的更改表示当前运行中页面的平均分数与上次运行中得分的平均值，即使配置为包含的页面集合在两次运行之间发生了更改也是如此。

“更改值”量度可以是以下量度之一：

* **正值**  — 自上次生产管道运行以来，所选测试中的页面已得到改进

* **负值**  — 自上次生产管道运行以来，页面在所选测试中已回调

* **无更改**  — 自上次运行生产管道以来，页面的得分相同

* **不适用**  — 之前没有可供比较的得分

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 页面级别得分{#page-level-scores}

通过深入任何测试，可以查看更详细的页面级别评分。 用户将能够查看各个页面对特定测试的得分情况以及与上次运行测试时相比的变化。

单击任意单个页面的详细信息将提供有关已评估页面元素的信息，并在检测到改进机会时提供修复问题的指导。 Google Lighthouse提供了测试和相关指导的详细信息。

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
