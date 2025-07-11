---
title: AEM Forms as a Cloud Service通信API
description: 在云中使用AEM Forms Communication API生成、操作和保护文档
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 8803896bf728524833a0dde004ddaa2e8b6bb103
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 28%

---


# AEM Forms as a Cloud Service通信API {#communications-apis-overview}

> **版本可用性**
>
> * **AEM 6.5**： [AEM文档服务概述](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html?lang=zh-Hans)
> * **AEM as a Cloud Service**：本文

## 简介

AEM Forms as a Cloud Service中的通信API可帮助您创建品牌批准、个性化和标准化的文档，以满足您的业务需求。 这些功能强大的API使您能够以编程方式生成、操作和保护文档，无论是在按需还是高容量批处理中。

### 主要优点

* **简化文档生成** — 通过将模板与客户数据合并来创建个性化文档
* **强大的文档操作** — 以编程方式组合、重新排列和验证PDF文档
* **灵活的部署选项** — 使用按需API满足低延迟需求，或使用批量API进行高吞吐量操作
* **增强的安全性** — 应用数字签名、认证和加密来保护敏感文档
* **云原生架构** — 利用可扩展的安全云基础架构，无维护开销

## API功能概述

Communications API提供了一组全面的文档处理功能，可划分为以下功能区域：

| 文档生成 | 文档操作 | 文档提取 | 文档转换 | 记录Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| 通过将模板与各种格式(包括PDF和打印格式)的数据合并来生成个性化文档。 | 以编程方式组合、重新排列和验证PDF文档以创建新文档包。 | 从PDF文档中提取属性、元数据和内容以供进一步处理。 | 在多种格式之间转换文档，包括PDF/A合规性验证以满足存档需求。 | 应用数字签名、认证和加密来保护文档。 |

[API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)提供了有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API参考文档也以.yaml格式提供。 您可以下载.yaml并将其上传到Postman以检查API的功能。

## 文档生成

