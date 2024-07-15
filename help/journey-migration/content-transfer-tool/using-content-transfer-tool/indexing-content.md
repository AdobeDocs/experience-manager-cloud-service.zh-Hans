---
title: 迁移内容后建立索引
description: 了解迁移过程将如何对目标Cloud Service实例上的摄取内容进行索引。
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 9%

---

# 迁移内容后建立索引 {#Indexing-content}

## 索引 {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="内容索引"
>abstract="AEM 索引是指将内容迁移到 Cloud Service 实例后为 Cloud Service 实例上的内容编制索引。需要编制索引以支持搜索该实例上的内容。"

在Cloud Acceleration Manager完成将内容摄取到Cloud Service实例中后，便可以使用它。 最初，内容未编入索引，这可能会导致环境不稳定，出现不可搜索的内容和性能下降等问题。 为获得实例上的最佳性能，迁移过程将自动开始索引内容。 除了监视索引进度外，没有其他可执行的操作。

> 有关如何开始引入的信息，请参阅[将内容引入到Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)。

以下步骤显示了索引期间可在UI中看到的一般流程。 某些标签在工具提示中提供有用的上下文，因此请确保将鼠标悬停在项目上以了解有关当前索引状态的更多信息。

首先，转到Cloud Acceleration Manager。 单击项目信息卡，然后单击内容传输信息卡。 导航到&#x200B;**引入作业**&#x200B;并查看列出的作业。

>[!NOTE]
>您可以通过引入作业的操作，使用……下拉列表查看或下载索引日志。 日志将位于
> 索引作业完成后，“索引日志”操作部分

### 待处理

这是摄取运行时在索引作业开始之前摄取作业行的显示方式。 无需用户执行任何操作。 如果摄取由于任何原因失败，则索引作业的队列将被取消而不是开始。

![图像](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### 正在运行

摄取成功后，索引作业将自动启动。 摄取作业行将显示AEM索引状态的进度图标。 您可以打开持续时间对话框以查看作业进度。

![图像](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### 完成

当索引作业成功时，实例已准备好以最佳性能使用。 此时，索引作业日志可供查看或下载以进行检查。

![图像](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### 错误数

对目标Cloud Service实例编制索引很可能成功。 在某些情况下，该操作可能会失败，并且引入作业行将如下所示。 在所有情况下，都可以通过将鼠标悬停在故障状态上来查找故障的一些详细信息，这些信息可能会帮助您确定后续步骤。 此时，索引作业日志可供查看或下载，以帮助发现故障源。 如果下一个步骤不明确，请联系Adobe支持并提供摄取和索引日志的详细信息。

>[!TIP]
>
> 列入允许列表如果索引作业运行时间过长，请确保未通过Cloud Manager应用[IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)，因为它会阻止Cloud Acceleration Manager访问迁移服务。

![图像](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## 后续内容 {#whats-next}

对目标云服务实例编制索引后，您可以查看索引作业的日志并查找详细信息和错误。

迁移完成。 可以开始测试和验证目标云服务实例。
