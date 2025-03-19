---
title: 如何在通用编辑器中集成表单的表单数据模型(FDM)？
description: 了解如何基于表单数据模型(FDM)创建表单。 在FDM中生成并编辑数据模型对象的示例数据。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 381aad580762fe957e1dc1d5824e4d35098f1ca4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 7%

---

# 在通用编辑器中集成表单与表单数据模型

将表单与通用编辑器中的表单数据模型(FDM)集成后，您可以使用各种后端数据源来创建表单数据模型(FDM)。 您可以将表单数据模型(FDM)用作各种表单工作流中的架构。 根据数据源中可用的数据模型对象和服务，配置数据源并创建表单数据模型(FDM)。

## 考虑

* 当前不支持通用编辑器中表单的预填充服务。

## 先决条件

在通用编辑器中使用表单数据模型配置表单之前，请确保已完成以下步骤：

* [配置数据Source](/help/forms/configure-data-sources.md)：设置数据源以将表单连接到后端数据。
* [创建表单数据模型(FDM)](/help/forms/create-form-data-models.md)：使用配置的数据源中的数据对象和服务构建数据模型。
* [配置数据模型对象和服务](/help/forms/work-with-form-data-model.md)：映射数据模型对象和服务，以确保表单和数据源之间的数据流畅无阻。

## 在通用编辑器中使用表单数据模型创建Forms

在通用编辑器中，您可以创建：
* [基于架构的表单](#schema-based-form)：基于架构的表单使用在&#x200B;**数据**&#x200B;选项卡中创建表单期间配置的数据源，自动将数据绑定到表单字段。
* [非基于架构的表单](#non-schema-based-form)：非基于架构的表单要求您手动添加数据源并绑定内容树中的每个字段。

通用编辑器中的![表单类型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

这些方法让您能够根据自己的需求，灵活地将数据模型与表单连接起来。

### 基于架构的表单

创建基于架构的表单时，会自动为其配置数据源，并且表单字段已通过数据绑定链接到数据。 要使用“表单创建”向导创建基于架构的表单，请执行以下步骤：

1. 登录到您的[!DNL Experience Manager Forms]创作实例。
2. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
3. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。 向导随即打开。在&#x200B;**Source**&#x200B;选项卡中，选择一个模板：

   ![Edge Delivery Services模板](/help/edge/assets/create-eds-forms.png)

   当您选择基于Edge Delivery Services的模板时，将启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。 您可以转到&#x200B;**[!UICONTROL 数据Source]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡以选择数据源或提交操作。

4. 在&#x200B;**数据**&#x200B;选项卡中，您可以选择以下数据模型之一：

   * **表单数据模型(FDM)**：将数据模型对象和服务从数据源集成到表单中。 如果您的表单需要从多个源读取和写入数据，请选择表单数据模型(FDM)。

   * **JSON架构**：通过关联定义数据结构的JSON架构，将表单与后端系统集成。 它允许您使用架构元素添加动态内容。

     例如，选择已创建的名为Pet表单数据模型的表单数据模型。

     ![选择表单数据模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     默认情况下，关联JSON架构或表单数据模型(FDM)的所有字段都会被自动选择并转换为相应的表单组件，从而简化创作过程。 该向导还允许您使用复选框有选择地选择要包含在表单中的字段。

5. 单击&#x200B;**[!UICONTROL 创建]**，将出现&#x200B;**创建表单**&#x200B;向导。
6. 指定&#x200B;**名称**&#x200B;和&#x200B;**标题**。
7. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 `edsforms`，则它位于帐户 `wkndforms` 下，其 URL 为：
   `https://github.com/wkndforms/edsforms`
8. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建基于架构的表单](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

   ![创作表单](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   使用来自关联数据源的数据元素创建表单，表单字段具有预配置的数据绑定。

   ![自动数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您现在可以为表单添加和[配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

### 不基于架构的表单

创建非基于架构的表单时，不会配置数据源。 您可以稍后编辑表单属性，以添加数据源并手动配置表单字段的数据绑定。 执行以下步骤以编辑表单属性并添加数据源：

1. 登录到您的[!DNL Experience Manager Forms]创作实例。
1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择要为其添加数据源的表单，然后单击&#x200B;**[!UICONTROL 属性]**。
   ![打开表单属性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   表单属性打开。
1. 单击以打开&#x200B;**表单模型**&#x200B;选项卡，并从&#x200B;**从**&#x200B;下拉菜单中选择。 您可以选择以下选项之一：

   * **表单数据模型(FDM)**：使用表单数据模型创建表单。
   * **连接器**：使用Adobe Marketo数据源创建表单。
   * **架构**：使用上传到AEM Forms的JSON架构创建表单。
   * **无**：从头开始创建表单，而不使用任何表单模型。

     例如，选择表单数据模型(FDM)

     ![选择表单模型选项卡](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. 从下拉列表中选择已创建的表单数据模型(FDM)。 例如，从下拉列表中选择已创建的名为Pet表单数据模型的表单数据模型。

   ![选择FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   选择表单数据模型(FDM)时，将显示警告对话框。 单击&#x200B;**确定**&#x200B;关闭对话框。

   ![表单模型向导](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。
1. 打开表单进行编辑。 该表单将在通用编辑器中打开以进行创作。

   ![不基于架构的表单创作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   关联表单数据模型(FDM)中存在的表单元素显示在&#x200B;**属性面板**&#x200B;的&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中。

   ![表单数据Source](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 从&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中选择数据元素，然后单击&#x200B;**[!UICONTROL 添加]**。

   ![添加数据元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   您还可以拖放这些元素来构建自适应表单。 单击&#x200B;**[!UICONTROL 添加]**&#x200B;后，从&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡中选择的元素将添加到您的表单中，并且添加的元素前面会出现一个勾号。

   ![生成表单](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   您必须在表单元素的&#x200B;**绑定引用**属性中指定数据绑定，以手动将其添加到表单元素。
例如，我们为表单中已存在的**Pet名称**&#x200B;文本框添加一个数据绑定引用：

   ![手动添加表单字段的数据](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   您现在可以为表单添加和[配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

## 另请参阅

{{universal-editor-see-also}}
