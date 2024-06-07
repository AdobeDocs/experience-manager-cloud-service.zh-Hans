---
title: 浏览 Cloud Manager UI
description: 了解 Cloud Manager UI 的组织方式，以及如何管理您的程序和环境。
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 89%

---

# 导航 Cloud Manger UI {#navigation}

了解 Cloud Manager UI 的组织方式，以及如何管理您的程序和环境。

Cloud manage UI 主要由两个图形界面组成：

* 在[我的程序控制台](#my-programs)中，您可以查看和管理您的所有程序。
* 在[程序概述窗口](#program-overview)中，您可以查看单个程序的详细信息，并对其进行管理。

>[!TIP]
>
>另请查看 [入门文档历程](/help/journey-onboarding/overview.md) 有关如何使用Cloud Manager启动和运行AEMas a Cloud Service的完整概述。

## 我的程序控制台 {#my-programs}

当您登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager 并选择适当的组织时，您将会进入&#x200B;**我的程序**&#x200B;控制台。

![我的程序控制台](assets/my-programs-console.png)

“我的程序”控制台提供了对您在所选组织中有权访问的所有程序的概述。它由几个部分组成。

1. 用于组织选择、警报和帐户设置的[工具栏](#toolbars-my-programs-toolbars)
1. [统计数据和行动号召](#statistics)，用于概述您最近的活动
1. [计划和许可证](#programs-license)用于了解您当前的许可证状态并管理您的程序
1. [快速链接](#quick-links)可用于轻松访问相关资源

>[!TIP]
>
>有关程序的详细信息，请参阅文档[程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

### 工具栏 {#my-programs-toolbars}

有两个工具栏彼此叠放在一起。

#### Cloud Manager 标头 {#cloud-manager-header}

第一个是 Cloud Manager 标头，它会在您浏览 Cloud Manager 时持久显示。作为一个锚点，它有助于您访问适用于各个 Cloud Manager 程序的设置和信息。

![Experience Cloud 标头](assets/experience-cloud-header.png)

1. 无论您在浏览 Cloud Manager 的哪个分区，Cloud Manager 按钮都会带您返回到 Cloud Manager 中的“我的程序”控制台。
1. 点击或单击“反馈”按钮，向 Adobe 提供有关 Cloud Manager 的反馈。
1. 组织选择器会显示您当前登录的组织（在此示例中为 Foundation Internal）。如果您的 Adobe ID 与多个组织关联，请点击或单击以切换到另一个组织。
1. 点击或单击解决方案切换器可快速跳转到其他 Experience Cloud 解决方案。
1. 可使用帮助图标快速访问学习和支持资源。
1. 通知图标带有一个标记，其中显示当前分配的未完成[通知](/help/implementing/cloud-manager/notifications.md)的数量。
1. 选择代表用户的图标来访问用户设置。如果您尚未配置用户图片，系统会随机分配一个图标。

#### 程序工具栏 {#program-toolbar}

程序工具栏可以提供在 Cloud Manager 程序和适合上下文的操作之间切换的链接。

![程序工具栏](assets/program-toolbar.png)

1. 程序选择器会打开一个下拉菜单，您可以在其中快速选择其他程序或采取适合上下文的操作，例如创建一个新程序
1. 通过“快速入门”链接，您可以访问[入门文档历程](/help/journey-onboarding/overview.md)，以便快速开始使用 Cloud Manager。
1. 操作按钮可以提供适合上下文的操作，例如创建新程序。

### 统计数据 {#statistics}

统计信息部分提供了您组织的汇总数据，例如，如果您已成功设置了程序，则可能会显示过去 90 天的活动统计数据，其中包括：

* [部署](/help/implementing/cloud-manager/deploy-code.md)次数
* 已发现的[代码质量问题](/help/implementing/cloud-manager/code-quality-testing.md)数量
* 版本数

或者，如果您刚刚开始建立您的组织，则可能会有关于后续步骤或文档资源的提示。

### 程序和许可证 {#programs-license}

“我的程序”控制台的主要内容是程序列表和许可证状态。

#### 程序选项卡 {#programs}

**程序**&#x200B;选项卡列出了代表您有权访问的每个程序的信息卡。点击或单击信息卡即可访问相关程序的&#x200B;**程序概述**&#x200B;页面，以了解有关该程序的详细信息。

使用排序选项可以更好地找到您需要的程序。

![排序选项](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序依据
   * 创建日期（默认）
   * 项目名称
   * 状态
* 升序（默认）/降序
* 网格视图（默认）
* 列表视图

每个程序都会由一张信息卡（或表格中的一行）来表示，其中提供该程序的概述以及采取操作的快速链接。

![程序信息卡](assets/program-card.png)

* 程序图像（如果进行了配置）
* 项目名称
* 服务类型： **Experience Manager云** 对于AEM as a *Cloud Service计划或 [**Experience Manager** 用于AMS程序](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：沙盒或生产
* 状态
* 已配置的解决方案
* 创建日期

根据创建项目时选择的选项，生产项目可能会带有显示附加功能的标记。

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA徽章](assets/hipaa.png)

* [WAF-DDOS保护](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![waf-DDOS徽章](assets/waf-ddos-protection.png)

* [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99.99% SLA徽章](assets/9999-sla.png)

通过信息图标还可以快速访问有关该程序的附加信息（在列表视图中很有用）。

![信息](assets/information-list-view.png)

通过省略号图标可以访问可在该程序上执行的其他操作。

![程序的省略号按钮](assets/program-ellipsis.png)

* 导航至程序的特定[环境](/help/implementing/cloud-manager/manage-environments.md) 
* 打开[程序概述](#program-overview)
* [编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [删除沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>有关程序以及创建和管理程序的详细信息，请参阅以下文档。
>
>* [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### 许可证选项卡 {#license-tab}

此 **许可证** 选项卡可让您快速访问 [许可证仪表板。](/help/implementing/cloud-manager/license-dashboard.md)

### 快速链接 {#quick-links}

通过快速链接部分可以访问常用的相关资源。

## 程序概述窗口 {#program-overview}

当您在“我的程序”控制台中选择一个程序后，您就会进入“程序概述”。

![程序概述](assets/program-overview.png)

通过程序概述，您可以访问 Cloud Manager 程序的所有详细信息。与“我的程序”控制台一样，它由几个部分组成。

1. 通过[工具栏](#program-overview-toolbar)可快速跳转回“我的程序”控制台并导航程序
1. [选项卡](#program-tabs)用于在程序的不同方面之间进行切换
1. 根据对程序的最后操作制定的[行动号召](#cta)
1. 对程序[环境的概述](#environments)
1. 对程序[管道的概述](#pipelines)
1. An [性能概述](#performance) 的
1.  [有用资源](#useful-resources)的链接

### 工具栏 {#program-overview-toolbar}

程序概述的工具栏与[我的程序控制台的工具栏非常相似。](#my-programs-toolbars) 这里仅说明差异。

#### Cloud Manager 标头 {#cloud-manager-header-2}

Cloud Manager 标头有一个汉堡菜单，该菜单可自动打开以显示程序概述中的可导航选项卡。

![Cloud Manager 汉堡菜单](assets/cloud-manager-hamburger.png)

点击或单击汉堡菜单图标即可隐藏标签。

#### 程序工具栏 {#program-toolbar-2}

程序的工具栏仍然允许您快速切换到其他程序，但它还可以执行适合上下文的操作，例如添加和编辑程序。

![程序工具栏](assets/cloud-manager-program-toolbar.png)

此外，如果您选择使用汉堡菜单隐藏选项卡，则工具栏始终会提供您所在的选项卡。

### 程序选项卡 {#program-tabs}

每个程序都有许多与之相关的选项和数据。这些数据被收集到选项卡中，以简化程序导航。通过这些选项卡您可以访问：

* 概述：当前文档中描述的程序概述
* [活动](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)：程序的管道运行历史
* [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)：为程序配置的所有管道
* [存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)：为程序配置的所有存储库
* [报告](/help/implementing/cloud-manager/sla-reporting.md)：SLA 数据等量度
* [环境](/help/implementing/cloud-manager/manage-environments.md)：为程序配置的所有环境
* [内容集](/help/implementing/developing/tools/content-copy.md)：为复制目的而创建的内容集
* [复制内容活动](/help/implementing/developing/tools/content-copy.md)：内容复制活动
* 学习路径：有关 Cloud Manager 的其他学习资源

默认情况下，当您打开一个程序时，您会进入&#x200B;**概述**&#x200B;选项卡。当前选项卡会突出显示。选择另一个选项卡来显示其详细信息。

使用 [Cloud Manager 标头](#cloud-manager-header-2)中的汉堡菜单来隐藏选项卡。

### 行动呼吁 {#cta}

行动呼吁部分将会根据您的程序状态为您提供有用的信息。对于新程序，您可能会看到所提供的后续步骤，以及上线日期提醒（[在程序创建期间设置）。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新项目的行动号召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

对于实时程序，上次部署的状态包含详细信息链接以及开始新部署的链接。

![行动呼吁](/help/implementing/cloud-manager/assets/info-banner.png)

### 环境信息卡 {#environments}

**环境**&#x200B;信息卡可以为您提供环境概述以及快速操作的链接。

**环境**&#x200B;信息卡仅列出三个新环境。 单击&#x200B;**全部显示**&#x200B;按钮，查看程序的所有环境。

请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)文档，了解有关如何管理环境的详细信息。

### 管道信息卡 {#pipelines}

**管道**&#x200B;信息卡可以为您提供管道概述以及快速操作的链接。

**管道**&#x200B;信息卡仅会列出三条管道。单击&#x200B;**全部显示**&#x200B;按钮，查看程序的所有管道。

请参阅[管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)文档，了解有关如何管理管道的详细信息。

### 性能卡 {#performance}

此 **性能** 信息卡提供了 **[CDN功能板。](/help/implementing/cloud-manager/cdn-performance.md)**

![性能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 有用的资源 {#useful-resources}

**实用资源**&#x200B;部分提供了 Cloud Manager 其他学习资源的链接。
