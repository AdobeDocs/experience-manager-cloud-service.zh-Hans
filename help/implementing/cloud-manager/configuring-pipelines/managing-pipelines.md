---
title: 管理管道
description: 了解如何管理现有管道，包括编辑、运行和删除它们。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 34%

---


# 管理管道 {#managing-pipelines}

了解如何管理现有管道，包括编辑、运行和删除它们。

## 管道信息卡 {#pipeline-card}

Cloud Manager 中的&#x200B;**项目概述**&#x200B;页面上的&#x200B;**管道**&#x200B;信息卡概述了您的所有管道及其当前状态。

![Cloud Manager 中的管道信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

通过单击每个管道旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，您可以执行以下操作：

* [运行管道](#running-pipelines)
* [取消管道](#cancel)
* [编辑管道](#editing-pipelines)
* [删除管道](#deleting-pipelines)
* [查看管道的上次运行详细信息](#view-details)

在管道列表的底部，您有以下常规选项：

* **添加** — 到[添加新的生产管道](configuring-production-pipelines.md)或[添加新的非生产管道](configuring-non-production-pipelines.md)
* **全部显示** – 将用户转至管道屏幕以在更详细的表中查看所有管道。
* **访问存储库信息** – 显示访问 Cloud Manager Git 存储库所需的信息
* **了解详情** – 导航到 CI/CD 管道文档资源。

## 管道页面 {#pipelines}

**管道**&#x200B;页面显示所选项目的所有管道的完整列表。此信息非常有用，因为它提供的信息比[管道信息卡](#pipeline-card)中提供的信息更全面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**项目概述**&#x200B;页面，单击![管道选项卡 — 工作流图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **管道**&#x200B;选项卡。

1. 在&#x200B;**管道**&#x200B;页面上，您可以看到项目的所有管道列表，并且可以像在&#x200B;**管道信息卡**&#x200B;中一样启动和停止管道执行。

如果管道正在执行，请单击&#x200B;**状态**&#x200B;列中的![信息 — 媒体图标](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg)以显示包含有关执行的详细信息的弹出窗口。 在弹出窗口中，单击&#x200B;**查看详细信息**&#x200B;以查看管道执行的[详细信息](#view-details)。

![管道执行详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


您还可以单击管道旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以采取适用于该管道状态的其他操作，例如[编辑](#editing-pipelines)它或[取消执行](#cancel)。

![管道操作](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## 活动页面 {#activity}

**活动**&#x200B;页面显示选定项目和其他重要项目的所有管道执行的完整列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面，单击侧边菜单中的![铃铛图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **活动**。

1. 在&#x200B;**活动**&#x200B;页面中，您可以看到项目的所有管道执行的列表，包括当前执行和历史执行。

如果管道正在执行，您可以单击&#x200B;**状态**&#x200B;列中的![信息 — 媒体图标](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg)以显示一个弹出窗口，其中显示有关执行的信息。

![管道执行详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

单击表示管道执行的行可查看管道执行的[详细信息](#view-details)。

您还可以单击![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)对管道执行执行执行其他操作，例如查看其详细信息或下载日志，这将转到[管道详细信息页面](#view-details)。

![管道执行操作](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## 运行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡。

1. 单击您运行的管道旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击![运行 — 播放图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg) **运行**。

   管道运行开始，**状态**&#x200B;列显示其进度。

您可以通过再次单击![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)并单击&#x200B;**[查看详细信息](#view-details)**&#x200B;来查看运行的详细信息。

根据管道类型，您可以通过再次单击![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)并单击&#x200B;**取消**&#x200B;来取消运行。

## 编辑管道 {#editing-pipelines}

如果管道未运行，您可以对其进行编辑。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡。

1. 单击要编辑的管道旁的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击&#x200B;**编辑**。

1. 在&#x200B;**编辑生产管道**&#x200B;或&#x200B;**编辑非生产管道**&#x200B;对话框中，编辑在创建管道时输入的相同详细信息。

   有关对管道可用的字段和配置选项的详细信息，请参阅以下页面。
   * [配置生产管道](configuring-production-pipelines.md)
   * [配置非生产管道](configuring-non-production-pipelines.md)

1. 完成后，单击&#x200B;**更新**。

>[!NOTE]
>
>专用存储库不支持 Web 层和配置管道。有关详细信息和完整的限制列表，请参阅[在Cloud Manager中添加专用GitHub存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

## 删除管道 {#deleting-pipelines}

如果管道未运行，您可以将其删除。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡。

1. 单击您运行的管道旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击&#x200B;**删除**。


## 查看管道的上次运行详细信息 {#view-details}

您可以检查管道的详细信息，以查看其最近运行的状态和日志。 但是，仅当管道当前正在运行或已执行至少一次时，您才能访问详细信息。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡。

1. 从下拉菜单中，单击您运行的管道旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击&#x200B;**查看上一个执行**。

   您将转到运行中的管道的详细信息页面。

   ![管道详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   在此页面中，您可以查看管道各个步骤的状态并检索构建日志以进行诊断。 有关代码部署和测试运行的详细信息，请参阅[部署代码](/help/implementing/cloud-manager/deploy-code.md)。

   管道执行中的所有步骤都将显示，而尚未开始的步骤将灰显。已完成的步骤将显示其持续时间。

   管道步骤完成后，会显示摘要。

   ![步骤摘要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. 单击&#x200B;**查看详细信息**&#x200B;展开&#x200B;**持续时间**&#x200B;部分，您可以在此部分中查看基于项目历史趋势的管道平均持续时间。

   ![持续时间](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. 如果您的管道包含标记问题的&#x200B;**代码扫描**&#x200B;步骤，请单击&#x200B;**下载详细信息**&#x200B;以访问未通过测试的[代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)的列表。

   ![代码质量问题](assets/managing-pipelines-code-quality-issues.png)

   CSV文件包含一个&#x200B;**项目文件位置**&#x200B;列，该列显示问题代码相对于项目的路径。 相反，**File Location**&#x200B;列反映了Maven生成的路径。

   ![项目代码扫描问题详情](assets/managing-pipelines-code-quality-details.png)

## 取消管道 {#cancel}

如果管道运行处于验证或构建图像阶段，则可以安全地取消管道运行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在项目概述页面中，在&#x200B;**管道**&#x200B;信息卡上单击要取消的管道的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![正在取消管道](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. 单击&#x200B;**取消**。

或者，您可以从管道详细信息页面取消管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到![管道 — 工作流图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **管道**&#x200B;选项卡，然后选择要取消的管道。

   您将转到运行中的管道的详细信息页面。

   ![取消管道详细信息](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. 单击&#x200B;**取消**。
