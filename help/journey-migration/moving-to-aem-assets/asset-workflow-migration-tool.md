---
title: 资产工作流迁移工具
description: 资产工作流迁移工具
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 30%

---

# 资产工作流迁移工具 {#asset-workflow-migration}

资产工作流迁移工具可用于自动将资产处理工作流从 AEM 的内部部署或 AMS 部署迁移到处理配置文件和 OSGi 配置，以在 AEM Assets as a Cloud Service 中使用。

## 简介 {#introduction}

本节介绍了有关资产工作流迁移工具的资源和实施详细信息。

借助此实用程序，AEM 开发人员可以将现有 AEM 资产处理工作流迁移到 AEM as a Cloud Service。

## 支持的工作流 {#migration-support-for-workflows}

这些工作流支持的迁移级别各不相同。 查看此[特定工作流列表](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根据提供的支持，这些工作流分为以下类别。 Adobe支持迁移`SUPPORTED`、`REQUIRED`或`OPTIONAL`类别中列出的工作流。 不支持其他类别中提到的工作流步骤。

* `SUPPORTED`： [!DNL Experience Manager Assets]as a Cloud Service支持的功能。
* `OPTIONAL`： [!DNL Experience Manager Assets]as a Cloud Service中的可选功能。
* `REQUIRED`：添加到工作流的必需步骤。
* `UNNECESSARY`： [!DNL Experience Manager Assets]as a Cloud Service中不需要功能。
* `NUI_OOTB`： [Asset compute服务](/help/assets/asset-microservices-configure-and-use.md)提供的功能。
* `DMS7_OOTB`：默认提供[!DNL Dynamic Media]连接器的功能。
* `NUI_MIGRATED`：已迁移到Asset compute服务](/help/assets/asset-microservices-configure-and-use.md)的[处理配置文件。
* `UNSUPPORTED`： [!DNL Experience Manager Assets]as a Cloud Service当前不支持。

## 使用资产工作流迁移工具 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**：Adobe建议通过`aio-cli-plugin-aem-cloud-service-migration`使用资产工作流迁移工具（[!DNL Experience Manager]作为[!DNL Adobe I/O] CLI的[!DNL Cloud Service]代码重构插件）。 要了解如何安装和使用插件，请参阅[Git资源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)。

* **独立实用程序**：资产工作流迁移工具也可以作为独立实用程序执行。 要了解如何从源安装和生成代码，请参阅[Git资源： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]  — 工作流迁移](https://github.com/adobe/aem-cloud-migration)。
