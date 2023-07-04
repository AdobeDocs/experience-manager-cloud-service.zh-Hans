---
title: 如何创建自适应表单？
description: 通过我们的分步教程了解如何创建移动式自适应Forms。 这些表单可以无缝地跨设备调整，确保流畅的体验。
keywords: 自适应Forms、移动Forms、响应式Forms、HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
source-git-commit: 0efdb9353ef908cf5a655c989ae7be1107c8f3de
workflow-type: tm+mt
source-wordcount: '2849'
ht-degree: 4%

---


# 创建自适应表单 {#creating-an-adaptive-form}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service | 本文 |

通过自适应Forms，您可以创建有吸引力的响应式、动态自适应表单。 AEM Forms为企业提供了便于用户使用的向导，以快速创建自适应Forms。 该向导具有快速选项卡导航，可轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，请了解可供您使用的Forms组件类型：

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化数据捕获组件。 这些组件为您的数字注册体验提供自定义功能、缩短开发时间并降低维护成本。 开发人员可以轻松自定义这些组件并为它们设置样式。 **Adobe建议使用这些现代且可扩展的组件来开发自适应Forms**.

* [自适应Forms Foundation组件](creating-adaptive-form.md)：它们是经典（旧）数据捕获组件。 您可以继续使用这些组件来编辑现有的基于基础组件的自适应表单。 如果要创建新表单，Adobe建议使用  [创建自适应Forms的核心组件Forms](#create-an-adaptive-form-core-components).

![创建自适应表单的向导](/help/release-notes/assets/wizard.png){width="100%" align="center"}


>[!BEGINTABS]

>[!TAB 使用核心组件创建自适应Forms]

## 先决条件 {#pre-requisites-to-create-a-core-components-based-adaptive-form}

创建自适应表单需要满足以下条件：

* **为您的环境启用自适应Forms核心组件**：创建新项目时，已为您的环境启用自适应Forms核心组件。 如果您有一个基于Archetype 39或更早版本的Formsas a Cloud Service环境， [为您的环境启用自适应Forms核心组件](enable-adaptive-forms-core-components.md). 在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有包含特定属性和内容结构的预格式化的组件。 它还提供定义主题和提交操作的选项。 主题定义外观，提交操作定义在提交自适应表单时要执行的操作。 例如，将收集的数据发送到数据源。 Cloud Service提供一个OOTB模板，名称为空：

   * 此 `blank` 所有新的AEM Formsas a Cloud Service计划中都包含模板。
   * 您可以通过包管理器安装参考包，以添加 `blank` 模板添加到您的AEM Formsas a Cloud Service程序。
   * 您还可以 [创建新的自适应Forms模板（核心组件）](template-editor.md) 从头开始。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。  此 `Canvas` 所有新的AEM Formsas a Cloud Service计划中都包含模板。
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**：将您的用户添加到 [!DNL forms-users] 组。 董事会成员 [!DNL forms-users] 组有权创建自适应表单。 有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).


## 创建自适应表单 {#create-an-adaptive-form-core-components}

1. 登录 [!DNL Experience Manager Forms] 创作实例。 它可以是云实例或本地开发实例。

