---
title: 如何在通用编辑器中为一个表单集成表单数据模型 (FDM)？
description: 了解如何基于表单数据模型（FDM）创建表单。在 FDM 中生成并编辑数据模型对象的样本数据。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 95998daf04ae579ca11896953903852e6140c3a4
workflow-type: ht
source-wordcount: '1207'
ht-degree: 100%

---

# 在通用编辑器中将表单与表单数据模型集成

在通用编辑器中将表单与表单数据模型 (FDM) 集成，这样就可以使用不同的后端数据源来创建表单数据模型 (FDM)。您可以在各种表单工作流中将表单数据模型 (FDM) 用作架构。配置数据源并根据数据源中可用的数据模型对象和服务创建表单数据模型 (FDM)。

## 注意事项

* 如果您在通用编辑器界面中看不到&#x200B;**数据源**&#x200B;图标，或者在右侧属性面板中看不到&#x200B;**绑定引用**&#x200B;属性，就请在&#x200B;**扩展管理器**&#x200B;中启用&#x200B;**数据源**&#x200B;扩展。

  ![扩展管理器](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

  请参阅[扩展管理器功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用编辑器中启用和禁用扩展。

* 目前通用编辑器中不支持表单预填服务。

## 前提条件

在通用编辑器中用表单数据模型配置表单之前，请确保已完成以下步骤：

* [配置数据源](/help/forms/configure-data-sources.md)：设置数据源，以将表单连接到后端数据。
* [创建表单数据模型 (FDM)](/help/forms/create-form-data-models.md)：使用来自所配置的数据源的数据对象和服务生成数据模型。
* [配置数据模型对象和服务](/help/forms/work-with-form-data-model.md)：映射数据模型对象和服务，以确保表单与数据源之间的数据流顺畅。

## 在通用编辑器中使用表单数据模型创建表单

在通用编辑器中，您可以创建：

* [基于架构的表单](#schema-based-form)：基于架构的表单使用在表单创建过程中在&#x200B;**数据**&#x200B;选项卡中配置的数据源，自动将数据绑定到表单字段。
* [非基于架构的表单](#non-schema-based-form)：非基于架构的表单需要您手动添加数据源并绑定内容树中的每个字段。

![通用编辑器中的表单类型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

这些方法使您可以根据需要灵活地将数据模型与表单连接起来。

### 基于架构的表单

当您创建基于架构的表单时，它会自动配置数据源，并且表单字段已经通过数据绑定与数据关联。要使用表单创建向导创建基于架构的表单，请执行以下步骤：

1. 登录到[!DNL Experience Manager Forms]作者实例。
1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**。向导随即打开。在&#x200B;**源**&#x200B;选项卡中，选择一个模板：

   ![选择 Edge Delivery Services 模板](/help/edge/assets/create-eds-forms.png)

   选择基于 Edge Delivery Services 的模板后，**[!UICONTROL 创建]**&#x200B;按钮就被启用。您可以在&#x200B;**[!UICONTROL 数据源]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中选择一个数据源或提交操作。

1. 在&#x200B;**数据**&#x200B;选项卡中，您可以选择以下一个数据模型：

   * **表单数据模型 (FDM)**：将来自数据源的数据模型对象和服务集成到表单中。如果您的表单需要从多个来源读写数据，请选择表单数据模型 (FDM)。

   * **JSON 架构**：通过关联一个定义数据结构的 JSON 架构将您的表单与后端系统集成。它允许您使用架构元素添加动态内容。

     例如，选择已创建的名为“宠物表单数据模型”的表单数据模型。

     ![选择表单数据模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     默认情况下，关联的 JSON 架构或表单数据模型 (FDM) 的所有字段都将自动选定并转换为相应的表单组件，从而简化创作过程。该向导还允许您使用复选框选择表单中要包含哪些字段。

1. 单击&#x200B;**[!UICONTROL 创建]**，将出现&#x200B;**创建表单**&#x200B;向导。
1. 指定&#x200B;**名称**&#x200B;和&#x200B;**标题**。
1. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 `edsforms`，则它位于帐户 `wkndforms` 下，其 URL 为：
   `https://github.com/wkndforms/edsforms`
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建基于架构的表单](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

   ![创作表单](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   创建该表单时使用了来自关联数据源的数据元素，其中的表单字段已预配置了数据绑定。

   ![自动数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您现在可以为表单添加和[配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

### 非基于架构的表单

当您创建非基于架构的表单时，不配置任何数据源。您可以稍后编辑表单属性以添加数据源，然后手动配置表单字段的数据绑定。执行以下步骤来编辑表单属性并添加数据源：

1. 登录到[!DNL Experience Manager Forms]作者实例。
1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择要添加数据源的表单，然后单击&#x200B;**[!UICONTROL 属性]**。
   ![打开表单属性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   这将打开表单属性。
1. 单击打开&#x200B;**表单模型**&#x200B;选项卡，然后在&#x200B;**从中选择**&#x200B;下拉菜单中选择。您可以选择以下选项之一：

   * **表单数据模型 (FDM)**：使用表单数据模型创建表单。
   * **连接器**：使用 Adobe Marketo 数据源创建表单。
   * **架构**：使用上传到 AEM Forms 的 JSON 架构创建表单。
   * **无**：从头创建表单，不使用任何表单模型。

     例如，选择表单数据模型 (FDM)

     ![选择表单模型选项卡](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. 从下拉列表中选择已创建的表单数据模型（FDM）。例如，从下拉列表中选择已创建的名为“宠物表单数据模型”的表单数据模型。

   ![选择 FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   选择表单数据模型（FDM）时，会出现警告对话框。单击 **OK**，关闭对话框。

   ![表单模型向导](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。
1. 打开表单进行编辑。表单在通用编辑器中打开以进行创作。

   ![非基于架构的表单创作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   相关表单数据模型 (FDM) 中的表单元素显示在&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**属性面板**&#x200B;中的&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中。

   ![表单数据源](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 从&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中选择数据元素，然后单击&#x200B;**[!UICONTROL 添加]**。

   ![添加数据元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   您还可以拖放这些元素来生成自适应表单。单击&#x200B;**[!UICONTROL 添加]**&#x200B;后，在&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中选定的元素将添加到表单中，添加的元素前面会显示一个对勾。

   ![生成表单](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

您可以从&#x200B;**绑定引用**&#x200B;属性中选择数据绑定，将其添加到一个表单字段中。例如，将数据绑定引用添加到表单中已有的 **Id** 文本框中。要从数据源树中为表单字段选择数据绑定，请执行以下步骤：

1. 打开要为其添加数据绑定引用的表单字段的属性。
1. 前往&#x200B;**绑定引用**&#x200B;属性，然后单击&#x200B;**浏览**&#x200B;图标。

   ![将数据绑定手动添加到一个表单字段](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

1. 在&#x200B;**选择绑定引用**&#x200B;向导中，从数据源树中选择数据绑定引用。

   ![选择数据绑定引用](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

1. 从数据源树中选择要绑定到表单字段的数据元素，然后单击&#x200B;**选择**。

   ![选择数据元素](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)。

   表单字段绑定到数据元素，并显示在&#x200B;**绑定引用**&#x200B;属性中。

   ![自动数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您也可以为表单字段手动编辑&#x200B;**绑定引用**&#x200B;属性。

您现在可以为表单添加和[配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

## 另请参阅

{{universal-editor-see-also}}
