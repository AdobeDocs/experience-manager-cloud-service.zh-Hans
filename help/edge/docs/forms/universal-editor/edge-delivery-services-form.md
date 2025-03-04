---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: bb01a76ae2bfd78ae648e91545f34f20fabebd10
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 100%

---


# Edge Delivery Services Forms

Adobe Edge Delivery Services Forms 改变了表单的创作、执行和处理方式。使用 Edge Delivery Services，组织可以快速、安全地创建高度可用的数字化表单，通过快速开发环境提升用户体验和运营效率。通过 Edge Delivery Services Forms，您可以提高转化率、降低成本并加速内容投放。

## Edge Delivery Services Forms 的优点

* **更快的表单创建**：利用完美的 Lighthouse 评分构建高性能表单，并使用真实用户监控（RUM）持续监控表单的实际性能。

* **简化的创作流程**：轻松管理多个来源的内容，提高灵活性。您可以使用所见即所得（WYSIWYG）和基于文档的创作方式创建表单，从而实现各种内容格式的无缝集成。

* **非技术用户也能轻松使用**：Edge Delivery Services 使非程序员也能轻松管理和发布表单，而无需丰富的编程知识。

* **改善用户体验**：确保快速的加载时间和顺畅的交互，为用户提供最短的等待时间和直观的表单填写体验。

* **无服务器执行**：Edge Delivery Services 支持表单逻辑的无服务器执行。这包括：

   * **客户端验证**：表单字段验证在客户端进行，减少了往返延迟。

   * **预填和个性化**：表单数据预填在客户端进行，实现顺畅无缝的用户体验。

   * **提交处理**：表单提交经过验证并安全转发，无需中央服务器

## Edge Delivery Services Forms 如何运作？

用户可以使用基于文档的创作工具（如 Google Drive、SharePoint 或用于所见即所得创作的通用编辑器）创作 Edge Delivery Services Forms，同时使用 GitHub 存储库中提供的基本样式、行为和组件。创作完成后，Edge Delivery Services Forms 就可以使用表单提交服务将数据发送到任何平台。

![Edge Delivery Services Forms 如何运作？](/help/edge/docs/forms/assets/eds-forms-working.png)

### Edge Delivery Services Forms 的关键组件

Edge Delivery Servies Forms 的关键组件有：

* **GitHub 存储库**：GitHub 存储库可用作创建 Edge Delivery Services Forms 的样板。这些表单使用存储库中的基本样式和功能，用户可以向 Edge Delivery Services Forms 添加自定义功能和自定义组件。

* **表单创作**：Edge Delivery Services Forms 支持两种类型的创作：所见即所得和基于文档的创作。基于文档的创作使用户能够使用熟悉的工具（如 Google Docs 和 Microsoft Office）创建表单。在所见即所得的创建方式中，用户可以使用通用编辑器直观地设计表单，非技术用户也能轻松创建和管理表单。通用编辑器可提供直观的表单创建体验，并提供多种表单功能。

* **表单提交服务**：使用表单提交服务，您可以将表单提交的数据存储在任何平台上，如 OneDrive、SharePoint 或 Google Sheets，从而方便您在首选系统中访问和管理表单数据。

## 创作表单

Adobe Experience Manager 提供并支持多个编辑器来创作表单。您可以使用：
* [通用编辑器（用于所见即所得的创作）](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel 或 Google Sheets（称为基于文档的创作）](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### 通用编辑器（用于所见即所得的创作）

通用编辑器是一个多功能可视化编辑器，提供所见即所得（WYSIWYG）功能，确保获得直观的表单创建体验。建议在创建新表单时使用通用编辑器，因为它提供了现代、用户友好的设计和方便的拖放界面。

要使用通用编辑器创建表单，需要使用 AEM 环境中可用的 Edge Delivery Services 模板。这些表单的外观继承自 Edge Delivery Services GitHub 存储库中的配置。[AEM 环境与 Edge Delivery Services GitHub 存储库之间的连接](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)必须建立，才能在 Edge Delivery Services 上发布这些表单。

有关如何使用通用编辑器进行创作的详细步骤，请参阅文章[使用通用编辑器创作内容](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)。

### Microsoft Excel 或 Google Sheets（称为基于文档的创作）

您可以使用基于文档的创作方式通过 Microsoft Excel 或 Google Sheets 文件来创作表单，这样可以利用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 的强大生态系统和 API。这种方法对于创建没有高级提交服务的简单表单特别有用。

要开始使用 Microsoft Excel 或 Google Sheets 创建表单，[使用 AEM Forms 样板设置 AEM 项目](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，并将相应的 GitHub 存储库克隆到本地计算机上。AEM Forms Edge Delivery 提供了一项称为自适应表单区块（Adaptive Forms Block）的功能，可简化创建用于捕获和存储数据的表单的过程。要了解如何使用 Edge Delivery Services 上的自适应表单区块创建和发布表单，请参阅[创建表单](/help/edge/docs/forms/create-forms.md)。

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### 如何在不同类型的表单创作中进行选择？

下表概述了每个创作编辑器的功能和用例，帮助您根据自己的要求和表单提交需求选择合适的编辑器。

| **表单创作编辑器** | **关键方法** | **功能** | **发布方式** | **用例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **基于文档的创作** | 利用熟悉的工具（如 Google Docs 和 Microsoft Office）来创建表单。 | 使用电子表格设计表单，数据直接提交到 Google Sheets 或 Microsoft Excel 工作表。</br> </br>这些表单的创建和部署速度更快。为这些表单开发自定义组件和样式不需要任何 AEM 知识。 | 这些表单发布在 Edge Delivery Services 上，在 Google Lighthouse 上得分非常高。</br> </br>高分可带来更快的渲染速度和更好的 SEO。 | 这些表单非常适合快速原型开发或不需要高级提交服务的基本表单。</br> </br>这些特点非常适合需要在电子表格中存储数据的调查、注册或反馈表单。这些表单发布在 Edge Delivery Services 上 |
| **通用编辑器**</br> </br>如果要创建新表单，请使用通用编辑器来创建表单。 | 提供所见即所得的界面，用于直观的表单创建。 | 使用直观的拖放界面设计表单。</br> </br>这些表单借用了相应表单配置的 Edge Delivery Services GitHub 存储库外观。 | 这些表单发布在 Edge Delivery Services 上，在 Google Lighthouse 上得分非常高。</br> </br> 高分可带来更快的渲染速度和更好的 SEO。 | 这些表单非常适合创建 Edge Delivery Service 站点和页面表单。这些表单场景涉及复杂表单、复杂工作流、自定义操作或与外部系统集成 |

>[!NOTE]
>
>
> 如果发现通用编辑器中缺少自适应表单编辑器中以前提供的任何功能，可以使用您的官方电子邮件地址发送电子邮件至 aem-forms-ea@adobe.com 进行申请。

## 另请参阅

{{see-more-forms-eds}}
