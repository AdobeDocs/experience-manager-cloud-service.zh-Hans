---
title: 生产和暂存环境的运行状况评估
description: 了解如何使用Cloud Manager的运行状况评估。 您可以扫描AEM环境、运行和查看报告、查看问题详细信息、导出PDF以及管理过去运行。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 9%

---


# 健康评估 {#about-health-assessment}

运行状况评估是AEM as a Cloud Service中对Cloud Manager中的生产和暂存环境进行的自动非侵入式扫描。 它评估内容、代码和配置以发现反模式并偏离最佳实践，从而提高安全性和性能。

运行状况评估服务执行以下操作：

* 扫描环境并暴露性能瓶颈、低效和风险。
* 分析内容结构，如Blueprint、活动副本和客户配置。
* 检测过时的依赖项，包括AEM SDK和第三方库。
* 标记代码质量问题，如不正确的注释和效率低下的模式。
* 在功能板（如操作中心）中提供可操作的指导。
* 推动主动修复以提高系统性能。

每次运行都会按严重程度列出问题，并提供指向指导和建议修复的链接，同时支持报表的PDF导出。 您可以使用当前状态的&#x200B;**最新报表**&#x200B;视图和&#x200B;**过去报表**&#x200B;来比较运行。

另请参阅[运行状况评估模式](#ha-patterns)以了解规则定义和修正详细信息。

## 访问“运行状况评估”页面 {#access-health-assessment}

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登录 Cloud Manager。
1. 在&#x200B;**快速访问**&#x200B;部分中，单击&#x200B;**Experience Manager**。
1. 在左侧面板中点击 **Cloud Manager**。
1. 选择所需的组织。 下图是图示。 选择您自己的组织名称。

   ![在Cloud Manager中选择组织](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. 在&#x200B;**我的程序**&#x200B;控制台上，单击要查看其报告的程序。

1. 执行以下任一操作：
   * 在&#x200B;**环境**&#x200B;信息卡中，单击环境名称右侧的![省略号图标或“更多”图标](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然后从菜单中选择&#x200B;**运行状况评估**。

     ![从环境信息卡中的省略号菜单中选择运行状况评估](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * 从左侧菜单的&#x200B;**服务**&#x200B;下，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。 在“环境”页面的环境名称右侧，单击![省略号图标或“更多”图标](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然后从菜单中选择&#x200B;**运行状况评估**。

     ![从环境页面上的省略号菜单中选择运行状况评估](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## 为所选环境运行新报告 {#run-report}

1. [访问运行状况评估页面](#access-health-assessment)。
1. 在&#x200B;**运行状况评估**&#x200B;页面的右上角，确认您即将评估的目标环境。

   如果环境不正确，请单击![V形下拉菜单或下拉菜单选择其他环境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，以从列表中选择正确的环境。

1. 单击&#x200B;**运行报告**。

   ![单击“运行状况评估”页面上的“生成新报告”按钮](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   在选定环境中运行报告时，**运行报告**&#x200B;将保持禁用状态，直到它完成。

   ![正在运行报告](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   报告完成后，该报告将显示在&#x200B;**运行状况评估**&#x200B;页面的&#x200B;**最新报告**&#x200B;部分中。

## 查看最新报告 {#view-latest-report}

* 在&#x200B;**运行状况评估**&#x200B;页面上，查看&#x200B;**最新报告**&#x200B;部分以了解以下信息：

   * 最近运行的结果。
   * 运行日期和时间。
   * 问题总数。
   * 最关键问题的亮点。
   * 操作：**[查看详细信息](#view-report-details)**&#x200B;或&#x200B;**[下载所有问题的PDF](#download-pdf-report)**。

  ![为所选环境生成新报告后显示的“最新评估”页面](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### 查看最新的报告详细信息 {#view-report-details}

* 在&#x200B;**运行状况评估**&#x200B;页面的&#x200B;**最新报告**&#x200B;标题右侧，单击![省略号图标或更多图标](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然后单击&#x200B;**查看详细信息**&#x200B;或&#x200B;**下载**。

  **查看详细信息**&#x200B;选项显示以下内容：

   * 全面的问题列表。
   * 能够查看调查结果和问题描述。
   * 能够查看包含潜在修复的文档。

     ![问题描述和发现](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * 通过&#x200B;**下载**&#x200B;选项，您可以在PDF中下载各个问题报告。

     ![下载各个问题报告的PDF](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### 下载整个报表的PDF {#download-pdf-report}

* 在报表页面的右上角附近，单击&#x200B;**下载**。

  将生成一个ZIP文件，其中包含报告中检测到的所有问题的PDF。

  ![下载在报告中发现的所有问题的PDF](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## 查看过去的报告 {#review-past-reports}

在&#x200B;**运行状况评估**&#x200B;页面上，查看&#x200B;**过去的报告**&#x200B;部分以了解以下信息：

* 查看任何先前报告的详细信息。
* 查看每次运行的日期。
* 下载适用于任何报表的PDF。
* 按日期、问题数或环境排序。

![审阅过去的报告](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* 在&#x200B;**过去的报告**&#x200B;标题的右侧，单击![V形下拉菜单或下拉菜单以选择其他环境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)来按日期对过去的报告进行排序。
* 在报表的最右侧，单击![省略号图标或更多图标](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然后单击&#x200B;**查看详细信息**&#x200B;或&#x200B;**下载**。


## 运行状况评估模式 {#ha-patterns}

下面是健康评估在AEM as a Cloud Service中检测到的反模式和问题的完整列表。 该表将项目分组为三种类型：Content Analysis、Code Analysis和Cloud Service Optimizer反模式，并针对每种类型进行说明。

| 模式名称 | 类别 | 类型 | 描述 | 影响 | 自动修复？ |
| --- | --- | --- | --- | --- | --- |
| 添加直接用户的自定义AEM组 | 安全性 | 内容分析 | 用户直接添加到AEM组，而不是将IMS组添加为成员。 | 权限管理和安全治理可能会变得复杂。 [IMS支持](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/ims-support) | 否 |
| 页面中缺少JCR内容节点 | 存储库结构 | 内容分析 | 页面中缺少`jcr:content`节点。 | Experience Manager as a Cloud Service中的功能限制。 [模式检测 — ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | 否 |
| 页面中缺少Sling资源类型 | 存储库结构 | 内容分析 | 页面中缺少`sling:resourceType`。 | Experience Manager as a Cloud Service中的功能限制。 [模式检测 — ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | 否 |
| 节点数过多的页面 | 性能 | 内容分析 | 页面结构中包含大量节点。 | 页面加载时间缓慢且用户体验不佳。 [模式检测 — PCX](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | 否 |
| 运行的工作流实例过多 | 性能 | 内容分析 | 正在运行的工作流实例过多。 | 整体系统性能下降。 [维护任务](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/operations/maintenance) | 否 |
| 未清除的已完成工作流实例 | 性能 | 内容分析 | 未清除较早完成的工作流实例。 | 降低了系统效率和存储成本。 [维护任务](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/operations/maintenance) | 否 |
| 内容片段使用情况统计数据 | 统计数据 | 内容分析 | 跟踪正在使用的内容片段的数量。 | 不适用 | 不适用 |
| 内容片段模型使用情况统计数据 | 统计数据 | 内容分析 | 跟踪正在使用的内容片段模型的数量。 | 不适用 | 不适用 |
| MSM大量Blueprint | 统计数据 | 内容分析 | 跟踪Blueprint的数量。 | 它可以增加管理复杂性并使内容治理更加困难。 | 不适用 |
| 每个Blueprint的MSM页面数 | 统计数据 | 内容分析 | 跟踪每个Blueprint的页面数。 | 它可以增加管理复杂性并使内容治理更加困难。 | 不适用 |
| MSM过多的活动副本 | 统计数据 | 内容分析 | 跟踪活动副本的数量。 | 它可能会导致转出期间出现性能问题并使内容同步复杂化。 | 不适用 |
| 每个Blueprint的MSM活动副本过多 | 统计数据 | 内容分析 | 跟踪每个Blueprint的活动副本数。 | 它可能会导致转出期间出现性能问题并使内容同步复杂化。 | 不适用 |
| Assets的数量 | 统计数据 | 内容分析 | 跟踪资源数。 | 不适用 | 不适用 |
| 站点数 | 统计数据 | 内容分析 | 跟踪站点的数量。 | 不适用 | 不适用 |
| Forms的数量 | 统计数据 | 内容分析 | 跟踪表单的数量。 | 不适用 | 不适用 |
| 表单片段 | 统计数据 | 内容分析 | 跟踪表单片段的数量。 | 不适用 | 不适用 |
| 交互通信 | 统计数据 | 内容分析 | 跟踪表单通信交互的次数。 | 不适用 | 不适用 |
| FDM | 统计数据 | 内容分析 | 跟踪表单数据模型的数量。 | 不适用 | 不适用 |
| 已过时的依赖项 | 依赖项 | 代码分析 | 突出显示客户存储库中过时的依赖项。 | 与较新的AEM版本不兼容；可能存在安全漏洞。 | 否 |
| AEM SDK版本不匹配 | 依赖项 | 代码分析 | 旧版本(n-2)与Cloud Manager环境版本相比。 | 它可能会导致Cloud Manager中的生成错误以及本地开发环境中的问题。 | 否 |
| Mockito核心依赖关系已过时 | 依赖项 | 代码分析 | 对于AEM as a Cloud Service，低于4.x.x的版本被视为已过时。 | 它可能会导致Cloud Manager中的生成错误以及本地开发环境中的问题。 | 否 |
| 不支持的注释 | 依赖项 | 代码分析 | 客户的Cloud Manager存储库中不支持的注释。 | 潜在的应用程序故障和性能下降。 | 否 |
| Sling模型中的@Inject注释 | 依赖项 | 代码分析 | 已弃用`@Inject`注释。 | 由于注入解析度开销而降低了应用程序性能。 | 否 |
| 出站HTTP请求 | 性能 | Cloud Service Optimizer反模式 | 在请求上下文、高超时或未关闭连接中的使用存在问题。 | 整体系统性能下降和可能的中断。 | 是 |
| 查询速度较慢 | 性能 | Cloud Service Optimizer反模式 | 客户代码查询缓慢。 | 系统性能降低和潜在的超时。 | 是 |

### 类别 {#ha-patterns-categories}

| 类别 | 描述 |
| --- | --- |
| 安全性 | 与安全实践、用户管理和访问控制相关的模式。 |
| 性能 | 影响应用程序和系统性能的模式。 |
| 存储库结构 | 与JCR存储库组织和结构相关的模式。 |
| 依赖项 | 与代码依赖性和版本管理相关的模式。 |
| 统计数据 | 表示使用统计信息和量度的模式。 |



