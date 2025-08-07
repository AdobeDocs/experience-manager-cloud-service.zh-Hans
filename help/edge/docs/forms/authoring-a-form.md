---
title: 如何在 AEM 中创作表单？
description: 了解 Adobe Experience Manager (AEM) 中提供的各种表单创作平台以及如何根据您的要求选择合适的平台。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
hide: true
hidefromToC: true
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 100%

---

# 如何在 Adobe Experience Manager (AEM) 中创作表单？

Adobe Experience Manager (AEM) 提供了一个灵活的平台，用于创建引人入胜、动态的响应式自适应表单。它提供了直观的用户界面和丰富的开箱即用组件，用于构建和管理自适应表单。根据您的要求，创作表单时可以使用或不使用表单模型或架构。

## 选择创作平台时需要考虑的关键因素

AEM 提供多种表单创作选项来创建引人入胜的交互式表单。选择表单创作环境时，请考虑以下因素：

| 📝 **考虑因素** | 💡 **要问什么** |
|----------------------|--------------------|
| **用户专业知识** | 谁将创作表单——开发人员、业务用户还是内容作者？ |
| **表单复杂性** | 表单是否需要高级规则、动态部分或集成？ |
| **可重用性需求** | 表单的某些部分是否需要在不同的表单或项目中被重复使用？ |
| **设计灵活性** | 您是否需要能完全控制布局、主题和样式？ |
| **集成要求** | 表单是否需要连接到数据模型、工作流或外部系统？ |
| **易于使用** | 对于您团队的技术技能水平来说，该平台是否直观？ |
| **性能和可扩展性** | 表单是否会大规模使用或在高流量环境中使用？ |
| **全渠道投放** | 表单是否会在网站、移动应用程序、信息亭或多个渠道上使用？ |
| **发布灵活性** | 表单将在 AEM、Edge Delivery 或自定义应用程序的哪里发布？ |

## AEM 中表单创作方法概述

AEM 支持多种创作方法，每种方法都适合不同的用户需求、技术技能水平和发布目标。

- [基础组件](/help/forms/create-adaptive-form-tutorial.md)：使用基础组件构建传统的交互式表单。最适合要与旧版系统集成或者要采用长期建立的工作流程的表单。使用基础组件创作的表单只能在 AEM 上发布，并且与 Edge Delivery Services 不兼容。

- [核心组件](/help/forms/creating-adaptive-form-core-components.md)：使用核心组件创建现代化、响应式且可扩展的表单。它们支持可重用性、无障碍可访问性和更佳的性能。使用核心组件创作的表单可以在 AEM 和 Edge Delivery Services 上发布，从而提供跨平台的灵活性。