1. 在“Experience Manager登录”页上输入您的凭据。 登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 此时将打开向导。 在源选项卡中，选择一个模板：

   ![核心组件模板](/help/forms/assets/core-components-template.png){width="100%" align="center"}

   选择模板时，将自动选择模板中指定的主题和提交操作，并且 **[!UICONTROL 创建]** 按钮已启用。 您可以转到 **[!UICONTROL 样式]** 或 **[!UICONTROL 提交]** 选项卡以选择不同的主题或提交操作。 如果所选模板未指定主题，则“创建”按钮将保持禁用状态。 您可以转到 **[!UICONTROL 样式]** 选项卡以手动选择主题。

   >[!NOTE]
   >
   >
   > 如果你没有， **自适应Forms（核心组件）** 环境模板， [为您的环境启用自适应Forms核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 在为您的环境启用核心组件时， **自适应Forms（核心组件）** 模板即添加到您的环境中。

1. 在 **[!UICONTROL 样式]** 选项卡，选择一个主题：

   * 当所选模板指定主题时，将在向导中自动选择主题。 您还可以从“样式”选项卡中选择其他主题。

   * 如果所选模板未指定主题，可以使用“样式”选项卡选择主题。 此 **[!UICONTROL 创建]** 按钮仅在选择主题后启用。

1. （可选）在数据选项卡中，选择一个数据模型：

   * **表单数据模型**：A [表单数据模型](data-integration.md) 允许您将实体和服务从不同的数据源集成到自适应表单。 如果要创建的自适应表单涉及从多个数据源获取数据以及将数据写入多个数据源，请选择表单数据模型。

   * **JSON架构**： [JSON架构](adaptive-form-json-schema-form-model.md) 我们的基于核心组件的自适应表单提供关联JSON架构（表示正在生成或使用的数据的结构）的功能，从而允许与贵组织的后端系统无缝集成。 这种关联使作者能够使用架构的元素动态地将内容添加到自适应表单。 在创作过程中，架构的元素可在内容浏览器的数据模型对象选项卡中轻松访问，并且所有字段都会自动添加到任何新创建的自适应表单中。

   默认情况下，会自动选择相关JSON架构的所有字段并将其转换为相应的自适应表单组件，从而简化创作过程。 该向导提供了额外的便利性，允许您通过使用复选框有选择地选择应包含在自适应表单中的字段。

1. 在 **[!UICONTROL 提交]** 选项卡，选择提交操作：

   * 选择模板时，将自动选择模板中指定的提交操作。 您可以从“提交”选项卡中选择其他提交操作。 此 **[!UICONTROL 提交]** 选项卡显示所有可用的提交操作。

   * 当所选模板未指定提交操作时，您可以使用 **[!UICONTROL 提交]** 选项卡以选择提交操作

1. （可选）在 **[!UICONTROL 投放]** 选项卡，您可以为自适应表单指定发布或取消发布日期。

1. 点按 **[!UICONTROL 创建]**. 将显示一个对话框，用于指定保存自适应表单的标题、名称和位置：

   * **[!UICONTROL 标题]** 指定表单的显示名称。 标题可帮助您识别 [!DNL Experience Manager Forms] 用户界面。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成“名称”字段的值。 您可以更改建议值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入均被替换为连字符。
   * **[!UICONTROL 路径：]** 指定保存自适应表单的位置。 您可以直接将自适应表单保存在 `/content/dam/formsanddocuments` 或创建文件夹，例如 `/content/dam/formsanddocuments/adaptiveforms` 以保存自适应表单。 请确保先创建文件夹，然后再在路径中使用它。 此 **[!UICONTROL 路径]** 字段不会自动创建文件夹。

1. 点按 **[!UICONTROL 创建]**. 创建自适应表单，并在自适应Forms编辑器中打开该表单。 编辑器将显示模板中可用的内容。  根据自适应表单的类型，关联表单中显示的表单元素 <!--XFA form template, XML schema or --> JSON架构或表单数据模型显示在 **[!UICONTROL 数据模型对象]** 的选项卡 **[!UICONTROL 内容浏览器]** 在侧栏中。 您还可以拖放这些元素来构建自适应表单。

现在，您可以将自适应Forms核心组件拖放到自适应Forms容器中来设计和创建表单。

## 可用的自适应Forms核心组件 {#available-core-components}

自适应Forms核心组件是标准化的数据捕获组件。 这些组件提供自定义功能，有助于缩短开发时间，并降低数字注册体验的维护成本。 [自适应Forms核心组件文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans) 提供了可用组件的详细列表以及有关每个组件功能的详细信息。 您也可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心组件运行情况。

## 编辑自适应表单的表单模型属性 {#edit-form-model-core-components-based-adaptive-forms}

1. 选择自适应表单并点按 ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg){width="100%" align="center"} > **[!UICONTROL 打开属性]**. 此时将打开“表单属性”页面。

1. 转到 **[!UICONTROL 表单模型]** 选项卡并选择表单模型。 如果自适应表单没有表单模型，您可以自由选择JSON架构或表单数据模型。 另一方面，如果自适应表单已基于表单模型，则可以选择切换到相同类型的另一个表单模型。 例如，如果表单使用JSON架构，您可以轻松切换到另一个JSON架构，同样，如果表单使用表单数据模型，您可以切换到另一个表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。

