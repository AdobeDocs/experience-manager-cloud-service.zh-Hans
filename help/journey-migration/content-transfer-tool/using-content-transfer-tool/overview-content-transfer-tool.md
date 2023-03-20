---
title: 内容传输工具概述
description: 内容传输工具概述
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: ac35bbe5ad78e07cc5292e089f3d71c6a8ed6ccc
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 79%

---

# 概述 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概述"
>abstract="内容传输工具是 Adobe 开发的一项工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例。此工具还会自动传输主体（用户或组）。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="准则和最佳实践"

内容传输工具是 Adobe 开发的一个工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例。

此工具还会自动传输主体（用户或组）。

已提供新版本的内容传输工具，它将内容传输过程与 Cloud Acceleration Manager 集成。强烈建议切换到此新版本，充分利用其所有优势。

* 一次性提取迁移集并将它并行摄取到多个环境中的自助方式
* 通过更好的加载状态、防护机制和错误处理改善用户体验
* 摄取日志将保留，并且始终可用于进行故障排除

要开始使用新版本，您需要卸载旧版本的内容传输工具，因为该工具的架构发生了重大更改。

>[!NOTE]
>
> 对于正在进行迁移的情况，您可以继续使用早期版本的 CTT，直到迁移完成。有关与早期版本的 CTT 相关的文档，请参阅[旧版文档](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md)。

## 内容传输工具中的阶段 {#phases-content-transfer-tool}

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关更多详细信息，请参阅[内容传输中的提取流程](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)。

   >[!NOTE]
   >用户映射现在作为创作提取阶段的一部分自动运行（但可以选择在创作时禁用，或在发布时启用）。 请参阅 [用户映射和主迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) 以了解更多详细信息。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)。

## 迁移集的属性 {#attributes-migration-set}

迁移集具有以下属性：

* 利用新版本，您可以在 Cloud Acceleration Manager 中创建的项目中创建最多五个迁移集。
* 每个迁移集应具有唯一的名称。

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取阶段，要对现有迁移集进行&#x200B;***增补***，则必须禁用&#x200B;*覆盖*&#x200B;选项。有关更多详细信息，请参阅[增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关更多详细信息，请参阅[增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)。

## 迁移集到期 {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="迁移集的到期"
>abstract="了解迁移集的到期。"

所有迁移集在长时间不活动约90天后最终会过期。 在一段时间内，在项目卡和迁移作业表行中显示指示器后，迁移集将过期，其数据将不再可用。 通过执行迁移集，可以轻松延长到期时间：

* 编辑其描述
* 获取提取密钥
* 对其执行提取
* 从中执行摄取

可以在迁移集行上监控迁移集的到期情况。 此外，还添加了项目卡片，以显示迁移集即将到达其过期日期的有用可视化指示。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## 后续内容 {#whats-next}

在您了解内容传输工具并查看其概述（描述此工具可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例）后，您必须查看[内容传输工具的先决条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)。
