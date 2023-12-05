---
title: 如何发送自适应表单以供审查？ 如何管理aem自适应表单的审核？
description: 审核是一种机制，它允许审核者使用“分配任务”步骤为自适应表单执行不同的任务。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# 创建和管理自适应表单审核 {#review-step-forms-aem-sites-page}

使用 [分配步骤](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) 在AEM工作流中，审阅者审阅提交的表单并对其执行操作。 要使用“分配任务”步骤复查已提交的表单，请执行以下步骤：

1. [创建AEM工作流](#create-an-aem-workflow)
1. [配置自适应表单容器的提交操作](#configure-submit-action)
1. [审核后提交自适应表单](#submit-af-after-review)

## 创建AEM工作流 {#create-an-aem-workflow}

1. 在编辑模式下打开创作实例。
1. 转到 **[!UICONTROL 工具]** >  **[!UICONTROL 工作流]** >  **[!UICONTROL 模型]** > **[!UICONTROL 创建]** > **[!UICONTROL 创建模型]**
1. 指定工作流的标题并添加 **[分配任务]** 步骤
1. 选择 ![settings_icon](assets/settings_icon.png) 在操作栏上。 此 **[!UICONTROL 分配任务]** 对话框打开。
1. 打开 [!UICONTROL 表单和文档] 选项卡并打开 [!UICONTROL 预填充] 下拉列表并指定：

   * 使用以下方式选择输入数据文件
   * 使用以下方式选择输入附件

   ![审核步骤](/help/forms/assets/assigntask-review1.gif)

1. 打开 **[!UICONTROL 被分派人]** 选项卡并打开 [!UICONTROL 预填充] 下拉列表并指定 **[!UICONTROL 分配选项]**：

   ![审核步骤](/help/forms/assets/review-assignstep.png)

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

## 配置提交操作 {#configure-submit-action}

现在，在站点的页面上配置自适应表单容器组件的提交操作：

1. 转至站点的页面。
1. 选择 ![settings_icon](assets/settings_icon.png) 自适应表单容器的。 此 **[!UICONTROL 自适应表单容器]** 对话框打开。
1. 打开 **[!UICONTROL 提交]** 制表符并指定 **[!UICONTROL 提交操作]** 到 [调用AEM工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 单击 [完成] 以保存设置。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## 审核后提交自适应表单 {#submit-af-after-review}

要查看和确认提交的自适应表单，请执行以下操作：

1. 转到 [!UICONTROL 工具] >  [!UICONTROL 工作流] >  [!UICONTROL 实例]
1. 在收件箱中，您可以看到正在创建实例。
1. 选择实例，然后单击 [!UICONTROL 打开].
1. 现在，您可以查看提交的表单。

审阅者执行不同的操作：

* **提交**：审核者完成表单并提交以进行进一步处理。
* **保存**：查看者将表单保存为其当前状态，而不提交表单。
* **重置**：查看者会清除对表单所做的任何更改，并将其恢复为原始状态。
* **委派**：审核者将表单的所有权转移给其他人员，以便进一步操作或审核。
