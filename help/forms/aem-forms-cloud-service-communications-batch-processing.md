---
title: 轻松批量创建PDF — 掌握批处理技术 — 生成数百万份PDF文档的自助指南！
description: 如何创建以品牌为导向的个性化通信？
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 2%

---

# AEM Formsas a Cloud Service通信批量处理

通信允许您创建、收集和提供面向品牌的个性化通信，如业务往来函、文档、报表、索赔处理函、福利通知、每月账单和欢迎资料包。 您可以使用Communications API将模板(XFA或PDF)与客户数据相结合，生成PDF、PS、PCL、DPL、IPL和ZPL格式的文档。

通信提供API用于按需生成和计划生成文档。 您可以按需使用同步API，也可以使用批处理API （异步API）生成计划的文档：

* 同步API适用于按需、低延迟和单记录文档生成用例。 这些 API 更适用于基于用户操作的用例。例如，在用户填写表单后生成文档。

* 批处理API（异步API）适用于计划的高吞吐量多文档生成用例。 这些 API 会批量生成文档。例如，每月生成的电话帐单、信用卡对帐单和收益对帐单。

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## 批处理操作 {#batch-operations}

批处理操作是在计划时间间隔内为一组记录生成多个类型相似的文档的过程。 批处理操作包括两部分：配置（定义）和执行。

* **配置（定义）**：批量配置存储有关要为生成的文档设置的各种资源和属性的信息。 例如，它提供了有关XDP或PDF模板和要使用的客户数据的位置的详细信息，并为输出文档指定各种属性。

* **执行**：要启动批处理操作，请将批处理配置名称传递到批处理执行API。

### 批处理操作的组件 {#components-of-a-batch-operations}

**云配置**：Experience Manger云配置可帮助您将Experience Manager实例连接到客户拥有的Microsoft Azure Storage。 它可让您为客户拥有的Microsoft Azure帐户指定凭据以连接到该帐户。

**批量数据存储配置(USC)**：批量数据配置可帮助您为批处理API配置特定的Blob存储实例。 它可让您在客户拥有的Microsoft Azure Blob Storage中指定输入和输出位置。

**批处理API**：可让您创建批处理配置并根据这些配置执行批处理运行，以将PDF或XDP模板与数据合并并生成PDF、PS、PCL、DPL、IPL和ZPL格式的输出。 通信提供了批处理API，用于配置管理和批量执行。

![data-merge-table](assets/communications-batch-structure.png)

**存储**：通信API使用客户拥有的Microsoft Azure云存储来获取客户记录并存储生成的文档。 您可以在Experience Manager Cloud Service配置中配置Microsoft Azure Storage。

**应用程序**：使用批处理API生成和使用文档的自定义应用程序。

## 使用批处理操作生成多个文档 {#generate-multiple-documents-using-batch-operations}

您可以使用批处理操作按计划间隔生成多个文档。

