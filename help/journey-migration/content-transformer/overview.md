---
title: 内容转换器概述
description: 了解如何使用内容转换器检测和修复BPA报告的内容相关问题。
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# 概述 {#overview-ct}

Content Transformer (CT)是由Adobe开发的工具，可用于在将内容从当前的AEM实施(内部部署或Managed Services)迁移到AEM as a Cloud Service之前，自动检测和修复[最佳实践分析器(BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)报告的内容相关问题。

通过允许用户执行批量操作，例如移动或删除，内容转换器可帮助解决属于以下[BPA模式类别](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)（如下表所示）的问题。 这可以显着减少与迁移项目相关的时间并降低复杂性。

## 内容转换器涵盖的模式类别和建议的解决方案 {#pattern-categories-and-benefits}

| 图案代码 | 可疑类型/子类型 | 在将内容迁移到AEM as a Cloud Service之前的潜在修复 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | 将这些资源移动到其他位置或删除它们，以确保它们未迁移到AEM as a Cloud Service。 |
| CAV | content.area.violation | 将路径临时移动到`/etc/packages/content-transformation/paths`以确保它们未迁移到AEM as a Cloud Service。 |
| DOPI | deprecated.ordered.index | 删除已弃用的索引。 |
| OAUI | non.migrated.oauth.users | 请删除这些用户，以确保他们不会迁移到AEM as a Cloud Service。 |
| PCX | page.complexity.medium <br> page.complexity.high | 删除页面/子页面，或将它们移动到其他位置，以确保它们未迁移到AEM as a Cloud Service。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | 删除已创建的复制代理。 <br>或<br>删除修改/添加的属性。 |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | 移到正确的位置，以避免迁移期间出现问题。 |
| URS | node.size | 将节点临时移动到`/etc/packages/content-transformation/paths`以确保它们未迁移到AEM as a Cloud Service。 |

## 内容转换器提供的优势 {#benefits}

内容转换器提供以下优势：

* 故障保护：内容转换器每次对存储库进行修改以修复问题时，都会创建一个包。 如果需要，可以通过安装包恢复到以前的状态。
* 易于使用： Content Transformer已与Content Transfer Tool集成，并附带简单直观的用户界面。
* 节省时间：当大量内容问题属于一种模式类别时，您可以通过多次单击内容转换器来解决所有问题。
