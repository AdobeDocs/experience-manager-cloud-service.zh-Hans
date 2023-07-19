---
title: 如何为自适应表单配置提交操作
description: 自适应表单提供多个提交操作。 提交操作定义提交后如何处理自适应表单。 您可以使用内置的提交操作或创建自己的提交操作。
hide: true
hidefromtoc: true
source-git-commit: ac9689a911be119ae53d5e1134595c567370b7c4
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 2%

---

# 自适应表单提交操作 {#configuring-the-submit-action}

<span class="preview"> Adobe建议使用核心组件来 [将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) 或 [创建独立的自适应Forms](/help/forms/creating-adaptive-form-core-components.md). </span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service | 本文 |
| 应用到 | ✅自适应表单核心组件，❎ [自适应表单基础组件](/help/forms/configuring-submit-actions.md) |


提交操作允许您选择通过自适应表单捕获的数据的目标。 当用户单击 **[!UICONTROL 提交]** 按钮。 Formsas a Cloud Service针对基于核心组件的自适应Forms，提供了一系列预建提交操作。 这些现成的提交操作使您能够：

* 通过电子邮件轻松发送表单数据。
* 在传输数据时启动Microsoft Power Automate流或AEM Workflow。
* 直接将表单数据传输到Microsoft SharePoint Server、Microsoft Azure Blob Storage或Microsoft OneDrive。
* 使用表单数据模型将数据无缝发送到配置的数据源。
* 方便地将数据提交到REST端点。

您还可以 [扩展默认提交操作](custom-submit-action-form.md) 以创建您自己的提交操作。

## 选择并配置自适应表单的提交操作 {#select-and-configure-submit-action}

要为表单选择并配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。

