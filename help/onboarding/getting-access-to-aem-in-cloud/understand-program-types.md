---
title: 了解项目和项目类型
description: 了解项目和项目类型——云服务
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# 了解程序和程序类型 {#understanding-programs}

在云管理器中，最上方是租户实体，该实体中可包含多个项目。  每个项目不能包含多个生产环境和多个非生产环境。

下图显示了Cloud Manager中的实体层次结构。

![图像](assets/program-types1.png)

## 项目类型 {#program-types}

用户可以创建沙 **箱** 或常规 **项目** 。

通常 *创建沙箱* ，以用于培训、运行演示、启用、POC或文档。 它不是用于承载实时流量的，并且将具有常规项目不会受到的限制。 它将包括站点和资产，并将自动填充包含示例代码、开发环境和非生产渠道的Git分支。

会 *创建常规项目* ，以在将来的适当时间启用实时流量。