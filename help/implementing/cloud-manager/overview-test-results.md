---
title: Cloud Manager 测试概述
description: 概述 Cloud Manager 自动运行的三种类型的测试，确保自定义代码的质量。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 100%

---


# Cloud Manager 测试概述 {#overview}

Cloud Service 管道的 Cloud Manager 支持三类测试。

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   * 代码质量测试评估应用程序代码的质量。
   * 代码质量管道在所有非生产和生产管道中的构建步骤之后立即执行。
   * 由 Cloud Manager 执行的[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)是根据 AEM Engineering 的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   * 功能测试是[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)的阶段测试阶段的一部分，也是[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)的测试阶段的可选部分。

1. [体验审核测试](/help/implementing/cloud-manager/experience-audit-dashboard.md)

   * 体验审核测试已在所有 Cloud Manager 生产管道中启用，无法跳过。

这些测试可以是：

* 客户编写
* Adobe 编写
* 使用开源工具创建

>[!NOTE]
>
> 客户编写的测试和 Adobe 编写的测试都在专为运行此类测试而设计的容器化基础架构中运行。
