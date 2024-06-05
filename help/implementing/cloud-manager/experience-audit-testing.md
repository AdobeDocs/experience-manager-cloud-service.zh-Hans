---
title: 体验审核测试
description: 了解体验审核如何验证您的部署过程，并帮助确保部署的更改符合性能、可访问性、最佳实践和 SEO 的基线标准。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 58%

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

Cloud Manager中的体验审核可确保用户在站点上的体验达到最高标准。

审核结果可提供丰富信息，允许部署管理员查看分数以及当前分数和以前分数之间的变化。此细节对于确定当前部署中是否引入了回归非常有用。

体验审核由Google Lighthouse提供支持，这是Google的开源工具。

>[!INFO]
>
>自 2023 年 8 月 31 日起生效，体验审核将转变为展示特定于移动平台的结果。移动性能量度通常注册的比桌面性能低，因此您应该预计在此更改后报告的性能会发生变化。

## 可用性 {#availability}

体验审核适用于Cloud Manager：

* 默认情况下，站点生产管道。
* 前端开发管道（可选）。

请参阅 [配置部分](#configuration) 有关如何为可选环境配置审核的更多信息。

## 配置 {#configuration}

默认情况下，生产管道可以使用体验审核。 可以选择为前端开发管道启用它。 在所有情况下，您需要定义在管道执行期间评估哪些内容路径。

在设置管道时，您可以配置体验审核中包含的页面。

1. 根据要配置的管道类型，按照以下说明进行操作：

   * 添加新 [生产管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 如果您希望定义要由审核评估的路径。
   * 添加新 [非生产管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 如果您希望在前端管道或开发全栈管道上启用审核。
   * 或者，您可以 [编辑现有管道，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) 并更新现有选项。

1. 如果要添加或编辑要使用体验审核的非生产管道，则必须选择 **体验审核** 上的复选框 **源代码** 选项卡。

   ![启用体验审核](assets/experience-audit-enable.jpg)

   * 这仅对于非生产管道是必需的。
   * 此 **体验审核** 选项卡。

1. 对于生产管道和非生产管道，您都可以定义应包含在上的体验审核中的路径 **体验审核** 选项卡。

   * 页面路径必须以开头 `/` 和相对于您的网站。
   * 例如，如果您的网站为 `wknd.site` 并希望 `https://wknd.site/us/en/about-us.html` 在体验审核中，输入路径 `/us/en/about-us.html`.

   ![定义体验审核路径](assets/experience-audit-add-page.png)

1. 点击或单击 **添加页面** 路径将自动填写您的环境地址，并添加到路径表中。

   ![保存表的路径](assets/experience-audit-page-added.png)

1. 重复前两步，根据需要继续添加路径。

   * 最多可以添加 25 条路径。
   * 如果您未定义任何路径，则默认情况下，网站主页会包含在体验审核中。

1. 单击&#x200B;**保存**&#x200B;以保存管道。

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

* **正值**  — 自上次生产管道运行以来，所选测试的页面有所改进。

* **负值**  — 自上次生产管道运行以来，页面已在所选测试上回归。

* **无更改**  — 自上次生产管道运行以来，页面得分相同。

* **不适用** – 没有可供比较的先前分数。

![了解体验审核结果](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### 页面级别分数 {#page-level-scores}

通过深入到任何测试中，都可以获得更详细的页面级别评分。您可以看到各个页面对特定测试的评分以及与上一次测试运行相比的变化。

单击任何单个页面的详细信息，可以提供有关已评估页面元素的信息，以及在检测到改进机会时修复问题的指导。

![页面级别分数](/help/implementing/cloud-manager/assets/exp-audit-2.png)
