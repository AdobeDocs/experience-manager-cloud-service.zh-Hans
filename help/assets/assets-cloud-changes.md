---
title: ' [!DNL Adobe Experience Manager Assets] 中a [!DNL Cloud Service]的显着变化'
description: 与[!DNLAdobe Experience Manager6.5]相比， [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 的显着变化。
translation-type: tm+mt
source-git-commit: ed449eea146ec18bdc4d25ae4938f9a36180037d
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 3%

---


# 对[!DNL Experience Manager Assets]作为[!DNL Cloud Service] {#notable-changes}的显着更改

[!DNL Adobe Experience Manager] 这为管理 [!DNL Cloud Service] 您的Experience Manager项目带来了许多新功能和可能性。与作为[!DNL Cloud Service]的[!DNL Experience Manager]相比，[!DNL Experience Manager Assets]内部部署或作为Adobe托管服务托管之间有许多差异。 本文重点介绍[!DNL Assets]功能的重要区别。

与[Experience Manager] 6.5相比，主要区别在于：

* [资产摄取、上传和处理](#asset-ingestion)。
* [用于云本机处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

## 资产摄取和处理{#asset-ingestion}

通过支持更好的摄取缩放、更快的上传、使用微服务更快的处理以及批量摄取，资源上传已经过优化，从而提高了效率。 产品功能（Web用户界面、桌面客户端）已更新。 此外，这可能会影响一些现有自定义设置。

* [!DNL Experience Manager] 使用直接二进制访问原则上传和下载资产，并使用资产微服务处理资产。请参阅[microservices的概述](/help/assets/asset-microservices-overview.md)。
   * 资产上传[（直接二进制访问](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)）。
   * 有关技术详细信息，请参阅[直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 有关基本CRUD操作的可用API方法的比较，请参阅[API和资产操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，资产微服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取和用于索引的文本提取)。
   * 请参阅[配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中具有自定义的工作流步骤，可以使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。
* 使用包管理器上传的资产需要使用[!DNL Assets]界面中的&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作进行手动重新处理。
* 没有扩展或扩展不正确的数字资产不会根据需要进行处理。 例如，上传此类资产时，资产可能不会发生任何情况，或者处理用户档案不正确。 用户仍可以在DAM中存储二进制文件。

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名惯例）。

## 开发和测试资产微服务{#asset-microservices}

资产微型服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务以优化处理不同的资产类型和处理选项。 资产微服务有助于避免对第三方渲染工具和方法（如ImageMagick）的需求并简化配置，同时为常见文件类型提供现成功能。 您现在可以处理[范围广泛的文件类型](/help/assets/file-format-support.md)，这些类型的开箱即用格式比先前版本的Experience Manager所能处理的格式更多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。 不能将ImageMagick的复杂配置用于[!UICONTROL 处理用户档案]配置。 使用[!DNL Dynamic Media]进行视频的高级FFmpeg转码，使用处理用户档案进行MP4视频的基本转码[。](/help/assets/manage-video-assets.md#transcode-video)

资产微服务是一种云本机服务，可自动配置并连接到Cloud Manager中管理的Experience Manager项目和环境中的。 要扩展或自定义Experience Manager，开发人员可以将现有内容或资产与在云环境中生成的演绎版结合使用，以使用、显示、下载资产测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)将代码更改部署到云开发环境，并通过资产微服务处理的完全执行进行测试。

## 删除了经典 UI {#classic-ui}

经典UI在Experience Manager中不再作为[!DNL Cloud Service]可用。 标准界面是触屏优化UI。

>[!MORELIKETHIS]
>
>* [介绍 [!DNL Adobe Experience Manager] a [!DNL Cloud Service]](/help/overview/introduction.md)
>* [ [!DNL Experience Manager] as a [!DNL Cloud Service] 概述——新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* [!DNL Experience Manager]的[架构](/help/core-concepts/architecture.md)作为[!DNL Cloud Service]
>* [a的显 [!DNL Experience Manager] 着变化 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)
>* [a的显 [!DNL Experience Manager Sites] 着变化 [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

