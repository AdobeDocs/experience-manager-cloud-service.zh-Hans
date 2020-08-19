---
title: 内容审核测试-Cloud Services
description: 内容审核测试-Cloud Services
translation-type: tm+mt
source-git-commit: ce25ec1472dc349937fdbd5f7265d4295fe111e8
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# 内容审核测试 {#content-audit-testing}

内容审核是Cloud Manager Sites Production管道中的一项功能，该管道由Google的开放源代码工具Lighthouse提供支持。 此功能在所有Cloud Manager Production管道中都启用。

它可验证部署过程并有助于确保部署了更改：

1. 满足性能、辅助功能、最佳实践、SEO（搜索引擎优化）和PWA（渐进式Web应用程序）的基准标准。

1. 不要在这些维度中包含回归。

Cloud Manager中的内容审核可确保站点上的最终用户数字体验保持为最高标准。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否会引入退化，很有价值。

## 了解内容审核结果 {#understanding-content-audit-results}

内容审核通过“生产管道”执行页面提供聚合和详细的页面级测试结果。

* 聚合级别指标衡量已审核页面的平均得分。
* 还可以通过向下展开来获取各个页面级别的分数。
* 可以详细查看各个测试的结果，以及如何修正在内容审核过程中确定的任何问题的指导。
* 测试结果的历史记录将保留在Cloud Manager中，这样客户就可以查看在管道运行中引入的更改是否包含先前运行的任何回归。

### 聚合分数 {#aggregate-scores}

每种测试类型(性能、辅助功能、SEO、最佳实践和聚合)都有PWA级别得分。

聚合级别得分取得运行中包含的页面的平均得分。 聚合级别的更改表示当前运行中页面的平均分数与上次运行的平均分数相比，即使配置为包含的页面集合在两次运行之间发生更改也是如此。

“更改”量度的值可以是以下值之一：

* **正值** -自上次生产管道运行以来，在所选测试中页面已得到改进

* **负值** -自上次生产管道运行以来，页面在所选测试上出现倒退

* **无更改** -自上次运行生产管道以来，页面的得分相同

* **N/A** —— 没有可供比较的先前得分

   ![](/help/implementing/developing/introduction/assets/content-audit-test1.png)

### 页面级别得分 {#page-level-scores}

通过钻取任何测试，可以查看更详细的页面级别评分。 用户将能够查看特定测试的各个页面的得分情况以及与上次运行测试时的更改情况。

单击任何单个页面的详细信息将提供有关已评估页面元素的信息，并指导您在检测到改进机会时修复问题。 测试的细节和相关指导由Google Lighthouse提供。

![](/help/implementing/developing/introduction/assets/page-level-scores.png)

