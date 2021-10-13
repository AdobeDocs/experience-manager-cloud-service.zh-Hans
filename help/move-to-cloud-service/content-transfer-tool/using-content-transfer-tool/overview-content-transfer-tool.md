---
title: 内容传输工具概述
description: 内容传输工具概述
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: f9becda129472f669a4d4511fc158e49be5d34d7
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 58%

---

# 概述 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概述"
>abstract="内容传输工具是由Adobe开发的工具，可用于将现有内容从源AEM实例（内部部署或AMS）移至目标AEM Cloud Service实例。 此工具还会自动传输主体（用户或组）。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="提取流程"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="摄取流程"

内容传输工具是 Adobe 开发的一个工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM 云服务实例。

此工具还会自动传输主体（用户或组）。

## 内容传输工具中的阶段 {#phases-content-transfer-tool}

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关更多详细信息，请参阅[内容传输中的提取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html)。

   >[!NOTE]
   > 建议在提取阶段中运行用户映射工具。 有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html)。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅内容传输中的[摄取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html)。

## 迁移集的属性 {#attributes-migration-set}

迁移集具有以下属性：

* 在内容传输活动期间，一次最多可以创建和维护10个迁移集。
* 每个迁移集应具有唯一的名称。
* 如果迁移集处于非活动状态的时间超过 30 天，则将会自动删除该迁移集。
* 每当您创建迁移集时，它都会与特定环境关联。您只能摄取到同一环境的创作或发布实例中。


内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取阶段，要对现有迁移集进行&#x200B;***增补***，则必须禁用&#x200B;*覆盖*&#x200B;选项。有关更多详细信息，请参阅[增补提取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关更多详细信息，请参阅[增补摄取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process)。

## 下一步 {#whats-next}

了解了内容传输工具及其概述（其中介绍了此工具）后，您便可以使用它将现有内容从源AEM实例（内部部署或AMS）移动到目标AEM Cloud Service实例，您必须查看[内容传输工具的先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)。

