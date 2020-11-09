---
title: 资产工作流迁移工具
description: '资产工作流迁移工具 '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# 资产工作流迁移工具 {#asset-workflow-migration}

资产工作流迁移工具可用于自动将资产处理工作流从 AEM 的内部部署或 AMS 部署迁移到处理配置文件和 OSGi 配置，以在 AEM Assets as a Cloud Service 中使用。

## 简介 {#introduction}

本节介绍了有关资产工作流迁移工具的资源和实施详细信息。

借助此实用程序，AEM 开发人员可以将现有 AEM 资产处理工作流迁移到 AEM as a Cloud Service。

## 支持的工作流 {#migration-support-for-workflows}

工作流的迁移支持级别各不相同。 查看特 [定工作流的列表](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根据提供的支持，这些工作流分为以下类别。 Adobe支持迁移列在、或 `SUPPORTED`类别 `REQUIRED`中的 `OPTIONAL` 工作流。 不支持其他类别中提及的工作流步骤。

* `SUPPORTED`:支持的 [!DNL Experience Manager Assets] Cloud Service功能。
* `OPTIONAL`:作为Cloud Service [!DNL Experience Manager Assets] 的可选功能。
* `REQUIRED`:添加到工作流的必需步骤。
* `UNNECESSARY`:功能在Cloud Service [!DNL Experience Manager Assets] 中不是必需的。
* `NUI_OOTB`:asset compute服务 [提供的功能](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`:默认连接器提供 [!DNL Dynamic Media] 的功能。
* `NUI_MIGRATED`:已迁移到 [Asset compute服务的处理用户档案](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`:当前不支持 [!DNL Experience Manager Assets] 作为Cloud Service。

## 安装资产工作流迁移工具 {#installing-tool}

请参阅 **[Git 资源：AEM Assets as a Cloud Service - 工作流迁移](https://github.com/adobe/aem-cloud-migration)**，以了解有关通过源安装和构建代码的信息。
