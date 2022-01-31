---
title: Experience Manager [!DNL Forms] as a Cloud Service通信批处理
description: 如何创建以品牌为导向的个性化通信？
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: f8f9aeb12d7a988deaf1ceed2cdf29519f8102dd
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Formsas a Cloud Service通信 — 批处理

通信允许您创建、组合和提供以品牌为导向的个性化通信，如商务信函、文档、报表、理赔处理信函、福利通知、理赔处理信函、每月账单和欢迎资料包。 您可以使用通信API将模板(XFA或PDF)与客户数据结合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文档。

通信为按需和计划的文档生成提供了API。 您可以将同步API用于按需API和批量API（异步API），以进行计划文档生成：

* 同步API适用于按需、低延迟和单记录文档生成用例。 这些API更适合基于用户操作的用例。 例如，在用户填写表单后生成文档。

* 批处理API（异步API）适用于计划的高吞吐量多文档生成用例。 这些API可批量生成文档。 例如，每月生成的电话账单、信用卡报表和福利报表。

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## 批处理操作 {#batch-operations}

批处理操作是按计划时间间隔为一组记录生成多个类似类型的文档的过程。 批处理操作包含两个部分：配置（定义）和执行。

* **配置（定义）**:批处理配置存储有关要为生成的文档设置的各种资产和属性的信息。 例如，它提供了有关XDP或PDF模板以及要用于为输出文档指定各种属性的客户数据的位置的详细信息。

* **执行**:要启动批处理操作，请将批处理配置名称传递到批处理执行API。

### 批处理操作的组件 {#components-of-a-batch-operations}

**云配置**:Experience Manger Cloud配置可帮助您将Experience Manager实例连接到客户拥有的Microsoft Azure Storage。 它允许您指定客户拥有的Microsoft Azure帐户的凭据以连接到该帐户。

**批量数据存储配置(USC)**:批量数据配置可帮助您为批量API配置Blob存储的特定实例。 它允许您在客户拥有的Microsoft Azure Blob Storage中指定输入和输出位置。

**批量API**:允许您创建批处理配置并根据这些配置执行批处理运行，以将PDF或XDP模板与数据合并，并以PDF、PS、PCL、DPL、IPL和ZPL格式生成输出。 通信为配置管理和批量执行提供了批量API。

![数据合并表](assets/communications-batch-structure.png)

**存储**:通信API使用客户拥有的Microsoft Azure Cloud存储来获取客户记录并存储生成的文档。 在“Microsoft配置”中配置Experience Manager Cloud Service Azure存储。

**应用程序**:您的自定义应用程序，用于使用批处理API生成和使用文档。

## 使用批处理操作生成多个文档 {#generate-multiple-documents-using-batch-operations}

您可以使用批处理操作以计划的间隔生成多个文档。

