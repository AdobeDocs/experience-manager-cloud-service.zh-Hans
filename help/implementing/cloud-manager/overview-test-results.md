---
title: Cloud Manager 测试概述
description: 概述 Cloud Manager 自动运行的三种类型的测试，确保自定义代码的质量。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 94f818b7622e0f878d15ba30e2f07a169bd114c3
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 85%

---


# Cloud Manager 测试概述 {#overview}

Cloud Service 管道的 Cloud Manager 支持三类测试。

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   * 代码质量测试评估应用程序代码的质量。
   * 代码质量管道在所有非生产和生产管道中的构建步骤之后立即执行。
   * 由 Cloud Manager 执行的[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)是根据 AEM Engineering 的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   * 功能测试是 [生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [非生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 体验审核测试已在所有 Cloud Manager 生产管道中启用，无法跳过。

这些测试可以是：

* 客户编写
* Adobe 编写
* 使用开源工具创建

>[!NOTE]
>
> 客户编写的测试和 Adobe 编写的测试都在专为运行此类测试而设计的容器化基础架构中运行。
