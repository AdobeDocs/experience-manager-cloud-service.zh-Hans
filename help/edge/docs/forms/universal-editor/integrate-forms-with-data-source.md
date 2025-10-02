---
title: 如何在通用编辑器中为一个表单集成表单数据模型 (FDM)？
description: 了解如何基于表单数据模型 (FDM) 为 Edge Delivery Services 创建表单。在 FDM 中生成并编辑数据模型对象的样本数据。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 7d3ea5bdc6545b9610f595660fcfb2ef70c837de
workflow-type: ht
source-wordcount: '716'
ht-degree: 100%

---


# 将表单与表单数据模型 (FDM) 集成

通过 FDM 将您的表单与后端数据源连接，以启用数据绑定、验证和提交工作流。

## 先决条件

将 FDM 与您的表单集成之前，先完成以下步骤：

1. **[配置数据源](/help/forms/configure-data-sources.md)**：设置后端连接
2. **[创建表单数据模型](/help/forms/create-form-data-models.md)**：定义数据结构和服务
3. **[配置数据模型对象](/help/forms/work-with-form-data-model.md)**：映射数据关系

## 注意事项

如果您在通用编辑器界面中看不到&#x200B;**数据源**&#x200B;图标，或者在右侧属性面板中看不到&#x200B;**绑定引用**&#x200B;属性，就请在&#x200B;**扩展管理器**&#x200B;中启用&#x200B;**数据源**&#x200B;扩展。

![通用编辑器扩展管理器界面截图，说明了可用的扩展项，包括可用于支持表单集成的数据源扩展](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

请参阅[扩展管理器功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用编辑器中启用和禁用扩展。

## 选择您的表单类型

通用编辑器支持两种表单创建方法：

| 方面 | 基于架构的表单 | 非基于架构的表单 |
|--------|-------------------|----------------------|
| **设置复杂性** | 简单（自动绑定） | 手动（逐个字段绑定） |
| **用例** | 明确定义了数据结构的新表单 | 现有表单或要求灵活 |
| **数据源** | 创建过程中必需 | 可以后期添加 |
| **绑定** | 字段自动绑定 | 每个字段手动绑定 |

![通用编辑器中的表单类型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## 基于架构的表单

基于架构的表单会自动配置数据源，并将表单字段与数据绑定。这种方法特别适用于具有明确定义的数据结构的新表单。

### 创建基于架构的表单

1. **访问表单控制台**
   - 登录您的 [!DNL Experience Manager Forms] 作者实例
   - 导航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**

2. **开始创建表单**
   - 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**
   - 选择一个 Edge Delivery Services 模板
   - 启用后，点击&#x200B;**[!UICONTROL 创建]**

   ![Edge Delivery Services 模板](/help/edge/assets/create-eds-forms.png)

3. **配置数据模型**
   - 前往&#x200B;**数据**&#x200B;选项卡
   - 为多个数据源选择&#x200B;**表单数据模型 (FDM)**，为单个后端系统选择 **JSON 架构**
   - 选择您创建的 FDM（例如，宠物表单数据模型）

   ![选择表单数据模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **完成表单设置**
   - 输入&#x200B;**名称**&#x200B;和&#x200B;**标题**
   - 指定 **GitHub URL**（例如 `https://github.com/wkndforms/edsforms`）
   - 单击&#x200B;**[!UICONTROL 创建]**

   ![创建基于架构的表单](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### 验证基于架构的表单

表单在通用编辑器中打开，并带有预先配置的数据绑定：

![通用编辑器界面截图，展示了一个基于数据架构的表单，包含预填充的表单字段，内容浏览器中列出了可用的数据源元素](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![自动数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 非基于架构的表单

非架构表单需要手动进行数据源配置和字段绑定。这种方法为现有表单或要求复杂的情况提供了灵活性。

### 创建非基于架构的表单

1. **访问表单属性**
   - 登录您的 [!DNL Experience Manager Forms] 作者实例
   - 导航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**
   - 选择表单，然后点击&#x200B;**[!UICONTROL 属性]**

   ![打开表单属性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **配置表单模型**
   - 打开&#x200B;**表单模型**&#x200B;选项卡
   - 从&#x200B;**选择表单**&#x200B;下拉菜单中选择&#x200B;**表单数据模型 (FDM)**
   - 从列表中选择您的 FDM

   ![选择表单模型选项卡](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![选择 FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **确认配置**
   - 在警告对话框中点击 **OK**
   - 点击&#x200B;**[!UICONTROL 保存并关闭]**

   ![表单模型向导](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### 添加数据元素

1. **打开表单进行编辑**
   - 表单在通用编辑器中打开

   ![非基于架构的表单创作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **访问数据源元素**
   - 在&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;中前往&#x200B;**[!UICONTROL 数据源]**&#x200B;选项卡
   - 查看 FDM 中可用的数据元素

   ![表单数据源](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **将元素添加到表单**
   - 选择数据元素，然后点击&#x200B;**[!UICONTROL 添加]**
   - 或者拖放元素来构建表单

   ![添加数据元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![通用编辑器界面截图，展示了用户正在构建一个非架构表单，从“数据源”选项卡中拖放数据元素到表单结构中](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### 添加手动数据绑定

对于现有的表单字段，通过&#x200B;**绑定引用**&#x200B;属性添加数据绑定：

1. **打开字段属性**
   - 选择要绑定的表单字段
   - 打开其属性面板

2. **配置绑定引用**
   - 前往&#x200B;**绑定引用**&#x200B;属性
   - 点击&#x200B;**浏览**&#x200B;图标

   ![将数据绑定手动添加到一个表单字段](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **选择数据元素**
   - 在&#x200B;**选择绑定引用**&#x200B;向导中，从数据源树中选择
   - 选择所需的数据元素，然后点击&#x200B;**选择**

   ![选择数据绑定引用](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![选择数据元素](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)。

4. **验证绑定**
   - 表单字段现在与此数据元素绑定
   - 此绑定显示在&#x200B;**绑定引用**&#x200B;属性中

   ![自动数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 验证集成

完成集成后：

1. **测试数据绑定**：验证表单字段显示正确的数据
2. **验证提交**：确保数据保存到所配置的源
3. **检查错误处理方法**：使用无效数据场景进行测试

## 后续步骤

配置[提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)，完成您的表单工作流。
