---
title: 如何为自适应表单配置提交操作？
description: 自适应表单提供了多个提交操作。提交操作定义了提交后处理自适应表单的方式。您可以使用内置的提交操作或创建您自己的提交操作。
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 58%

---


# 提交由自适应Forms支持的操作

自适应表单可让您创建引人入胜、响应式、动态和自适应的表单。它们提供了直观的用户界面和一组现成的组件，可用于高效地设计和管理表单。 您可以配置各种提交操作以将表单数据发送到OneDrive、SharePoint、Workfront Fusion等服务。

当用户单击自适应表单上的&#x200B;**[!UICONTROL 提交]**&#x200B;按钮时，会触发提交操作。 Forms as a Cloud Service提供了多个现成的提交操作。 通过内置提交操作，您可以：

* 通过电子邮件轻松发送表单数据
* 在传输数据时启动Microsoft®Power Automate流或AEM Workflow。
* 直接将表单数据传输到Microsoft®SharePoint Server、Microsoft®Azure Blob Storage或Microsoft® OneDrive。
* 使用表单数据模型(FDM)将数据无缝发送到配置的数据源。
* 方便地将数据提交到 REST 端点。

## 提交由自适应Forms支持的操作

AEM forms提供了以下现成的提交操作：

* [发送电子邮件](/help/forms/configure-submit-action-send-email.md)
* [调用 Power Automate 流](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [调用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [使用表单数据模型（FDM）提交](/help/forms/using-form-data-model.md)
* [提交到 Azure Blob 存储](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
* [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [调用 AEM 工作流](/help/forms/configure-submit-action-workflow.md)
* [提交到Marketo启用](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [提交到Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [提交到电子表格](/help/forms/forms-submission-service.md)

您还可以将自适应表单提交到其他存储配置：

* [将自适应表单连接到 Salesforce 应用程序](/help/forms/aem-forms-salesforce-integration.md)
* [将自适应表单连接到 Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

## 跨创作类型提交操作支持

下表显示了AEM Forms中使用的表单创作方法支持哪些提交操作：

| 提交操作 | [基础组件](/help/forms/configuring-submit-actions.md) | [核心组件](/help/forms/configure-submit-actions-core-components.md) | [通用编辑器](/help/forms/configure-submit-action-eds-forms.md#submit-actions-supported-by-adaptive-forms-created-in-universal-editor) | [基于文档的Forms](/help/forms/configure-submit-action-eds-forms.md#supported-submit-actions-for-document-based-forms) |
|----------------------------|------------------------|------------------|------------------|------------------------|
| 发送电子邮件 | 支持✅ | 支持✅ | 支持✅ |                        |
| Power Automate流 | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交到 SharePoint | 支持✅ | 支持✅ | 支持✅ |                        |
| Workfront Fusion | 支持✅ | 支持✅ | 支持✅ |                        |
| 使用FDM提交 | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交到AEP | 支持✅ | 支持✅ | 支持✅ |                        |
| Azure Blob存储 | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交到REST端点 | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交至 Marketo Engage | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交到 OneDrive | 支持✅ | 支持✅ | 支持✅ |                        |
| 调用 AEM 工作流 | 支持✅ | 支持✅ | 支持✅ |                        |
| 提交到电子表格 |                        |                  | 支持✅ | 支持✅ |


## 自适应表单中的服务器端重新验证

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些 JavaScript 验证来强制实施一些业务规则。但在现代浏览器中，最终用户有办法绕过这些验证，并使用各种技术（例如，Web Browser DevTools Console）手动进行提交。此类技术也适用于自适应表单。尽管表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑并向服务器提交无效数据。无效数据会破坏表单作者强制实施的业务规则。

此外，利用服务器端重新验证功能，可以运行自适应表单作者在服务器上设计自适应表单时提供的验证。这可防止任何可能的数据提交损害和与表单验证相关的业务规则违反情况。


### 在服务器上进行哪些验证？

在服务器上重新运行的自适应表单的所有现成的 (OOTB) 字段验证包括：

* 必填
* 验证图片子句
* 验证表达式

使用边栏中自适应表单容器下方的&#x200B;**[!UICONTROL 在服务器上重新验证]**，可以为当前表单启用或禁用服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

**启用服务器端验证**

如果最终用户绕过这些验证并提交表单，服务器将重新执行验证。如果服务器端验证失败，则将停止提交事务。用户将再次看到原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
>
>服务器端验证将验证表单模型。建议您创建一个单独的客户端库以用于验证，不要将它与同一客户端库中的 HTML 样式和 DOM 操作等其他项混合。

<!--### Supporting Custom functions in Validation Expressions {#supporting-custom-functions-in-validation-expressions-br}

At times, if there are **complex validation rules**, the exact validation script reside in custom functions and author calls these custom functions from field validation expression. To make this custom function library known and available while performing server-side validations, the form author can configure the name of AEM client library under the **[!UICONTROL Basic]** tab of Adaptive Form Container properties as shown below.

![Supporting Custom functions in Validation Expressions](assets/clientlib-cat.png)

Supporting Custom functions in Validation Expressions

Author can configure customJavaScript library per Adaptive Form. In the library, only keep the reusable functions, which have dependency on jquery and underscore.js third-party libraries.

Refer to the following articles to learn how to create custom functions for:

* [Adaptive Forms based on Foundation Components](/help/forms/rule-editor.md#custom-functions-in-rule-editor)
* [Adaptive Forms based on Core Components](/help/forms/create-and-use-custom-functions.md)
* [Adaptive Forms authored using Document-Based Authoring](/help/edge/docs/forms/rules-forms.md#create-a-custom-function)
* [Adaptive Forms created using the Universal Editor](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#create-a-custom-function)

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.-->

## 另请参阅

{{af-submit-action}}

