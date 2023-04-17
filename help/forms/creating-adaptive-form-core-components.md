---
title: 如何创建自适应表单？
description: 了解如何使用 [!DNL Experience Manager Forms]. 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: a4fd268cb143c1356de3db9d55b16ccb58b67d4b
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# 创建自适应表单（核心组件） {#creating-an-adaptive-form-core-components}

自适应表单可让您创建引人入胜、响应式、动态和自适应的表单。AEM Forms提供了业务用户友好向导，可快速创建自适应Forms。 向导具有快速的选项卡导航，可轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

开始之前，请了解可供您使用的Forms组件类型：

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans):这些是标准化的数据捕获组件。 这些组件为您的数字注册体验提供了自定义功能、缩短了开发时间并降低了维护成本。 开发人员可以轻松自定义和设置这些组件的样式。 Adobe建议利用这些现代且可扩展的组件来开发自适应Forms。

* [自适应Forms Foundation组件](creating-adaptive-form.md):这些是经典（旧）数据捕获组件。 您可以继续使用这些组件来编辑现有的基于自适应表单的基础组件。 如果要创建新表单，Adobe建议使用  [自适应Forms核心组件](creating-adaptive-form-core-components.md) 创建自适应Forms。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)


## 先决条件

您需要满足以下条件才能创建自适应表单：

