---
title: AEM中的维护任务作为Cloud Service
description: 'AEM中的维护任务作为Cloud Service '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---


# AEM中的维护任务作为Cloud Service

维护任务是在计划上运行以优化存储库的进程。 以AEM为Cloud Service，客户配置维护任务的操作属性的需求非常小。 客户可以将资源集中在应用程序级别上，使基础架构操作Adobe。

有关维护任务的其他信息，请参阅以下页面：

* [AEM维护指南](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [运营仪表板维护任务](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## 配置维护任务

在AEM的先前版本中，您可以使用维护卡（“工具”>“操作”>“维护”）配置维护任务。 对于AEM作为Cloud Service，维护卡不再可用，因此应使用云管理器将配置提交到源控制并进行部署。 Adobe将管理不需要客户决策的维护任务（例如，数据存储垃圾收集），而客户可以配置其他维护任务（请参阅下表）。

>[!CAUTION]
>
>Adobe保留覆盖客户维护任务配置设置的权利，以减轻性能降低等问题。

下表说明了在发行AEM时作为Cloud Service可用的维护任务。

| 维护任务 | 配置的所有者 | 如何配置（可选） |
|---|---|---|
| 数据存储垃圾收集 | Adobe | N/A —— 完全Adobe自有 |
| 版本清除 | Adobe | 完全归Adobe所有，但在将来，客户将能够配置某些参数。 |
| 审核日志清除 | Adobe | 完全归Adobe所有，但在将来，客户将能够配置某些参数。 |
| Lucene 二进制文件清理 | Adobe | 未使用，因此由Adobe禁用。 |
| 临时任务清除 | 客户 | 必须用github完成。 <br> 通过在文件夹或下创建属性，覆盖下 `/libs` 的现成维护窗口配置节 `/apps/settings/granite/operations/maintenance/granite_weekly` 点 `granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上述节点下添加另一个节点（将其命名）并使用相 `granite_TaskPurgeTask`应的属性，启用维护任务。 <br> 配置OSGI属性，请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流清除 | 客户 | 必须用github完成。 <br> 通过在文件夹或下创建属性，覆盖下 `/libs` 的现成维护窗口配置节点`/apps/settings/granite/operations/maintenance/granite_weekly``granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上述节点下添加另一个节点（将其命名）并使用相 `granite_WorkflowPurgeTask`应的属性，启用维护任务。 <br> 配置OSGI属性，请参 [阅AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 项目清除 | 客户 | 必须用github完成。 <br> 通过在文件夹或下创建属性，覆盖下 `/libs` 的现成维护窗口配置节 `/apps/settings/granite/operations/maintenance/granite_weekly` 点 `granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上述节点（命名它）下添加具有相应属性的节 `granite_ProjectPurgeTask`点，启用维护任务。 <br> 配置OSGI属性请参 [阅AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客户可以计划要在每日、每周或每月维护窗口中执行的工作流清除、临时任务清除和项目清除维护任务。 这些配置应直接在源代码控件中进行编辑。 下表说明了每个窗口可用的配置参数。

<table>
  <tr>
    <th>维护窗口配置</th>
    <th>配置的所有者</th>
    <th>配置类型</th>
    <th>位置</th>
    <th>示例</th>
    <th>参数</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_daily </code></td>
    <td>请参见下面的代码示例1</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> =每日（不应更改此值）</li>
    <li><strong>windowStartTime</strong> = HH:MM，使用24小时。 定义与每日维护窗口关联的维护任务何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与每日维护窗口关联的维护任务在尚未完成时应停止执行的时间。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每周</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_weekly</code></td>
    <td>请参见下面的代码示例2</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（此值不应更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，使用24小时。 定义与每周维护窗口关联的维护任务何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与每周维护窗口关联的维护任务在尚未完成时应停止执行的时间。</li>
    <li><strong>windowScheduleWekdays =从1到7的2个值的数组。 例如，[5,5]。</strong> 阵列的第一个值是调度作业的开始日，第二个值是停止作业的结束日。 开始和结束的确切时间分别受windowStartTime和windowEndTime控制。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_monthly</code></td>
    <td>请参见下面的代码示例3</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> =每日（不应更改此值）</li>
    <li><strong>windowStartTime</strong> = HH:MM，使用24小时。 定义与“每月维护”窗口关联的维护任务何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与“每月维护”窗口关联的维护任务在尚未完成时应停止执行的时间。</li>
    <li><strong>windowScheduleWekdays =从1到7的2个值的数组。 例如，[5,5]。</strong> 阵列的第一个值是调度作业的开始日，第二个值是停止作业的结束日。 开始和结束的确切时间分别受windowStartTime和windowEndTime控制。</li>
    <li><strong>windowFirstLastStartDay - 0</strong> /10在月的第一周计划，或1在月的最后一周计划。 缺少值将有效地计划每天的工作，这受每月windowScheduleWekdays的约束。</li>
    </ul> </td> 
  </tr>
</table>

代码示例1

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

代码示例2

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

代码示例3

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