>[!VIDEO](https://video.tv.adobe.com/v/338349)

您可以观看视频或执行以下说明，了解如何使用批处理操作生成文档。 视频中使用的API引用文档采用.yaml格式。 您可以下载 [批量API](assets/batch-api.yaml) 文件并上传到Postman，以检查API的功能，并观看视频。

### 先决条件 {#pre-requisites}

要使用批处理API，需要满足以下条件：

* [Microsoft Azure存储帐户](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* PDF或XDP模板
* [要与模板合并的数据](#form-data)
* 具有Experience Manager管理员权限的用户

### 设置环境 {#setup-your-environment}

在使用批处理操作之前：

* 将客户数据（XML文件）上传到Microsoft Azure Blob Storage
* 创建云配置
* 创建批量数据存储配置
* 将模板和其他资产上传到Experience Manager FormsCloud Service实例

### 将客户数据（XML文件）上传到Azure存储 {#upload-customer-data-to-Azure-Storage}

在Microsoft Azure存储上，创建 [容器](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) 和 [上传客户数据(XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) 到 [文件夹](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) 在容器内。
>[!NOTE]
>
>您可以配置Microsoft Azure存储，以自动清除输入文件夹或按计划间隔将输出文件夹的内容移动到其他位置。 但是，请确保在引用文件夹的批处理操作仍在运行时未清理文件夹。

### 创建云配置 {#create-a-cloud-configuration}

云配置将您的Experience Manager实例连接到Microsoft Azure Storage。 要创建云配置，请执行以下操作：

1. 转到工具>Cloud Services> Azure Storage
1. 打开用于托管配置的文件夹，然后单击创建。 使用全局文件夹或创建文件夹。
1. 指定要连接到服务的配置和凭据的名称。 您可以 [从Microsoft Azure存储门户中检索这些凭据](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. 单击创建。

您的Experience Manager实例现已准备好连接到Microsoft Azure Storage，并在需要时使用它存储和读取内容。

### 创建批量数据存储配置 {#create-batch-data-store-configuration}

批量数据配置可帮助您配置用于输入和输出的容器和文件夹。 您将客户记录保留在“源文件夹”中，生成的文档将放在“目标文件夹”中。

要创建配置，请执行以下操作：

1. 转到工具> Forms > Unified Storage Connector 。
1. 打开用于托管配置的文件夹，然后单击创建。 使用全局文件夹或创建文件夹。
1. 指定配置的标题和名称。 在“存储”中，选择Microsoft Azure存储。
1. 在存储配置路径中，浏览并选择云配置，该配置包含客户拥有的Azure存储帐户的凭据。
1. 在“源文件夹”中，指定Azure存储容器的名称以及包含记录的文件夹。
1. 在目标文件夹中，指定Azure存储容器的路径，并指定用于存储生成文档的文件夹。
1. 单击创建。

您的Experience Manager实例现已连接到Microsoft Azure存储，并配置为检索数据并将数据发送到Microsoft Azure存储上的特定位置。

### 将模板和其他资产上传到Experience Manager实例 {#upload-templates-and-other-assets-to-your-AEM-instance}

组织通常具有多个模板。 例如，信用卡报表、福利报表和索赔申请各有一个模板。 将所有此类XDP和PDF模板上传到Experience Manager实例。 要上传模板，请执行以下操作：

1. 打开Experience Manager实例。
1. 转到Forms > Forms和文档
1. 单击创建>文件夹，然后创建文件夹。 打开该文件夹。
1. 单击创建>文件上传，然后上传模板。

## 使用批处理API生成文档 {#use-batch-API-to-generate-documents}

要使用批处理API，请创建批处理配置并根据该配置执行运行。 API文档提供了有关用于创建和运行批处理的API、相应参数和可能的错误的信息。 您可以下载 [API定义文件](assets/batch-api.yaml) 文件并上传到 [邮递员](https://go.postman.co/home) 或用于测试API以创建和运行批处理操作的类似软件。

### 创建批处理 {#create-a-batch}

要创建批，请使用 `POST /config` API。 在HTTP请求正文中包含以下必需属性：

* **configName**:指定批的唯一名称。 例如, `wknd-job`
* **dataSourceConfigUri**:指定批量数据存储配置的位置。 它可以是配置的相对路径或绝对路径。 例如：`/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputTypes**:指定输出格式：PDF和打印。 如果使用PRINT输出类型，请在 `printedOutputOptionsList` 属性中，请至少指定一个打印选项。 打印选项通过其渲染类型进行标识，因此当前不允许使用具有相同渲染类型的多个打印选项。 支持的格式为PS、PCL、DPL、IPL和ZPL。

* **模板**:指定模板的绝对或相对路径。 例如, `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

如果指定相对路径，则还应提供内容根。 有关内容根的详细信息，请参阅API文档。

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

您可以使用 `GET /config /[configName]` 以查看批配置的详细信息。

### 运行批处理 {#run-a-batch}

要运行（执行）批处理，请使用 `POST /config /[configName]/execution`. 例如，要运行名为wknd-demo的批处理，请使用/config/wknd-demo/execution。 服务器在接受请求时返回HTTP响应代码202。 API不会返回任何有效负载，但服务器上运行的批处理作业的HTTP响应标头中唯一代码（执行标识符）除外。 您可以使用执行标识符来检索批处理的状态。

>[!NOTE]
>
>在批处理运行时，请勿对相应的源文件夹和目标文件夹、数据源配置和Microsoft Azure Cloud配置进行任何更改。

### 检查批的状态 {#status-of-a-batch}

要检索批的状态，请使用 `GET /config /[configName]/execution/[execution-identifier]`. 批量执行请求的HTTP响应标头中包含执行标识符。

状态请求的响应包含状态部分。 它提供了有关批处理作业状态、管道中已经（已读取并正在处理）的记录数以及每个outputType/renderType（进行中、成功和失败项目数）的状态的详细信息。 状态还包括批处理作业的开始和结束时间以及有关错误的信息（如果有）。 结束时间为–1，直到实际完成批处理运行。

>[!NOTE]
>
>* 请求多种PRINT格式时，状态包含多个条目。 例如，PRINT/ZPL、PRINT/IPL。
>* 批处理作业不会同时读取所有记录，而是会继续读取和增加记录数。 因此，状态会返回–1，直到读取所有记录。


### 查看生成的文档 {#view-generated-documents}

在完成作业时，生成的文档被存储到 `success` 文件夹。 如果存在任何错误，服务将创建 `failure` 文件夹。 它提供了有关错误类型和原因的信息。

让我们通过一个示例来了解一下：假设有一个输入数据文件 `record1.xml` 和两种输出类型： `PDF` 和 `PCL`. 然后，目标位置包含两个子文件夹 `pdf` 和 `pcl`，则每种输出类型对应一个。 假设PDF生成成功，则 `pdf` 子文件夹包含 `success` 子文件夹，而子文件夹又包含实际生成的PDF文档 `record1.pdf`. 假设PCL生成失败，然后 `pcl` 子文件夹包含 `failure` 子文件夹，该子文件夹又包含错误文件 `record1.error.txt` 其中包含错误的详细信息。 此外，目标位置还包含一个名为的临时文件夹 `__tmp__` 它保存在批量执行过程中所需的某些文件。 当没有引用目标文件夹的活动批处理运行时，可以删除此文件夹。

>[!NOTE]
>
>根据输入记录的数量和模板的复杂性，处理批处理可能需要一些时间，在检查输出文件的目标文件夹之前需要等待几分钟。

## API参考文档

API参考文档提供了有关API提供的所有参数、身份验证方法和各种服务的详细信息。 API引用文档以.yaml格式提供。 您可以下载 [批量API](assets/batch-api.yaml) 并将其上传到Postman以检查API的功能。