* **为环境启用自适应Forms核心组件**:创建新项目时，您的环境中已启用自适应Forms核心组件。 如果您有基于Archetype 39或更早版本的Formsas a Cloud Service环境， [为环境启用自适应Forms核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 在为环境启用核心组件时， **自适应Forms（核心组件）** 模板和画布主题会添加到您的环境中。 如果您的AEM SDK版本低于2023.02.0, [确保 `prerelease` 环境中已启用的标记](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) 因为自适应Forms核心组件在2023.02.0版之前是预先购买的一部分。

* **自适应表单模板**:模板提供了基本结构并定义了自适应表单的外观（布局和样式）。 它具有预格式化的组件，其中包含某些属性和内容结构。 它还提供了用于定义主题和提交操作的选项。 主题定义了外观和感觉，并定义了提交自适应表单时要执行的操作。 例如，将收集的数据发送到数据源。 云服务提供了一个名为空的OOTB模板：

   * 的 `blank` 模板包含在每个新的AEM Formsas a Cloud Service计划中。
   * 您可以通过包管理器安装引用包，以添加 `blank` 模板添加到AEM Formsas a Cloud Service计划。
   * 您还可以 [创建新的自适应Forms模板（核心组件）](template-editor.md) 白手起家。

* **自适应表单主题**:主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式将反映在相应的组件上。  的 `Canvas` 模板包含在每个新的AEM Formsas a Cloud Service计划中。

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **权限**:将用户添加到 [!DNL forms-users] 群组。 成员 [!DNL forms-users] 群组有权创建自适应表单。 有关特定用户群组的表单的详细列表，请参阅 [群组和权限](forms-groups-privileges-tasks.md).


## 创建自适应表单（核心组件） {#create-an-adaptive-form-core-components}

1. 登录到 [!DNL Experience Manager Forms] 创作实例。 它可以是云实例或本地开发实例。

1. 在Experience Manager登录页面上输入凭据。 登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]**  > **[!UICONTROL 自适应Forms]**. 随即会打开向导。 在“源”选项卡中，选择一个模板：

   ![核心组件模板](/help/forms/assets/core-components-template.png)

   选择模板时，会自动选择模板中指定的主题和提交操作，并且 **[!UICONTROL 创建]** 按钮。 您可以转到 **[!UICONTROL 样式]** 或 **[!UICONTROL 提交]** 选项卡，以选择其他主题或提交操作。 如果选定的模板未指定主题，则创建按钮仍处于禁用状态。 您可以转到 **[!UICONTROL 样式]** 选项卡来访问Advertising Cloud的帮助。

   >[!NOTE]
   >
   >
   > 如果你没有， **自适应Forms（核心组件）** 模板， [为环境启用自适应Forms核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 在为环境启用核心组件时， **自适应Forms（核心组件）** 模板。

1. 在 **[!UICONTROL 样式]** 选项卡，选择主题：

   * 当所选模板指定主题时，将在向导中自动选择该主题。 您还可以从“样式”选项卡中选择其他主题。

   * 如果所选模板未指定主题，则可以使用“样式”选项卡选择主题。 的 **[!UICONTROL 创建]** 按钮时，才会启用此选项。

1. （可选）在数据选项卡中，选择一个数据模型：

   * **表单数据模型**:A [表单数据模型](data-integration.md) 允许您将来自不同数据源的实体和服务集成到自适应表单。 如果要创建的自适应表单涉及从多个数据源获取数据并将数据写入多个数据源，请选择表单数据模型。

   * **JSON架构**: [JSON架构](adaptive-form-json-schema-form-model.md) 我们基于核心组件的自适应表单提供了关联JSON模式（表示正在生成或使用的数据的结构）的功能，从而允许与贵组织的后端系统无缝集成。 通过此关联，作者可以使用架构的元素动态地将内容添加到自适应表单。 在创作过程中，架构的元素可以在内容浏览器的数据模型对象选项卡中轻松访问，并且所有字段都会自动添加到任何新创建的自适应表单中。

   默认情况下，关联的JSON架构的所有字段都会自动选择并转换为相应的自适应表单组件，从而简化创作过程。 该向导为您提供了更多便利，允许您通过使用复选框有选择地选择自适应表单中应包含的字段。

1. 在 **[!UICONTROL 提交]** 选项卡，选择提交操作：

   * 选择模板时，将自动选择在模板中指定的提交操作。 您可以从“提交”选项卡中选择其他提交操作。 的 **[!UICONTROL 提交]** 选项卡会显示所有可用的提交操作。

   * 如果选定的模板未指定提交操作，则可以使用 **[!UICONTROL 提交]** 选项卡来选择提交操作

1. （可选）在 **[!UICONTROL 投放]** 选项卡，您可以为自适应表单指定发布或取消发布日期。

1. 点按 **[!UICONTROL 创建]**. 此时会出现一个对话框，用于指定标题、名称和保存自适应表单的位置：

   * **[!UICONTROL 标题]** 指定表单的显示名称。 标题可帮助您在 [!DNL Experience Manager Forms] 用户界面。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。
   * **[!UICONTROL 路径：]** 指定自适应表单的保存位置。 您可以直接在 `/content/dam/formsanddocuments` 或创建文件夹，例如 `/content/dam/formsanddocuments/adaptiveforms` 以保存自适应表单。 确保在路径中使用文件夹之前先创建该文件夹。 的 **[!UICONTROL 路径]** 字段不会自动创建文件夹。

1. 点按 **[!UICONTROL 创建]**. 此时会创建自适应表单，并在自适应Forms编辑器中打开该表单。 编辑器显示模板中可用的内容。  根据自适应表单的类型，关联 <!--XFA form template, XML schema or --> JSON架构或表单数据模型显示在 **[!UICONTROL 数据模型对象]** 选项卡 **[!UICONTROL 内容浏览器]** 中。 您还可以拖放这些元素以构建自适应表单。

现在，您可以将自适应Forms核心组件拖放到自适应Forms容器以设计和创建表单。

## 可用的自适应Forms核心组件

自适应Forms核心组件是标准化的数据捕获组件。 这些组件提供了自定义功能，有助于缩短开发时间并降低数字注册体验的维护成本。 [自适应Forms核心组件文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans) 提供了可用组件的详细列表以及有关每个组件功能的详细信息。 您还可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心组件。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

1. 选择自适应表单并点按 ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**. 此时将打开“表单属性”页面。

1. 转到 **[!UICONTROL 表单模型]** 选项卡，然后选择表单模型。 如果自适应表单没有表单模型，则您可以自由选择JSON架构或表单数据模型。 另一方面，如果自适应表单已基于表单模型，则可以选择切换到同一类型的其他表单模型。 例如，如果表单使用JSON模式，则可以轻松切换到其他JSON模式，同样，如果表单使用表单数据模型，也可以切换到其他表单数据模型。

1. 点按 **[!UICONTROL 保存]** 以保存属性。
