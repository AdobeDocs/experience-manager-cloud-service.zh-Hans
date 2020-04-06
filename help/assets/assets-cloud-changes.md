---
title: Adobe Experience Manager资产作为云服务的显着变化
description: 与Experience Manager 6.5相比，AEM Cloud服务中对Adobe Experience Manager资产的显着更改
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager作为云服务，为管理AEM项目提供了许多新功能和可能性。 但是，与作为云服务的Experience Manager相比，Experience Manager资产在预置或Adobe Managed Service中存在许多差异。 本文档重点介绍了这些重要差异。

>[!NOTE]
>
>本文档重点介绍特定于Experience Manager资产（作为云服务）的显着更改。 查看对Experience Manager作 [为云服务的常规更改](/help/release-notes/aem-cloud-changes.md)。

与Experience Manager 6.5相比，主要区别在于：

* [资产摄取](#asset-ingestion)
* [删除了经典 UI](#classic-ui)

## 资产摄取 {#asset-ingestion}

资产上传已经过优化，可提高效率，从而更好地扩展资产摄取和更快地上传。 产品功能（Web用户界面、桌面客户端）已更新。 但是，这可能会影响一些现有的自定义代码。

* Experience Manager使用直接二进制访问原则上传和下载资产，并使用资产微服务进行资产处理。 请参阅 [资产摄取概述](/help/assets/asset-microservices-overview.md)
   * 通过直接二进制 [访问上传资产](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * 有关技术详细信息，请参 [阅直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* AEM 早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。相反，资产微型服务提供了可扩展的、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取、文本提取)
   * 请参阅 [配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中实现自定义的工作流步骤， [可使用后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 。
* 通过包管理器输入的资产需要使用“资产”界面中的&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作执行手动重新处理。

使用资产微服务生成的标准演绎版以向后兼容的方式存储在资产存储库节点中（相同的命名约定）。

## 开发和测试资产微服务 {#developing-testing-asset-microservices}

Asset microservices是一种原生云服务，可自动配置并连接到Experience Manager中在Cloud Manager中管理的客户项目和环境中的Experience Manager。 致力于扩展Experience Manager或进行自定义的开发人员可以使用现有内容(或资产与在云环境中生成的演绎版一起使用)来测试和验证其代码，包括使用、显示和下载资产。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用管道将代码更改部署到云开发环境，并测试资产微服务处理的完全执行。

## 删除了经典 UI {#classic-ui}

经典UI在Experience Manager中不再作为云服务可用。
