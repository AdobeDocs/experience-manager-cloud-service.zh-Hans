---
title: 了解计划和计划类型
description: 了解计划和计划类型——云服务
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388

---


# 了解程序和程序类型 {#understanding-programs}

在Cloud manager中，租户实体位于最顶部，其中可包含多个程序。  每个计划最多只能包含一个生产环境和多个非生产环境。

下图显示了Cloud manager中的实体层次结构。

![图像](assets/program-types1.png)

## 计划类型 {#program-types}

用户可以创建 **Sandbox** 或 **Regular程序** 。

通常 *创建沙箱* ，以用于培训、运行演示、启用、POC或文档。 它不能承载实时流量，并且会有常规程序不会受到的限制。 它将包括站点和资产，并将自动填充包含示例代码、开发环境和非生产渠道的Git分支。

会创 *建常规程序* ，以在将来的适当时间启用实时流量。