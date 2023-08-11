---
title: 体验审核功能板
description: 了解体验审核如何验证您的部署过程，并通过清晰、信息丰富的仪表板界面帮助确保部署的更改符合性能、可访问性、最佳实践和SEO的基线标准。
source-git-commit: 7a8e6c3d226b02c65943629d0df196252218aa3c
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 22%

---


# 体验审核功能板 {#experience-audit-dashboard}


了解体验审核如何验证您的部署过程，并通过清晰、信息丰富的仪表板界面帮助确保部署的更改符合性能、可访问性、最佳实践和SEO的基线标准。

>[!NOTE]
>
>此功能仅适用于 [率先采用者计划。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>有关AEMas a Cloud Service的现有体验审核功能的详细信息，请参阅此文档 [体验审核测试。](/help/implementing/cloud-manager/experience-audit-testing.md)

## 概述 {#overview}

体验审核是 Cloud Manager Sites 生产管道中的现有功能，用于验证部署过程并帮助确保部署的更改：

1. 满足性能、可访问性、最佳实践、SEO（搜索引擎优化）和 PWA（渐进式 Web 应用程序）的基线标准。

1. 不要引入回归。

Cloud Manager 中的体验审核可确保最终用户在网站上的体验达到最高标准。

审核结果可提供丰富信息，允许部署管理员查看分数以及当前分数和以前分数之间的变化。 此细节对于确定当前部署中是否引入了回归非常有用。

体验审核由提供支持 [Google灯塔，](https://developer.chrome.com/docs/lighthouse/overview/) Google中的一种开源工具，已在所有Cloud Manager生产管道中启用。

>[!TIP]
>
>在[设置您的管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)时，您可以配置要包含在体验审核中的页面。

## 体验审核功能板 {#dashboard}

经验审计的结果载于 **暂存测试** 生产管道的阶段，通过 [生产管道执行页面。](/help/implementing/cloud-manager/deploy-code.md)

![管道中的仪表板](assets/dashboard.png)

体验审核提供汇总和详细的页面级测试结果，这些结果汇总在四个选项卡上：

* **[Insights](#insights)** 简要描述提高站点性能的可行建议。
* **[灯塔分数](#lighthouse)** 是此管道执行中部署的代码的Lighthouse得分摘要。
* **[页面](#pages)** 是专门配置以供分析的页面的性能摘要。
* **[问题](#issues)** 总结在此管道执行的代码中检测到的任何性能问题。

### 见解 {#insights}

此 **Insights** 选项卡简要说明提高站点性能的可行建议。

![见解](assets/insights.png)

点按或单击 **显示更多** 按钮以打开整个仪表板。

在 **见解和推荐** 部分，您会找到可操作推荐的详细列表，这些推荐具有明确的值指示符，与性能中可以预期的收益以及受影响的页面百分比相关联。 这让您能够轻松地为团队排列这些推荐的优先级。

![见解和推荐](assets/insights-recommendations.png)

要导航回生产管道执行页面，只需选择浏览器上的后退箭头。

### 灯塔分数 {#lighthouse}

此 **灯塔分数** 选项卡汇总了在此管道执行中部署的代码的Lighthouse分数。

![灯塔分数](assets/lighthouse.png)

点按或单击 **显示更多** 按钮以打开整个仪表板。

在 **灯塔分数** 部分，您可以找到各种分数的趋势视图。 选择 **性能**， **辅助功能**， **PWA**，或 **SEO** 以查看这些值的每月趋势视图。

![Lighthouse得分图](assets/lighthouse-scores.png)

请注意，图表上的每个点都是感兴趣的月份中所有部署的平均值。

要导航回生产管道执行页面，只需选择浏览器上的后退箭头。

### 页面 {#pages}

此 **页面** 选项卡汇总了专门配置为进行分析的页面的性能。

![“页面”选项卡](assets/pages.png)

点按或单击 **显示更多** 按钮以打开整个仪表板。

此 **页面** 部分提供了已测试的页面及其最新Lighthouse性能分数和细分的列表。

![页面查看](assets/pages-view.png)

在[设置您的管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)时，您可以配置要包含在体验审核中的页面。

要导航回生产管道执行页面，只需选择浏览器上的后退箭头。

### 问题 {#issues}

此 **问题** 选项卡总结在此管道执行的代码中检测到的任何性能问题。

![“问题”选项卡](assets/issues.png)

点按或单击 **显示更多** 按钮以打开整个仪表板。

在 **见解和推荐** 部分，您可以找到可操作推荐的更详细列表，这些推荐带有明确的值指示符，与性能中可以预期的收益以及受影响的页面百分比相关联。 这让您能够轻松地为团队排列这些推荐的优先级。

![见解和推荐](assets/insights-recommendations.png)

要导航回生产管道执行页面，只需选择浏览器上的后退箭头。

### 页面详细信息 {#page-detail}

如果您在的选项卡上点按或单击页面的链接， **体验审核** 管道执行页面选项卡的部分或 **页面** 查看特定页面的详细信息。

![页面数据](assets/page-data.png)

您可以看到各个页面对特定测试的评分以及与上一次测试运行相比的变化。

单击任何单个页面的详细信息，可以提供有关已评估页面元素的信息，以及在检测到改进机会时修复问题的指导。

要导航回生产管道执行页面，只需选择浏览器上的后退箭头。