>[!VIDEO](https://video.tv.adobe.com/v/338349)

您可以观看视频或执行以下说明，了解如何使用批处理操作生成文档。 视频中使用的API参考文档以.yaml格式提供。 您可以下载 [批处理API](assets/batch-api.yaml) 将其上载到Postman以检查API的功能并观看视频。

### 先决条件 {#pre-requisites}

要使用批处理API，需要满足以下条件：

* [Microsoft Azure Storage帐户](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* XDPPDF模板
* [要与模板合并的数据](#form-data)
* 具有Experience Manager管理员权限的用户

### 设置环境 {#setup-your-environment}

使用批处理操作之前：

* 将客户数据（XML文件）上传到Microsoft Azure Blob Storage
* 创建云配置
* 创建批量数据存储配置
* 将模板和其他资源上传到Experience Manager FormsCloud Service实例

### 将客户数据（XML文件）上传到Azure存储 {#upload-customer-data-to-Azure-Storage}

在您的Microsoft Azure Storage上，创建 [容器](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) 和 [上传客户数据(XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) 到 [文件夹](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) 在容器内。
>[!NOTE]
>
>您可以将Microsoft Azure Storage配置为自动清理输入文件夹，或按计划时间间隔将输出文件夹的内容移动到其他位置。 但是，请确保在引用文件夹的批处理操作仍在运行时不清理文件夹。

### 创建云配置 {#create-a-cloud-configuration}

云配置可将您的Experience Manager实例连接到Microsoft Azure Storage。 要创建云配置，请执行以下操作：

1. 转到“工具”>“Cloud Service”>“Azure存储”
1. 打开文件夹以托管配置，然后单击“创建”。 您可以使用全局文件夹或创建文件夹。
1. 指定要连接到服务的配置和凭据的名称。 您可以 [从Microsoft Azure Storage门户检索这些凭据](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. 单击创建。

您的Experience Manager实例现在可以连接到Microsoft Azure Storage，并在需要时使用它来存储和读取内容。

### 创建批量数据存储配置 {#create-batch-data-store-configuration}

批量数据配置可帮助您配置用于输入和输出的容器和文件夹。 将客户记录保存在源文件夹中，生成的文档则保存在目标文件夹中。

要创建配置，请执行以下操作：

1. 转到“工具” > “Forms” > “统一存储连接器” 。
1. 打开文件夹以托管配置，然后单击“创建”。 您可以使用全局文件夹或创建文件夹。
1. 指定配置的标题和名称。 在存储中，选择Microsoft Azure Storage。
1. 在存储配置路径中，浏览并选择云配置，该配置包含客户拥有的Azure存储帐户的凭据。
1. 在源文件夹中，指定Azure存储容器和包含记录的文件夹的名称。
1. 在目标文件夹中，指定Azure存储容器的路径和用于存储生成的文档的文件夹。
1. 单击创建。

您的Experience Manager实例现在已连接到Microsoft Azure Storage，并已配置为检索数据并将其发送到Microsoft Azure Storage上的特定位置。

### 将模板和其他资源上传到Experience Manager实例 {#upload-templates-and-other-assets-to-your-AEM-instance}

组织通常有多个模板。 例如，信用卡对帐单、福利对帐单和报销申请都使用一个模板。 将所有此类XDP和PDF模板上传到您的Experience Manager实例。 要上传模板，请执行以下操作：

1. 打开您的Experience Manager实例。
1. 转到Forms > Forms和文档
1. 单击“创建”>“文件夹”，然后创建一个文件夹。 打开文件夹。
1. 单击“创建”>“文件上载”并上载模板。

## 使用批处理API生成文档 {#use-batch-API-to-generate-documents}

要使用批处理API，请创建批处理配置并根据该配置执行运行。 API文档提供了有关用于创建和运行批处理的API、相应参数和可能错误的信息。 您可以下载 [API定义文件](assets/batch-api.yaml) 文件并将其上传到 [Postman](https://go.postman.co/home) 或类似的软件测试API以创建并运行批处理操作。

### 创建批次 {#create-a-batch}

要创建批处理，请使用 `POST /config` API。 在HTTP请求正文中包含以下必需属性：

* **配置名称**：指定批次的唯一名称。 例如，`wknd-job`
* **dataSourceConfigUri**：指定批量数据存储配置的位置。 它可以是配置的相对路径或绝对路径。 例如：`/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputType**：指定输出格式：PDF和打印。 如果使用PRINT输出类型，请输入 `printedOutputOptionsList` 属性，至少指定一个打印选项。 打印选项由其渲染类型标识，因此目前不允许使用同一渲染类型的多个打印选项。 支持的格式包括PS、PCL、DPL、IPL和ZPL。

* **模板**：指定模板的绝对或相对路径。 例如，`crx:///content/dam/formsanddocuments/wknd/statements.xdp`

如果指定相对路径，则还应提供内容根。 有关内容根的详细信息，请参阅API文档。

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

您可以使用 `GET /config /[configName]` 查看批次配置的详细信息。

### 运行批次 {#run-a-batch}

要运行（执行）批处理，请使用 `POST /config /[configName]/execution`. 例如，要运行名为wknd-demo的批次，请使用/config/wknd-demo/execution。 服务器接受请求时返回HTTP响应代码202。 除了在服务器上运行的批处理作业的HTTP响应标头中的唯一代码(execution-identifier)之外，API不返回任何有效负载。 您可以使用执行标识符检索批次的状态。

>[!NOTE]
>
>在批处理运行时，请勿对相应的源文件夹和目标文件夹、数据源配置以及Microsoft Azure云配置进行任何更改。

### 检查批次的状态 {#status-of-a-batch}

要检索批次的状态，请使用 `GET /config /[configName]/execution/[execution-identifier]`. 执行标识符包含在批处理执行请求的HTTP响应的标头中。

状态请求的响应包含状态部分。 它提供有关批处理作业状态、已在管道中的记录数（已读取和正在处理）以及每个outputType/renderType的状态（正在处理的项目数、成功的项目数和失败的项目数）的详细信息。 状态还包括批处理作业的开始和结束时间以及有关错误的信息（如果有）。 在批处理运行实际完成之前，结束时间为–1。

>[!NOTE]
>
>* 请求多个PRINT格式时，状态包含多个条目。 例如，PRINT/ZPL、PRINT/IPL。
>* 批处理作业不会同时读取所有记录，而是继续读取并增加记录数。 因此，在读取所有记录之前，状态将返回–1。

### 查看生成的文档 {#view-generated-documents}

作业完成后，生成的文档将存储到 `success` 位于在批处理数据存储配置中指定的目标位置的文件夹。 如果有任何错误，服务将创建 `failure` 文件夹。 它提供有关错误类型和原因的信息。

让我们通过一个示例来了解：假设有一个输入数据文件 `record1.xml` 以及两种输出类型： `PDF` 和 `PCL`. 然后，目标位置包含两个子文件夹 `pdf` 和 `pcl`，每种输出类型一个。 假设PDF生成成功，然后 `pdf` 子文件夹包含 `success` 包含实际生成的PDF文档的子文件夹 `record1.pdf`. 假设PCL生成失败，则 `pcl` 子文件夹包含 `failure` 包含错误文件的子文件夹 `record1.error.txt` 其中包含错误的详细信息。 此外，目标位置还包含一个名为的临时文件夹 `__tmp__` 中保存批处理执行期间所需的某些文件。 当没有引用目标文件夹的活动批处理运行时，可以删除此文件夹。

>[!NOTE]
>
>根据输入记录的数量和模板的复杂性，处理批处理可能需要一些时间，请等待几分钟，然后再检查输出文件的目标文件夹。

## API参考文档

API参考文档提供了有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API参考文档以.yaml格式提供。 您可以下载 [批处理API](assets/batch-api.yaml) 并将其上传到Postman以检查API的功能。

>[!MORELIKETHIS]
>
>* [AEM Formsas a Cloud Service通信简介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [自适应Forms的AEM Formsas a Cloud Service架构和通信API](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)