---
title: 浏览Cloud Manager UI
description: 了解Cloud Manager UI的组织方式以及如何导航以管理您的程序和环境。
source-git-commit: a0f80a363cb47be9e3d8f7fa96ea3068eb077d42
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 6%

---


# 浏览Cloud Manger UI {#navigation}

了解Cloud Manager UI的组织方式以及如何导航以管理您的程序和环境。

Cloud Manage UI主要由两个图形界面组成：

* [我的程序控制台](#my-programs) 您可以在其中查看和管理所有程序。
* [程序概述窗口](#program-overview) 在这里，您可以查看详细信息和管理单个项目。

>[!TIP]
>
>另请查看 [入门文档历程](/help/journey-onboarding/overview.md) 有关如何使用Cloud Manager启动和运行AEMas a Cloud Service的完整概述。

## 我的程序控制台 {#my-programs}

登录Cloud Manager时，位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择合适的组织，您即将 **我的项目群** 控制台。

![我的程序控制台](assets/my-programs-console.png)

“我的程序”控制台提供了选定组织中您有权访问的所有程序的概述。 它由若干部分组成。

1. [工具栏](#toolbars-my-programs-toolbars) 用于组织选择、警报和帐户设置
1. [统计和行动号召](#statistics) 有关最近活动的概述
1. [程序和许可证](#programs-license) 了解您当前的许可证状态并管理您的程序
1. [快速链接](#quick-links) 轻松访问相关资源

>[!TIP]
>
>请参阅文档 [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 了解计划的详细信息。

### 工具栏 {#my-programs-toolbars}

两个工具栏相互顶置。

#### Cloud Manager标头 {#cloud-manager-header}

第一个是Cloud Manager标头，您在导航Cloud Manager时它是永久性的。 它是一个锚点，通过它，可访问跨多个Cloud Manager程序应用的设置和信息。

![Experience Cloud 标题](assets/experience-cloud-header.png)

1. 无论您在Cloud Manager中的什么位置，Cloud Manager按钮都会将您带回Cloud Manager的“我的程序”控制台。
1. 点按或单击反馈按钮向Adobe提供有关Cloud Manager的反馈。
1. 组织选择器显示您当前登录的组织（在本例中为Foundation Internal）。 如果您的 Adobe ID 与多个组织关联，请点按或单击以切换到另一个组织。
1. 点按或单击解决方案切换器可快速跳转到其他 Experience Cloud 解决方案。
1. 可使用帮助图标快速访问学习和支持资源。
1. 通知图标带有标记，显示当前分配的未完成数量 [通知。](/help/implementing/cloud-manager/notifications.md)
1. 选择代表您的用户的图标以访问您的用户设置。 如果您尚未配置用户图片，系统会随机分配一个图标。

#### 项目工具栏 {#program-toolbar}

程序工具栏提供相应的链接，用于在适用于上下文的Cloud Manager程序和操作之间切换。

![项目工具栏](assets/program-toolbar.png)

1. 项目选择器会打开一个下拉菜单，您可以在其中快速选择其他项目或执行与上下文相关的操作，如创建新项目
1. 通过快速入门链接，您可以访问 [入门文档历程](/help/journey-onboarding/overview.md) 以启动并运行Cloud Manager。
1. 操作按钮提供了与上下文相关的操作，例如创建新项目。

### 统计数据 {#statistics}

统计部分提供组织的汇总数据，例如，如果您已成功设置程序，则可能会显示过去90天的活动统计，包括：

* 数量 [部署](/help/implementing/cloud-manager/deploy-code.md)
* 数量 [代码质量问题](/help/implementing/cloud-manager/code-quality-testing.md) 已识别
* 内部版本数

或者，如果您刚刚开始设置组织，则可能会提供有关后续步骤或文档资源的提示。

### 程序和许可证 {#programs-license}

“我的程序”控制台的主要内容是程序的列表和许可证的状态。

#### “程序”选项卡 {#programs}

此 **程序** 选项卡列出了代表您有权访问的每个程序的卡片。 点按或单击卡片以访问 **项目概述** 页面，了解有关计划的详细信息。

使用排序选项更好地查找您需要的程序。

![排序选项](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序依据
   * 创建日期（默认）
   * 项目名称
   * 状态
* 升序（默认）/降序
* 网格视图（默认）
* 列表视图

每个项目都由一个卡片（或表格中的行）表示，提供了项目的概述以及采取行动的快速链接。

![程序卡](assets/program-card.png)

* 项目图像（如果已配置）
* 项目名称
* 服务类型： **Experience Manager云** 对于AEM as a *Cloud Service计划或 [**Experience Manager** 用于AMS程序](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [项目类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：沙盒或生产
* 状态
* 配置的解决方案
* 创建日期

根据创建项目时选择的选项，生产项目可能会带有显示附加功能的标记。

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA徽章](assets/hipaa.png)

* [WAF-DDOS保护](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![waf-DDOS徽章](assets/waf-ddos-protection.png)

* [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99.99% SLA徽章](assets/9999-sla.png)

利用信息图标，还可以快速访问有关项目群的其他信息（在列表视图中很有用）。

![信息](assets/information-list-view.png)

利用省略号图标，可访问对程序执行的其他操作。

![程序的省略号按钮](assets/program-ellipsis.png)

* 导航到特定 [环境](/help/implementing/cloud-manager/manage-environments.md) 的
* 打开 [项目概述](#program-overview)
* [编辑项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [删除沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>有关程序以及创建和管理程序的详细信息，请参阅以下文档。
>
>* [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### “许可证”选项卡 {#license-tab}

此 **许可证** 选项卡可让您快速访问 [许可证仪表板。](/help/implementing/cloud-manager/license-dashboard.md)

### 快速链接 {#quick-links}

利用快速链接部分，可访问常用的相关资源。

## 程序概述窗口 {#program-overview}

在“我的程序”控制台中选择程序后，您将转到程序概述。

![程序概述](assets/program-overview.png)

通过程序概述，您可以访问Cloud Manager程序的所有详细信息。 与“我的程序”控制台一样，它由若干部分组成。

1. [工具栏](#program-overview-toolbar) 快速跳回“我的程序”控制台并导航程序
1. [选项卡](#program-tabs) 在程序的不同方面之间进行切换
1. A [行动号召](#cta) 根据程序的最后一次操作
1. An [环境概述](#environments) 的
1. An [管道概述](#pipelines) 的
1. An [性能概述](#performance) 的
1. 链接到 [有用资源](#useful-resources)

### 工具栏 {#program-overview-toolbar}

程序概述的工具栏与 [我的程序控制台。](#my-programs-toolbars) 此处仅说明了二者的差异。

#### Cloud Manager标头 {#cloud-manager-header-2}

Cloud Manager标题具有一个自动打开的汉堡菜单，可显示项目概述的可导航选项卡。

![Cloud Manager汉堡菜单](assets/cloud-manager-hamburger.png)

点按或单击汉堡菜单图标以隐藏选项卡。

#### 项目工具栏 {#program-toolbar-2}

程序工具栏仍然允许您快速切换到其他程序，但还允许您访问与上下文相关的操作，例如添加和编辑程序。

![项目工具栏](assets/cloud-manager-program-toolbar.png)

此外，如果您选择使用汉堡菜单隐藏选项卡，则工具栏始终提供您所在的选项卡。

### 项目群选项卡 {#program-tabs}

每个程序都有许多相关的选项和数据。 这些数据会收集到选项卡中，以便简化程序导航。 通过选项卡，您可以访问：

* 概述 — 当前文档中所述的程序概述
* [活动](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)  — 程序的管道运行历史记录
* [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)  — 为项目配置的所有管道
* [存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 为项目配置的所有存储库
* [报表](/help/implementing/cloud-manager/sla-reporting.md)  — 指标，如SLA数据
* [环境](/help/implementing/cloud-manager/manage-environments.md)  — 为项目配置的所有环境
* [内容集](/help/implementing/developing/tools/content-copy.md)  — 为复制目的而创建的内容集
* [复制内容活动](/help/implementing/developing/tools/content-copy.md)  — 内容复制活动
* 学习路径 — 有关Cloud Manager的其他学习资源

默认情况下，打开程序时，您会到达 **概述** 选项卡。 当前选项卡被加亮。 选择另一个选项卡以显示其详细信息。

使用中的汉堡菜单 [Cloud Manager标头](#cloud-manager-header-2) 以隐藏选项卡。

### 行动号召 {#cta}

行动号召部分将根据项目的状态为您提供有用的信息。 对于新计划，您可以看到提供的后续步骤以及上线日期提醒， [在程序创建期间设置。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新项目的行动号召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

对于实时项目，显示上次部署的状态，其中包含详细信息链接和开始新部署的链接。

![行动号召](/help/implementing/cloud-manager/assets/info-banner.png)

### 环境信息卡 {#environments}

此 **环境** 信息卡概述了您的环境并提供了快速操作链接。

**环境**&#x200B;信息卡仅列出三个新环境。 单击 **显示全部** 查看程序的所有环境。

请参阅文档 [管理环境](/help/implementing/cloud-manager/manage-environments.md) 有关如何管理环境的详细信息。

### 管道信息卡 {#pipelines}

此 **管道** 信息卡提供了管道概述以及快速操作链接。

此 **管道** 信息卡仅列出三条管道。 单击 **显示全部** 查看项目的所有管道。

请参阅文档 [管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) 有关如何管理管道的详细信息。

### 性能卡 {#performance}

此 **性能** 信息卡提供了 **[CDN功能板。](/help/implementing/cloud-manager/cdn-performance.md)**

![性能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 有用的资源 {#useful-resources}

此 **有用资源** 部分提供指向Cloud Manager其他学习资源的链接。
