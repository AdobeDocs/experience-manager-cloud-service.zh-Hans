---
title: 测试结果概述-Cloud Services
description: 测试结果概述-Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# 概述 {#overview}

云服务的 Cloud Manager 管道执行将支持执行针对暂存环境运行的测试。这与在构建和单元测试步骤中运行的测试相反，这些测试在脱机状态下运行，无法访问任何正在运行的AEM环境。

Cloud Manager为Cloud Services管道支持三类别测试：

1. [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)
1. [功能测试](/help/implementing/cloud-manager/functional-testing.md)
1. [内容审核测试](/help/implementing/cloud-manager/content-audit-testing.md)

这些测试可以是：

* 客户写作
* Adobe编写
* 开放源码工具（由Google的Lighthouse提供支持）

   >[!NOTE]
   > 客户编写的测试和Adobe编写的测试都在为运行这些类型的测试而设计的容器化基础架构中运行。

