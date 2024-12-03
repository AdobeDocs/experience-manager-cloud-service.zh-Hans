---
title: 什么是Formsas a Cloud Service通信API？
description: 使用通信API签名、认证或保护文档，自动化PDF生成过程，以及将PDF文档转换为另一种格式。
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs.
feature: Adaptive Forms, APIs & Integrations
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 13c1febf55c9b15eab49d356fc1ba3f3d91ad055
workflow-type: tm+mt
source-wordcount: '2374'
ht-degree: 41%

---

# AEM Formsas a Cloud Service通信API {#frequently-asked-questions}

![主页图像](assets/cloud-communication-apis-hero-image.jpeg)


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service | 本文 |

通信功能可帮助您创建品牌批准的、个性化的和标准化的文档，例如商业信函、对帐单、理赔处理函、收益通知函、月度帐单或欢迎套件。

该功能提供 API 来生成和操作文档。您可以按需生成或操作文档，也可以创建批处理作业来按定义的时间间隔生成多个文档。通信 API 提供：

* 按需简化和批量文档生成功能。

* 按需组合、重新排列和验证 PDF 文档的能力。

* 用于更轻松地与外部系统集成的 HTTP API。包括用于按需（低延迟）和批处理操作（高吞吐量操作）的单独 API。

* 对数据的安全访问。通信 API 仅连接到客户指定的数据存储库并从中访问数据，从而使通信变得高度安全。

[API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)提供了有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API参考文档也以.yaml格式提供。 您可以下载.yaml并将其上传到Postman以检查API的功能。


<!-- 
![A sample credit card statement](assets/statement.png)
A credit card statement can be created using Communications APIs. This sample statement uses same template but separate data for each customer depending on their usage of credit card.

-->

## 文档生成

