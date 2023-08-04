---
title: AEMas a Cloud Service中的备份和恢复
description: 了解AEMas a Cloud Service中的备份和恢复
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 24%

---


# AEMas a Cloud Service中的备份和恢复 {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="备份和恢复"
>abstract="AEM as a Cloud Service 可以将客户的完整应用程序（代码和内容）还原到过去七天内特定的预先设定时间，这会替换生产环境中的内容。此功能仅应在代码或内容存在严重问题时使用。该过程失去还原的备份所处的时刻与当前之间的最新数据。暂存内容也会恢复到旧版本。"

如果发生内容或数据损坏，AEMas a Cloud Service可以恢复客户的完整应用程序（代码和内容）。 过去7天内，它将恢复到预先确定的特定时间，以替换生产环境。
如果客户的部署（这意味着部署的应用程序代码已损坏或出错），则最好修复该代码并将其前滚到新版本中，而不是从备份中恢复该代码。 执行备份的方式不会影响应用程序的运行时性能。

>[!CAUTION]
>
>此功能仅应在代码或内容存在严重问题时使用。该过程失去还原的备份所处的时刻与当前之间的最新数据。暂存内容也会恢复到旧版本。

## 使用方法 {#how-to-use}

客户应提交支持工单，描述所遇到的问题。 支持工单通常会导致Adobe支持进行调查，然后用户可以确定是否需要恢复。

AEMas a Cloud Service支持：

* 用于暂存、生产和开发环境的备份和恢复。
* 24小时时间点恢复，这意味着系统可以恢复到过去24小时内的任何时间点。
* 从过去7天内Adobe定义的特定时间戳每天执行两次恢复。 任何复制消息（删除、更新、创建）都会被保留。

在所有情况下，自定义代码版本都是从还原点之前的上次成功部署中获取的。

恢复时间目标(RTO)可能有所不同，但作为一般准则，恢复顺序平均需要60到90分钟，具体取决于多种因素，如存储库大小。 预览环境和多区域发布者可能会延长恢复时间目标。

恢复后，AEM版本将更新为最新版本。

>[!CAUTION]
>
>来自已删除环境的数据将永久丢失且无法恢复。

## 异地备份 {#offsite-backup}

虽然常规备份涵盖AEM Cloud Service中意外删除或技术故障的风险，但还必须涵盖因区域故障而引发的风险。 除了可用性之外，此类数据区域中断的最大风险主要是数据丢失。
AEMas a Cloud Service会将此风险作为所有AEM生产环境的标准来涵盖。 它连续将整个AEM内容复制到远程区域，并让该内容在三个月内可用于恢复。 Adobe将此功能称为“异地备份”。
如果数据区域发生中断，则AEM Service Reliability Engineering会执行用于暂存和生产环境的AEM Cloud Service的恢复。
