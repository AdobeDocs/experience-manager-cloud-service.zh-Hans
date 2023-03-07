---
title: 内容传输工具概述
description: 内容传输工具概述
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 8a55e011a93ce069f067192f58bd36399a39130b
workflow-type: ht
source-wordcount: '627'
ht-degree: 100%

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

   有关更多详细信息，请参阅[内容传输中的提取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html)。

   >[!NOTE]
   > 建议在提取阶段运行用户映射工具。有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html)。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html)。

## 迁移集的属性 {#attributes-migration-set}

迁移集具有以下属性：

* 利用新版本，您可以在 Cloud Acceleration Manager 中创建的项目中创建最多五个迁移集。
* 每个迁移集应具有唯一的名称。

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取阶段，要对现有迁移集进行&#x200B;***增补***，则必须禁用&#x200B;*覆盖*&#x200B;选项。有关更多详细信息，请参阅[增补提取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关更多详细信息，请参阅[增补摄取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process)。

## 后续内容 {#whats-next}

在您了解内容传输工具并查看其概述（描述此工具可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例）后，您必须查看[内容传输工具的先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)。
