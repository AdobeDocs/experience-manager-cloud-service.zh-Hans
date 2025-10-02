---
title: 体验审核仪表板
description: 了解体验审核如何验证您的部署过程，确保更改符合性能、可访问性、最佳实践和SEO的基线标准。 它提供了一个清晰且信息丰富的仪表板界面来跟踪这些指标。
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---


# 体验审核功能板 {#experience-audit-dashboard}

<!-- Engineer architect over this feature was Bogdan Anton; scrum master Alexandru Nica -->

了解体验审核如何验证您的部署过程，确保更改符合性能、可访问性、最佳实践和SEO（搜索引擎优化）的基线标准。 它提供了一个清晰且信息丰富的仪表板界面来跟踪这些指标。

## 概述 {#overview}

体验审核可验证部署过程并帮助确保部署更改：

1. 满足性能、可访问性、最佳实践和SEO的基线标准。
1. 不要引入回归。

Cloud Manager中的体验审核可确保用户在该网站上的体验达到最高标准。

审核结果可提供丰富信息，允许部署管理员查看分数以及当前分数和以前分数之间的变化。此细节对于确定当前部署中是否引入了回归非常有用。

体验审核由[Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/)提供支持，这是Google的开源工具，可在所有Cloud Manager生产管道中启用。

## 可用性 {#availability}

体验审核适用于Cloud Manager：

* （默认）站点生产管道。
* （可选）开发全栈管道。
* （可选）开发前端管道。

