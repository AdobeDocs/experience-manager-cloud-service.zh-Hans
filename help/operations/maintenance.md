---
title: AEM as a Cloud Service 中的维护任务
description: AEM as a Cloud Service 中的维护任务
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: cd48b78383974027d8980397632c395a5958edbf
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 4%

---

# AEM as a Cloud Service 中的维护任务

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="维护任务"
>abstract="维护任务是按计划运行以优化存储库的进程。 借助AEMas a Cloud Service，客户配置维护任务的操作属性的需求非常小。 客户可以将资源集中在应用程序级别的问题上，从而让基础架构操作Adobe。"

维护任务是按计划运行以优化存储库的进程。 借助AEMas a Cloud Service，客户配置维护任务的操作属性的需求非常小。 客户可以将资源集中在应用程序级别的问题上，从而让基础架构操作Adobe。

## 配置维护任务

在AEM的早期版本中，您可以使用维护卡（工具>操作>维护）配置维护任务。 对于AEMas a Cloud Service，维护卡不再可用，因此应将配置提交到源控件并使用Cloud Manager进行部署。 Adobe会管理那些具有客户无法配置的设置的维护任务（例如，数据存储垃圾收集、审核日志清除、版本清除）。 其他维护任务可由客户配置，如下表所述。

>[!CAUTION]
>
>Adobe保留覆盖客户维护任务配置设置以缓解性能下降等问题的权限。

下表说明了在发布AEMas a Cloud Service时可用的维护任务。

<!--| Maintenance Task | Who owns the configuration | How to configure (optional)  |
|---|---|---|
| Datastore garbage collection | Adobe | N/A - fully Adobe owned |
| Version Purge | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Audit Log Purge  | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Lucene Binaries Cleanup | Adobe | Unused and therefore disabled by Adobe. |
| Ad-hoc Task Purge | Customer | Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_TaskPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see the [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)|
| Workflow Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder`/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_WorkflowPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Project Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding a node under the node above (name it `granite_ProjectPurgeTask`) with the appropriate properties. <br> Configure OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Customers can schedule each of the Workflow Purge, Ad-hoc Task Purge and Project Purge Maintenance tasks to be executed during the daily, weekly, or monthly maintenance windows. These configurations should be edited directly in source control. The table below describes the configuration parameters available for each of the window. Also, see the locations and code samples provided after the table.-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>维护任务</th>
    <th>配置的所有者</th>
    <th>如何配置（可选）</th>
  </tr>  
  <tr>
    <td>数据存储垃圾收集</td>
    <td>Adobe</td>
    <td>不适用 — 完全Adobe拥有</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>Adobe</td>
    <td>为了使创作层保持性能， <code>/content</code> 将根据以下行为清除存储库的节点：<br><ol>
  <li>30天以上的版本将被删除</li>
  <li>过去30天中最新的5个版本将保留</li>
  <li>无论上述规则如何，都会保留最新版本。</li>
</ol><br>注意：自2022年3月14日起，上述行为将对新环境强制执行，并将于2022年4月21日对现有环境（那些是在2022年3月14日之前创建的环境）强制执行。</td>
  </td>
  </tr>
  <tr>
    <td>审核日志清除</td>
    <td>Adobe</td>
    <td>为了使创作层保持性能， <code>/content</code> 将根据以下行为清除存储库的节点：<br><ol>
  <li>对于复制审核，将删除3天以前的审核日志</li>
  <li>对于DAM（资产）审核，将删除超过30天的审核日志</li>
  <li>对于页面审核，将删除3天以前的日志。<br></li>
</ol><br>注意：自2022年3月14日起，上述行为将对新环境强制执行，并将于2022年4月21日对现有环境（那些是在2022年3月14日之前创建的环境）强制执行。</td>
   </td>
  </tr>
  <tr>
    <td>Lucene 二进制文件清理</td>
    <td>Adobe</td>
    <td>未使用，因此被Adobe禁用。</td>
  </td>
  </tr>
  <tr>
    <td>临时任务清除</td>
    <td>客户</td>
    <td>
    <p>必须在git中完成。 覆盖下的现成维护窗口配置节点 <code>/libs</code> 通过在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>.</p>
    <p>有关其他配置详细信息，请参阅下面的“维护窗口”表。 通过在上述节点下添加另一个节点（将其命名为）来启用维护任务 <code>granite_TaskPurgeTask</code>)来访问Advertising Cloud的帮助。 配置OSGI属性，请参阅 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5维护任务文档</a>.</p>
  </td>
  </tr>
    <tr>
    <td>工作流清除</td>
    <td>客户</td>
    <td>
    <p>必须在git中完成。 覆盖下的现成维护窗口配置节点 <code>/libs</code> 通过在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>. 有关其他配置详细信息，请参阅下面的“维护窗口”表。</p>
    <p>通过在上述节点下添加另一个节点（将其命名为）来启用维护任务 <code>granite_WorkflowPurgeTask</code>)来访问Advertising Cloud的帮助。 配置OSGI属性，请参阅 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5维护任务文档</a>.</p>
  </td>
  </tr>
  <tr>
    <td>项目清除</td>
    <td>客户</td>
    <td>
    <p>必须在git中完成。 覆盖下的现成维护窗口配置节点 <code>/libs</code> 通过在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>. 有关其他配置详细信息，请参阅下面的“维护窗口”表。</p>
    <p>通过在上述节点下添加另一个节点（将其命名为）来启用维护任务 <code>granite_ProjectPurgeTask</code>)来访问Advertising Cloud的帮助。 配置OSGI属性，请参阅 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5维护任务文档</a>.</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
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
  <p><strong>windowStartTime=HH:MM</strong> 用作24小时钟。 定义与每日维护窗口关联的维护任务应何时开始执行。</p>
  <p><strong>windowEndTime=HH:MM</strong> 用作24小时钟。 定义与每日维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
  </td> 
  </tr>
  <tr>
    <td>每周</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （不应更改此值）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作24小时钟。 定义与每周维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作24小时钟。 定义与每周维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
    <p><strong>windowScheduleWeekdays=1-7之间的2个值的数组(例如，[5,5])</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR节点定义</td>
    <td>
    <p><strong>windowSchedule=daily</strong> （不应更改此值）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作24小时钟。 定义与每月维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作24小时钟。 定义与每月维护窗口关联的维护任务在尚未完成时应停止执行的时间。</p>
    <p><strong>windowScheduleWeekdays=1-7之间的2个值的数组(例如，[5,5])</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别受windowStartTime和windowEndTime的约束。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0表示在当月的第一周计划，1表示在当月的最后一周计划。 如果没有值，则实际上会按照每月windowScheduleWeekdays的规定，每天计划作业。</p>
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
