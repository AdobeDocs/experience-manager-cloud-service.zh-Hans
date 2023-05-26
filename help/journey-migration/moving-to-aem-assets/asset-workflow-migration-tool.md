---
title: 资产工作流迁移工具
description: 资产工作流迁移工具
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# 资产工作流迁移工具 {#asset-workflow-migration}

资产工作流迁移工具可用于自动将资产处理工作流从 AEM 的内部部署或 AMS 部署迁移到处理配置文件和 OSGi 配置，以在 AEM Assets as a Cloud Service 中使用。

## 简介 {#introduction}

本节介绍了有关资产工作流迁移工具的资源和实施详细信息。

借助此实用程序，AEM 开发人员可以将现有 AEM 资产处理工作流迁移到 AEM as a Cloud Service。

## 支持的工作流 {#migration-support-for-workflows}

工作流具有不同的迁移支持级别。 查看此 [特定工作流的列表](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). 根据提供的支持，这些工作流分为以下类别。 Adobe支持迁移中列出的工作流 `SUPPORTED`， `REQUIRED`，或 `OPTIONAL` 类别。 不支持其他类别中提到的工作流步骤。

* `SUPPORTED`：中支持的功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `OPTIONAL`：中的可选功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `REQUIRED`：添加到工作流的必需步骤。
* `UNNECESSARY`：中不需要功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `NUI_OOTB`：提供的功能 [asset compute服务](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`：默认提供的功能 [!DNL Dynamic Media] 连接器。
* `NUI_MIGRATED`：已迁移到 [处理Asset compute服务的配置文件](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`：当前不支持 [!DNL Experience Manager Assets] as a Cloud Service。

## 使用资产工作流迁移工具 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**：Adobe建议通过以下方式使用资源工作流迁移工具： `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] as a [!DNL Cloud Service] 的代码重构插件 [!DNL Adobe I/O] CLI)。 要了解如何安装和使用插件，请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **独立实用程序**：资产工作流迁移工具也可以作为独立的实用程序执行。 要了解如何从源安装和构建代码，请参阅 [Git资源： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]  — 工作流迁移](https://github.com/adobe/aem-cloud-migration).