1. 单击  **[!UICONTROL 提交]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置提交操作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 选择并配置 **[!UICONTROL 提交操作]**，具体取决于您的要求。 有关所选提交操作的详细信息，请参阅：

   * [发送电子邮件](#send-email)
   * [提交到 SharePoint](#submit-to-sharedrive)
   * [使用表单数据模型提交](#submit-using-form-data-model)
   * [提交到 Azure Blob Storage](#azure-blob-storage)
   * [提交到REST端点](#submit-to-rest-endpoint)
   * [提交到 OneDrive](#submit-to-onedrive)
   * [调用AEM Workflow](#invoke-an-aem-workflow)

## 发送电子邮件 {#send-email}

要在成功提交表单后向一个或多个收件人发送电子邮件，您可以使用 **[!UICONTROL 发送电子邮件]** 提交操作。 通过此操作，可创建包含预定义格式的表单数据的电子邮件。 例如，请考虑以下模板，其中从提交的表单数据中检索客户名称、送货地址、省/市/自治区名称和邮政编码：

    ```
    
    嗨${customer_Name}，
    
    以下内容设置为您的默认送货地址：
    ${customer_Name}，
    ${customer_Shipping_Address}，
    ${customer_State}，
    ${customer_ZIPCode}
    
    致敬，
    WKND
    
    ```

>[!NOTE]
>
> * 对于所有表单字段而言，即使它们放置在自适应表单的不同面板上，拥有唯一的元素名称也非常重要。
> * 使用AEMas a Cloud Service时，出站电子邮件需要加密。 默认情况下，出站电子邮件功能处于禁用状态。 要激活它，请将支持票证提交到 [请求访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

此外， **[!UICONTROL 发送电子邮件]** 提交操作提供了将附件和记录文档(DoR)包含在电子邮件中的选项。

要启用 [!UICONTROL 附加记录文档] 选项，请参阅有关以下内容的文档： [配置自适应表单以生成记录文档(DoR)](generate-document-of-record-core-components.md). 您可以从自适应表单属性中启用此选项。

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

此 **[!UICONTROL 提交到SharePoint]** 提交操作可将自适应表单与Microsoft® SharePoint存储相关联。 您可以将表单数据文件、附件或记录文档提交到连接的Microsoft® Sharepoint存储。 要使用 **[!UICONTROL 提交到SharePoint]** 以自适应表单提交操作：

1. [创建SharePoint配置](#create-a-sharepoint-configuration-create-sharepoint-configuration)：用于将AEM Forms连接到您的Microsoft® Sharepoint存储。
2. [在自适应表单中使用提交到SharePoint提交操作](#use-sharepoint-configuartion-in-af)：它将您的自适应表单连接到配置的Microsoft® SharePoint。

### 创建SharePoint配置 {#create-sharepoint-configuration}

要将AEM Forms连接到Microsoft® Sharepoint存储，请执行以下操作：

1. 转到您的 **AEM Forms** 实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 选择 **配置容器**. 请勿单击“Configuration Container（配置容器）”的复选框。 单击配置容器的名称以将其选定。 该配置将存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。此时将显示SharePoint配置向导。
   ![Sharepoint配置](/help/forms/assets/sharepoint_configuration.png)
1. 指定 **[!UICONTROL 标题]**， **[!UICONTROL 客户端ID]**， **[!UICONTROL 客户端密码]** 和 **[!UICONTROL OAuth URL]**. 有关如何检索OAuth URL的客户端ID、客户端密钥和租户ID的信息，请参阅 [Microsoft®文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以检索 `Client ID` 和 `Client Secret` 从Microsoft® Azure门户访问您的应用程序。
   * 在Microsoft® Azure门户中，将重定向URI添加为 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Replace `[author-instance]` 使用AEM Forms创作实例的URL。
   * 添加API权限 `offline_access` 和 `Sites.Manage.All` 以提供读/写权限。
   * 使用OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` 使用 `tenant-id` 从Microsoft® Azure门户访问您的应用程序。

   >[!NOTE]
   >
   > 此 **客户端密码** 字段是必填字段还是可选字段，具体取决于您的Azure Active Directory应用程序配置。 如果您的应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击 **[!UICONTROL Connect]**. 成功连接后， `Connection Successful` 出现消息。

1. 要选择文件夹以保存数据，请选择 **SharePoint站点** > **文档库** > **SharePoint文件夹**， 。

   >[!NOTE]
   >
   >* 默认情况下， `forms-ootb-storage-adaptive-forms-submission` 文件夹在选定的SharePoint站点中可用。 如果该文件夹不可用，请使用 **创建文件夹** 选项来创建它。

现在，您可以将此SharePoint Sites配置用于 **提交到SharePoint** 在自适应表单中提交操作。

### 在自适应表单中使用提交到SharePoint提交操作 {#use-sharepoint-configuartion-in-af}

您可以使用上一节中创建的SharePoint配置将数据或记录文档保存在SharePoint文件夹中。 执行以下步骤，在自适应表单中使用提交到SharePoint提交操作：

1. 创建 [自适应表单](/help/forms/creating-adaptive-form.md). 创建自适应表单时，选择 [!UICONTROL 配置容器] 用于 [创建SharePoint配置](#create-sharepoint-configuration).

   >[!NOTE]
   >
   > 当否 [!UICONTROL 配置容器] 已选中，则全局 [!UICONTROL 存储配置] 文件夹出现在“提交操作”属性窗口中。

1. 选择 **提交操作** 作为 **[!UICONTROL 提交到SharePoint]**.
1. 选择已配置的 **[!UICONTROL 存储配置]**. 它指定SharePoint中用于保存表单数据和记录文档的文件夹。
1. 单击 **[!UICONTROL 保存]** 以保存提交设置。

提交表单时，数据将保存在指定的Microsoft® Sharepoint存储位置（文件夹）中。
已保存数据的文件夹结构为 `/folder_name/form_name/year/month/date/submission_id/data`.

## 使用表单数据模型提交 {#submit-using-form-data-model}

此 **[!UICONTROL 使用表单数据模型提交]** 提交操作将表单数据模型中指定数据模型对象的已提交自适应表单数据写入其数据源。 在配置提交操作时，您可以选择提交的数据要写回其数据源的数据模型对象。

此外，您还可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。 有关表单数据模型的信息，请参阅 [[!DNL AEM Forms] 数据集成](data-integration.md).

## 提交到REST端点 {#submit-to-rest-endpoint}

使用 **[!UICONTROL 提交到REST端点]** 将提交的数据发布到rest URL的操作。 URL可以是内部（渲染表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。 数据被发布为资源的路径。 例如，/content/restEndPoint。 对于此类post请求，使用提交请求的身份验证信息。

要向外部服务器发布数据，请提供URL。 URL的格式为 `https://host:port/path_to_rest_end_point`. 确保将路径配置为匿名处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，用户在 `textbox` 使用参数捕获 `param1`. 用于发布使用捕获的数据的语法 `param1` 为：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数包括 `dataXml` 和 `attachments`.

例如，在脚本中使用这两个参数将数据解析到rest端点。 您可以使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中， `data` 存储XML数据，以及 `att` 存储附件数据。

此 **[!UICONTROL 提交到REST端点]** 提交操作在HTTPGET请求过程中，将表单中填写的数据提交到配置的确认页面。 您可以添加要请求的字段的名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示， `param1` 和 `param2` 作为参数传递，其值复制自 **文本框** 和 **numericbox** 用于执行下一个操作的字段。

![配置Rest端点提交操作](assets/action-config.png)

您还可以 **[!UICONTROL 启用POST请求]** 并提供用于发布请求的URL。 要将数据提交到托管表单的AEM服务器，请使用与AEM服务器的根路径对应的相对路径。 例如：`/content/forms/af/SampleForm.html`。要向任何其他服务器提交数据，请使用绝对路径。

>[!NOTE]
>
>要在REST URL中将这些字段作为参数传递，所有字段必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

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

## 调用AEM Workflow {#invoke-an-aem-workflow}

此 **[!UICONTROL 调用AEM Workflow]** 提交操作将自适应表单与 [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). 提交表单时，关联的工作流会在创作实例上自动启动。 可将数据文件、附件和记录文档保存到工作流的有效负荷位置或变量。 如果工作流标记为外部数据存储并配置为外部数据存储，则只有变量选项可用。 您可以从可用于工作流模型的变量列表中进行选择。 如果工作流在稍后阶段标记为外部数据存储，而不是在创建工作流时标记为外部数据存储，则请确保已设置所需的变量配置。

提交操作将以下内容置于工作流的有效负荷位置，如果工作流标记为外部数据存储，则置于变量：

* **数据文件**：它包含提交到自适应表单的数据。 您可以使用 **[!UICONTROL 数据文件路径]** 选项，用于指定文件的名称以及相对于有效负荷的文件路径。 例如， `/addresschange/data.xml` path创建一个名为的文件夹 `addresschange` 并将其相对于有效负荷放置。 您也可仅指定 `data.xml` 只发送已提交的数据而不创建文件夹层次结构。 如果工作流标记为外部数据存储，请使用变量选项，并从工作流模型的可用变量列表中选择变量。

* **附件**：您可以使用 **[!UICONTROL 附件路径]** 选项，用于指定用于存储已上载到自适应表单的附件的文件夹名称。 将创建相对于有效负荷的文件夹。 如果工作流标记为外部数据存储，请使用变量选项，并从工作流模型的可用变量列表中选择变量。

* **记录文档**：它包含为自适应表单生成的记录文档。 您可以使用 **[!UICONTROL 记录文档路径]** 用于指定记录文档文件的名称以及相对于有效负荷的文件路径的选项。 例如， `/addresschange/DoR.pdf` path创建一个名为的文件夹 `addresschange` 相对于有效负荷，并放置 `DoR.pdf` 相对于有效负荷。 您也可仅指定 `DoR.pdf` 仅保存记录文档，而不创建文件夹层次结构。 如果工作流标记为外部数据存储，请使用变量选项，并从工作流模型的可用变量列表中选择变量。

使用之前 **[!UICONTROL 调用AEM Workflow]** 提交操作为配置以下 **[!UICONTROL AEM DS设置服务]** 配置：

* **[!UICONTROL 处理服务器URL]**：处理服务器是触发Forms或AEM Workflow的服务器。 这可以与AEM创作实例或其他服务器的URL相同。

* **[!UICONTROL 处理服务器用户名]**：工作流用户的用户名

* **[!UICONTROL 处理服务器密码]**：工作流用户的密码



## 提交到 OneDrive {#submit-to-onedrive}

此 **[!UICONTROL 提交到OneDrive]** 提交操作将自适应表单与Microsoft® OneDrive连接。 您可以将表单数据、文件、附件或记录文档提交到连接的Microsoft® OneDrive存储。 要使用 [!UICONTROL 提交到OneDrive] 以自适应表单提交操作：

1. [创建OneDrive配置](#create-a-onedrive-configuration-create-onedrive-configuration)：用于将AEM Forms连接到您的Microsoft® OneDrive存储。
2. [在自适应表单中使用提交到OneDrive提交操作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：它将您的自适应表单连接到配置的Microsoft® OneDrive。

### 创建OneDrive配置 {#create-onedrice-configuration}

要将AEM Forms连接到Microsoft® OneDrive存储，请执行以下操作：

1. 转到您的 **AEM Forms Author** 实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. 一旦您选择 **[!UICONTROL Microsoft® OneDrive]**，您将被重定向到 **[!UICONTROL OneDrive浏览器]**.
1. 选择 **配置容器**. 该配置将存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。出现OneDrive配置向导。

   ![OneDrive配置屏幕](/help/forms/assets/onedrive-configuration.png)

1. 指定 **[!UICONTROL 标题]**， **[!UICONTROL 客户端ID]**， **[!UICONTROL 客户端密码]** 和 **[!UICONTROL OAuth URL]**. 有关如何检索OAuth URL的客户端ID、客户端密钥和租户ID的信息，请参阅 [Microsoft®文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以检索 `Client ID` 和 `Client Secret` 从Microsoft® Azure门户访问您的应用程序。
   * 在Microsoft® Azure门户中，将重定向URI添加为 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Replace `[author-instance]` 使用创作实例的URL。
   * 添加API权限 `offline_access` 和 `Files.ReadWrite.All` 以提供读/写权限。
   * 使用OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` 使用 `tenant-id` 从Microsoft® Azure门户访问您的应用程序。

   >[!NOTE]
   >
   > 此 **客户端密码** 字段是必填字段还是可选字段取决于您的Azure Active Directory应用程序配置。 如果您的应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击 **[!UICONTROL Connect]**. 成功连接后， `Connection Successful` 出现消息。

1. 现在，选择 **[!UICONTROL OneDrive容器]** > **[OneDrive文件夹]**  以保存数据。

   >[!NOTE]
   >
   >* 默认情况下， `forms-ootb-storage-adaptive-forms-submission` 存在于OneDrive容器中。
   > * 创建文件夹为 `forms-ootb-storage-adaptive-forms-submission`，如果尚未出现，请单击 **创建文件夹**.

现在，您可以在自适应表单中将此OneDrive存储配置用于提交操作。

### 在自适应表单中使用OneDrive配置 {#use-onedrive-configuartion-in-af}

您可以在自适应表单中使用创建的OneDrive存储配置，将数据或生成的记录文档保存在OneDrive文件夹中。 执行以下步骤，在自适应表单中使用OneDrive存储配置，如下所示：
1. 创建 [自适应表单](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 选择相同的 [!UICONTROL 配置容器] 自适应表单，您已在该表单中创建了OneDrive存储。
   > * 如果否 [!UICONTROL 配置容器] 选择，然后全局 [!UICONTROL 存储配置] 文件夹出现在“提交操作”属性窗口中。

1. 选择 **提交操作** 作为 **[!UICONTROL 提交到OneDrive]**.
   ![OneDriveGIF](/help/forms/assets/onedrive-video.gif)
1. 选择 **[!UICONTROL 存储配置]**，以保存数据。
1. 单击 **[!UICONTROL 保存]** 以保存提交设置。

提交表单时，数据将保存在指定的Microsoft® OneDrive存储中。
要保存数据的文件夹结构为 `/folder_name/form_name/year/month/date/submission_id/data`.

## 提交到 Azure Blob Storage {#submit-to-azure-blob-storage}

此 **[!UICONTROL 提交到Azure Blob存储]**  提交操作可将自适应表单与Microsoft® Azure门户连接。 您可以将表单数据、文件、附件或记录文档提交到连接的Azure存储容器。 要对Azure Blob存储使用提交操作，请执行以下操作：

1. [创建Azure Blob存储容器](#create-a-azure-blob-storage-container-create-azure-configuration)：用于将AEM Forms连接到Azure Storage容器。
2. [在自适应表单中使用Azure存储配置](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：它将您的自适应表单连接到配置的Azure存储容器。

### 创建Azure Blob存储容器 {#create-azure-configuration}

要将AEM Forms连接到Azure Storage容器，请执行以下操作：
1. 转到您的 **AEM Forms Author** 实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Azure存储]**.
1. 一旦您选择 **[!UICONTROL Azure存储]**，您将被重定向到 **[!UICONTROL Azure存储浏览器]**.
1. 选择 **配置容器**. 该配置将存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。将显示“创建Azure存储配置”向导。

   ![Azure存储配置](/help/forms/assets/azure-storage-configuration.png)

1. 指定 **[!UICONTROL 标题]**， **[!UICONTROL Azure存储帐户]** 和 **[!UICONTROL Azure访问密钥]**.

   * 您可以检索 `Azure Storage Account` 名称和 `Azure Access key` 从Microsoft® Azure门户中的存储帐户。

1. 单击“**[!UICONTROL 保存]**”。

现在，您可以在自适应表单中将此Azure存储容器配置用于提交操作。

### 在自适应表单中使用Azure存储配置 {#use-azure-storage-configuartion-in-af}

您可以在自适应表单中使用创建的Azure存储容器配置，以将数据或生成的记录文档保存在Azure存储容器中。 执行以下步骤以在自适应表单中使用Azure存储容器配置，如下所示：
1. 创建 [自适应表单](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 选择相同的 [!UICONTROL 配置容器] 自适应表单，您已在该表单中创建了OneDrive存储。
   > * 如果否 [!UICONTROL 配置容器] 选择，然后全局 [!UICONTROL 存储配置] 文件夹出现在“提交操作”属性窗口中。

1. 选择 **提交操作** 作为 **[!UICONTROL 提交到Azure Blob存储]**.
   ![Azure Blob存储GIF](/help/forms/assets/azure-submit-video.gif)

1. 选择 **[!UICONTROL 存储配置]**，以保存数据。
1. 单击 **[!UICONTROL 保存]** 以保存提交设置。

提交表单时，数据将保存在指定的Azure存储容器配置中。
要保存数据的文件夹结构为 `/configuration_container/form_name/year/month/date/submission_id/data`.

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 使用同步或异步提交 {#use-synchronous-or-asynchronous-submission}

提交操作可以使用同步或异步提交。

**同步提交**：传统上，Web窗体配置为同步提交。 在同步提交中，当用户提交表单时，他们将被重定向到确认页面、感谢页面，或者如果提交失败，则被重定向到错误页面。 您可以选择 **[!UICONTROL 使用异步提交]** 用于将用户重定向到网页或在提交时显示消息的选项。

![配置提交操作](assets/thank-you-setting.png)

**异步提交**：单页应用程序等现代Web体验越来越受欢迎，这是因为在后台进行客户端 — 服务器交互时，网页保持静态。 现在，您可以通过以下方式为自适应Forms提供此体验 [配置异步提交](asynchronous-submissions-adaptive-forms.md).

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些JavaScript验证，以实施一些业务规则。 但在现代浏览器中，最终用户能够绕过这些验证，并使用各种技术（如Web浏览器DevTools控制台）手动提交内容。 此类技术对于自适应Forms也有效。 表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑并将无效数据提交到服务器。 无效数据将破坏表单作者已强制执行的业务规则。

通过服务器端重新验证功能，还可以在服务器上运行Adaptive Forms作者在设计Adaptive Form时提供的验证。 它可防止在表单验证方面可能出现的任何数据提交和业务规则违规受损。

### 要在服务器上验证什么？ {#what-to-validate-on-server-br}

在服务器上重新运行的自适应表单的所有开箱即用(OOTB)字段验证包括：

* 必需
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用 **[!UICONTROL 在服务器上重新验证]** 在侧栏中的自适应表单容器下，启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将再次执行验证。 如果验证在服务器端失败，则提交事务将停止。 最终用户将再次看到原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
>
>服务器端验证验证表单模型。 建议为验证创建单独的客户端库，并且不要在同一客户端库中将其与HTML样式和DOM操作等其他内容混合。

### 在验证表达式中支持自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时候，如果有 **复杂验证规则**，精确验证脚本驻留在自定义函数中，作者从字段验证表达式中调用这些自定义函数。 要使此自定义函数库在执行服务器端验证时已知且可用，表单作者可以在下配置AEM客户端库的名称 **[!UICONTROL 基本]** “自适应表单容器”属性的选项卡，如下所示。

![在验证表达式中支持自定义函数](assets/clientlib-cat.png)

在验证表达式中支持自定义函数

作者可以按自适应表单配置customJavaScript库。 在库中，仅保留依赖于jquery和underscore.js第三方库的可重用函数。

## 提交操作的错误处理 {#error-handling-on-submit-action}

作为AEM安全和强化指南的一部分，请配置自定义错误页面，如400.jsp、404.jsp和500.jsp。 在提交表单时出现400、404或500错误时，将调用这些处理程序。 在Publish节点上触发这些错误代码时，也会调用处理程序。 您还可以为其他HTTP错误代码创建JSP页。

当您将表单数据模型或基于XML或JSON数据投诉模式的自适应表单预填充到数据不包含的架构时 `<afData>`， `<afBoundData>`、和 `</afUnboundData>` 标签时，自适应表单中无界字段的数据将丢失。 架构可以是XML架构、JSON架构或表单数据模型。 未限定的字段是自适应表单字段，不带 `bindref` 属性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
