---
title: 如何为自适应表单配置提交操作？
description: 自适应表单提供了多个提交操作。提交操作定义了提交后处理自适应表单的方式。您可以使用内置的提交操作或创建您自己的提交操作。
keywords: 如何为自适应表单选择提交操作、将自适应表单连接到sharepoint列表、将自适应表单连接到sharepoint文档库、将自适应表单连接到表单数据模型(FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 19%

---


# 提交适用于Edge Delivery Services Forms的操作

| 版本 | 文章链接 |
|---------|-----------------------------|
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=zh-Hans) |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（核心组件） | [单击此处](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | 本文 |

提交操作定义用户提交表单时所发生的情况，例如存储数据、触发工作流或与第三方系统集成。 您可以配置的提交操作的类型取决于用于创建Edge Delivery Services Forms的创作方法。

您可以使用[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)或使用[基于Edge Delivery Services的Forms](/help/edge/docs/forms/overview.md)创作来创建Forms，并相应地使用不同的提交操作配置表单。

## 为在通用编辑器中创建的Forms提交操作

在通用编辑器中创作的[自适应Forms](/help/edge/docs/forms/universal-editor/create-forms.md)支持以下提交操作：

* [发送电子邮件](/help/forms/configure-submit-action-send-email.md)
* [调用Power Automate流](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [调用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [使用表单数据模型（FDM）提交](/help/forms/using-form-data-model.md)
* [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交到REST端点](/help/forms/configure-submit-action-restpoint.md)
* [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [调用 AEM 工作流](/help/forms/configure-submit-action-workflow.md)
* [提交至 Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [提交到Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [提交到电子表格](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

您可以使用&#x200B;**编辑表单属性**&#x200B;扩展的&#x200B;**提交**&#x200B;选项卡为在Universal Editor中创建的表单配置提交操作。

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
> * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

## 提交基于文档的Forms的操作

基于文档的Forms仅支持提交到电子表格。 要了解如何设置电子表格以接收提交的数据，请参阅[设置Google工作表或Microsoft Excel文件以开始接受数据](/help/edge/docs/forms/submit-forms.md)文章中的说明。

## 另请参阅 {#see-also}

{{af-submit-action}}