有关如何为可选环境配置审核的更多信息，请参阅[配置部分](#configuration)。

审核作为管道的一部分运行。 审核也可以[在管道外部按需运行](#on-demand)。

## 配置 {#configuration}

默认情况下，生产管道可以使用体验审核。 可以选择启用它来开发全栈管道和前端管道。 在所有情况下，您需要定义在管道执行期间评估哪些内容路径。

1. 根据要配置的管道类型，执行以下操作之一：

   * [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)以定义希望审核评估的路径。
   * [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)（如果要在前端或开发全栈管道上启用审核）。
   * [编辑现有管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，并更新现有选项。

1. 要在添加或编辑非生产管道时使用体验审核，请选中&#x200B;**体验审核**&#x200B;复选框。 您可以在&#x200B;**Source代码**&#x200B;选项卡中找到此选项。

   ![正在启用体验审核](/help/implementing/cloud-manager/reports/assets/experience-audit-enable.jpg)

   * 仅对于非生产管道是必需的。
   * 选中该复选框后，将显示&#x200B;**体验审核**&#x200B;选项卡。

1. 对于生产和非生产管道，您定义应包含在&#x200B;**体验审核**&#x200B;选项卡上的体验审核中的路径。

   * 页面路径必须以`/`开头，并且相对于您的网站。
   * 例如，如果您的网站为`wknd.site`，并且希望在体验审核中包含`https://wknd.site/us/en/about-us.html`，请输入路径`/us/en/about-us.html`。

   ![定义体验审核路径](/help/implementing/cloud-manager/reports/assets/experience-audit-add-page.png)

1. 单击&#x200B;**添加页面**，路径会自动填写您的环境地址，并添加到路径表中。

   ![保存表的路径](/help/implementing/cloud-manager/reports/assets/experience-audit-page-added.png)

1. 重复前两步，根据需要继续添加路径。

   * 最多可以添加 25 条路径。
   * 如果您未定义任何路径，则默认情况下，网站主页会包含在体验审核中。

1. 单击&#x200B;**保存**。

## 体验审核结果 {#results}

体验审核的结果在通过&#x200B;**生产管道执行页面**&#x200B;的生产管道的[阶段测试](/help/implementing/cloud-manager/deploy-code.md)阶段中显示。

![管道中的仪表板](/help/implementing/cloud-manager/reports/assets/experience-audit-dashboard.png)

体验审核提供[配置的页面](#configuration)的Google Lighthouse得分中位数以及与上一次扫描的得分差异。

从管道的&#x200B;**阶段测试**&#x200B;阶段的此摘要视图中，您有两个选项：

* **[查看最慢的页面](#view-slowest-pages)**
* **[查看完整报告](#view-full-report)**

您可以通过单击Cloud Manager仪表板中的&#x200B;**报告**&#x200B;选项卡来访问完整的审核结果。 除了管道运行详细信息中显示的摘要之外，您还可以直接查看[完整报告](#view-full-report)。

>[!TIP]
>
>以下部分介绍了如何查看体验审核的结果。
>
>* 若要了解有关审核工作方式的更多详细信息，请参阅[体验审核评估详细信息](#details)。
>* 要了解如何按需运行体验审核，请参阅[按需审核报告](#on-demand)。
>* 如果您遇到审核问题，请参阅[体验审核遇到问题](#issues)。

### 查看最慢的页面 {#view-slowest-pages}

单击&#x200B;**查看最慢的页面**&#x200B;以打开&#x200B;**最慢的5页**&#x200B;对话框。 将显示您[配置为审核](#configuration)的五个性能最低的页面。

![最慢的五个](/help/implementing/cloud-manager/reports/assets/experience-audit-slowest-five.png)

Cloud Manager按&#x200B;**性能**、**辅助功能**、**最佳实践**&#x200B;和&#x200B;**SEO**&#x200B;划分得分，显示每个指标与上一次审核的偏差。

默认情况下，将打开包含移动设备得分的对话框。 使用对话框顶部附近的&#x200B;**设备**&#x200B;切换开关可以查看桌面分数。

该对话框旨在为您提供快速概览。 有关完整的详细信息，请单击&#x200B;**查看完整报告**。

### 查看完整报告 {#view-full-report}

您可以通过执行以下操作来查看完整的体验审核报告：

* 在&#x200B;**`View full report`**&#x200B;最慢的5页&#x200B;**[对话框中单击](#view-slowest-pages)**。
* 查看管道&#x200B;**`View full report`**&#x200B;的[执行时单击](#results)。
* 单击Cloud Manager中的&#x200B;**报表**&#x200B;选项卡。

Cloud Manager的&#x200B;**报告**&#x200B;选项卡已打开，其中显示&#x200B;**体验审核**。

![体验审核报告](/help/implementing/cloud-manager/reports/assets/experience-audit-reports.png)

报告分为两个区域：

* **[页面得分 — 趋势](#trend)**
* **[体验审核扫描结果](#results)**

#### 页面得分 — 趋势 {#trend}

默认情况下，**页面得分 — 趋势**&#x200B;的选定视图是&#x200B;**去年**&#x200B;的&#x200B;**中间分数**。

通过单击图例中的类别名称，可以选择查看特定Lighthouse类别的趋势。

![趋势可选](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-selectable.png)

使用图表顶部的下拉列表&#x200B;**选择**&#x200B;选择特定于页面的详细信息，使用底部的&#x200B;**查看**&#x200B;和&#x200B;**触发器**&#x200B;下拉列表分别选择不同的时间范围和触发器类型。

通过&#x200B;**视图**&#x200B;下拉列表可以选择预设时间范围，也可以选择更具体视图的自定义间隔。

![趋势视图](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-view.png)

将鼠标悬停在图表上时，工具提示会在特定的时间点显示Google Lighthouse类别的值。

![趋势详细信息](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-details.png)

如果单击某个时间点的图表，将打开一个弹出窗口，其中显示该扫描的详细信息。 单击&#x200B;**打开体验审核扫描**&#x200B;将该扫描结果加载到&#x200B;**[体验审核扫描结果](#scan-results)**&#x200B;部分。

![选择其他扫描](/help/implementing/cloud-manager/reports/assets/experience-audit-open-scan.png)

#### 体验审核扫描结果 {#scan-results}

**体验审核扫描结果**&#x200B;部分提供了所有扫描页面上的分数的详细信息。 使用&#x200B;**上一个**&#x200B;和&#x200B;**下一个**&#x200B;按钮逐页浏览结果，并选择显示的页数。

![扫描的页面](/help/implementing/cloud-manager/reports/assets/experience-audit-scanned-pages.png)

单击特定页面的链接将更新&#x200B;**页面得分 — 趋势**&#x200B;部分&#x200B;[**的筛选器**&#x200B;选择](#trend)，并显示&#x200B;**原始报告**&#x200B;选项卡，该选项卡为您提供每次页面审核的得分。 单击&#x200B;**Lighthouse报告**&#x200B;列中的报告日期，以检索原始数据的JSON文件。

![原始报告](/help/implementing/cloud-manager/reports/assets/experience-audit-raw-reports.png)

在浏览器中打开的新选项卡会将您引导至`https://googlechrome.github.io/lighthouse/viewer/`。 它会自动加载一个签名的URL，其中包含所选页面的Lighthouse原始JSON报告，以便进行详细检查。

![查看原始报告](/help/implementing/cloud-manager/reports/assets/experience-audit-view-raw-report.png)

## 按需扫描审核报告 {#on-demand}

体验审核报告除了在管道执行期间运行之外，还可以按需生成。 此选项是一个很好的解决方案，可以快速扫描页面，而无需运行管道。

要运行按需扫描，请导航到&#x200B;**报告**&#x200B;选项卡，以便查看完整的审核报告，然后单击&#x200B;**运行扫描**&#x200B;按钮。

![按需扫描](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand.png)

当按需扫描已运行时，**运行扫描**&#x200B;按钮将变为不可用，并且带有时钟图标。

![按需扫描正在运行](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-running.png)

按需扫描会触发对最新25个[配置页面](#configuration)的体验审核，通常在几分钟内完成。

完成后，评分图将自动更新，您可以完全按照管道执行扫描来检查结果。

您可以使用&#x200B;**触发器**&#x200B;选择器根据触发器类型筛选得分图表。

![触发器筛选器](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>仅当未删除环境且同一环境中没有其他待处理扫描时，才能启动按需扫描。

## 体验审核遇到问题 {#issues}

如果您配置的[要审核的](#configuration)页面不可用或审核过程中存在其他错误，则体验审核会反映这一事实。

管道显示一个可展开的错误部分，以查看它无法访问的相对URL路径。

体验审核遇到的![问题](/help/implementing/cloud-manager/reports/assets/experience-audit-issues.png)

如果查看完整报告，则详细信息将显示在&#x200B;**[体验审核扫描结果](#results)**&#x200B;部分中，该部分也是可扩展的。

![完整报告问题](/help/implementing/cloud-manager/reports/assets/experience-audit-issues-report.png)

页面可能不可用的部分原因是：

* 该配置阻止访问。
* 该页面不存在。
* 页面重定向需要基本身份验证以外的身份验证。
* 出现内部问题。

>[!TIP]
>
>[访问页面的原始报告](#scan-results)可以提供有关为什么无法审核该页面的详细信息。

## 体验审核评估详细信息 {#details}

以下详细信息提供了有关Experience Audit如何评估您的网站的其他信息。 对于功能的常规使用，这些参数不是必需的，此处提供这些参数是为了完整起见。

* 审核会扫描来自发布者的`.com`配置的体验审核页面路径[的源(](#configuration))域，以模拟真实的用户体验，帮助您做出更好的网站管理和优化决策。
* 在生产全栈管道中，将扫描暂存环境。 要确保审核期间提供相关详细信息，暂存环境的内容应尽可能接近生产环境。
* 在&#x200B;**页面得分 — 趋势**&#x200B;部分&#x200B;[**的下拉**&#x200B;选择](#trend)中显示的页面都是体验审核过去扫描过的已知页面。
