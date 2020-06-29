---
title: Adobe Experience Manager资产作为Cloud Service的显着变化
description: 与Adobe Experience Manager6.5相比，AEMCloud Service中的Adobe Experience Manager资产发生了显着变化。
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 10%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager作为Cloud Service，为管理AEM项目带来了许多新功能和可能性。 但是，与Experience Manager作为Cloud Service相比，内部部署或Adobe Managed Service中的Experience Manager资产有许多不同。 本文档强调了资产功能的重要差异。

与Experience Manager6.5相比，主要区别在于：

* [资产摄取和上传](#asset-ingestion)。
* [用于云处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

>[!NOTE]
>此文档突出了对AEM Assets的显着变化。 有关AEM作为Cloud Service和其他模块的常规更改，请参阅：
>
>* [Adobe Experience Manager 云服务简介](/help/overview/introduction.md)
>* 作 [为Cloud Service的AEM概述——新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager 云服务[架构](/help/core-concepts/architecture.md)
>* [对AEM作为Cloud Service的显着更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
>* [对 Sites 作为 AEM 云服务的显著更改](/help/sites-cloud/sites-cloud-changes.md)
>* [Adobe Experience Manager 云服务教程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


## 资产摄取和上传 {#asset-ingestion}

通过支持更好的资产摄取和更快的上传，资源上传已经过优化，从而提高了效率。 产品功能（Web用户界面、桌面客户端）已更新。 但是，这可能会影响一些现有的自定义。

* Experience Manager使用直接二进制访问原则进行上传和下载，资产微服务用于资产处理。 请参 [阅资产摄取概述](/help/assets/asset-microservices-overview.md)。
   * 通过直接二 [进制访问上传资产](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 有关技术详细信息，请参 [阅直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。
* AEM 早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。相反，资产微服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取、用于索引的文本提取)。
   * 请参 [阅配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中具有自定义的工作流 [步骤，可以使用后](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 处理工作流。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名惯例）。

## 开发和测试资产微服务 {#asset-microservices}

资产微型服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务以优化处理不同的资产类型和处理选项。 资产微服务有助于避免对第三方渲染工具和方法（如ImageMagick）的需求并简化配置，同时为常见文件类型提供现成功能。 您现在可以处 [理各种现成格式的文件](/help/assets/file-format-support.md) ，这些格式比以前版本的Experience Manager所能处理的格式更多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。 不能将ImageMagick的复杂配置用于处 [!UICONTROL 理用户档案配] 置。 此外，还可 [!DNL Dynamic Media] 用于视频的FFmpeg转码。

资产微服务是一种云本机服务，可自动配置并连接到Cloud Manager中管理的Experience Manager项目和环境中的。 要扩展或自定义Experience Manager，开发人员可以将现有内容或资产与在云环境中生成的演绎版结合使用，以使用、显示、下载资产测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用管道将代码更改部署到云开发环境, [并在完全执行资产微服务处理](/help/implementing/cloud-manager/configure-pipeline.md) 的情况下进行测试。

## 删除了经典 UI {#classic-ui}

经典UI不再作为Experience Manager提供。 标准界面是触屏优化UI。
