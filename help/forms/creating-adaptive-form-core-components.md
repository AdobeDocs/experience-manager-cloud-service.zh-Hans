---
title: 如何基于核心组件创建自适应表单？
description: 了解如何使用 [!DNL Experience Manager Forms]创建自适应表单。 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型(FDM)和XML或JSON架构创建自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 812b1e41b460783d3fa220bd24ecfcfd4208a5df
workflow-type: tm+mt
source-wordcount: '2370'
ht-degree: 51%

---

# 创建自适应表单（核心组件） {#creating-an-adaptive-form-core-components}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |


自适应表单使您能够创建引人入胜、响应式、动态和自适应的表单。AEM Forms 提供便于企业用户使用的向导以快速创建自适应表单。该向导可快速地在选项卡之间导航，从而轻松地选择预先配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，了解可使用的表单组件类型：

* [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化的数据捕获组件。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。开发人员可以轻松地自定义这些组件并设置其样式。Adobe建议使用这些现代化的、可扩展的组件来开发自适应Forms。

* [自适应表单基础组件](creating-adaptive-form.md)：这些是经典（旧版）数据捕获组件。您可以继续使用这些组件来编辑您现有的基于基础组件的自适应表单。如果创建新表单，Adobe建议使用[自适应Forms核心组件](creating-adaptive-form-core-components.md)创建自适应Forms。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)


## 先决条件

您需要以下项来创建自适应表单：

* **为您的环境启用自适应Forms核心组件**：在创建项目时，已为您的环境启用自适应Forms核心组件。 如果您有基于 Archetype 39 或更早版本的 Forms as a Cloud Service 环境，请[为您的环境启用自适应表单核心组件](enable-adaptive-forms-core-components.md)。在为您的环境启用核心组件时，会将&#x200B;**自适应Forms （核心组件）**&#x200B;模板和主题添加到您的环境中。 如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（版面和样式）。它的预格式化的组件包含某些属性和内容结构。它还提供用于定义主题和提交操作的选项。主题定义外观，提交操作定义在提交自适应表单时执行的操作。例如，将收集到的数据发送到数据源。Cloud Service 提供一个名为 blank 的 OOTB 模板：

   * `blank` 模板包含在每个新的 AEM Forms as a Cloud Service 项目中。
   * 您可以通过包管理器安装参考包，以将 `blank` 模板添加到 AEM Forms as a Cloud Service 项目。
   * 您也可以[从头开始创建自适应Forms模板（核心组件）](/help/forms/template-editor-core-components.md)。
   * 您还可以将[示例模板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)部署到您的环境。 这些功能可帮助您迅速创建表单。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。`Canvas`模板包含在每个新的AEM Formsas a Cloud Service计划中。 您还可以将[示例主题](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)部署到您的环境。 这些功能可帮助您开始设计表单的样式，并提供一个基础结构，以根据业务需求创建或自定义主题。

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**：将用户添加到[!DNL forms-users]组。[!DNL forms-users]组的成员具有创建自适应表单的权限。有关特定于表单的用户组的详细列表，请参阅[组和权限](forms-groups-privileges-tasks.md)。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## 创建自适应表单  {#create-an-adaptive-form-core-components}

1. 登录到 [!DNL Experience Manager Forms] 创作实例。它可以是云实例或本地开发实例。

1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。 向导随即打开。在“源”选项卡中，选择一个模板：

   ![核心组件模板](/help/forms/assets/core-components-template.png)

   选择一个模板时，会自动选择该模板中指定的主题和提交操作，并启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡以选择不同的主题或提交操作。如果所选模板未指定主题，则“创建”按钮将保持禁用状态。您可以转到&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡以手动选择主题。

   >[!NOTE]
   >
   >
   > 如果环境中没有&#x200B;**自适应表单（核心组件）**&#x200B;模板，请[为您的环境启用自适应表单核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。在为您的环境启用核心组件时，会将&#x200B;**自适应表单（核心组件）**&#x200B;模板添加到您的环境。

1. 在&#x200B;**[!UICONTROL 样式]**&#x200B;选项卡中，选择一个主题：

   * 如果所选模板指定了一个主题，该主题将在向导中自动选定。您还可以从“样式”选项卡中选择其他主题。

   * 如果所选模板未指定主题，您可以使用“样式”选项卡选择主题。**[!UICONTROL 创建]**&#x200B;按钮仅在选择主题后启用。

1. （可选）在“数据”选项卡中，选择一个数据模型：

   * **表单数据模型(FDM)**： [表单数据模型](data-integration.md)允许您将实体和服务从不同的数据源集成到自适应表单中。 如果要创建的自适应表单涉及从多个数据源获取数据以及将数据写入多个数据源，请选择表单数据模型(FDM)。

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

1. 选择&#x200B;**[!UICONTROL 创建]**。自适应表单将创建并在自适应表单编辑器中打开。该编辑器显示模板中可用的内容。根据自适应表单的类型，关联<!--XFA form template, XML schema or --> JSON架构或表单数据模型(FDM)中存在的表单元素将显示在侧边栏中&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中。 您还可以拖放这些元素来生成自适应表单。

