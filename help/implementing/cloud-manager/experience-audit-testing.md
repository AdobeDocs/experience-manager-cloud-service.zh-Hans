---
title: 体验审核测试-Cloud Services
description: 体验审核测试-Cloud Services
translation-type: tm+mt
source-git-commit: 28ba5412190560b21b27068832ba05cfff24c079
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# 体验审核测试 {#experience-audit-testing}

Experience Audit是Cloud Manager Sites Production管道中的一项功能，由Google Lighthouse提供支持，Google是一款开放源代码工具。 此功能在所有Cloud Manager Production管道中都启用。

它可验证部署过程并有助于确保部署了更改：

1. 满足性能、辅助功能、最佳实践、SEO（搜索引擎优化）和PWA（渐进式Web应用程序）的基准标准。

1. 不要在这些维度中包含回归。

Cloud Manager中的Experience Audit可确保站点上的最终用户数字体验保持为最高标准。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否会引入退化，很有价值。

## 了解体验审计结果 {#understanding-experience-audit-results}

体验审核通过生产管道执行页面提供聚合和详细的页面级测试结果。

* 聚合级别指标衡量已审核的页面中的平均分数，包括性能、辅助功能、最佳实践、SEO（搜索引擎优化）。
   >[!NOTE]
   >“Progressive Web App(PWA)”得分不包括在摘要得分中，只会显示在页面级报告详细信息屏幕中。
* 还可以通过向下展开来获取各个页面级别的分数。
* 可以详细查看各个测试的结果，以及如何修正在内容审核过程中确定的任何问题的指导。
* 测试结果的历史记录将保留在Cloud Manager中，这样客户就可以查看在管道运行中引入的更改是否包含先前运行的任何回归。

### 聚合分数 {#aggregate-scores}

每个测试类型（如性能、辅助功能、SEO和最佳实践）都有聚合级别得分。
>[!NOTE]
>“Progressive Web App(PWA)”得分不包括在摘要得分中，只会显示在页面级报告详细信息屏幕中。

聚合级别得分取得运行中包含的页面的平均得分。 聚合级别的更改表示当前运行中页面的平均分数与上次运行的平均分数相比，即使配置为包含的页面集合在两次运行之间发生更改也是如此。

“更改”量度的值可以是以下值之一：

* **正值** -自上次生产管道运行以来，在所选测试中页面已得到改进

* **负值** -自上次生产管道运行以来，页面在所选测试上出现倒退

* **无更改** -自上次运行生产管道以来，页面的得分相同

* **N/A** —— 没有可供比较的先前得分

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 页面级别得分 {#page-level-scores}

通过钻取任何测试，可以查看更详细的页面级别评分。 用户将能够查看特定测试的各个页面的得分情况以及与上次运行测试时的更改情况。

单击任何单个页面的详细信息将提供有关已评估页面元素的信息，并指导您在检测到改进机会时修复问题。 测试的细节和相关指导由Google Lighthouse提供。

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)

