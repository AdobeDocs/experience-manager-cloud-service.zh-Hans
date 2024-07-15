---
title: SLA 报告
description: 了解如何查看生产 AEM 环境相对于约定的服务水平协议 (SLA) 的性能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 54%

---


# SLA 报告 {#sla-reporting}

了解如何查看生产 AEM 环境相对于约定的服务水平协议 (SLA) 的性能。

## 简介 {#introduction}

SLA 报告数据可通过&#x200B;**报告**&#x200B;选项卡用于每个生产程序。请按照以下步骤访问。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 使用侧面导航面板，从&#x200B;**概述**&#x200B;页面导航到&#x200B;**报告**&#x200B;选项卡。

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

## 刷新间隔 {#refresh}

SLA报告使您能够深入了解AEM生产环境的性能，并且是最新的，但不是即时的。 SLA报告生成每月进行一次，对于上个月标记为“生产”的新项目会生成一次。 它不是即时的。 由于此延迟，在查看SLA报告时，请牢记以下事项：

* 报告的SLA将是当月开始时存在的SLA，即使当月SLA发生了更改。
* 如果月初由于程序不存在而没有SLA，则应用创建程序之日存在的SLA。

## 预览环境 {#preview}

预览环境旨在作为内容作者在发布之前验证内容最终体验的工具。 因此，预览环境在设计时没有提供高可用性，也没有相关的SLA。
