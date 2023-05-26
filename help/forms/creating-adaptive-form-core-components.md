---
title: 如何创建自适应表单
description: 了解如何使用创建自适应表单 [!DNL Experience Manager Forms]. 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 7%

---

# 创建自适应表单（核心组件） {#creating-an-adaptive-form-core-components}

通过自适应Forms，您可以创建有吸引力的响应式、动态自适应表单。 AEM Forms为企业提供了便于用户使用的向导来快速创建自适应Forms。 该向导具有快速选项卡导航，可轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，请了解可供您使用的Forms组件类型：

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化数据捕获组件。 这些组件为您的数字注册体验提供自定义功能、缩短开发时间并降低维护成本。 开发人员可以轻松自定义这些组件并为它们设置样式。 Adobe建议利用这些现代化的、可扩展的组件来开发自适应Forms。

* [自适应Forms Foundation组件](creating-adaptive-form.md)：它们是经典（旧）数据捕获组件。 您可以继续使用这些组件来编辑现有的基于基础组件的自适应表单。 如果要创建新表单，Adobe建议使用  [自适应Forms核心组件](creating-adaptive-form-core-components.md) 创建自适应Forms。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)


## 先决条件

创建自适应表单需要满足以下条件：

* **为您的环境启用自适应Forms核心组件**：创建新项目时，已为您的环境启用自适应Forms核心组件。 如果您有基于 Archetype 39 或更早版本的 Forms as a Cloud Service 环境，请[为您的环境启用自适应表单核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有包含特定属性和内容结构的预格式化的组件。 它还提供定义主题和提交操作的选项。 主题定义外观，提交操作定义在提交自适应表单时要执行的操作。 例如，将收集的数据发送到数据源。 Cloud Service提供一个OOTB模板，名称为空：

   * 此 `blank` 所有新的AEM Formsas a Cloud Service计划中都包含模板。
   * 您可以通过包管理器安装参考包，以添加 `blank` 模板添加到您的AEM Formsas a Cloud Service程序。
   * 您还可以 [创建新的自适应Forms模板（核心组件）](template-editor.md) 从头开始。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。  此 `Canvas` 所有新的AEM Formsas a Cloud Service计划中都包含模板。

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**：将您的用户添加到 [!DNL forms-users] 组。 董事会成员 [!DNL forms-users] 组有权创建自适应表单。 有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).


## 创建自适应表单（核心组件） {#create-an-adaptive-form-core-components}

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

现在，您可以将自适应Forms核心组件拖放到自适应Forms容器中来设计和创建表单。

## 可用的自适应Forms核心组件

自适应Forms核心组件是标准化的数据捕获组件。 这些组件提供自定义功能，有助于缩短开发时间，并降低数字注册体验的维护成本。 [自适应Forms核心组件文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans) 提供了可用组件的详细列表以及有关每个组件功能的详细信息。 您也可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心组件运行情况。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

1. 选择自适应表单并点按 ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**. 此时将打开“表单属性”页面。

1. 转到 **[!UICONTROL 表单模型]** 选项卡并选择表单模型。 如果自适应表单没有表单模型，您可以自由选择JSON架构或表单数据模型。 另一方面，如果自适应表单已基于表单模型，则可以选择切换到相同类型的另一个表单模型。 例如，如果表单使用JSON架构，您可以轻松切换到另一个JSON架构，同样，如果表单使用表单数据模型，您可以切换到另一个表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。
