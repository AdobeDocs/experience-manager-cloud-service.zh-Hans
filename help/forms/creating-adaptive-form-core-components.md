---
title: 如何创建自适应表单
description: 了解如何使用创建自适应表单 [!DNL Experience Manager Forms]. 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 8ac35abd1335b4e31a6dc0d8812cc9df333e69a4
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 6%

---

# 创建自适应表单 {#creating-an-adaptive-form-core-components}

通过自适应Forms，您可以创建有吸引力的响应式、动态自适应表单。 AEM Forms为企业提供了便于用户使用的向导，以快速创建自适应Forms。 该向导具有快速选项卡导航，可轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，请了解可供您使用的Forms组件类型：

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化数据捕获组件。 这些组件为您的数字注册体验提供自定义功能、缩短开发时间并降低维护成本。 开发人员可以轻松自定义这些组件并为它们设置样式。 Adobe建议利用这些现代化的、可扩展的组件来开发自适应Forms。

* [自适应Forms Foundation组件](creating-adaptive-form.md)：它们是经典（旧）数据捕获组件。 您可以继续使用这些组件来编辑现有的基于基础组件的自适应表单。 如果要创建新表单，Adobe建议使用  [自适应Forms核心组件](creating-adaptive-form-core-components.md) 创建自适应Forms。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)


## 先决条件

创建自适应表单需要满足以下条件：

* **为您的环境启用自适应Forms核心组件**：创建新项目时，已为您的环境启用自适应Forms核心组件。 如果您有基于 Archetype 39 或更早版本的 Forms as a Cloud Service 环境，请[为您的环境启用自适应表单核心组件](enable-adaptive-forms-core-components.md)。在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有包含特定属性和内容结构的预格式化的组件。 它还提供定义主题和提交操作的选项。 主题定义外观，提交操作定义在提交自适应表单时要执行的操作。 例如，将收集的数据发送到数据源。 Cloud Service提供一个OOTB模板，名称为空：

   * 此 `blank` 所有新的AEM Formsas a Cloud Service计划中都包含模板。
   * 您可以通过包管理器安装参考包，以添加 `blank` 模板添加到您的AEM Formsas a Cloud Service程序。
   * 您还可以 [创建新的自适应Forms模板（核心组件）](template-editor.md) 从头开始。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。  此 `Canvas` 所有新的AEM Formsas a Cloud Service计划中都包含模板。
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**：将您的用户添加到 [!DNL forms-users] 组。 董事会成员 [!DNL forms-users] 组有权创建自适应表单。 有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).


## 创建自适应表单  {#create-an-adaptive-form-core-components}

1. 登录 [!DNL Experience Manager Forms] 创作实例。 它可以是云实例或本地开发实例。

1. 在“Experience Manager登录”页上输入您的凭据。 登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 此时将打开向导。 在源选项卡中，选择一个模板：

   ![核心组件模板](/help/forms/assets/core-components-template.png)

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

现在，您可以拖放 [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 调适型Forms容器以设计和创建表单。 您也可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心组件运行情况。

## 为自适应表单配置提交操作 {#configure-submit-action-for-form}

提交操作允许您选择通过自适应表单捕获的数据的目标。 当用户单击自适应表单上的提交按钮时，会触发该事件。 自适应表单包括一些开箱即用的提交操作。 您还可以扩展默认提交操作以创建自己的自定义提交操作。 要为表单配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。

1. 单击  **[!UICONTROL 提交]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置提交操作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 选择并配置 **[!UICONTROL 提交操作]**，具体取决于您的要求。 有关提交操作的详细信息，请参阅 [自适应表单提交操作](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 将用户重定向到页面或在提交表单时显示感谢消息

在提交表单时，您可以将用户重定向到其他网页或消息。 要重定向用户或配置感谢消息，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 提交]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置重定向页面或感谢消息](/help/forms/assets/adaptive-forms-redirect-message.png)

   * 要配置重定向URL，请为提交选项选择 **[!UICONTROL 重定向到URL]** 选项，然后浏览并选择AEM Sites页面，或提供外部页面的URL。

   * 要配置自定义或感谢消息，请在“提交”选项中选择 **[!UICONTROL 显示消息]** 选项，并在 **[!UICONTROL 消息内容]** 盒子。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。

## 为自适应表单配置架构或表单数据模型{#configure-schema-or-data-model-for-form}

您可以使用表单数据模型将表单连接到数据源，以根据用户操作发送和接收数据。 您还可以将表单连接到JSON架构，以预定义格式接收提交的数据。 根据要求，将表单连接到JSON架构或表单数据模型：

* [创建JSON架构并上传到您的环境](/help/forms/adaptive-form-json-schema-form-model.md)
* [创建表单数据模型](/help/forms/create-form-data-models.md)

### 为表单配置JSON架构或表单数据模型

要为表单配置JSON架构或表单数据模型，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 数据模型]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置JSON架构或表单数据模型](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根据您的要求，选择并配置JSON架构或表单数据模型：

   * 当您选择 **[!UICONTROL 表单模型]** 选项，使用 **[!UICONTROL 选择表单数据模型]** 选项以选择预配置的表单数据模型。
   * 当您选择 **[!UICONTROL 架构]** 选项，使用 **[!UICONTROL 架构]** 选项来为您的表单选择JSON架构。

1. 单击&#x200B;**[!UICONTROL 完成]**。

## 配置预填充服务  {#configure-prefill-service-for-form}

您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 您可以：

* [创建自定义预填充服务](/help/forms/prepopulate-adaptive-form-fields.md)
* [使用表单数据模型预填充服务](#fdm-prefill-service)

### 使用表单数据模型预填充服务预填充自适应表单的字段 {#fdm-prefill-service}

您可以使用表单数据模型预填充服务预填充使用表单数据模型或自定义预填充服务的自适应表单的字段。 表单数据模型预填充服务使用 [获取已配置表单数据模型的服务](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 以检索数据。 要对自适应表单使用表单数据模型预填充服务，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/assets/configure-icon.svg) 图标。 随即会打开用于配置数据模型的自适应表单容器对话框。
   ![单击扳手图标以打开自适应表单容器对话框以配置重定向页面或感谢消息](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. 选择表单数据模型. 打开 **[!UICONTROL 基本]** 选项卡。 在预填充服务中，选择 **[!UICONTROL 表单数据模型预填充服务]**.
1. 单击&#x200B;**[!UICONTROL 完成]**。您的自适应表单现在配置为使用表单数据模型预填充。 您现在可以使用 [规则编辑器](rule-editor.md) 创建规则以预填充表单的字段。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

1. 选择自适应表单并点按 ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**. 此时将打开“表单属性”页面。

1. 转到 **[!UICONTROL 表单模型]** 选项卡并选择表单模型。 如果自适应表单没有表单模型，您可以自由选择JSON架构或表单数据模型。 另一方面，如果自适应表单已基于表单模型，则可以选择切换到相同类型的另一个表单模型。 例如，如果表单使用JSON架构，您可以轻松切换到另一个JSON架构，同样，如果表单使用表单数据模型，您可以切换到另一个表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。


## 查看下一个

* [为表单创建样式或主题](using-themes-in-core-components.md)
* [使用规则编辑器将动态行为添加到表单](rule-editor.md)
* [为不同的屏幕大小和设备类型设置表单布局](/help/sites-cloud/authoring/features/responsive-layout.md)


## 相关文章 {#related-article}

* [创建基于独立核心组件的自适应表单](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)
