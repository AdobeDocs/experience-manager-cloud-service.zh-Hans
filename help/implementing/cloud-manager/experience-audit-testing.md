---
title: 体验审核测试
description: 了解体验审核如何验证您的部署流程，并帮助确保部署的更改符合性能、辅助功能、最佳实践和SEO的基准标准。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 1a7a9ee78d09a9360922a63dfa315ef9d106209e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# 体验审核测试 {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="体验审核测试"
>abstract="了解体验审核如何验证您的部署流程，并帮助确保部署的更改符合性能、辅助功能、最佳实践和SEO的基准标准。"

了解体验审核如何验证您的部署流程，并帮助确保部署的更改符合性能、辅助功能、最佳实践和SEO的基准标准。

## 概述 {#overview}

体验审核是Cloud Manager Sites生产管道中提供的一项功能，可验证部署流程并帮助确保部署更改：

1. 符合性能、辅助功能、最佳实践、SEO（搜索引擎优化）和PWA（渐进式Web应用程序）的基准标准。

1. 不要引入回归。

Cloud Manager中的体验审核可确保最终用户在网站上的体验符合最高标准。

审核结果是信息性的，它允许部署管理器查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否引入回归参数非常有价值。

Experience Audit由Google Lighthouse提供支持，Lighthouse是Google的一款开源工具，在所有Cloud Manager生产管道中均已启用。

## 了解体验审核结果 {#understanding-experience-audit-results}

体验审核通过 [生产管道执行页面。](/help/implementing/cloud-manager/deploy-code.md)

* 聚合量度衡量经过审核的页面中的平均分数，这些分数是为了获得性能、辅助功能、最佳实践、SEO（搜索引擎优化）。
* 单个页面级别的得分也可通过向下钻取获得。
* 有关分数的详细信息，可查看各个测试的结果，以及有关如何修正已识别的任何问题的指导。
* 测试结果的历史记录将保留在Cloud Manager中，用于确定管道中引入的更改是否包含来自上次运行的任何回归。

### 总分 {#aggregate-scores}

聚合级别分数采用运行中包含的页面的平均分数。 聚合级别的更改表示当前运行中页面的平均分数与上次运行中得分的平均值，即使配置为包含的页面集合在两次运行之间发生了更改也是如此。

每种测试类型（如性能、辅助功能、SEO和最佳实践）都有一个汇总级别得分。

更改量度可以具有以下值之一。

* **正值**  — 自上次运行生产管道以来，所选测试的页面已得到改进。

* **负值**  — 自上次生产管道运行以来，页面在所选测试中出现了倒退。

* **无更改**  — 自上次运行生产管道以来，页面的得分相同。

* **不适用**  — 之前没有可供比较的得分。

![体验审核结果](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 页面级别得分 {#page-level-scores}

通过深入任何测试，可获得更详细的页面级别评分。 您可以查看各个页面对特定测试的得分情况，以及与上次测试运行相比的更改。

单击任意单个页面的详细信息可提供有关已评估页面元素的信息，并在检测到改进机会时提供修复问题的指导。

![页面级别得分](/help/implementing/cloud-manager/assets/exp-audit-2.png)
