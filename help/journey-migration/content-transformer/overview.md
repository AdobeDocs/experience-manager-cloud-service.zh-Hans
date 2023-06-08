---
title: 内容转换器概述
description: 内容转换器概述
source-git-commit: 55eedd342f048e19bad5c6fbfdd16a468ff1f4f9
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---

# 概述 {#overview-ct}

Content Transformer (CT)是由Adobe开发的一个工具，可用于自动检测和修复由以下组件报告的内容相关问题 [Best Practices Analyzer (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 在将内容从当前AEM实施(内部部署或Managed Services)迁移到AEMas a Cloud Service之前。

内容转换器可帮助解决以下问题 [BPA模式类别](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html) （如下表所示），允许用户执行批量操作，例如移动或删除。 这可以显着减少与迁移项目相关的时间并降低复杂性。

## 内容转换器涵盖的模式类别和建议的解决方案 {#pattern-categories-and-benefits}

| 图案代码 | 可疑类型/子类型 | 在将内容迁移到AEMas a Cloud Service之前可能会进行的修复 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | 将这些资源移动到其他位置或删除它们，以确保它们不会迁移到AEMas a Cloud Service。 |
| CAV | content.area.violation | 将路径临时移动到 `/etc/packages/content-transformation/paths` 以确保它们不会迁移到AEMas a Cloud Service。 |
| DOPI | deprecated.ordered.index | 删除已弃用的索引。 |
| OAUI | non.migrated.oauth.users | 请删除这些用户，以确保他们不会迁移到AEMas a Cloud Service。 |
| PCX | page.complexity.medium <br> page.complexity.high | 删除页面/子页面，或将其移动到其他位置，以确保它们不会迁移到AEMas a Cloud Service。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modifiation <br> custom.replication.agent.detection | 删除新创建的复制代理。 <br> 或 <br> 删除修改/添加的属性。 |
| URS | clientlibs.location <br> 文件位置 <br> node.location <br> 工作流程位置 | 移到正确的位置，以避免迁移期间出现问题。 |
| URS | node.size | 将节点临时移动到`/etc/packages/content-transformation/paths` 以确保它们不会迁移到AEMas a Cloud Service。 |

## 内容转换器提供的优势 {#benefits}

内容转换器提供以下优势：

* 故障保护：内容转换器每次对存储库进行修改以修复问题时，都会创建一个包。 如果需要，可以通过安装包恢复为以前的状态。
* 易于使用： Content Transformer已与Content Transfer Tool集成，并带有直观的简单用户界面。
* 节省时间：当大量内容问题属于一个模式类别时，只需点击几下即可使用内容转换器解决所有问题。
