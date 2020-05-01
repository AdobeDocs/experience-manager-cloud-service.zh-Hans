---
title: Adobe Experience Manager资产作为云服务的显着变化
description: 与Adobe Experience Manager 6.5相比，AEM Cloud服务中对Adobe Experience Manager资产的显着更改。
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager作为一种云服务，为管理AEM项目带来许多新功能和可能性。 但是，与Experience Manager作为云服务相比，Experience Manager Assets在内部部署或在Adobe Managed Service中存在很多差异。 本文档强调了资产功能的重要差异。 有关其他更改，请参 [阅对Experience Manager作为云服务的一般更改](/help/release-notes/aem-cloud-changes.md)。

与Experience Manager 6.5相比，主要区别在于：

* [资产摄取和上传](#asset-ingestion)。
* [用于云处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

## 资产摄取和上传 {#asset-ingestion}

通过支持更好的资产摄取和更快的上传，资源上传已经过优化，从而提高了效率。 产品功能（Web用户界面、桌面客户端）已更新。 但是，这可能会影响一些现有的自定义。

* Experience Manager使用直接二进制访问原则进行上传和下载，使用资产微服务进行资产处理。 请参 [阅资产摄取概述](/help/assets/asset-microservices-overview.md)。
   * 通过直接二 [进制访问上传资产](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 有关技术详细信息，请参 [阅直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。
* AEM 早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。相反，资产微服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取、用于索引的文本提取)。
   * 请参 [阅配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中具有自定义的工作流 [步骤，可以使用后](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 处理工作流。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名惯例）。

## 开发和测试资产微服务 {#asset-microservices}

资产微型服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务以优化处理不同的资产类型和处理选项。 Asset microservices有助于避免对第三方渲染工具和方法（如ImageMagick和FFmpeg转码）的需求，并简化配置，同时为常见文件类型提供开箱即用功能。 目前，云服务中不提供ImageMagick集成和FFMmpeg转码。

Asset microservices是一种云本机服务，可自动配置并连接到Experience Manager中在Cloud Manager中管理的客户项目和环境。 要扩展或自定义Experience Manager，开发人员可以将现有内容或资产与在云环境中生成的演绎版结合使用，以使用、显示、下载资产来测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用管道将代码更改部署到云开发环境, [并在完全执行资产微服务处理](/help/implementing/cloud-manager/configure-pipeline.md) 的情况下进行测试。

## 删除了经典 UI {#classic-ui}

Experience Manager中不再以云服务的形式提供经典UI。 标准界面是触屏优化UI。