>[!TAB 使用基础组件创建自适应Forms]

## 先决条件 {#pre-requisites-to-create-a-foundation-components-based-adaptive-form}

创建自适应表单需要满足以下条件：

* **权限**：将您的用户添加到 [!DNL forms-users] 以向他们提供创建自适应表单的权限。 有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).

* **自适应表单主题**：主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。 您可以 [创建新主题](themes.md) 或 [导入现有主题](import-export-forms-templates.md#uploading-a-theme). 您还可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) 一些示例主题。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有包含特定属性和内容结构的预格式化的组件。 它还提供定义主题和提交操作的选项。 主题定义外观，提交操作定义在提交自适应表单时要执行的操作。 例如，将收集的数据发送到数据源。 Cloud Service支持两种类型的模板：

   * **可编辑的模板**：您可以 [新建](template-editor.md) 或 [导入现有的可编辑模板](migrate-to-forms-as-a-cloud-service.md). 您还可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests。) 以获取一些示例可编辑模板。

   * **静态模板**：这些是旧版模板，仅建议从Adobe Managed Services (AMS)和内部部署AEM Forms安装(AEM 6.5 Forms或更低版本)迁移的客户使用。 这些模板允许您继续使用在静态模板中的现有投资。 在创建新的自适应表单时，建议使用可编辑的模板。


## 创建自适应表单 {#create-an-adaptive-form-foundation-components}

1. 访问 [!DNL Experience Manager Forms] 创作实例。 它可以是云实例或本地开发实例。

1. 在“Experience Manager登录”页上输入您的凭据。

   登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 此时将打开向导。
