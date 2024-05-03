---
title: 如何创建自适应表单？
description: 通过我们的分步教程了解如何创建移动响应式自适应表单。这些表单可以跨设备无缝适应，从而确保流畅体验。
keywords: 自适应Forms、响应式Forms、HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: 6f1c3fe7-b61e-47ce-b565-15b4904db092
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 77%

---

# 创建自适应表单 {#creating-an-adaptive-form}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service | 本文 |

自适应表单使您能够创建引人入胜、响应式、动态和自适应的表单。AEM Forms 提供便于企业用户使用的向导以快速创建自适应表单。该向导可快速地在选项卡之间导航，从而轻松地选择预先配置的模板、样式、字段和提交选项以创建自适应表单。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png){width="100%" align="center"}

在开始之前，了解可使用的表单组件类型：

* [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化的数据捕获组件。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。开发人员可以轻松地自定义这些组件并设置其样式。您可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 以查看可用核心组件的实际操作&#x200B;**Adobe 建议使用这些现代的、可扩展组件来开发自适应表单**。

* [自适应表单基础组件](creating-adaptive-form.md)：这些是经典（旧版）数据捕获组件。您可以继续使用这些组件来编辑您现有的基于基础组件的自适应表单。如果您正在创建新表单，Adobe 建议使用[用于创建自适应表单的自适应表单核心组件](#create-an-adaptive-form-core-components)。

>[!BEGINTABS]

>[!TAB 使用核心组件创建自适应表单（推荐）]

您需要以下项来创建自适应表单：

* **为您的环境启用自适应Forms核心组件**：在创建项目时，已为您的环境启用自适应Forms核心组件。 如果您有基于 Archetype 39 或更早版本的 Forms as a Cloud Service 环境，请[为您的环境启用自适应表单核心组件](enable-adaptive-forms-core-components.md)。在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（版面和样式）。它的预格式化的组件包含某些属性和内容结构。它还提供用于定义主题和提交操作的选项。主题定义外观，提交操作定义在提交自适应表单时执行的操作。例如，将收集到的数据发送到数据源。Cloud Service 提供一个名为 blank 的 OOTB 模板：

   * `blank` 模板包含在每个新的 AEM Forms as a Cloud Service 项目中。
   * 您可以通过包管理器安装参考包，以将 `blank` 模板添加到 AEM Forms as a Cloud Service 项目。
   * 您还可以 [创建自适应Forms模板（核心组件）](template-editor.md) 从头开始。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。`Canvas` 模板包含在每个新的 AEM Forms as a Cloud Service 项目中。
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**：将用户添加到[!DNL forms-users]组。[!DNL forms-users]组的成员具有创建自适应表单的权限。有关特定于表单的用户组的详细列表，请参阅[组和权限](forms-groups-privileges-tasks.md)。


## 创建自适应表单 {#create-an-adaptive-form-core-components}

1. 登录到 [!DNL Experience Manager Forms] 创作实例。它可以是云实例或本地开发实例。

1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 选择 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 向导随即打开。在“源”选项卡中，选择一个模板：

   ![核心组件模板](/help/forms/assets/core-components-template.png){width="100%" align="center"}

   选择一个模板时，会自动选择该模板中指定的主题和提交操作，并启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡以选择不同的主题或提交操作。如果所选模板未指定主题，则“创建”按钮将保持禁用状态。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡以手动选择主题。

   >[!NOTE]
   >
   >
   > 如果环境中没有&#x200B;**自适应表单（核心组件）**&#x200B;模板，请[为您的环境启用自适应表单核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。在为您的环境启用核心组件时，会将&#x200B;**自适应表单（核心组件）**&#x200B;模板添加到您的环境。

1. 在&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡中，选择一个主题：

   * 如果所选模板指定了一个主题，该主题将在向导中自动选定。您还可以从“样式”选项卡中选择其他主题。

   * 如果所选模板未指定主题，您可以使用“样式”选项卡选择主题。**[!UICONTROL 创建]**&#x200B;按钮仅在选择主题后启用。

1. （可选）在“数据”选项卡中，选择一个数据模型：

   * **表单数据模型**：A [表单数据模型(FDM)](data-integration.md) 允许您将实体和服务从不同的数据源集成到自适应表单中。 如果要创建的自适应表单涉及从多个数据源获取数据以及将数据写入多个数据源，请选择表单数据模型(FDM)。

   * **JSON 架构**：[JSON 架构](adaptive-form-json-schema-form-model.md)我们的基于核心组件的自适应表单允许与组织的后端系统无缝集成，并能够与表示正在生成或使用的数据结构的 JSON 架构关联。利用此关联，作者可以使用架构的元素将内容动态添加到自适应表单。在创作过程中，架构的元素可在内容浏览器的数据模型对象选项卡中轻松访问，并且所有字段都会自动添加到任何创建的自适应表单中。

   默认情况下，关联的 JSON 架构的所有字段都将自动选定并转换为相应的自适应表单组件，从而简化创作过程。该向导可让您使用复选框选择性地选定应包含在自适应表单中的字段，更加方便。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，选择提交操作：

   * 选择一个模板时，该模板中指定的提交操作将自动选定。您可以从“提交”选项卡中选择其他提交操作。**[!UICONTROL 提交]**&#x200B;选项卡显示所有可用的提交操作。

   * 如果所选模板未指定提交操作，您可以使用&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡来选择提交操作

1. （可选）在&#x200B;**[!UICONTROL 交付]**&#x200B;选项卡中，您可以为自适应表单指定发布或取消发布日期。

1. 选择&#x200B;**[!UICONTROL 创建]**。将出现一个对话框，用于指定标题、名称和位置以保存自适应表单：

   * **[!UICONTROL 标题]**：指定表单的显示名称。标题可帮助您在 [!DNL Experience Manager Forms] 用户界面中标识表单。
   * **[!UICONTROL 名称：]**&#x200B;指定表单的名称。在存储库中创建具有指定名称的节点。在开始键入标题时，名称字段的值将自动生成。您可以更改建议的值。名称字段只能包含字母数字字符、连字符和下划线。所有无效的输入都将替换为连字符。
   * **[!UICONTROL 路径：]**&#x200B;指定用于保存自适应表单的位置。您可以直接将自适应表单保存在 `/content/dam/formsanddocuments`，也可以创建一个文件夹（例如 `/content/dam/formsanddocuments/adaptiveforms`）来保存自适应表单。确保先创建文件夹，然后再在路径中使用它。**[!UICONTROL 路径]**&#x200B;字段不会自动创建文件夹。

1. 选择&#x200B;**[!UICONTROL 创建]**。自适应表单将创建并在自适应表单编辑器中打开。该编辑器显示模板中可用的内容。根据自适应表单的类型，关联表单中存在的表单元素 <!--XFA form template, XML schema or --> JSON架构或表单数据模型(FDM)显示在 **[!UICONTROL 数据模型对象]** 选项卡 **[!UICONTROL 内容浏览器]** 在侧栏中。

现在，您可以拖放[自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans#components)或架构元素来生成自适应表单。


## 编辑自适应表单的表单模型属性 {#edit-form-model-core-components-based-adaptive-forms}

1. 选择自适应表单，然后选择 ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**. 这将打开“表单属性”页面。

1. 转到&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡并选择表单模型。如果自适应表单没有表单模型，您可以自由选择JSON架构或表单数据模型(FDM)。 另一方面，如果自适应表单已基于一个表单模型，则可以选择切换到另一个相同类型的表单模型。例如，如果表单使用JSON架构，您可以轻松切换到另一个JSON架构，同样，如果表单使用表单数据模型(FDM)，您可以切换到另一个表单数据模型(FDM)。

1. 选择 **[!UICONTROL 保存]** 以保存属性。

>[!TAB 使用基础组件创建自适应表单]

您需要以下项来创建自适应表单：

* **权限**：将用户添加到[!DNL forms-users]，为他们提供创建自适应表单的权限。有关特定于表单的用户组的详细列表，请参阅[组和权限](forms-groups-privileges-tasks.md)。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。您可以 [创建主题](themes.md) 或 [导入现有主题](import-export-forms-templates.md#uploading-a-theme). 您还可以为一些示例主题部署[最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project)。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（版面和样式）。它的预格式化的组件包含某些属性和内容结构。它还提供用于定义主题和提交操作的选项。主题定义外观，提交操作定义在提交自适应表单时执行的操作。例如，将收集到的数据发送到数据源。Cloud Service 支持两种类型的模板：

   * **可编辑的模板**：您可以 [创建](template-editor.md) 或 [导入现有的可编辑模板](migrate-to-forms-as-a-cloud-service.md). 您还可以部署[最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=zh-Hans#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.)以获取一些可编辑模板示例。

   * **静态模板**：这些是旧版模板，仅建议从 Adobe Managed Services (AMS) 和内部部署 AEM Forms 安装（AEM 6.5 Forms 或更早版本）迁移的客户使用。它们可让您继续使用投资购买的现有静态模板。创建自适应表单时，请使用可编辑的模板。


## 创建自适应表单 {#create-an-adaptive-form-foundation-components}

1. 访问 [!DNL Experience Manager Forms] 创作实例。它可以是云实例或本地开发实例。

1. 在 Experience Manager 登录页面上输入您的凭据。

   登录后，在左上角选择 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 选择 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 向导随即打开。
1. 在“源”选项卡中，选择一个模板：

   * 选择一个可编辑模板时，会自动选择该模板中指定的主题和提交操作，并启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡以选择不同的主题或提交操作。如果所选可编辑模板未指定主题，则“创建”按钮将保持禁用状态。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡以手动选择主题。

     >[!NOTE]
     >
     > 您还可以使用自适应表单编辑器创建[!UICONTROL 记录文档]模板。有关更多信息，请参阅[自适应表单编辑器中的记录文档支持](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)。

   * 选择静态模板时，数据、样式、提交、交付和预览选项将不可用。创建自适应表单时，建议使用可编辑的模板。

1. 在&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡中，选择一个主题：

   * 如果所选模板指定了一个主题，该主题将在向导中自动选定。您还可以从“样式”选项卡中选择其他主题。
   * 如果所选模板未指定主题，您可以使用“样式”选项卡选择主题。**[!UICONTROL 创建]**&#x200B;按钮仅在选择主题后启用。

1. （可选）在&#x200B;**[!UICONTROL 数据]**&#x200B;选项卡中，选择一个数据模型：

   * **表单数据模型**：A [表单数据模型(FDM)](data-integration.md) 允许您将实体和服务从不同的数据源集成到自适应表单中。 如果要创建的自适应表单涉及从多个数据源获取数据以及将数据写入多个数据源，请选择表单数据模型(FDM)。

   * **JSON 架构**：[JSON 架构](adaptive-form-json-schema-form-model.md)表示组织中的后端系统生成或使用的数据所在的结构。您可以将架构与自适应表单相关联，并使用其元素将动态内容添加到自适应表单。在创作自适应Forms时，可在内容浏览器的数据模型对象选项卡中使用架构的元素，并且所有字段也已添加到创建的自适应表单。

   默认情况下，将选定数据模型的所有字段。在创建自适应表单时，所有选定的数据模型字段将转换为相应的自适应表单组件。该向导中的复选框可让您仅选择那些应包含在自适应表单中的字段。

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，选择提交操作：

   * 选择一个模板时，该模板中指定的提交操作将自动选定。您可以从“提交”选项卡中选择其他提交操作。**[!UICONTROL 提交]**&#x200B;选项卡显示所有可用的提交操作。

   * 如果所选模板未指定提交操作，您可以使用&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡来选择提交操作

1. （可选）在“交付”选项卡中，您可以为自适应表单指定发布或取消发布日期。

1. 选择&#x200B;**[!UICONTROL 创建]**。将出现一个对话框，用于指定标题、名称和位置以保存自适应表单：

   * **[!UICONTROL 标题]**：指定表单的显示名称。标题可帮助您在 [!DNL Experience Manager Forms] 用户界面中标识表单。
   * **[!UICONTROL 名称：]**&#x200B;指定表单的名称。在存储库中创建具有指定名称的节点。在开始键入标题时，名称字段的值将自动生成。您可以更改建议的值。名称字段只能包含字母数字字符、连字符和下划线。所有无效的输入都将替换为连字符。
   * **[!UICONTROL 路径：]**&#x200B;指定用于保存自适应表单的位置。您可以直接将自适应表单保存在 `/content/dam/formsanddocuments`，也可以创建一个文件夹（例如 `/content/dam/formsanddocuments/adaptiveforms`）来保存自适应表单。确保先创建文件夹，然后再在路径中使用它。**[!UICONTROL 路径]**&#x200B;字段不会自动创建文件夹。

1. 选择&#x200B;**[!UICONTROL 创建]**。自适应表单将创建并在自适应表单编辑器中打开。该编辑器显示模板中可用的内容。它还会显示侧栏，以根据需要自定义创建的表单。

   根据自适应表单的类型，关联表单中存在的表单元素 <!--XFA form template, XML schema or --> JSON架构或表单数据模型(FDM)显示在 **[!UICONTROL 数据模型对象]** 选项卡 **[!UICONTROL 内容浏览器]** 在侧栏中。 您还可以拖放这些元素来生成自适应表单。

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Select to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, select on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Select **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and select Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model2). -->

## 编辑自适应表单的表单模型属性 {#edit-form-model-foundation-components}

您可以更改自适应表单的表单模型(基于JSON或表单数据模型(FDM))。 您无法从一种表单模型更改为另一种表单模型。

1. 选择自适应表单，然后选择 **属性** 图标。
1. 打开&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡并执行下列操作之一。

   * 如果自适应表单没有表单模型，则可以选择其他表单模型并相应地选择 <!-- a form template, --> XML或JSON架构，或表单数据模型(FDM)。
   * 如果自适应表单基于表单模型，则可以选择其他 <!-- form template, --> XML或JSON架构，或相同表单模型的表单数据模型(FDM)。

1. 选择 **[!UICONTROL 保存]** 以保存属性。

您还可以在自适应表单编辑器或自适应表单模板编辑器中修改表单模型属性。

1. 选择&#x200B;**[!UICONTROL 自适应表单容器（根）]**&#x200B;组件。
1. 单击![配置](/help/forms/assets/configure-icon.svg)图标来打开自适应表单容器的&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 数据模型]**&#x200B;选项卡并执行下列操作之一：

   * 如果自适应表单没有表单模型，则可以选择表单模型并相应地选择 <!-- a form template, --> XML或JSON架构，或表单数据模型(FDM)。
   * 如果自适应表单基于表单模型，则无法更改表单模型。您可以选择其他 <!-- form template, --> 适用时，适用于相同表单模型的XML或JSON架构或表单数据模型(FDM)。
1. 选择 ![保存](/help/forms/assets/check-button.png) 以保存属性。

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png){width="100%" align="center"}

>[!NOTE]
>
> 您还可以将自适应表单另存为模板。有关更多信息，请参阅[使用自适应表单创建模板](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template)。

>[!ENDTABS]


## 后续步骤

* [将 Adobe Sign 与 Forms 结合使用](working-with-adobe-sign.md)
* [将 Google reCaptcha 与 Forms 结合使用](captcha-adaptive-forms.md)
* [将可重复部分添加到表单](create-forms-repeatable-sections.md)
* [预填充表单字段](prepopulate-adaptive-form-fields.md)

>[!MORELIKETHIS]
>
>* [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
