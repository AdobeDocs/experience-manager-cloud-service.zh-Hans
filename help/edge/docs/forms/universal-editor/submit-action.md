---
title: 如何配置自适应表单的提交操作？
description: 自适应表单提供了多个提交操作。提交操作定义了提交后处理自适应表单的方式。您可以使用内置的提交操作或创建您自己的提交操作。
keywords: 如何选择自适应表单的提交操作，将自适应表单与 sharepoint 列表连接，将自适应表单与 sharepoint 文档库连接，将自适应表单与表单数据模型 (FDM) 连接
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 100%

---

# 自适应表单提交操作

| 版本 | 文章链接 |
|---------|-----------------------------|
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（核心组件） | [单击此处](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | 本文 |


表单提交是用户旅程中至关重要的最后一步——在此阶段，将会处理所收集的数据并触发相应操作。本文档提供了在通用编辑器中配置和管理自适应表单提交操作的完整指南。

## 您将了解的内容

阅读本文档后，您将掌握以下内容：

- 为表单配置不同类型的提交操作
- 设置 REST 端点提交，以实现与外部系统的集成
- 配置表单响应的电子邮件提交
- 实施针对特定业务需求的自定义提交操作
- 处理表单提交过程中的验证与出错场景

## 目标受众

本指南面向以下人群：

- 负责实施提交逻辑的&#x200B;**表单开发人员**
- 负责将表单与后端系统连接起来的&#x200B;**系统集成商**
- 负责定义表单工作流的&#x200B;**业务分析师**
- 负责设计表单提交流程的&#x200B;**技术架构师**

## 在通用编辑器中创建的表单的提交操作

[在通用编辑器中创作的自适应表单](/help/edge/docs/forms/universal-editor/create-forms.md)支持以下提交操作：

- [发送电子邮件](/help/forms/configure-submit-action-send-email.md)
- [调用 Power Automate 流](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [调用 Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [使用表单数据模型（FDM）提交](/help/forms/integrate-adaptive-form-with-fdm.md)
- [提交到 Azure Blob 存储](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [调用 AEM 工作流](/help/forms/configure-submit-action-workflow.md)
- [提交至 Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [提交到 Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [提交到电子表格](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

您可以使用&#x200B;**编辑表单属性**&#x200B;扩展的&#x200B;**提交**&#x200B;选项卡，配置在通用编辑器中创建的表单的提交操作。

**如何配置通用编辑器中创作的表单的提交操作？**
您可以使用**编辑表单属性**&#x200B;扩展的&#x200B;**提交**&#x200B;选项卡，配置在通用编辑器中创建的表单的提交操作。

![表单属性图标](/help/forms/assets/ue-form-properties-icon.png)

![表单属性向导](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

>[!NOTE]
>
> - 如果您在通用编辑器界面中没有看到&#x200B;**编辑表单属性**&#x200B;图标，请在 Extension Manager 中启用&#x200B;**编辑表单属性**&#x200B;扩展。
> - 请参阅[扩展管理器功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用编辑器中启用或禁用扩展。
