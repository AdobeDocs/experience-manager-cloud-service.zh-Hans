---
title: 体验审核仪表板
description: 了解体验审核如何验证您的部署过程，并通过清晰、信息丰富的仪表板界面帮助确保部署的更改符合性能、可访问性、最佳实践和SEO的基线标准。
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 8%

---


# 体验审核仪表板 {#experience-audit-dashboard}

了解体验审核如何验证您的部署过程，并通过清晰、信息丰富的仪表板界面帮助确保部署的更改符合性能、可访问性、最佳实践和SEO的基线标准。

>[!NOTE]
>
>此功能仅适用于[早期采用者计划。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>有关AEMas a Cloud Service的现有体验审核功能的详细信息，请参阅此文档 [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)

## 概述 {#overview}

体验审核会验证部署过程，并帮助确保已部署更改：

1. 满足性能、可访问性、最佳实践、SEO（搜索引擎优化）和 PWA（渐进式 Web 应用程序）的基线标准。

1. 不要引入回归。

Cloud Manager中的体验审核可确保用户在站点上的体验达到最高标准。

审核结果可提供丰富信息，允许部署管理员查看分数以及当前分数和以前分数之间的变化。此细节对于确定当前部署中是否引入了回归非常有用。

体验审核由提供支持 [Google灯塔](https://developer.chrome.com/docs/lighthouse/overview/)，Google中的一种开源工具，已在所有Cloud Manager生产管道中启用。

## 可用性 {#availability}

体验审核适用于Cloud Manager：

* 默认情况下，站点生产管道
* 开发全栈管道（可选）
* 开发前端管道（可选）

请参阅 [配置部分](#configuration) 有关如何为可选环境配置审核的更多信息。

审核作为管道的一部分运行。 审核也可以 [按需运行](#on-demand) 在管道外。

## 配置 {#configuration}

默认情况下，生产管道可以使用体验审核。 可以选择启用它来开发全栈管道和前端管道。 在所有情况下，您需要定义在管道执行期间评估哪些内容路径。

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

## 体验审核结果 {#results}

经验审核的结果列于&#x200B;**阶段测试**&#x200B;生产管道阶段[生产管道执行页面。](/help/implementing/cloud-manager/deploy-code.md)

![管道中的仪表板](assets/experience-audit-dashboard.jpg)

体验审核提供以下各项的Google Lighthouse得分中位数： [已配置页面](#configuration) 和上次扫描的得分差异。

从此摘要视图中，查看 **暂存测试** 在管道阶段，您有两个选项：

* **[查看最慢的页面](#view-slowest-pages)**
* **[查看完整报告](#view-full-report)**

除了在管道运行的详细信息中介绍的摘要之外，您还可以通过使用 **报表** 用于访问的Cloud Manager功能板选项卡 [完整的报告](#view-full-report) 直接。

>[!TIP]
>
>以下部分介绍了如何查看体验审核的结果。
>
>* 如果您想详细了解审核的工作方式，请参阅部分 [体验审核评估详细信息。](#details)
>* 如果您想了解如何按需运行体验审核，请参阅部分 [按需审核报表。](#on-demand)
>* 如果您遇到审核问题，请参阅部分 [体验审核遇到问题。](#issues)
>* 有关一般性能提示，请参阅部分 [一般性能提示。](#performance-tips)

### 查看最慢的页面 {#view-slowest-pages}

点击或单击 **查看最慢的页面** 打开 **最慢5页** 对话框，显示您认为五个性能最低的页面 [配置为审核。](#configuration)

![最慢的五](assets/experience-audit-slowest-five.jpg)

得分划分依据 **性能**， **辅助功能**， **最佳实践**、和 **SEO** 以及各个指标与上一次审核的偏差。

默认情况下，对话框打开，其中显示移动设备的得分。 您可以通过以下方式将此项更改为桌面分数 **设备** 在对话框顶部切换。

该对话框用于快速概述。 有关完整的详细信息，请点按或单击 **查看完整报告**.

### 查看完整报告 {#view-full-report}

您可以通过以下方式查看完整的体验审核报告：

* 点击或单击 **查看完整报告** 在 **[最慢5页](#view-slowest-pages)** 对话框。
* 点击或单击 **查看完整报告** 查看 [管道的执行。](#results)
* 点击或单击 **报表** 选项卡。

此 **报表** 将打开Cloud Manager的选项卡，并显示 **体验审核**.

![体验审核报告](assets/experience-audit-reports.png)

报告分为两个区域：

* **[页面得分 — 趋势](#trend)**
* **[体验审核扫描结果](#results)**

#### 页面分数 - 趋势 {#trend}

默认情况下，选定的视图 **页面得分 — 趋势** 是 **中位数分数** 对于 **过去6个月**.

使用 **选择** 和 **视图** 图表按钮顶部和底部的下拉列表，分别选择特定于页面的详细信息和不同的时间范围。 点按或单击，然后 **更新趋势** 按钮以应用选择并刷新图表。

将鼠标悬停在图表上时，工具提示会在特定的时间点显示Google Lighthouse类别的值。

![趋势详细信息](assets/experience-audit-trend-details.png)

如果您在某个时间点点按或单击图表，将打开一个弹出窗口，其中包含该扫描的详细信息。 点按或单击 **打开体验审核扫描** 将扫描结果加载到 **[体验审核扫描结果](#scan-results)** 部分。

![选择其他扫描](assets/experience-audit-open-scan.png)

#### 体验审核扫描结果 {#scan-results}

此 **体验审核扫描结果** 部分提供了有关如何提高得分的建议以及所有扫描页面的详细信息。 它分为两个部分：

* **[Recommendations](#recommendations)**
* **[扫描的页面](#scanned-pages)**

##### 推荐 {#recommendations}

此 **Recommendations** 部分显示一组汇总的分析。 默认情况下，推荐 **性能** 将显示。 使用旁边的下拉菜单 **Recommendations** 更改为其他类别。

![Recommendations](assets/experience-audit-recommendations.png)

点按或单击任何推荐的V形标记可显示有关该推荐的详细信息。

![推荐详细信息](assets/experience-audit-recommendation-details.png)

如果可用，则扩展的推荐详细信息中还包含推荐影响的百分比，以帮助重点关注最具影响力的更改。

点按或单击 **查看页面** “详细信息”视图中的链接，以查看建议适用的页面。

![推荐详细信息页面](assets/experience-audit-details-pages.png)

##### 扫描的页面 {#scanned-pages}

此 **扫描的页面** 部分提供所有扫描页面的详细信息分数。 您可以使用 **上一页** 和 **下一个** 按钮浏览结果并选择显示的页面数量。

![扫描的页面](assets/experience-audit-scanned-pages.png)

点按或单击特定页面的链接将更新 **选择** 筛选条件 [**页面得分 — 趋势** 部分](#trend) 并显示 **分数和建议** 选项卡中选定的页面。

![页面结果](assets/experience-audit-page-results.png)

此 **原始报告** 选项卡会为您提供每次页面审核的分数。 点按或单击 **下载** 图标来检索原始数据的JSON文件。

![原始报告](assets/experience-audit-raw-reports.png)

这将在您的浏览器中打开一个新选项卡，指向 `https://googlechrome.github.io/lighthouse/viewer/` 带有选定页面的Lighthouse原始JavaScript对象表示法(JSON)报告的已签名URL，该报告会自动打开以供详细检查

![查看原始报告](assets/experience-audit-view-raw-report.png)

## 按需审核报表 {#on-demand}

除了在管道执行期间运行之外，还可按需生成体验审核报表。 这是一个很好的解决方案，可以快速扫描页面，而无需运行管道。

要运行按需扫描，请导航至  **报表** 选项卡以查看完整的审核报表，然后点按或单击 **运行扫描** 按钮。

![按需扫描](assets/experience-audit-on-demand.png)

按需扫描会触发对最新25个体验的审核 [已配置页面](#configuration) 通常会在几分钟内完成。

完成后，分数图表将自动更新，您可以完全按照管道执行扫描来检查结果。

您可以使用根据触发器类型筛选得分图表 **触发器** 选择器。

![触发器筛选器](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>仅当未删除环境且同一环境中没有其他待处理扫描时，才能启动按需扫描。

## 体验审核遇到的问题 {#issues}

如果 [您配置的页面](#configuration) 不会被审计，经验审计反映了这一点。

管道显示一个可展开的错误部分，以查看它无法访问的相对URL路径。

![体验审核遇到的问题](assets/experience-audit-issues.jpg)

如果查看完整报告，详细信息将显示在 **[体验审核扫描结果](#results)** 部分。

![完整报告问题](assets/experience-audit-issues-reports.jpeg)

页面可能不可用的部分原因是：

* 该配置阻止访问。
* 该页面不存在。
* 页面重定向需要基本身份验证以外的身份验证。
* 出现内部问题。
* 等等。

>[!TIP]
>
>[访问原始报告](#scanned-pages) 对于页面，可以提供有关为何无法审核该页面的详细信息。

## 一般性能提示 {#performance-tips}

易于修复的两个最常见的影响问题与累积版面偏移(CLS)和最大内容绘制(LCP)有关。

可以通过以下方式改善这些缺陷：

* 请勿延迟加载折页上方的图像（浏览器中可见的内容无需向下滚动）。
* 正确排列加载资源的优先顺序（例如，在加载文档后异步加载折叠下方的图像）。
* 预取用于呈现折叠上方内容的JavaScript和CSS文件（如果需要）。
* 通过为加载缓慢或稍后呈现的容器指定纵横比来保留垂直空间。
* 将图像转换为WebP格式以减小其大小。
* 使用 `<picture>` 和图像 `srcset` 不同的视区大小调整不同的图像大小（并确保调整大小有效）。

## 体验审核评估详细信息 {#details}

以下详细信息提供了有关Experience Audit如何评估您的网站的其他信息。 对于功能的常规使用，这些参数不是必需的，此处提供这些参数是为了完整起见。

* 尽管 [已配置的体验审核页面路径](#configuration) 显示 `.com` 在发布者的域中，审核会扫描源(`.net`)域中，以确保检测到开发期间出现的问题。
   * 此 `.com` 域使用CDN，可以产生更好的得分或包含缓存的结果。
* 在生产全栈管道中，将扫描暂存环境。
   * 要确保审核在审核期间提供相关详细信息，暂存环境的内容应尽可能接近生产环境。
* 中显示的页面 **选择** 中的下拉菜单 [**页面得分 — 趋势** 部分](#trend) 是过去由体验审核扫描的所有已知页面。
* [推荐](#recommendations) 可能会有潜在的增益，而且与以前的扫描不同。
   * 体验审核通过处理每个页面的原始报表并将浪费的字节数或毫秒数与对性能得分具有加权影响的分析进行关联，来估计潜在的增益。
   * 审核会提供此信息（以及受影响的页面），以帮助决定要执行哪项建议。
   * 欲知更多详情，请参见 [“一般性能提示”部分](#performance-tips)
* 鉴于前端管道可以部署到现有环境（或者可能有多个前端管道针对同一环境），并且扫描结果在环境级别聚合，因此无论触发扫描的管道执行如何，得分、趋势和推荐都会显示在同一选定环境中。
