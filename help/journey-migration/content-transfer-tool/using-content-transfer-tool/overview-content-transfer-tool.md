---
title: 内容传输工具概述
description: 了解如何使用内容传输工具将内容从内部部署AEM实例传输到AEM as a Cloud Service
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
feature: Migration
role: Admin
source-git-commit: e73933acc3ff23d1456f03b288f2f842a6289ace
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 56%

---


# 概述 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概述"
>abstract="内容传输工具是 Adobe 开发的一个工具，可用于启动从源 AEM 实例（内部部署或 AMS）到目标 AEM Cloud Service 实例的现有内容迁移。这个工具也会自动转移群组。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="准则和最佳实践"

内容传输工具是由Adobe开发的工具，可用于启动将现有内容从源AEM实例（内部部署或AMS）迁移到目标AEM Cloud Service实例。

此工具还会自动传输组。  有关详细信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

内容传输工具将内容传输过程与Cloud Acceleration Manager集成在一起。 这使用户能够获得它提供的所有好处：

* 一次性提取迁移集并将它并行摄取到多个环境中的自助方式
* 通过更好的加载状态、护栏和错误处理改善用户体验
* 摄取日志将保留，并且始终可用于进行故障排除
* 验证和主体迁移报告均可用于验证

## 内容传输工具中的阶段 {#phases-content-transfer-tool}

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关详细信息，请参阅内容传输中的[提取流程](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)。

## 迁移集的属性 {#attributes-migration-set}

迁移集具有以下属性：

* 使用新版本，您可以在Cloud Acceleration Manager中创建的项目中最多创建10个迁移集。
* 每个迁移集应具有唯一的名称。

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取阶段，要对现有迁移集进行&#x200B;***增补***，则必须禁用&#x200B;*覆盖*&#x200B;选项。有关详细信息，请参阅[增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关详细信息，请参阅[增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)。

## 迁移集到期 {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="迁移集的到期"
>abstract="了解迁移集的到期。"

所有迁移集将在长时间不活动约45天后最终过期。 在项目信息卡和迁移作业表行上显示指示符一段时间后，迁移集将过期，并且其数据将不再可用。 通过以下方式根据迁移集执行操作，可以轻松延长到期时间：

* 编辑其描述
* 获取其提取密钥
* 对其执行提取
* 从中执行引入

可以在“迁移集”行上监视迁移集的到期情况。 此外，还添加了项目的信息卡，这是一个有用的视觉标志，表明迁移集即将到期。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)

## 后续内容 {#whats-next}

在您了解内容传输工具并查看其概述（描述此工具可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例）后，您必须查看[内容传输工具的先决条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)。
