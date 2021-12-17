---
title: 准备阶段
description: 准备阶段
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 87%

---

# 就绪 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="规划过渡"
>abstract="在开始过渡到 Cloud Service 的历程之前，您应该熟悉 AEM as a Cloud Service，并查看已对它所做的显著更改以及已替换或已弃用的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

在开始过渡到 Cloud Service 的历程之前，您应该熟悉 AEM as a Cloud Service，并查看已对它所做的显著更改以及已替换或已弃用的功能。

## 显著更改 {#notable-changes}

AEM as a Cloud Service 为管理 AEM 项目提供了许多新功能和可能性。

但是，与 AEM as a Cloud Service 相比，内部部署版或 Adobe Managed Service 中的 AEM 存在很大差异。

请参阅 [对 AEM 云服务的显著更改](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html)，以了解重要差异。

## 已弃用功能 {#deprecated-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

请参阅[已弃用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features)，以了解有关在 Experience Manager as a Cloud Service 中标记为已弃用的特性和功能的更多信息。

## 了解规划阶段 {#introduction}

下图显示了“规划”阶段所包含的关键步骤：

![图像](/help/journey-migration/assets/planning-phaseimg1.png)

### 评估云服务准备情况 {#access-cloud-readiness}

规划阶段的第一步就是评估您对从现有 AEM 版本移动到 Cloud Service 的准备情况，并确定需要重构才能与 AEM as a Cloud Service 兼容的区域。

您需要根据显著更改和已弃用功能对当前 AEM 源代码进行全面评估，以确定过渡历程中预期的工作量。

您可以通过在当前AEM版本上运行最佳实践分析器来加快评估步骤。 有关更多详细信息，请参阅 [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

>[!NOTE]
>如果您已经有权访问 Cloud Manager 和云服务环境，则建议在 Cloud Manager 代码质量管道中运行当前代码，以评估与云服务兼容所需的代码更改。

### 审查资源计划 {#review-resource-planning}

评估了移动到云服务所需的工作量后，您应该确定资源，创建团队并针对过渡旅程规划角色和职责。

### 建立 KPI {#establish-kpis}

如果您以前尚未建立关键绩效指标 (KPI)，则建议为 Adobe Experience Manager (AEM) 实施建立 KPI，以帮助团队专注于最重要的事情。

请参阅[制定 KPI](https://guided.adobe.com/welcome/aem/part6.html)，以了解如何为您的业务目标选择恰当的 KPI。
