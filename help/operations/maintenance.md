---
title: AEMas a Cloud Service中的维护任务
description: AEMas a Cloud Service中的维护任务
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 3e0de69033883bb77fae5be83d47167663bea3fd
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 2%

---

# AEMas a Cloud Service中的维护任务

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="维护任务"
>abstract="维护任务是按计划运行以优化存储库的进程。 借助AEMas a Cloud Service，客户配置维护任务的操作属性的需求非常小。 客户可以将资源集中在应用程序级别的问题上，从而让基础架构操作Adobe。"

维护任务是按计划运行以优化存储库的进程。 借助AEMas a Cloud Service，客户配置维护任务的操作属性的需求非常小。 客户可以将资源集中在应用程序级别的问题上，从而让基础架构操作Adobe。

## 配置维护任务

在AEM的早期版本中，您可以使用维护卡（工具>操作>维护）配置维护任务。 对于AEMas a Cloud Service，维护卡不再可用，因此应将配置提交到源控件并使用Cloud Manager进行部署。 Adobe将管理不需要客户决策的维护任务（例如，数据存储垃圾收集），而客户可以配置其他维护任务（请参阅下表）。

>[!CAUTION]
>
>Adobe保留覆盖客户维护任务配置设置以缓解性能下降等问题的权限。

下表说明了在AEMas a Cloud Service发布时可用的维护任务。

| 维护任务 | 配置的所有者 | 如何配置（可选） |
|---|---|---|
| 数据存储垃圾收集 | Adobe | 不适用 — 完全Adobe拥有 |
| 版本清除 | Adobe | 完全由Adobe拥有，但将来，客户将能够配置某些参数。 |
| 审核日志清除 | Adobe | 完全由Adobe拥有，但将来，客户将能够配置某些参数。 |
| Lucene 二进制文件清理 | Adobe | 未使用，因此被Adobe禁用。 |
| 临时任务清除 | 客户 | 必须在github中完成。 <br> 通过在文件夹或下创建属性，覆盖下 `/libs` 的现成维护窗口配 `/apps/settings/granite/operations/maintenance/granite_weekly` 置节 `granite_daily`点。有关其他配置详细信息，请参阅下面的“维护窗口”表。 <br> 通过在上面的节点（将其命名为）下添加另一个具有相应属性的节 `granite_TaskPurgeTask`点，来启用维护任务。<br> 配置OSGi属性，请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流清除 | 客户 | 必须在github中完成。 <br> 通过在文件夹下创建属性，覆盖下 `/libs` 的现成维护窗口配`/apps/settings/granite/operations/maintenance/granite_weekly` 置节 `granite_daily`点。有关其他配置详细信息，请参阅下面的“维护窗口”表。 <br> 通过在上面的节点（将其命名为）下添加另一个具有相应属性的节 `granite_WorkflowPurgeTask`点，来启用维护任务。<br> 配置OSGi属性，请参 [阅AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 项目清除 | 客户 | 必须在github中完成。 <br> 通过在文件夹或下创建属性，覆盖下 `/libs` 的现成维护窗口配 `/apps/settings/granite/operations/maintenance/granite_weekly` 置节 `granite_daily`点。有关其他配置详细信息，请参阅下面的“维护窗口”表。 <br> 通过在上述节点（将其命名为）下添加具有相应属性的节点， `granite_ProjectPurgeTask`来启用维护任务。<br> 配置OSGi属性请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客户可以安排在每日、每周或每月维护时段执行每个工作流清除、临时任务清除和项目清除维护任务。 应直接在源代码管理中编辑这些配置。 下表描述了可用于每个窗口的配置参数。 另外，请参阅表后面提供的位置和代码示例。

<table>
 <tbody>
  <tr>
    <th>维护窗口配置</th>
    <th>配置的所有者</th>
    <th>配置类型</th>
    <th>参数</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客户</td>
    <td>JCR节点定义</td>
  <td>
  <p><strong>windowSchedule=daily</strong> （不应更改此值）</p>
  <p><strong>windowStartTime=HH:</strong> 用作24小时制。定义与每日维护窗口关联的维护任务应何时开始执行。</p>
  <p><strong>windowEndTime=HH:</strong> 用作24小时制。定义与每日维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
  </td> 
  </tr>
  <tr>
    <td>每周</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （不应更改此值）</p>
    <p><strong>windowStartTime=HH:</strong> 用作24小时制。定义与每周维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:</strong> 用作24小时制。定义与每周维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
    <p><strong>windowScheduleWeekdays=1-7之间的2个值的数组(例如，[5,5])</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td>
    <p><strong>windowSchedule=daily</strong> （不应更改此值）</p>
    <p><strong>windowStartTime=HH:</strong> 用作24小时制。定义与每月维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:</strong> 用作24小时制。定义与每月维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
    <p><strong>windowScheduleWeekdays=1-7之间的2个值的数组(例如，[5,5])</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</p>
    <p><strong>windowFirstLastStartDay= 0/1 </strong> 0，用于在月的第一周进行计划，或在月的最后一周进行计划。如果没有值，则实际上会按照每月windowScheduleWeekdays的规定，每天计划作业。</p>
    </td> 
    </tr>
    </tbody>
</table>

**位置**:

* 每日 — /apps/settings/granite/operations/maintenance/granite_daily
* 每周 — /apps/settings/granite/operations/maintenance/granite_weekly
* 每月 — /apps/settings/granite/operations/maintenance/granite_monthly

**代码示例**:

代码示例1（每日）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

代码示例2（每周）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

代码示例3（每月）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```