1. 在源选项卡中，选择一个模板：

   * 选择可编辑模板时，将自动选择模板中指定的主题和提交操作，并且 **[!UICONTROL 创建]** 按钮已启用。 您可以转到 **[!UICONTROL 样式]** 或 **[!UICONTROL 提交]** 选项卡以选择不同的主题或提交操作。 如果选定的可编辑模板未指定主题，则创建按钮将保持禁用状态。 您可以转到 **[!UICONTROL 样式]** 选项卡以手动选择主题。

     >[!NOTE]
     >
     > 您还可以创建 [!UICONTROL 记录文档] 使用自适应Forms编辑器的模板。 有关更多信息，请参阅 [自适应表单编辑器中的记录文档支持](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * 选择静态模板时，数据、样式、提交、提交和预览选项不可用。 在创建新的自适应表单时，建议使用可编辑的模板。

1. 在 **[!UICONTROL 样式]** 选项卡，选择一个主题：

   * 当所选模板指定主题时，将在向导中自动选择主题。 您还可以从“样式”选项卡中选择其他主题。
   * 如果所选模板未指定主题，可以使用“样式”选项卡选择主题。 此 **[!UICONTROL 创建]** 按钮仅在选择主题后启用。

1. （可选）在 **[!UICONTROL 数据]** 选项卡中，选择一个数据模型：

   * **表单数据模型**：A [表单数据模型](data-integration.md) 允许您将实体和服务从不同的数据源集成到自适应表单。 如果要创建的自适应表单涉及从多个数据源获取数据以及将数据写入多个数据源，请选择表单数据模型。

   * **JSON架构**： [JSON架构](adaptive-form-json-schema-form-model.md) 表示组织中的后端系统生成或使用数据的结构。 您可以将架构与自适应表单相关联，并使用其元素将动态内容添加到自适应表单。在创作自适应Forms时，架构的元素可在内容浏览器的数据模型对象选项卡中使用，并且所有字段也都已添加到新创建的自适应表单中。

   默认情况下，选择数据模型的所有字段。 创建自适应表单时，所有选定的数据模型字段都会转换为相应的自适应表单组件。 该向导为您提供复选框，以便您仅选择应包含在自适应表单中的字段。

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. 在 **[!UICONTROL 提交]** 选项卡，选择提交操作：

   * 选择模板时，将自动选择模板中指定的提交操作。 您可以从“提交”选项卡中选择其他提交操作。 此 **[!UICONTROL 提交]** 选项卡显示所有可用的提交操作。

   * 当所选模板未指定提交操作时，您可以使用 **[!UICONTROL 提交]** 选项卡以选择提交操作

1. （可选）在“交付”选项卡中，您可以为自适应表单指定发布或取消发布日期。

1. 点按 **[!UICONTROL 创建]**. 将显示一个对话框，用于指定保存自适应表单的标题、名称和位置：

   * **[!UICONTROL 标题]** 指定表单的显示名称。 标题可帮助您识别 [!DNL Experience Manager Forms] 用户界面。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成“名称”字段的值。 您可以更改建议值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入均被替换为连字符。
   * **[!UICONTROL 路径：]** 指定保存自适应表单的位置。 您可以直接将自适应表单保存在 `/content/dam/formsanddocuments` 或创建文件夹，例如 `/content/dam/formsanddocuments/adaptiveforms` 以保存自适应表单。 请确保先创建文件夹，然后再在路径中使用它。 此 **[!UICONTROL 路径：]** 字段不会自动创建文件夹。

1. 点按 **[!UICONTROL 创建]**. 创建自适应表单，并在自适应Forms编辑器中打开该表单。 编辑器将显示模板中可用的内容。 它还显示侧栏，以根据需要自定义新创建的表单。

   根据自适应表单的类型，关联表单中显示的表单元素 <!--XFA form template, XML schema or --> JSON架构或表单数据模型显示在 **[!UICONTROL 数据模型对象]** 的选项卡 **[!UICONTROL 内容浏览器]** 在侧栏中。 您还可以拖放这些元素来构建自适应表单。

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
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

您可以更改自适应表单的表单模型（基于JSON或表单数据模型）。 不能从一个表单模型更改到另一个表单模型。

1. 选择自适应表单并点按 **属性** 图标。
1. 打开 **[!UICONTROL 表单模型]** 按tab键，然后执行以下操作之一。

   * 如果自适应表单没有表单模型，则可以选择其他表单模型并相应地选择 <!-- a form template, --> XML或JSON架构，或表单数据模型。
   * 如果自适应表单基于表单模型，则可以选择其他 <!-- form template, --> XML或JSON架构，或相同表单模型的表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。

您还可以从自适应表单编辑器或自适应表单模板编辑器中修改表单模型属性。

1. 选择 **[!UICONTROL 自适应表单容器（根）]** 组件。
1. 单击 ![“配置”图标](/help/forms/assets/configure-icon.svg){width="100%" align="center"} 图标以打开 **[!UICONTROL 属性]** 自适应表单容器的。
1. 选择 **[!UICONTROL 数据模型]** 选项卡，然后执行以下操作之一：

   * 如果自适应表单没有表单模型，则可以选择表单模型，然后相应地选择 <!-- a form template, --> XML或JSON架构，或表单数据模型。
   * 如果自适应表单基于表单模型，则无法更改表单模型。 您可以选择其他 <!-- form template, --> 适用于相同表单模型的XML或JSON架构，或表单数据模型。
1. 点按 ![保存](/help/forms/assets/check-button.png) 以保存属性。

![FDM — 架构 — 支持](/help/forms/assets/fdmsupport.png){width="100%" align="center"}

>[!NOTE]
>
> 您还可以将自适应表单另存为模板。 有关更多信息，请参阅 [使用自适应表单创建模板](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

>[!ENDTABS]


## 后续步骤

* [将Adobe Sign与Forms结合使用](working-with-adobe-sign.md)
* [在Forms中使用Google reCaptcha](captcha-adaptive-forms.md)
* [向表单添加可重复部分](create-forms-repeatable-sections.md)
* [预填充表单字段](prepopulate-adaptive-form-fields.md)

>[!MORELIKETHIS]
>
>* [在AEM Sites页面或体验片段中创建自适应表单](create-or-add-an-adaptive-form-to-aem-sites-page.md)
>* [创建自定义自适应Forms主题](using-themes-in-core-components.md)
>* [配置表单的提交操作](configuring-submit-actions.md)
>* [可用的自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#components)
