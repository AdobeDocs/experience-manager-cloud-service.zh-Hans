---
title: 重构工具概述
description: 了解如何使用AEM重构工具
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="Guidelines and Best Practices"

-->

# 重构工具概述 {#refactoring-tools-overview}

**重构工具**&#x200B;简化了更新现有AEM项目以使其与&#x200B;**AEM as a Cloud Service (AEMaaCS)**&#x200B;兼容的流程。 这些工具可自动执行常见的重构和现代化任务，并与&#x200B;**Cloud Acceleration Manager (CAM)**&#x200B;集成以实现无缝体验。

重构工具以前仅作为CLI实用程序提供，现在可提供具有自动检查、配置生成和作业执行等功能的统一界面 — 减少手动开销并提高可见性。

## 检查工作流 {#inspection-workflow}

**检查工作流**&#x200B;简化了运行重构工具的准备过程。

### 主要功能：

* **自动触发器** — 上传项目会自动开始检查。
* **配置生成** — 工具将检查上传的源代码，并生成必要的配置。
* **有效负载提交** — 这些配置将直接传递到所选工具以供执行。

## 可用的重构工具

### 存储库现代化器 {#repo-modernizer}

**存储库现代化器**&#x200B;重新构建您的AEM项目的存储库布局和内容，以符合AEMaaCS标准和最佳实践。 它以增强的自动化和准确性取代了旧版存储库现代化工具。

### 代码转换器 {#code-transformer}

**代码转换器**&#x200B;使用智能模式识别和AI驱动的分析来检测和更新与AEMaaCS不兼容的代码段。 此工具可简化迁移工作并减少手动代码更改。

## 重构工作流阶段 {#phases-in-refactoring-tools}

重构工具遵循结构化的两阶段流程：

### 第1阶段：上传Source代码

* 使用CAM界面上载源代码（ZIP格式）。
* 上传后，将自动触发&#x200B;**检查工作流**&#x200B;以分析项目并准备工具执行。

>[!NOTE]
>在检查过程中，不允许上传其他项目。

### 阶段2：触发重构作业

成功检查后，可以运行一个或多个重构工具：

* **运行存储库现代化器** — 执行存储库现代化。
* **运行代码转换器** — 根据检查输出运行代码转换。
* **一起运行所有工具** — 在单个操作中执行所有可用的工具。

>[!NOTE]
>只有在成功上传并检查源代码后，才能启动重构作业。

>[!NOTE]
>用户可以并行触发多个重构作业，但每个作业将单独执行。
