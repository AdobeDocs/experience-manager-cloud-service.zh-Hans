---
title: 管理和编辑程序
description: 了解如何在创建生产和沙盒程序后进行编辑，并调整其选项。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 2dfae31e32d375c82c4f690624e48f7f09feb4df
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 32%

---


# 管理和编辑程序 {#editing-programs}

此 **我的项目群** 页面提供了您有权访问的所有程序的概述。 在选择单个项目时， **项目概述** 页面提供程序的详细信息概览。

从 **项目概述**，具有必要权限的用户可以编辑 [在您的组织中创建的生产程序](creating-production-programs.md) 和 [在您的组织中创建的沙盒程序。](creating-sandbox-programs.md) 通过编辑项目，您可以：

* 将 Sites 解决方案添加到具有 Assets 的现有项目，反之亦然。
* 从具有 Sites 和 Assets 的现有项目中删除 Sites 或 Assets。
* 将另一未使用的解决方案权利添加到现有项目或添加为新项目。
* 删除沙盒项目。

## 权限 {#permissions}

您必须是 **业务负责人** 用于编辑程序或删除沙盒程序以及访问许可证仪表板的角色。

## 我的项目群 {#my-programs}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 此 **我的项目群** 页面以图块形式显示您有权访问的所有程序的列表。

![“我的项目群”页面](/help/implementing/cloud-manager/assets/my-programs.png)

### 行动号召 {#cta}

页面顶部是与组织状态相关的行动号召。 例如，如果您已成功设置项目，则可能会显示过去90天内的活动统计数据，包括：

* 数量 [部署](/help/implementing/cloud-manager/deploy-code.md)
* 数量 [代码质量问题](/help/implementing/cloud-manager/code-quality-testing.md) 已识别
* 内部版本数

或者，如果您刚刚开始设置组织，则可能会提供有关后续步骤或文档资源的提示。

### “程序”选项卡 {#programs-tab}

此 **程序** 选项卡列出了代表您有权访问的每个程序的卡片。 点按或单击卡片以访问 **项目概述** 页面，了解有关计划的详细信息。

使用排序选项更好地查找您需要的程序。

![排序选项](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序方式
   * 创建日期（默认）
   * 项目名称
   * 状态
* 升序（默认）/降序
* 网格视图（默认）
* 列表视图

### “许可证”选项卡 {#license-tab}

此 **许可证** 选项卡可让您快速访问 [许可证仪表板。](/help/implementing/cloud-manager/license-dashboard.md)

## 项目概述 {#program-overview}

一旦您从 **[我的项目群](#my-programs)** 页面，Cloud Manager打开 **项目概述** 页面。

![项目概述页面](/help/implementing/cloud-manager/assets/program-overview.png)

点按或单击页面左上角的项目名称，可快速切换到另一个项目或返回 **[我的项目群](#my-programs)** 页面。 您还可以 [编辑所选项目](#editing) 或 [添加项目。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

![项目切换器](/help/implementing/cloud-manager/assets/program-switcher.png)

顶部的行动号召将根据项目的状态为您提供有用的信息。 对于新计划，您可以看到提供的后续步骤以及上线日期提醒， [在程序创建期间设置。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新项目的行动号召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

对于实时项目，显示上次部署的状态，其中包含详细信息链接和开始新部署的链接。

![行动号召](/help/implementing/cloud-manager/assets/info-banner.png)

**环境** 和 **管道** 信息卡可快速概述所选项目中的这两者。

![卡片](/help/implementing/cloud-manager/assets/environments-pipelines.png)

此 **性能** 信息卡提供了 **[CDN功能板。](/help/implementing/cloud-manager/cdn-performance.md)**

![性能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

## 编辑程序 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](#my-programs)** 页面上，单击要编辑的程序以显示其详细信息。

1. 单击页面左上方的项目名称，然后选择&#x200B;**编辑项目**。

   ![“编辑程序”选项](assets/edit-program-overview.png)

1. 此 **编辑项目** 页面打开 **常规** 选项卡。

   ![“常规”选项卡](assets/edit-program-prod1.png)

1. 可用于编辑程序的选项与创建程序时的选项相同。
   * 请查看文档 [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 和 [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 了解各个选项的详细信息。
   * [其他选项](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) 可用于您的生产程序，具体取决于您组织的权利。

1. 单击&#x200B;**更新**&#x200B;以将更改保存到项目。

将保存对程序所做的更改。

>[!NOTE]
>
>无论何时编辑项目，包括添加或删除解决方案或加载项，这些更改都将在下次部署后生效。

## 删除沙盒项目 {#delete-sandbox-program}

删除沙盒项目将删除与其关联的所有环境和管道。

>[!TIP]
>
>具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以选择删除其生产和暂存环境，而非整个沙盒项目。

要删除沙盒项目，请执行以下操作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](#my-programs)** 页面上，单击要编辑的程序以显示其详细信息。

1. 单击页面左上角的程序名称，然后选择 **删除项目群**.

   ![“删除程序”选项](assets/delete-sandbox1.png)

或者，您可以从 Cloud Manager 概述页面单击程序卡上的省略号按钮，然后选择&#x200B;**删除程序**。

![从程序信息卡删除沙盒](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能删除沙盒程序。无法删除生产项目。
