---
title: 如何将AEM工作流与自适应表单集成？
description: 探索使用AEM Forms提交操作自动启动工作流的过程。
keywords: AEM Workflow，将自适应表单与AEM Workflow集成，调用AEM Workflow提交操作
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 61%

---

# 将AEM自适应表单与AEM Workflow集成：简化业务流程

**[!UICONTROL 调用AEM工作流]**&#x200B;提交操作将自适应表单与AEM工作流相关联。 在提交表单时，关联的工作流将在创作实例上自动启动。您可以将数据文件、附件和记录文档保存到工作流的有效负荷位置或变量。 如果已为外部数据存储标记和配置工作流，则仅变量选项可用。您可以从可用于工作流模型的变量的列表中进行选择。如果在稍后阶段而不是在创建工作流时为外部数据存储标记了工作流，请确保所需的变量配置已到位。

>[!NOTE]
>
>  了解如何[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)以定义用户启动工作流时执行的一系列步骤。 您还可以定义模型属性，例如工作流是临时工作流还是使用多个资源。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。

## 优点

将AEM工作流与自适应Forms集成的一些优势包括：

* AEM Workflow集成允许自动化涉及表单提交的复杂业务流程。
* AEM Workflow支持条件逻辑，因此允许根据表单数据或外部因素进行动态决策。
* AEM Workflow根据预定义的规则和条件路由任务，确保将任务分配给适当的人员或组。

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## 将AEM工作流程与自适应Forms集成 {#steps-to-integrate-workflow-with-af}

>[!BEGINTABS]

>[!TAB 基础组件]

要为基于基础组件的自适应表单设置使用[AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)的自动流程，请执行以下步骤：

1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**提交操作**&#x200B;作为&#x200B;**[!UICONTROL 调用AEM工作流]**。
1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;下拉列表中选择工作流模型。
1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储数据文件下拉列表中选择选项。

   **数据文件**：它包含已提交到自适应表单的数据。您可以使用&#x200B;**[!UICONTROL 数据文件路径]**&#x200B;选项来指定文件名和相对于负载的文件路径。例如，`/addresschange/data.xml` 路径会创建一个名为 `addresschange` 的文件夹，并将它放置在负载的相对位置。您也可以仅指定 `data.xml` 以仅发送提交的数据而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

   ![invoke-workflow-fc](/help/forms/assets/invoke-workflow-fc.png)

1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储附件下拉列表中选择选项。

   **附件**：您可以使用&#x200B;**[!UICONTROL 附件路径]**&#x200B;选项指定用于存储已上传到自适应表单的附件的文件夹名称。该文件夹是相对于负载创建的。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

1. 使用&#x200B;**[!UICONTROL 从]**&#x200B;记录文档下拉列表中选择选项。

   **记录文档**：它包含为自适应表单生成的记录文档。您可以使用&#x200B;**[!UICONTROL 记录文档路径]**&#x200B;选项来指定记录文档的文件名以及相对于负载的文件路径。例如，`/addresschange/DoR.pdf` 路径将创建一个相对于负载的名为 `addresschange` 的文件夹，并相对于负载放置 `DoR.pdf`。您也可以仅指定 `DoR.pdf` 以仅保存记录文档而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。
1. 单击&#x200B;**[!UICONTROL 完成]**。

   >[!NOTE]
   >
   > 详细了解[以Forms为中心的AEM工作流 — 自动化业务流程的步骤参考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!TAB 核心组件]

要为基于核心组件的自适应表单设置使用[AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)的自动流程，请执行以下步骤：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 调用AEM工作流]** 。

   发送电子邮件的![操作配置](/help/forms/assets/configure-invoke-aem-workflow.png)

1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;下拉列表中选择工作流模型。
1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储数据文件下拉列表中选择选项。

   **数据文件**：它包含已提交到自适应表单的数据。您可以使用&#x200B;**[!UICONTROL 数据文件路径]**&#x200B;选项来指定文件名和相对于负载的文件路径。例如，`/addresschange/data.xml` 路径会创建一个名为 `addresschange` 的文件夹，并将它放置在负载的相对位置。您也可以仅指定 `data.xml` 以仅发送提交的数据而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储附件下拉列表中选择选项。

   **附件**：您可以使用&#x200B;**[!UICONTROL 附件路径]**&#x200B;选项指定用于存储已上传到自适应表单的附件的文件夹名称。该文件夹是相对于负载创建的。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

1. 使用&#x200B;**[!UICONTROL 从]**&#x200B;记录文档下拉列表中选择选项。

   **记录文档**：它包含为自适应表单生成的记录文档。您可以使用&#x200B;**[!UICONTROL 记录文档路径]**&#x200B;选项来指定记录文档的文件名以及相对于负载的文件路径。例如，`/addresschange/DoR.pdf` 路径将创建一个相对于负载的名为 `addresschange` 的文件夹，并相对于负载放置 `DoR.pdf`。您也可以仅指定 `DoR.pdf` 以仅保存记录文档而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。
1. 单击&#x200B;**[!UICONTROL 完成]**。

   >[!NOTE]
   >
   > 详细了解[以Forms为中心的AEM工作流 — 自动化业务流程的步骤参考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!TAB 通用编辑器]

要为在Universal Editor中创作的自适应表单设置使用[AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)的自动进程，请执行以下步骤：

1. 打开自适应表单进行编辑。
1. 单击编辑器上的&#x200B;**编辑表单属性**&#x200B;扩展。
出现&#x200B;**表单属性**&#x200B;对话框。

   >[!NOTE]
   >
   > * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
   > * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

1. 单击&#x200B;**提交**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 调用AEM工作流]**&#x200B;提交操作。


   发送电子邮件的![操作配置](/help/forms/assets/invoke-service-ue.png)

1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;下拉列表中选择工作流模型。
1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储数据文件下拉列表中选择选项。

   **数据文件**：它包含已提交到自适应表单的数据。您可以使用&#x200B;**[!UICONTROL 数据文件路径]**&#x200B;选项来指定文件名和相对于负载的文件路径。例如，`/addresschange/data.xml` 路径会创建一个名为 `addresschange` 的文件夹，并将它放置在负载的相对位置。您也可以仅指定 `data.xml` 以仅发送提交的数据而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

1. 从&#x200B;**[!UICONTROL 使用]**&#x200B;存储附件下拉列表中选择选项。

   **附件**：您可以使用&#x200B;**[!UICONTROL 附件路径]**&#x200B;选项指定用于存储已上传到自适应表单的附件的文件夹名称。该文件夹是相对于负载创建的。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

1. 使用&#x200B;**[!UICONTROL 从]**&#x200B;记录文档下拉列表中选择选项。

   **记录文档**：它包含为自适应表单生成的记录文档。您可以使用&#x200B;**[!UICONTROL 记录文档路径]**&#x200B;选项来指定记录文档的文件名以及相对于负载的文件路径。例如，`/addresschange/DoR.pdf` 路径将创建一个相对于负载的名为 `addresschange` 的文件夹，并相对于负载放置 `DoR.pdf`。您也可以仅指定 `DoR.pdf` 以仅保存记录文档而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。
1. 单击&#x200B;**[!UICONTROL 完成]**。

   >[!NOTE]
   >
   > 详细了解[以Forms为中心的AEM工作流 — 自动化业务流程的步骤参考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!ENDTABS]

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## 相关文章

{{af-submit-action}}
