---
title: Adobe Experience Manager资产作为云服务的显着变化
description: 与Experience Manager 6.5相比，AEM Cloud服务中对Adobe Experience Manager资产的显着更改
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Experience Manager资产作为云服务的显着变化 {#notable-changes}

Adobe Experience manager作为云服务，为管理AEM项目提供了许多新功能和可能性。 但是，与作为云服务的Experience Manager相比，Experience Manager资产在预置型或Adobe Managed service中存在许多差异。 本文档突出强调了重要差异。

>[!NOTE]
>
>本文档重点介绍特定于Experience Manager Assets作为云服务的显着更改。 查看对Experience manager作 [为云服务的常规更改](/help/release-notes/aem-cloud-changes.md)。

与Experience Manager 6.5相比，主要区别在于：

* [资产摄取](#asset-ingestion)
* [删除经典UI](#classic-ui)

## 资产摄取 {#asset-ingestion}

资产上传已经过优化，可提高效率，从而更好地扩展资产摄取和更快地上传。 产品功能（Web用户界面、桌面客户端）已更新。 但是，这可能会影响一些现有的自定义代码。

* Experience manager使用直接二进制访问原则上传和下载资产，并使用资产微服务进行资产处理。 请参阅 [资产摄取概述](/help/assets/asset-microservices-overview.md)
   * 通过直接二进制 [访问上传资产](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * 有关技术详细信息，请参 [阅直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* AEM早期版本 **[!UICONTROL 中的默认工作流]** DAM资产更新不再可用。 相反，资产微型服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理（演绎版、元数据提取、文本提取以用于索引）
   * 请参阅 [配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中实现自定义的工作流步骤， [可使用后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 。
* 通过包管理器导入的资产需要使用资产界面中的重新处理 **[!UICONTROL 资产操作]** ，手动进行重新处理。

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名约定）。

## 开发和测试资产微服务 {#developing-testing-asset-microservices}

Asset Microservices是一种原生云服务，可在Cloud manager中管理的客户程序和环境中自动配置并连接到Experience Manager。 致力于扩展Experience manager或进行自定义的开发人员可以使用现有内容（或资产与在云环境中生成的演绎版一起使用）来测试和验证其代码，包括使用、显示和下载资产。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用管道将代码更改部署到云开发环境，并测试资产微服务处理的完全执行。

## 删除经典UI {#classic-ui}

经典UI在Experience manager中不再作为云服务可用。
