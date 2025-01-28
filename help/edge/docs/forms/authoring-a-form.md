---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: ht
source-wordcount: '877'
ht-degree: 100%

---


# 创作表单

Adobe Experience Manager 提供并支持多个编辑器来创作表单。您可以使用：
* 通用编辑器（用于所见即所得的创作）
* Microsoft Excel 或 Google Sheets（称为基于文档的创作）
* 自适应表单编辑器（用于核心组件或基于基础组件的创作）

**[要添加的图像]**

## 通用编辑器（用于所见即所得的创作）

通用编辑器是一个多功能可视化编辑器，提供所见即所得（WYSIWYG）功能，确保获得直观的表单创建体验。建议在创建新表单时使用通用编辑器，因为它提供了现代、用户友好的设计和方便的拖放界面。

要使用通用编辑器创建表单，需要使用 AEM 环境中可用的 Edge Delivery Services 模板。这些表单的外观继承自 Edge Delivery Services GitHub 存储库中的配置。[AEM 环境与 Edge Delivery Services GitHub 存储库之间的连接](/help/edge/docs/forms/publishing-forms.md)必须建立，才能在 Edge Delivery Services 上发布这些表单。

有关如何使用通用编辑器进行创作的详细步骤，请参阅文章[使用通用编辑器创作内容](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)。

## Microsoft Excel 或 Google Sheets（称为基于文档的创作）

您可以使用基于文档的创作方式通过 Microsoft Excel 或 Google Sheets 文件来创作表单，这样可以利用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 的强大生态系统和 API。这种方法对于创建没有高级提交服务的简单表单特别有用。

要开始使用 Microsoft Excel 或 Google Sheets 创建表单，[使用 AEM Forms 样板设置 AEM 项目](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，并将相应的 GitHub 存储库克隆到本地计算机上。AEM Forms Edge Delivery 提供了一项称为自适应表单区块（Adaptive Forms Block）的功能，可简化创建用于捕获和存储数据的表单的过程。要了解如何使用 Edge Delivery Services 上的自适应表单区块创建和发布表单，请参阅[创建表单](/help/edge/docs/forms/create-forms.md)。

## 自适应表单编辑器（用于核心组件或基于基础组件的创作）

您可以创建具有吸引力、响应性和动态性的表单。自适应表单编辑器提供了一个用户友好的向导，可让您快速创建自适应表单。表单向导具有简单的选项卡导航功能，使您能够为基础或核心组件、主题、数据模型和提交选项选择预配置模板，从而高效地创建表单。

[使用核心组件创作表单](/help/forms/creating-adaptive-form-core-components.md)可以利用可定制的标准化数据捕获组件，减少开发时间，降低维护成本，增强数字注册体验。这些表单可以使用 Edge Delivery Services 上的自适应表单区块或通过 AEM 发布实例进行发布。

[使用基础组件创作表单](/help/forms/create-an-adaptive-form.md) 使用的是经典的数据捕获组件。这些表单只能使用 AEM 发布实例发布。

您还可以在 AEM 环境和 Edge Delivery Services GitHub 存储库之间建立[连接后，在 Edge Delivery Services 上发布使用自适应表单编辑器创建的表单](/help/edge/docs/forms/publishing-forms.md)。

## 如何在不同类型的表单创作中进行选择？

下表概述了每个创作编辑器的功能和用例，帮助您根据自己的要求和表单提交需求选择合适的编辑器。

| **表单创作编辑器** | **关键方法** | **功能** | **发布方式** | **用例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **基于文档的创作** | 利用熟悉的工具（如 Google Docs 和 Microsoft Office）来创建表单。 | 使用电子表格设计表单，数据直接提交到 Google Sheets 或 Microsoft Excel 工作表。</br> </br>这些表单的创建和部署速度更快。为这些表单开发自定义组件和样式不需要任何 AEM 知识。 | 这些表单发布在 Edge Delivery Services 上，在 Google Lighthouse 上得分非常高。</br> </br>高分可带来更快的渲染速度和更好的 SEO。 | 这些表单非常适合快速原型开发或不需要高级提交服务的基本表单。</br> </br>这些特点非常适合需要在电子表格中存储数据的调查、注册或反馈表单。这些表单发布在 Edge Delivery Services 上 |
| **通用编辑器**</br> </br>如果要创建新表单，请使用通用编辑器来创建表单。 | 提供所见即所得的界面，用于直观的表单创建。 | 使用直观的拖放界面设计表单。</br> </br>这些表单借用了相应表单配置的 Edge Delivery Services GitHub 存储库外观。 | 这些表单发布在 Edge Delivery Services 上，在 Google Lighthouse 上得分非常高。</br> </br> 高分可带来更快的渲染速度和更好的 SEO。 | 这些表单非常适合创建 Edge Delivery Service 站点和页面表单。这些表单场景涉及复杂表单、复杂工作流、自定义操作或与外部系统集成 |
| **自适应表单编辑器** | 提供向导驱动的方法，使用模板、样式和预定义字段快速开始表单创作。 | 使用这些编辑器来创建基于核心组件的表单或基于基础组件的表单。 | 这些表单可以在 Edge Delivery Services 上或通过 AEM 发布实例发布。 | 使用这些编辑器来创建基于核心组件的表单或基于基础组件的表单。非常适合涉及复杂表单、复杂工作流、自定义操作或与外部系统集成的场景。 |


>[!NOTE]
>
>
> 如果发现通用编辑器中缺少自适应表单编辑器中以前提供的任何功能，可以使用您的官方电子邮件地址发送电子邮件至 aem-forms-ea@adobe.com 进行申请。

## 相关文章

* [使用 Microsoft Excel 或 Google Sheets 进行基于文档的创作](/help/edge/docs/forms/create-forms.md)
* [用于所见即所得创作的通用编辑器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
* [创建自适应表单（核心组件）](/help/forms/create-an-adaptive-form.md)

## 另请参阅

{{see-more-forms-eds}}