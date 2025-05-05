---
title: 如何在AEM中创作表单？
description: 了解Adobe Experience Manager (AEM)中可用的各种表单创作平台，以及如何根据您的要求选择正确的平台。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: f6c6b4c17482eb519fb0d4287704d775d0a5da00
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 7%

---


# 如何在Adobe Experience Manager (AEM)中创作Forms？

Adobe Experience Manager (AEM)为创建有吸引力、响应式、动态和自适应表单提供了一个灵活的平台。 它提供了直观的用户界面和一组丰富的现成组件，用于构建和管理自适应Forms。 Forms可以不使用表单模型或架构进行创作，具体取决于您的要求。

## 选择创作平台时的主要注意事项

AEM提供了多个表单创作选项，用于创建交互式且具有吸引力的表单。 选择表单创作环境时，请考虑以下因素：

| ??**注意事项** | ??**要问什么** |
|----------------------|--------------------|
| **用户专业知识** | 谁将创作表单 — 开发人员、业务用户或内容作者？ |
| **表单复杂性** | 该表单是否需要高级规则、动态部分或集成？ |
| **可重用性需求** | 表单的各个部分是否会在不同的表单或项目中重复使用？ |
| **设计灵活性** | 是否需要完全控制布局、主题和样式？ |
| **集成要求** | 表单是否需要连接到数据模型、工作流或外部系统？ |
| **易用性** | 该平台对于您团队的技术技能水平是否直观？ |
| **性能和可扩展性** | 表单是大规模使用还是在高流量环境中使用？ |
| **全渠道投放** | 该表单是否会用于网站、移动应用程序、网亭或多个渠道？ |
| **发布灵活性** | 表单将在AEM、Edge Delivery或自定义应用程序上的何处发布？ |

## AEM中的表单创作方法概述

AEM支持多种创作方法，每种方法都适合不同的用户需求、技术技能水平和发布目标。

* [基础组件](/help/forms/create-adaptive-form-tutorial.md)：使用基础组件构建传统的交互式表单。 最适合与旧版系统集成或依赖长期建立的工作流的表单。 通过基础组件创作的Forms只能在AEM上发布，并且与Edge Delivery Services不兼容。

