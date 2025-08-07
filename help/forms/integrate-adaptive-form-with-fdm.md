---
title: 如何将表单的表单数据模型(FDM)与自适应表单集成？
description: 了解如何基于表单数据模型（FDM）创建表单。在 FDM 中生成并编辑数据模型对象的样本数据。
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 2c3e8f6f8dab1004a6fbd9be8f5604b1570a1808
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 28%

---

# 将表单与表单数据模型集成

将表单与表单数据模型(FDM)集成允许您使用不同的后端数据源来创建表单数据模型(FDM)。 您可以在各种表单工作流中将表单数据模型 (FDM) 用作架构。配置数据源并根据数据源中可用的数据模型对象和服务创建表单数据模型 (FDM)。

## 将Forms与表单数据模型(FDM)集成的优势

* **无缝后端连接**：将表单连接到各种后端系统(如数据库、REST API、SOAP服务、CRM)，无需自定义代码。 这样可以实现实时数据交换并减少集成工作。
* **集中式数据架构**&#x200B;表单数据模型用作统一的数据架构，它简化了跨多个表单和工作流程使用的数据对象和服务的映射和管理。

* **改进的表单预填充和提交**：使用表单数据服务轻松配置预填充和提交操作，确保准确且最新的数据检索和存储。

* **对动态工作流的支持**：表单数据模型可与工作流集成，以根据提交或检索的数据自动执行业务流程，从而提高整体效率。

## 前提条件

在使用表单数据模型配置表单之前，请确保已完成以下步骤：

* [配置数据源](/help/forms/configure-data-sources.md)：设置数据源，以将表单连接到后端数据。
* [创建表单数据模型 (FDM)](/help/forms/create-form-data-models.md)：使用来自所配置的数据源的数据对象和服务生成数据模型。
* [配置数据模型对象和服务](/help/forms/work-with-form-data-model.md)：映射数据模型对象和服务，以确保表单与数据源之间的数据流顺畅。

>[!BEGINTABS]

>[!TAB 基础组件]

执行以下步骤以使用基于基础组件的自适应表单配置表单数据模型，如下所示：

1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 使用表单数据模型提交]**。

   ![使用表单数据模型提交](/help/forms/assets/submit-uisng-fdm-fc.png)

1. 选择要提交&#x200B;**[!UICONTROL 配置的已创建]**&#x200B;数据模型。
要将附件提交到数据库，请选择&#x200B;**提交表单附件**。 通过选择&#x200B;**提交记录文档**&#x200B;将记录文档(DoR)保存在数据库中。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

>[!TAB 核心组件]

执行以下步骤以使用基于核心组件的自适应表单配置表单数据模型，如下所示：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[使用表单数据模型提交]**。
   ![使用表单数据模型提交](/help/forms/assets/submit-uisng-fdm-cc.png)

1. 选择要提交&#x200B;**[!UICONTROL 配置的已创建]**&#x200B;数据模型。
要将附件提交到数据库，请选择&#x200B;**提交表单附件**。 通过选择&#x200B;**提交记录文档**&#x200B;将记录文档(DoR)保存在数据库中。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

>[!TAB 通用编辑器]

执行以下步骤以使用在Universal as中创作的自适应表单配置表单数据模型：

1. 打开自适应表单进行编辑。
1. 单击编辑器上的&#x200B;**编辑表单属性**&#x200B;扩展。
出现&#x200B;**表单属性**&#x200B;对话框。

   >[!NOTE]
   >
   > * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
   > * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。
1. 单击&#x200B;**提交**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 使用表单数据模型提交]**。
   ![OneDrive GIF](/help/forms/assets/submit-uisng-fdm-ue.png)
如果选择&#x200B;**保存具有原始名称的附件**，则附件会使用其原始文件名存储在文件夹中。 您还可以将记录文档(DoR)保存到Azure Blob存储中。
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**

有关如何集成在通用编辑器中编写的表单的详细说明，请参阅文章[将Forms与通用编辑器中的表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

>[!ENDTABS]

## 相关文章

{{af-submit-action}}
