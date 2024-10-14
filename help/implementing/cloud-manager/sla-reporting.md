---
title: SLA 报告
description: 了解如何查看生产AEM环境相对于签订的服务水平协议的性能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 13%

---


# SLA 报告 {#sla-reporting}

了解如何查看生产AEM环境相对于签订的SLA（服务级别协议）的性能。

## 查看SLA报表 {#introduction}

SLA报表数据跟踪两个生产层的性能指标：创作层和Publish层。

选定年份的折线图包括从1月至12月的每月数据点。 将跟踪以下量度。

| 跟踪的量度 | 线条颜色 | 描述 |
| --- | --- | --- |
| 作者层实际情况 | 浅绿色 | 测量出的由Adobe或Adobe供应商引起的生产创作层保理事件的正常运行时间。 |
| 作者层合同 | 深蓝色 | 您与Adobe签订的合同中为创作层定义的SLA。 |
| 发布层实际情况 | 橙色 | 测量的Publish生产层的正常运行时间，由Adobe或Adobe供应商引起的保理事件。 |
| 发布层合同 | 红色 | 您与Adobe公司签订的合同中为Publish层定义的SLA。 |

**查看SLA报告：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**项目概述**&#x200B;页面的左侧菜单中，单击&#x200B;**报告**。

1. 单击&#x200B;**SLA报表**。

   ![SLA报告线形图](/help/implementing/cloud-manager/assets/cm-sla-report.png)

1. 单击所需的年份以查看SLA数据的折线图。

1. （可选）执行以下任一操作：

   * 将光标滚动到折线图中的数据点上，以显示该点的特定值。
   * 在折线图的年份下方，单击下载图标以保存折线图的PNG图像文件。
   * 单击某个指标名称可仅查看该指标的数据。 或者，在选择或取消选择一个或多个量度名称时按键盘上的`Shift`。

   ![显示详细数据](/help/implementing/cloud-manager/assets/cm-sla-download.png)

## 事件分析 {#event-analysis}

此图表下的&#x200B;**事件分析**&#x200B;部分显示在选定年份中发生的与项目相关的事件集。

每个事件均具有一个时间范围、一个原因和一组注释。

![事件分析示例](assets/sla-reporting-c.png)

## 刷新SLA报表的时间间隔 {#refresh}

SLA报表可让您深入了解AEM生产环境的性能，并且是最新的，但不是即时的。 SLA报表生成每月进行，并且为标记为`Production previous month`的新程序生成。 它不是即时的。 由于此延迟，在查看SLA报表时，请牢记以下事项：

* 报告的SLA是本月初存在的报表，即使SLA在该月发生了更改。
* 如果月初由于程序不存在而没有SLA，则创建程序之日存在的SLA适用。

## 预览环境 {#preview}

预览环境旨在作为内容作者在发布之前验证内容最终体验的工具。 由于此功能，预览环境在设计时没有提供高可用性，因此没有相关的SLA。
