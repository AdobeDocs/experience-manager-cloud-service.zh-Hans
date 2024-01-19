---
title: 如何为自适应表单创建表单数据模型？
description: 了解如何基于表单数据模型(FDM)创建自适应Forms和片段。 在FDM中生成并编辑数据模型对象的示例数据。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 6e01a5bfc4e8bf7cc9537c9c03af08cd253a1ade
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 7%

---

# 使用表单数据模型 {#use-form-data-model}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html) |
| AEM as a Cloud Service | 本文 |


![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 通过数据集成，您可以使用不同的后端数据源来创建表单数据模型，以将其用作各种自适应Forms中的架构 <!--and interactive communications--> 工作流。 它需要根据数据源中可用的数据模型对象和服务配置数据源并创建表单数据模型。 有关更多信息，请参阅以下内容：

* [[!DNL Experience Manager Forms] 数据集成](data-integration.md)
* [配置数据源](configure-data-sources.md)
* [创建表单数据模型](create-form-data-models.md)
* [使用表单数据模型](work-with-form-data-model.md)

表单数据模型是JSON架构的扩展，可用于执行以下操作：

* [创建自适应Forms和片段](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [使用示例数据预览](#preview-ic)
* [使用表单数据模型服务](#prefill)
* [将提交的自适应表单数据写回数据源](#write-af)
* [使用自适应表单规则调用服务](#invoke-services)

## 创建自适应Forms和片段 {#create-af}

您可以创建 [自适应Forms](creating-adaptive-form.md) 和自适应表单片段 <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> 基于表单数据模型。 执行以下操作，以便在创建自适应表单或自适应表单片段时使用表单数据模型：

1. 在添加属性屏幕上的表单模型选项卡中，选择 **[!UICONTROL 表单数据模型]** 在 **[!UICONTROL 选择自]** 下拉列表。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 选择以展开 **[!UICONTROL 选择表单数据模型]**. 列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**仅自适应表单片段**)您可以仅根据表单数据模型中一个数据模型对象创建自适应表单片段。 展开 **[!UICONTROL 表单数据模型定义]** 下拉菜单。 它列出了指定表单数据模型中的所有数据模型对象。 从列表中选择数据模型对象。

   ![create-af-3](assets/create-af-3.png)

   创建基于表单数据模型的自适应表单或自适应表单片段后，表单数据模型对象将显示在 **[!UICONTROL 数据源]** 自适应表单编辑器中内容浏览器的选项卡。

   >[!NOTE]
   >
   >对于自适应表单片段，只有创作时选择的数据模型对象及其关联的数据模型对象会显示在数据源选项卡中。

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   您可以将数据模型对象拖放到自适应表单或片段上以添加表单字段。 添加的表单字段保留元数据属性，并与数据模型对象属性绑定。 绑定可确保字段值在表单提交时在相应的数据源中更新，并在表单呈现时预填充。

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## 使用示例数据预览 {#preview-ic}

表单数据模型编辑器允许您为表单数据模型中的数据模型对象生成和编辑示例数据。 您可以使用此数据来预览和测试 <!--interactive communications and--> 自适应Forms。 在预览之前必须生成示例数据，如中所述 [使用表单数据模型](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and select **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and select **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

要预览包含示例数据的自适应表单，请在创作模式下打开自适应表单，然后选择 **[!UICONTROL 预览]**.

## 使用表单数据模型服务预填充 {#prefill}

[!DNL Experience Manager Forms] 提供为自适应Forms启用的现成表单数据模型预填充服务 <!--and interactive communications--> 基于表单数据模型。 预填充服务在自适应表单中查询数据模型对象的数据源 <!--and interactive communication--> 并相应地在呈现表单或通信时预填充数据。

要为自适应表单启用表单数据模型预填充服务，请打开自适应表单容器属性，然后选择 **[!UICONTROL 表单数据模型预填充服务]** 从 **[!UICONTROL 预填充服务]** 基本折叠面板中的下拉列表。 然后，保存属性。

![预填充服务](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## 将提交的自适应表单数据写入数据源 {#write-af}

当用户提交基于表单数据模型的表单时，您可以配置表单以将数据模型对象的提交数据写入其数据源。 要实现此用例， [!DNL Experience Manager Forms] 提供 [表单数据模型提交操作](configuring-submit-actions.md)，现成仅适用于基于表单数据模型的自适应Forms。 它将为数据模型对象提交的数据写入其数据源。

要配置表单数据模型提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从 **[!UICONTROL 提交操作]** 下拉列表，选择 **[!UICONTROL 使用表单数据模型提交]**.

   ![操作配置](/help/forms/assets/configure-submit-action-invoke-fdm.png)

1. 指定 **[!UICONTROL 要提交的数据模型]**.
1. 单击 **[!UICONTROL 完成]**

在表单提交时，将配置数据模型对象的数据写入各自的数据源。 此外，您可以使用表单数据模型和记录文档 (DoR) 将表单附件提交到数据源。有关表单数据模型的信息，请参阅[[!DNL AEM Forms] 数据集成](data-integration.md)。

<!--![data-submission](assets/data-submission.png)-->

>[!NOTE]
>
> AEMas a Cloud Service提供了多种现成的提交操作来处理表单提交。 有关这些选项的更多信息，请参阅 [自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)  文章。

您还可以使用二进制数据模型对象属性将表单附件提交到数据源。 执行以下操作以将附件提交到JDBC数据源：

1. 将包含二进制属性的数据模型对象添加到表单数据模型。
1. 在自适应表单中，拖放 **[!UICONTROL 文件附件]** 将组件浏览器中的组件移入自适应表单。
1. 选择以选择添加的组件，然后选择 ![settings_icon](assets/configure-icon.svg) 以打开组件的属性浏览器。
1. 在绑定引用字段中，选择 ![foldersearch_18](assets/folder-search-icon.svg) 并导航以选择您在表单数据模型中添加的二进制属性。 根据需要配置其他属性。

   选择 ![复选按钮](assets/save_icon.svg) 以保存属性。 附件字段现在绑定到表单数据模型的二进制属性。

1. 在自适应表单容器属性的提交部分中，启用 **[!UICONTROL 提交表单附件]**. 在提交表单时，它将二进制属性字段中的附件提交到数据源。

## 使用规则在自适应Forms中调用服务 {#invoke-services}

在基于表单数据模型的自适应表单中，您可以 [创建规则](rule-editor.md) 以调用在表单数据模型中配置的服务。 此 **[!UICONTROL 调用服务]** 规则中的操作列出了表单数据模型中的所有可用服务，并允许您选择服务的输入和输出字段。 您也可以使用 **[!UICONTROL 设置值]** 用于调用表单数据模型服务并将字段的值设置为服务返回的输出的规则类型。

例如，以下规则调用一个将Employee ID作为输入的get服务，返回的值将填充到表单中对应的Dependent ID、Last Name、First Name和Gender字段中。

![invoke-service](assets/invoke-service.png)

此外，您可以使用 `guidelib.dataIntegrationUtils.executeOperation` 用于在规则编辑器的代码编辑器中编写JavaScript的API。 <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### 使用自定义函数调用表单数据模型 {#invoke-form-data-model-using-custom-functions}

您可以 [使用自定义函数从规则编辑器调用表单数据模型](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions). 要调用表单数据模型，请将表单数据模型添加到允许列表。 要将表单数据模型添加到允许列表，请执行以下操作：

1. 转到Experience ManagerWeb控制台，网址为 `https://server:host/system/console/configMgr`.
1. 定位 **[!UICONTROL 用于服务调用的表单数据模型的自适应表单级白名单 — 配置工厂]**.
1. 单击 ![加号图标](/help/forms/assets/Smock_Add_18_N.svg) 图标以添加配置……
1. 添加 **[!UICONTROL 内容路径模式]** 以指定自适应Forms的位置。  默认情况下，该值为 `/content/forms/af/(.*)` 包括所有自适应Forms。 您还可以指定特定自适应表单的路径。
1. 添加 **[!UICONTROL 表单数据模型路径模式]** 以指定表单数据模型的位置。 默认情况下，该值为 `/content/dams/formsanddocuments-fdm/(.*)` 包括所有表单数据模型。 您还可以指定特定表单数据模型的路径。
1. 保存设置。

添加的配置将保存在下 **[!UICONTROL 用于服务调用的表单数据模型的自适应表单级白名单 — 配置工厂]** 选项。

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> 要通过AEM原型项目使用自定义函数从规则编辑器调用表单数据模型，请执行以下操作：
>
>1. [创建配置文件](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json).
>1. 设置getContentPathPattern和getFormDataModelPathPattern的属性。
>1. 部署项目。
