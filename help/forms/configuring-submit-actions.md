---
title: 如何为自适应表单配置提交操作
description: 自适应表单提供了多个提交操作。 提交操作定义提交后如何处理自适应表单。 您可以使用内置的提交操作或创建您自己的操作。
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 895290aa0080e159549cd2de70f0e710c4a0ee34
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 3%

---

# 自适应表单提交操作 {#configuring-the-submit-action}

用户单击 **[!UICONTROL 提交]** 按钮。 自适应Forms提供了一些开箱即用的提交操作。 现成可用的提交操作包括：

* [提交到REST端点](#submit-to-rest-endpoint)
* [发送电子邮件](#send-email)
* [使用表单数据模型提交](#submit-using-form-data-model)
* [调用AEM工作流](#invoke-an-aem-workflow)

您还可以 [扩展默认的提交操作](custom-submit-action-form.md) 创建您自己的提交操作。

您可以在 **[!UICONTROL 提交]** 自适应表单容器属性的部分。

![配置提交操作](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.


-->




## 提交到REST端点 {#submit-to-rest-endpoint}

使用 **[!UICONTROL 提交到REST端点]** 操作将提交的数据发布到rest URL。 URL可以是内部服务器（呈现表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。 数据将发布到资源的路径中。 例如， /content/restEndPoint。 对于这种帖子请求，使用提交请求的验证信息。

要将数据发布到外部服务器，请提供URL。 URL的格式为 `https://host:port/path_to_rest_end_point`. 确保以匿名方式配置路径以处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上例中，用户在 `textbox` 使用参数捕获 `param1`. 用于发布使用 `param1` 为：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数也是 `dataXml` 和 `attachments`.

例如，在脚本中使用这两个参数将数据解析到其余的端点。 使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在本例中， `data` 存储XML数据， `att` 存储附件数据。

的 **[!UICONTROL 提交到REST端点]** 提交操作会将表单中填写的数据作为HTTPGET请求的一部分提交到配置的确认页面。 您可以添加要请求的字段名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示， `param1` 和 `param2` 将作为参数进行传递，并且值复制自 **文本框** 和 **数字框** 字段。

![配置Rest端点提交操作](assets/action-config.png)

您还可以 **[!UICONTROL 启用POST请求]** 和提供用于发布请求的URL。 要向托管表单的AEM服务器提交数据，请使用与AEM服务器的根路径对应的相对路径。 例如, `/content/forms/af/SampleForm.html`. 要向任何其他服务器提交数据，请使用绝对路径。

>[!NOTE]
>
>要在REST URL中将字段作为参数传递，所有字段必须具有不同的元素名称，即使这些字段放置在不同的面板上也是如此。

## 发送电子邮件 {#send-email}

您可以使用 **[!UICONTROL 发送电子邮件]** 提交操作，以在成功提交表单时向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。 例如，在以下模板中，将从提交的表单数据中检索客户名称、送货地址、状态名称和邮政编码。

    &quot;
    
    您好${customer_Name},
    
    以下是默认送货地址：
    ${customer_name},
    ${customer_Shipping_Address},
    ${customer_state},
    ${customer_ZIPCode}
    
    敬
    WKND
    
    &quot;

>[!NOTE]
>
> * 所有表单字段必须具有不同的元素名称，即使这些字段放置在自适应表单的不同面板上也是如此。
> * AEMas a Cloud Service要求对出站邮件进行加密。 默认情况下，禁用出站电子邮件。 要激活它，请将支持票证提交到 [请求访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


您还可以在电子邮件中包含附件和记录文档(DoR)。 启用 **[!UICONTROL 附加记录文档]** ，请配置自适应表单以生成记录文档(DoR)。 您可以启用选项，以从“自适应表单”属性生成记录文档。



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## 使用表单数据模型提交 {#submit-using-form-data-model}

的 **[!UICONTROL 使用表单数据模型提交]** 提交操作会将表单数据模型中指定数据模型对象提交的自适应表单数据写入其数据源。 在配置提交操作时，您可以选择要将其提交的数据写回其数据源的数据模型对象。

此外，您还可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。 有关表单数据模型的信息，请参阅 [[!DNL AEM Forms] 数据集成](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## 调用AEM工作流 {#invoke-an-aem-workflow}

的 **[!UICONTROL 调用AEM工作流]** 提交操作将自适应表单与 [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). 提交表单后，关联的工作流将自动在创作实例上启动。 您可以将数据文件、附件和记录文档保存到工作流的有效负荷位置或变量中。 如果为外部数据存储标记了工作流并为外部数据存储配置了工作流，则只有变量选项可用。 您可以从可用于工作流模型的变量列表中进行选择。 如果在以后阶段而不是在创建工作流时将工作流标记为外部数据存储，请确保已设置所需的变量配置。

提交操作会将以下内容放置在工作流的有效负载位置，或者如果将工作流标记为外部数据存储，则放置变量：

* **数据文件**:它包含提交到自适应表单的数据。 您可以使用 **[!UICONTROL 数据文件路径]** 选项，以指定文件的名称和相对于有效负载的文件路径。 例如， `/addresschange/data.xml` 路径会创建名为 `addresschange` 并将其放置在有效载荷上。 您还可以仅指定 `data.xml` ，以便在不创建文件夹层次结构的情况下仅发送提交的数据。 如果工作流标记为外部数据存储，请使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

* **附件**:您可以使用 **[!UICONTROL 附件路径]** 选项，以指定用于存储上传到自适应表单的附件的文件夹名称。 文件夹是相对于有效负载创建的。 如果工作流标记为外部数据存储，请使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

* **记录文档**:它包含为自适应表单生成的记录文档。 您可以使用 **[!UICONTROL 记录路径文档]** 选项，指定记录文档的名称和相对于有效负荷的文件路径。 例如， `/addresschange/DoR.pdf` 路径会创建名为 `addresschange` 相对于有效负载，并将 `DoR.pdf` 相对于有效载荷。 您还可以仅指定 `DoR.pdf` 以仅保存记录文档，而不创建文件夹层次结构。 如果工作流标记为外部数据存储，请使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

在使用 **[!UICONTROL 调用AEM工作流]** 提交操作为 **[!UICONTROL AEM DS设置服务]** 配置：

* **[!UICONTROL 处理服务器URL]**:处理服务器是触发Forms或AEM工作流的服务器。 此URL可以与AEM创作实例或其他服务器的URL相同。

* **[!UICONTROL 处理服务器用户名]**:工作流用户的用户名

* **[!UICONTROL 处理服务器密码]**:工作流用户的密码

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 使用同步或异步提交 {#use-synchronous-or-asynchronous-submission}

提交操作可以使用同步或异步提交。

**同步提交**:传统上，Web表单配置为同步提交。 在同步提交中，当用户提交表单时，会将用户重定向到确认页面、感谢页面，或者如果提交失败，则会重定向到错误页面。 您可以选择 **[!UICONTROL 使用异步提交]** 选项，将用户重定向到网页或在提交时显示消息。

![配置提交操作](assets/thank-you-setting.png)

**异步提交**:现代Web体验（如单页应用程序）越来越受欢迎，其中网页保持静态，而客户端 — 服务器交互在后台进行。 您现在可以通过自适应Forms提供此体验，具体方式为 [配置异步提交](asynchronous-submissions-adaptive-forms.md).

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员会在客户端放置一些JavaScript验证，以强制执行一些业务规则。 但在现代浏览器中，最终用户可以绕过这些验证，使用各种技术（如Web浏览器开发工具控制台）手动执行提交。 此类技术也适用于自适应Forms。 表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑，将无效数据提交到服务器。 无效数据会破坏表单作者强制执行的业务规则。

服务器端重新验证功能还允许运行自适应Forms作者在服务器上设计自适应表单时提供的验证。 它可防止在表单验证中表示的数据提交和业务规则违规的任何潜在危害。

### 在服务器上验证什么？ {#what-to-validate-on-server-br}

自适应表单的开箱即用(OOTB)字段验证（将在服务器中重新运行）包括：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用 **[!UICONTROL 在服务器上重新验证]** 在侧栏的自适应表单容器下，启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将再次执行验证。 如果验证在服务器端失败，则提交事务将停止。 最终用户将再次看到原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
>
>服务器端验证可验证表单模型。 建议您创建一个单独的客户端库以进行验证，但不要将其与HTML样式和DOM操作等其他内容混合到同一客户端库中。

### 在验证表达式中支持自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果 **复杂验证规则**，则精确验证脚本位于自定义函数中，并且作者从字段验证表达式中调用这些自定义函数。 要在执行服务器端验证时将此自定义函数库知晓并可用，表单作者可以在 **[!UICONTROL 基本]** 自适应表单容器属性的选项卡，如下所示。

![在验证表达式中支持自定义函数](assets/clientlib-cat.png)

在验证表达式中支持自定义函数

作者可以根据自适应表单配置customJavaScript库。 在库中，仅保留依赖于jquery和undersore.js第三方库的可重用函数。

## 处理提交操作时出错 {#error-handling-on-submit-action}

作为AEM安全和强化准则的一部分，请配置自定义错误页，如400.jsp、404.jsp和500.jsp。 在提交表单400、404或500错误时，会调用这些处理程序。 当在“发布”节点上触发这些错误代码时，也会调用处理程序。 您还可以为其他HTTP错误代码创建JSP页。

当您使用XML或JSON数据预填表单数据模型或基于架构的自适应表单时，会向数据不包含的架构投诉 `<afData>`, `<afBoundData>`和 `</afUnboundData>` 标记，则自适应表单的无界字段的数据将丢失。 架构可以是XML架构、JSON架构或表单数据模型。 无界字段是自适应表单字段， `bindref` 属性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
