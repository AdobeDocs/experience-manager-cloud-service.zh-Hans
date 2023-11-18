---
title: 管理管道
description: 了解如何管理现有管道，包括编辑、运行和删除它们。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 69%

---


# 管理管道 {#managing-pipelines}

了解如何管理现有管道，包括编辑、运行和删除它们。

## 管道信息卡 {#pipeline-card}

Cloud Manager 中的&#x200B;**项目概述**&#x200B;页面上的&#x200B;**管道**&#x200B;信息卡概述了您的所有管道及其当前状态。

![Cloud Manager 中的管道信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

通过单击每个管道旁边的省略号按钮，可以执行以下操作。

* [运行管道](#running-pipelines)
* [编辑管道](#editing-pipelines)
* [删除管道](#deleting-pipelines)
* [查看详细信息](#view-details)

管道列表的底部提供了常规选项。

* **添加** – 用于[添加新的生产管道](configuring-production-pipelines.md)或[添加新的非生产管道](configuring-non-production-pipelines.md)
* **全部显示** – 将用户转至管道屏幕以在更详细的表中查看所有管道。
* **访问存储库信息** – 显示访问 Cloud Manager Git 存储库所需的信息
* **了解详情** – 导航到 CI/CD 管道文档资源。

## 管道窗口 {#pipelines}

**管道**&#x200B;窗口显示所选项目的所有管道的完整列表。此列表很有用，因为它提供的信息比[管道信息卡](#pipeline-card)中的信息更全面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从 **项目概述** 页面上，选择 **管道** 制表符以切换到 **管道** 窗口。

1. 在这里，您可以看到项目的所有管道的列表，以及启动和停止管道执行，就像在&#x200B;**管道信息卡**&#x200B;中一样。

如果管道正在执行，则将鼠标悬停在其&#x200B;**状态**&#x200B;列上将显示有关执行的详细信息。

![管道执行详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

点按或单击&#x200B;**查看详细信息**&#x200B;将转至[管道执行的详细信息。](#view-details)

## 活动窗口 {#activity}

**活动**&#x200B;窗口显示所选项目的所有管道执行的完整列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从 **项目概述** 页面上，选择 **活动** 制表符以切换到 **活动** 窗口。

1. 在这里，您可以看到项目的所有管道执行的列表，包括当前执行和历史执行。

如果管道正在执行，则将鼠标悬停在其&#x200B;**状态**&#x200B;列上将显示有关执行的详细信息。

![管道执行详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

点按或单击&#x200B;**查看详细信息**&#x200B;将转至[管道执行的详细信息。](#view-details)

## 运行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至 **管道** 中的卡 **项目概述** 页面并单击运行的管道旁边的省略号按钮，然后选择 **运行** 菜单。

1. 管道将开始运行，并在&#x200B;**状态**&#x200B;栏中显示运行状态。

您可以通过再次单击省略号按钮并选择&#x200B;**[查看详细信息](#view-details)**&#x200B;来查看运行的详细信息。

根据管道类型，您可以通过再次单击省略号按钮并选择&#x200B;**取消**&#x200B;来取消运行。

## 编辑管道 {#editing-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至 **管道** 中的卡 **项目概述** 页面，单击要编辑的管道旁边的省略号按钮，然后选择 **编辑** 菜单。

1. 这将显示&#x200B;**编辑生产管道**&#x200B;或&#x200B;**编辑非生产管道**&#x200B;对话框，您可在其中编辑在创建管道时输入的相同详细信息。

   * 有关对管道可用的字段和配置选项的详细信息，请参阅以下页面。
      * [配置生产管道](configuring-production-pipelines.md)
      * [配置非生产管道](configuring-non-production-pipelines.md)

1. 单击 **更新** 在编辑完管道后。

>[!NOTE]
>
>您无法编辑运行中的管道。

## 删除管道 {#deleting-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至 **管道** 中的卡 **项目概述** 页面并单击运行的管道旁边的省略号按钮，然后选择 **删除** 菜单。

>[!NOTE]
>
>您无法删除运行中的管道。

## 查看管道详细信息 {#view-details}

您可以查看管道的详细信息，以查看其上次运行的状态和日志。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至 **管道** 中的卡 **项目概述** 页面并单击运行的管道旁边的省略号按钮，然后选择 **查看详细信息** 菜单。

1. 您将转到运行中的管道的详细信息页面。

![管道详细信息](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

在此页面中，您可以查看管道各个步骤的状态并检索构建日志以进行诊断。查看文档 [部署代码](/help/implementing/cloud-manager/deploy-code.md) 有关代码部署和测试运行的详细信息。

管道执行中的所有步骤都将显示，而尚未开始的步骤将灰显。已完成的步骤将显示其持续时间。

管道步骤完成后，将显示摘要。

![步骤摘要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

选择 **查看详细信息** 用于显示 **持续时间** 部分。 这包括基于该项目的历史趋势的管道的平均持续时间。

![持续时间](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>您只能查看运行中的或已运行至少一次的管道的详细信息。

## 取消管道 {#cancel}

如果管道处于验证或构建图像阶段，您可以安全地取消管道运行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在程序概述页面上，单击要取消的管道的省略号按钮 **管道** 卡片。

   ![取消管道](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. 选择 **取消**.

或者，您可以从管道详细信息页面取消管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至 **管道** 选项卡 **项目概述** 页面上，并选择要取消的管道。

1. 您将转到运行中的管道的详细信息页面。

   ![取消管道详细信息](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. 选择 **取消**.
