---
title: 资产工作流迁移工具
description: 资产工作流迁移工具
exl-id: 18490295-ead6-4691-8983-a6d4054e4264
source-git-commit: a0fb2714bc74c620d90153746930757301e62fd7
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 29%

---

# 资产工作流迁移工具 {#asset-workflow-migration}

资产工作流迁移工具可用于自动将资产处理工作流从 AEM 的内部部署或 AMS 部署迁移到处理配置文件和 OSGi 配置，以在 AEM Assets as a Cloud Service 中使用。

## 简介 {#introduction}

本节介绍了有关资产工作流迁移工具的资源和实施详细信息。

借助此实用程序，AEM 开发人员可以将现有 AEM 资产处理工作流迁移到 AEM as a Cloud Service。

## 支持的工作流{#migration-support-for-workflows}

工作流具有不同级别的迁移支持。 请参阅此[特定工作流的列表](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根据提供的支持，工作流分为以下类别。 Adobe支持迁移`SUPPORTED`、`REQUIRED`或`OPTIONAL`类别中列出的工作流。 不支持其他类别中提及的工作流步骤。

* `SUPPORTED`:支持的 [!DNL Experience Manager Assets] 作为Cloud Service。
* `OPTIONAL`:中的可选 [!DNL Experience Manager Assets] 功能作为Cloud Service。
* `REQUIRED`:添加到工作流的必需步骤。
* `UNNECESSARY`:在中，作为Cloud Service [!DNL Experience Manager Assets] 不需要功能。
* `NUI_OOTB`:asset compute服务 [提供的功能](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`:默认连接器提供 [!DNL Dynamic Media] 的功能。
* `NUI_MIGRATED`:已迁移到 [Asset compute服务的处理配置文件](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`:当前不支持 [!DNL Experience Manager Assets] 作为Cloud Service。

## 使用资产工作流迁移工具{#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**:Adobe建议通过使用资产工作流迁移 `aio-cli-plugin-aem-cloud-service-migration` 工具([!DNL Experience Manager] 作为 [!DNL Cloud Service] CLI的代码重构插 [!DNL Adobe I/O] 件)。要了解如何安装和使用插件，请参阅[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)。

* **独立实用程序**:资产工作流迁移工具也可以作为独立实用程序执行。要了解如何从源安装和构建代码，请参阅&#x200B;**[Git资源： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]  — 工作流迁移](https://github.com/adobe/aem-cloud-migration)**。
