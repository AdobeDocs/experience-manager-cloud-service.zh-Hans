---
title: 导航Cloud Manager UI
description: 了解 Cloud Manager UI 的组织方式，以及如何管理您的程序和环境。
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b9fb178760b74cb0e101506b6a9ff5ae30c18490
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 52%

---


# 导航 Cloud Manger UI {#navigation}

了解 Cloud Manager UI 的组织方式，以及如何管理您的程序和环境。

Cloud manage UI 主要由两个图形界面组成：

* 在[我的程序控制台](#my-programs-console)中，您可以查看和管理您的所有程序。
* 在[程序概述窗口](#program-overview)中，您可以查看单个程序的详细信息，并对其进行管理。

>[!TIP]
>
>另请查看[入门文档历程](/help/journey-onboarding/overview.md)，全面了解如何使用Cloud Manager启动和运行AEM as a Cloud Service。

## 我的程序控制台 {#my-programs-console}

当您登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager 并选择适当的组织时，您将会进入&#x200B;**我的程序**&#x200B;控制台。

![我的程序控制台](assets/my-programs-console.png)

“我的程序”控制台提供了对您在所选组织中有权访问的所有程序的概述。它由几个部分组成。

1. 用于组织选择、警报和帐户设置的[工具栏](#toolbars-my-programs-toolbars)
1. 选项卡允许您切换程序的当前视图。
   * **主页** 视图（默认），选择 **我的程序** 视图，其中显示所有项目的概览
   * 访问[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)的&#x200B;**许可证**。
   * 请注意，选项卡默认为关闭，可以使用 [Cloud Manager 标头中的汉堡菜单显示](#cloud-manager-header)。
1. [统计数据和行动号召](#statistics)，用于概述您最近的活动
1. [**我的程序** 部分](#my-programs-section) ，其中概述了您的所有计划
1. [快速链接](#quick-links-section)以轻松访问相关资源。

>[!TIP]
>
>有关程序的详细信息，请参阅文档[程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

### 工具栏 {#my-programs-toolbars}

有两个工具栏彼此叠放在一起。

#### Cloud Manager 标头 {#cloud-manager-header}

第一个是 Cloud Manager 标头，它会在您浏览 Cloud Manager 时持久显示。作为一个锚点，它有助于您访问适用于各个 Cloud Manager 程序的设置和信息。

![Experience Cloud 标头](assets/experience-cloud-header.png)

1. 单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)（显示/隐藏侧菜单）可让您访问各种选项卡，这些选项卡可带您访问各个程序的特定部分。 或者，您可以根据上下文在[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)和&#x200B;**[我的程序](#my-programs-console)**&#x200B;控制台之间切换。
1. 单击“AdobeCloud Manager”按钮可让您返回Cloud Manager的“我的程序”控制台，无论您在Cloud Manager中的哪个位置。
1. 单击&#x200B;**反馈**&#x200B;向Adobe提供有关Cloud Manager的反馈。
1. 单击组织选择器可显示您当前已登录的组织（在本例中为Foundation Internal）。 如果您的 Adobe ID 与多个组织关联，请单击以切换到另一个组织。
1. 单击![应用图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) （解决方案切换器）可快速跳转到其他Experience Cloud解决方案。
1. 单击![帮助图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Help_18_N.svg)可让您快速访问学习和支持资源。
1. 单击![铃铛图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) （[通知](/help/implementing/cloud-manager/notifications.md)）查看通知和公告等。
1. 单击表示用户对您的用户设置的访问权限的图标。 如果您尚未配置用户图片，系统会随机分配一个图标。

#### 程序工具栏 {#program-toolbar}

程序工具栏可以提供在 Cloud Manager 程序和适合上下文的操作之间切换的链接。

![程序工具栏](assets/program-toolbar.png)

1. **我的程序**&#x200B;选择器会打开一个下拉列表，您可以在其中快速选择其他程序或执行与上下文相关的操作，如创建新程序
1. 通过&#x200B;**快速入门**&#x200B;链接，您可以访问[入门文档历程](/help/journey-onboarding/overview.md)，以启动并运行Cloud Manager。
1. 操作按钮提供了与上下文相关的操作，例如添加项目。

### 统计和行动号召 {#statistics}

统计和行动号召部分提供组织的汇总数据，例如，如果您已成功设置程序，则可能会显示过去90天的活动统计数据，包括：

* [部署](/help/implementing/cloud-manager/deploy-code.md)次数
* 已发现的[代码质量问题](/help/implementing/cloud-manager/code-quality-testing.md)数量
* 版本数

或者，如果您刚刚开始建立您的组织，则可能会有关于后续步骤或文档资源的提示。

### “我的项目群”部分 {#my-programs-section}

**我的程序**&#x200B;控制台的主要内容是&#x200B;**我的程序**&#x200B;部分中的程序列表。

**我的程序**&#x200B;部分列出了代表每个程序的卡片。 点击或单击信息卡即可访问相关程序的&#x200B;**程序概述**&#x200B;页面，以了解有关该程序的详细信息。

>[!NOTE]
>
>根据您的权限，您可能无法选择某些程序。


要更轻松地查找所需的程序，请使用排序选项。

![排序选项](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序依据
   * 创建日期（默认）
   * 项目名称
   * 状态
* 升序（默认）/降序
* 网格视图（默认）
* 列表视图

#### 程序信息卡 {#program-cards}

信息卡（或表格中的行）表示每个项目，提供项目的概述以及要执行操作的快速链接。

![程序信息卡](assets/program-card.png)

* 程序图像（如果进行了配置）
* 项目名称
* 服务类型：
   * 用于AEM as a Cloud Service程序的&#x200B;**Experience Manager云**
   * [AMS程序](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)的&#x200B;**Experience Manager**
* [项目类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：
   * 沙盒
   * 生产
* 状态
* 已配置的解决方案
* 创建日期

根据创建项目时选择的选项，生产项目可能会带有显示附加功能的标记。

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA徽章](assets/hipaa.png)

* [WAF-DDOS保护](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![WAF-DDOS徽章](assets/waf-ddos-protection.png)

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
>* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### 快速链接部分 {#quick-links-section}

利用快速链接部分，可访问相关的常用资源。

## 项目概述窗口 {#program-overview}

在&#x200B;**[我的程序](#my-programs-console)**&#x200B;控制台中选择程序后，将转到&#x200B;**程序概述**&#x200B;窗口。

![程序概述](assets/program-overview.png)

通过程序概述，您可以访问 Cloud Manager 程序的所有详细信息。与&#x200B;**我的程序**&#x200B;控制台一样，它由若干部分组成。

1. [工具栏](#program-overview-toolbar)快速跳回“我的程序”控制台，并导航该程序
1. [选项卡](#program-tabs)用于在程序的不同方面之间进行切换
1. 根据对程序的最后操作制定的[行动号召](#cta)
1. 对程序[环境的概述](#environments)
1. 对程序[管道的概述](#pipelines)
1. [计划绩效](#performance)概述
1.  [有用资源](#useful-resources)的链接

### 工具栏 {#program-overview-toolbar}

程序概述的工具栏与[我的程序控制台](#my-programs-toolbars)的工具栏类似。 这里仅说明差异。

#### Cloud Manager 标头 {#cloud-manager-header-2}

Cloud Manager 标头有一个汉堡菜单，该菜单可自动打开以显示程序概述中的可导航选项卡。

![Cloud Manager 汉堡菜单](assets/cloud-manager-hamburger.png)

点击或单击汉堡菜单图标即可隐藏标签。

#### 程序工具栏 {#program-toolbar-2}

程序的工具栏仍然允许您快速切换到其他程序，但它还可以执行适合上下文的操作，例如添加和编辑程序。

![程序工具栏](assets/cloud-manager-program-toolbar.png)

工具栏始终显示您当前所在的选项卡，即使您使用汉堡菜单隐藏了这些选项卡。

### 程序选项卡 {#program-tabs}

每个程序都有许多与之相关的选项和数据。 这些选项和数据会收集到选项卡中，以便简化程序导航。 通过这些选项卡您可以访问：

**计划**

* ![现代网格视图图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg)概述 — 程序概述，如当前文档中所述
* ![铃铛图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) [活动](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) — 项目的管道运行历史记录
* ![工作流图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) — 为项目配置的所有管道
* ![文件夹图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) [存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md) — 为项目配置的所有存储库
* ![图形饼图图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg) [报表](/help/implementing/cloud-manager/sla-reporting.md) - SLA数据等量度

**服务**

* ![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) [环境](/help/implementing/cloud-manager/manage-environments.md) — 为程序配置的所有环境
* ![网页图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Edge Delivery站点](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) — 管理Edge Delivery站点
* ![设置图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) [域设置](/help/implementing/cloud-manager/custom-domain-names/introduction.md) — 管理项目的自定义域名
* ![锁定已关闭图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) [SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) — 管理程序的SSL证书
* ![社交网络图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) [CDN配置](/help/implementing/cloud-manager/custom-domain-names/introduction.md) — 管理CDN配置
* ![任务列表图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) [IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) — 为某些IP地址定义允许列表
* ![Box图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) [内容集](/help/implementing/developing/tools/content-copy.md) — 为复制目的而创建的内容集
* ![历史记录图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) [复制内容活动](/help/implementing/developing/tools/content-copy.md) — 内容复制活动
* ![渠道图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg) [网络基础架构](/help/security/configuring-advanced-networking.md) — 管理程序的高级联网选项

**资源**

* 学习路径：有关 Cloud Manager 的其他学习资源

默认情况下，当您打开一个程序时，您会进入&#x200B;**概述**&#x200B;选项卡。当前选项卡会突出显示。选择另一个选项卡来显示其详细信息。

使用 [Cloud Manager 标头](#cloud-manager-header-2)中的汉堡菜单来隐藏选项卡。

### 呼叫段 {#cta}

行动号召部分会根据您的程序状态为您提供有用的信息。 对于新计划，您可能会看到给出的后续步骤以及上线日期提醒，[在计划创建期间设置](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。

新项目的![行动号召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

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

**性能**&#x200B;卡提供&#x200B;**[CDN仪表板](/help/implementing/cloud-manager/cdn-performance.md)**&#x200B;的概述。

![性能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 有用的资源 {#useful-resources}

**实用资源**&#x200B;部分提供了 Cloud Manager 其他学习资源的链接。
