---
title: Cloud Manager测试概述
description: 获取Cloud Manager自动运行的三种测试类型的概述，以确保自定义代码的质量。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---


# Cloud Manager测试概述 {#overview}

Cloud Manager支持三种类别的Cloud Services管道测试。

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   * 代码质量测试会评估应用程序代码的质量。
   * 在所有非生产和生产管道中，代码质量管道将紧随构建步骤执行。
   * 的 [自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md) 由Cloud Manager执行的操作是根据AEM Engineering中的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   * 功能测试是生产管道阶段测试阶段的一部分。

1. [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 体验审核测试在所有Cloud Manager生产管道中都已启用，并且无法跳过。

这些测试可以是：

* 客户编写
* Adobe写入
* 使用开源工具创建

>[!NOTE]
>
> 客户编写的测试和Adobe编写的测试均在专为运行此类测试而设计的容器化基础架构中运行。
