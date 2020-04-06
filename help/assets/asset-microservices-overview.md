---
title: 了解资产微型服务如何处理云中的数字资产
description: 使用云本机、可扩展的资产处理微服务处理您的数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 55dd497caaa25cf7c0d8da1c1400b74f7d265d29

---


# 资产微型服务的资产摄取和处理概述 {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.

-->

Adobe Experience Manager作为云服务，提供了利用Experience Manager应用程序和功能的云本机方式。 此新架构的关键元素之一是资产摄取和处理，由资产微服务提供支持。

资产微型服务使用云服务提供可伸缩的、具有弹性的资产处理，这些服务由Adobe管理，以优化处理不同的资产类型和处理选项。 主要优势包括：

* 可扩展的体系结构允许对资源密集型操作进行无缝处理。
* 高效的索引和文本提取不会影响Experience Manager环境的性能。
* 在Experience Manager环境中，将工作流处理资产处理的需求降至最低。 这可以释放资源，最大限度地减少Experience Manager的负载，并提供可伸缩性。
* 提高了资产处理的恢复力。 处理非典型文件（如损坏的文件或超大文件）时的潜在问题不再影响部署的性能。
* 简化了管理员的资产处理配置。
* 资产处理设置由Adobe管理和维护，以提供最知名的配置，用于处理各种文件类型的再现、元数据和文本提取
* 在适用情况下使用原生Adobe文件处理服务，提供高保真输出和 [对Adobe专有格式的高效处理](file-format-support.md)。
* 能够配置后处理工作流以添加特定于用户的操作和集成。

Asset microservices有助于避免对第三方渲染工具（如ImageMagick）的需求并简化系统配置，同时为常见文件类型提供开箱即用的功能。

## 高级架构 {#asset-microservices-architecture}

高级架构图描述了整个系统中资产获取和处理以及资产流的关键元素。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![使用资产微型服务获取和处理资](assets/asset-microservices-overview.png "产微型服务获取和处理资产")

使用资产微服务获取和处理的关键步骤是：

* 客户端（如Web浏览器或Adobe Asset Link）向Experience Manager发送上传请求，并将二进制文件直接上传到二进制云存储。
* 直接二进制上传完成后，客户端将通知Experience Manager。
* Experience Manager会向资产微型服务发送处理请求。 请求内容取决于Experience Manager中的处理用户档案配置，该配置指定了应生成哪些再现
* Assets microservices后端接收该请求，并基于该请求将其调度到一个或多个MicroServices。 每个微服务都直接从二进制云存储中访问原始二进制。
* 处理结果（如演绎版）存储在二进制云存储中。
* Experience Manager会收到通知，该处理已完成，并有指向生成的二进制文件（演绎版）的直接指针，然后Experience Manager中会为上传的资产提供这些二进制文件

这是资产获取和处理的基本流程。 如果已配置，Experience Manager还可以开始客户的工作流模型以对资产进行后处理——例如，执行特定于客户环境的某些自定义步骤，如从客户的企业系统中获取信息以添加到资产属性。

摄取和处理流程显示了Experience Manager的资产微服务架构所利用的几个关键概念：

* **直接二进制访问** -在为Experience Manager环境配置后，资产会被传输（并上传）到Cloud Binary Store，然后AEM、资产微型服务和客户端可以直接访问它们来执行工作。 这将网络负载和存储二进制文件的复制降至最低
* **外部化处理** -在AEM环境之外完成资产处理，并节省其资源（CPU、内存），以便为最终用户提供关键数字资产管理功能并支持与系统的交互式工作

## 通过直接二进制访问上传资产 {#asset-upload-with-direct-binary-access}

Experience Manager客户端是产品提供的一部分，默认情况下，所有客户端均支持通过直接二进制访问进行上传。 这包括使用Web界面、Adobe Asset Link和AEM桌面应用程序上传。

您可以使用自定义上传工具，这些工具可直接与AEM HTTP API一起使用。 您可以直接使用这些API，或者使用和扩展以下实现上传协议的开放源项目：

* [开放源上传库](https://github.com/adobe/aem-upload)
* [开放源代码命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

有关详细信息，请参阅 [上传资产](add-assets.md)。

## 添加自定义资产后期处理 {#add-custom-asset-post-processing}

虽然大多数客户应从可配置的资产微服务获得其所有资产处理需求，但有些客户可能需要额外的资产处理。 如果资产需要根据来自其他系统的集成信息进行处理，则尤为如此。 在这种情况下，可以使用自定义的后处理工作流。

后期处理工作流是常规AEM工作流模型，在AEM Workflow编辑器中创建和管理。 客户可以配置工作流以对资产执行其他处理步骤，包括使用可用的现成工作流步骤和自定义工作流。

Adobe Experience Manager可配置为在资产处理完成后自动触发后处理工作流。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [开始使用资产微服务](asset-microservices-configure-and-use.md)
>* [支持的文件格式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [AEM 桌面应用程序](https://docs.adobe.com/content/help/zh-Hans/experience-manager-desktop-app/using/introduction.html)
>* [关于直接二进制访问的Apache Oak文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

