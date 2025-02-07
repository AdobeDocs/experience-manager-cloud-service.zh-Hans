---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST端点，提交到REST端点，将数据发布到REST URL，配置REST端点操作
feature: Adaptive Forms, Core Components
title: 如何为自适应表单配置提交操作？
role: User, Developer
source-git-commit: c20b8909bb884f14bd7fe59f190de3cd375a7111
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 56%

---

# 为REST端点提交操作配置自适应表单

使用&#x200B;**[!UICONTROL 提交到REST端点]**&#x200B;操作将提交的数据发布到REST URL。 该 URL 可以属于内部服务器（呈现表单的服务器）或外部服务器。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。

## 优点

为自适应Forms配置&#x200B;**[!UICONTROL 提交到REST端点]**&#x200B;提交操作的一些优点包括：

* 它通过RESTful API实现了表单数据与外部系统和服务的无缝集成。
* 它提供了灵活性，可处理从自适应Forms提交的数据，并支持动态和复杂的数据结构。
* 它支持将表单字段动态映射到REST端点URL中的参数，从而允许进行自适应和可自定义的数据提交。


## 配置提交到REST端点提交操作 {#steps-to-configure-submit-to-restendpoint-submit-action}

要根据Swagger Open API规范配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 提交到Rest终结点]**。
   提交到Rest终结点的![操作配置](/help/forms/assets/submit-action-restendpoint.png)

   要将数据发布到内部服务器，请提供资源的路径。数据将发布到资源的路径。例如，`/content/restEndPoint`。对于此类 POST 请求，将使用提交请求的身份验证信息。

   要将数据发布到外部服务器，请提供 URL。URL 的格式为 `https://host:port/path_to_rest_end_point`。确保配置以匿名方式处理 POST 请求的路径。

   ![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

   在上面的示例中，使用参数 `param1` 捕获用户在 `textbox` 中输入的信息。用于发布使用 `param1` 捕获的数据的语法为：

   `String data=request.getParameter("param1");`

   同样，用于发布 XML 数据和附件的参数为 `dataXml` 和 `attachments`。

   例如，您在脚本中使用这两个参数来解析传输到 REST 端点的数据。您使用以下语法来存储和解析数据：

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   在此示例中，`data` 存储 XML 数据，`att` 存储附件数据。

   **[!UICONTROL 提交到 REST 端点]**&#x200B;提交操作将表单中填入的数据作为 HTTP GET 请求的一部分提交到配置的确认页面。您可以添加要请求的字段的名称。 请求的格式为：

   `{fieldName}={request parameter name}`

   如下图所示，`param1` 和 `param2` 作为参数传递，其值是从下一操作中使用的&#x200B;**文本框**&#x200B;和&#x200B;**数字框**&#x200B;字段复制的。

   ![配置 REST 端点提交操作](assets/action-config.png)

   您也可以&#x200B;**[!UICONTROL 启用 POST 请求]**&#x200B;并提供用于发布请求的 URL。要将数据提交到托管表单的 AEM 服务器，请使用与 AEM 服务器的根路径对应的相对路径。例如，`/content/forms/af/SampleForm.html`。要将数据提交到任何其他服务器，请使用绝对路径。

1. 单击&#x200B;**[!UICONTROL 完成]**。

### 根据服务Rest端点配置提交操作 {#config-service-endpoint-auth}

<span class="preview">服务终结点功能在早期采用程序下，仅适用于核心组件。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 提交到Rest终结点]**。
1. 启用POST请求。
1. 指定REST端点URL。
1. 选择您为服务Rest端点身份验证类型创建的配置和内容类型。 若要了解有关身份验证类型和内容类型的更多信息，请访问[配置数据源](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)。
   ![配置Rest终结点](assets/rest-service-endpoint-config.png)
1. 单击“完成”。

## 最佳实践

* 将数据发布到外部服务器时，请确保URL的安全，并配置该路径以匿名方式处理POST请求以保护敏感信息。
* 要将字段作为 REST URL 中的参数传递，所有字段都必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

## 相关文章

{{af-submit-action}}
