---
title: SLA 报告
description: 了解如何查看生产 AEM 环境相对于约定的服务水平协议 (SLA) 的性能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 91%

---


# SLA 报告 {#sla-reporting}

了解如何查看生产 AEM 环境相对于约定的服务水平协议 (SLA) 的性能。

## 简介 {#introduction}

SLA 报告数据可通过&#x200B;**报告**&#x200B;选项卡用于每个生产程序。请按照以下步骤访问。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**报告**&#x200B;选项卡。

1. 单击所需的年份以查看绘制的SLA数据。

![SLA 图形示例](assets/sla-reporting-1.png)

将光标滚动到数据点上，显示该点的特定值。

![显示详细数据](assets/sla-reporting-b.png)

## SLA 量度 {#sla-metrics}

选定年份的图表包括几个数据集。

* **发布层合同** – 这是您与 Adobe 签订的合同中为发布层定义的 SLA。

* **实际发布层** – 这是测量出的由 Adobe 或 Adobe 供应商引起的生产发布层保理事件的正常运行时间。

* **作者层合同** – 这是您与 Adobe 签订的合同中为创作层定义的 SLA。

* **实际作者层** – 这是测量出的由 Adobe 或 Adobe 供应商引起的生产作者层保理事件的正常运行时间。

## 事件分析 {#event-analysis}

此图表下的&#x200B;**事件分析**&#x200B;部分显示在选定年份中发生的与项目相关的事件集。

每个事件均具有一个时间范围、一个原因和一组注释。

![事件分析示例](assets/sla-reporting-c.png)
