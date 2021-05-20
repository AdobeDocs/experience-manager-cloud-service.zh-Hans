---
title: 测试结果概述 — Cloud Services
description: 测试结果概述 — Cloud Services
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 概述 {#overview}

Cloud Manager支持的Cloud Services管道测试有三大类别：

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   代码质量测试会评估应用程序代码的质量。 在所有非生产和生产管道中，代码质量管道将在构建步骤之后立即执行。

   由Cloud Manager执行的[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)是根据AEM Engineering中的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   功能测试是生产管道阶段测试阶段的一部分。

1. [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)

   体验审核测试在所有Cloud Manager生产管道中都已启用，且无法跳过。

这些测试可以是：

* 客户编写
* Adobe写入
* 开源工具

   >[!NOTE]
   > 客户编写的测试和Adobe编写的测试都在专为运行这些类型测试而设计的容器化基础架构中运行。