通信文档生成 API 有助于将模板（XFA 或 PDF）与客户数据（XML）相结合，生成 PDF 和打印格式（如 PS、PCL、DPL、IPL 和 ZPL 格式）的文档。这些 API 将 PDF 和 XFA 模板与 [XML 数据](communications-known-issues-limitations.md#form-data)结合使用，按需生成单个文档或使用批处理作业生成多个文档。

通常，您使用 [Designer](use-forms-designer.md) 创建模板，并使用通信 API 将数据与模板合并。您的应用程序可以将输出文档发送到网络打印机、本地打印机或存储系统以进行存档。典型的现成和自定义工作流如下所示：

![通信文档生成工作流](assets/communicaions-workflow.png)

根据用例，您还可以将这些文档设为通过您的网站或存储服务器下载。

文档生成 API 的一些示例包括：

### 创建 PDF 文档 {#create-pdf-documents}

您可以使用文档生成 API 创建基于表单设计和 XML 表单数据的 PDF 文档。输出是非交互式 PDF 文档。也就是说，用户无法输入或修改表单数据。基本工作流是将 XML 表单数据与表单设计合并来创建 PDF 文档。下图说明如何合并表单设计和 XML 表单数据以生成 PDF 文档。

![创建 PDF 文档](assets/outPutPDF_popup.png)
图：典型的 PDF 文档创建工作流

### 创建 PostScript (PS)、打印机指令语言 (PCL)、Zebra 打印语言 (ZPL) 文档 {#create-PS-PCL-ZPL-documents}

您可以使用文档生成API创建基于XDP表单设计或PDF文档的PostScript (PS)、打印机命令语言(PCL)和斑马打印语言(ZPL)文档。 这些 API 有助于将表单设计与表单数据合并以生成文档。您可以将文档保存到文件，并开发一个自定义流程来将它发送到打印机。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 处理批量数据可创建多个文档 {#processing-batch-data-to-create-multiple-documents}

您可以使用文档生成 API 为 XML 批处理数据源中的每条记录创建单独的文档。您可以批量和在异步架构下生成文档。您可以配置各种用于转换的参数，然后开始批处理。

![创建 PDF 文档](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## 文档操作

通信文档操作（文档转换）API有助于组合、重新排列PDF文档。 通常，您创建一个 DDX 并将它提交给文档操作 API 来汇编或重新排列文档。[DDX 文档](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)提供了有关如何使用源文档生成一组所需文档的说明。DDX 引用文档提供了有关所有受支持操作的详细信息。文档操作的一些示例包括：

### 汇编 PDF 文档

您可以使用文档操作 API 将两个或更多 PDF 或 XDP 文档汇编成一个 PDF 文档或 PDF 文档组合。以下是组合PDF文档的一些方法：

* 汇编一个简单的 PDF 文档
* 创建 PDF 文档组合
* 汇编加密的文档
* 使用 Bates 编号汇编文档
* 合并和汇编文档

![将多个 PDF 文档汇编成一个简单 PDF 文档](assets/as_document_assembly.png)
图：将多个 PDF 文档汇编成一个简单 PDF 文档

### 拆分 PDF 文档

您可以使用文档操作 API 来拆分 PDF 文档。API 可以从源文档中提取页面或根据书签拆分源文档。通常，如果 PDF 文档最初是从多个单独文档（例如对帐单集合）创建的，则此任务很有用。

* 从源文档中提取页面
* 根据书签拆分源文档

![根据书签将一个源文档拆分成多个文档](assets/as_intro_pdfsfrombookmarks.png)
图：根据书签将一个源文档拆分成多个文档

>[!NOTE]
>
> AEM Forms提供了多种内置字体，可与PDF文件无缝集成。 要查看支持的字体列表，[单击此处](/help/forms/supported-out-of-the-box-fonts.md)。

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments.

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## 文档提取

<span class="preview">文档提取功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

文档提取服务允许您获取PDF文档的属性，如使用权限、PDF属性和元数据。 文档提取功能包括：

* 获取PDF文档的属性，例如，如果PDF具有附件、注释、其Acrobat版本等。
* 提取在PDF文档中启用的使用权限，用户将启用或禁用的使用权限检索到PDF文档，以实现Adobe Acrobat Reader的可扩展性。
* 获取PDF文档中存在的元数据信息，元数据是有关文档的信息（与文档内容不同，例如文本和图形）。 Adobe可扩展元数据平台(XMP)是处理文档元数据的标准。 XMP Utilities服务可以从PDF文档中检索XMP元数据，并将XMP元数据导出到PDF文档中。

[API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)提供了有关API提供的所有参数、身份验证方法和服务的详细信息。 API参考文档也以.yaml格式提供。 您可以下载.yaml并将其上传到Postman以检查API的功能。

<!--

<span class="preview"> The XMP Utilities Service capability is under Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>

### XMP Utilities {#XMP-utilities}

<span class="preview"> The XMP Utilities Service capability is under Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>

PDF documents contain metadata, which is information about the document (as distinguished from the contents of the document, such as text and graphics). The Adobe Extensible Metadata Platform (XMP) is a standard for handling document metadata. The XMP Utilities service can retrieve and save XMP metadata from PDF documents and import XMP metadata into PDF documents.

-->

## 文档转换

### 转换为符合 PDF/A 标准的文档并进行验证

通信文档转换API有助于将PDF文档转换为PDF/A。您可以使用这些API将PDF文档转换为符合PDF/A标准的文档，还可以确定PDF文档是否符合PDF/A标准。 PDF/A是一种用于长期保存文档内容的存档格式。 字体将嵌入到文档中，并且文件是未压缩的。因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/文档不包含音频和视频内容。 支持的PDF/A合规性标准包括PDF/A-1a、1b、2a、2b、3a和3b。

### 将PDF转换为XDP {#convert-pdf-to-xdp}

<span class="preview"> ConvertPDF到XDP的功能在早期采用者计划下。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

将PDF文档转换为XDP文件。 若要将PDF文档成功转换为XDP文件，PDF文档必须在词典中包含XFA流。

## 记录Assurance {#doc-assurance}

DocAssurance服务包括签名和加密API：

### 签名API

利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。<!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. -->安全功能应用于文档本身，在文档的整个生命周期内保持安全和受控制。 在防火墙之外，当文档离线下载以及提交回组织时，文档将保持安全。 您可以使用签名API完成以下任务：

* 向PDF文档添加可见签名字段。
* 向PDF文档添加不可见的签名字段。
* 在PDF文档中签署指定的签名字段。
* 认证PDF文档
* 从PDF文档中的指定签名字段中移除签名
* 从PDF文档中删除指定的签名字段

<span class="preview">从早期采用程序下可用的PDF文档中移除指定签名字段的签名并删除指定签名字段。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>


<!--

### Remove Signature APIs

The Remove Signature API helps to remove an existing digital signatures from a PDF document. This API is useful when you need to update or revise a signed document and reapply signatures. It maintains document integrity while effectively clearing signatures from specific pages or the entire file. Use cases include re-signing documents with updated data or clearing previous approvals for revised versions.


### Remove Signature Field APIs

The Remove Signature Field API is tailored for removing signature fields from a PDF document. This is ideal when you need to delete empty or unused signature fields to streamline document presentation. It enables users to eliminate signature fields without impacting other form fields or the document structure, making it easier to create cleaner, final versions of a document that no longer require signatures.

-->

### 加密API

加密API允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问权限。 如果使用密码对PDF文档进行加密，则必须先指定打开密码，然后才能在Adobe Reader或Adobe Acrobat中查看文档。<!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

您可以使用加密API完成以下任务：

* 使用密码加密PDF文档。
* 从PDF文档中删除基于密码的加密。
* 检索应用于PDF文档的安全类型。
* 返回应用于PDF文档的安全类型。

签名API和加密API都是[同步API](#types-of-communications-apis-types)。


### 文档实用工具 {#doc-utility}

带同步API的文档实用程序可帮助您在PDF和XDP文件格式之间转换文档。 将使用权限应用到文档，并从文档中提取启用的使用权限。 查询有关PDF单据的信息。 <!-- determines whether a PDF document contains comments or attachments and more, and use document transformation services for XMP utilities-->使用权限API的详细信息如下：


#### 使用权限API(Reader扩展)

<span class="preview">使用权限(Reader扩展)功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

使用权限功能通过扩展具有其他使用权限的Adobe Reader的功能，使您的组织可以轻松共享交互式PDF文档。 该服务可与Adobe Reader 7.0或更高版本配合使用，并向PDF文档添加了使用权限。 此操作激活在使用Adobe Reader打开PDF文档时通常不可用的功能，例如向文档添加注释、填写表单和保存文档。

当PDF文档添加了相应的使用权限后，收件人可以在Adobe Reader中执行以下操作：

* 在线或离线完成PDF文档和表单，使收件人能够在本地保存副本以保存其记录，同时仍保持添加的信息完好无损。
* 将PDF文档保存到本地硬盘，以保留原始文档以及任何其他注释、数据或附件。
* 将文件和媒体剪辑附加到PDF文档。
* 通过使用行业标准公钥基础设施(PKI)技术应用数字签名对PDF文档进行签名、认证和身份验证。
* 以电子方式提交已完成或添加注释的PDF文档。
* 使用PDF文档和表单作为内部数据库和Web服务的直观开发前端。
* 与其他人共享PDF文档，以便审阅人可以使用直观的标记工具添加注释。 这些工具包括电子便笺、印章、高亮和文本删除线。 Acrobat中提供了相同的函数。
* 支持条码Forms解码。

在Adobe Reader中打开启用了权限的PDF文档时，会自动激活这些特殊使用权限功能。 当用户使用完启用了权限的文档时，这些功能在Adobe Reader中再次被禁用。 它们保持禁用状态，直到用户收到另一个启用了权限的PDF文档。

#### 启用或禁用使用权限

用于扩展PDFReader服务的各种使用权限功能包括：

* **条形码解码**：解码PDF文档中的条形码。

* **备注**：脱机评论PDF文档。

* **联机评论**：联机评论PDF文档。

* **数字签名**：向PDF文档添加数字签名。

* **动态表单字段**：向PDF文档添加表单字段。

* **动态表单页**：将表单页添加到PDF文档。

* **嵌入的文件**：在PDF文档中嵌入文件。

* **表单数据导入**：将表单数据导入到PDF文档。

* **表单数据导出**：将表单数据导入到PDF文档。

* **表单填写**：在PDF文档中填写表单字段。

* **联机Forms**：从PDF文档访问Web服务或数据库。

* **独立提交**：从PDF文档离线提交表单数据。


#### 其他功能

* **消息**：在打开应用了一个或多个使用权限的PDF文档时，Adobe Acrobat Reader中显示的消息。
* **解锁密码**：打开加密的PDF文档所需的密码。 通常，这是文档打开密码，但如果PDF文档受权限密码的额外保护，则可以使用任一密码来打开文档。

## 通信 API 的类型 {#types}

通信功能提供用于按需和批量文档生成的 HTTP API：

* **[同步 API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;适用于按需、低延迟、单一记录文档生成场景。这些 API 更适用于基于用户操作的用例。例如，在用户填写完表单后生成文档。

* **[批处理 API（异步 API）](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;适用于计划的、高吞吐量和多文档生成场景。这些 API 会批量生成文档。例如，每月生成电话帐单、信用卡对帐单和福利对帐单。

## 入门培训

通信功能作为面向 Forms as a Cloud Service 用户的独立和附加模块提供。您可以联系Adobe销售团队或您的Adobe代表以请求获取访问权限。 Adobe 可为您的组织开启访问渠道，并为您指定为组织中管理员的人员提供所需的权限。管理员可以向贵组织的Formsas a Cloud Service开发人员（用户）授予权限以使用这些API。

新用户引导后，要为Formsas a Cloud Service环境启用通信功能，请执行以下操作：

1. 登录 Cloud Manager，并打开您的 AEM Forms as a Cloud Service 实例。

1. 打开“编辑程序”选项，转到“解决方案和加载项”选项卡，然后选择&#x200B;**[!UICONTROL Forms - 通信]**&#x200B;选项。

   ![通信](assets/communications.png)

   如果您已启用 **[!UICONTROL Forms - 数字登记]**&#x200B;选项，则选择 **[!UICONTROL Forms - 通信加载项]**&#x200B;选项。

   ![加载项](assets/add-on.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。

1. 运行构建管道。成功运行构建管道后，将为您的环境启用通信 API。

>[!NOTE]
>
> 要启用和配置文档操作API，请将以下规则添加到[Dispatcher配置](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example, ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## 另请参阅 {#see-also}

* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [自适应Forms的AEM Formsas a Cloud Service架构和通信API](/help/forms/aem-forms-cloud-service-architecture.md)
