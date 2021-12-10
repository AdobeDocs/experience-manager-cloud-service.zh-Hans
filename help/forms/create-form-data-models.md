---
title: 如何创建表单数据模型？
description: Experience Manager Forms数据集成提供了直观的用户界面，用于创建和使用表单数据模型。 了解如何使用或不使用配置的数据源来创建表单数据模型。
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# 创建表单数据模型 {#create-form-data-model}

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 数据集成提供了直观的用户界面，用于创建和使用表单数据模型。 表单数据模型依赖于数据源来交换数据；但是，无论是否具有数据源，您都可以创建表单数据模型。 根据您是否配置了数据源，可以通过两种方法来创建来自数据模型：

* **使用预配置的数据源**:如果您已按照 [配置数据源](configure-data-sources.md)，则可在创建表单数据模型时选择它们。 它从可用于表单数据模型的选定数据源中引入所有数据模型对象、属性和服务。

* **没有数据源**:如果尚未为表单数据模型配置数据源，则仍然可以在没有数据源的情况下创建它。 您可以使用表单数据模型创作自适应Forms <!--and interactive communication--> 然后用样本数据测试。 当数据源可用时，您可以将表单数据模型与数据源绑定，该数据源会自动反映在关联的自适应Forms中<!--and interactive communications-->.

>[!NOTE]
>
>您必须是这两者的成员 **fdm-author** 和 **forms-user** 群组，以便能够创建和使用表单数据模型。 联系您的 [!DNL Experience Manager] 管理员成为组的成员。

## 创建表单数据模型 {#data-sources}

确保已按照 [配置数据源](configure-data-sources.md). 请执行以下操作，以根据配置的数据源创建表单数据模型：

1. 在 [!DNL Experience Manager] 创作实例，导航到 **[!UICONTROL Forms >数据集成]**.
1. 点按 **[!UICONTROL 创建>表单数据模型]**.
1. 在创建表单数据模型对话框中：

   * 指定表单数据模型的名称。
   * (**可选**)为表单数据模型指定标题、描述和标记。
   * (**仅当配置了数据源时，才可选且适用**)点按 **[!UICONTROL 数据源配置]** 字段，然后选择云服务所在的配置节点。 它将下一页可供选择的数据源列表限制为选定配置节点中可用的数据源列表。 但是，任何JDBC数据库和 [!DNL Experience Manager] 默认情况下，会列出用户配置文件数据源。 如果不选择配置节点，则会列出来自所有配置节点的数据源。

1. 点按 **[!UICONTROL 下一个]**.

1. (**仅在配置数据源时适用**) **[!UICONTROL 选择数据源]** 屏幕会列出可用的数据源（如果有）。 选择要在表单数据模型中使用的数据源。
1. 点按 **[!UICONTROL 创建]** 在确认对话框上，点按 **[!UICONTROL 打开]** 打开表单数据模型编辑器。

   让我们查看表单数据模型编辑器UI的不同组件。

   ![具有三个数据源的表单数据模型 — RESTful服务， [!DNL Experience Manager] 用户配置文件和RDBMS。](assets/fdm-ui.png)

   A. **[!UICONTROL 数据源]** 列出表单数据模型中的数据源。 展开数据源以查看其数据模型对象和服务。

   B. **[!UICONTROL 刷新数据源定义]** 从已配置的数据源中获取数据源定义中的任何更改，并在表单数据模型编辑器的“数据源”选项卡中对其进行更新。

   C. **[!UICONTROL 模型]** 显示已添加数据模型对象的内容区域。

   D. **[!UICONTROL 服务]** 显示添加数据源操作或服务的内容区域。

   E. **[!UICONTROL 工具栏]** 用于处理表单数据模型的工具。 工具栏根据表单数据模型中的选定对象显示更多选项。

   F. **[!UICONTROL 添加选定项]** 将所选数据模型对象和服务添加到表单数据模型。

有关表单数据模型编辑器以及如何使用它编辑和配置表单数据模型的更多信息，请参阅 [使用表单数据模型](work-with-form-data-model.md).

## 更新数据源 {#update}

执行以下操作，以向现有表单数据模型添加或更新数据源。

1. 转到 **[!UICONTROL Forms >数据集成]**，选择要在其中添加或更新数据源的表单数据模型，然后点按 **[!UICONTROL 属性]**.
1. 在表单数据模型属性中，转到 **[!UICONTROL 更新源]** 选项卡。

   在 **[!UICONTROL 更新源]** 选项卡：

   * 点按 **[!UICONTROL 上下文感知配置]** 字段，然后选择要添加的数据源的云配置所在的配置节点。 如果您没有选择节点，则云配置仅驻留在 `global` 点按时会列出节点 **[!UICONTROL 添加源]**.

   * 要添加新数据源，请点按 **[!UICONTROL 添加源]** 并选择要添加到表单数据模型的数据源。 在中配置的所有数据源 `global` 将显示选定的配置节点（如果有）。

   * 要将现有数据源替换为同类型的其他数据源，请点按 **[!UICONTROL 编辑]** 图标，然后从可用数据源列表中选择。
   * 要删除现有数据源，请点按 **[!UICONTROL 删除]** 图标。 如果在表单数据模型中添加数据源中的数据模型对象，则会禁用“删除”图标。

      ![fdm-properties](assets/fdm-properties.png)

1. 点按 **[!UICONTROL 保存并关闭]** 以保存更新。

>[!NOTE]
>
>在表单数据模型中添加新数据源或更新现有数据源后，请确保在自适应Forms中（视情况而定）更新绑定引用<!--and interactive communications--> 使用更新的表单数据模型的报表包。

## 下面的步骤 {#next-steps}

现在，您有一个表单数据模型，其中添加了数据源。 接下来，您可以编辑表单数据模型以添加和配置数据模型对象和服务、添加数据模型对象之间的关联、编辑属性、添加自定义数据模型对象和属性、生成示例数据等。

有关更多信息，请参阅 [使用表单数据模型](work-with-form-data-model.md).
