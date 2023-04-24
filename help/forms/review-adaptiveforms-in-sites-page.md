---
title: 创建和管理在站点页面中嵌入或创建的自适应Forms审阅
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: 审核是一种机制，它允许审核人员使用“分配任务”步骤为自适应表单执行不同任务
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# 网站页面中Forms的审阅步骤 {#review-step-forms-aem-sites-page}

使用 [分配步骤](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) 在AEM工作流中，审阅人会审阅提交的表单并对其执行操作。 要使用“分配”任务步骤查看已提交的表单，请执行以下步骤：

1. [创建AEM工作流](#create-an-aem-workflow)
1. [配置自适应表单容器的提交操作](#configure-submit-action)
1. [审核后提交自适应表单](#submit-af-after-review)

## 创建AEM工作流 {#create-an-aem-workflow}

1. 在编辑模式下打开创作实例。
1. 转到 **[!UICONTROL 工具]** >  **[!UICONTROL 工作流]** >  **[!UICONTROL 模型]** > **[!UICONTROL 创建]** > **[!UICONTROL 创建模型]**
1. 指定工作流的标题并添加 **[分配任务]** 步骤
1. 点按 ![settings_icon](assets/settings_icon.png) 中。 的 **[!UICONTROL 分配任务]** 对话框。
1. 打开 [!UICONTROL 表单和文档] 选项卡，打开 [!UICONTROL 预填充] 下拉框并指定：

* 使用以下方式选择输入数据文件
* 使用以下方式选择输入附件

   ![审阅步骤](/help/forms/assets/assigntask-review1.gif)

1. 打开 **[!UICONTROL 被分派人]** 选项卡，打开 [!UICONTROL 预填充] 下拉框和指定 **[!UICONTROL 分配选项]**:

   ![审阅步骤](/help/forms/assets/review-assignstep.png)

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

## 配置提交操作 {#configure-submit-action}

现在，在网站页面上配置自适应表单容器组件的提交操作：

1. 转到网站的页面。
1. 点按 ![settings_icon](assets/settings_icon.png) 自适应表单容器的URL。 的 **[!UICONTROL 自适应表单容器]** 对话框。
1. 打开 **[!UICONTROL 提交]** 选项卡，指定 **[!UICONTROL 提交操作]** to [调用AEM工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 单击 [完成] 来保存设置。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## 审核后提交自适应表单 {#submit-af-after-review}

要查看并确认提交的自适应表单，请执行以下操作：

1. 转到 [!UICONTROL 工具] >  [!UICONTROL 工作流] >  [!UICONTROL 实例]
1. 在收件箱中，您可以看到正在创建实例。
1. 选择实例并单击 [!UICONTROL 打开].
1. 现在，您可以看到已提交的表单。

审阅人执行不同的操作：

* **提交**:审核人员填写并提交表单以供进一步处理。
* **保存**:审阅者将表单保存为其当前状态，而不提交表单。
* **重置**:审阅人清除对表单所做的任何更改，并将其恢复为原始状态。
* **委派**:审核人员将表单的所有权转移给他人，以便进一步操作或审核。
