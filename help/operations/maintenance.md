---
title: AEM中作为云服务的维护任务
description: 'AEM中作为云服务的维护任务 '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# AEM中作为云服务的维护任务

维护任务是按计划运行以优化存储库的进程。 将AEM作为云服务，客户配置维护任务的操作属性的需求很少。 客户可以将资源集中在应用程序级别上，将基础结构操作留给Adobe。

有关维护任务的其他信息，请参阅以下页面：

* [AEM维护指南](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [操作控制板维护任务](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## 配置维护任务

在AEM的早期版本中，您可以使用维护卡（“工具”>“操作”>“维护”）配置维护任务。 对于AEM云服务，维护卡不再可用，因此应使用云管理器将配置提交到源控制并进行部署。 Adobe将管理不需要客户决策的维护任务（例如，Datastore Garbage Collection），而客户可以配置其他维护任务（请参阅下表）。

>[!CAUTION]
>
>Adobe保留覆盖客户的维护任务配置设置以减轻性能降级等问题的权利。

下表说明了在AEM发布时作为云服务可用的维护任务。

| 维护任务 | 谁拥有配置 | 如何配置（可选） |
|---|---|---|
| 数据存储垃圾收集 | Adobe | 无——完全由Adobe拥有 |
| 版本清除 | Adobe | 完全归Adobe所有，但客户将来能够配置某些参数。 |
| 审核日志清除 | Adobe | 完全归Adobe所有，但客户将来能够配置某些参数。 |
| Lucene 二进制文件清理 | Adobe | 未使用，因此Adobe禁用。 |
| 临时任务清除 | 客户 | 必须用github完成。 <br> 使用或覆盖维护窗口配 `/libs` 置节 `/apps` 点 `/conf/global/settings/granite/operations/maintenance/granite_weekly` 和节点 `granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上面的节点下添加另一个节点（将其命名）并使用相应的 `granite_TaskPurgeTask`属性来启用维护任务。 <br> 配置OSGI属性，请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流清除 | 客户 | 必须用github完成。 <br> 使用或覆盖维护窗口配 `/libs` 置节 `/apps` 点 `/conf/global/settings/granite/operations/maintenance/granite_weekly` 和节点 `granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上面的节点下添加另一个节点（将其命名）并使用相应的 `granite_WorkflowPurgeTask`属性来启用维护任务。 <br> 配置OSGI属性，请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 项目清除 | 客户 | 必须用github完成。 <br> 使用或覆盖维护窗口配 `/libs` 置节 `/apps` 点 `/conf/global/settings/granite/operations/maintenance/granite_weekly` 和节点 `granite_daily`。 有关其他配置详细信息，请参阅下面的维护窗口表。 <br> 通过在上面的节点下添加一个节点（将其命名）并使用相应的属 `granite_ProjectPurgeTask`性来启用维护任务。 <br> 配置OSGI属性，请参阅 [AEM 6.5维护任务文档](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客户可以计划在每日、每周或每月维护窗口期间执行的每个工作流清除、临时任务清除和项目清除维护任务。 这些配置应直接在源控件中编辑。 下表描述了每个窗口可用的配置参数。

<table>
  <tr>
    <th>维护窗口配置</th>
    <th>谁拥有配置</th>
    <th>配置类型</th>
    <th>位置</th>
    <th>示例</th>
    <th>参数</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_daily </code> (它将覆盖和中的 <code>/apps</code> 节点 <code>/libs</code>)</td>
    <td>请参见下面的代码示例1</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（此值不应更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小时钟。 定义与“每日维护”窗口关联的“维护任务”何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与每日维护窗口关联的维护任务在尚未完成时应停止执行的时间。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每周</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code> (它将覆盖和中的 <code>/apps</code> 节点 <code>/libs</code>)</td>
    <td>请参见下面的代码示例2</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（此值不应更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小时钟。 定义与每周维护窗口关联的维护任务何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与每周维护窗口关联的维护任务在尚未完成时应停止执行的时间。</li>
    <li><strong>windowScheduleWeekdays =由2个值组成的数组，范围从1-7。 例如，[5,5]。</strong> 数组的第一个值是调度作业的开始日，第二个值是将停止作业的结束日。 开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_monthly</code> (它将覆盖和中的 <code>/apps</code> 节点 <code>/libs</code>)</td>
    <td>请参见下面的代码示例3</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（此值不应更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小时钟。 定义与“每月维护”窗口关联的“维护任务”何时开始执行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，使用24小时。 定义与“每月维护”窗口关联的“维护任务”在尚未完成时应停止执行的时间。</li>
    <li><strong>windowScheduleWeekdays =由2个值组成的数组，范围从1-7。 例如，[5,5]。</strong> 数组的第一个值是调度作业的开始日，第二个值是将停止作业的结束日。 开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0，在月的第一周预定，或在月的最后一周预定。 如果没有值，将有效地安排每月的工作，并受每月windowScheduleWeekdays的约束。</li>
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