* [核心组件](/help/forms/creating-adaptive-form-core-components.md)：使用核心组件创建现代、响应式且可伸缩的表单。 它们支持可重用性、可访问性和更好的性能。 使用核心组件创作的Forms可在AEM和Edge Delivery Services上发布，从而提供跨平台的灵活性。

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)： Edge Delivery Services Forms改变了表单的创作、执行和处理方式。 使用 Edge Delivery Services，组织可以快速、安全地创建高度可用的数字化表单，通过快速开发环境提升用户体验和运营效率。您可以通过两种方式创作Edge Delivery Services Forms：
   * [WYSIWYG创作](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：使用通用编辑器创建可视、拖放的表单，非常适合技术知识有限的内容作者。 使用Universal Editor创作的Forms交付使用Edge Delivery Services，以实现快速、轻量级的渲染。
   * [基于文档的创作](/help/edge/docs/forms/tutorial.md)：使用Microsoft Excel或Google Sheets等工具定义表单结构和内容。 此方法对于偏好使用电子表格驱动输入的业务用户非常有用。 这些表单通常通过Edge Delivery Services发布，适用于轻量、高容量的用例。
* [Headless创作](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)：使用API对任何前端(例如React、Angular、移动应用程序或信息亭)将表单渲染为JSON，而不依赖于AEM。 目前，仅核心组件支持Headless投放。 Headless表单非常适用于全渠道用例，并且在AEM页面渲染之外单独使用，使其灵活适用于自定义前端部署。

### AEM表单创作方法的比较分析

下&#x200B;表简要比较了各种AEM表单创作方法，重点介绍了方法、功能、发布选项和理想用例，以帮助您选择最符合自己需求的方法。

| **注意事项** | **基础组件** | **核心组件** | **通用编辑器(WYSIWYG)** | **基于文档的创作** | **Headless创作** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **适合** | 在AEM中维护旧版表单和工作流 | 具有复杂工作流和集成的可扩展现代表单 | 为具有复杂要求的Edge Delivery服务站点创建表单 | 无需高级提交服务的快速原型制作或基本表单 | 跨平台（Web、移动设备、网亭等）的全渠道体验 |
| **用户专业知识** | 开发人员、内容作者 | 开发人员、高级作者 | 商业用户、内容作者 | 商业用户 | 开发人员 |
| **表单复杂性** | 基本表单 | 具有动态部分的复杂表单 | 具有自定义操作的复杂表单 | 简单表单 | 高度复杂、API驱动的表单 |
| **设计灵活性** | 有限 | 高（CSS/JS自定义） | 审核（基于模板） | 有限 | 高（前端框架控制） |
| **集成功能** | 基本AEM工作流 | 高级（数据模型、工作流） | 与外部系统集成 | 基本(Google Sheets、Excel) | 通过API实现完全控制 |
| **发布方式** | 仅限AEM | AEM 和 Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | 通过API访问任何前端 |
| **性能和SEO** | 标准 | 与基础组件相比有所改进 | Google Lighthouse得分较高，渲染速度更快，SEO更好 | Google Lighthouse得分较高，渲染速度更快，SEO更好 | 取决于实施 |
| **全渠道投放** | 有限 | 审核 | 审核 | 有限 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM表单创作方法的功能比较

下表详细比较了不同AEM表单创作方法的主要功能，有助于您根据需求选择最合适的方法&#x200B;。

| **功能** | **基础组件** | **核心组件** | **通用编辑器(WYSIWYG)** | **基于文档的创作** | **Headless创作** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **与站点的统一组合** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **嵌入表单支持** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **规则（动态行为）** | 具有自定义函数的高级规则编辑器 | 具有自定义函数的高级规则编辑器 | 具有自定义函数的高级规则编辑器 | 有限：显示/隐藏、计算值、自定义函数 | 有限：需要自定义实施 |
| **附件支持** | ✅ | ✅ | ✅ | ℹ️（早期访问） | ❌ |
| **CAPTCHA支持** | reCAPTCHA v2/Enterprise、hCaptcha (EA)、Turnstile (EA) | reCAPTCHA v2/Enterprise、hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 需要自定义集成 |
| **提交功能** | REST端点、电子邮件、表单数据模型(FDM)、调用AEM Workflow、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion (EA) | REST端点、电子邮件、表单数据模型(FDM)、调用AEM Workflow、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion (EA) | REST端点、电子邮件、表单数据模型(FDM)、调用AEM Workflow、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion (EA) | 仅限电子表格 | 自定义API端点 |
| **数据架构** | FDM，自定义 | FDM，自定义 | FDM，自定义 | 自定义 | 自定义 |
| **预填充** | ✅ | ✅ | ??（通过向导） | ✅ | 自定义实施 |
| **片段** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **可视规则编辑器** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **本地化** | ✅ | ✅ | ??（通过Sites） | ℹ️(Excel — 手动， Google Sheets功能) | 自定义实施 |
| **数据架构（数据树）** | ✅ | ✅ | ??（通过UI扩展） | ❌ | 自定义实施 |
| **模板支持** | ✅ | ✅ | 仅初始内容，无策略 | ❌ | 自定义实施 |
| **门户** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **DoR创作** | ✅ | ✅ | ??（经德里纳） | ❌ | ❌ |
| **DoR生成** | ✅ | ✅ | ??(FORMS-2475新增) | ❌ | ❌ |
| **主题** | ✅ | ✅ | ℹ️（项目级） | ℹ️（项目级） | 自定义实施 |
| **自定义组件** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB和自定义函数** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **片段引用** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **签名集成** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL支持** | ❌ | ✅ | ?? | ?? | 自定义实施 |
| **试验** | ❌ | ❌ | ✅ | ✅ | 自定义实施 |
| 通过Workfront进行&#x200B;**任务管理** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Personalization扩展** | ❌ | ❌ | ?? | ❌ | 自定义实施 |
| **编辑器自定义** | ❌ | ❌ | ✅（通过UI扩展） | ❌ | 自定义实施 |
| **提交操作** | ✅ | ✅ | ✅ | 仅限电子表格 | 自定义实施 |


## 相关文章

* [使用 Microsoft Excel 或 Google Sheets 进行基于文档的创作](/help/edge/docs/forms/create-forms.md)
* [用于所见即所得创作的通用编辑器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
* [创建自适应表单（核心组件）](/help/forms/create-an-adaptive-form.md)
