---
title: 添加Edge Delivery管道
description: 了解如何添加Edge Delivery管道以生成代码并将其部署到生产环境。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="私人测试版" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#gitlab-bitbucket"
hide: false
index: false
hidefromtoc: false
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---


# 添加Edge Delivery管道 {#configure-production-pipeline}

了解如何配置Edge Delivery管道以生成代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境。 在获得批准后，它会将相同的代码部署到生产环境。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置生产管道。

>[!NOTE]
>
>在发生以下情况之前，无法配置Edge Delivery管道：
>
>* 将创建一个程序，其中包含一个Edge Delivery Services站点和一个映射的域。 否则，用户界面中的选项&#x200B;**添加Edge Delivery管道**&#x200B;显示为禁用，并且工具提示将说明缺少的要求。<!-- CMGR‑69680 -->
>* Git存储库至少有一个分支。
>* 将创建生产和暂存环境。

在开始部署代码之前，请从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>您可以在初始配置后[编辑管道设置](managing-pipelines.md)。

**添加Edge Delivery管道：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择所需的组织。

1. 在&#x200B;**我的程序**&#x200B;页面上，选择所需的程序。

   在Cloud Manager中![我的程序页](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. 执行下列操作之一：

   * **从管道信息卡添加Edge Delivery管道**

      1. 在左边栏中的&#x200B;**计划**&#x200B;下，单击&#x200B;**![概述图标](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [概述](/help/implementing/cloud-manager/navigation.md#my-programs)**。
      1. 在&#x200B;**项目概述**&#x200B;页面的&#x200B;**管道**&#x200B;信息卡下，单击&#x200B;**![加号](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)添加**，然后选择&#x200B;**添加Edge Delivery管道**。

         ![项目概述页面上的管道信息卡](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

   * **从管道页面添加Edge Delivery管道**

      1. 在左边栏中的&#x200B;**项目**&#x200B;下，单击&#x200B;**![工作流图标或管道图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)管道**。
      1. 在管道页面的右上角附近，单击&#x200B;**添加管道** > **添加Edge Delivery管道**。

         ![具有“添加管道”按钮的“管道”页面](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

1. 在&#x200B;**添加Edge Delivery管道**&#x200B;对话框的&#x200B;**管道名称**&#x200B;文本字段中，键入描述性管道标签。

   ![添加Edge Delivery管道对话框](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. 选择您想要的管道&#x200B;**部署触发器**&#x200B;选项。

   * **手动** — 你开始部署。
   * **在Git发生更改时** - Git承诺会自动启动部署。 利用此选项，如有必要，您仍然可以手动启动管道。

1. 单击&#x200B;**继续**。

1. 在&#x200B;**Source代码**&#x200B;下，设置以下选项：

   * **部署环境** — 显示目标环境字段；保持只读状态。

   * **存储库** — 使用下拉列表将管道指向存储Edge Delivery配置的确切Git存储库。

     另请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支** — 使用下拉列表选择所选存储库中的特定分支。 如有必要，请单击“回收”图标或“刷新”图标![，以便在最近推送后重新加载Git分支下拉列表](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg)
   * **代码位置** — 定义管道就绪代码在存储库中开始的文件夹路径（`/`等于存储库根）。

   ![配置管道](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. 单击&#x200B;**保存**。

您现在可以在[项目概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;卡或&#x200B;**管道**&#x200B;页面上&#x200B;**管理您的管道**。
