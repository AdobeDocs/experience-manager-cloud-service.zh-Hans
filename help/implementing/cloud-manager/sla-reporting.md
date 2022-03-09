---
title: SLA 报告
description: 了解如何查看生产AEM环境相对于已签订合同的服务级别协议(SLA)的性能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# SLA 报告 {#sla-reporting}

了解如何查看生产AEM环境相对于已签订合同的服务级别协议(SLA)的性能。

## 简介 {#introduction}

SLA报告数据可通过 **报表** 选项卡。 请按照以下步骤访问。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **报表** 选项卡 **概述** 页面。

1. 单击所需的年份，以查看绘制的SLA数据图。

![SLA图示例](assets/sla-reporting-1.png)

将光标置于数据点上以显示该点的特定值。

![显示详细数据](assets/sla-reporting-b.png)

## SLA量度 {#sla-metrics}

选定年份的图表包含许多数据集。

* **发布层合同**  — 这是您与发布层Adobe签订的合同中定义的SLA。

* **发布层实际**  — 这是由Adobe或Adobe供应商导致的生产发布层保理事件的正常运行时间。

* **创作层合同**  — 这是您与创作层Adobe签订的合同中定义的SLA。

* **创作层实际值**  — 这是由Adobe或Adobe供应商导致的生产创作层保理事件的正常运行时间。

## 事件分析 {#event-analysis}

的 **事件分析** 图表下的部分显示选定年份中针对该程序发生的事件集。

每个事件都有一个时间范围、原因和一组评论。

![事件分析示例](assets/sla-reporting-c.png)
