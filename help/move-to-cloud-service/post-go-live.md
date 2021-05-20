---
title: 上线后阶段
description: 上线后阶段
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 100%

---

# 上线后 {#post-go-live}

在上线后阶段，您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

以下工具可用于对 AEM as a Cloud Service 环境进行故障诊断：

* **开发人员控制台**
* **CRX/DE Lite**
* **管理日志**


## 开发人员控制台 {#developer-console}

开发人员控制台中提供了调试 AEM as a Cloud Service 开发人员环境的功能，可用于开发、暂存和生产环境。

请参阅[实施 AEM as a Cloud Service](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)，了解有关开发工具的更多信息。

## CRX/DE Lite {#crxde-lite}

作为用户，您可以在开发环境中访问 CRX/DE Lite，但不能在暂存或生产环境中访问。

>[!IMPORTANT]
>在运行时写入不可变存储库（例如 `/libs` 和 `/apps`）将会导致错误。此外，作为客户，您将无法访问用于暂存和生产环境的开发人员工具。

请参阅[使用 CRX/DE Lite 进行开发](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRX/DE Lite 来开发 AEM 应用程序。

## 管理日志 {#managing-logs}

用户可以访问选定环境的可用日志文件列表。

请参阅[访问和管理日志](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html)，了解如何通过 UI 或通过 Cloud Manager 从 API 访问和管理日志。

### 其他支持 {#additional-support}

如果您对云服务的访问权限存有任何疑问，请联系您的 Adobe 代表或 Adobe AEM CQ 支持门户。