- [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)：Edge Delivery Services Forms 改变了表单的创作、执行和处理方式。使用 Edge Delivery Services，组织可以快速、安全地创建高度可用的数字化表单，通过快速开发环境提升用户体验和运营效率。您可以通过两种方式创作 Edge Delivery Services 表单：
   - [所见即所得创作](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：使用 Universal Editor 进行可视化拖放式表单创建，非常适合技术知识有限的内容创作者。使用 Universal Editor 创作的表单通过 Edge Delivery Services 投放，以实现快速的轻量级渲染。
   - [文档式创作](/help/edge/docs/forms/tutorial.md)：使用 Microsoft Excel 或 Google Sheets 等工具来定义表单结构和内容。此方法对于喜欢采用电子表格驱动输入方式的商业用户很有用。这些表单通常通过 Edge Delivery Services 发布，适用于轻量级、大容量的用例。
- [无头创作](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)：使用 API 将表单为任何前端呈现 JSON，例如 React、Angular、移动应用程序或信息亭，而无需依赖 AEM。目前，只有核心组件支持无头投放。无头表单非常适合全渠道用例，并可独立于 AEM 的页面渲染使用，这使其能够灵活地用于自定义前端部署。

### AEM 表单创作方法的比较分析

下表对各种 AEM 表单创作方法进行了简要比较，重点介绍了方法、特点、发布选项和理想用例，以帮助您选择最适合您需求的方法。

| **考虑因素** | **基础组件** | **核心组件** | **Universal Editor （所见即所得）** | **文档式创作** | **无头创作** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **特别适合** | 在 AEM 中维护旧版表单和工作流程 | 具有复杂工作流程和集成的现代化可扩展表单 | 为要求复杂的 Edge Delivery Service 网站创建表单 | 快速制作原型或无需高级提交服务的基本表单 | 跨平台的全渠道体验（网页、移动设备、信息亭等） |
| **用户专业知识** | 开发人员、内容作者 | 开发人员、高级作者 | 商业用户、内容作者 | 企业用户 | 开发人员 |
| **表单复杂性** | 基本表单 | 具有动态部分的复杂表单 | 具有自定义操作的复杂表单 | 简单表单 | API 驱动的高度复杂表单 |
| **设计灵活性** | 有限制 | 高（CSS/JS 定制） | 中等（基于模板） | 有限制 | 高（前端框架控制） |
| **集成能力** | 基本 AEM 工作流 | 高级（数据模型、工作流） | 与外部系统集成 | 基础（Google Sheets、Excel） | 通过 API 完全控制 |
| **发布方式** | 仅限 AEM | AEM 和 Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | 通过 API 的任何前端 |
| **性能与 SEO** | 标准 | 改进了基础组件 | Google Lighthouse 高评分，确保更快的渲染和更好的 SEO | Google Lighthouse 高评分，确保更快的渲染和更好的 SEO | 取决于实施 |
| **全渠道投放** | 有限制 | 中等 | 中等 | 有限制 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM 表单创作方法的功能比较

下表详细比较了不同 AEM 表单创作方法的主要功能，帮助您选择最适合您需求的方法。&#x200B;

| **功能** | **基础组件** | **核心组件** | **Universal Editor （所见即所得）** | **文档式创作** | **无头创作** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **统一构成网站** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **嵌入表单支持** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **规则（动态行为）** | 带有自定义函数的高级规则编辑器 | 带有自定义函数的高级规则编辑器 | 带有自定义函数的高级规则编辑器 | 有限制：显示/隐藏、计算值、自定义函数 | 有限制：需要自定义实施 |
| **附件支持** | ✅ | ✅ | ✅ | ℹ️（抢先体验） | ❌ |
| **验证码支持** | reCAPTCHA v2/Enterprise、hCaptcha (EA)、Turnstile (EA) | reCAPTCHA v2/Enterprise、hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 需要自定义集成 |
| **提交功能** | REST 端点、电子邮件、表单数据模型 (FDM)、调用 AEM 工作流、SharePoint, OneDrive, Azure Blob Storage、Power Automate、Workfront Fusion (EA) | REST 端点、电子邮件、表单数据模型 (FDM)、调用 AEM 工作流、SharePoint, OneDrive, Azure Blob Storage、Power Automate、Workfront Fusion (EA) | REST 端点、电子邮件、表单数据模型 (FDM)、调用 AEM 工作流、SharePoint, OneDrive, Azure Blob Storage、Power Automate、Workfront Fusion (EA) | 仅限电子表格 | 自定义 API 端点 |
| **数据架构** | FDM，自定义 | FDM，自定义 | FDM，自定义 | 自定义 | 自定义 |
| **预填充** | ✅ | ✅ | 💡（通过向导） | ✅ | 自定义实施 |
| **片段** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **可视化规则编辑器** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **本地化** | ✅ | ✅ | 💡（通过 Sites） | ℹ️（Excel - 手册，Google Sheets 函数） | 自定义实施 |
| **数据架构（数据树）** | ✅ | ✅ | 💡（通过 UI 扩展） | ❌ | 自定义实施 |
| **模板支持** | ✅ | ✅ | 仅初始内容，无策略 | ❌ | 自定义实施 |
| **门户** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **记录文档创作** | ✅ | ✅ | 💡（通过 Derlina） | ❌ | ❌ |
| **记录文档生成** | ✅ | ✅ | 💡（FORMS-2475 新） | ❌ | ❌ |
| **主题** | ✅ | ✅ | ℹ️（在项目层面） | ℹ️（在项目层面） | 自定义实施 |
| **自定义组件** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB 与自定义函数** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **片段引用** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Sign 集成** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL 支持** | ❌ | ✅ | 💡 | 💡 | 自定义实施 |
| **试验** | ❌ | ❌ | ✅ | ✅ | 自定义实施 |
| **通过 Workfront 进行任务管理** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **个性化扩展** | ❌ | ❌ | 💡 | ❌ | 自定义实施 |
| **编辑器自定义** | ❌ | ❌ | ✅（通过 UI 扩展） | ❌ | 自定义实施 |
| **提交操作** | ✅ | ✅ | ✅ | 仅限电子表格 | 自定义实施 |


## 相关文章

- [使用 Microsoft Excel 或 Google Sheets 进行文档式创作](/help/edge/docs/forms/create-forms.md)
- [用于所见即所得创作的 Universal Editor ](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
- [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
- [创建自适应表单（核心组件）](/help/forms/create-an-adaptive-form.md)
