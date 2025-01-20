---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# 创作表单

Adobe Experience Manager提供并支持多个编辑器来创作表单。 您可以使用：
* 通用编辑器(用于WYSIWYG创作)
* Microsoft Excel或Google Sheets（称为基于文档的创作）
* 自适应Forms编辑器（适用于核心组件或基于基础组件的创作）

**[要添加的图像]**

## 通用编辑器(用于WYSIWYG创作)

通用编辑器是一个通用的可视化编辑器，它提供了“所见即所得”(WYSIWYG)功能，确保提供直观的表单创建体验。 建议在创建新表单时使用通用编辑器，因为它提供了现代、用户友好的设计和方便的拖放界面。

要使用通用编辑器创建表单，需要使用AEM环境中可用的Edge Delivery Services模板。 这些表单的外观继承自Edge Delivery ServicesGitHub存储库中的配置。 [已建立AEM环境和Edge Delivery ServicesGitHub存储库之间的连接](/help/edge/docs/forms/publishing-forms.md)，以便能够在Edge Delivery Services上发布这些表单。

有关如何使用通用编辑器进行创作的详细步骤，请参阅[使用通用编辑器创作内容](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)一文。

## Microsoft Excel或Google Sheets（称为基于文档的创作）

您可以使用基于文档的创作功能结合Microsoft Excel或Google Sheets文件来创作表单，从而利用Google Sheets、Microsoft Excel和Microsoft SharePoint强大的生态系统和API。 这种方法对于创建没有高级提交服务的简单表单特别有用。

要开始使用Microsoft Excel或Google Sheets创建表单，[请使用AEM Forms样板](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)设置AEM项目，并将相应的GitHub存储库克隆到本地计算机。 AEM Forms Edge Delivery提供了称为自适应Forms块的功能，此功能可简化创建用于捕获和存储数据的表单的过程。 要了解如何在Edge Delivery Services上使用自适应Forms块创建和发布表单，请参阅[创建表单](/help/edge/docs/forms/create-forms.md)。

## 自适应Forms编辑器（适用于核心组件或基于基础组件的创作）

您可以创作吸引人、响应式且动态的表单。 自适应表单编辑器提供了一个用户友好的向导，允许您快速创建自适应Forms。 表单向导具有简单的选项卡导航功能，允许您为基础组件或核心组件、主题、数据模型和提交选项选择预配置的模板，以便高效地创建表单。

使用核心组件[创作表单](/help/forms/creating-adaptive-form-core-components.md)可让您利用可自定义的标准化数据捕获组件，从而缩短开发时间并降低数字注册体验的维护成本。 这些表单可以在Edge Delivery Services上使用自适应Forms块或通过AEM Publish实例进行发布。

[使用Foundation组件创作表单](/help/forms/create-an-adaptive-form.md)使用的是经典数据捕获组件。 这些表单只能使用AEM Publish实例发布。

通过在AEM环境与Edge Delivery Services GitHub存储库](/help/edge/docs/forms/publishing-forms.md)之间建立[连接，您还可以在Edge Delivery Services上发布使用自适应Forms编辑器创建的表单。

## 如何在各种类型的表单创作之间进行选择？

下表概述了每个创作编辑器的功能和用例，可帮助您根据要求和表单提交需求选择合适的编辑器。

| **表单创作编辑器** | **键方法** | **功能** | **发布方法** | **用例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **基于文档的创作** | 利用Google Docs和Microsoft Office等熟悉的工具创建表单。 | Forms使用电子表格进行设计，其中的数据直接提交到Google工作表或Microsoft Excel工作表。</br> </br>创建和部署这些表单的速度更快。 您无需预先了解AEM即可为这些表单开发自定义组件和样式。 | 这些表单发布在Edge Delivery Services上，在Google Lighthouse中的得分很高。</br> </br>高分数可加快渲染速度并改善SEO。 | 这些表单非常适用于快速原型制作或不需要高级提交服务的基本表单。</br> </br>这些表单非常适用于需要将数据存储在电子表格中的调查、注册或反馈表单。 这些表单发布在Edge Delivery服务上 |
| **通用编辑器** </br> </br>如果您正在创建新表单，请使用通用编辑器创建表单。 | 提供WYSIWYG界面以便直观地创建表单。 | Forms使用直观的拖放界面进行设计。</br> </br>这些表单从已配置的Edge Delivery Services GitHub存储库中为相应表单借用外观。 | 这些表单发布在Edge Delivery Services上，在Google Lighthouse中的得分很高。</br> </br>高分数可加快渲染速度并改善SEO。 | 这些表单非常适用于为Edge Delivery服务站点和页面创建表单。 这些表单方案涉及复杂表单、复杂工作流、自定义操作或与外部系统的集成 |
| **自适应Forms编辑器** | 提供了一种向导驱动的方法，以使用模板、样式和预定义字段快速开始表单创作。 | 使用这些编辑器可创建基于核心组件的表单或基于基础组件的表单。 | 这些表单可以在Edge Delivery Services上发布，也可以通过AEM Publish实例发布。 | 使用这些编辑器可创建基于核心组件的表单或基于基础组件的表单。 非常适用于涉及复杂表单、复杂工作流、自定义操作或与外部系统集成的场景。 |


>[!NOTE]
>
>
> 如果您发现通用编辑器中缺少先前在自适应Forms编辑器中提供的任何功能，则可以使用官方电子邮件地址向mailto:aem-forms-ea@adobe.com发送电子邮件以请求这些功能。

## 相关文章

* [使用Microsoft Excel或Google Sheets进行基于文档的创作](/help/edge/docs/forms/create-forms.md)
* 用于WYSIWYG创作的[通用编辑器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
* [创建自适应表单（核心组件）](/help/forms/create-an-adaptive-form.md)

## 另请参阅

{{see-more-forms-eds}}