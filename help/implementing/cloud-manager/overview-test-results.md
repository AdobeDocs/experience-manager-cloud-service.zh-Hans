---
title: 测试结果概述-Cloud Services
description: 测试结果概述-Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 概述 {#overview}

Cloud Manager为Cloud Services管道支持三类别测试：

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)

   代码质量测试会评估应用程序代码的质量。 代码质量管道在所有非生产和生产管道中紧接构建步骤后执行。

   由云 [管理器执行的](/help/implementing/cloud-manager/custom-code-quality-rules.md) “自定义代码质量规则”是根据AEM Engineering的最佳实践创建的。

1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)

   功能测试是生产管道的阶段测试阶段的一部分。

1. [内容审核测试](/help/implementing/cloud-manager/content-audit-testing.md)

   内容审核测试在所有Cloud Manager生产管道中都处于启用状态，无法跳过。

这些测试可以是：

* 客户写作
* Adobe编写
* 开源工具

   >[!NOTE]
   > 客户编写的测试和Adobe编写的测试都在为运行这些类型的测试而设计的容器化基础架构中运行。

