---
title: 使用资产微服务处理资产
description: 使用云本机、可扩展的资产处理微服务处理您的数字资产。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Release Information,Asset Processing
role: Architect,Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 2%

---


# 资产微服务资产摄取和处理概述{#asset-microservices-overview}

Adobe Experience Manager作为[!DNL Cloud Service]提供了一种云本机方法来利用Experience Manager应用程序和功能。 此新架构的关键元素之一是资产摄取和处理，由资产微服务提供支持。 资产微服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务，以优化处理不同资产类型和处理选项。 云本机资产微服务的主要优势是：

* 可扩展的体系结构允许对资源密集型操作进行无缝处理。
* 高效的索引和文本提取，不会影响Experience Manager环境的性能。
* 最大限度地减少工作流在Experience Manager环境中处理资产处理的需求。 这将释放资源，最大限度地减少Experience Manager负载，并提供可扩展性。
* 提高了资产处理的恢复力。 处理非典型文件（如损坏的文件或超大文件）时的潜在问题不再影响部署的性能。
* 为管理员简化了资产处理配置。
* 资产处理设置由Adobe管理和维护，以提供用于处理各种文件类型的演绎版、元数据和文本提取的最知名配置
* 在适用情况下使用本机Adobe文件处理服务，提供高保真输出和[对Adobe专有格式的有效处理](file-format-support.md)。
* 能够配置后处理工作流，以添加特定于用户的操作和集成。

Asset microservices有助于避免对第三方渲染工具和方法（如ImageMagick和FFmpeg转码）的需求并简化配置，同时在默认情况下为常见文件类型提供基本功能。

## 高级体系结构{#asset-microservices-architecture}

高级架构图描述了整个系统中资产摄取和处理以及资产流动的关键元素。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![使用资产微服务获取和处理资](assets/asset-microservices-overview.png "产微服务获取和处理资产")

使用资产微服务进行获取和处理的关键步骤是：

* 客户端(如Web浏览器或Adobe资产链接)会向Experience Manager和开始发送上传请求，将二进制文件直接上传到二进制云存储。
* 当直接二进制上传完成时，客户端将通知Experience Manager。
* Experience Manager向资产microservices发送处理请求。 请求内容取决于指定的Experience Manager中的处理用户档案配置，要生成哪些再现。
* Assets microservices后端接收请求，根据请求将其调度到一个或多个microservices。 每个微服务直接从二进制云存储中访问原始二进制。
* 处理结果（如演绎版）存储在二进制云存储中。
* Experience Manager会收到通知，指向生成的二进制文件（演绎版）的直接指针已完成处理。 生成的演绎版可用于已上传的资产的Experience Manager。

这是资产获取和处理的基本流程。 如果已配置，Experience Manager还可以开始自定义工作流模型以对资产进行后处理。 例如，执行特定于您的环境的自定义步骤，例如从企业系统获取信息并添加到资产属性。

获取和处理流是资产微服务架构中用于Experience Manager的关键概念。

* **直接二进制访问**:在为Experience Manager环境配置后，资产会被传输（并上传）到Cloud Binary Store，然后，资产微型服务会被传输 [!DNL Experience Manager]（并上传），最后，客户可以直接访问这些资产以执行其工作。这样可以最大限度地减少网络上的负载和存储二进制文件的复制
* **外部化处理**:资源处理在环境之外完 [!DNL Experience Manager] 成，并节省其资源（CPU、内存），以提供关键的数字资产管理功能并支持与系统为最终用户提供的交互式工作

## 通过直接二进制访问{#asset-upload-with-direct-binary-access}上传资产

Experience Manager客户端是产品提供的一部分，默认情况下，所有支持通过直接二进制访问上传。 这包括使用Web界面上传、Adobe Asset Link和[!DNL Experience Manager]桌面应用程序。

您可以使用自定义上载工具，这些工具可直接与[!DNL Experience Manager] HTTP API一起使用。 您可以直接使用这些API，或者使用和扩展以下实现上载协议的开放源码项目：

* [开放源上载库](https://github.com/adobe/aem-upload)
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

有关详细信息，请参阅[上传资产](add-assets.md)。

## 添加自定义资产后期处理{#add-custom-asset-post-processing}

虽然大多数客户应从可配置的资产微服务获得其所有资产处理需求，但有些客户可能需要额外的资产处理。 如果资产需要根据来自其他系统的集成信息进行处理，则尤为如此。 在这种情况下，可以使用自定义的后处理工作流。

后处理工作流是常规的[!DNL Experience Manager]工作流模型，在[!DNL Experience Manager]工作流编辑器中创建和管理。 客户可以配置工作流对资产执行其他处理步骤，包括使用可用的现成工作流步骤和自定义工作流。

Adobe Experience Manager可以配置为在资产处理完成后自动触发后处理工作流。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [开始使用资产微服务](asset-microservices-configure-and-use.md)
>* [支持的文件格式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [关于直接二进制访问的Apache Oak文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

