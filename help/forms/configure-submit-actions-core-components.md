---
title: 如何配置自适应表单的提交操作
description: 自适应表单提供了多个提交操作。提交操作定义了提交后处理自适应表单的方式。您可以使用内置的提交操作或创建您自己的提交操作。
hide: true
hidefromtoc: true
source-git-commit: be57fe6c54f2ee07378e16bae601500f71e7ce6b
workflow-type: tm+mt
source-wordcount: '3575'
ht-degree: 95%

---

# 自适应表单提交操作 {#configuring-the-submit-action}

<span class="preview"> Adobe 建议使用核心组件[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)或[创建独立的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service | 本文 |
| 应用到 | ✅ 自适应表单核心组件，❎[自适应表单基础组件](/help/forms/configuring-submit-actions.md) |


提交操作让您选择通过自适应表单捕获的数据的目标。当用户单击自适应表单上的&#x200B;**[!UICONTROL 提交]**&#x200B;按钮时，将触发此操作。Forms as a Cloud Service（针对基于核心组件的自适应表单）提供了一系列预建的提交操作。这些现成的提交操作可让您：

* 通过电子邮件轻松发送表单数据。
* 在传输数据时启动 Microsoft Power Automate 流程或 AEM 工作流。
* 直接将表单数据传输到 Microsoft SharePoint Server、Microsoft Azure Blob 存储或 Microsoft OneDrive。
* 使用表单数据模型将数据无缝发送到配置的数据源。
* 方便地将数据提交到 REST 端点。

您也可以[扩展默认提交操作](custom-submit-action-form.md)以创建您自己的提交操作。

## 选择并配置自适应表单的提交操作 {#select-and-configure-submit-action}

要为表单选择并配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。

1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。

   ![单击扳手图标以打开“自适应表单容器”对话框来配置提交操作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 根据要求选择并配置&#x200B;**[!UICONTROL 提交操作]**。有关所选提交操作的详细信息，请参阅：

   * [发送电子邮件](#send-email)
   * [提交到 SharePoint](#submit-to-sharedrive)
   * [使用表单数据模型提交](#submit-using-form-data-model)
   * [提交到 Azure Blob 存储](#azure-blob-storage)
   * [提交到 REST 端点](#submit-to-rest-endpoint)
   * [提交到 OneDrive](#submit-to-onedrive)
   * [调用 AEM 工作流](#invoke-an-aem-workflow)
   * [提交到Power Automate](#microsoft-power-automate)

## 发送电子邮件 {#send-email}

要在成功提交表单后向一个或多个收件人发送电子邮件，您可以使用&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;提交操作。利用此操作，可以创建一封包含预定义格式的表单数据的电子邮件。例如，考虑使用以下模板，其中从提交的表单数据中检索客户名称、配送地址、州名称和邮政编码：

    ```
    
    ${customer_Name}，您好！
    
    以下内容设定为您的默认配送地址：
    ${customer_Name}，
    ${customer_Shipping_Address}，
    ${customer_State}，
    ${customer_ZIPCode}
    
    此致，
    WKND
    
    ```

>[!NOTE]
>
> * 对于所有表单字段来说，拥有唯一的元素名称至关重要，即使它们位于自适应表单中的不同面板上。
> * 在使用 AEM as a Cloud Service 时，出站电子邮件需要进行加密。默认情况下，出站电子邮件功能处于禁用状态。要激活此功能，请提交支持票证以[请求访问权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=zh-Hans#sending-email)。

此外，**[!UICONTROL 发送电子邮件]**&#x200B;提交操作提供了在电子邮件中包含附件和记录文档 (DoR) 的选项。

要启用[!UICONTROL 附加记录文档]选项，请参阅有关[配置自适应表单以生成记录文档 (DoR)](generate-document-of-record-core-components.md)的文档。您可以从自适应表单属性中启用此选项。

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

## 提交到 SharePoint {#submit-to-sharedrive}

**[!UICONTROL 提交到 SharePoint]**&#x200B;提交操作将自适应表单与 Microsoft® SharePoint 存储连接起来。您可以将表单数据、文件、附件或记录文档提交到连接的 Microsoft® Sharepoint 存储。要在自适应表单中使用&#x200B;**[!UICONTROL 提交到 SharePoint]** 提交操作，请执行以下操作：

1. [创建 SharePoint 配置](#create-a-sharepoint-configuration-create-sharepoint-configuration)：它将 AEM Forms 连接到 Microsoft® Sharepoint 存储。
2. [在自适应表单中使用“提交到 SharePoint”提交操作](#use-sharepoint-configuartion-in-af)：它将自适应表单连接到配置的 Microsoft® SharePoint。

### 创建 SharePoint 配置 {#create-sharepoint-configuration}

要将 AEM Forms 连接到 Microsoft® Sharepoint 存储，请执行以下操作：

1. 转到 **AEM Forms** 实例 > **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**。
1. 选择&#x200B;**配置容器**。不要单击配置容器的复选框。单击配置容器的名称以将其选中。配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。这将显示 SharePoint 配置向导。
   ![SharePoint 配置](/help/forms/assets/sharepoint_configuration.png)
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。将 `[author-instance]` 替换为 AEM Forms 创作实例的 URL。
   * 添加 API 权限 `offline_access` 和 `Sites.Manage.All` 以提供读/写权限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

   >[!NOTE]
   >
   > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。

1. 要选择文件夹来保存数据，请选择 **SharePoint Site** > **文档库** > **SharePoint 文件夹**。

   >[!NOTE]
   >
   >* 默认情况下，`forms-ootb-storage-adaptive-forms-submission` 文件夹可在选定的 SharePoint Site 中使用。如果该文件夹不可用，请使用&#x200B;**创建文件夹**&#x200B;选项来创建它。

现在，您可以在自适应表单中将此 SharePoint Sites 配置用于&#x200B;**提交到 SharePoint** 提交操作。

### 在自适应表单中使用“提交到 SharePoint”提交操作 {#use-sharepoint-configuartion-in-af}

您可以使用上一部分中创建的 SharePoint 配置，将数据或记录文档保存到 SharePoint 文件夹中。执行以下步骤，在自适应表单中使用“提交到 SharePoint”提交操作：

1. 创建[自适应表单](/help/forms/creating-adaptive-form.md)。在创建自适应表单时，选择用于[创建 SharePoint 配置](#create-sharepoint-configuration)的[!UICONTROL 配置容器]。

   >[!NOTE]
   >
   > 如果未选择[!UICONTROL 配置容器]，全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

1. 选择&#x200B;**[!UICONTROL 提交到 SharePoint]** 作为&#x200B;**提交操作**。
1. 选择已配置的&#x200B;**[!UICONTROL 存储配置]**。它指定 SharePoint 中用于保存表单数据和记录文档的文件夹。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

在提交表单时，数据将保存到指定的 Microsoft® Sharepoint 存储位置（文件夹）中。
已保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 使用表单数据模型提交 {#submit-using-form-data-model}

**[!UICONTROL 使用表单数据模型提交]**&#x200B;提交操作将表单数据模型中指定的数据模型对象的已提交自适应表单数据写入其数据源。在配置该提交操作时，可以选择要将其提交数据写回其数据源的数据模型对象。

此外，您可以使用表单数据模型和记录文档 (DoR) 将表单附件提交到数据源。有关表单数据模型的信息，请参阅[[!DNL AEM Forms] 数据集成](data-integration.md)。

## 提交到 REST 端点 {#submit-to-rest-endpoint}

使用&#x200B;**[!UICONTROL 提交到 REST 端点]**&#x200B;操作将提交的数据发布到 REST URL。该 URL 可以属于内部服务器（呈现表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。数据将发布到资源的路径。例如，/content/restEndPoint。对于此类 POST 请求，将使用提交请求的身份验证信息。

要将数据发布到外部服务器，请提供 URL。URL 的格式为 `https://host:port/path_to_rest_end_point`。确保配置以匿名方式处理 POST 请求的路径。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，使用参数 `param1` 捕获用户在 `textbox` 中输入的信息。用于发布使用 `param1` 捕获的数据的语法为：

`String data=request.getParameter("param1");`

同样，用于发布 XML 数据和附件的参数为 `dataXml` 和 `attachments`。

例如，您在脚本中使用这两个参数来解析传输到 REST 端点的数据。您使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中，`data` 存储 XML 数据，`att` 存储附件数据。

**[!UICONTROL 提交到 REST 端点]**&#x200B;提交操作将表单中填入的数据作为 HTTP GET 请求的一部分提交到配置的确认页面。您可以添加要请求的字段的名称。请求的格式为：

`{fieldName}={request parameter name}`

如下图所示，`param1` 和 `param2` 作为参数传递，其值是从下一操作中使用的&#x200B;**文本框**&#x200B;和&#x200B;**数字框**&#x200B;字段复制的。

![配置 REST 端点提交操作](assets/action-config.png)

您也可以&#x200B;**[!UICONTROL 启用 POST 请求]**&#x200B;并提供用于发布请求的 URL。要将数据提交到托管表单的 AEM 服务器，请使用与 AEM 服务器的根路径对应的相对路径。例如，`/content/forms/af/SampleForm.html`。要将数据提交到任何其他服务器，请使用绝对路径。

>[!NOTE]
>
>要将字段作为 REST URL 中的参数传递，所有字段都必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->



<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## 调用 AEM 工作流 {#invoke-an-aem-workflow}

**[!UICONTROL 调用 AEM 工作流]**&#x200B;提交操作将自适应表单与 [AEM 工作流](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)相关联。在提交表单时，关联的工作流将在创作实例上自动启动。您可以将数据文件、附件和记录文档保存到工作流的负载位置或变量。如果已为外部数据存储标记和配置工作流，则仅变量选项可用。您可以从可用于工作流模型的变量的列表中进行选择。如果在稍后阶段而不是在创建工作流时为外部数据存储标记了工作流，请确保所需的变量配置已到位。

该提交操作将以下内容放置在工作流的负载位置或变量中（如果为外部数据存储标记了工作流）：

* **数据文件**：它包含已提交到自适应表单的数据。您可以使用&#x200B;**[!UICONTROL 数据文件路径]**&#x200B;选项来指定文件名和相对于负载的文件路径。例如，`/addresschange/data.xml` 路径会创建一个名为 `addresschange` 的文件夹，并将它放置在负载的相对位置。您也可以仅指定 `data.xml` 以仅发送提交的数据而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

* **附件**：您可以使用&#x200B;**[!UICONTROL 附件路径]**&#x200B;选项指定用于存储已上传到自适应表单的附件的文件夹名称。该文件夹是相对于负载创建的。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

* **记录文档**：它包含为自适应表单生成的记录文档。您可以使用&#x200B;**[!UICONTROL 记录文档路径]**&#x200B;选项来指定记录文档的文件名以及相对于负载的文件路径。例如，`/addresschange/DoR.pdf` 路径将创建一个相对于负载的名为 `addresschange` 的文件夹，并相对于负载放置 `DoR.pdf`。您也可以仅指定 `DoR.pdf` 以仅保存记录文档而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

使用&#x200B;**[!UICONTROL 调用 AEM 工作流]**&#x200B;提交操作之前，为 **[!UICONTROL AEM DS 设置服务]**&#x200B;配置进行以下设置：

* **[!UICONTROL 处理服务器 URL]**：处理服务器是触发表单或 AEM 工作流的服务器。这可以与 AEM 创作实例或其他服务器的 URL 相同。

* **[!UICONTROL 处理服务器用户名]**：工作流用户的用户名

* **[!UICONTROL 处理服务器密码]**：工作流用户的密码



## 提交到 OneDrive {#submit-to-onedrive}

**[!UICONTROL 提交到 OneDrive]**&#x200B;提交操作将自适应表单与 Microsoft® OneDrive 连接起来。您可以将表单数据、文件、附件或记录文档提交到连接的 Microsoft® OneDrive 存储。要在自适应表单中使用[!UICONTROL 提交到 OneDrive] 提交操作，请执行以下操作：

1. [创建 OneDrive 配置](#create-a-onedrive-configuration-create-onedrive-configuration)：它将 AEM Forms 连接到 Microsoft® OneDrive 存储。
2. [在自适应表单中使用“提交到 OneDrive”提交操作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：它将自适应表单
连接到配置的 Microsoft® OneDrive。

### 创建 OneDrive 配置 {#create-onedrice-configuration}

要将 AEM Forms 连接到 Microsoft® OneDrive 存储，请执行以下操作：

1. 转到 **AEM Forms 创作**&#x200B;实例 > **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® OneDrive]**。
1. 选定 **[!UICONTROL Microsoft® OneDrive]** 后，您将重定向到 **[!UICONTROL OneDrive 浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。这将显示 OneDrive 配置向导。

   ![OneDrive 配置屏幕](/help/forms/assets/onedrive-configuration.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 添加 API 权限 `offline_access` 和 `Files.ReadWrite.All` 以提供读/写权限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

   >[!NOTE]
   >
   > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。

1. 现在，选择 **[!UICONTROL OneDrive 容器]** > **[OneDrive 文件夹]**&#x200B;以保存数据。

   >[!NOTE]
   >
   >* 默认情况下，`forms-ootb-storage-adaptive-forms-submission` 位于 OneDrive 容器中。
   > * 通过单击&#x200B;**创建文件夹**&#x200B;来创建一个 `forms-ootb-storage-adaptive-forms-submission` 形式的文件夹（如果该文件夹不存在）。

现在，您可以在自适应表单中将此 OneDrive 存储配置用于提交操作。

### 在自适应表单中使用 OneDrive 配置 {#use-onedrive-configuartion-in-af}

您可以在自适应表单中使用创建的 OneDrive 存储配置，将数据或生成的记录文档保存在 OneDrive 文件夹中。在以下情况下，执行以下步骤可在自适应表单中使用 OneDrive 存储配置：
1. 创建[自适应表单](/help/forms/creating-adaptive-form.md)。

   >[!NOTE]
   >
   > * 为自适应表单选择相同的[!UICONTROL 配置容器]，您已在其中创建 OneDrive 存储。
   > * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

1. 选择&#x200B;**[!UICONTROL 提交到 OneDrive]** 作为&#x200B;**提交操作**。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

在提交表单时，数据将保存在指定的 Microsoft® OneDrive 存储中。
用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 提交到 Azure Blob 存储 {#submit-to-azure-blob-storage}

**[!UICONTROL 提交到 Azure Blob 存储]**&#x200B;提交操作将自适应表单与 Microsoft® Azure 门户连接起来。您可以将表单数据、文件、附件或记录文档提交到连接的 Azure 存储容器。要使用 Azure Blob 存储的提交操作，请执行以下操作：

1. [创建 Azure Blob 存储容器](#create-a-azure-blob-storage-container-create-azure-configuration)：它将 AEM Forms 连接到 Azure 存储容器。
2. [在自适应表单中使用 Azure 存储配置](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：它将自适应表单连接到配置的 Azure 存储容器。

### 创建 Azure Blob 存储容器 {#create-azure-configuration}

要将 AEM Forms 连接到 Azure 存储容器，请执行以下操作：
1. 转到 **AEM Forms 创作**&#x200B;实例 > **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure 存储]**。
1. 选定 **[!UICONTROL Azure 存储]**&#x200B;后，您将重定向到 **[!UICONTROL Azure 存储浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。这将显示“创建 Azure 存储配置”向导。

   ![Azure 存储配置](/help/forms/assets/azure-storage-configuration.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL Azure 存储帐户]**&#x200B;和 **[!UICONTROL Azure 访问密钥]**。

   * 您可以从 Microsoft® Azure 门户中的存储帐户检索 `Azure Storage Account`名称和 `Azure Access key`。

1. 单击&#x200B;**[!UICONTROL 保存]**。

现在，您可以在自适应表单中将此 Azure 存储容器配置用于提交操作。

### 在自适应表单中使用 Azure 存储配置 {#use-azure-storage-configuartion-in-af}

您可以在自适应表单中使用创建的 Azure 存储容器配置，将数据或生成的记录文档保存在 Azure 存储容器中。执行以下步骤可在自适应表单中使用 Azure 存储容器配置：
1. 创建[自适应表单](/help/forms/creating-adaptive-form.md)。

   >[!NOTE]
   >
   > * 为自适应表单选择相同的[!UICONTROL 配置容器]，您已在其中创建 OneDrive 存储。
   > * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

1. 选择&#x200B;**[!UICONTROL 提交到 Azure Blob 存储]**&#x200B;作为&#x200B;**提交操作**。
   ![Azure Blob 存储 GIF](/help/forms/assets/azure-submit-video.gif)

1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

提交表单时，数据将保存在指定的 Azure 存储容器配置中。
用于保存数据的文件夹结构是 `/configuration_container/form_name/year/month/date/submission_id/data`。

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process)。


## 提交到Power Automate {#microsoft-power-automate}

您可以配置自适应表单以在提交时运行Microsoft® Power Automate Cloud Flow。 配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automation Cloud Flow 进行处理。 它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。以下是自适应表单与Microsoft® Power Automate集成后可执行的操作示例：

* 在Power Automate业务流程中使用自适应Forms数据
* 使用Power Automate将捕获的数据发送到500多个数据源或任何公开可用的API
* 对捕获的数据执行复杂的计算
* 按预定义的计划将自适应Forms数据保存到存储系统

自适应Forms编辑器提供 **调用Microsoft® Power Automate流** 将自适应表单数据、附件和记录文档的提交操作发送到Power Automate Cloud Flow。 要使用Submit操作将捕获的数据发送到Microsoft®Power Automate， [将Formsas a Cloud Service实例与Microsoft® Power Automate连接](forms-microsoft-power-automate-integration.md)

成功配置后，使用 [调用Microsoft® Power Automate流](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) 提交操作以将数据发送到Power Automate流。

## 使用同步或异步提交 {#use-synchronous-or-asynchronous-submission}

提交操作可使用同步或异步提交。

**同步提交**：传统上，Web 表单配置为以同步方式提交。在同步提交中，当用户提交表单时，他们将重定向到确认页面、感谢页面或（如果提交失败）错误页面。您可以选择&#x200B;**[!UICONTROL 使用异步提交]**&#x200B;选项，将用户重定向到网页或在提交时显示消息。

![配置提交操作](assets/thank-you-setting.png)

**异步提交**：像单页面应用程序这样的现代 Web 体验越来越受欢迎，其中网页保持静态，而客户端与服务器的交互在后台进行。您现在可以通过[配置异步提交](asynchronous-submissions-adaptive-forms.md)来使用自适应表单提供此体验。

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些 JavaScript 验证来强制实施一些业务规则。但在现代浏览器中，最终用户有办法绕过这些验证，并使用各种技术（例如，Web Browser DevTools Console）手动进行提交。此类技术也适用于自适应表单。尽管表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑并向服务器提交无效数据。无效数据会破坏表单作者强制实施的业务规则。

此外，利用服务器端重新验证功能，可以运行自适应表单作者在服务器上设计自适应表单时提供的验证。这可防止任何可能的数据提交损害和与表单验证相关的业务规则违反情况。

### 在服务器上进行哪些验证？ {#what-to-validate-on-server-br}

在服务器上重新运行的自适应表单的所有现成的 (OOTB) 字段验证包括：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用边栏中自适应表单容器下方的&#x200B;**[!UICONTROL 在服务器上重新验证]**，可以为当前表单启用或禁用服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将重新执行验证。如果服务器端验证失败，则将停止提交事务。最终用户将再次看到原始表单。捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
>
>服务器端验证将验证表单模型。建议您创建一个单独的客户端库以用于验证，不要将它与同一客户端库中的 HTML 样式和 DOM 操作等其他项混合。

### 支持验证表达式中的自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果存在&#x200B;**复杂的验证规则**，则准确的验证脚本驻留在自定义函数中，并且作者从字段验证表达式中调用这些自定义函数。要在执行服务器端验证时使此自定义函数库已知并可用，表单作者可以在自适应表单容器属性的&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡下配置 AEM 客户端库的名称，如下所示。

![支持验证表达式中的自定义函数](assets/clientlib-cat.png)

支持验证表达式中的自定义函数

作者可以为每个自适应表单配置自定义 JavaScript 库。该库中只保留可重用的函数，这些函数依赖 jquery 和 underscore.js 第三方库。

## 提交操作的错误处理 {#error-handling-on-submit-action}

作为 AEM 安全和强化指南的一部分，配置自定义错误页面，例如 400.jsp、404.jsp 和 500.jsp。如果提交表单时出现 400、404 或 500 错误，则将调用这些处理程序。在发布节点上触发这些错误代码时，也将调用处理程序。您还可以为其他 HTTP 错误代码创建 JSP 页面。

在使用符合架构（其中数据不包含 `<afData>`、`<afBoundData>` 和 `</afUnboundData>` 标签）的 XML 或 JSON 数据预填充表单数据模型或基于架构的自适应表单时，自适应表单的未绑定字段的数据将丢失。该架构可以是 XML 架构、JSON 架构或表单数据模型。未绑定的字段是自适应表单字段，不带 `bindref` 属性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
