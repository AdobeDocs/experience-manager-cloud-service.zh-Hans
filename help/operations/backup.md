---
title: 在AEMas a Cloud Service中备份和恢复
description: 在AEMas a Cloud Service中备份和恢复
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: eec03acf5d208236ddac338134f95fb3aaa5ee26
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 24%

---


# 在AEMas a Cloud Service中备份和恢复 {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="备份和恢复"
>abstract="AEM as a Cloud Service 可以将客户的完整应用程序（代码和内容）还原到过去七天内特定的预先设定时间，这会替换生产环境中的内容。此功能仅应在代码或内容存在严重问题时使用。所还原备份的时间点与当前时间点之间的最新数据将丢失。暂存内容也将恢复到旧版本。"

如果发生内容或数据损坏，AEM as a Cloud Service可以将客户的完整应用程序（代码和内容）还原到过去七天中的特定预定时间，以替换生产中的内容。
如果客户的部署（即已部署的应用程序代码已损坏或有故障），最好修复它并转到新版本，而不是从备份中恢复它。 备份的执行方式对应用程序的运行时性能没有影响。

>[!CAUTION]
>
>此功能仅应在代码或内容存在严重问题时使用。所还原备份的时间点与当前时间点之间的最新数据将丢失。暂存内容也将恢复到旧版本。

## 使用方法 {#how-to-use}

客户应提交支持票证，描述遇到的问题。 这将导致Adobe支持部门进行调查，调查人员将确定是否需要恢复。

AEMas a Cloud Service支持：

* 用于暂存、生产和开发环境的备份和恢复。
* 24小时时间点恢复，这意味着系统可以在过去24小时内恢复到任何点。
* 从特定的Adobe定义时间戳中恢复过去7天，该时间戳每天使用两次。  任何复制消息（删除、更新、创建）都将保留。

在所有情况下，自定义代码版本都将从恢复点之前的上次成功部署中获取。

恢复时间目标(RTO)可能有所不同，但作为一般准则，恢复顺序平均需要60到90分钟，具体时间取决于多个因素，如存储库大小。 预览环境和多区域发布者可能会延长恢复时间目标。

恢复后，AEM版本将更新为最新版本。

>[!CAUTION]
>
>来自已删除环境的数据将永久丢失且无法恢复。

## 异地备份 {#offsite-backup}

常规备份涵盖AEM云服务中意外删除或技术故障的风险，但也必须涵盖区域故障可能引起的风险。 除了可用性，此类数据区域中断的最大风险主要是数据丢失。
AEM as a Cloud Service通过连续将整个AEM内容复制到远程区域并使其可用于3个月的恢复，将此风险作为所有AEM生产环境的标准。 我们称此功能为“非现场备份”。
在数据区域发生中断时，AEM Service Reliability Engineering会恢复用于暂存和生产环境的AEM云服务。
