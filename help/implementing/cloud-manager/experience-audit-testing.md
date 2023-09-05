---
title: 体验审核测试
description: 了解体验审核如何验证您的部署过程，并帮助确保部署的更改符合性能、可访问性、最佳实践和 SEO 的基线标准。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 9f305e1127957fdba6dae978da4ac5fce4d3a776
workflow-type: ht
source-wordcount: '588'
ht-degree: 100%

---


# 体验审核测试 {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="体验审核测试"
>abstract="了解体验审核如何验证您的部署过程，并帮助确保部署的更改符合性能、可访问性、最佳实践和 SEO 的基线标准。"

了解体验审核如何验证您的部署过程，并帮助确保部署的更改符合性能、可访问性、最佳实践和 SEO 的基线标准。

## 概述 {#overview}

体验审核是 Cloud Manager Sites 生产管道中的现有功能，用于验证部署过程并帮助确保部署的更改：

1. 满足性能、可访问性、最佳实践、SEO（搜索引擎优化）和 PWA（渐进式 Web 应用程序）的基线标准。

1. 不要引入回归。

Cloud Manager 中的体验审核可确保最终用户在网站上的体验达到最高标准。

审核结果可提供丰富信息，允许部署管理员查看分数以及当前分数和以前分数之间的变化。此细节对于确定当前部署中是否引入了回归非常有用。

体验审核由 Google Lighthouse 提供支持，这是 Google 的开源工具，可在所有 Cloud Manager 生产管道中使用。

>[!INFO]
>
>自 2023 年 8 月 31 日起生效，体验审核将转变为展示特定于移动平台的结果。请注意，移动设备的性能指标通常低于桌面设备的性能指标，因此，预计此更改后的报告性能会发生变化。

>[!TIP]
>
>在[设置您的管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)时，您可以配置要包含在体验审核中的页面。

## 了解体验审核结果 {#understanding-experience-audit-results}

体验审核通过[生产管道执行页面提供聚合和详细的页面级测试结果。](/help/implementing/cloud-manager/deploy-code.md)

* 聚合量度衡量了页面的平均分数，这些页面的性能、可访问性、最佳实践、SEO（搜索引擎优化）都经过了审核。
* 还可以通过深入分析获得单个页面级别的分数。
* 分数的详细信息可用于查看各个测试的结果，以及作为纠正所发现问题的指导。
* 测试结果的历史记录将保存在 Cloud Manager 中，可确定管道中引入的更改是否包含上一次运行的任何回归。

### 总分 {#aggregate-scores}

汇总分数采用运行中包含的页面的平均分数。 汇总分数的变化表示当前运行中页面的平均分数与上次运行的平均分数相比的平均分数，即使配置为包含的页面集合在两次运行之间发生了变化。

每个测试类型如性能、可访问性、SEO 和最佳实践，都有一个汇总分数。

变化量度可以具有以下值之一。

* **正值** – 自上次生产管道运行以来，所选测试的页面有所改进。

* **负值** – 自上次生产管道运行以来，页面已在所选测试上回归。

* **无变化** – 自上次生产管道运行以来，页面得分相同。

* **不适用** – 没有可供比较的先前分数。

![了解体验审核结果](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### 页面级别分数 {#page-level-scores}

通过深入到任何测试中，都可以获得更详细的页面级别评分。您可以看到各个页面对特定测试的评分以及与上一次测试运行相比的变化。

单击任何单个页面的详细信息，可以提供有关已评估页面元素的信息，以及在检测到改进机会时修复问题的指导。

![页面级别分数](/help/implementing/cloud-manager/assets/exp-audit-2.png)