现在，您可以将[自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)拖放到自适应Forms容器中以设计和创建表单。 您还可以访问[https://aemcomponents.dev/](https://aemcomponents.dev/)以查看正在运行的可用核心组件。

>[!NOTE]
>
> 您也可以[使用XFA表单模板（*.XDP文件）创建自适应Forms](/help/forms/create-adaptive-form-using-xfa-templates.md)。 它使您能够通过直接在自适应Forms中重用XDP文件中的字段来节省时间。

## 配置自适应表单的提交操作 {#configure-submit-action-for-form}

提交操作让您选择通过自适应表单捕获的数据的目标。当用户单击自适应表单上的提交按钮时，会触发该事件。 自适应表单包括一些现成的提交操作。 您还可以扩展默认提交操作以创建自己的自定义提交操作。 要为表单配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。

1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。

   ![单击扳手图标以打开“自适应表单容器”对话框来配置提交操作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 根据要求选择并配置&#x200B;**[!UICONTROL 提交操作]**。有关提交操作的详细信息，请参阅[自适应表单提交操作](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 将用户重定向到页面或在提交表单时显示感谢消息

在提交表单时，您可以将用户重定向到其他网页或消息。 要重定向用户或配置感谢消息，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。

   ![单击“扳手”图标以打开“自适应表单容器”对话框以配置重定向页面或感谢消息](/help/forms/assets/adaptive-forms-redirect-message.png)

   * 要配置重定向URL，请在提交选项中，选择&#x200B;**[!UICONTROL 重定向到URL]**&#x200B;选项，然后浏览并选择AEM Sites页面或提供外部页面的URL。

   * 要配置自定义或感谢消息，请在“提交”选项中选择&#x200B;**[!UICONTROL 显示消息]**&#x200B;选项，然后在&#x200B;**[!UICONTROL 消息内容]**&#x200B;框中提供消息。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。

## 为自适应表单配置架构或表单数据模型(FDM){#configure-schema-or-data-model-for-form}

您可以使用表单数据模型(FDM)将表单连接到数据Source，以根据用户操作发送和接收数据。 您还可以将表单连接到 JSON 架构，以接收预定义格式的提交数据。根据要求，将表单连接到JSON架构或表单数据模型(FDM)：

* [创建JSON架构并上传到您的环境](/help/forms/adaptive-form-json-schema-form-model.md)
* [创建表单数据模型(FDM)](/help/forms/create-form-data-models.md)

### 为表单配置JSON架构或表单数据模型(FDM)

要为表单配置JSON架构或表单数据模型(FDM)，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 数据模型]**&#x200B;选项卡。

   ![单击“扳手”图标以打开自适应表单容器对话框以配置JSON架构或表单数据模型(FDM)](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根据您的要求，选择并配置JSON架构或表单数据模型(FDM)：

   * 选择&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项时，请使用&#x200B;**[!UICONTROL 选择表单数据模型]**&#x200B;选项来选择预配置的表单数据模型(FDM)。
   * 选择&#x200B;**[!UICONTROL 架构]**&#x200B;选项时，请使用&#x200B;**[!UICONTROL 架构]**&#x200B;选项为您的表单选择JSON架构。

1. 单击&#x200B;**[!UICONTROL 完成]**。

## 配置预填充服务  {#configure-prefill-service-for-form}

您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 您可以：

* [创建自定义预填充服务](/help/forms/prepopulate-adaptive-form-fields.md)
* [使用表单数据模型预填充服务](#fdm-prefill-service)

### 使用表单数据模型预填充服务预填充自适应表单的字段 {#fdm-prefill-service}

您可以使用表单数据模型预填充服务通过表单数据模型或自定义预填充服务预填充自适应表单的字段。 表单数据模型预填充服务使用配置的表单数据模型[&#128279;](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)的Get服务检索数据。 要对自适应表单使用表单数据模型预填充服务，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/assets/configure-icon.svg)图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
   ![单击“扳手”图标以打开“自适应表单容器”对话框以配置重定向页面或感谢消息](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. 选择表单数据模型(FDM)。 打开&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡。 在预填充服务中，选择&#x200B;**[!UICONTROL 表单数据模型预填充服务]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。 您的自适应表单现在配置为使用表单数据模型预填充。 您现在可以使用[规则编辑器](rule-editor.md)创建规则以预填充表单的字段。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

1. 选择自适应表单，然后选择![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**。 这将打开“表单属性”页面。

1. 转到&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡并选择表单模型。如果自适应表单没有表单模型，您可以自由选择JSON架构或表单数据模型(FDM)。 另一方面，如果自适应表单已基于一个表单模型，则可以选择切换到另一个相同类型的表单模型。例如，如果表单使用JSON架构，您可以轻松切换到另一个JSON架构，同样，如果表单使用表单数据模型(FDM)，您可以切换到另一个表单数据模型(FDM)。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存属性。


## 如何重命名AEM自适应表单？ {#rename-an-AEM-Adaptive-Form}

要重命名自适应表单，请执行以下步骤：

1. 在AEM Forms用户界面中选择自适应表单。
1. 单击位于上边栏上的&#x200B;**属性**。
1. 在&#x200B;**标题**&#x200B;选项卡中更改表单的名称，如下图所示。
1. 单击&#x200B;**保存并关闭**。

![重命名AEM自适应表单](/help/forms/assets/change-af-name.png)

<!--

## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)

-->

## 另请参阅 {#see-also}

{{see-also}}
* [使用规则编辑器将动态行为添加到表单](/help/forms/rule-editor-core-components.md)
* [为不同的屏幕大小和设备类型设置表单布局](/help/sites-cloud/authoring/page-editor/responsive-layout.md)

