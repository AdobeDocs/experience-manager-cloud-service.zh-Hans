---
title: 建立和管理內嵌或建立於Sites頁面的最適化Forms稽核
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: 稽核是一種機制，可讓稽核者使用指派任務步驟為最適化表單執行不同任務
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# 網站頁面中Forms的檢閱步驟 {#review-step-forms-aem-sites-page}

使用 [指派步驟](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) 在AEM工作流程中，稽核者會稽核提交的表單並對其執行操作。 若要使用「指派」工作步驟來複查已提交的表單，請遵循下列步驟：

1. [建立AEM工作流程](#create-an-aem-workflow)
1. [設定最適化表單容器的提交動作](#configure-submit-action)
1. [稽核後提交最適化表單](#submit-af-after-review)

## 建立AEM工作流程 {#create-an-aem-workflow}

1. 在編輯模式下開啟您的作者執行個體。
1. 前往 **[!UICONTROL 工具]** >  **[!UICONTROL 工作流程]** >  **[!UICONTROL 模型]** > **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**
1. 指定工作流程的標題並新增 **[指派任務]** 步驟
1. 點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **[!UICONTROL 指派任務]** 對話方塊開啟。
1. 開啟 [!UICONTROL 表單和檔案] 標籤並開啟 [!UICONTROL 預先填入] 下拉式清單並指定：

   * 使用以下方式选择输入数据文件
   * 使用以下方式选择输入附件

   ![檢閱步驟](/help/forms/assets/assigntask-review1.gif)

1. 開啟 **[!UICONTROL 被指定者]** 標籤並開啟 [!UICONTROL 預先填入] 下拉式清單並指定 **[!UICONTROL 指派選項]**：

   ![檢閱步驟](/help/forms/assets/review-assignstep.png)

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

## 設定提交動作 {#configure-submit-action}

現在，請在網站的頁面上設定最適化表單容器元件的「提交」動作：

1. 前往網站的頁面。
1. 點選 ![settings_icon](assets/settings_icon.png) 最適化表單容器的預設值。 此 **[!UICONTROL 最適化表單容器]** 對話方塊開啟。
1. 開啟 **[!UICONTROL 提交]** 定位字元並指定 **[!UICONTROL 提交動作]** 至 [叫用AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 按一下 [完成] 以儲存設定。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## 稽核後提交最適化表單 {#submit-af-after-review}

若要檢閱並確認已提交的最適化表單：

1. 前往 [!UICONTROL 工具] >  [!UICONTROL 工作流程] >  [!UICONTROL 執行個體]
1. 在「收件匣」中，您可以看到正在建立執行個體。
1. 選取執行個體並按一下 [!UICONTROL 開啟].
1. 現在，您可以檢視提交的表單。

稽核者會執行不同的動作，如：

* **提交**：稽核者完成表單並提交以進行進一步處理。
* **儲存**：稽核者將表單儲存為目前狀態而不提交。
* **重設**：檢閱者會清除對表單所做的任何變更，並將其還原為原始狀態。
* **委派**：稽核者會將表單的所有權轉讓給其他人，以採取進一步行動或進行稽核。
