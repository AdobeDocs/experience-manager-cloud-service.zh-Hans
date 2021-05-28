---
title: 在AEM as aCloud Service中备份和还原
description: 在AEM as aCloud Service中备份和还原
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 在AEM as aCloud Service中备份和还原


>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="备份和恢复"
>abstract="AEM as aCloud Service可以将客户的完整应用程序（代码和内容）还原到过去七天中特定的预定时间，从而替换生产环境。 仅当代码或内容存在严重问题时，才应使用此功能。 从还原备份到当前备份之间的最近数据将丢失。 暂存版本也将还原到旧版本。"

如果发生内容或数据损坏，AEM as aCloud Service可以将客户的完整应用程序（代码和内容）还原到过去七天中的特定预定时间，以替换生产中的内容。
如果客户的部署（即已部署的应用程序代码已损坏或有故障），最好修复它并转到新版本，而不是从备份中恢复它。 备份的执行方式对应用程序的运行时性能没有影响。

>[!CAUTION]
>
>仅当代码或内容存在严重问题时，才应使用此功能。 从还原备份到当前备份之间的最近数据将丢失。 暂存版本也将还原到旧版本。

## 使用方法

客户应提交支持票证，描述遇到的问题。 这将导致Adobe支持部门进行调查，调查人员将确定是否需要恢复。

AEM as aCloud Service支持：

* 24小时时间点恢复，这意味着系统可以在过去24小时内恢复到任何点。
* 从过去7天中每天使用一次的特定Adobe定义时间戳进行恢复。  任何复制消息（删除、更新、创建）都将保留。

在所有情况下，自定义代码版本都将从恢复点之前的上次成功部署中获取。

恢复时间目标(RTO)将因存储库的大小而异，但作为一般准则，恢复序列一旦开始，则大约需要30分钟。

恢复后，AEM版本将更新为最新版本。

**已删除环境中的数据将永久丢失，无法恢复。**