通信文档生成API帮助将模板(XFA或PDF)与客户数据(XML)相结合，以生成PDF、AFP（高级功能演示）和打印格式（如PS、PCL、DPL、IPL和ZPL格式）的文档。 这些API使用带有[XML数据](communications-known-issues-limitations.md#form-data)的PDF和XFA模板来根据需要生成单个文档，或使用批处理作业生成多个文档。

通常，您使用 [Designer](use-forms-designer.md) 创建模板，并使用通信 API 将数据与模板合并。您的应用程序可以将输出文档发送到网络打印机、本地打印机或存储系统以进行存档。典型的现成和自定义工作流如下所示：

![通信文档生成工作流](assets/communicaions-workflow.png)

根据用例，您还可以将这些文档设为通过您的网站或存储服务器下载。

### 关键文档生成功能

#### 创建PDF/AFP电子格式的文档

您可以使用文档生成API创建基于表单设计和XML表单数据的PDF或AFP格式文档。 输出是非交互式文档。 也就是说，用户无法输入或修改表单数据。一个基本的工作流程是将XML表单数据与表单设计合并，以创建文档。 下图说明如何合并表单设计和 XML 表单数据以生成 PDF 文档。

![创建PDF文档](assets/outPutPDF_popup.png)
图：创建文档的典型工作流

下表显示了AFP格式与PDF格式之间的差异：

| **功能** | **AFP（高级函数演示）** | **PDF（可移植文档格式）** |
|---------------------------|--------------------------------------------------------------------|-------------------------------------------------------------|
| **用途** | 大量印刷和制作交易文件 | 通用文档共享和查看 |
| **用例** | 银行对帐单、票据、发票、保险单据 | 电子书、表格、报告、简历、手册 |
| **平台来源** | 由IBM开发 | 由 Adobe 开发 |
| **结构** | 具有结构化字段和对象的面向页面的格式 | 面向页面，但布局固定 |
| **可编辑性** | 专为生产打印而设计，很少进行编辑 | 可使用各种工具进行编辑，例如Adobe Acrobat |
| **文件大小和性能** | 针对高速打印环境的性能而优化 | 对于批量输出，可能会更大，优化程度更低 |
| **交互性** | 最小到无；静态页面 | 支持交互式元素，如表单、链接、JavaScript |
| **输出控件** | 对打印机布局的细粒度控制 | 针对屏幕和打印优化的可视布局 |
| **字体和图形** | 使用字体和资源引用；需要渲染器来解释 | 将字体和图像直接嵌入到文件中 |

文档生成API返回生成的PDF文档或AFP文档。 您还可以选择将生成的PDF上传到Azure Blob Storage。

<span class="preview">使用文档生成API将生成的PDF上传到Azure Blob Storage功能位于[早期采用者计划](/help/forms/early-access-ea-features.md)下。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

#### 创建 PostScript (PS)、打印机指令语言 (PCL)、Zebra 打印语言 (ZPL) 文档 {#create-PS-PCL-ZPL-documents}

您可以使用文档生成API创建基于XDP表单设计或PDF文档的PostScript (PS)、打印机命令语言(PCL)和斑马打印语言(ZPL)文档。 这些 API 有助于将表单设计与表单数据合并以生成文档。您可以将文档保存到文件，并开发一个自定义流程来将它发送到打印机。

#### 处理批量数据可创建多个文档 {#processing-batch-data-to-create-multiple-documents}

您可以使用文档生成 API 为 XML 批处理数据源中的每条记录创建单独的文档。您可以批量和在异步架构下生成文档。您可以配置各种用于转换的参数，然后开始批处理。

![创建 PDF 文档](assets/ou_OutputBatchMany_popup.png)

## 文档操作

通信文档操作（文档转换）API有助于组合、重新排列PDF文档。 通常，您创建一个 DDX 并将它提交给文档操作 API 来汇编或重新排列文档。[DDX 文档](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)提供了有关如何使用源文档生成一组所需文档的说明。DDX参考文档提供了有关所有受支持操作的详细信息。

### 关键文档操作功能

#### 汇编 PDF 文档

您可以使用文档操作 API 将两个或更多 PDF 或 XDP 文档汇编成一个 PDF 文档或 PDF 文档组合。以下是组合PDF文档的一些方式：

* 汇编一个简单的 PDF 文档
* 创建 PDF 文档组合
* 汇编加密的文档
* 使用 Bates 编号汇编文档
* 合并和汇编文档

![将多个 PDF 文档汇编成一个简单 PDF 文档](assets/as_document_assembly.png)
图：将多个 PDF 文档汇编成一个简单 PDF 文档

#### 拆分 PDF 文档

您可以使用文档操作 API 来拆分 PDF 文档。API 可以从源文档中提取页面或根据书签拆分源文档。通常，如果 PDF 文档最初是从多个单独文档（例如对帐单集合）创建的，则此任务很有用。

* 从源文档中提取页面
* 根据书签拆分源文档

![根据书签将一个源文档拆分成多个文档](assets/as_intro_pdfsfrombookmarks.png)
图：根据书签将一个源文档拆分成多个文档

>[!NOTE]
>
> AEM Forms提供了多种内置字体，可与PDF文件无缝集成。 要查看支持的字体列表，[单击此处](/help/forms/supported-out-of-the-box-fonts.md)。

## 文档提取

<span class="preview">文档提取功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

文档提取服务使您能够获取PDF文档的属性，如使用权限、PDF属性和元数据。 文档提取功能包括：

* 获取PDF文档的属性，例如PDF是否包含附件、注释、其Acrobat版本等。
* 提取在PDF文档中启用的使用权限，用户将启用或禁用的使用权限检索到PDF文档以实现Adobe Acrobat Reader的可扩展性。
* 获取存在于PDF文档中的元数据信息，元数据是有关该文档的信息（与文档内容不同，例如文本和图形）。 Adobe可扩展元数据平台(XMP)是用于处理文档元数据的标准。 XMP实用工具服务可以从XMP文档中检索PDF元数据，并将XMP元数据导出到PDF文档中。

[API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)提供了有关API提供的所有参数、身份验证方法和服务的详细信息。 API参考文档也以.yaml格式提供。 您可以下载.yaml并将其上传到Postman以检查API的功能。

## 文档转换

### 转换为符合 PDF/A 标准的文档并进行验证

Communications文档转换API有助于将PDF文档转换为PDF/A。您可以使用这些API将PDF文档转换为符合PDF/A的文档，还可以确定PDF文档是否符合PDF/A标准。 PDF/A是一种用于长期保存文档内容的存档格式。 字体将嵌入到文档中，并且文件是未压缩的。因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/A文档不包含音频和视频内容。 支持的PDF/A合规性标准包括PDF/A-1a、1b、2a、2b、3a和3b。

### 将PDF转换为XDP {#convert-pdf-to-xdp}

<span class="preview">将PDF转换为XDP功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

将PDF文档转换为XDP文件。 对于要成功转换为XDP文件的PDF文档，PDF文档必须在词典中包含XFA流。

## 记录Assurance {#doc-assurance}

DocAssurance服务包括签名和加密API：

### 签名API

利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。<!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. -->安全功能应用于文档本身，在文档的整个生命周期内保持安全和受控制。 在防火墙之外，当文档离线下载以及提交回组织时，文档将保持安全。 您可以使用签名API完成以下任务：

* 向PDF文档添加可见签名字段。
* 向PDF文档添加不可见的签名字段。
* 在PDF文档中签署指定的签名字段。
* 认证PDF文档
* 从PDF文档的指定签名字段中移除签名
* 从PDF文档中删除指定的签名字段

<span class="preview">从早期采用程序下提供的PDF文档中，从指定的签名字段中移除签名并删除指定的签名字段。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

### 加密API

加密API允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问权限。 如果PDF文档使用密码加密，用户必须先指定打开密码，然后才能在Adobe Reader或Adobe Acrobat中查看文档。<!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

您可以使用加密API完成以下任务：

* 使用密码加密PDF文档。
* 从PDF文档中删除基于密码的加密。
* 检索应用于PDF文档的安全类型。
* 返回应用于PDF文档的安全类型。

签名API和加密API都是[同步API](#types-of-communications-apis-types)。

### 文档实用工具 {#doc-utility}

带同步API的文档实用程序可帮助您在PDF和XDP文件格式之间转换文档。 将使用权限应用到文档，并从文档中提取启用的使用权限。 查询有关PDF文档的信息。 <!-- determines whether a PDF document contains comments or attachments and more, and use document transformation services for XMP utilities-->使用权限API的详细信息如下：

#### 使用权限API(Reader扩展)

<span class="preview">使用权限(Reader扩展)功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

使用权限功能通过使用其他使用权限来扩展Adobe Reader的功能，您的组织可以轻松共享交互式PDF文档。 该服务可与Adobe Reader 7.0或更高版本配合使用，并向PDF文档添加了使用权限。 此操作激活在使用Adobe Reader打开PDF文档时通常不可用的功能，例如向文档添加注释、填写表单和保存文档。

当PDF文档添加了相应的使用权限后，收件人可以在Adobe Reader中执行以下操作：

* 在线或离线完成PDF文档和表单，允许收件人在本地保存副本以保存其记录，并且仍保持添加的信息完整。
* 将PDF文档保存到本地硬盘，以保留原始文档以及任何其他注释、数据或附件。
* 将文件和媒体剪辑附加到PDF文档。
* 通过使用行业标准公钥基础设施(PKI)技术应用数字签名对PDF文档进行签名、认证和身份验证。
* 以电子方式提交已完成或添加注释的PDF文档。
* 使用PDF文档和表单作为内部数据库和Web服务的直观开发前端。
* 与其他人共享PDF文档，以便审阅人可以使用直观的标记工具添加注释。 这些工具包括电子便笺、印章、高亮和文本删除线。 Acrobat中提供了相同的函数。
* 支持条码Forms解码。

在Adobe Reader中打开启用了权限的PDF文档时，会自动激活这些特殊使用权限功能。 当用户使用完启用了权限的文档时，这些功能在Adobe Reader中再次被禁用。 它们会保持禁用状态，直到用户收到另一个启用了权限的PDF文档。

#### 启用或禁用使用权限

用于扩展PDF Reader服务的各种使用权限功能包括：

* **条形码解码**：解码PDF文档中的条形码。

* **备注**：脱机评论PDF文档。

* **联机评论**：联机评论PDF文档。

* **数字签名**：向PDF文档添加数字签名。

* **动态表单字段**：向PDF文档添加表单字段。

* **动态表单页面**：将表单页面添加到PDF文档。

* **嵌入的文件**：在PDF文档中嵌入文件。

* **表单数据导入**：将表单数据导入到PDF文档。

* **表单数据导出**：将表单数据导入到PDF文档。

* **表单填写**：在PDF文档中填写表单字段。

* **联机Forms**：从PDF文档访问Web服务或数据库。

* **独立提交**：从PDF文档离线提交表单数据。

#### 其他功能

* **消息**：在打开应用了一个或多个使用权限的PDF文档时，Adobe Acrobat Reader中显示的消息。
* **解锁密码**：打开加密的PDF文档所需的密码。 通常，这是文档打开密码，但如果PDF文档另外受权限密码保护，则可以使用任一密码来打开文档。

## 通信 API 的类型 {#types}

通信功能提供用于按需和批量文档生成的 HTTP API：

* **[同步 API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;适用于按需、低延迟、单一记录文档生成场景。这些 API 更适用于基于用户操作的用例。例如，在用户填写完表单后生成文档。

* **[批处理 API（异步 API）](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;适用于计划的、高吞吐量和多文档生成场景。这些 API 会批量生成文档。例如，每月生成电话帐单、信用卡对帐单和福利对帐单。

## 入门培训

通信功能作为面向 Forms as a Cloud Service 用户的独立和附加模块提供。您可以联系Adobe销售团队或Adobe代表以请求获取访问权限。 Adobe 可为您的组织开启访问渠道，并为您指定为组织中管理员的人员提供所需的权限。管理员可以向贵组织的Forms as a Cloud Service开发人员（用户）授予权限以使用这些API。

新用户引导后，要为Forms as a Cloud Service环境启用通信功能，请执行以下操作：

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

## 其他资源 {#see-also}

* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service架构](/help/forms/aem-forms-cloud-service-architecture.md)
* [API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [早期采用者计划功能](/help/forms/early-access-ea-features.md)
