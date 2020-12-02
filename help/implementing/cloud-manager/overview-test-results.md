---
title: 测试结果概述-Cloud Services
description: 测试结果概述-Cloud Services
translation-type: tm+mt
source-git-commit: d03ef0afe91760e35ef4e8fb3e3f2c833cbf945c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 概述 {#overview}

Cloud Manager为Cloud Services管道支持三类别测试：

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   代码质量测试会评估应用程序代码的质量。 代码质量管道在所有非生产和生产管道中紧接构建步骤后执行。

   由云管理器执行的[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)是根据AEM工程的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   功能测试是生产管道的阶段测试阶段的一部分。

1. [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)

   Experience Audit Testing已在所有Cloud Manager Production Pipeline中启用，无法跳过。

这些测试可以是：

* 客户写作
* Adobe编写
* 开源工具

   >[!NOTE]
   > 客户编写的测试和Adobe编写的测试都在为运行这些类型的测试而设计的容器化基础架构中运行。

