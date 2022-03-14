---
title: 如何创建自适应表单？
description: '了解如何使用 [!DNL Experience Manager Forms]. 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。 '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 创建自适应表单 {#creating-an-adaptive-form}

自适应Forms让您能够创建有吸引力的响应式、动态且自适应的表单。 [!DNL AEM Forms] 提供了直观的用户界面和现成的组件，用于创建和使用自适应Forms。 您可以选择基于表单模型或架构创建自适应表单，也可以不使用表单模型创建自适应表单。 必须仔细选择不仅适合您的要求，而且扩展您现有的基础设施投资和资产的表单模式。 您可以从以下选项中进行选择，以创建自适应表单：

* **使用表单数据模型**
   [数据集成](data-integration.md) 允许您将来自不同数据源的实体和服务集成到表单数据模型中，以用于创建自适应Forms。 如果要创建的自适应表单涉及从多个数据源获取数据和将数据写入多个数据源，请选择表单数据模型。

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **使用XML架构定义(XSD)或JSON架构**
XML和JSON架构表示组织内的后端系统生成或使用数据的结构。 您可以将架构与自适应表单相关联，并使用其元素向自适应表单添加动态内容。 创作自适应Forms时，架构的元素将可用在内容浏览器的“数据模型对象”选项卡中。

* **不使用表单模型或不使用表单模型**
使用此选项创建的自适应Forms不使用任何表单模型。 从这种表单生成的数据XML具有平坦结构，其中具有字段和相应的值。

## 先决条件

您需要满足以下条件才能创建自适应表单：

* 自适应表单模板。 模板提供了基本结构并定义了自适应表单的外观（布局和样式）。 它包含预格式化的组件，其中包含某些属性和内容结构您可以 [创建新模板](template-editor.md)、导入现有模板，或下载并导入一些 [示例模板](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52).
* 自适应表单主题。 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式将反映在相应的组件上。 您可以 [创建新主题](themes.md), [导入现有主题](import-export-forms-templates.md#uploading-a-theme)，或下载或导入某些 [示例主题](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25).
* 将用户添加到 [!DNL forms-users] 以向他们提供创建自适应表单的权限。 有关特定用户群组的表单的详细列表，请参阅 [群组和权限](forms-groups-privileges-tasks.md).

## 创建自适应表单 {#strong-create-an-adaptive-form-strong}

按照以下步骤创建自适应表单。

1. 访问 [!DNL Experience Manager Forms] 创作实例。 它可以是云实例或本地开发实例。

1. 在Experience Manager登录页面上输入凭据。

   登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]** 选择 **[!UICONTROL 自适应表单]**. 选择模板并点按 **[!UICONTROL 下一个]**.
1. 选项 **[!UICONTROL 添加属性]** 中。 指定以下属性字段的值。 标题和名称字段是必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。 标题可帮助您在 [!DNL Experience Manager Forms] 用户界面。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。
   * **[!UICONTROL 描述：]** 指定有关表单的详细信息。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在 **[!UICONTROL 标记]** 框中。

1. 您可以基于以下任一表单模型创建自适应表单：

   * [表单数据模型](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [XML或JSON架构](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 无或没有任何表单模型

   您可以在 **[!UICONTROL 表单模型]** 选项卡 **[!UICONTROL 添加属性]** 页面。 默认情况下，所选的表单模型为 **[!UICONTROL 无]**.

1. 点按&#x200B;**[!UICONTROL 创建]**。随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。

1. 点按 **[!UICONTROL 打开]** 在新选项卡中打开新创建的表单。 此时将打开表单进行编辑，并显示模板中可用的内容。 它还会显示侧栏，以根据需要自定义新创建的表单。

   根据自适应表单的类型，关联 <!--XFA form template, -->XML架构或JSON架构显示在 **[!UICONTROL 数据模型对象]** 选项卡 **[!UICONTROL 内容浏览器]** 中。 您还可以拖放这些元素以构建自适应表单。

## 基于表单数据模型创建自适应表单 {#fdm}

[数据集成](data-integration.md) 允许您集成多个数据源，并将其实体和服务整合在一起，以创建表单数据模型。 它是JSON模式的扩展。 您可以使用表单数据模型创建自适应表单。 在表单数据模型中配置的实体或数据模型对象可用作表单创作的数据模型对象。 它们绑定到相应的数据源，用于预填表单并将提交的数据写回相应的数据源。 您还可以使用自适应表单规则调用在表单数据模型中配置的服务。

要使用表单数据模型创建自适应表单，请执行以下操作：

1. 在“添加属性”屏幕上的“表单模型”选项卡中，选择 **[!UICONTROL 表单数据模型]** 在 **[!UICONTROL 选择自]** 下拉列表。

   ![创建自适应表单](assets/create-af-1-1.png)

1. 点按以展开 **[!UICONTROL 选择表单数据模型]**. 将列出所有可用的表单数据模型。从数据模型中选择。

>[!NOTE]
>
>您还可以更改自适应表单的表单数据模型。 有关详细步骤，请参阅 [编辑自适应表单的表单模型属性](#edit-form-model).

## 基于XML或JSON架构创建自适应表单 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON架构表示组织内的后端系统生成或使用数据的结构。 您可以将架构与自适应表单相关联，并使用其元素向自适应表单添加动态内容。 架构的元素位于内容浏览器的“数据模型对象”选项卡中，用于创作自适应Forms。 您可以拖放架构元素以构建表单。

请参阅以下文档，了解如何设计XML或JSON模式以创作自适应Forms。

* [使用XML架构创建自适应Forms](adaptive-form-xml-schema-form-model.md)
* [使用JSON模式创建自适应Forms](adaptive-form-json-schema-form-model.md)

请执行以下操作以将XML或JSON架构用作自适应表单的表单模型：

1. 在 **[!UICONTROL 添加属性]** 在自适应表单创建页面的步骤中，点按 **[!UICONTROL 表单模型]** 选项卡。
1. 在“表单模型”(Form Model)选项卡中，选择 **[!UICONTROL 架构]** 从 **[!UICONTROL 选择自]** 下拉字段。

1. 点按 **[!UICONTROL 选择架构]** 并执行以下操作之一：

   * **[!UICONTROL 从磁盘上传]**  — 选择此选项，然后点按上传架构定义，以从文件系统浏览并上传XML架构或JSON架构。 上传的架构文件驻留在表单中，其他自适应Forms无法访问该文件。
   * **[!UICONTROL 在存储库中搜索]**  — 选择此选项可从存储库中可用的架构定义文件列表中进行选择。 选择XML或JSON架构文件作为表单模型。 所选架构通过引用与表单关联，并可在其他自适应Forms中使用。

      确保JSON架构文件名以 **.schema.json**. 例如：mySchema.schema.json
   ![选择XML或JSON架构](assets/upload-schema.png)
   **图：** *选择XML或JSON架构*

1. （仅限XML架构）选择或上载XML架构后，请指定要与自适应表单映射的选定XSD文件的根元素。

   ![选择XSD根元素](assets/xsd-root-element.png)
   **图：** *选择XSD根元素*

>[!NOTE]
>
>您还可以更改自适应表单的架构。 有关详细步骤，请参阅 [编辑自适应表单的表单模型属性](#edit-form-model).

## 编辑自适应表单的表单模型属性 {#edit-form-model}

创建自适应Forms时不使用表单模型（对表单模型使用无选项）或使用表单模型(如 <!-- form template, --> XML架构、JSON架构或表单数据模型。 可以将自适应表单的表单模型从“无”更改为其他表单模型。 对于基于表单模型的自适应表单，您可以选择其他 <!-- form template,--> 同一表单模型的XML架构、JSON架构或表单数据模型。 但是，不能将一个表单模型更改为另一个表单模型。

1. 选择自适应表单，然后点按 **属性** 图标。
1. 打开 **[!UICONTROL 表单模型]** ，然后执行以下操作之一。

   * 如果自适应表单没有表单模型，则可以选择其他表单模型并相应地选择 <!-- a form template, --> XML或JSON架构，或表单数据模型。
   * 如果自适应表单基于表单模型，则可以选择其他表单模型 <!-- form template, --> XML或JSON架构，或同一表单模型的表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。
