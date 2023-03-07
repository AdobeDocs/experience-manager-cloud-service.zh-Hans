---
title: 使用资产微服务处理资产
description: 使用云原生和可扩展的资产处理微服务来处理数字资产。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Release Information,Asset Processing
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: ht
source-wordcount: '820'
ht-degree: 100%

---

# 使用资产微服务进行资产获取和处理概述 {#asset-microservices-overview}

Adobe Experience Manager as a [!DNL Cloud Service] 提供了一种云原生方法来利用 Experience Manager 应用程序和功能。这种新架构的关键元素之一是由资产微服务提供支持的资产摄取和处理。资产微服务使用云服务来对资产进行可扩展的弹性处理。Adobe 管理云服务以实施对不同的资源类型和处理选项的最优处理。云原生资产微服务的主要好处是：

* 可扩展架构，允许无缝处理资源密集型操作。
* 高效索引和文本提取，不影响 Experience Manager 环境的性能。
* 最大限度地减少对用于在 Experience Manager 环境中控制资产处理的工作流的需求。这将释放资源，最大限度地减少 Experience Manager 上的负载，并提供可扩展性。
* 提高了资产处理的弹性。处理非典型的文件（例如，损坏的文件或超大文件）时出现的潜在问题再也不会影响部署的性能。
* 为管理员简化了资产处理配置。
* 资产处理设置由 Adobe 管理和维护，从而提供最佳配置来处理各种文件类型的再现、元数据和文本提取
* 在适用的情况下使用本机 Adobe 文件处理服务，提供高保真输出并[高效处理 Adobe 专有格式](file-format-support.md)。
* 能够配置处理后工作流以添加用户特定的操作和集成。

资产微服务有助于消除对第三方呈现工具和方法（如 [!DNL ImageMagick] 和 FFmpeg 转码）的需求并简化配置，同时默认提供用于常见文件格式的基本功能。

## 高层架构 {#asset-microservices-architecture}

高级架构图描述了资产摄取和处理的关键元素以及系统中的资产流。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![使用资产微服务进行资产摄取和处理](assets/asset-microservices-overview.png "使用资产微服务进行资产摄取和处理")

使用资产微服务进行摄取和处理的主要步骤是：

* Web 浏览器或 Adobe Asset Link 等客户端向 [!DNL Experience Manager] 发送上传请求，并开始将二进制文件直接上传到二进制云存储。
* 在完成直接二进制上传后，客户端将告知 [!DNL Experience Manager]。
* [!DNL Experience Manager] 向资产微服务发送处理请求。请求内容取决于 [!DNL Experience Manager] 中指定要生成哪些演绎版的处理配置文件配置。
* 资产微服务后端将接收请求，并根据请求将它发送到一个或多个微服务。每个微服务直接从二进制云存储访问原始二进制文件。
* 处理的结果（例如演绎版）将存储在二进制云存储中。
* Experience Manager 会收到处理已完成的通知以及指向生成的二进制文件（演绎版）的直接指针。为上传的资产生成的演绎版在 [!DNL Experience Manager] 中可用。

这是资产摄取和处理的基本流程。如果已配置，Experience Manager 还可以启动自定义工作流模型来对资产进行后处理。例如，执行特定于环境的自定义步骤，例如，从企业系统中获取信息并添加到资产属性。

摄取和处理流是 Experience Manager 的资产微服务架构的关键概念。

* **直接二进制访问**：针对 Experience Manager 环境进行配置后，资产将依次传输（并上传）到云二进制存储、[!DNL Experience Manager] 和资产微服务，最后客户端可以直接访问它们以便执行工作。这将最大限度地减少网络负载和存储的二进制文件的重复
* **外部化处理**：资产处理在 [!DNL Experience Manager] 环境外部完成，并节省其资源（CPU、内存）以便提供关键的数字资产管理 (DAM) 功能，同时支持与最终用户的系统进行交互

## 使用直接二进制访问的资产上传 {#asset-upload-with-direct-binary-access}

Experience Manager 客户端是产品的一部分，默认情况下都支持使用直接二进制访问进行上传。其中包括使用 Web 界面、Adobe Asset Link 和 [!DNL Experience Manager] 桌面应用程序进行上传。

您可以使用自定义上传工具，它们直接与 [!DNL Experience Manager] HTTP API 一起使用。您可以直接使用这些 API，也可以使用和扩展以下实施上传协议的开源项目：

* [开源上传库](https://github.com/adobe/aem-upload)
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

有关更多信息，请参阅[上传资产](add-assets.md)。

## 添加自定义资产后处理 {#add-custom-asset-post-processing}

虽然大多数客户应从可配置的资产微服务中获得所有资产处理需求，但有些客户可能需要额外的资产处理。在需要根据来自其他系统的信息通过集成处理资产时，情况尤为如此。在这种情况下，可以使用自定义后处理工作流。

后处理工作流是常规 [!DNL Experience Manager] 工作流模型，该模型是在 [!DNL Experience Manager] 工作流编辑器中创建和管理的。客户可以配置工作流以对资产执行额外的处理步骤，包括使用现成的工作流步骤和自定义工作流。

可以将 Adobe Experience Manager 配置为在资产处理完成后自动触发后处理工作流。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [开始使用资产微服务](asset-microservices-configure-and-use.md)
>* [支持的文件格式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [关于直接二进制访问的 Apache Oak 文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

