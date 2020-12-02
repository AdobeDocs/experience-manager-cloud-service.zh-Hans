---
title: Adobe Experience Manager资产中a [!DNL Cloud Service]的显着变化
description: 与Adobe Experience Manager6.5相比，AEM中Adobe Experience Manager资产的显着变化 [!DNL Cloud Service] 。
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 6%

---


# 对Experience Manager资产的显着更改为[!DNL Cloud Service] {#notable-changes}

Adobe Experience Manager公司[!DNL Cloud Service]为管理AEM项目带来了许多新功能和可能性。 但是，与[!DNL Cloud Service]Experience Manager相比，Adobe资产在内部部署或在Experience Manager托管服务中存在许多差异。 本文档强调了资产功能的重要差异。

与Experience Manager6.5相比，主要区别在于：

* [资产摄取和上传](#asset-ingestion)。
* [用于云本机处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

>[!NOTE]
>
>这一文档突显了AEM Assets的显着变化。 有关[!DNL Cloud Service]和其他模块对Experience Manager的常规更改，请参阅：
>
>* [Adobe Experience Manager as a 简介 [!DNL Cloud Service]](/help/overview/introduction.md)
>* AEM a[概述a [!DNL Cloud Service] -新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a [架构](/help/core-concepts/architecture.md)[!DNL Cloud Service]
>* [AEM as a(发行说明 [!DNL Cloud Service] )的显着更改](/help/release-notes/aem-cloud-changes.md)
>* [AEM Sites [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [Adobe Experience Manager [!DNL Cloud Service] 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## 资产摄取和上传{#asset-ingestion}

通过支持更好的资产摄取和更快的上传，资源上传已经过优化，从而提高了效率。 产品功能（Web用户界面、桌面客户端）已更新。 但是，这可能会影响一些现有的自定义。

* Experience Manager使用直接二进制访问原则进行上传和下载，资产微服务用于资产处理。 请参阅[资产摄取概述](/help/assets/asset-microservices-overview.md)。
   * 资产上传[（直接二进制访问](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)）。
   * 有关技术详细信息，请参阅[直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
* AEM 早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。相反，资产微服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取、用于索引的文本提取)。
   * 请参阅[配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中具有自定义的工作流步骤，可以使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。
* 通过包管理器导入的资产需要使用资产界面中的&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作进行手动重新处理。

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名惯例）。

## 开发和测试资产微服务{#asset-microservices}

资产微型服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务以优化处理不同的资产类型和处理选项。 资产微服务有助于避免对第三方渲染工具和方法（如ImageMagick）的需求并简化配置，同时为常见文件类型提供现成功能。 您现在可以处理[范围广泛的文件类型](/help/assets/file-format-support.md)，这些类型的开箱即用格式比先前版本的Experience Manager所能处理的格式更多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。 不能将ImageMagick的复杂配置用于[!UICONTROL 处理用户档案]配置。 使用[!DNL Dynamic Media]对视频进行FFmpeg转码，使用处理用户档案对MP4视频进行[基本转码。](/help/assets/manage-video-assets.md#transcode-video)

资产微服务是一种云本机服务，可自动配置并连接到Cloud Manager中管理的Experience Manager项目和环境中的。 要扩展或自定义Experience Manager，开发人员可以将现有内容或资产与在云环境中生成的演绎版结合使用，以使用、显示、下载资产测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)将代码更改部署到云开发环境，并通过资产微服务处理的完全执行进行测试。

## 删除了经典 UI {#classic-ui}

经典UI在Experience Manager中不再作为[!DNL Cloud Service]可用。 标准界面是触屏优化UI。
