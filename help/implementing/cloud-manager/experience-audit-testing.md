---
title: 体验审核测试 — Cloud Services
description: 体验审核测试 — Cloud Services
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 体验审核测试{#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Experience Audit Testing"
>abstract="Experience Audit是Cloud Manager Sites Production管道中的一项功能，由Google的开放源代码工具Google Lighthouse提供支持。 此功能在所有Cloud Manager Production管道中都启用。"

Experience Audit是Cloud Manager Sites Production管道中的一项功能，由Google的开放源代码工具Google Lighthouse提供支持。 此功能在所有Cloud Manager Production管道中都启用。

它可验证部署过程并有助于确保部署了以下更改：

1. 符合性能、辅助功能、最佳实践、SEO（搜索引擎优化）和PWA（渐进式Web应用程序）的基准标准。

1. 不要将回归包含在这些维度中。

Cloud Manager中的Experience Audit可确保站点上的最终用户数字体验保持为最高标准。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 这一洞察对于确定当前部署中是否引入回归很有价值。

## 了解体验审计结果{#understanding-experience-audit-results}

Experience Audit通过“生产管道”执行页提供聚合和详细的页面级测试结果。

* 聚合级别量度衡量已审核的页面中的平均分数，这些页面包括性能、辅助功能、最佳实践、SEO（搜索引擎优化）。
   >[!NOTE]
   >“Progressive Web App(PWA)”得分未包含在摘要得分中，并且只会显示在页面级别报告详细信息屏幕中。
* 您还可以通过向下钻取来获取各个页面级别的分数。
* 可以查看各个测试的结果，并了解如何修正在体验审核过程中发现的任何问题。
* 测试结果的历史记录将保留在Cloud Manager中，以便客户能够查看在管道运行中引入的更改是否包含上次运行的任何回归。

### 聚合分数{#aggregate-scores}

每种测试类型（如性能、辅助功能、SEO和最佳实践）都有聚合级别得分。
>[!NOTE]
>“Progressive Web App(PWA)”得分未包含在摘要得分中，并且只会显示在页面级别报告详细信息屏幕中。

聚合级别得分取的是运行中包含的页面的平均得分。 聚合级别的更改表示当前运行中页面的平均分数与上次运行的平均分数相比，即使配置为包含的页面集合在运行之间发生更改也是如此。

“更改”量度的值可以是以下值之一：

* **正值**  — 自上次生产管道运行以来，页面在所选测试中有所改进

* **负值**  — 自上次生产管道运行以来，页面在所选测试上出现倒退

* **无更改**  — 自上次运行生产管道以来，页面的得分相同

* **N/A**  — 没有可用于比较的先前得分

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 页级得分{#page-level-scores}

通过钻取任何测试，可以查看更详细的页面级别评分。 用户将能够查看各个页面对特定测试的得分情况以及与上次运行测试时相比的变化。

单击任何单个页面的详细信息将提供有关已评估页面元素的信息，并指导您在检测到改进机会时修复问题。 测试的细节和相关指导由Google Lighthouse提供。

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
